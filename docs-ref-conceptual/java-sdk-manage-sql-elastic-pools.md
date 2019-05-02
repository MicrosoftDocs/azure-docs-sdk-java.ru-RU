---
title: Управление эластичными пулами баз данных SQL с помощью Java | Документация Майкрософт
description: Пример кода для создания и настройки баз данных SQL Azure с помощью пакета Azure SDK для Java
author: rloutlaw
manager: douge
ms.assetid: 9b461de8-46bc-4650-8e9e-59531f4e2a53
ms.topic: article
ms.service: Azure
ms.devlang: java
ms.technology: Azure
ms.date: 3/30/2017
ms.author: routlaw;asirveda
ms.openlocfilehash: 59d2601ef21b91a364887fe0548cb95023c79b5e
ms.sourcegitcommit: 115f4c8ad07a11f17d79e9d945d63917836b11c8
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "61592689"
---
# <a name="manage-azure-sql-databases-in-elastic-pools-from-your-java-applications"></a><span data-ttu-id="e615a-103">Управление базами данных SQL Azure в эластичных пулах с помощью приложений Java</span><span class="sxs-lookup"><span data-stu-id="e615a-103">Manage Azure SQL databases in elastic pools from your Java applications</span></span>

<span data-ttu-id="e615a-104">[Этот пример](https://github.com/Azure-Samples/sql-database-java-manage-sql-dbs-in-elastic-pool) создает сервер базы данных SQL с [эластичным пулом](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-pool) для управления ресурсами нескольких баз данных в одном плане и их масштабирования.</span><span class="sxs-lookup"><span data-stu-id="e615a-104">[This sample](https://github.com/Azure-Samples/sql-database-java-manage-sql-dbs-in-elastic-pool) creates a SQL database server with an [elastic pool](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-pool) to manage and scale resources for mulitple databases in a single plan.</span></span>

## <a name="run-the-sample"></a><span data-ttu-id="e615a-105">Запуск примера</span><span class="sxs-lookup"><span data-stu-id="e615a-105">Run the sample</span></span>

<span data-ttu-id="e615a-106">Создайте [файл проверки подлинности](https://github.com/Azure/azure-sdk-for-java/blob/master/AUTH.md), задайте переменную среды `AZURE_AUTH_LOCATION` и укажите полный путь к файлу на компьютере.</span><span class="sxs-lookup"><span data-stu-id="e615a-106">Create an [authentication file](https://github.com/Azure/azure-sdk-for-java/blob/master/AUTH.md) and set an environment variable `AZURE_AUTH_LOCATION` with the full path to the file on your computer.</span></span> <span data-ttu-id="e615a-107">Далее выполните:</span><span class="sxs-lookup"><span data-stu-id="e615a-107">Then run:</span></span>

```
git clone https://github.com/Azure-Samples/sql-database-java-manage-sql-dbs-in-elastic-pool
cd sql-database-java-manage-sql-dbs-in-elastic-pool
mvn clean compile exec:java
```

<span data-ttu-id="e615a-108">[Просмотрите полный пример кода на GitHub](https://github.com/Azure-Samples/sql-database-java-manage-sql-dbs-in-elastic-pool).</span><span class="sxs-lookup"><span data-stu-id="e615a-108">[View the complete code sample on GitHub](https://github.com/Azure-Samples/sql-database-java-manage-sql-dbs-in-elastic-pool)</span></span>

## <a name="authenticate-with-azure"></a><span data-ttu-id="e615a-109">Проверка подлинности с помощью Azure</span><span class="sxs-lookup"><span data-stu-id="e615a-109">Authenticate with Azure</span></span>

[!INCLUDE [auth-include](includes/java-auth-include.md)]

## <a name="create-a-sql-database-server-with-an-elastic-pool"></a><span data-ttu-id="e615a-110">Создание сервера Базы данных SQL с эластичным пулом</span><span class="sxs-lookup"><span data-stu-id="e615a-110">Create a SQL database server with an elastic pool</span></span>

```java
SqlServer sqlServer = azure.sqlServers().define(sqlServerName)
                    .withRegion(Region.US_EAST)
                    .withNewResourceGroup(rgName)
                    .withAdministratorLogin(administratorLogin)
                    .withAdministratorPassword(administratorPassword)
                    // Use ElasticPoolEditions.STANDARD as the edition
                    // and create two databases
                    .withNewElasticPool(elasticPoolName, ElasticPoolEditions.STANDARD, 
                        database1Name, database2Name)
                    .create();
```

<span data-ttu-id="e615a-111">Значения из текущего выпуска см. в [справочнике класса ElasticPoolEditions](https://docs.microsoft.com/java/api/com.microsoft.azure.management.sql._elastic_pool_editions).</span><span class="sxs-lookup"><span data-stu-id="e615a-111">See the [ElasticPoolEditions class reference](https://docs.microsoft.com/java/api/com.microsoft.azure.management.sql._elastic_pool_editions) for current edition values.</span></span> <span data-ttu-id="e615a-112">Чтобы сравнить характеристики ресурсов выпуска, см. [документацию по эластичному пулу баз данных SQL](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-pool).</span><span class="sxs-lookup"><span data-stu-id="e615a-112">Review the [SQL database elastic pool documentation](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-pool) to compare edition resource characteristics.</span></span> 

## <a name="change-database-transaction-unit-dtu-settings-in-an-elastic-pool"></a><span data-ttu-id="e615a-113">Изменение параметров единиц передачи данных (DTU) базы данных в эластичном пуле</span><span class="sxs-lookup"><span data-stu-id="e615a-113">Change Database Transaction Unit (DTU) settings in an elastic pool</span></span>

```java
// Set an pool of 200 eDTUs to share between the databases
// and ensure that a database always has 10 DTUs available but never uses more than 50
elasticPool = elasticPool.update()
                    .withDtu(200)
                    .withDatabaseDtuMin(10)
                    .withDatabaseDtuMax(50)
                    .apply();
```

<span data-ttu-id="e615a-114">Дополнительные сведения о выделении ресурсов для баз данных SQL см. в [документации по DTU и eDTU](https://docs.microsoft.com/azure/sql-database/sql-database-what-is-a-dtu).</span><span class="sxs-lookup"><span data-stu-id="e615a-114">Review the [DTUs and eDTUs documentation](https://docs.microsoft.com/azure/sql-database/sql-database-what-is-a-dtu) to learn more about allocating resources to SQL databases.</span></span>

## <a name="create-a-new-database-and-add-it-to-an-elastic-pool"></a><span data-ttu-id="e615a-115">Создание новой базы данных и ее добавление в эластичный пул</span><span class="sxs-lookup"><span data-stu-id="e615a-115">Create a new database and add it to an elastic pool</span></span>

```java
// Add a newly created database to the elastic pool
SqlDatabase anotherDatabase = sqlServer.databases().define(anotherDatabaseName).create();
elasticPool.update().withExistingDatabase(anotherDatabase).apply();            
```

<span data-ttu-id="e615a-116">В первой инструкции API создает `anotherDatabase` на [уровне S0](https://docs.microsoft.com/azure/sql-database/sql-database-service-tiers).</span><span class="sxs-lookup"><span data-stu-id="e615a-116">The API creates `anotherDatabase` at [S0 tier](https://docs.microsoft.com/azure/sql-database/sql-database-service-tiers) in the first statement.</span></span> <span data-ttu-id="e615a-117">После перемещения `anotherDatabase` в эластичный пул базе данных присваиваются ресурсы на основе параметров пула.</span><span class="sxs-lookup"><span data-stu-id="e615a-117">Moving `anotherDatabase` to the elastic pool assigns the database resources based on the pool settings.</span></span>

## <a name="remove-a-database-from-an-elastic-pool"></a><span data-ttu-id="e615a-118">Удаление базы данных из эластичного пула</span><span class="sxs-lookup"><span data-stu-id="e615a-118">Remove a database from an elastic pool</span></span>
```java
// Assign an edition since the database resources are no longer managed in the pool 
anotherDatabase = anotherDatabase.update()
                     .withoutElasticPool()
                     .withEdition(DatabaseEditions.STANDARD)
                     .apply();
```

<span data-ttu-id="e615a-119">Значения, которые нужно передать в `withEdition()`, см. в [справочнике по классу DatabaseEditions](https://docs.microsoft.com/java/api/com.microsoft.azure.management.sql._database_editions).</span><span class="sxs-lookup"><span data-stu-id="e615a-119">See the [DatabaseEditions class reference](https://docs.microsoft.com/java/api/com.microsoft.azure.management.sql._database_editions) for values to pass to `withEdition()`.</span></span>

## <a name="list-current-database-activities-in-an-elastic-pool"></a><span data-ttu-id="e615a-120">Получение списка текущих действий базы данных в эластичном пуле</span><span class="sxs-lookup"><span data-stu-id="e615a-120">List current database activities in an elastic pool</span></span>
```java
// get a list of in-flight elastic operations on databases in the pool and log them 
for (ElasticPoolDatabaseActivity databaseActivity : elasticPool.listDatabaseActivities()) {
    System.out.println("Database " + databaseActivity.databaseName() 
        + " performing operation " + databaseActivity.operation() + 
        " with objective " + databaseActivity.requestedServiceObjective());
}
```

<span data-ttu-id="e615a-121">Действия базы данных включают перемещение базы данных в эластичный пул или из него и обновление баз данных в эластичном пуле.</span><span class="sxs-lookup"><span data-stu-id="e615a-121">Database activities include moving a database in or out of an elastic pool and updating databases in an elastic pool.</span></span>


## <a name="list-databases-in-an-elastic-pool"></a><span data-ttu-id="e615a-122">Получение списка баз данных в пуле эластичных БД</span><span class="sxs-lookup"><span data-stu-id="e615a-122">List databases in an elastic pool</span></span>
```java
// Log a list of databases in the elastic pool 
for (SqlDatabase databaseInServer : elasticPool.listDatabases()) {
    System.out.println(databaseInServer.name());
}
```

<span data-ttu-id="e615a-123">Инструкции по отправке более подробных запросов к базам данных см. в методах, приведенных в [этой статье](https://docs.microsoft.com/java/api/com.microsoft.azure.management.sql._sql_database).</span><span class="sxs-lookup"><span data-stu-id="e615a-123">Review the methods in [com.microsoft.azure.management.sql.SqlDatabase](https://docs.microsoft.com/java/api/com.microsoft.azure.management.sql._sql_database) to query the databases in more detail.</span></span>

## <a name="delete-an-elastic-pool"></a><span data-ttu-id="e615a-124">Удаление эластичного пула</span><span class="sxs-lookup"><span data-stu-id="e615a-124">Delete an elastic pool</span></span>
```java
sqlServer.elasticPools().delete(elasticPoolName);
```

<span data-ttu-id="e615a-125">Прежде чем удалять эластичный пул, убедитесь, что он пуст.</span><span class="sxs-lookup"><span data-stu-id="e615a-125">The elastic pool must be empty before deleting it.</span></span>

## <a name="sample-code-summary"></a><span data-ttu-id="e615a-126">Сводка примера кода</span><span class="sxs-lookup"><span data-stu-id="e615a-126">Sample code summary.</span></span>

<span data-ttu-id="e615a-127">Пример создает сервер SQL с двумя базами данных, управляемыми в одном эластичном пуле.</span><span class="sxs-lookup"><span data-stu-id="e615a-127">The sample creates a SQL server with two databases managed in a single elasic pool.</span></span> <span data-ttu-id="e615a-128">Ограничения ресурсов для эластичного пула обновляются, а затем в пул добавляются другие базы данных.</span><span class="sxs-lookup"><span data-stu-id="e615a-128">The elastic pool resource limits are updated, then additional databases are added to the pool.</span></span> <span data-ttu-id="e615a-129">Затем код считывает конфигурацию и состояние эластичного пула.</span><span class="sxs-lookup"><span data-stu-id="e615a-129">The code then reads the elastic pool's configuration and state.</span></span> 

<span data-ttu-id="e615a-130">Перед завершением пример удаляет все созданные им ресурсы.</span><span class="sxs-lookup"><span data-stu-id="e615a-130">The sample deletes all resources it created before exiting.</span></span>

| <span data-ttu-id="e615a-131">Класс, используемый в примере</span><span class="sxs-lookup"><span data-stu-id="e615a-131">Class used in sample</span></span> | <span data-ttu-id="e615a-132">Примечания</span><span class="sxs-lookup"><span data-stu-id="e615a-132">Notes</span></span> |
|-------|-------|
| [<span data-ttu-id="e615a-133">SqlServer</span><span class="sxs-lookup"><span data-stu-id="e615a-133">SqlServer</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.sql._sql_server) | <span data-ttu-id="e615a-134">Сервер базы данных SQL в Azure, созданный с помощью текучей цепочки `azure.sqlServers().define()...create()`.</span><span class="sxs-lookup"><span data-stu-id="e615a-134">SQL DB server in Azure created by `azure.sqlServers().define()...create()` fluent chain.</span></span> <span data-ttu-id="e615a-135">Указывает методы для создания эластичных пулов и баз данных и работы с ними.</span><span class="sxs-lookup"><span data-stu-id="e615a-135">Provides methods to create and work with elastic pools and databases.</span></span> 
| [<span data-ttu-id="e615a-136">SqlDatabase</span><span class="sxs-lookup"><span data-stu-id="e615a-136">SqlDatabase</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.sql._sql_database) | <span data-ttu-id="e615a-137">Объект на стороне клиента, представляющий базу данных SQL.</span><span class="sxs-lookup"><span data-stu-id="e615a-137">Client side object representing a SQL database.</span></span> <span data-ttu-id="e615a-138">Создан с помощью команды `sqlServer().define()...create()`.</span><span class="sxs-lookup"><span data-stu-id="e615a-138">Created through `sqlServer().define()...create()`.</span></span> 
| [<span data-ttu-id="e615a-139">DatabaseEditions</span><span class="sxs-lookup"><span data-stu-id="e615a-139">DatabaseEditions</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.sql._database_editions) | <span data-ttu-id="e615a-140">Постоянные статические поля, используемые для настройки ресурсов базы данных при создании базы данных за пределами эластичного пула или при перемещении базы данных за пределы эластичного пула.</span><span class="sxs-lookup"><span data-stu-id="e615a-140">Constant static fields used to set database resources when creating a database outside of an elastic pool or when moving a database out of an elastic pool</span></span>  
| [<span data-ttu-id="e615a-141">SqlElasticPool</span><span class="sxs-lookup"><span data-stu-id="e615a-141">SqlElasticPool</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.sql._sql_elastic_pool) | <span data-ttu-id="e615a-142">Создан из раздела `withNewElasticPool()` текучей цепочки, которая создала сервер SQL Server в Azure.</span><span class="sxs-lookup"><span data-stu-id="e615a-142">Created from the `withNewElasticPool()` section of the fluent chain that created the SqlServer in Azure.</span></span> <span data-ttu-id="e615a-143">Указывает методы для задания ограничений ресурсов для баз данных, запущенных в эластичном пуле, и для самого пула.</span><span class="sxs-lookup"><span data-stu-id="e615a-143">Provides methods to set resource limits for databases running in the elastic pool and for the elastic pool itself.</span></span> 
| [<span data-ttu-id="e615a-144">ElasticPoolEditions</span><span class="sxs-lookup"><span data-stu-id="e615a-144">ElasticPoolEditions</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.sql._elastic_pool_editions) | <span data-ttu-id="e615a-145">Класс постоянных полей, определяющий ресурсы, доступные для эластичного пула.</span><span class="sxs-lookup"><span data-stu-id="e615a-145">Class of constant fields defining the resources available to an elastic pool.</span></span> <span data-ttu-id="e615a-146">Сведения об уровне см в [документации по эластичному пулу базы данных SQL](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-pool).</span><span class="sxs-lookup"><span data-stu-id="e615a-146">See [SQL database elastic pool documentation](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-pool) for tier details.</span></span> 
| [<span data-ttu-id="e615a-147">ElasticPoolDatabaseActivity</span><span class="sxs-lookup"><span data-stu-id="e615a-147">ElasticPoolDatabaseActivity</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.sql._elastic_pool_database_activity) | <span data-ttu-id="e615a-148">Получен из `SqlElasticPool.listDatabaseActivities()`.</span><span class="sxs-lookup"><span data-stu-id="e615a-148">Retreived from `SqlElasticPool.listDatabaseActivities()`.</span></span> <span data-ttu-id="e615a-149">Каждый объект этого типа представляет действие, примененное к базе данных в эластичном пуле.</span><span class="sxs-lookup"><span data-stu-id="e615a-149">Each object of this type represents an activity performed on a database in the elastic pool.</span></span>
| [<span data-ttu-id="e615a-150">ElasticPoolActivity</span><span class="sxs-lookup"><span data-stu-id="e615a-150">ElasticPoolActivity</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.sql._elastic_pool_activity) | <span data-ttu-id="e615a-151">Извлечен в виде списка из `SqlElasticPool.listActivities()`.</span><span class="sxs-lookup"><span data-stu-id="e615a-151">Retrieved in a List from `SqlElasticPool.listActivities()`.</span></span> <span data-ttu-id="e615a-152">Каждый объект в списке представляет действие, примененное к эластичному пулу (а не к базам данных в эластичном пуле).</span><span class="sxs-lookup"><span data-stu-id="e615a-152">Each of object in the list represents an activity performed on the elastic pool (not the databases in the elastic pool).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e615a-153">Дополнительная информация</span><span class="sxs-lookup"><span data-stu-id="e615a-153">Next steps</span></span>

[!INCLUDE [next-steps](includes/java-next-steps.md)]