---
title: Как использовать начальное приложение Spring Boot Starter с Azure Key Vault
description: Сведения о настройке приложения Spring Boot Initializer с помощью начального приложения Azure Key Vault.
services: key-vault
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 02/01/2018
ms.devlang: java
ms.service: key-vault
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: identity
ms.openlocfilehash: a2734fc08f2f59f64ba6c6c20ff18d75070b68d5
ms.sourcegitcommit: 5282a51bf31771671df01af5814df1d2b8e4620c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/28/2018
ms.locfileid: "37090717"
---
# <a name="how-to-use-the-spring-boot-starter-for-azure-key-vault"></a><span data-ttu-id="4b847-103">Как использовать начальное приложение Spring Boot Starter с Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="4b847-103">How to use the Spring Boot Starter for Azure Key Vault</span></span>

## <a name="overview"></a><span data-ttu-id="4b847-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="4b847-104">Overview</span></span>

<span data-ttu-id="4b847-105">В этой статье описано, как создать с помощью **[Spring Initializr]** начальное приложение Spring Boot для Azure Key Vault для получения строки подключения, которая хранится в виде секрета в хранилище ключей.</span><span class="sxs-lookup"><span data-stu-id="4b847-105">This article demonstrates creating an app with the **[Spring Initializr]** that uses the Spring Boot Starter for Azure Key Vault to retrieve a connection string that is stored as a secret in a key vault.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4b847-106">предварительным требованиям</span><span class="sxs-lookup"><span data-stu-id="4b847-106">Prerequisites</span></span>

<span data-ttu-id="4b847-107">Чтобы выполнить действия, описанные в этой статье, необходимо следующее:</span><span class="sxs-lookup"><span data-stu-id="4b847-107">The following prerequisites are required in order to complete the steps in this article:</span></span>

