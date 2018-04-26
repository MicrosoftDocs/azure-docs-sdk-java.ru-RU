---
title: Библиотеки Azure Data Lake Store для Java
description: Справочная документация по библиотекам Data Lake Store для Java
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
ms.openlocfilehash: bcd1fd17759f7d171006d7b2126019d00d06d1db
ms.sourcegitcommit: 49b17bbf34732512f836ee634818f1058147ff5c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2018
---
# <a name="azure-data-lake-store-libraries-for-java"></a>Библиотеки Azure Data Lake Store для Java

## <a name="overview"></a>Обзор

Используйте [Azure Data Lake Store](/azure/data-lake-store/data-lake-store-overview) для централизованного сбора данных любого размера, типа и с любой скоростью приема для ведения аналитики.

Чтобы приступить к работе с Data Lake Store, ознакомьтесь со статьей [Начало работы с хранилищем озера данных Azure с помощью Java](/azure/data-lake-store/data-lake-store-get-started-java-sdk).


## <a name="client-library"></a>Клиентская библиотека

Выполняйте чтение и запись файлов, задавайте разрешения и метаданные и управляйте файлами и каталогами в Data Lake Store с помощью клиентской библиотеки.

[Добавьте зависимость](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) в файл Maven `pom.xml`, чтобы использовать клиентскую библиотеку в проекте.

```XML
<dependency>
   <groupId>com.microsoft.azure</groupId>
   <artifactId>azure-data-lake-store-sdk</artifactId>
   <version>2.1.5</version>
</dependency>
```   

## <a name="example"></a>Пример

Создайте клиент Data Lake с полным доменным именем и маркером доступа OAuth2, а затем создайте файл в Data Lake и запишите данные в него.

```java
// AccessTokenProvider provider = new ClientCredsTokenProvider(authTokenEndpoint, clientId, clientKey);
ADLStoreClient client = ADLStoreClient.createClient(accountFQDN, provider);

// create directory
client.createDirectory("/a/b/w");
        
// create file and write some content
String filename = "/a/b/c.txt";
OutputStream stream = client.createFile(filename, IfExists.OVERWRITE  );
PrintStream out = new PrintStream(stream);
for (int i = 1; i <= 10; i++) {
    out.println("This is line #" + i);
    out.format("This is the same line (%d), but using formatted output. %n", i);
}
out.close();
```

> [!div class="nextstepaction"]
> [Обзор клиентских API-интерфейсов](/java/api/overview/azure/datalakestore/client)


## <a name="management-api"></a>API управления

Используйте API управления, чтобы управлять учетными записями Data Lake Store, правилами брандмауэра и доверенными поставщиками удостоверений.

[Добавьте зависимость](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) в файл Maven `pom.xml`, чтобы использовать API управления в проекте.


```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-datalake-store</artifactId>
    <version>1.0.0-beta1.3</version>
</dependency>
```

> [!div class="nextstepaction"]
> [Обзор API-интерфейсов управления](/java/api/overview/azure/datalakestore/management)

## <a name="samples"></a>Примеры

[Azure Data Lake Get Started][1] (Приступая к работе с Azure Data Lake) 

[1]: https://github.com/Azure-Samples/data-lake-store-java-upload-download-get-started

Ознакомьтесь с другими [примерами кода Java для Azure Data Lake Store](https://azure.microsoft.com/resources/samples/?platform=java&term=lake), которые можно использовать в приложениях.
