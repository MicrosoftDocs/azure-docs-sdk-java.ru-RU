---
title: Как использовать начальное приложение Spring Boot Starter с Azure Key Vault
description: Сведения о настройке приложения Spring Boot Initializer с помощью начального приложения Azure Key Vault.
services: key-vault
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 11/21/2018
ms.devlang: java
ms.service: key-vault
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: identity
ms.openlocfilehash: fcb18de809f4465239f1f360a755624a5095e03a
ms.sourcegitcommit: 8d0c59ae7c91adbb9be3c3e6d4a3429ffe51519d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/27/2018
ms.locfileid: "52339158"
---
# <a name="how-to-use-the-spring-boot-starter-for-azure-key-vault"></a><span data-ttu-id="e1a0b-103">Как использовать начальное приложение Spring Boot Starter с Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="e1a0b-103">How to use the Spring Boot Starter for Azure Key Vault</span></span>

## <a name="overview"></a><span data-ttu-id="e1a0b-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="e1a0b-104">Overview</span></span>

<span data-ttu-id="e1a0b-105">В этой статье описано, как создать с помощью **[Spring Initializr]** начальное приложение Spring Boot для Azure Key Vault для получения строки подключения, которая хранится в виде секрета в хранилище ключей.</span><span class="sxs-lookup"><span data-stu-id="e1a0b-105">This article demonstrates creating an app with the **[Spring Initializr]** that uses the Spring Boot Starter for Azure Key Vault to retrieve a connection string that is stored as a secret in a key vault.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e1a0b-106">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="e1a0b-106">Prerequisites</span></span>

<span data-ttu-id="e1a0b-107">Чтобы выполнить действия, описанные в этой статье, необходимо следующее:</span><span class="sxs-lookup"><span data-stu-id="e1a0b-107">The following prerequisites are required in order to complete the steps in this article:</span></span>

