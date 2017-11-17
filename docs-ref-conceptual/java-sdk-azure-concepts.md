---
title: "Библиотеки управления Azure для Java: принципы использования и шаблоны"
description: 
keywords: Azure, Java, SDK, API, Maven, Gradle, authentication, active directory, service principal
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 04/16/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: multiple
ms.assetid: f452468b-7aae-4944-abad-0b1aaf19170d
ms.openlocfilehash: 052c4de1e8f9ff0ece5f36d1c3514bad8c04cfec
ms.sourcegitcommit: 1500f341a96d9da461c288abf4baf79f494ae662
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/28/2017
---
# <a name="azure-management-library-concepts"></a><span data-ttu-id="f06bb-103">Библиотеки управления Azure: принципы использования</span><span class="sxs-lookup"><span data-stu-id="f06bb-103">Azure management library concepts</span></span>

## <a name="build-resources-through-a-fluent-interface"></a><span data-ttu-id="f06bb-104">Создание ресурсов с помощью текучего API</span><span class="sxs-lookup"><span data-stu-id="f06bb-104">Build resources through a fluent interface</span></span>

<span data-ttu-id="f06bb-105">Текучий API — это шаблон, который создает объекты с использованием цепочки методов, правильно настраивающей атрибуты объекта.</span><span class="sxs-lookup"><span data-stu-id="f06bb-105">A fluent interface is a pattern that creates objects using a method chain that correctly configures the object's attributes.</span></span> <span data-ttu-id="f06bb-106">Например, создайте учетную запись хранения Azure:</span><span class="sxs-lookup"><span data-stu-id="f06bb-106">For example, to create a new Azure Storage account</span></span>

```java
StorageAccount storage = azure.storageAccounts().define(storageAccountName)
    .withRegion(region)
    .withNewResourceGroup(resourceGroup)
    .create();
```

<span data-ttu-id="f06bb-107">При выполнении цепочки методов ваша среда IDE предлагает для вызова следующий метод в процессе текучего обмена данными.</span><span class="sxs-lookup"><span data-stu-id="f06bb-107">As you go through the method chain, your IDE suggests the next method to call in the fluent conversation.</span></span>   

![GIF-изображение: выполнение команды IntelliJ в текучей цепочке](media/intelliJFluent.gif)

<span data-ttu-id="f06bb-109">Помещайте в цепочку методы, предлагаемые IDE, до тех пор, пока это требуется для определяемого ресурса Azure.</span><span class="sxs-lookup"><span data-stu-id="f06bb-109">Chain the methods suggested by the IDE as long as they make sense for the Azure resource being defined.</span></span> <span data-ttu-id="f06bb-110">Если вы пропустите обязательный метод в цепочке, IDE выделит его, отметив как ошибку.</span><span class="sxs-lookup"><span data-stu-id="f06bb-110">If you are missing a required method in the chain your IDE will highlight it with an error.</span></span>

## <a name="resource-collections"></a><span data-ttu-id="f06bb-111">Коллекции ресурсов</span><span class="sxs-lookup"><span data-stu-id="f06bb-111">Resource collections</span></span>

<span data-ttu-id="f06bb-112">У библиотеки управления есть единая точка входа через объект `com.microsoft.azure.management.Azure` верхнего уровня для создания и обновления ресурсов.</span><span class="sxs-lookup"><span data-stu-id="f06bb-112">The management library has a single point of entry through the top-level `com.microsoft.azure.management.Azure` object to create and update resources.</span></span> <span data-ttu-id="f06bb-113">Выберите тип ресурсов для работы, используя методы коллекций ресурсов, определенные в объекте `Azure`.</span><span class="sxs-lookup"><span data-stu-id="f06bb-113">Select which type of resources to work with using the resource collection methods defined in the `Azure` object.</span></span> <span data-ttu-id="f06bb-114">Например, база данных SQL:</span><span class="sxs-lookup"><span data-stu-id="f06bb-114">For example, SQL Database:</span></span>

```java
SqlServer sqlServer = azure.sqlServers().define(sqlServerName)
    .withRegion(Region.US_EAST)
    .withNewResourceGroup(rgName)
    .withAdministratorLogin(administratorLogin)
    .withAdministratorPassword(administratorPassword)
    .create();
```

## <a name="lists-and-iterations"></a><span data-ttu-id="f06bb-115">Списки и итерации</span><span class="sxs-lookup"><span data-stu-id="f06bb-115">Lists and iterations</span></span>

