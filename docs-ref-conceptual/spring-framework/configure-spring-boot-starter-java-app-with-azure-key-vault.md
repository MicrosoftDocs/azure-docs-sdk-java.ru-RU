---
title: "Как использовать начальное приложение Spring Boot Starter с Azure Key Vault"
description: "Сведения о настройке приложения Spring Boot Initializer с помощью начального приложения Azure Key Vault."
services: key-vault
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
ms.assetid: 
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: multiple
ms.devlang: java
ms.topic: article
ms.date: 11/29/2017
ms.author: robmcm
ms.openlocfilehash: 8b35a972a00c995730dfa59b1b6a47fab7716b76
ms.sourcegitcommit: fc48e038721e6910cb8b1f8951df765d517e504d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/06/2017
---
# <a name="how-to-use-the-spring-boot-starter-for-azure-key-vault"></a><span data-ttu-id="9ba94-103">Как использовать начальное приложение Spring Boot Starter с Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="9ba94-103">How to use the Spring Boot Starter for Azure Key Vault</span></span>

## <a name="overview"></a><span data-ttu-id="9ba94-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="9ba94-104">Overview</span></span>

<span data-ttu-id="9ba94-105">В этой статье описано, как создать с помощью **[Spring Initializr]** начальное приложение Spring Boot для Azure Key Vault для получения строки подключения, которая хранится в виде секрета в хранилище ключей.</span><span class="sxs-lookup"><span data-stu-id="9ba94-105">This article demonstrates creating an app with the **[Spring Initializr]** which uses the Spring Boot Starter for Azure Key Vault to retrieve a connection string that is stored as a secret in a key vault.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9ba94-106">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="9ba94-106">Prerequisites</span></span>

<span data-ttu-id="9ba94-107">Чтобы выполнить действия, описанные в этой статье, необходимо иметь следующие компоненты:</span><span class="sxs-lookup"><span data-stu-id="9ba94-107">The following prerequisites are required in order to follow the steps in this article:</span></span>

