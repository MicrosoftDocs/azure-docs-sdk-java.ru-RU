---
title: "Библиотеки службы приложений Azure для Java"
description: "Автоматизируйте развертывание веб-приложений в службе приложений Azure с помощью API-интерфейсов управления Azure."
keywords: Azure, Java, SDK, API, web apps, mobile, App Service
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 07/09/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: appservice
ms.openlocfilehash: 7e1d7eed9d8fa8d2f872f2902e2ce3f2b3dab7b6
ms.sourcegitcommit: 634ab7578c73a219f8f3a2a6d43999d9d372cb43
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/09/2017
---
# <a name="azure-app-service-libraries-for-java"></a>Библиотеки службы приложений Azure для Java

## <a name="overview"></a>Обзор

Развертывайте и администрируйте веб-сайты, веб-приложения и REST API с помощью [службы приложений Azure](/azure/app-service).

Чтобы приступить к работе со службой приложений Azure, см. инструкции по [созданию веб-приложения Java в Azure](/azure/app-service-web/app-service-web-get-started-java).

## <a name="management-api"></a>API управления

Развертывайте, масштабируйте и настраивайте приложения в службе приложений Azure с помощью API управления.

[Добавьте зависимость](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) в файл Maven `pom.xml`, чтобы использовать API управления в проекте.

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-appservice</artifactId>
    <version>1.3.0</version>
</dependency>
```   

> [!div class="nextstepaction"]
> [Обзор API-интерфейсов управления](/java/api/overview/azure)

### <a name="example"></a>Пример

Разверните веб-приложение из образа Docker в веб-приложение Azure под управлением Linux.

```java
WebApp app = azure.webApps().define("newLinuxWebApp")
    .withExistingLinuxPlan(myLinuxAppServicePlan)
    .withExistingResourceGroup("myResourceGroup")
    .withPrivateDockerHubImage("username/my-java-app")
    .withCredentials("dockerHubUser","dockerHubPassword")
    .withAppSetting("PORT","8080").
    .create();
```

## <a name="samples"></a>Примеры

[Развертывание веб-приложения из FTP или репозитория GitHub][1]  
[Переключение между версиями приложения с помощью слотов развертывания][2]  
[Настройка личного домена][3]   
[Масштабирование веб-приложения в нескольких регионах][4]   

Ознакомьтесь с [примером кода Java для службы приложений Azure](https://azure.microsoft.com/resources/samples/?platform=java&term=appservice), который можно использовать в своих приложениях.

[1]: ../docs-ref-conceptual/java-sdk-configure-webapp-sources.md
[2]: https://azure.microsoft.com/resources/samples/app-service-java-manage-staging-and-production-slots-for-web-apps/
[3]: https://azure.microsoft.com/resources/samples/app-service-java-manage-web-apps-with-custom-domains/
[4]: https://azure.microsoft.com/resources/samples/app-service-java-scale-web-apps-on-linux/