<span data-ttu-id="f06bb-116">Каждая коллекция ресурсов использует метод `list()`, который возвращает каждый экземпляр этого ресурса в текущей подписке.</span><span class="sxs-lookup"><span data-stu-id="f06bb-116">Each resource collection has a `list()` method to return every instance of that resource in your current subscription.</span></span> <span data-ttu-id="f06bb-117">Например, `azure.sqlServers().list()` возвращает все базы данных SQL в подписке.</span><span class="sxs-lookup"><span data-stu-id="f06bb-117">For example, `azure.sqlServers().list()` returns all SQL databases in the subscription.</span></span>

<span data-ttu-id="f06bb-118">Используйте метод `listByResourceGroup(String groupname)`, чтобы ограничить возвращаемый список определенной [группой ресурсов Azure](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups).</span><span class="sxs-lookup"><span data-stu-id="f06bb-118">Use the `listByResourceGroup(String groupname)` method to scope the returned List to a specific [Azure resource group](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups).</span></span>  

<span data-ttu-id="f06bb-119">Выполняйте поиск и итерацию для возвращаемой коллекции `PagedList<T>` так же, как для обычного списка `List<T>`:</span><span class="sxs-lookup"><span data-stu-id="f06bb-119">Search and iterate over the returned `PagedList<T>` collection just as you would a normal `List<T>`:</span></span>

```java
PagedList<VirtualMachine> vms = azure.virtualMachines().list();
for (VirtualMachine vm : vms) {
    System.out.println("Found virtual machine with ID " + vm.id());
}
```   

## <a name="collections-returned-from-queries"></a><span data-ttu-id="f06bb-120">Коллекции, возвращенные по запросам</span><span class="sxs-lookup"><span data-stu-id="f06bb-120">Collections returned from queries</span></span>

<span data-ttu-id="f06bb-121">Библиотеки управления возвращают определенные типы коллекций по запросам на основе структуры результатов.</span><span class="sxs-lookup"><span data-stu-id="f06bb-121">The management libraries return specific collection types from queries based on the structure of the results.</span></span>

- <span data-ttu-id="f06bb-122">`List<T>` — неупорядоченные данные, для которых легко можно выполнять поиск и итерацию.</span><span class="sxs-lookup"><span data-stu-id="f06bb-122">`List<T>`: Unordered data that is easy to search and iterate over.</span></span>
- <span data-ttu-id="f06bb-123">`Map<T>` — сопоставлениями являются пары "ключ-значение" с уникальными ключами, но не обязательно с уникальными значениями.</span><span class="sxs-lookup"><span data-stu-id="f06bb-123">`Map<T>`: Maps are key/value pairs with unique keys, but not necessarily unique values.</span></span> <span data-ttu-id="f06bb-124">Примером сопоставления будут параметры веб-приложения службы приложений.</span><span class="sxs-lookup"><span data-stu-id="f06bb-124">An example of a Map would be app settings for an App Service Web App.</span></span>
- <span data-ttu-id="f06bb-125">`Set<T>` — наборы имеют уникальные ключи и значения.</span><span class="sxs-lookup"><span data-stu-id="f06bb-125">`Set<T>`: Sets have unique keys and values.</span></span> <span data-ttu-id="f06bb-126">Пример набора — сети, подключенные к виртуальной машине с уникальным идентификатором (ключом) и уникальной конфигурацией сети (значением).</span><span class="sxs-lookup"><span data-stu-id="f06bb-126">An example of a Set would be networks attached to a virtual machine, which would have both an unique identifier (the key) and a unique network configuration (the value).</span></span>

## <a name="actionable-verbs"></a><span data-ttu-id="f06bb-127">Готовые к работе команды</span><span class="sxs-lookup"><span data-stu-id="f06bb-127">Actionable verbs</span></span>

<span data-ttu-id="f06bb-128">Методы с командами в именах выполняются в Azure немедленно.</span><span class="sxs-lookup"><span data-stu-id="f06bb-128">Methods with verbs in their names take immediate action in Azure.</span></span> <span data-ttu-id="f06bb-129">Эти методы работают синхронно. Пока они не будут завершены, выполнение в текущем потоке блокируется.</span><span class="sxs-lookup"><span data-stu-id="f06bb-129">These methods work synchronously and block execution in the current thread until they complete.</span></span> 