* <span data-ttu-id="4b847-108">Подписка Azure. Если у вас ее еще нет, вы можете активировать [преимущества для подписчиков MSDN] или зарегистрироваться для получения [бесплатной учетной записи Azure].</span><span class="sxs-lookup"><span data-stu-id="4b847-108">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="4b847-109">[Пакет разработчиков Java (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/) версии 1.7 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="4b847-109">A [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), version 1.7 or later.</span></span>
* <span data-ttu-id="4b847-110">[Apache Maven](http://maven.apache.org/) версии 3.0 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="4b847-110">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>

## <a name="create-an-app-using-the-spring-initialzr"></a><span data-ttu-id="4b847-111">Создание приложения с помощью Spring Initialzr</span><span class="sxs-lookup"><span data-stu-id="4b847-111">Create an app using the Spring Initialzr</span></span>

1. <span data-ttu-id="4b847-112">Перейдите по адресу <https://start.spring.io/>.</span><span class="sxs-lookup"><span data-stu-id="4b847-112">Browse to <https://start.spring.io/>.</span></span>

1. <span data-ttu-id="4b847-113">Укажите, что необходимо создать проект **Maven** с помощью **Java**, введите имя **группы** и **артефакта** вашего приложения, а затем щелкните ссылку, чтобы **перейти к полной версии** Spring Initializr.</span><span class="sxs-lookup"><span data-stu-id="4b847-113">Specify that you want to generate a **Maven** project with **Java**, enter the **Group** and **Aritifact** names for your application, and then click the link to **Switch to the full version** of the Spring Initializr.</span></span>

   ![Указание имен группы и артефакта][secrets-01]

1. <span data-ttu-id="4b847-115">Прокрутите вниз до раздела **Azure** статьи и установите флажок рядом с пунктом **Azure Key Vault**.</span><span class="sxs-lookup"><span data-stu-id="4b847-115">Scroll down to the **Azure** section and check the box for **Azure Key Vault**.</span></span>

   ![Выбор начального приложения Azure Key Vault][secrets-02]

1. <span data-ttu-id="4b847-117">Прокрутите страницу вниз и нажмите кнопку, чтобы **создать проект**.</span><span class="sxs-lookup"><span data-stu-id="4b847-117">Scroll to the bottom of the page and click the button to **Generate Project**.</span></span>

   ![Создание проекта Spring Boot][secrets-03]

1. <span data-ttu-id="4b847-119">При появлении запроса скачайте проект на локальный компьютер.</span><span class="sxs-lookup"><span data-stu-id="4b847-119">When prompted, download the project to a path on your local computer.</span></span>

## <a name="sign-into-azure-and-select-the-subscription-to-use"></a><span data-ttu-id="4b847-120">Вход в Azure и выбор подписки для использования</span><span class="sxs-lookup"><span data-stu-id="4b847-120">Sign into Azure and select the subscription to use</span></span>

1. <span data-ttu-id="4b847-121">Откройте окно командной строки.</span><span class="sxs-lookup"><span data-stu-id="4b847-121">Open a command prompt.</span></span>

1. <span data-ttu-id="4b847-122">Войдите в учетную запись Azure с помощью интерфейса командной строки Azure.</span><span class="sxs-lookup"><span data-stu-id="4b847-122">Sign into your Azure account by using the Azure CLI:</span></span>

   ```azurecli
   az login
   ```
   <span data-ttu-id="4b847-123">Для завершения процесса входа следуйте инструкциям.</span><span class="sxs-lookup"><span data-stu-id="4b847-123">Follow the instructions to complete the sign-in process.</span></span>

1. <span data-ttu-id="4b847-124">Отобразите список подписок:</span><span class="sxs-lookup"><span data-stu-id="4b847-124">List your subscriptions:</span></span>

   ```azurecli
   az account list
   ```
   <span data-ttu-id="4b847-125">Azure отобразит список подписок, и вам нужно будет скопировать идентификатор GUID для подписки, которая будет использоваться, например:</span><span class="sxs-lookup"><span data-stu-id="4b847-125">Azure will return a list of your subscriptions, and you will need to copy the GUID for the subscription that you want to use; for example:</span></span>

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
   ```

1. <span data-ttu-id="4b847-126">Укажите GUID учетной записи, которую вы собираетесь использовать в Azure, например:</span><span class="sxs-lookup"><span data-stu-id="4b847-126">Specify the GUID for the account you want to use with Azure; for example:</span></span>

   ```azurecli
   az account set -s ssssssss-ssss-ssss-ssss-ssssssssssss
   ```

## <a name="create-and-configure-a-new-azure-key-vault-using-the-azure-cli"></a><span data-ttu-id="4b847-127">Создание и настройка Azure Key Vault с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="4b847-127">Create and configure a new Azure Key Vault using the Azure CLI</span></span>

1. <span data-ttu-id="4b847-128">Создайте группу ресурсов Azure, которые будут использоваться для хранилища ключей, например:</span><span class="sxs-lookup"><span data-stu-id="4b847-128">Create a resource group for the Azure resources you will use for your key vault; for example:</span></span>
   ```azurecli
   az group create --name wingtiptoysresources --location westus
   ```
   <span data-ttu-id="4b847-129">Описание</span><span class="sxs-lookup"><span data-stu-id="4b847-129">Where:</span></span>

   | <span data-ttu-id="4b847-130">Параметр</span><span class="sxs-lookup"><span data-stu-id="4b847-130">Parameter</span></span> | <span data-ttu-id="4b847-131">ОПИСАНИЕ</span><span class="sxs-lookup"><span data-stu-id="4b847-131">Description</span></span> |
   |---|---|
   | `name` | <span data-ttu-id="4b847-132">Указывает уникальное имя для группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="4b847-132">Specifies a unique name for your resource group.</span></span> |
   | `location` | <span data-ttu-id="4b847-133">Указывает [регион Azure](https://azure.microsoft.com/regions/) для размещения группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="4b847-133">Specifies the [Azure region](https://azure.microsoft.com/regions/) where your resource group will be hosted.</span></span> |

   <span data-ttu-id="4b847-134">В Azure CLI отобразятся результаты созданной группы ресурсов, например:</span><span class="sxs-lookup"><span data-stu-id="4b847-134">The Azure CLI will display the results of your resource group creation; for example:</span></span>  

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

2. <span data-ttu-id="4b847-135">Создайте субъект-службу Azure, связанный с зарегистрированным приложением, например:</span><span class="sxs-lookup"><span data-stu-id="4b847-135">Create an Azure service principal from your application registration; for example:</span></span>
   ```shell
   az ad sp create-for-rbac --name "wingtiptoysuser"
   ```
   <span data-ttu-id="4b847-136">Описание</span><span class="sxs-lookup"><span data-stu-id="4b847-136">Where:</span></span>

   | <span data-ttu-id="4b847-137">Параметр</span><span class="sxs-lookup"><span data-stu-id="4b847-137">Parameter</span></span> | <span data-ttu-id="4b847-138">ОПИСАНИЕ</span><span class="sxs-lookup"><span data-stu-id="4b847-138">Description</span></span> |
   |---|---|
   | `name` | <span data-ttu-id="4b847-139">Определяет имя пользователя для субъекта-службы Azure.</span><span class="sxs-lookup"><span data-stu-id="4b847-139">Specifies the name for your Azure service principal.</span></span> |

   <span data-ttu-id="4b847-140">Azure CLI отобразит сообщение о состоянии JSON, которое содержит значения *appId* и *password* (вы будете использовать эти значения в качестве идентификатора клиента и пароля клиента позже), например:</span><span class="sxs-lookup"><span data-stu-id="4b847-140">The Azure CLI will return a JSON status message that contains the *appId* and *password*, which you will use later as the client id and client password; for example:</span></span>

   ```json
   {
     "appId": "iiiiiiii-iiii-iiii-iiii-iiiiiiiiiiii",
     "displayName": "wingtiptoysuser",
     "name": "http://wingtiptoysuser",
     "password": "pppppppp-pppp-pppp-pppp-pppppppppppp",
     "tenant": "tttttttt-tttt-tttt-tttt-tttttttttttt"
   }
   ```

3. <span data-ttu-id="4b847-141">Создайте хранилище ключей в группе ресурсов, например:</span><span class="sxs-lookup"><span data-stu-id="4b847-141">Create a new key vault in the resource group; for example:</span></span>
   ```azurecli
   az keyvault create --name wingtiptoyskeyvault --resource-group wingtiptoysresources --location westus --enabled-for-deployment true --enabled-for-disk-encryption true --enabled-for-template-deployment true --sku standard --query properties.vaultUri
   ```
   <span data-ttu-id="4b847-142">Описание</span><span class="sxs-lookup"><span data-stu-id="4b847-142">Where:</span></span>

   | <span data-ttu-id="4b847-143">Параметр</span><span class="sxs-lookup"><span data-stu-id="4b847-143">Parameter</span></span> | <span data-ttu-id="4b847-144">ОПИСАНИЕ</span><span class="sxs-lookup"><span data-stu-id="4b847-144">Description</span></span> |
   |---|---|
   | `name` | <span data-ttu-id="4b847-145">Указывает уникальное имя для хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="4b847-145">Specifies a unique name for your key vault.</span></span> |
   | `location` | <span data-ttu-id="4b847-146">Указывает [регион Azure](https://azure.microsoft.com/regions/) для размещения группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="4b847-146">Specifies the [Azure region](https://azure.microsoft.com/regions/) where your resource group will be hosted.</span></span> |
   | `enabled-for-deployment` | <span data-ttu-id="4b847-147">Указывает [вариант развертывания хранилища ключей](https://docs.microsoft.com/en-us/cli/azure/keyvault).</span><span class="sxs-lookup"><span data-stu-id="4b847-147">Specifies the [key vault deployment option](https://docs.microsoft.com/en-us/cli/azure/keyvault).</span></span> |
   | `enabled-for-disk-encryption` | <span data-ttu-id="4b847-148">Указывает [вариант шифрования хранилища ключей](https://docs.microsoft.com/en-us/cli/azure/keyvault).</span><span class="sxs-lookup"><span data-stu-id="4b847-148">Specifies the [key vault encryption option](https://docs.microsoft.com/en-us/cli/azure/keyvault).</span></span> |
   | `enabled-for-template-deployment` | <span data-ttu-id="4b847-149">Указывает [вариант шифрования хранилища ключей](https://docs.microsoft.com/en-us/cli/azure/keyvault).</span><span class="sxs-lookup"><span data-stu-id="4b847-149">Specifies the [key vault encryption option](https://docs.microsoft.com/en-us/cli/azure/keyvault).</span></span> |
   | `sku` | <span data-ttu-id="4b847-150">Указывает [вариант номера SKU хранилища ключей](https://docs.microsoft.com/en-us/cli/azure/keyvault).</span><span class="sxs-lookup"><span data-stu-id="4b847-150">Specifies the [key vault SKU option](https://docs.microsoft.com/en-us/cli/azure/keyvault).</span></span> |
   | `query` | <span data-ttu-id="4b847-151">Указывает значение, извлекаемое из ответа — URI хранилища ключей, необходимый для работы с этим руководством.</span><span class="sxs-lookup"><span data-stu-id="4b847-151">Specifies a value to retrieve from the response, which is the key vault URI that you will need to complete this tutorial.</span></span> |

   <span data-ttu-id="4b847-152">Azure CLI отобразит этот URI для хранилища ключей для дальнейшего использования, например:</span><span class="sxs-lookup"><span data-stu-id="4b847-152">The Azure CLI will display the URI for key vault, which you will use later; for example:</span></span>  

   ```
   "https://wingtiptoyskeyvault.vault.azure.net"
   ```

4. <span data-ttu-id="4b847-153">Настройте политику доступа для ранее созданного субъекта-службы Azure, например:</span><span class="sxs-lookup"><span data-stu-id="4b847-153">Set the access policy for the Azure service principal you created earlier; for example:</span></span>
   ```azurecli
   az keyvault set-policy --name wingtiptoyskeyvault --secret-permission set get list delete --spn "iiiiiiii-iiii-iiii-iiii-iiiiiiiiiiii"
   ```
   <span data-ttu-id="4b847-154">Описание</span><span class="sxs-lookup"><span data-stu-id="4b847-154">Where:</span></span>

   | <span data-ttu-id="4b847-155">Параметр</span><span class="sxs-lookup"><span data-stu-id="4b847-155">Parameter</span></span> | <span data-ttu-id="4b847-156">ОПИСАНИЕ</span><span class="sxs-lookup"><span data-stu-id="4b847-156">Description</span></span> |
   |---|---|
   | `name` | <span data-ttu-id="4b847-157">Указывает имя используемого хранилища ключей (см. выше).</span><span class="sxs-lookup"><span data-stu-id="4b847-157">Specifies your key vault name from earlier.</span></span> |
   | `secret-permission` | <span data-ttu-id="4b847-158">Указывает [политики безопасности](https://docs.microsoft.com/en-us/cli/azure/keyvault) для хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="4b847-158">Specifies the [security policies](https://docs.microsoft.com/en-us/cli/azure/keyvault) for your key vault.</span></span> |
   | `spn` | <span data-ttu-id="4b847-159">Указывает идентификатор GUID для зарегистрированного приложения (см. выше).</span><span class="sxs-lookup"><span data-stu-id="4b847-159">Specifies the GUID for your application registration from earlier.</span></span> |

   <span data-ttu-id="4b847-160">В Azure CLI отобразятся результаты создания политики безопасности, например:</span><span class="sxs-lookup"><span data-stu-id="4b847-160">The Azure CLI will display the results of your security policy creation; for example:</span></span>  

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

5. <span data-ttu-id="4b847-161">Сохраните секрет в новом хранилище ключей, например:</span><span class="sxs-lookup"><span data-stu-id="4b847-161">Store a secret in your new key vault; for example:</span></span>
   ```azurecli
   az keyvault secret set --vault-name "wingtiptoyskeyvault" --name "connectionString" --value "jdbc:sqlserver://SERVER.database.windows.net:1433;database=DATABASE;"
   ```
   <span data-ttu-id="4b847-162">Описание</span><span class="sxs-lookup"><span data-stu-id="4b847-162">Where:</span></span>

   | <span data-ttu-id="4b847-163">Параметр</span><span class="sxs-lookup"><span data-stu-id="4b847-163">Parameter</span></span> | <span data-ttu-id="4b847-164">ОПИСАНИЕ</span><span class="sxs-lookup"><span data-stu-id="4b847-164">Description</span></span> |
   |---|---|
   | `vault-name` | <span data-ttu-id="4b847-165">Указывает имя используемого хранилища ключей (см. выше).</span><span class="sxs-lookup"><span data-stu-id="4b847-165">Specifies your key vault name from earlier.</span></span> |
   | `name` | <span data-ttu-id="4b847-166">Указывает имя секрета.</span><span class="sxs-lookup"><span data-stu-id="4b847-166">Specifies the name of your secret.</span></span> |
   | `value` | <span data-ttu-id="4b847-167">Указывает значение секрета.</span><span class="sxs-lookup"><span data-stu-id="4b847-167">Specifies the value of your secret.</span></span> |

   <span data-ttu-id="4b847-168">В Azure CLI отобразятся результаты создания секрета, например:</span><span class="sxs-lookup"><span data-stu-id="4b847-168">The Azure CLI will display the results of your secret creation; for example:</span></span>  

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

## <a name="configure-and-compile-your-spring-boot-application"></a><span data-ttu-id="4b847-169">Настройка и компиляция приложения Spring Boot</span><span class="sxs-lookup"><span data-stu-id="4b847-169">Configure and compile your Spring Boot application</span></span>

1. <span data-ttu-id="4b847-170">Распакуйте архив с файлами проекта Spring Boot, которые вы скачали в каталог.</span><span class="sxs-lookup"><span data-stu-id="4b847-170">Extract the files from the Spring Boot project archive files that you downloaded earlier into a directory.</span></span>

2. <span data-ttu-id="4b847-171">В папке *main/src/ресурсы* проекта откройте файл *application.properties* в текстовом редакторе.</span><span class="sxs-lookup"><span data-stu-id="4b847-171">Navigate to the *src/main/resources* folder in your project and open the *application.properties* file in a text editor.</span></span>

3. <span data-ttu-id="4b847-172">Добавьте значения для хранилища ключей, используя ранее выполненные действия, например:</span><span class="sxs-lookup"><span data-stu-id="4b847-172">Add the values for your key vault using values from the steps that you completed earlier in this tutorial; for example:</span></span>
   ```yaml
   azure.keyvault.uri=https://wingtiptoyskeyvault.vault.azure.net/
   azure.keyvault.client-id=iiiiiiii-iiii-iiii-iiii-iiiiiiiiiiii
   azure.keyvault.client-key=pppppppp-pppp-pppp-pppp-pppppppppppp
   ```
   <span data-ttu-id="4b847-173">Описание</span><span class="sxs-lookup"><span data-stu-id="4b847-173">Where:</span></span>

   |          <span data-ttu-id="4b847-174">Параметр</span><span class="sxs-lookup"><span data-stu-id="4b847-174">Parameter</span></span>          |                                 <span data-ttu-id="4b847-175">ОПИСАНИЕ</span><span class="sxs-lookup"><span data-stu-id="4b847-175">Description</span></span>                                 |
   |-----------------------------|-----------------------------------------------------------------------------|
   |    `azure.keyvault.uri`     |           <span data-ttu-id="4b847-176">Указывает URI, полученный при создании хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="4b847-176">Specifies the URI from when you created your key vault.</span></span>           |
   | `azure.keyvault.client-id`  |  <span data-ttu-id="4b847-177">Указывает GUID *appId*, полученный при создании субъекта-службы.</span><span class="sxs-lookup"><span data-stu-id="4b847-177">Specifies the *appId* GUID from when you created your service principal.</span></span>   |
   | `azure.keyvault.client-key` | <span data-ttu-id="4b847-178">Указывает GUID *password*, полученный при создании субъекта-службы.</span><span class="sxs-lookup"><span data-stu-id="4b847-178">Specifies the *password* GUID from when you created your service principal.</span></span> |


4. <span data-ttu-id="4b847-179">Перейдите к файлу с основным кодом проекта, например: */src/main/java/com/wingtiptoys/secrets*.</span><span class="sxs-lookup"><span data-stu-id="4b847-179">Navigate to the main source code file of your project; for example: */src/main/java/com/wingtiptoys/secrets*.</span></span>

5. <span data-ttu-id="4b847-180">Откройте в текстовом редакторе основной файл Java приложения, например: *SecretsApplication.java*. Добавьте следующие строки в файл:</span><span class="sxs-lookup"><span data-stu-id="4b847-180">Open the application's main Java file in a file in a text editor; for example: *SecretsApplication.java*, and add the following lines to the file:</span></span>

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
   <span data-ttu-id="4b847-181">Этот пример кода извлекает строку подключения из хранилища ключей и отображает ее в командной строке.</span><span class="sxs-lookup"><span data-stu-id="4b847-181">This code example retrieves the connection string from the key vault and displays it to the command line.</span></span>

6. <span data-ttu-id="4b847-182">Сохраните и закройте файл Java.</span><span class="sxs-lookup"><span data-stu-id="4b847-182">Save and close the Java file.</span></span>

## <a name="build-and-test-your-app"></a><span data-ttu-id="4b847-183">Создание и тестирование приложения</span><span class="sxs-lookup"><span data-stu-id="4b847-183">Build and test your app</span></span>

1. <span data-ttu-id="4b847-184">Перейдите в каталог с файлом *pom.xml* приложения Spring Boot:</span><span class="sxs-lookup"><span data-stu-id="4b847-184">Navigate to the directory where the *pom.xml* file for your Spring Boot app is located:</span></span>

1. <span data-ttu-id="4b847-185">Создайте приложение Spring Boot с помощью Maven, например:</span><span class="sxs-lookup"><span data-stu-id="4b847-185">Build your Spring Boot application with Maven; for example:</span></span>

   ```bash
   mvn clean package
   ```

   <span data-ttu-id="4b847-186">В Maven отобразятся результаты создания.</span><span class="sxs-lookup"><span data-stu-id="4b847-186">Maven will display the results of your build.</span></span>

   ![Состояние сборки приложения Spring Boot][build-application-01]

1. <span data-ttu-id="4b847-188">Запустите приложение Spring Boot с помощью Maven. В приложении отобразится строка подключения, полученная из хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="4b847-188">Run your Spring Boot application with Maven; the application will display the connection string from your key vault.</span></span> <span data-ttu-id="4b847-189">Например: </span><span class="sxs-lookup"><span data-stu-id="4b847-189">For example:</span></span>

   ```bash
   mvn spring-boot:run
   ```

   ![Сообщение о времени выполнения Spring Boot][build-application-02]

## <a name="next-steps"></a><span data-ttu-id="4b847-191">Дополнительная информация</span><span class="sxs-lookup"><span data-stu-id="4b847-191">Next steps</span></span>

<span data-ttu-id="4b847-192">См. дополнительные сведения об использовании Azure Key Vault:</span><span class="sxs-lookup"><span data-stu-id="4b847-192">For more information about using Azure Key Vaults, see the following articles:</span></span>

* <span data-ttu-id="4b847-193">[Документация по хранилищу ключей].</span><span class="sxs-lookup"><span data-stu-id="4b847-193">[Key Vault Documentation].</span></span>

* <span data-ttu-id="4b847-194">[Приступая к работе с хранилищем ключей Azure]</span><span class="sxs-lookup"><span data-stu-id="4b847-194">[Get started with Azure Key Vault]</span></span>

<span data-ttu-id="4b847-195">Дополнительные сведения об использовании приложений Spring Boot в Azure см. в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="4b847-195">For more information about using Spring Boot applications on Azure, see the following articles:</span></span>

* [<span data-ttu-id="4b847-196">Развертывание приложения Spring Boot Application в службе приложений Azure</span><span class="sxs-lookup"><span data-stu-id="4b847-196">Deploy a Spring Boot Application to the Azure App Service</span></span>](deploy-spring-boot-java-web-app-on-azure.md)

* [<span data-ttu-id="4b847-197">Запуск приложения Spring Boot в кластере Kubernetes в Службе контейнеров Azure</span><span class="sxs-lookup"><span data-stu-id="4b847-197">Running a Spring Boot Application on a Kubernetes Cluster in the Azure Container Service</span></span>](deploy-spring-boot-java-app-on-kubernetes.md)

<span data-ttu-id="4b847-198">Дополнительные сведения об использовании Azure с Java см. в руководствах по [Azure для разработчиков Java] и [Java Tools for Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="4b847-198">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Java Tools for Visual Studio Team Services].</span></span>

<!-- URL List -->

[Документация по хранилищу ключей]: /azure/key-vault/
[Key Vault Documentation]: /azure/key-vault/
[Приступая к работе с хранилищем ключей Azure]: /azure/key-vault/key-vault-get-started
[Get started with Azure Key Vault]: /azure/key-vault/key-vault-get-started
[Azure для разработчиков Java]: https://docs.microsoft.com/java/azure/
[Azure for Java Developers]: https://docs.microsoft.com/java/azure/
[бесплатной учетной записи Azure]: https://azure.microsoft.com/pricing/free-trial/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/ (Инструменты Java для Visual Studio Team Services)
[Преимущества для подписчиков MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Initializr]: https://start.spring.io/
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[secrets-01]: media/configure-spring-boot-starter-java-app-with-azure-key-vault/secrets-01.png
[secrets-02]: media/configure-spring-boot-starter-java-app-with-azure-key-vault/secrets-02.png
[secrets-03]: media/configure-spring-boot-starter-java-app-with-azure-key-vault/secrets-03.png

[build-application-01]: media/configure-spring-boot-starter-java-app-with-azure-key-vault/build-application-01.png
[build-application-02]: media/configure-spring-boot-starter-java-app-with-azure-key-vault/build-application-02.png