* <span data-ttu-id="9ba94-108">Подписка Azure; если у вас еще нет подписки Azure, вы можете активировать [преимущества для подписчиков MSDN] или зарегистрироваться для получения [бесплатной учетной записи Azure].</span><span class="sxs-lookup"><span data-stu-id="9ba94-108">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="9ba94-109">[Пакет разработчиков Java (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/) версии 1.7 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="9ba94-109">A [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), version 1.7 or later.</span></span>
* <span data-ttu-id="9ba94-110">[Apache Maven](http://maven.apache.org/) версии 3.0 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="9ba94-110">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>

## <a name="create-an-app-using-the-spring-initialzr"></a><span data-ttu-id="9ba94-111">Создание приложения с помощью Spring Initialzr</span><span class="sxs-lookup"><span data-stu-id="9ba94-111">Create an app using the Spring Initialzr</span></span>

1. <span data-ttu-id="9ba94-112">Перейдите по адресу <https://start.spring.io/>.</span><span class="sxs-lookup"><span data-stu-id="9ba94-112">Browse to <https://start.spring.io/>.</span></span>

1. <span data-ttu-id="9ba94-113">Укажите, что необходимо создать проект **Maven** с помощью **Java**, введите имя **группы** и **артефакта** вашего приложения, а затем щелкните ссылку, чтобы **перейти к полной версии** Spring Initializr.</span><span class="sxs-lookup"><span data-stu-id="9ba94-113">Specify that you want to generate a **Maven** project with **Java**, enter the **Group** and **Aritifact** names for your application, and then click the link to **Switch to the full version** of the Spring Initializr.</span></span>

   ![Указание имен группы и артефакта][secrets-01]

1. <span data-ttu-id="9ba94-115">Прокрутите вниз до раздела **Azure** статьи и установите флажок рядом с пунктом **Azure Key Vault**.</span><span class="sxs-lookup"><span data-stu-id="9ba94-115">Scroll down to the **Azure** section and check the box for **Azure Key Vault**.</span></span>

   ![Выбор начального приложения Azure Key Vault][secrets-02]

1. <span data-ttu-id="9ba94-117">Прокрутите страницу вниз и нажмите кнопку, чтобы **создать проект**.</span><span class="sxs-lookup"><span data-stu-id="9ba94-117">Scroll to the bottom of the page and click the button to **Generate Project**.</span></span>

   ![Создание проекта Spring Boot][secrets-03]

1. <span data-ttu-id="9ba94-119">При появлении запроса скачайте проект на локальный компьютер.</span><span class="sxs-lookup"><span data-stu-id="9ba94-119">When prompted, download the project to a path on your local computer.</span></span>

## <a name="sign-into-azure-and-select-the-subscription-to-use"></a><span data-ttu-id="9ba94-120">Вход в Azure и выбор подписки для использования</span><span class="sxs-lookup"><span data-stu-id="9ba94-120">Sign into Azure and select the subscription to use</span></span>

1. <span data-ttu-id="9ba94-121">Откройте окно командной строки.</span><span class="sxs-lookup"><span data-stu-id="9ba94-121">Open a command prompt.</span></span>

1. <span data-ttu-id="9ba94-122">Войдите в учетную запись Azure с помощью интерфейса командной строки Azure.</span><span class="sxs-lookup"><span data-stu-id="9ba94-122">Sign into your Azure account by using the Azure CLI:</span></span>

   ```azurecli
   az login
   ```
   <span data-ttu-id="9ba94-123">Для завершения процесса входа следуйте инструкциям.</span><span class="sxs-lookup"><span data-stu-id="9ba94-123">Follow the instructions to complete the sign-in process.</span></span>

1. <span data-ttu-id="9ba94-124">Отобразите список подписок:</span><span class="sxs-lookup"><span data-stu-id="9ba94-124">List your subscriptions:</span></span>

   ```azurecli
   az account list
   ```
   <span data-ttu-id="9ba94-125">Azure отобразит список подписок, и вам нужно будет скопировать идентификатор GUID для подписки, которая будет использоваться, например:</span><span class="sxs-lookup"><span data-stu-id="9ba94-125">Azure will return a list of your subscriptions, and you will need to copy the GUID for the subscription that you want to use; for example:</span></span>

   ```json
   [
     {
       "cloudName": "AzureCloud",
       "id": "ssssssss-ssss-ssss-ssss-ssssssssssss",
       "isDefault": true,
       "name": "Converted Windows Azure MSDN - Visual Studio Ultimate",
       "state": "Enabled",
       "tenantId": "tttttttt-tttt-tttt-tttt-tttttttttttt",
       "user": {
         "name": "contoso@microsoft.com",
         "type": "user"
       }
     }
   ]

1. Specify the GUID for the account you want to use with Azure; for example:

   ```azurecli
   az account set -s ssssssss-ssss-ssss-ssss-ssssssssssss
   ```

## <a name="create-and-configure-a-new-azure-key-vault-using-the-azure-cli"></a><span data-ttu-id="9ba94-126">Создание и настройка Azure Key Vault с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="9ba94-126">Create and configure a new Azure Key Vault using the Azure CLI</span></span>

1. <span data-ttu-id="9ba94-127">Создайте группу ресурсов Azure, которые будут использоваться для хранилища ключей, например:</span><span class="sxs-lookup"><span data-stu-id="9ba94-127">Create a resource group for the Azure resources you will use for your key vault; for example:</span></span>
   ```azurecli
   az group create --name wingtiptoysresources --location westus
   ```
   <span data-ttu-id="9ba94-128">Описание</span><span class="sxs-lookup"><span data-stu-id="9ba94-128">Where:</span></span>
   | <span data-ttu-id="9ba94-129">Параметр</span><span class="sxs-lookup"><span data-stu-id="9ba94-129">Parameter</span></span> | <span data-ttu-id="9ba94-130">Описание</span><span class="sxs-lookup"><span data-stu-id="9ba94-130">Description</span></span> |
   |---|---|
   | `name` | <span data-ttu-id="9ba94-131">Указывает уникальное имя для группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="9ba94-131">Specifies a unique name for your resource group.</span></span> |
   | `location` | <span data-ttu-id="9ba94-132">Указывает [регион Azure](https://azure.microsoft.com/regions/) для размещения группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="9ba94-132">Specifies the [Azure region](https://azure.microsoft.com/regions/) where your resource group will be hosted.</span></span> |

   <span data-ttu-id="9ba94-133">В Azure CLI отобразятся результаты созданной группы ресурсов, например:</span><span class="sxs-lookup"><span data-stu-id="9ba94-133">The Azure CLI will display the results of your resource group creation; for example:</span></span>  

   ```json
   {
     "id": "/subscriptions/ssssssss-ssss-ssss-ssss-ssssssssssss/resourceGroups/wingtiptoysresources",
     "location": "westus",
     "managedBy": null,
     "name": "wingtiptoysresources",
     "properties": {
       "provisioningState": "Succeeded"
     },
     "tags": null
   }
   ```

1. <span data-ttu-id="9ba94-134">Создайте субъект-службу Azure, связанный с зарегистрированным приложением, например:</span><span class="sxs-lookup"><span data-stu-id="9ba94-134">Create an Azure service principal from your application registration; for example:</span></span>
   ```shell
   az ad sp create-for-rbac --name "wingtiptoysuser"
   ```
   | <span data-ttu-id="9ba94-135">Параметр</span><span class="sxs-lookup"><span data-stu-id="9ba94-135">Parameter</span></span> | <span data-ttu-id="9ba94-136">Описание</span><span class="sxs-lookup"><span data-stu-id="9ba94-136">Description</span></span> |
   |---|---|
   | `id` | <span data-ttu-id="9ba94-137">Указывает идентификатор GUID из предыдущего зарегистрированного приложения.</span><span class="sxs-lookup"><span data-stu-id="9ba94-137">Specifies the GUID from your application registration earlier.</span></span> |

   <span data-ttu-id="9ba94-138">Azure CLI отобразит сообщение о состоянии JSON, которое содержит значения *appId* и *password* (вы будете использовать эти значения в качестве идентификатора клиента и пароля клиента позже), например:</span><span class="sxs-lookup"><span data-stu-id="9ba94-138">The Azure CLI will return a JSON status message that contains the *appId* and *password*, which you will use later as the client id and client password; for example:</span></span>

   ```json
   {
     "appId": "iiiiiiii-iiii-iiii-iiii-iiiiiiiiiiii",
     "displayName": "wingtiptoysuser",
     "name": "http://wingtiptoysuser",
     "password": "pppppppp-pppp-pppp-pppp-pppppppppppp",
     "tenant": "tttttttt-tttt-tttt-tttt-tttttttttttt"
   }
   ```

1. <span data-ttu-id="9ba94-139">Создайте хранилище ключей в группе ресурсов, например:</span><span class="sxs-lookup"><span data-stu-id="9ba94-139">Create a new key vault in the resource group; for example:</span></span>
   ```azurecli
   az keyvault create --name wingtiptoyskeyvault --resource-group wingtiptoysresources --location westus --enabled-for-deployment true --enabled-for-disk-encryption true --enabled-for-template-deployment true --sku standard --query properties.vaultUri
   ```
   <span data-ttu-id="9ba94-140">Описание</span><span class="sxs-lookup"><span data-stu-id="9ba94-140">Where:</span></span>
   | <span data-ttu-id="9ba94-141">Параметр</span><span class="sxs-lookup"><span data-stu-id="9ba94-141">Parameter</span></span> | <span data-ttu-id="9ba94-142">Описание</span><span class="sxs-lookup"><span data-stu-id="9ba94-142">Description</span></span> |
   |---|---|
   | `name` | <span data-ttu-id="9ba94-143">Указывает уникальное имя для хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="9ba94-143">Specifies a unique name for your key vault.</span></span> |
   | `location` | <span data-ttu-id="9ba94-144">Указывает [регион Azure](https://azure.microsoft.com/regions/) для размещения группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="9ba94-144">Specifies the [Azure region](https://azure.microsoft.com/regions/) where your resource group will be hosted.</span></span> |
   | `enabled-for-deployment` | <span data-ttu-id="9ba94-145">Указывает [вариант развертывания хранилища ключей](https://docs.microsoft.com/en-us/cli/azure/keyvault).</span><span class="sxs-lookup"><span data-stu-id="9ba94-145">Specifies the [key vault deployment option](https://docs.microsoft.com/en-us/cli/azure/keyvault).</span></span> |
   | `enabled-for-disk-encryption` | <span data-ttu-id="9ba94-146">Указывает [вариант шифрования хранилища ключей](https://docs.microsoft.com/en-us/cli/azure/keyvault).</span><span class="sxs-lookup"><span data-stu-id="9ba94-146">Specifies the [key vault encryption option](https://docs.microsoft.com/en-us/cli/azure/keyvault).</span></span> |
   | `enabled-for-template-deployment` | <span data-ttu-id="9ba94-147">Указывает [вариант шифрования хранилища ключей](https://docs.microsoft.com/en-us/cli/azure/keyvault).</span><span class="sxs-lookup"><span data-stu-id="9ba94-147">Specifies the [key vault encryption option](https://docs.microsoft.com/en-us/cli/azure/keyvault).</span></span> |
   | `sku` | <span data-ttu-id="9ba94-148">Указывает [вариант номера SKU хранилища ключей](https://docs.microsoft.com/en-us/cli/azure/keyvault).</span><span class="sxs-lookup"><span data-stu-id="9ba94-148">Specifies the [key vault SKU option](https://docs.microsoft.com/en-us/cli/azure/keyvault).</span></span> |
   | `query` | <span data-ttu-id="9ba94-149">Указывает значение, извлекаемое из ответа — URI хранилища ключей, необходимый для работы с этим руководством.</span><span class="sxs-lookup"><span data-stu-id="9ba94-149">Specifies a value to retrieve from the response, which is the key vault URI that you will need to complete this tutorial.</span></span> |

   <span data-ttu-id="9ba94-150">Azure CLI отобразит этот URI для хранилища ключей для дальнейшего использования, например:</span><span class="sxs-lookup"><span data-stu-id="9ba94-150">The Azure CLI will display the URI for key vault, which you will use later; for example:</span></span>  

   ```
   "https://wingtiptoyskeyvault.vault.azure.net"
   ```

1. <span data-ttu-id="9ba94-151">Настройте политику доступа для ранее созданного субъекта-службы Azure, например:</span><span class="sxs-lookup"><span data-stu-id="9ba94-151">Set the access policy for the Azure service principal you created earlier; for example:</span></span>
   ```azurecli
   az keyvault set-policy --name wingtiptoyskeyvault --secret-permission set get list delete --spn "iiiiiiii-iiii-iiii-iiii-iiiiiiiiiiii"
   ```
   <span data-ttu-id="9ba94-152">Описание</span><span class="sxs-lookup"><span data-stu-id="9ba94-152">Where:</span></span>
   | <span data-ttu-id="9ba94-153">Параметр</span><span class="sxs-lookup"><span data-stu-id="9ba94-153">Parameter</span></span> | <span data-ttu-id="9ba94-154">Описание</span><span class="sxs-lookup"><span data-stu-id="9ba94-154">Description</span></span> |
   |---|---|
   | `name` | <span data-ttu-id="9ba94-155">Указывает имя используемого хранилища ключей (см. выше).</span><span class="sxs-lookup"><span data-stu-id="9ba94-155">Specifies your key vault name from earlier.</span></span> |
   | `secret-permission` | <span data-ttu-id="9ba94-156">Указывает [политики безопасности](https://docs.microsoft.com/en-us/cli/azure/keyvault) для хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="9ba94-156">Specifies the [security policies](https://docs.microsoft.com/en-us/cli/azure/keyvault) for your key vault.</span></span> |
   | `object-id` | <span data-ttu-id="9ba94-157">Указывает идентификатор GUID для зарегистрированного приложения (см. выше).</span><span class="sxs-lookup"><span data-stu-id="9ba94-157">Specifies the GUID for your application registration from earlier.</span></span> |

   <span data-ttu-id="9ba94-158">В Azure CLI отобразятся результаты создания политики безопасности, например:</span><span class="sxs-lookup"><span data-stu-id="9ba94-158">The Azure CLI will display the results of your security policy creation; for example:</span></span>  

   ```json
   {
     "id": "/subscriptions/ssssssss-ssss-ssss-ssss-ssssssssssss/...",
     "location": "westus",
     "name": "wingtiptoyskeyvault",
     "properties": {
       ...
       ... (A long list of values will be displayed here.)
       ...
     },
     "resourceGroup": "wingtiptoysresources",
     "tags": {},
     "type": "Microsoft.KeyVault/vaults"
   }
   ```

1. <span data-ttu-id="9ba94-159">Сохраните секрет в новом хранилище ключей, например:</span><span class="sxs-lookup"><span data-stu-id="9ba94-159">Store a secret in your new key vault; for example:</span></span>
   ```azurecli
   az keyvault secret set --vault-name "wingtiptoyskeyvault" --name "connectionString" --value "jdbc:sqlserver://SERVER.database.windows.net:1433;database=DATABASE;"
   ```
   <span data-ttu-id="9ba94-160">Описание</span><span class="sxs-lookup"><span data-stu-id="9ba94-160">Where:</span></span>
   | <span data-ttu-id="9ba94-161">Параметр</span><span class="sxs-lookup"><span data-stu-id="9ba94-161">Parameter</span></span> | <span data-ttu-id="9ba94-162">Описание</span><span class="sxs-lookup"><span data-stu-id="9ba94-162">Description</span></span> |
   |---|---|
   | `vault-name` | <span data-ttu-id="9ba94-163">Указывает имя используемого хранилища ключей (см. выше).</span><span class="sxs-lookup"><span data-stu-id="9ba94-163">Specifies your key vault name from earlier.</span></span> |
   | `name` | <span data-ttu-id="9ba94-164">Указывает имя секрета.</span><span class="sxs-lookup"><span data-stu-id="9ba94-164">Specifies the name of your secret.</span></span> |
   | `value` | <span data-ttu-id="9ba94-165">Указывает значение секрета.</span><span class="sxs-lookup"><span data-stu-id="9ba94-165">Specifies the value of your secret.</span></span> |

   <span data-ttu-id="9ba94-166">В Azure CLI отобразятся результаты создания секрета, например:</span><span class="sxs-lookup"><span data-stu-id="9ba94-166">The Azure CLI will display the results of your secret creation; for example:</span></span>  

   ```json
   {
     "attributes": {
       "created": "2017-12-01T09:00:16+00:00",
       "enabled": true,
       "expires": null,
       "notBefore": null,
       "recoveryLevel": "Purgeable",
       "updated": "2017-12-01T09:00:16+00:00"
     },
     "contentType": null,
     "id": "https://wingtiptoyskeyvault.vault.azure.net/secrets/connectionString/123456789abcdef123456789abcdef",
     "kid": null,
     "managed": null,
     "tags": {
       "file-encoding": "utf-8"
     },
     "value": "jdbc:sqlserver://wingtiptoys.database.windows.net:1433;database=DATABASE;"
   }
   ```

## <a name="configure-and-compile-your-spring-boot-application"></a><span data-ttu-id="9ba94-167">Настройка и компиляция приложения Spring Boot</span><span class="sxs-lookup"><span data-stu-id="9ba94-167">Configure and compile your Spring Boot application</span></span>

1. <span data-ttu-id="9ba94-168">Распакуйте архив с файлами проекта Spring Boot, которые вы скачали в каталог.</span><span class="sxs-lookup"><span data-stu-id="9ba94-168">Extract the files from the Spring Boot project archive files that you downloaded earlier into a directory.</span></span>

1. <span data-ttu-id="9ba94-169">В папке *main/src/ресурсы* проекта откройте файл *application.properties* в текстовом редакторе.</span><span class="sxs-lookup"><span data-stu-id="9ba94-169">Navigate to the *src/main/resources* folder in your project and open the *application.properties* file in a text editor.</span></span>

1. <span data-ttu-id="9ba94-170">Добавьте значения для хранилища ключей, используя ранее выполненные действия, например:</span><span class="sxs-lookup"><span data-stu-id="9ba94-170">Add the values for your key vault using values from the steps that you completed earlier in this tutorial; for example:</span></span>
   ```yaml
   azure.keyvault.uri=https://wingtiptoyskeyvault.vault.azure.net/
   azure.keyvault.client-id=iiiiiiii-iiii-iiii-iiii-iiiiiiiiiiii
   azure.keyvault.client-key=pppppppp-pppp-pppp-pppp-pppppppppppp
   ```
   <span data-ttu-id="9ba94-171">Описание</span><span class="sxs-lookup"><span data-stu-id="9ba94-171">Where:</span></span>
   | <span data-ttu-id="9ba94-172">Параметр</span><span class="sxs-lookup"><span data-stu-id="9ba94-172">Parameter</span></span> | <span data-ttu-id="9ba94-173">Описание</span><span class="sxs-lookup"><span data-stu-id="9ba94-173">Description</span></span> |
   |---|---|
   | `azure.keyvault.uri` | <span data-ttu-id="9ba94-174">Указывает URI, полученный при создании хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="9ba94-174">Specifies the URI from when you created your key vault.</span></span> |
   | `azure.keyvault.client-id` | <span data-ttu-id="9ba94-175">Указывает GUID *appId*, полученный при создании субъекта-службы.</span><span class="sxs-lookup"><span data-stu-id="9ba94-175">Specifies the *appId* GUID from when you created your service principal.</span></span> |
   | `azure.keyvault.client-key` | <span data-ttu-id="9ba94-176">Указывает GUID *password*, полученный при создании субъекта-службы.</span><span class="sxs-lookup"><span data-stu-id="9ba94-176">Specifies the *password* GUID from when you created your service principal.</span></span> |

1. <span data-ttu-id="9ba94-177">Перейдите к файлу с основным кодом проекта, например: */src/main/java/com/wingtiptoys/secrets*.</span><span class="sxs-lookup"><span data-stu-id="9ba94-177">Navigate to the main source code file of your project; for example: */src/main/java/com/wingtiptoys/secrets*.</span></span>

1. <span data-ttu-id="9ba94-178">Откройте в текстовом редакторе основной файл Java приложения, например: *SecretsApplication.java*. Добавьте следующие строки в файл:</span><span class="sxs-lookup"><span data-stu-id="9ba94-178">Open the application's main Java file in a file in a text editor; for example: *SecretsApplication.java*, and add the following lines to the file:</span></span>

   ```java
   package com.wingtiptoys.secrets;

   import org.springframework.boot.SpringApplication;
   import org.springframework.boot.autoconfigure.SpringBootApplication;
   import org.springframework.beans.factory.annotation.Value;
   import org.springframework.boot.CommandLineRunner;

   @SpringBootApplication
   public class SecretsApplication implements CommandLineRunner {

      @Value("${connectionString}")
      private String connectionString;

      public static void main(String[] args) {
         SpringApplication.run(SecretsApplication.class, args);
      }

      public void run(String... varl) throws Exception {
         System.out.println(String.format("\nConnection String stored in Azure Key Vault:\n%s\n",connectionString));
      }
   }
   ```
   <span data-ttu-id="9ba94-179">Этот пример кода извлекает строку подключения из хранилища ключей и отображает ее в командной строке.</span><span class="sxs-lookup"><span data-stu-id="9ba94-179">This code example retrieves the connection string from the key vault and displays it to the command line.</span></span>

1. <span data-ttu-id="9ba94-180">Сохраните и закройте файл Java.</span><span class="sxs-lookup"><span data-stu-id="9ba94-180">Save and close the Java file.</span></span>

## <a name="build-and-test-your-app"></a><span data-ttu-id="9ba94-181">Создание и тестирование приложения</span><span class="sxs-lookup"><span data-stu-id="9ba94-181">Build and test your app</span></span>

1. <span data-ttu-id="9ba94-182">Перейдите в каталог с файлом *pom.xml* приложения Spring Boot:</span><span class="sxs-lookup"><span data-stu-id="9ba94-182">Navigate to the directory where the *pom.xml* file for your Spring Boot app is located:</span></span>

1. <span data-ttu-id="9ba94-183">Создайте приложение Spring Boot с помощью Maven, например:</span><span class="sxs-lookup"><span data-stu-id="9ba94-183">Build your Spring Boot application with Maven; for example:</span></span>

   ```bash
   mvn clean package
   ```

   <span data-ttu-id="9ba94-184">В Maven отобразятся результаты создания.</span><span class="sxs-lookup"><span data-stu-id="9ba94-184">Maven will display the results of your build.</span></span>

   ![Состояние сборки приложения Spring Boot][build-application-01]

1. <span data-ttu-id="9ba94-186">Запустите приложение Spring Boot с помощью Maven. В приложении отобразится строка подключения, полученная из хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="9ba94-186">Run your Spring Boot application with Maven; the application will display the connection string from your key vault.</span></span> <span data-ttu-id="9ba94-187">Например:</span><span class="sxs-lookup"><span data-stu-id="9ba94-187">For example:</span></span>

   ```bash
   mvn spring-boot:run
   ```

   ![Сообщение о времени выполнения Spring Boot][build-application-02]

## <a name="next-steps"></a><span data-ttu-id="9ba94-189">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9ba94-189">Next steps</span></span>

<span data-ttu-id="9ba94-190">См. дополнительные сведения об использовании Azure Key Vault:</span><span class="sxs-lookup"><span data-stu-id="9ba94-190">For more information about using Azure Key Vaults, see the following articles:</span></span>

* <span data-ttu-id="9ba94-191">[Документация по Key Vault].</span><span class="sxs-lookup"><span data-stu-id="9ba94-191">[Key Vault Documentation].</span></span>

* <span data-ttu-id="9ba94-192">[Приступая к работе с хранилищем ключей Azure]</span><span class="sxs-lookup"><span data-stu-id="9ba94-192">[Get started with Azure Key Vault]</span></span>

<span data-ttu-id="9ba94-193">Дополнительные сведения об использовании приложений Spring Boot в Azure см. в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="9ba94-193">For more information about using Spring Boot applications on Azure, see the following articles:</span></span>

* [<span data-ttu-id="9ba94-194">Развертывание приложения Spring Boot Application в службе приложений Azure</span><span class="sxs-lookup"><span data-stu-id="9ba94-194">Deploy a Spring Boot Application to the Azure App Service</span></span>](deploy-spring-boot-java-web-app-on-azure.md)

* [<span data-ttu-id="9ba94-195">Запуск приложения Spring Boot в кластере Kubernetes в Службе контейнеров Azure</span><span class="sxs-lookup"><span data-stu-id="9ba94-195">Running a Spring Boot Application on a Kubernetes Cluster in the Azure Container Service</span></span>](deploy-spring-boot-java-app-on-kubernetes.md)

<span data-ttu-id="9ba94-196">Дополнительные сведения об использовании Azure с Java см. в руководствах по [Azure для разработчиков Java] и [инструментах Java для Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="9ba94-196">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Java Tools for Visual Studio Team Services].</span></span>

<!-- URL List -->

[Документация по Key Vault]: /azure/key-vault/
[Приступая к работе с хранилищем ключей Azure]: /azure/key-vault/key-vault-get-started
[Azure для разработчиков Java]: https://docs.microsoft.com/java/azure/
[бесплатной учетной записи Azure]: https://azure.microsoft.com/pricing/free-trial/
[инструментах Java для Visual Studio Team Services]: https://java.visualstudio.com/ (Инструменты Java для Visual Studio Team Services)
[преимущества для подписчиков MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Initializr]: https://start.spring.io/
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[secrets-01]: media/configure-spring-boot-starter-java-app-with-azure-key-vault/secrets-01.png
[secrets-02]: media/configure-spring-boot-starter-java-app-with-azure-key-vault/secrets-02.png
[secrets-03]: media/configure-spring-boot-starter-java-app-with-azure-key-vault/secrets-03.png

[build-application-01]: media/configure-spring-boot-starter-java-app-with-azure-key-vault/build-application-01.png
[build-application-02]: media/configure-spring-boot-starter-java-app-with-azure-key-vault/build-application-02.png