| <span data-ttu-id="f06bb-130">Команда</span><span class="sxs-lookup"><span data-stu-id="f06bb-130">Verb</span></span>   |  <span data-ttu-id="f06bb-131">Пример использования</span><span class="sxs-lookup"><span data-stu-id="f06bb-131">Sample Usage</span></span> |
|--------|---------------|
| <span data-ttu-id="f06bb-132">create</span><span class="sxs-lookup"><span data-stu-id="f06bb-132">create</span></span> | `azure.virtualMachines().create(listOfVMCreatables)` |
| <span data-ttu-id="f06bb-133">apply</span><span class="sxs-lookup"><span data-stu-id="f06bb-133">apply</span></span>  | `virtualMachineScaleSet.update().withCapacity(6).apply()` |
| <span data-ttu-id="f06bb-134">удалить</span><span class="sxs-lookup"><span data-stu-id="f06bb-134">delete</span></span> | `azure.disks().deleteById(id)` | 
| <span data-ttu-id="f06bb-135">list</span><span class="sxs-lookup"><span data-stu-id="f06bb-135">list</span></span>   | `azure.sqlServers().list()` | 
| <span data-ttu-id="f06bb-136">get</span><span class="sxs-lookup"><span data-stu-id="f06bb-136">get</span></span>    | `VirtualMachine vm  = azure.virtualMachines().getByResourceGroup(group, vmName)` |

>[!NOTE]
> <span data-ttu-id="f06bb-137">`define()`и `update()` являются командами, но они не блокируют выполнение, если не сопровождаются `create()` или `apply()`.</span><span class="sxs-lookup"><span data-stu-id="f06bb-137">`define()` and `update()` are verbs but do not block unless followed by a `create()` or `apply()`.</span></span>
 
