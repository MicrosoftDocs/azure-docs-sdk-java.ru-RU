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
# <a name="azure-data-lake-store-libraries-for-java"></a><span data-ttu-id="9a040-104">Библиотеки Azure Data Lake Store для Java</span><span class="sxs-lookup"><span data-stu-id="9a040-104">Azure Data Lake Store libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="9a040-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="9a040-105">Overview</span></span>

<span data-ttu-id="9a040-106">Используйте [Azure Data Lake Store](/azure/data-lake-store/data-lake-store-overview) для централизованного сбора данных любого размера, типа и с любой скоростью приема для ведения аналитики.</span><span class="sxs-lookup"><span data-stu-id="9a040-106">Capture data of any size, type, and ingestion speed in a single place for analytics with [Azure Data Lake Store](/azure/data-lake-store/data-lake-store-overview).</span></span>

<span data-ttu-id="9a040-107">Чтобы приступить к работе с Data Lake Store, ознакомьтесь со статьей [Начало работы с хранилищем озера данных Azure с помощью Java](/azure/data-lake-store/data-lake-store-get-started-java-sdk).</span><span class="sxs-lookup"><span data-stu-id="9a040-107">To get started with Data Lake Store, see [Get started with Azure Data Lake Store using Java](/azure/data-lake-store/data-lake-store-get-started-java-sdk).</span></span>


## <a name="client-library"></a><span data-ttu-id="9a040-108">Клиентская библиотека</span><span class="sxs-lookup"><span data-stu-id="9a040-108">Client library</span></span>

<span data-ttu-id="9a040-109">Выполняйте чтение и запись файлов, задавайте разрешения и метаданные и управляйте файлами и каталогами в Data Lake Store с помощью клиентской библиотеки.</span><span class="sxs-lookup"><span data-stu-id="9a040-109">Read and write files, set permissions and metadata, and manage files and directories in Data Lake Store with the client library.</span></span>

<span data-ttu-id="9a040-110">[Добавьте зависимость](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) в файл Maven `pom.xml`, чтобы использовать клиентскую библиотеку в проекте.</span><span class="sxs-lookup"><span data-stu-id="9a040-110">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the client library in your project.</span></span>

```XML
<dependency>
   <groupId>com.microsoft.azure</groupId>
   <artifactId>azure-data-lake-store-sdk</artifactId>
   <version>2.1.5</version>
</dependency>
```   

## <a name="example"></a><span data-ttu-id="9a040-111">Пример</span><span class="sxs-lookup"><span data-stu-id="9a040-111">Example</span></span>

<span data-ttu-id="9a040-112">Создайте клиент Data Lake с полным доменным именем и маркером доступа OAuth2, а затем создайте файл в Data Lake и запишите данные в него.</span><span class="sxs-lookup"><span data-stu-id="9a040-112">Create a Data Lake client from a fully qualified domain name and OAuth2 access token, then create a file in Data Lake and write to it.</span></span>

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
> [<span data-ttu-id="9a040-113">Обзор клиентских API-интерфейсов</span><span class="sxs-lookup"><span data-stu-id="9a040-113">Explore the Client APIs</span></span>](/java/api/overview/azure/datalakestore/client)


## <a name="management-api"></a><span data-ttu-id="9a040-114">API управления</span><span class="sxs-lookup"><span data-stu-id="9a040-114">Management API</span></span>

<span data-ttu-id="9a040-115">Используйте API управления, чтобы управлять учетными записями Data Lake Store, правилами брандмауэра и доверенными поставщиками удостоверений.</span><span class="sxs-lookup"><span data-stu-id="9a040-115">Use the management API to manage Data Lake Store accounts, firewall rules, and trusted identity providers.</span></span>

<span data-ttu-id="9a040-116">[Добавьте зависимость](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) в файл Maven `pom.xml`, чтобы использовать API управления в проекте.</span><span class="sxs-lookup"><span data-stu-id="9a040-116">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the management API in your project.</span></span>


```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-datalake-store</artifactId>
    <version>1.0.0-beta1.3</version>
</dependency>
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="9a040-117">Обзор API-интерфейсов управления</span><span class="sxs-lookup"><span data-stu-id="9a040-117">Explore the Management APIs</span></span>](/java/api/overview/azure/datalakestore/management)

## <a name="samples"></a><span data-ttu-id="9a040-118">Примеры</span><span class="sxs-lookup"><span data-stu-id="9a040-118">Samples</span></span>

<span data-ttu-id="9a040-119">[Azure Data Lake Get Started][1] (Приступая к работе с Azure Data Lake)</span><span class="sxs-lookup"><span data-stu-id="9a040-119">[Azure Data Lake Get Started][1]</span></span> 

[1]: https://github.com/Azure-Samples/data-lake-store-java-upload-download-get-started

<span data-ttu-id="9a040-120">Ознакомьтесь с другими [примерами кода Java для Azure Data Lake Store](https://azure.microsoft.com/resources/samples/?platform=java&term=lake), которые можно использовать в приложениях.</span><span class="sxs-lookup"><span data-stu-id="9a040-120">Explore more [sample Java code for Azure Data Lake Store](https://azure.microsoft.com/resources/samples/?platform=java&term=lake) you can use in your apps.</span></span>
