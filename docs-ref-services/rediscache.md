---
title: Библиотеки кэша Redis для Azure для Java
description: Справочная документация по клиентским библиотекам Java и библиотекам управления кэша Redis для Azure
keywords: Azure, Java, SDK, API, cache, redis, web cache, key-value, in-memory
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 07/11/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: redis-cache
ms.openlocfilehash: dd03825d9ae7cba32087f92262d5ef213cf3af0b
ms.sourcegitcommit: 49b17bbf34732512f836ee634818f1058147ff5c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2018
ms.locfileid: "31823627"
---
# <a name="redis-cache-libraries-for-java"></a><span data-ttu-id="71199-104">Библиотеки кэша Redis для Azure для Java</span><span class="sxs-lookup"><span data-stu-id="71199-104">Redis Cache libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="71199-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="71199-105">Overview</span></span>

<span data-ttu-id="71199-106">Кэш Redis для Azure — это безопасное распределенное хранилище пар "ключ-значение" на основе популярного кэша [Redis](https://redis.io/) с открытым исходным кодом.</span><span class="sxs-lookup"><span data-stu-id="71199-106">Azure Redis Cache is a secure, distributed key-value store based on the popular open source [Redis](https://redis.io/) cache.</span></span> 

<span data-ttu-id="71199-107">Чтобы приступить к работе с кэшем Redis для Azure, см. инструкции по [использованию кэша Redis для Azure с помощью Java](/azure/redis-cache/cache-java-get-started).</span><span class="sxs-lookup"><span data-stu-id="71199-107">To get started with Azure Redis Cache, see [How to use Azure Redis Cache with Java](/azure/redis-cache/cache-java-get-started).</span></span>

## <a name="client-library"></a><span data-ttu-id="71199-108">Клиентская библиотека</span><span class="sxs-lookup"><span data-stu-id="71199-108">Client library</span></span>

<span data-ttu-id="71199-109">Подключайтесь к кэшу Redis для Azure, чтобы хранить и извлекать значения из кэша с помощью клиента [Jedis](https://github.com/xetorthio/jedis) с открытым исходным кодом.</span><span class="sxs-lookup"><span data-stu-id="71199-109">Connect to Azure Redis Cache and store and retrieve values from the cache using the open-source [Jedis](https://github.com/xetorthio/jedis) client.</span></span>  

<span data-ttu-id="71199-110">[Добавьте зависимость](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) в файл Maven `pom.xml`, чтобы использовать клиентскую библиотеку в проекте.</span><span class="sxs-lookup"><span data-stu-id="71199-110">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the client library in your project.</span></span>   

```XML
<dependency>
    <groupId>redis.clients</groupId>
    <artifactId>jedis</artifactId>
    <version>2.9.0</version>
    <type>jar</type>
</dependency>
```

## <a name="example"></a><span data-ttu-id="71199-111">Пример</span><span class="sxs-lookup"><span data-stu-id="71199-111">Example</span></span>

<span data-ttu-id="71199-112">Подключитесь к кэшу Redis для Azure и вставьте строку в кэш.</span><span class="sxs-lookup"><span data-stu-id="71199-112">Connect to Azure Redis and insert a string into the cache.</span></span>

```java
JedisShardInfo shardInfo = new JedisShardInfo("<name>.redis.cache.windows.net", 6380, useSsl);
    shardInfo.setPassword("<key>"); /* Use your access key. */
    Jedis jedis = new Jedis(shardInfo);
    jedis.set("foo", "bar");
```

## <a name="management-api"></a><span data-ttu-id="71199-113">API управления</span><span class="sxs-lookup"><span data-stu-id="71199-113">Management API</span></span>

<span data-ttu-id="71199-114">Создавайте и масштабируйте ресурсы кэша Redis для Azure и управляйте ключами доступа для API управления.</span><span class="sxs-lookup"><span data-stu-id="71199-114">Create and scale Azure Redis resources and manage access keys to with the management API.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-redis</artifactId>
    <version>1.3.0</version>
</dependency>
```

## <a name="example"></a><span data-ttu-id="71199-115">Пример</span><span class="sxs-lookup"><span data-stu-id="71199-115">Example</span></span>

<span data-ttu-id="71199-116">Создайте кэш Redis для Azure [уровня "Стандартный" в конфигурации с двумя узлами](https://azure.microsoft.com/services/cache/).</span><span class="sxs-lookup"><span data-stu-id="71199-116">Create a new Azure Redis Cache in the [two-node standard tier](https://azure.microsoft.com/services/cache/).</span></span> 

```java
RedisCache cache = azure.redisCaches().define(redisCacheName1)
    .withRegion(Region.US_CENTRAL)
    .withNewResourceGroup(rgName)
    .withStandardSku();
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="71199-117">Обзор API-интерфейсов управления</span><span class="sxs-lookup"><span data-stu-id="71199-117">Explore the Management APIs</span></span>](/java/api/overview/azure/rediscache/management)

## <a name="samples"></a><span data-ttu-id="71199-118">Примеры</span><span class="sxs-lookup"><span data-stu-id="71199-118">Samples</span></span>

[<span data-ttu-id="71199-119">Управление кэшем Redis для Azure</span><span class="sxs-lookup"><span data-stu-id="71199-119">Manage Azure Redis Cache</span></span>](https://github.com/Azure-Samples/redis-java-manage-cache)   

<span data-ttu-id="71199-120">Ознакомьтесь с [примерами кода Java для кэша Redis для Azure](https://azure.microsoft.com/resources/samples/?platform=java&term=redis), которые можно использовать в своих приложениях.</span><span class="sxs-lookup"><span data-stu-id="71199-120">Explore more [sample Java code for Azure Redis Cache](https://azure.microsoft.com/resources/samples/?platform=java&term=redis) you can use in your apps.</span></span>