<span data-ttu-id="f06bb-138">Есть асинхронные версии некоторых из этих методов с суффиксом `Async`, которые используют [реактивные расширения](https://github.com/ReactiveX/RxJava).</span><span class="sxs-lookup"><span data-stu-id="f06bb-138">Asynchronous versions of some of these  methods exist with the `Async` suffix using [Reactive extensions](https://github.com/ReactiveX/RxJava).</span></span> 

<span data-ttu-id="f06bb-139">Для некоторых объектов применяются другие методы, с помощью которых изменяется состояние ресурса в Azure.</span><span class="sxs-lookup"><span data-stu-id="f06bb-139">Some objects have other methods with that change the state of the resource in Azure.</span></span> <span data-ttu-id="f06bb-140">Например, `restart()` или `VirtualMachine`.</span><span class="sxs-lookup"><span data-stu-id="f06bb-140">For example, `restart()` on a `VirtualMachine`.</span></span>

```java
VirtualMachine vmToRestart = azure.getVirtualMachines().getById(id);
vmToRestart.restart();
```
<span data-ttu-id="f06bb-141">Для этих методов не всегда есть асинхронные версии, поэтому выполнение в потоке блокируется до их завершения.</span><span class="sxs-lookup"><span data-stu-id="f06bb-141">These methods do not always have asynchronous versions and will block execution on their thread until they complete.</span></span>

<a name="Creatables"></a>

## <a name="lazy-resource-creation"></a><span data-ttu-id="f06bb-142">Создание отложенных ресурсов</span><span class="sxs-lookup"><span data-stu-id="f06bb-142">Lazy resource creation</span></span>

<span data-ttu-id="f06bb-143">При создании ресурсов Azure возникает проблемная ситуация, когда новый ресурс зависит от другого ресурса, который еще не существует.</span><span class="sxs-lookup"><span data-stu-id="f06bb-143">A challenge when creating Azure resources arises when a new resource depends on another resource that doesn't yet exist.</span></span> <span data-ttu-id="f06bb-144">Пример такого сценария — резервирование общедоступного IP-адреса и настройка диска при создании виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="f06bb-144">An example of this scenario is reserving a public IP address and setting up a disk when creating a new virtual machine.</span></span> <span data-ttu-id="f06bb-145">Предположим, вам не нужно проверять резервирование адреса или создание диска, вы просто хотите убедиться в том, что виртуальная машина располагает этими ресурсами при создании.</span><span class="sxs-lookup"><span data-stu-id="f06bb-145">You don't want to verify reserving the address or the creating the disk, you just want to ensure the virtual machine has those resources when it is created.</span></span>

<span data-ttu-id="f06bb-146">Объекты `Creatable<T>` позволяют определить ресурсы Azure для использования в коде до того, как они будут созданы в вашей подписке.</span><span class="sxs-lookup"><span data-stu-id="f06bb-146">`Creatable<T>` objects let you define Azure resources for use in your code without waiting around for them to be created in your subscription.</span></span> <span data-ttu-id="f06bb-147">Библиотеки управления откладывают создание объектов `Creatable<T>`, пока они не потребуются.</span><span class="sxs-lookup"><span data-stu-id="f06bb-147">The management libraries defer creating  `Creatable<T>` objects until they are needed.</span></span>

<span data-ttu-id="f06bb-148">Создание объектов `Creatable<T>` для ресурсов Azure с помощью команды `define()`:</span><span class="sxs-lookup"><span data-stu-id="f06bb-148">Generate `Creatable<T>` objects for Azure resources through the `define()` verb:</span></span>

```java
Creatable<PublicIPAddress> publicIPAddressCreatable = azure.publicIPAddresses().define(publicIPAddressName)
    .withRegion(Region.US_EAST)
    .withNewResourceGroup(rgName);
```

<span data-ttu-id="f06bb-149">Ресурс Azure, определенный `Creatable<PublicIPAddress>` в этом примере, еще не существует в вашей подписке при выполнении этого кода.</span><span class="sxs-lookup"><span data-stu-id="f06bb-149">The Azure resource defined by the `Creatable<PublicIPAddress>` in this example does not yet exist in your subscription when this code executes.</span></span>  <span data-ttu-id="f06bb-150">Используйте объект `publicIPAddressCreatable` для создания других ресурсов Azure с этим IP-адресом.</span><span class="sxs-lookup"><span data-stu-id="f06bb-150">Use the `publicIPAddressCreatable` object to create other Azure resources with this IP address.</span></span> 

```java
Creatable<VirtualMachine> vmCreatable = azure.virtualMachines().define("creatableVM")
    .withNewPrimaryPublicIPAddress(publicIPAddressCreatable)
```

<span data-ttu-id="f06bb-151">Ресурсы `Creatable<T>` создаются в вашей подписке, когда любой ресурс, определенный с помощью объекта, собирается в Azure с использованием `create()`.</span><span class="sxs-lookup"><span data-stu-id="f06bb-151">The `Creatable<T>` resources are generated in your subscription when any resource that is defined using the object is built in Azure using `create()`.</span></span> <span data-ttu-id="f06bb-152">В продолжение примера IP-адреса и виртуальной машины:</span><span class="sxs-lookup"><span data-stu-id="f06bb-152">Continuing the IP address and virtual machine example:</span></span>

```java
CreatedResources<VirtualMachine> virtualMachine = azure.virtualMachines().create(vmCreatable);
```

<span data-ttu-id="f06bb-153">Передача `Creatable<T>` в вызовы `create()` возвращает объект `CreatedResources` вместо объекта с одним ресурсом.</span><span class="sxs-lookup"><span data-stu-id="f06bb-153">Passing the `Creatable<T>` to `create()` calls returns a `CreatedResources` object instead of a single resource object.</span></span>  <span data-ttu-id="f06bb-154">Объект `CreatedResources<T>` обеспечивает доступ ко всем ресурсам, созданным вызовом `create()`, а не только к типизированному ресурсу в вызове.</span><span class="sxs-lookup"><span data-stu-id="f06bb-154">The `CreatedResources<T>` object lets you access all resources created by the `create()` call, not just the typed resource in the call.</span></span> <span data-ttu-id="f06bb-155">Доступ к общедоступному IP-адресу, созданному в Azure для виртуальной машины, которая создается в примере выше:</span><span class="sxs-lookup"><span data-stu-id="f06bb-155">To access the public IP address created in Azure for the virtual machine created in the above example:</span></span>

```java
PublicIPAddress pip = (PublicIPAddress) virtualMachine.createdRelatedResource(publicIPAddressCreatable.key());
```    

## <a name="exception-handling"></a><span data-ttu-id="f06bb-156">Обработка исключений</span><span class="sxs-lookup"><span data-stu-id="f06bb-156">Exception handling</span></span>

<span data-ttu-id="f06bb-157">Классы исключений для библиотек управления расширяют `com.microsoft.rest.RestException`.</span><span class="sxs-lookup"><span data-stu-id="f06bb-157">The management libraries' Exception classes extend `com.microsoft.rest.RestException`.</span></span> <span data-ttu-id="f06bb-158">Перехват исключений, создаваемых библиотеками управления, выполняется с помощью блока `catch (RestException exception)` после соответствующей инструкции `try`.</span><span class="sxs-lookup"><span data-stu-id="f06bb-158">Catch exceptions generated by the management libraries with a `catch (RestException exception)` block after the relevant `try` statement.</span></span>

## <a name="logs-and-trace"></a><span data-ttu-id="f06bb-159">Журналы и трассировка</span><span class="sxs-lookup"><span data-stu-id="f06bb-159">Logs and trace</span></span>

<span data-ttu-id="f06bb-160">Настройте объем данных, записываемых в журнал из библиотеки управления, когда создаете объект точки входа `Azure` с использованием `withLogLevel()`.</span><span class="sxs-lookup"><span data-stu-id="f06bb-160">Configure the amount of logging from the management library when you build the entry point `Azure` object using `withLogLevel()`.</span></span> <span data-ttu-id="f06bb-161">Доступны следующие уровни трассировки:</span><span class="sxs-lookup"><span data-stu-id="f06bb-161">The following trace levels exist:</span></span>

| <span data-ttu-id="f06bb-162">Уровень трассировки</span><span class="sxs-lookup"><span data-stu-id="f06bb-162">Trace level</span></span> | <span data-ttu-id="f06bb-163">Ведение журнала включено</span><span class="sxs-lookup"><span data-stu-id="f06bb-163">Logging enabled</span></span> 
| ------------ | ---------------
| <span data-ttu-id="f06bb-164">com.microsoft.rest.LogLevel.NONE</span><span class="sxs-lookup"><span data-stu-id="f06bb-164">com.microsoft.rest.LogLevel.NONE</span></span> | <span data-ttu-id="f06bb-165">Нет выходных данных.</span><span class="sxs-lookup"><span data-stu-id="f06bb-165">No output</span></span>
| <span data-ttu-id="f06bb-166">com.microsoft.rest.LogLevel.BASIC</span><span class="sxs-lookup"><span data-stu-id="f06bb-166">com.microsoft.rest.LogLevel.BASIC</span></span> | <span data-ttu-id="f06bb-167">Регистрация URL-адресов для базовых вызовов REST, кодов и времени ответов.</span><span class="sxs-lookup"><span data-stu-id="f06bb-167">Logs the URLs to underlying REST calls, response codes and times</span></span>
| <span data-ttu-id="f06bb-168">com.microsoft.rest.LogLevel.BODY</span><span class="sxs-lookup"><span data-stu-id="f06bb-168">com.microsoft.rest.LogLevel.BODY</span></span> | <span data-ttu-id="f06bb-169">Регистрация тех же элементов, что и для уровня BASIC, а также текста запросов и ответов для вызовов REST.</span><span class="sxs-lookup"><span data-stu-id="f06bb-169">Everything in BASIC plus request and response bodies for the REST calls</span></span>
| <span data-ttu-id="f06bb-170">com.microsoft.rest.LogLevel.HEADERS</span><span class="sxs-lookup"><span data-stu-id="f06bb-170">com.microsoft.rest.LogLevel.HEADERS</span></span> | <span data-ttu-id="f06bb-171">Регистрация тех же элементов, что и для уровня BASIC, а также заголовков запросов и ответов для вызовов REST.</span><span class="sxs-lookup"><span data-stu-id="f06bb-171">Everything in BASIC plus the request and response headers REST calls</span></span>
| <span data-ttu-id="f06bb-172">com.microsoft.rest.LogLevel.BODY_AND_HEADERS</span><span class="sxs-lookup"><span data-stu-id="f06bb-172">com.microsoft.rest.LogLevel.BODY_AND_HEADERS</span></span> | <span data-ttu-id="f06bb-173">Регистрация тех же элементов, что и для уровней журнала BODY и HEADERS в совокупности.</span><span class="sxs-lookup"><span data-stu-id="f06bb-173">Everything in both BODY and HEADERS log level</span></span>

<span data-ttu-id="f06bb-174">Для регистрации выходных данных привяжите [реализацию ведения журналов SLF4J](https://www.slf4j.org/manual.html) к платформе ведения журналов, например [Log4J 2](https://logging.apache.org/log4j/2.x/).</span><span class="sxs-lookup"><span data-stu-id="f06bb-174">Bind a [SLF4J logging implementation](https://www.slf4j.org/manual.html) if you need to log output to a logging framework like [Log4J 2](https://logging.apache.org/log4j/2.x/).</span></span>