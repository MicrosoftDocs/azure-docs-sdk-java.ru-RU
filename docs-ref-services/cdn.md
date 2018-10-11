---
title: Библиотеки Azure CDN для Java
description: Справочная документация по библиотекам управления CDN для Java
keywords: Azure, Java, SDK, API, content, distribution, network, CDN
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 07/11/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: cdn
ms.openlocfilehash: 199e9b4b2b2431e23954d24e4adeb4326eb4741c
ms.sourcegitcommit: b64017f119177f97da7a5930489874e67b09c0fc
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/09/2018
ms.locfileid: "48893075"
---
# <a name="azure-cdn-libraries-for-java"></a><span data-ttu-id="b48a4-104">Библиотеки Azure CDN для Java</span><span class="sxs-lookup"><span data-stu-id="b48a4-104">Azure CDN libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="b48a4-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="b48a4-105">Overview</span></span>

<span data-ttu-id="b48a4-106">Кэшируйте статическое веб-содержимое в стратегически расположенных точках, обеспечивая максимальную пропускную способность для пользователей с помощью [сети доставки содержимого Azure](/azure/cdn/cdn-overview) (CDN).</span><span class="sxs-lookup"><span data-stu-id="b48a4-106">Cache static web content at strategically placed locations to provide maximum throughput for users with [Azure Content Delivery Network](/azure/cdn/cdn-overview) (CDN).</span></span>

<span data-ttu-id="b48a4-107">Чтобы приступить к работе с Azure CDN, см. инструкции по [началу работы с Azure CDN](/azure/cdn/cdn-create-new-endpoint).</span><span class="sxs-lookup"><span data-stu-id="b48a4-107">To get started with Azure CDN, see [Getting started with Azure CDN](/azure/cdn/cdn-create-new-endpoint).</span></span>

## <a name="management-api"></a><span data-ttu-id="b48a4-108">API управления</span><span class="sxs-lookup"><span data-stu-id="b48a4-108">Management API</span></span>

<span data-ttu-id="b48a4-109">Создавайте профили CDN, определяйте конечные точки и добавляйте содержимое в CDN с помощью API управления.</span><span class="sxs-lookup"><span data-stu-id="b48a4-109">Create CDN profiles, define endpoints, and add content to the CDN using the management API.</span></span>

<span data-ttu-id="b48a4-110">[Добавьте зависимость](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) в файл Maven `pom.xml`, чтобы использовать API управления в проекте.</span><span class="sxs-lookup"><span data-stu-id="b48a4-110">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the management API in your project.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-cdn</artifactId>
    <version>1.3.0</version>
</dependency>
```   

### <a name="example"></a><span data-ttu-id="b48a4-111">Пример</span><span class="sxs-lookup"><span data-stu-id="b48a4-111">Example</span></span>

<span data-ttu-id="b48a4-112">Создайте профиль CDN, назначьте конечные точки и загрузите содержимое в CDN.</span><span class="sxs-lookup"><span data-stu-id="b48a4-112">Create a CDN profile, assign endpoints, and load content into the CDN.</span></span>

```java
CdnProfile profile = azure.cdnProfiles().define("testCDN")
        .withRegion(Region.US_EAST)
        .withNewResourceGroup()
        .withStandardVerizonSku()
        .withNewEndpoint("webAppHostname1")
        .withNewEndpoint("webAppHostname2")
        .create();

List<String> contentList = new ArrayList<String>();
contentList.add("/client.js");
contentList.add("/media/fabrikam_logo.png");

for (CdnEndpoint endpoint : profile.endpoints().values()) {
    endpoint.loadContent(contentList);
}
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="b48a4-113">Обзор API-интерфейсов управления</span><span class="sxs-lookup"><span data-stu-id="b48a4-113">Explore the Management APIs</span></span>](/java/api/overview/azure/cdn/management)

## <a name="samples"></a><span data-ttu-id="b48a4-114">Примеры</span><span class="sxs-lookup"><span data-stu-id="b48a4-114">Samples</span></span>

[<span data-ttu-id="b48a4-115">Управление CDN с помощью Java</span><span class="sxs-lookup"><span data-stu-id="b48a4-115">Manage CDNs with Java</span></span>](https://github.com/Azure-Samples/cdn-java-manage-cdn)

<span data-ttu-id="b48a4-116">Ознакомьтесь с [примерами кода Java для Azure CDN](https://azure.microsoft.com/resources/samples/?platform=java&term=cdn), которые можно использовать в своих приложениях.</span><span class="sxs-lookup"><span data-stu-id="b48a4-116">Explore more [sample Java code for Azure CDN](https://azure.microsoft.com/resources/samples/?platform=java&term=cdn) you can use in your apps.</span></span>