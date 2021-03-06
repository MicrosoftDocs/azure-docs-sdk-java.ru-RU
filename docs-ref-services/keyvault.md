---
title: Библиотеки Azure Key Vault для Java
description: Обзор библиотек Azure Key Vault для Java
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
ms.openlocfilehash: f025479301fd923b7620e8560e8586c8ab63c80b
ms.sourcegitcommit: 8d0c59ae7c91adbb9be3c3e6d4a3429ffe51519d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/27/2018
ms.locfileid: "52338988"
---
# <a name="azure-key-vault-libraries-for-java"></a>Библиотеки Azure Key Vault для Java

## <a name="overview"></a>Обзор

Защищайте и администрируйте криптографические ключи и секреты, используемые облачными приложениями и службами, с помощью [Azure Key Vault](/azure/key-vault/).

Чтобы приступить к работе с Azure Key Vault, см. инструкции по [началу работы с Azure Key Vault](/azure/key-vault/key-vault-get-started).

## <a name="client-library"></a>Клиентская библиотека

Создавайте, обновляйте и удаляйте ключи и секреты в Azure Key Vault с помощью клиентских библиотек.

[Добавьте зависимость](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) в файл Maven `pom.xml`, чтобы использовать клиентскую библиотеку в проекте.  

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-keyvault</artifactId>
    <version>1.1.2</version>
</dependency>
```   

## <a name="example"></a>Пример

Получите [веб-ключ JSON](https://tools.ietf.org/html/draft-ietf-jose-json-web-key-18) из Key Vault.

```java
KeyVaultClient kvc = new KeyVaultClient(credentials);
KeyBundle returnedKeyBundle = kvc.getKey(vaultUrl, keyName);
JsonWebKey jsonKey = returnedKeyBundle.key();
```

> [!div class="nextstepaction"]
> [Обзор клиентских API-интерфейсов](/java/api/overview/azure/keyvault/client)


## <a name="management-api"></a>API управления

Используйте библиотеки управления Azure Key Vault, чтобы создавать хранилища ключей, авторизовать приложения и управлять разрешениями. 

[Добавьте зависимость](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) в файл Maven `pom.xml`, чтобы использовать API управления в проекте.  

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-keyvault</artifactId>
    <version>1.15.0</version>
</dependency>
```

## <a name="example"></a>Пример

Авторизуйте приложение, запущенное с использованием [субъекта-службы](/azure/azure-resource-manager/resource-group-create-service-principal-portal) `clientId`, чтобы перечислить и получить секреты из хранилища ключей. 

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
> [Обзор API-интерфейсов управления](/java/api/overview/azure/keyvault/management)


## <a name="samples"></a>Примеры

Ознакомьтесь с [примерами кода Java для Azure Key Vault](https://azure.microsoft.com/resources/samples/?platform=java&term=key+vault), которые можно использовать в своих приложениях.