* <span data-ttu-id="e1a0b-108">Подписка Azure. Если у вас ее еще нет, вы можете активировать [Преимущества для подписчиков MSDN] или зарегистрироваться для получения [бесплатной учетной записи Azure].</span><span class="sxs-lookup"><span data-stu-id="e1a0b-108">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="e1a0b-109">Поддерживаемая версия Java Development Kit (JDK).</span><span class="sxs-lookup"><span data-stu-id="e1a0b-109">A supported Java Development Kit (JDK).</span></span> <span data-ttu-id="e1a0b-110">Дополнительные сведения о версиях JDK, доступных для разработки в Azure, см. в статье <https://aka.ms/azure-jdks>.</span><span class="sxs-lookup"><span data-stu-id="e1a0b-110">For more information about the JDKs available for use when developing on Azure, see <https://aka.ms/azure-jdks>.</span></span>
* <span data-ttu-id="e1a0b-111">[Apache Maven](http://maven.apache.org/) версии 3.0 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="e1a0b-111">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>

## <a name="create-an-app-using-spring-initializr"></a><span data-ttu-id="e1a0b-112">Создание приложения с помощью Spring Initializr</span><span class="sxs-lookup"><span data-stu-id="e1a0b-112">Create an app using Spring Initializr</span></span>

1. <span data-ttu-id="e1a0b-113">Перейдите по адресу <https://start.spring.io/>.</span><span class="sxs-lookup"><span data-stu-id="e1a0b-113">Browse to <https://start.spring.io/>.</span></span>

1. <span data-ttu-id="e1a0b-114">Укажите, что необходимо создать проект **Maven** с помощью **Java**, введите имя **группы** и **артефакта** вашего приложения, а затем щелкните ссылку, чтобы **перейти к полной версии** Spring Initializr.</span><span class="sxs-lookup"><span data-stu-id="e1a0b-114">Specify that you want to generate a **Maven** project with **Java**, enter the **Group** and **Aritifact** names for your application, and then click the link to **Switch to the full version** of the Spring Initializr.</span></span>

   ![Указание имен группы и артефакта][secrets-01]

1. <span data-ttu-id="e1a0b-116">Прокрутите вниз до раздела **Azure** статьи и установите флажок рядом с пунктом **Azure Key Vault**.</span><span class="sxs-lookup"><span data-stu-id="e1a0b-116">Scroll down to the **Azure** section and check the box for **Azure Key Vault**.</span></span>

   ![Выбор начального приложения Azure Key Vault][secrets-02]

1. <span data-ttu-id="e1a0b-118">Прокрутите страницу вниз и нажмите кнопку, чтобы **создать проект**.</span><span class="sxs-lookup"><span data-stu-id="e1a0b-118">Scroll to the bottom of the page and click the button to **Generate Project**.</span></span>

   ![Создание проекта Spring Boot][secrets-03]

1. <span data-ttu-id="e1a0b-120">При появлении запроса скачайте проект на локальный компьютер.</span><span class="sxs-lookup"><span data-stu-id="e1a0b-120">When prompted, download the project to a path on your local computer.</span></span>

## <a name="sign-into-azure"></a><span data-ttu-id="e1a0b-121">Вход в Azure</span><span class="sxs-lookup"><span data-stu-id="e1a0b-121">Sign into Azure</span></span>

1. <span data-ttu-id="e1a0b-122">Откройте окно командной строки.</span><span class="sxs-lookup"><span data-stu-id="e1a0b-122">Open a command prompt.</span></span>

1. <span data-ttu-id="e1a0b-123">Войдите в учетную запись Azure с помощью интерфейса командной строки Azure.</span><span class="sxs-lookup"><span data-stu-id="e1a0b-123">Sign into your Azure account by using the Azure CLI:</span></span>

   ```azurecli
   az login
   ```
   <span data-ttu-id="e1a0b-124">Для завершения процесса входа следуйте инструкциям.</span><span class="sxs-lookup"><span data-stu-id="e1a0b-124">Follow the instructions to complete the sign-in process.</span></span>

1. <span data-ttu-id="e1a0b-125">Отобразите список подписок:</span><span class="sxs-lookup"><span data-stu-id="e1a0b-125">List your subscriptions:</span></span>

   ```azurecli
   az account list
   ```
   <span data-ttu-id="e1a0b-126">Azure отобразит список подписок, и вам нужно будет скопировать идентификатор GUID для подписки, которая будет использоваться, например:</span><span class="sxs-lookup"><span data-stu-id="e1a0b-126">Azure will return a list of your subscriptions, and you will need to copy the GUID for the subscription that you want to use; for example:</span></span>

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

1. <span data-ttu-id="e1a0b-127">Укажите GUID учетной записи, которую вы собираетесь использовать в Azure, например:</span><span class="sxs-lookup"><span data-stu-id="e1a0b-127">Specify the GUID for the account you want to use with Azure; for example:</span></span>

   ```azurecli
   az account set -s ssssssss-ssss-ssss-ssss-ssssssssssss
   ```

## <a name="create-a-new-azure-key-vault"></a><span data-ttu-id="e1a0b-128">Создание нового хранилища Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="e1a0b-128">Create a new Azure Key Vault</span></span>

1. <span data-ttu-id="e1a0b-129">Создайте группу ресурсов Azure, которые будут использоваться для хранилища ключей, например:</span><span class="sxs-lookup"><span data-stu-id="e1a0b-129">Create a resource group for the Azure resources you will use for your key vault; for example:</span></span>
   ```azurecli
   az group create --name wingtiptoysresources --location westus
   ```
   <span data-ttu-id="e1a0b-130">Описание</span><span class="sxs-lookup"><span data-stu-id="e1a0b-130">Where:</span></span>

   | <span data-ttu-id="e1a0b-131">Параметр</span><span class="sxs-lookup"><span data-stu-id="e1a0b-131">Parameter</span></span> | <span data-ttu-id="e1a0b-132">ОПИСАНИЕ</span><span class="sxs-lookup"><span data-stu-id="e1a0b-132">Description</span></span> |
   |---|---|
   | `name` | <span data-ttu-id="e1a0b-133">Указывает уникальное имя для группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="e1a0b-133">Specifies a unique name for your resource group.</span></span> |
   | `location` | <span data-ttu-id="e1a0b-134">Указывает [регион Azure](https://azure.microsoft.com/regions/) для размещения группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="e1a0b-134">Specifies the [Azure region](https://azure.microsoft.com/regions/) where your resource group will be hosted.</span></span> |

   <span data-ttu-id="e1a0b-135">В Azure CLI отобразятся результаты созданной группы ресурсов, например:</span><span class="sxs-lookup"><span data-stu-id="e1a0b-135">The Azure CLI will display the results of your resource group creation; for example:</span></span>  

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

2. <span data-ttu-id="e1a0b-136">Создайте субъект-службу Azure, связанный с зарегистрированным приложением, например:</span><span class="sxs-lookup"><span data-stu-id="e1a0b-136">Create an Azure service principal from your application registration; for example:</span></span>
   ```shell
   az ad sp create-for-rbac --name "wingtiptoysuser"
   ```
   <span data-ttu-id="e1a0b-137">Описание</span><span class="sxs-lookup"><span data-stu-id="e1a0b-137">Where:</span></span>

   | <span data-ttu-id="e1a0b-138">Параметр</span><span class="sxs-lookup"><span data-stu-id="e1a0b-138">Parameter</span></span> | <span data-ttu-id="e1a0b-139">ОПИСАНИЕ</span><span class="sxs-lookup"><span data-stu-id="e1a0b-139">Description</span></span> |
   |---|---|
   | `name` | <span data-ttu-id="e1a0b-140">Определяет имя пользователя для субъекта-службы Azure.</span><span class="sxs-lookup"><span data-stu-id="e1a0b-140">Specifies the name for your Azure service principal.</span></span> |

   <span data-ttu-id="e1a0b-141">Azure CLI отобразит сообщение о состоянии JSON, которое содержит значения *appId* и *password* (вы будете использовать эти значения в качестве идентификатора клиента и пароля клиента позже), например:</span><span class="sxs-lookup"><span data-stu-id="e1a0b-141">The Azure CLI will return a JSON status message that contains the *appId* and *password*, which you will use later as the client id and client password; for example:</span></span>

   ```json
   {
     "appId": "iiiiiiii-iiii-iiii-iiii-iiiiiiiiiiii",
     "displayName": "wingtiptoysuser",
     "name": "http://wingtiptoysuser",
     "password": "pppppppp-pppp-pppp-pppp-pppppppppppp",
     "tenant": "tttttttt-tttt-tttt-tttt-tttttttttttt"
   }
   ```

3. <span data-ttu-id="e1a0b-142">Создайте хранилище ключей в группе ресурсов, например:</span><span class="sxs-lookup"><span data-stu-id="e1a0b-142">Create a new key vault in the resource group; for example:</span></span>
   ```azurecli
   az keyvault create --name wingtiptoyskeyvault --resource-group wingtiptoysresources --location westus --enabled-for-deployment true --enabled-for-disk-encryption true --enabled-for-template-deployment true --sku standard --query properties.vaultUri
   ```
   <span data-ttu-id="e1a0b-143">Описание</span><span class="sxs-lookup"><span data-stu-id="e1a0b-143">Where:</span></span>

   | <span data-ttu-id="e1a0b-144">Параметр</span><span class="sxs-lookup"><span data-stu-id="e1a0b-144">Parameter</span></span> | <span data-ttu-id="e1a0b-145">ОПИСАНИЕ</span><span class="sxs-lookup"><span data-stu-id="e1a0b-145">Description</span></span> |
   |---|---|
   | `name` | <span data-ttu-id="e1a0b-146">Указывает уникальное имя для хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="e1a0b-146">Specifies a unique name for your key vault.</span></span> |
   | `location` | <span data-ttu-id="e1a0b-147">Указывает [регион Azure](https://azure.microsoft.com/regions/) для размещения группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="e1a0b-147">Specifies the [Azure region](https://azure.microsoft.com/regions/) where your resource group will be hosted.</span></span> |
   | `enabled-for-deployment` | <span data-ttu-id="e1a0b-148">Указывает [вариант развертывания хранилища ключей](https://docs.microsoft.com/cli/azure/keyvault).</span><span class="sxs-lookup"><span data-stu-id="e1a0b-148">Specifies the [key vault deployment option](https://docs.microsoft.com/cli/azure/keyvault).</span></span> |
   | `enabled-for-disk-encryption` | <span data-ttu-id="e1a0b-149">Указывает [вариант шифрования хранилища ключей](https://docs.microsoft.com/cli/azure/keyvault).</span><span class="sxs-lookup"><span data-stu-id="e1a0b-149">Specifies the [key vault encryption option](https://docs.microsoft.com/cli/azure/keyvault).</span></span> |
   | `enabled-for-template-deployment` | <span data-ttu-id="e1a0b-150">Указывает [вариант шифрования хранилища ключей](https://docs.microsoft.com/cli/azure/keyvault).</span><span class="sxs-lookup"><span data-stu-id="e1a0b-150">Specifies the [key vault encryption option](https://docs.microsoft.com/cli/azure/keyvault).</span></span> |
   | `sku` | <span data-ttu-id="e1a0b-151">Указывает [вариант номера SKU хранилища ключей](https://docs.microsoft.com/cli/azure/keyvault).</span><span class="sxs-lookup"><span data-stu-id="e1a0b-151">Specifies the [key vault SKU option](https://docs.microsoft.com/cli/azure/keyvault).</span></span> |
   | `query` | <span data-ttu-id="e1a0b-152">Указывает значение, извлекаемое из ответа — URI хранилища ключей, необходимый для работы с этим руководством.</span><span class="sxs-lookup"><span data-stu-id="e1a0b-152">Specifies a value to retrieve from the response, which is the key vault URI that you will need to complete this tutorial.</span></span> |

   <span data-ttu-id="e1a0b-153">Azure CLI отобразит этот URI для хранилища ключей для дальнейшего использования, например:</span><span class="sxs-lookup"><span data-stu-id="e1a0b-153">The Azure CLI will display the URI for key vault, which you will use later; for example:</span></span>  

   ```
   "https://wingtiptoyskeyvault.vault.azure.net"
   ```

4. <span data-ttu-id="e1a0b-154">Настройте политику доступа для ранее созданного субъекта-службы Azure, например:</span><span class="sxs-lookup"><span data-stu-id="e1a0b-154">Set the access policy for the Azure service principal you created earlier; for example:</span></span>
   ```azurecli
   az keyvault set-policy --name wingtiptoyskeyvault --secret-permission set get list delete --spn "iiiiiiii-iiii-iiii-iiii-iiiiiiiiiiii"
   ```
   <span data-ttu-id="e1a0b-155">Описание</span><span class="sxs-lookup"><span data-stu-id="e1a0b-155">Where:</span></span>

   | <span data-ttu-id="e1a0b-156">Параметр</span><span class="sxs-lookup"><span data-stu-id="e1a0b-156">Parameter</span></span> | <span data-ttu-id="e1a0b-157">ОПИСАНИЕ</span><span class="sxs-lookup"><span data-stu-id="e1a0b-157">Description</span></span> |
   |---|---|
   | `name` | <span data-ttu-id="e1a0b-158">Указывает имя используемого хранилища ключей (см. выше).</span><span class="sxs-lookup"><span data-stu-id="e1a0b-158">Specifies your key vault name from earlier.</span></span> |
   | `secret-permission` | <span data-ttu-id="e1a0b-159">Указывает [политики безопасности](https://docs.microsoft.com/cli/azure/keyvault) для хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="e1a0b-159">Specifies the [security policies](https://docs.microsoft.com/cli/azure/keyvault) for your key vault.</span></span> |
   | `spn` | <span data-ttu-id="e1a0b-160">Указывает идентификатор GUID для зарегистрированного приложения (см. выше).</span><span class="sxs-lookup"><span data-stu-id="e1a0b-160">Specifies the GUID for your application registration from earlier.</span></span> |

   <span data-ttu-id="e1a0b-161">В Azure CLI отобразятся результаты создания политики безопасности, например:</span><span class="sxs-lookup"><span data-stu-id="e1a0b-161">The Azure CLI will display the results of your security policy creation; for example:</span></span>  

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

5. <span data-ttu-id="e1a0b-162">Сохраните секрет в новом хранилище ключей, например:</span><span class="sxs-lookup"><span data-stu-id="e1a0b-162">Store a secret in your new key vault; for example:</span></span>
   ```azurecli
   az keyvault secret set --vault-name "wingtiptoyskeyvault" --name "connectionString" --value "jdbc:sqlserver://SERVER.database.windows.net:1433;database=DATABASE;"
   ```
   <span data-ttu-id="e1a0b-163">Описание</span><span class="sxs-lookup"><span data-stu-id="e1a0b-163">Where:</span></span>

   | <span data-ttu-id="e1a0b-164">Параметр</span><span class="sxs-lookup"><span data-stu-id="e1a0b-164">Parameter</span></span> | <span data-ttu-id="e1a0b-165">ОПИСАНИЕ</span><span class="sxs-lookup"><span data-stu-id="e1a0b-165">Description</span></span> |
   |---|---|
   | `vault-name` | <span data-ttu-id="e1a0b-166">Указывает имя используемого хранилища ключей (см. выше).</span><span class="sxs-lookup"><span data-stu-id="e1a0b-166">Specifies your key vault name from earlier.</span></span> |
   | `name` | <span data-ttu-id="e1a0b-167">Указывает имя секрета.</span><span class="sxs-lookup"><span data-stu-id="e1a0b-167">Specifies the name of your secret.</span></span> |
   | `value` | <span data-ttu-id="e1a0b-168">Указывает значение секрета.</span><span class="sxs-lookup"><span data-stu-id="e1a0b-168">Specifies the value of your secret.</span></span> |

   <span data-ttu-id="e1a0b-169">В Azure CLI отобразятся результаты создания секрета, например:</span><span class="sxs-lookup"><span data-stu-id="e1a0b-169">The Azure CLI will display the results of your secret creation; for example:</span></span>  

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

## <a name="configure-and-compile-your-app"></a><span data-ttu-id="e1a0b-170">Настройка и компиляция приложения</span><span class="sxs-lookup"><span data-stu-id="e1a0b-170">Configure and compile your app</span></span>

1. <span data-ttu-id="e1a0b-171">Распакуйте архив с файлами проекта Spring Boot, которые вы скачали в каталог.</span><span class="sxs-lookup"><span data-stu-id="e1a0b-171">Extract the files from the Spring Boot project archive files that you downloaded earlier into a directory.</span></span>

2. <span data-ttu-id="e1a0b-172">В папке *main/src/ресурсы* проекта откройте файл *application.properties* в текстовом редакторе.</span><span class="sxs-lookup"><span data-stu-id="e1a0b-172">Navigate to the *src/main/resources* folder in your project and open the *application.properties* file in a text editor.</span></span>

3. <span data-ttu-id="e1a0b-173">Добавьте значения для хранилища ключей, используя ранее выполненные действия, например:</span><span class="sxs-lookup"><span data-stu-id="e1a0b-173">Add the values for your key vault using values from the steps that you completed earlier in this tutorial; for example:</span></span>
   ```yaml
   azure.keyvault.uri=https://wingtiptoyskeyvault.vault.azure.net/
   azure.keyvault.client-id=iiiiiiii-iiii-iiii-iiii-iiiiiiiiiiii
   azure.keyvault.client-key=pppppppp-pppp-pppp-pppp-pppppppppppp
   ```
   <span data-ttu-id="e1a0b-174">Описание</span><span class="sxs-lookup"><span data-stu-id="e1a0b-174">Where:</span></span>

   |          <span data-ttu-id="e1a0b-175">Параметр</span><span class="sxs-lookup"><span data-stu-id="e1a0b-175">Parameter</span></span>          |                                 <span data-ttu-id="e1a0b-176">ОПИСАНИЕ</span><span class="sxs-lookup"><span data-stu-id="e1a0b-176">Description</span></span>                                 |
   |-----------------------------|-----------------------------------------------------------------------------|
   |    `azure.keyvault.uri`     |           <span data-ttu-id="e1a0b-177">Указывает URI, полученный при создании хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="e1a0b-177">Specifies the URI from when you created your key vault.</span></span>           |
   | `azure.keyvault.client-id`  |  <span data-ttu-id="e1a0b-178">Указывает GUID *appId*, полученный при создании субъекта-службы.</span><span class="sxs-lookup"><span data-stu-id="e1a0b-178">Specifies the *appId* GUID from when you created your service principal.</span></span>   |
   | `azure.keyvault.client-key` | <span data-ttu-id="e1a0b-179">Указывает GUID *password*, полученный при создании субъекта-службы.</span><span class="sxs-lookup"><span data-stu-id="e1a0b-179">Specifies the *password* GUID from when you created your service principal.</span></span> |


4. <span data-ttu-id="e1a0b-180">Перейдите к файлу с основным кодом проекта, например: */src/main/java/com/wingtiptoys/secrets*.</span><span class="sxs-lookup"><span data-stu-id="e1a0b-180">Navigate to the main source code file of your project; for example: */src/main/java/com/wingtiptoys/secrets*.</span></span>

5. <span data-ttu-id="e1a0b-181">Откройте в текстовом редакторе основной файл Java приложения, например: *SecretsApplication.java*. Добавьте следующие строки в файл:</span><span class="sxs-lookup"><span data-stu-id="e1a0b-181">Open the application's main Java file in a file in a text editor; for example: *SecretsApplication.java*, and add the following lines to the file:</span></span>

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
   <span data-ttu-id="e1a0b-182">Этот пример кода извлекает строку подключения из хранилища ключей и отображает ее в командной строке.</span><span class="sxs-lookup"><span data-stu-id="e1a0b-182">This code example retrieves the connection string from the key vault and displays it to the command line.</span></span>

6. <span data-ttu-id="e1a0b-183">Сохраните и закройте файл Java.</span><span class="sxs-lookup"><span data-stu-id="e1a0b-183">Save and close the Java file.</span></span>

## <a name="build-and-test-your-app"></a><span data-ttu-id="e1a0b-184">Создание и тестирование приложения</span><span class="sxs-lookup"><span data-stu-id="e1a0b-184">Build and test your app</span></span>

1. <span data-ttu-id="e1a0b-185">Перейдите в каталог с файлом *pom.xml* приложения Spring Boot:</span><span class="sxs-lookup"><span data-stu-id="e1a0b-185">Navigate to the directory where the *pom.xml* file for your Spring Boot app is located:</span></span>

1. <span data-ttu-id="e1a0b-186">Создайте приложение Spring Boot с помощью Maven, например:</span><span class="sxs-lookup"><span data-stu-id="e1a0b-186">Build your Spring Boot application with Maven; for example:</span></span>

   ```bash
   mvn clean package
   ```

   <span data-ttu-id="e1a0b-187">В Maven отобразятся результаты создания.</span><span class="sxs-lookup"><span data-stu-id="e1a0b-187">Maven will display the results of your build.</span></span>

   ![Состояние сборки приложения Spring Boot][build-application-01]

1. <span data-ttu-id="e1a0b-189">Запустите приложение Spring Boot с помощью Maven. В приложении отобразится строка подключения, полученная из хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="e1a0b-189">Run your Spring Boot application with Maven; the application will display the connection string from your key vault.</span></span> <span data-ttu-id="e1a0b-190">Например: </span><span class="sxs-lookup"><span data-stu-id="e1a0b-190">For example:</span></span>

   ```bash
   mvn spring-boot:run
   ```

   ![Сообщение о времени выполнения Spring Boot][build-application-02]

## <a name="summary"></a><span data-ttu-id="e1a0b-192">Сводка</span><span class="sxs-lookup"><span data-stu-id="e1a0b-192">Summary</span></span>

<span data-ttu-id="e1a0b-193">В этом руководстве вы создали веб-приложение Java с помощью **[Spring Initializr]**, создали хранилище Azure Key Vault для хранения конфиденциальной информации, а затем настроили созданное приложение для получения сведений из хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="e1a0b-193">In this tutorial, you created a new Java web application using the **[Spring Initializr]**, created ab Azure Key Vault to store sensitive information, and then configured your application to retrieve information from your key vault.</span></span>

<span data-ttu-id="e1a0b-194">См. дополнительные сведения об использовании Azure Key Vault:</span><span class="sxs-lookup"><span data-stu-id="e1a0b-194">For more information about using Azure Key Vaults, see the following articles:</span></span>

* <span data-ttu-id="e1a0b-195">[Документация по хранилищу ключей].</span><span class="sxs-lookup"><span data-stu-id="e1a0b-195">[Key Vault Documentation].</span></span>

* <span data-ttu-id="e1a0b-196">[Приступая к работе с хранилищем ключей Azure]</span><span class="sxs-lookup"><span data-stu-id="e1a0b-196">[Get started with Azure Key Vault]</span></span>

<span data-ttu-id="e1a0b-197">Дополнительные сведения об использовании приложений Spring Boot в Azure см. в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="e1a0b-197">For more information about using Spring Boot applications on Azure, see the following articles:</span></span>

* [<span data-ttu-id="e1a0b-198">Развертывание приложения Spring Boot Application в службе приложений Azure</span><span class="sxs-lookup"><span data-stu-id="e1a0b-198">Deploy a Spring Boot Application to the Azure App Service</span></span>](deploy-spring-boot-java-web-app-on-azure.md)

* [<span data-ttu-id="e1a0b-199">Запуск приложения Spring Boot в кластере Kubernetes в Службе контейнеров Azure</span><span class="sxs-lookup"><span data-stu-id="e1a0b-199">Running a Spring Boot Application on a Kubernetes Cluster in the Azure Container Service</span></span>](deploy-spring-boot-java-app-on-kubernetes.md)

<span data-ttu-id="e1a0b-200">Дополнительные сведения об использовании Azure с Java см. в руководствах по [Azure для разработчиков Java] и [инструментах Java для Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="e1a0b-200">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Java Tools for Visual Studio Team Services].</span></span>

## <a name="next-steps"></a><span data-ttu-id="e1a0b-201">Дополнительная информация</span><span class="sxs-lookup"><span data-stu-id="e1a0b-201">Next steps</span></span>

<span data-ttu-id="e1a0b-202">Дополнительные сведения о Spring и Azure см. в центре документации об использовании Spring в Azure.</span><span class="sxs-lookup"><span data-stu-id="e1a0b-202">To learn more about Spring and Azure, continue to the Spring on Azure documentation center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="e1a0b-203">Spring в Azure</span><span class="sxs-lookup"><span data-stu-id="e1a0b-203">Spring on Azure</span></span>](/java/azure/spring-framework)

<!-- URL List -->

[Документация по хранилищу ключей]: /azure/key-vault/
[Key Vault Documentation]: /azure/key-vault/
[Приступая к работе с хранилищем ключей Azure]: /azure/key-vault/key-vault-get-started
[Get started with Azure Key Vault]: /azure/key-vault/key-vault-get-started
[Azure для разработчиков Java]: https://docs.microsoft.com/java/azure/
[Azure for Java Developers]: https://docs.microsoft.com/java/azure/
[бесплатной учетной записи Azure]: https://azure.microsoft.com/pricing/free-trial/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[инструментах Java для Visual Studio Team Services]: https://java.visualstudio.com/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
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
