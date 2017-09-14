---
title: "Заметки о выпуске библиотек управления Azure для Java | Документация Майкрософт"
description: "Узнайте о новых возможностях и критически важных изменениях в библиотеках управления Azure для Java"
keywords: Azure, Java, API, reference, notes, updates, deprecate
author: routlaw
manager: douge
ms.assetid: 1f128cf9-f747-4344-84e1-f9964709deb8
ms.service: Azure
ms.devlang: java
ms.topic: reference
ms.technology: Azure
ms.date: 3/06/2016
ms.openlocfilehash: c0d5c4b3702d3bee4e93de51cec36e72aeaf598f
ms.sourcegitcommit: ae39830d5a54fedceac78d8df1718e77741e03fa
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/09/2017
---
# <a name="release-notes"></a><span data-ttu-id="fc23e-104">Заметки о выпуске</span><span class="sxs-lookup"><span data-stu-id="fc23e-104">Release Notes</span></span> 

## <a name="june-30-2017---110"></a><span data-ttu-id="fc23e-105">30 июня 2017 г. — 1.1.0</span><span class="sxs-lookup"><span data-stu-id="fc23e-105">June 30, 2017 - 1.1.0</span></span> 

<span data-ttu-id="fc23e-106">Версия 1.1 имеет обратную совместимость с версией 1.0 в API-интерфейсах, предназначенных для широкого использования, которые стали общедоступными (стабильными) в версии 1.0.</span><span class="sxs-lookup"><span data-stu-id="fc23e-106">V1.1 is backwards compatible with V1.0 in the APIs intended for public use that reached the general availability (stable) stage in V1.0.</span></span>

<span data-ttu-id="fc23e-107">В API-интерфейсы, отмеченные заметкой @Beta в версии 1.0, внесены некоторые критически важные изменения.</span><span class="sxs-lookup"><span data-stu-id="fc23e-107">Some breaking changes were introduced in APIs marked with the @Beta annotation in V.0</span></span>

