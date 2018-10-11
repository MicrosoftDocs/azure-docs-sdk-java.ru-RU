---
title: Библиотеки Azure Application Insights для Java
description: Справочная документация по API управления Azure Application Insights для Java
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
ms.openlocfilehash: d881ff66ad806e13f7d2cbafff6ce85c23240304
ms.sourcegitcommit: b64017f119177f97da7a5930489874e67b09c0fc
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/09/2018
ms.locfileid: "48893415"
---
# <a name="azure-application-insights-libraries-for-java"></a><span data-ttu-id="c901c-104">Библиотеки Azure Application Insights для Java</span><span class="sxs-lookup"><span data-stu-id="c901c-104">Azure Application Insights libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="c901c-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="c901c-105">Overview</span></span>

<span data-ttu-id="c901c-106">Определяйте, сортируйте и диагностируйте неполадки в веб-приложениях и службах с помощью [Application Insights](/azure/application-insights/app-insights-overview).</span><span class="sxs-lookup"><span data-stu-id="c901c-106">Detect, triage, and diagnose issues in your web apps and services with [Application Insights](/azure/application-insights/app-insights-overview).</span></span>

<span data-ttu-id="c901c-107">Чтобы приступить к работе с Application Insights, см. инструкции по [началу работы с Application Insights в веб-проекте Java](/azure/application-insights/app-insights-java-get-started).</span><span class="sxs-lookup"><span data-stu-id="c901c-107">To get started with Application Insights, see [Get started with Application Insights in a Java web project](/azure/application-insights/app-insights-java-get-started).</span></span>

## <a name="client-library"></a><span data-ttu-id="c901c-108">Клиентская библиотека</span><span class="sxs-lookup"><span data-stu-id="c901c-108">Client library</span></span>

<span data-ttu-id="c901c-109">Добавляйте данные телеметрии, чтобы отслеживать события, исключения и пользовательские метрики в своих приложениях с помощью клиентской библиотеки Application Insights.</span><span class="sxs-lookup"><span data-stu-id="c901c-109">Add telemetry to track events, exceptions, and user metrics in your apps with the Application Insights client library.</span></span>

<span data-ttu-id="c901c-110">[Добавьте зависимость](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) в файл Maven `pom.xml`, чтобы использовать клиентскую библиотеку в проекте.</span><span class="sxs-lookup"><span data-stu-id="c901c-110">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the client library in your project.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>applicationinsights-web</artifactId>   
    <version>1.0.8</version>
</dependency>
```   

### <a name="example"></a><span data-ttu-id="c901c-111">Пример</span><span class="sxs-lookup"><span data-stu-id="c901c-111">Example</span></span>

<span data-ttu-id="c901c-112">Создайте запись метрики и запишите значение для нее.</span><span class="sxs-lookup"><span data-stu-id="c901c-112">Create a new metric entry and record a value for it.</span></span>

```java
    MetricTelemetry sample = new MetricTelemetry();
    sample.setName("metric name");
    sample.setValue(42.3);
    telemetryClient.TrackMetric(sample);
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="c901c-113">Обзор клиентских API-интерфейсов</span><span class="sxs-lookup"><span data-stu-id="c901c-113">Explore the Client APIs</span></span>](/java/api/overview/azure/appinsights/client)

## <a name="samples"></a><span data-ttu-id="c901c-114">Примеры</span><span class="sxs-lookup"><span data-stu-id="c901c-114">Samples</span></span>

<span data-ttu-id="c901c-115">Ознакомьтесь с [примерами кода Java для Application Insights](https://azure.microsoft.com/en-us/resources/samples/?term=insights&platform=java), которые можно использовать в своих приложениях.</span><span class="sxs-lookup"><span data-stu-id="c901c-115">Explore more [sample Java code for Application Insights](https://azure.microsoft.com/en-us/resources/samples/?term=insights&platform=java) you can use in your apps.</span></span>
