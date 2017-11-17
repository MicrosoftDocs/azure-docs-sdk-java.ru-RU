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
# <a name="azure-app-service-libraries-for-java"></a><span data-ttu-id="da18b-104">Библиотеки службы приложений Azure для Java</span><span class="sxs-lookup"><span data-stu-id="da18b-104">Azure App Service libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="da18b-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="da18b-105">Overview</span></span>

<span data-ttu-id="da18b-106">Развертывайте и администрируйте веб-сайты, веб-приложения и REST API с помощью [службы приложений Azure](/azure/app-service).</span><span class="sxs-lookup"><span data-stu-id="da18b-106">Deploy and manage websites, web applications, and REST APIs with [Azure App Service](/azure/app-service).</span></span>

<span data-ttu-id="da18b-107">Чтобы приступить к работе со службой приложений Azure, см. инструкции по [созданию веб-приложения Java в Azure](/azure/app-service-web/app-service-web-get-started-java).</span><span class="sxs-lookup"><span data-stu-id="da18b-107">To get started with Azure App Service, see [Create your first Java web app in Azure](/azure/app-service-web/app-service-web-get-started-java).</span></span>

## <a name="management-api"></a><span data-ttu-id="da18b-108">API управления</span><span class="sxs-lookup"><span data-stu-id="da18b-108">Management API</span></span>

<span data-ttu-id="da18b-109">Развертывайте, масштабируйте и настраивайте приложения в службе приложений Azure с помощью API управления.</span><span class="sxs-lookup"><span data-stu-id="da18b-109">Deploy, scale, and configure applications in Azure App Service with the management API.</span></span>

<span data-ttu-id="da18b-110">[Добавьте зависимость](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) в файл Maven `pom.xml`, чтобы использовать API управления в проекте.</span><span class="sxs-lookup"><span data-stu-id="da18b-110">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the management API in your project.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-appservice</artifactId>
    <version>1.3.0</version>
</dependency>
```   

> [!div class="nextstepaction"]
> [<span data-ttu-id="da18b-111">Обзор API-интерфейсов управления</span><span class="sxs-lookup"><span data-stu-id="da18b-111">Explore the Management APIs</span></span>](/java/api/overview/azure)

### <a name="example"></a><span data-ttu-id="da18b-112">Пример</span><span class="sxs-lookup"><span data-stu-id="da18b-112">Example</span></span>

<span data-ttu-id="da18b-113">Разверните веб-приложение из образа Docker в веб-приложение Azure под управлением Linux.</span><span class="sxs-lookup"><span data-stu-id="da18b-113">Deploy a webapp from a Docker image into an Azure Web App running on Linux.</span></span>

```java
WebApp app = azure.webApps().define("newLinuxWebApp")
    .withExistingLinuxPlan(myLinuxAppServicePlan)
    .withExistingResourceGroup("myResourceGroup")
    .withPrivateDockerHubImage("username/my-java-app")
    .withCredentials("dockerHubUser","dockerHubPassword")
    .withAppSetting("PORT","8080").
    .create();
```

## <a name="samples"></a><span data-ttu-id="da18b-114">Примеры</span><span class="sxs-lookup"><span data-stu-id="da18b-114">Samples</span></span>

<span data-ttu-id="da18b-115">[Развертывание веб-приложения из FTP или репозитория GitHub][1]</span><span class="sxs-lookup"><span data-stu-id="da18b-115">[Deploy a web app from FTP or GitHub][1]</span></span>  
<span data-ttu-id="da18b-116">[Переключение между версиями приложения с помощью слотов развертывания][2]</span><span class="sxs-lookup"><span data-stu-id="da18b-116">[Swap between app versions with deployment slots][2]</span></span>  
<span data-ttu-id="da18b-117">[Настройка личного домена][3] </span><span class="sxs-lookup"><span data-stu-id="da18b-117">[Configure a custom domain][3] </span></span>  
<span data-ttu-id="da18b-118">[Масштабирование веб-приложения в нескольких регионах][4]</span><span class="sxs-lookup"><span data-stu-id="da18b-118">[Scale a web app across multiple regions][4]</span></span>   

<span data-ttu-id="da18b-119">Ознакомьтесь с [примером кода Java для службы приложений Azure](https://azure.microsoft.com/resources/samples/?platform=java&term=appservice), который можно использовать в своих приложениях.</span><span class="sxs-lookup"><span data-stu-id="da18b-119">Explore more [sample Java code for Azure App Service](https://azure.microsoft.com/resources/samples/?platform=java&term=appservice) you can use in your apps.</span></span>

[1]: ../docs-ref-conceptual/java-sdk-configure-webapp-sources.md
[2]: https://azure.microsoft.com/resources/samples/app-service-java-manage-staging-and-production-slots-for-web-apps/
[3]: https://azure.microsoft.com/resources/samples/app-service-java-manage-web-apps-with-custom-domains/
[4]: https://azure.microsoft.com/resources/samples/app-service-java-scale-web-apps-on-linux/