<span data-ttu-id="fc23e-108">При переносе кода в версию 1.1.0 ознакомьтесь с [этими заметками](https://github.com/Azure/azure-sdk-for-java/blob/master/notes/prepare-for-1.1.0.md) по подготовке кода версии 1.0.0 к версии 1.1.0.</span><span class="sxs-lookup"><span data-stu-id="fc23e-108">If you are migrating your code to 1.1.0, you can use [these notes](https://github.com/Azure/azure-sdk-for-java/blob/master/notes/prepare-for-1.1.0.md) for preparing your code for 1.1.0 from 1.0.0.</span></span>

### <a name="generally-availabile-in-v11"></a><span data-ttu-id="fc23e-109">Общедоступные возможности в версии 1.1</span><span class="sxs-lookup"><span data-stu-id="fc23e-109">Generally availabile in V1.1</span></span>

<span data-ttu-id="fc23e-110">Некоторые API-интерфейсы в версии 1.0, которые были доступны в бета-версии, теперь являются общедоступными в версии 1.1, в частности:</span><span class="sxs-lookup"><span data-stu-id="fc23e-110">Some of the APIs that were still in Beta in V1.0 are now GA in V1.1, in particular:</span></span>

- <span data-ttu-id="fc23e-111">асинхронные методы;</span><span class="sxs-lookup"><span data-stu-id="fc23e-111">async methods</span></span>
- <span data-ttu-id="fc23e-112">все методы в CDN, которые ранее были доступны в бета-версии;</span><span class="sxs-lookup"><span data-stu-id="fc23e-112">all methods in CDN that were previously in Beta</span></span>
- <span data-ttu-id="fc23e-113">все методы и интерфейсы шлюзов приложений, которые ранее были доступны в бета-версии.</span><span class="sxs-lookup"><span data-stu-id="fc23e-113">all methods and interfaces in Application Gateways that were previously in Beta</span></span>

 <span data-ttu-id="fc23e-114">Некоторые элементы библиотеки все еще находятся на стадии предварительной версии.</span><span class="sxs-lookup"><span data-stu-id="fc23e-114">Some parts of the library are still in Preview.</span></span> <span data-ttu-id="fc23e-115">Текущее состояние библиотек см. в таблице ниже.</span><span class="sxs-lookup"><span data-stu-id="fc23e-115">Refer to the table below for the current state of the libraries:</span></span>

<span data-ttu-id="fc23e-116">Служба или компонент</span><span class="sxs-lookup"><span data-stu-id="fc23e-116">Service or feature</span></span> | <span data-ttu-id="fc23e-117">Доступны в общедоступной версии</span><span class="sxs-lookup"><span data-stu-id="fc23e-117">Available as GA</span></span> | <span data-ttu-id="fc23e-118">Доступны в предварительной версии</span><span class="sxs-lookup"><span data-stu-id="fc23e-118">Available as Preview</span></span>  | <span data-ttu-id="fc23e-119">Скоро</span><span class="sxs-lookup"><span data-stu-id="fc23e-119">Coming soon</span></span> |
---------|---------|---------|---------|
<span data-ttu-id="fc23e-120">Среда выполнения приложений</span><span class="sxs-lookup"><span data-stu-id="fc23e-120">Compute</span></span>  | <span data-ttu-id="fc23e-121">Виртуальные машины и расширения виртуальных машин, масштабируемые наборы виртуальных машин, управляемые диски</span><span class="sxs-lookup"><span data-stu-id="fc23e-121">Virtual machines and VM extensions, Virtual machine scale sets, managed disks</span></span>   | <span data-ttu-id="fc23e-122">Служба контейнеров Azure, реестр контейнеров Azure</span><span class="sxs-lookup"><span data-stu-id="fc23e-122">Azure container service, Azure container registry</span></span> |    |
<span data-ttu-id="fc23e-123">Хранилище</span><span class="sxs-lookup"><span data-stu-id="fc23e-123">Storage</span></span>   |  <span data-ttu-id="fc23e-124">учетные записи хранения;</span><span class="sxs-lookup"><span data-stu-id="fc23e-124">Storage accounts</span></span>       |         |   <span data-ttu-id="fc23e-125">Шифрование</span><span class="sxs-lookup"><span data-stu-id="fc23e-125">Encryption</span></span>      |
<span data-ttu-id="fc23e-126">База данных SQL</span><span class="sxs-lookup"><span data-stu-id="fc23e-126">SQL Database</span></span>  | <span data-ttu-id="fc23e-127">Базы данных, брандмауэры, эластичные пулы</span><span class="sxs-lookup"><span data-stu-id="fc23e-127">Databases, firewalls, elastic pools</span></span>        |         |   <span data-ttu-id="fc23e-128">Дополнительные компоненты</span><span class="sxs-lookup"><span data-stu-id="fc23e-128">More features</span></span>      |
<span data-ttu-id="fc23e-129">Сеть</span><span class="sxs-lookup"><span data-stu-id="fc23e-129">Networking</span></span>    |  <span data-ttu-id="fc23e-130">Виртуальные сети, сетевые интерфейсы, IP-адреса, таблицы маршрутизации, группы безопасности сети, DNS, диспетчеры трафика, шлюзы приложений</span><span class="sxs-lookup"><span data-stu-id="fc23e-130">Virtual networks , network interfaces , IP addresses ,routing tables, network security groups , DNS, Traffic managers, Application gateways</span></span>  |    <span data-ttu-id="fc23e-131">Балансировщики нагрузки</span><span class="sxs-lookup"><span data-stu-id="fc23e-131">Load balancers</span></span>     |   <span data-ttu-id="fc23e-132">VPN, наблюдатели за сетями</span><span class="sxs-lookup"><span data-stu-id="fc23e-132">VPN, Network watchers</span></span>   |
<span data-ttu-id="fc23e-133">Дополнительные службы</span><span class="sxs-lookup"><span data-stu-id="fc23e-133">More services</span></span>    |  <span data-ttu-id="fc23e-134">Диспетчер ресурсов, хранилище ключей, Redis, CDN, пакетная служба</span><span class="sxs-lookup"><span data-stu-id="fc23e-134">Resource Manager, Key Vault, Redis,  CDN, Batch</span></span>       |  <span data-ttu-id="fc23e-135">Веб-приложения, приложения-функции, служебная шина, управление доступом на основе ролей Graph, DocumentDB</span><span class="sxs-lookup"><span data-stu-id="fc23e-135">Web apps, Function apps, Service Bus, Graph RBAC, DocumentDB</span></span>   | <span data-ttu-id="fc23e-136">Monitor, планировщик, управление Функциями, Поиск, дополнительные возможности для управления доступом на основе ролей Graph</span><span class="sxs-lookup"><span data-stu-id="fc23e-136">Monitor ,Scheduler, Functions management, Search, more Graph RBAC features</span></span>        |
<span data-ttu-id="fc23e-137">Основные компоненты</span><span class="sxs-lookup"><span data-stu-id="fc23e-137">Fundamentals</span></span>     |   <span data-ttu-id="fc23e-138">Базовая проверка подлинности, асинхронные методы</span><span class="sxs-lookup"><span data-stu-id="fc23e-138">Authentication - core , Async methods</span></span>       |      |         |

### <a name="import-with-maven"></a><span data-ttu-id="fc23e-139">Импорт с помощью Maven</span><span class="sxs-lookup"><span data-stu-id="fc23e-139">Import with Maven</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure</artifactId>
    <version>1.2.1</version>
</dependency>
```

### <a name="get-help-and-give-feedback"></a><span data-ttu-id="fc23e-140">Справка и отзывы</span><span class="sxs-lookup"><span data-stu-id="fc23e-140">Get help and give feedback</span></span>

<span data-ttu-id="fc23e-141">Обратитесь к сообществу [Stack Overflow](http://stackoverflow.com/questions/tagged/azure-java-sdk), чтобы получить справку по использованию библиотек в вашем коде.</span><span class="sxs-lookup"><span data-stu-id="fc23e-141">Check out the [Stack Overflow](http://stackoverflow.com/questions/tagged/azure-java-sdk) community for help using the libraries in your own code.</span></span> <span data-ttu-id="fc23e-142">Если у вас возникли ошибки или есть предложения по улучшению этих библиотек, сообщите о них на сайте [GitHub](https://github.com/Azure/azure-sdk-for-java/issues).</span><span class="sxs-lookup"><span data-stu-id="fc23e-142">If you encounter any bugs or have suggestions to improve these libraries, please file issues via [GitHub](https://github.com/Azure/azure-sdk-for-java/issues).</span></span>

### <a name="migrate-from-previous-releases"></a><span data-ttu-id="fc23e-143">Переход с предыдущих версий</span><span class="sxs-lookup"><span data-stu-id="fc23e-143">Migrate from previous releases</span></span>

<span data-ttu-id="fc23e-144">[Переход с версии 1.0.0-beta5](https://github.com/Azure/azure-sdk-for-java/blob/master/notes/prepare-for-1.0.0.md) [Переход с версии 1.1.0](https://github.com/Azure/azure-sdk-for-java/blob/master/notes/prepare-for-1.1.0.md)</span><span class="sxs-lookup"><span data-stu-id="fc23e-144">[Migrate from 1.0.0-beta5](https://github.com/Azure/azure-sdk-for-java/blob/master/notes/prepare-for-1.0.0.md)  [Migrate from 1.1.0](https://github.com/Azure/azure-sdk-for-java/blob/master/notes/prepare-for-1.1.0.md)</span></span>


