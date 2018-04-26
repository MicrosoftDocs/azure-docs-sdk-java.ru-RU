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
ms.sourcegitcommit: 49b17bbf34732512f836ee634818f1058147ff5c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2018
---
# <a name="azure-cdn-libraries-for-java"></a>Библиотеки Azure CDN для Java

## <a name="overview"></a>Обзор

Кэшируйте статическое веб-содержимое в стратегически расположенных точках, обеспечивая максимальную пропускную способность для пользователей с помощью [сети доставки содержимого Azure](/azure/cdn/cdn-overview) (CDN).

Чтобы приступить к работе с Azure CDN, см. инструкции по [началу работы с Azure CDN](/azure/cdn/cdn-create-new-endpoint).

## <a name="management-api"></a>API управления

Создавайте профили CDN, определяйте конечные точки и добавляйте содержимое в CDN с помощью API управления.

[Добавьте зависимость](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) в файл Maven `pom.xml`, чтобы использовать API управления в проекте.

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-cdn</artifactId>
    <version>1.3.0</version>
</dependency>
```   

### <a name="example"></a>Пример

Создайте профиль CDN, назначьте конечные точки и загрузите содержимое в CDN.

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
> [Обзор API-интерфейсов управления](/java/api/overview/azure/cdn/management)

## <a name="samples"></a>Примеры

[Управление CDN с помощью Java](https://github.com/Azure-Samples/cdn-java-manage-cdn)

Ознакомьтесь с [примерами кода Java для Azure CDN](https://azure.microsoft.com/resources/samples/?platform=java&term=cdn), которые можно использовать в своих приложениях.