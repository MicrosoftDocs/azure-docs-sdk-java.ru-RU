---
title: "Библиотеки Azure Application Insights для Java"
description: "Справочная документация по API управления Azure Application Insights для Java"
keywords: Azure, Java, SDK, API, AppInsights, telemetry, diagnostics, trace, logs, performance
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 07/21/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: appinsights
ms.openlocfilehash: 9f943dc87d9e9b3e015407eea4dfd2900040da37
ms.sourcegitcommit: 1500f341a96d9da461c288abf4baf79f494ae662
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/28/2017
---
# <a name="azure-application-insights-libraries-for-java"></a>Библиотеки Azure Application Insights для Java

## <a name="overview"></a>Обзор

Определяйте, сортируйте и диагностируйте неполадки в веб-приложениях и службах с помощью [Application Insights](/azure/application-insights/app-insights-overview).

Чтобы приступить к работе с Application Insights, см. инструкции по [началу работы с Application Insights в веб-проекте Java](/azure/application-insights/app-insights-java-get-started).

## <a name="client-library"></a>Клиентская библиотека

Добавляйте данные телеметрии, чтобы отслеживать события, исключения и пользовательские метрики в своих приложениях с помощью клиентской библиотеки Application Insights.

[Добавьте зависимость](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) в файл Maven `pom.xml`, чтобы использовать клиентскую библиотеку в проекте.

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>applicationinsights-web</artifactId>   
    <version>1.0.8</version>
</dependency>
```   

### <a name="example"></a>Пример

Создайте запись метрики и запишите значение для нее.

```java
    MetricTelemetry sample = new MetricTelemetry();
    sample.setName("metric name");
    sample.setValue(42.3);
    telemetryClient.TrackMetric(sample);
```

> [!div class="nextstepaction"]
> [Обзор клиентских API-интерфейсов](/java/api/overview/azure/appinsights/clientlibrary)

## <a name="samples"></a>Примеры

Ознакомьтесь с [примерами кода Java для Application Insights](https://azure.microsoft.com/en-us/resources/samples/?term=insights&platform=java), которые можно использовать в своих приложениях.