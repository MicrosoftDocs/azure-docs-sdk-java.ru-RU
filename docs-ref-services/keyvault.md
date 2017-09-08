---
title: "Библиотеки Azure Key Vault для Java"
description: "Обзор библиотек Azure Key Vault для Java"
keywords: Azure, Java, SDK, API, keyvault, secure, keys, secrets, vault
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 07/20/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: keyvault
ms.openlocfilehash: dc5e0552728e362451c033317e5a804c8067e79c
ms.sourcegitcommit: 1500f341a96d9da461c288abf4baf79f494ae662
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/28/2017
---
# <a name="azure-key-vault-libraries-for-java"></a><span data-ttu-id="d2e85-104">Библиотеки Azure Key Vault для Java</span><span class="sxs-lookup"><span data-stu-id="d2e85-104">Azure Key Vault libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="d2e85-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="d2e85-105">Overview</span></span>

<span data-ttu-id="d2e85-106">Защищайте и администрируйте криптографические ключи и секреты, используемые облачными приложениями и службами, с помощью [Azure Key Vault](/azure/key-vault/).</span><span class="sxs-lookup"><span data-stu-id="d2e85-106">Safeguard and manage cryptographic keys and secrets used by cloud applications and services with [Azure Key Vault](/azure/key-vault/).</span></span>

<span data-ttu-id="d2e85-107">Чтобы приступить к работе с Azure Key Vault, см. инструкции по [началу работы с Azure Key Vault](/azure/key-vault/key-vault-get-started).</span><span class="sxs-lookup"><span data-stu-id="d2e85-107">To get started with Azure Key Vault, see [Get started with Azure Key Vault](/azure/key-vault/key-vault-get-started).</span></span>

## <a name="client-library"></a><span data-ttu-id="d2e85-108">Клиентская библиотека</span><span class="sxs-lookup"><span data-stu-id="d2e85-108">Client library</span></span>

<span data-ttu-id="d2e85-109">Создавайте, обновляйте и удаляйте ключи и секреты в Azure Key Vault с помощью клиентских библиотек.</span><span class="sxs-lookup"><span data-stu-id="d2e85-109">Create, update, and delete keys and secrets in Azure Key Vault with the client libraries.</span></span>

<span data-ttu-id="d2e85-110">[Добавьте зависимость](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) в файл Maven `pom.xml`, чтобы использовать клиентскую библиотеку в проекте.</span><span class="sxs-lookup"><span data-stu-id="d2e85-110">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the client library in your project.</span></span>  

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-keyvault</artifactId>
    <version>1.0.0</version>
</dependency>
```   

## <a name="example"></a><span data-ttu-id="d2e85-111">Пример</span><span class="sxs-lookup"><span data-stu-id="d2e85-111">Example</span></span>

<span data-ttu-id="d2e85-112">Получите [веб-ключ JSON](https://tools.ietf.org/html/draft-ietf-jose-json-web-key-18) из Key Vault.</span><span class="sxs-lookup"><span data-stu-id="d2e85-112">Retrieve a [JSON web key](https://tools.ietf.org/html/draft-ietf-jose-json-web-key-18) from a Key Vault.</span></span>

```java
KeyVaultClient kvc = new KeyVaultClient(credentials);
KeyBundle returnedKeyBundle = getKey(vaultUrl, keyName);
JsonWebKey jsonKey = returnedKeyBundle.key();
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="d2e85-113">Обзор клиентских API-интерфейсов</span><span class="sxs-lookup"><span data-stu-id="d2e85-113">Explore the Client APIs</span></span>](/java/api/overview/azure/keyvault/clientlibrary)


## <a name="management-api"></a><span data-ttu-id="d2e85-114">API управления</span><span class="sxs-lookup"><span data-stu-id="d2e85-114">Management API</span></span>

<span data-ttu-id="d2e85-115">Используйте библиотеки управления Azure Key Vault, чтобы создавать хранилища ключей, авторизовать приложения и управлять разрешениями.</span><span class="sxs-lookup"><span data-stu-id="d2e85-115">Use the Azure Key Vault management libraries to create key vaults, authorize applications, and manage permissions.</span></span> 

<span data-ttu-id="d2e85-116">[Добавьте зависимость](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) в файл Maven `pom.xml`, чтобы использовать API управления в проекте.</span><span class="sxs-lookup"><span data-stu-id="d2e85-116">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the management API in your project.</span></span>  

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-keyvault</artifactId>
    <version>1.1.2</version>
</dependency>
```

## <a name="example"></a><span data-ttu-id="d2e85-117">Пример</span><span class="sxs-lookup"><span data-stu-id="d2e85-117">Example</span></span>

<span data-ttu-id="d2e85-118">Авторизуйте приложение, запущенное с использованием [субъекта-службы](/azure/azure-resource-manager/resource-group-create-service-principal-portal) `clientId`, чтобы перечислить и получить секреты из хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="d2e85-118">Authorize and application running with [service principal](/azure/azure-resource-manager/resource-group-create-service-principal-portal) `clientId` to list and retrieve secrets from a key vault.</span></span> 

```java
vault1 = vault1.update()
            .defineAccessPolicy()
                .forServicePrincipal(clientId)
                .allowKeyAllPermissions()
                .allowSecretPermissions(SecretPermissions.GET)
                .allowSecretPermissions(SecretPermissions.LIST)
                .attach()
            .apply();
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="d2e85-119">Обзор API-интерфейсов управления</span><span class="sxs-lookup"><span data-stu-id="d2e85-119">Explore the Management APIs</span></span>](/java/api/overview/azure/keyvault/managementapi)


## <a name="samples"></a><span data-ttu-id="d2e85-120">Примеры</span><span class="sxs-lookup"><span data-stu-id="d2e85-120">Samples</span></span>

<span data-ttu-id="d2e85-121">[Управление хранилищами ключей][1]</span><span class="sxs-lookup"><span data-stu-id="d2e85-121">[Manage Key Vaults][1]</span></span>   

[1]: https://github.com/Azure-Samples/key-vault-java-manage-key-vaults

<span data-ttu-id="d2e85-122">Ознакомьтесь с [примерами кода Java для Azure Key Vault](https://azure.microsoft.com/resources/samples/?platform=java&term=key+vault), которые можно использовать в своих приложениях.</span><span class="sxs-lookup"><span data-stu-id="d2e85-122">Explore more [sample Java code for Azure Key Vault](https://azure.microsoft.com/resources/samples/?platform=java&term=key+vault) you can use in your apps.</span></span>
