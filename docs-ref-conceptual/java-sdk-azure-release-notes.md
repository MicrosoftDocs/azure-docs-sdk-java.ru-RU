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
ms.openlocfilehash: 924ccf9bdaad4bc635f133adbcfcc8f797d06644
ms.sourcegitcommit: acc83bb537d77568b2a5427479d6354d6ae30885
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/03/2017
---
# <a name="release-notes"></a><span data-ttu-id="9245a-104">Заметки о выпуске</span><span class="sxs-lookup"><span data-stu-id="9245a-104">Release Notes</span></span> 

## <a name="october-5-2017---130"></a><span data-ttu-id="9245a-105">5 октября 2017 г. — 1.3.0</span><span class="sxs-lookup"><span data-stu-id="9245a-105">October 5, 2017 - 1.3.0</span></span> 

<span data-ttu-id="9245a-106">Версия 1.3.0 имеет обратную совместимость с предыдущими версиями для использования со службами и функциями, которые в предыдущих выпусках предоставляются в общедоступной (стабильной) версии.</span><span class="sxs-lookup"><span data-stu-id="9245a-106">Version 1.3.0 is backwards compatible with previous versions for services and features use that reached the general availability (stable) stage in previous releases.</span></span>

<span data-ttu-id="9245a-107">Все критические изменения, внесенные в предварительные версии этих служб, сопровождаются пометкой @Beta.</span><span class="sxs-lookup"><span data-stu-id="9245a-107">Any breaking changes from Preview versions for those services are marked with the @Beta annotation.</span></span>

