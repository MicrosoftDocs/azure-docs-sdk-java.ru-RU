---
title: Библиотеки Azure Data Lake Analytics для Java
description: Справочная документация по библиотекам Azure Data Lake Analytics для Java
keywords: Azure, Java, SDK, API, big data, data lake
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 06/21/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: data-lake-store
ms.openlocfilehash: c14c89f961951d114362adee4fec6239e78cffb3
ms.sourcegitcommit: 49b17bbf34732512f836ee634818f1058147ff5c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2018
---
# <a name="azure-data-lake-analytics-libraries-for-java"></a>Библиотеки Azure Data Lake Analytics для Java

## <a name="overview"></a>Обзор

Запускайте задания анализа больших данных для масштабирования больших массивов данных с помощью [Azure Data Lake Analytics](/azure/data-lake-analytics/data-lake-analytics-overview).

Чтобы приступить к работе с Azure Data Lake Analytics, см. инструкции по [началу работы с Azure Data Lake Analytics с помощью пакета SDK для Java](/azure/data-lake-analytics/data-lake-analytics-get-started-java-sdk).

## <a name="management-api"></a>API управления

Используйте API управления для администрирования учетных записей, заданий, политик и каталогов Data Lake Analytics.

[Добавьте зависимость](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) в файл Maven `pom.xml`, чтобы использовать API управления в проекте.


```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-datalake-analytics</artifactId>
    <version>1.0.0-beta1.3</version>
</dependency>
```

## <a name="example"></a>Пример

Отправьте новое задание U-SQL в Data Lake Analytics.

```java
// authenticate with service principal credentials
ApplicationTokenCredentials creds = new ApplicationTokenCredentials(_clientId, _tenantId, _clientSecret, null);
DataLakeAnalyticsJobManagementClient adlaJobClient = new DataLakeAnalyticsJobManagementClientImpl(creds);

// set up job parameters
UUID jobId = java.util.UUID.randomUUID();
USqlJobProperties properties = new USqlJobProperties();
properties.setScript("@input =  EXTRACT Data string FROM \"/input1.csv\" USING Extractors.Csv(); OUTPUT @input TO @\"/output1.csv\" USING Outputters.Csv();");
JobInformation parameters = new JobInformation();
parameters.setName("testJob");
parameters.setJobId(jobId);
parameters.setType(JobType.USQL);
parameters.setProperties(properties);

// create the job
JobInformation jobInfo = adlaJobClient.getJobOperations().create(accountName, jobId, parameters).getBody();

```

> [!div class="nextstepaction"]
> [Обзор API-интерфейсов управления](/java/api/overview/azure/datalakeanalytics/management)

## <a name="samples"></a>Примеры

[Работа с Azure Data Lake Analytics с помощью пакета SDK для Java][1] 

[1]: https://docs.microsoft.com/azure/data-lake-analytics/data-lake-analytics-get-started-java-sdk

См. [полный список](https://azure.microsoft.com/resources/samples/?platform=java&term=analytics) примеров для Azure Data Lake Analytics.
