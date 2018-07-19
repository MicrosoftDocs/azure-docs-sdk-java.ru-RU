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
# <a name="redis-cache-libraries-for-java"></a>Библиотеки кэша Redis для Azure для Java

## <a name="overview"></a>Обзор

Кэш Redis для Azure — это безопасное распределенное хранилище пар "ключ-значение" на основе популярного кэша [Redis](https://redis.io/) с открытым исходным кодом. 

Чтобы приступить к работе с кэшем Redis для Azure, см. инструкции по [использованию кэша Redis для Azure с помощью Java](/azure/redis-cache/cache-java-get-started).

## <a name="client-library"></a>Клиентская библиотека

Подключайтесь к кэшу Redis для Azure, чтобы хранить и извлекать значения из кэша с помощью клиента [Jedis](https://github.com/xetorthio/jedis) с открытым исходным кодом.  

[Добавьте зависимость](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) в файл Maven `pom.xml`, чтобы использовать клиентскую библиотеку в проекте.   

```XML
<dependency>
    <groupId>redis.clients</groupId>
    <artifactId>jedis</artifactId>
    <version>2.9.0</version>
    <type>jar</type>
</dependency>
```

## <a name="example"></a>Пример

Подключитесь к кэшу Redis для Azure и вставьте строку в кэш.

```java
JedisShardInfo shardInfo = new JedisShardInfo("<name>.redis.cache.windows.net", 6380, useSsl);
    shardInfo.setPassword("<key>"); /* Use your access key. */
    Jedis jedis = new Jedis(shardInfo);
    jedis.set("foo", "bar");
```

## <a name="management-api"></a>API управления

Создавайте и масштабируйте ресурсы кэша Redis для Azure и управляйте ключами доступа для API управления.

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-redis</artifactId>
    <version>1.3.0</version>
</dependency>
```

## <a name="example"></a>Пример

Создайте кэш Redis для Azure [уровня "Стандартный" в конфигурации с двумя узлами](https://azure.microsoft.com/services/cache/). 

```java
RedisCache cache = azure.redisCaches().define(redisCacheName1)
    .withRegion(Region.US_CENTRAL)
    .withNewResourceGroup(rgName)
    .withStandardSku();
```

> [!div class="nextstepaction"]
> [Обзор API-интерфейсов управления](/java/api/overview/azure/rediscache/management)

## <a name="samples"></a>Примеры

[Управление кэшем Redis для Azure](https://github.com/Azure-Samples/redis-java-manage-cache)   

Ознакомьтесь с [примерами кода Java для кэша Redis для Azure](https://azure.microsoft.com/resources/samples/?platform=java&term=redis), которые можно использовать в своих приложениях.