<span data-ttu-id="9245a-108">Если вы переносите код в версию 1.3.0, ознакомьтесь с [этими заметками](https://github.com/Azure/azure-sdk-for-java/blob/master/notes/prepare-for-1.3.0.md), чтобы подготовить код версии 1.0.0 к изменению до версии 1.3.</span><span class="sxs-lookup"><span data-stu-id="9245a-108">If you are migrating your code to 1.3.0, you can use [these notes](https://github.com/Azure/azure-sdk-for-java/blob/master/notes/prepare-for-1.3.0.md) to prepare your existing code for the 1.3 version.</span></span>

### <a name="generally-availabile-in-v13"></a><span data-ttu-id="9245a-109">Общедоступные возможности в версии 3.1</span><span class="sxs-lookup"><span data-stu-id="9245a-109">Generally availabile in V1.3</span></span>

<span data-ttu-id="9245a-110">Некоторые API-интерфейсы, доступные в бета-версии, теперь предоставляются как общедоступные. Сюда входят:</span><span class="sxs-lookup"><span data-stu-id="9245a-110">Some of the APIs that were still in Beta in previous releases are now GA, in particular:</span></span>

- <span data-ttu-id="9245a-111">асинхронные методы;</span><span class="sxs-lookup"><span data-stu-id="9245a-111">async methods</span></span>
- <span data-ttu-id="9245a-112">все методы в CDN, которые ранее были доступны в бета-версии;</span><span class="sxs-lookup"><span data-stu-id="9245a-112">all methods in CDN that were previously in Beta</span></span>
- <span data-ttu-id="9245a-113">все методы и интерфейсы шлюзов приложений, которые ранее были доступны в бета-версии.</span><span class="sxs-lookup"><span data-stu-id="9245a-113">all methods and interfaces in Application Gateways that were previously in Beta</span></span>

 <span data-ttu-id="9245a-114">Некоторые элементы библиотеки все еще находятся на стадии предварительной версии.</span><span class="sxs-lookup"><span data-stu-id="9245a-114">Some parts of the library are still in Preview.</span></span> <span data-ttu-id="9245a-115">Текущее состояние библиотек см. в таблице ниже.</span><span class="sxs-lookup"><span data-stu-id="9245a-115">Refer to the table below for the current state of the libraries:</span></span>

<span data-ttu-id="9245a-116">Служба или компонент</span><span class="sxs-lookup"><span data-stu-id="9245a-116">Service or feature</span></span> | <span data-ttu-id="9245a-117">Доступны в общедоступной версии</span><span class="sxs-lookup"><span data-stu-id="9245a-117">Available as GA</span></span> | <span data-ttu-id="9245a-118">Доступны в предварительной версии</span><span class="sxs-lookup"><span data-stu-id="9245a-118">Available as Preview</span></span> 
---------|---------|---------|-
<span data-ttu-id="9245a-119">Среда выполнения приложений</span><span class="sxs-lookup"><span data-stu-id="9245a-119">Compute</span></span>  | <span data-ttu-id="9245a-120">Виртуальные машины и расширения виртуальных машин, масштабируемые наборы виртуальных машин, управляемые диски</span><span class="sxs-lookup"><span data-stu-id="9245a-120">Virtual machines and VM extensions, Virtual machine scale sets, managed disks</span></span>   | <span data-ttu-id="9245a-121">Служба контейнеров Azure, реестр контейнеров Azure</span><span class="sxs-lookup"><span data-stu-id="9245a-121">Azure container service, Azure container registry</span></span> 
<span data-ttu-id="9245a-122">Хранилище</span><span class="sxs-lookup"><span data-stu-id="9245a-122">Storage</span></span>   |  <span data-ttu-id="9245a-123">учетные записи хранения;</span><span class="sxs-lookup"><span data-stu-id="9245a-123">Storage accounts</span></span>       |    <span data-ttu-id="9245a-124">Шифрование</span><span class="sxs-lookup"><span data-stu-id="9245a-124">Encryption</span></span>     
<span data-ttu-id="9245a-125">База данных SQL</span><span class="sxs-lookup"><span data-stu-id="9245a-125">SQL Database</span></span>  | <span data-ttu-id="9245a-126">Базы данных, брандмауэры, эластичные пулы</span><span class="sxs-lookup"><span data-stu-id="9245a-126">Databases, firewalls, elastic pools</span></span>              
<span data-ttu-id="9245a-127">Сеть</span><span class="sxs-lookup"><span data-stu-id="9245a-127">Networking</span></span>    |  <span data-ttu-id="9245a-128">Виртуальные сети, сетевые интерфейсы, IP-адреса, таблицы маршрутизации, группы безопасности сети, DNS, диспетчеры трафика, шлюзы приложений</span><span class="sxs-lookup"><span data-stu-id="9245a-128">Virtual networks , network interfaces , IP addresses ,routing tables, network security groups , DNS, Traffic managers, Application gateways</span></span>  |    <span data-ttu-id="9245a-129">подсистемы балансировки нагрузки, пиринги сетей, шлюзы виртуальных сетей, наблюдатели за сетями;</span><span class="sxs-lookup"><span data-stu-id="9245a-129">Load balancers, Network peering, Virtual Network Gateway, Network watchers</span></span> 
<span data-ttu-id="9245a-130">Другие службы</span><span class="sxs-lookup"><span data-stu-id="9245a-130">More services</span></span>    |  <span data-ttu-id="9245a-131">Диспетчер ресурсов, хранилище ключей, Redis, CDN, пакетная служба</span><span class="sxs-lookup"><span data-stu-id="9245a-131">Resource Manager, Key Vault, Redis,  CDN, Batch</span></span>       |  <span data-ttu-id="9245a-132">веб-приложения, приложения-функции, служебные шины, Graph RBAC, Cosmos DB, служба поиска;</span><span class="sxs-lookup"><span data-stu-id="9245a-132">Web apps, Function apps, Service Bus, Graph RBAC, Cosmos DB, Search</span></span>  
<span data-ttu-id="9245a-133">Основы</span><span class="sxs-lookup"><span data-stu-id="9245a-133">Fundamentals</span></span>     |   <span data-ttu-id="9245a-134">базовая идентификация, асинхронные методы, удостоверения управляемой службы.</span><span class="sxs-lookup"><span data-stu-id="9245a-134">Authentication - core , Async methods , Managed Service Identity</span></span>      |      |

> <span data-ttu-id="9245a-135">Функции, доступные в режиме предварительной версии, сопровождаются пометкой `@Beta` на уровне класса, интерфейса или метода в библиотеках.</span><span class="sxs-lookup"><span data-stu-id="9245a-135">Preview features are marked with a `@Beta` annotation at the class or interface or method level in libraries.</span></span> <span data-ttu-id="9245a-136">Эти функции могут измениться.</span><span class="sxs-lookup"><span data-stu-id="9245a-136">These features are subject to change.</span></span> <span data-ttu-id="9245a-137">В будущем они могут быть изменены любым образом (или даже удалены).</span><span class="sxs-lookup"><span data-stu-id="9245a-137">They can be modified in any way, or even removed, in the future.</span></span>

### <a name="import-with-maven"></a><span data-ttu-id="9245a-138">Импорт с помощью Maven</span><span class="sxs-lookup"><span data-stu-id="9245a-138">Import with Maven</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure</artifactId>
    <version>1.3.0</version>
</dependency>
```

### <a name="get-help-and-give-feedback"></a><span data-ttu-id="9245a-139">Справка и отзывы</span><span class="sxs-lookup"><span data-stu-id="9245a-139">Get help and give feedback</span></span>

<span data-ttu-id="9245a-140">Обратитесь к сообществу [Stack Overflow](http://stackoverflow.com/questions/tagged/azure-java-sdk), чтобы получить справку по использованию библиотек в вашем коде.</span><span class="sxs-lookup"><span data-stu-id="9245a-140">Check out the [Stack Overflow](http://stackoverflow.com/questions/tagged/azure-java-sdk) community for help using the libraries in your own code.</span></span> <span data-ttu-id="9245a-141">Если у вас возникли ошибки или есть предложения по улучшению этих библиотек, сообщите о них на сайте [GitHub](https://github.com/Azure/azure-sdk-for-java/issues).</span><span class="sxs-lookup"><span data-stu-id="9245a-141">If you encounter any bugs or have suggestions to improve these libraries, please file issues via [GitHub](https://github.com/Azure/azure-sdk-for-java/issues).</span></span>


