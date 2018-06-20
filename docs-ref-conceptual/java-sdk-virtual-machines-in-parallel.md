---
title: Параллельное создание виртуальных машин в разных регионах | Документация Майкрософт
description: Пример кода для параллельного создания виртуальных машин в разных регионах Azure с помощью пакета Azure SDK для Java
author: rloutlaw
manager: douge
ms.assetid: e5a36699-2d96-4571-84f9-a6af13f3c067
ms.service: Azure
ms.devlang: java
ms.topic: article
ms.date: 03/30/2017
ms.author: routlaw;asirveda
ms.openlocfilehash: e20feb555c3a360eceae60c1569af9a00a5cd027
ms.sourcegitcommit: 1500f341a96d9da461c288abf4baf79f494ae662
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/28/2017
ms.locfileid: "21931200"
---
# <a name="create-virtual-machines-across-multiple-regions-from-your-java-applications"></a><span data-ttu-id="b75e3-103">Создание виртуальных машин в нескольких регионах из приложений Java</span><span class="sxs-lookup"><span data-stu-id="b75e3-103">Create virtual machines across multiple regions from your Java applications</span></span>

<span data-ttu-id="b75e3-104">[В этом примере](https://github.com/Azure-Samples/compute-java-create-virtual-machines-across-regions-in-parallel) виртуальные машины создаются параллельно в разных регионах Azure с помощью [библиотек управления Azure для Java](https://github.com/Azure/azure-sdk-for-java).</span><span class="sxs-lookup"><span data-stu-id="b75e3-104">[This sample](https://github.com/Azure-Samples/compute-java-create-virtual-machines-across-regions-in-parallel) creates virtual machines in parallel across different Azure regions using the [Azure management libraries for Java](https://github.com/Azure/azure-sdk-for-java).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b75e3-105">В этом примере в четырех регионах создается 48 виртуальных машин [размером STANDARD_DS3_V2](http://docs.microsoft.com/azure/virtual-machines/virtual-machines-windows-sizes) под управлением LTS Ubuntu 16.04.</span><span class="sxs-lookup"><span data-stu-id="b75e3-105">The sample creates a total of 48 VMs running Ubuntu 16.04 LTS of [size STANDARD_DS3_V2](http://docs.microsoft.com/azure/virtual-machines/virtual-machines-windows-sizes) across four regions.</span></span> <span data-ttu-id="b75e3-106">Этот пример кода удаляет виртуальные машины перед завершением работы.</span><span class="sxs-lookup"><span data-stu-id="b75e3-106">The sample code deletes these virtual machines before exiting.</span></span> <span data-ttu-id="b75e3-107">Обязательно [проверьте квоты и ограничения службы](http://docs.microsoft.com/azure/azure-subscription-service-limits), прежде чем выполнять этот пример с определенным по умолчанию числом виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="b75e3-107">Make sure to [check your service limits and quota](http://docs.microsoft.com/azure/azure-subscription-service-limits) before running this sample with the default number of VMs.</span></span>

## <a name="run-the-sample"></a><span data-ttu-id="b75e3-108">Запуск примера</span><span class="sxs-lookup"><span data-stu-id="b75e3-108">Run the sample</span></span>

<span data-ttu-id="b75e3-109">Создайте [файл проверки подлинности](https://github.com/Azure/azure-sdk-for-java/blob/master/AUTH.md), задайте переменную среды `AZURE_AUTH_LOCATION` и укажите полный путь к файлу на компьютере.</span><span class="sxs-lookup"><span data-stu-id="b75e3-109">Create an [authentication file](https://github.com/Azure/azure-sdk-for-java/blob/master/AUTH.md) and set an environment variable `AZURE_AUTH_LOCATION` with the full path to the file on your computer.</span></span> <span data-ttu-id="b75e3-110">Далее выполните:</span><span class="sxs-lookup"><span data-stu-id="b75e3-110">Then run:</span></span>

```
git clone https://github.com/Azure-Samples/compute-java-create-virtual-machines-across-regions-in-parallel.git
cd compute-java-create-virtual-machines-across-regions-in-parallel
mvn clean compile exec:java
```

<span data-ttu-id="b75e3-111">Просмотрите [полный пример кода на GitHub](https://github.com/Azure-Samples/compute-java-create-virtual-machines-across-regions-in-parallel/blob/master/src/main/java/com/microsoft/azure/management/compute/samples/CreateVirtualMachinesInParallel.java).</span><span class="sxs-lookup"><span data-stu-id="b75e3-111">View the [complete code sample on GitHub](https://github.com/Azure-Samples/compute-java-create-virtual-machines-across-regions-in-parallel/blob/master/src/main/java/com/microsoft/azure/management/compute/samples/CreateVirtualMachinesInParallel.java).</span></span>

## <a name="authenticate-with-azure"></a><span data-ttu-id="b75e3-112">Проверка подлинности с помощью Azure</span><span class="sxs-lookup"><span data-stu-id="b75e3-112">Authenticate with Azure</span></span>

[!INCLUDE [auth-include](includes/java-auth-include.md)]

## <a name="set-locations-and-counts-for-the-virtual-machines"></a><span data-ttu-id="b75e3-113">Определение расположения и счетчиков для виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="b75e3-113">Set locations and counts for the virtual machines</span></span>

```java
// use a Map to define how where and how many VMs to create 
Map<Region, Integer> virtualMachinesByLocation = new HashMap<Region, Integer>();

// create 12 virtual machines in four regions
virtualMachinesByLocation.put(Region.US_EAST, 12);
virtualMachinesByLocation.put(Region.US_SOUTH_CENTRAL, 12);
virtualMachinesByLocation.put(Region.US_WEST, 12);
virtualMachinesByLocation.put(Region.US_NORTH_CENTRAL, 12);
```

<span data-ttu-id="b75e3-114">`Map` используется позже в этом примере для распределения виртуальных машин по всему миру.</span><span class="sxs-lookup"><span data-stu-id="b75e3-114">This `Map` is used later in the sample to set the distrubtion of the VMs worldwide.</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="b75e3-115">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="b75e3-115">Create a resource group</span></span> 

```java
// logically associate the resources in the sample into a randomly named resource group
final String rgName = SdkContext.randomResourceName("rgCOPD", 24);
ResourceGroup resourceGroup = azure.resourceGroups().define(rgName)
                .withRegion(Region.US_EAST)
                .create();
```

<span data-ttu-id="b75e3-116">Эта группа ресурсов управляет каждым ресурсом в примере,</span><span class="sxs-lookup"><span data-stu-id="b75e3-116">Each resource in the sample is managed by this resource group.</span></span> <span data-ttu-id="b75e3-117">что упрощает последующую очистку ресурсов. Для этого достаточно удалить группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="b75e3-117">This makes the resources easy to clean up later by deleting the resource group.</span></span>

## <a name="define-the-virtual-machines"></a><span data-ttu-id="b75e3-118">Определение виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="b75e3-118">Define the virtual machines</span></span>
```java
// list to store the VirtualMachine definitions
List<Creatable<VirtualMachine>> creatableVirtualMachines = new ArrayList<>();
    
// outer loop: iterate through each region included in the map
for (Map.Entry<Region, Integer> entry : virtualMachinesByLocation.entrySet()) {
    Region region = entry.getKey();
    Integer vmCount = entry.getValue();

    // Define one virtual network Creatable per region for the VMs to share
    String networkName = SdkContext.randomResourceName("vnetCOPD-", 20);
    Creatable<Network> networkCreatable = azure.networks().define(networkName)
           .withRegion(region)
           .withExistingResourceGroup(resourceGroup)
           .withAddressSpace("172.16.0.0/16");

    // Define one storage account Creatable per region for storing VM disks
    String storageAccountName = SdkContext.randomResourceName("stgcopd", 20);
    Creatable<StorageAccount> storageAccountCreatable = azure.storageAccounts()
        .define(storageAccountName)
              .withRegion(region)
              .withExistingResourceGroup(resourceGroup);

    // generate a common prefix for every VM name
    String linuxVMNamePrefix = SdkContext.randomResourceName("vm-", 15);

    // inner loop: iterate once for every VM instance in the region
    for (int i = 1; i <= vmCount; i++) {

        // Create one public IP address Creatable for each VM
        Creatable<PublicIpAddress> publicIpAddressCreatable = azure.publicIpAddresses()
             .define(String.format("%s-%d", linuxVMNamePrefix, i))
             .withRegion(region)
             .withExistingResourceGroup(resourceGroup)
             .withLeafDomainLabel(SdkContext.randomResourceName("pip", 10));

        publicIpCreatableKeys.add(publicIpAddressCreatable.key());

        // Create one virtual machine Creatable 
        Creatable<VirtualMachine> virtualMachineCreatable = azure.virtualMachines()
             .define(String.format("%s-%d", linuxVMNamePrefix, i))
             .withRegion(region)
             .withExistingResourceGroup(resourceGroup)
             .withNewPrimaryNetwork(networkCreatable)
             .withPrimaryPrivateIpAddressDynamic()
             .withNewPrimaryPublicIpAddress(publicIpAddressCreatable)
             .withPopularLinuxImage(KnownLinuxVirtualMachineImage.UBUNTU_SERVER_16_04_LTS)
             .withRootUsername(userName)
             .withSsh(sshKey)
             .withSize(VirtualMachineSizeTypes.STANDARD_DS3_V2)
             .withNewStorageAccount(storageAccountCreatable);
        // add the virtual machine Creatable to the list     
        creatableVirtualMachines.add(virtualMachineCreatable); 
     }
}
```

<span data-ttu-id="b75e3-119">Для внешнего цикла `for` выше выполняется итерация по каждому региону. При этом определяются объекты Creatable для виртуальной сети и учетной записи хранилища, которые будут использоваться всеми виртуальными машинами в этом регионе.</span><span class="sxs-lookup"><span data-stu-id="b75e3-119">The outer `for` loop above iterates through each region, defining a virtual network Creatable and storage account Creatable for use by all virtual machines in that region.</span></span> <span data-ttu-id="b75e3-120">Узнайте больше о применении [объектов Creatable](java-sdk-azure-concepts.md#Creatables), которые позволяют создавать ресурсы при использовании библиотек управления только в случае необходимости.</span><span class="sxs-lookup"><span data-stu-id="b75e3-120">Learn more about using [Creatables](java-sdk-azure-concepts.md#Creatables) to create resources only as needed when using the management libraries.</span></span>

<span data-ttu-id="b75e3-121">Внутренний цикл `for` получает объект Creatable для общедоступного IP-адреса виртуальной машины и определяет объект Creatable для виртуальной машины. При этом используются объекты Creatable для виртуальной сети, учетной записи хранения и общедоступного IP-адреса, определенного ранее.</span><span class="sxs-lookup"><span data-stu-id="b75e3-121">The inner `for` loop gets a public IP address Creatable for the virtual machine and then defines a virtual machine Creatable using the Creatables for the virtual network, storage account, and public IP address defined previously.</span></span>  <span data-ttu-id="b75e3-122">Затем объект Creatable VirtualMachine добавляется в список `creatableVirtualMachines`.</span><span class="sxs-lookup"><span data-stu-id="b75e3-122">This VirtualMachine Creatable is then added to the `creatableVirtualMachines` list.</span></span>

## <a name="create-the-virtual-machines"></a><span data-ttu-id="b75e3-123">Создание виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="b75e3-123">Create the virtual machines</span></span>

```java
// create all virtual machines defined in the list, return all Creatable objects used
// including networks, public IP addresses, and storage accounts
CreatedResources<VirtualMachine> virtualMachines = azure.virtualMachines().create(creatableVirtualMachines);

// list the IDs of each virtual machine created 
for (VirtualMachine virtualMachine : virtualMachines.values()) {
    System.out.println(virtualMachine.id());
}

// call createdRelatedResource(key) to get the resources used to define the virtual machines. 
// Save the key at the time you define the Creatable to use CreatedResources like this
for (String publicIpCreatableKey : publicIpCreatableKeys) {
    PublicIPAddress pip = 
         (PublicIPAddress) virtualMachines.createdRelatedResource(publicIpCreatableKey);
}
```

<span data-ttu-id="b75e3-124">Вызов `azure.virtualMachines().create(creatableVirtualMachines)` параллельно создает все виртуальные машины, определенные в списке `creatableVirtualMachines` во всех регионах.</span><span class="sxs-lookup"><span data-stu-id="b75e3-124">The `azure.virtualMachines().create(creatableVirtualMachines)` call creates all of the virtual machines defined in the `creatableVirtualMachines` List in parallel across the regions.</span></span>

<span data-ttu-id="b75e3-125">Используйте возвращаемый объект `CreatedResources<VirtualMachine>` для доступа к любым ресурсам, созданным в подписке Azure при выполнении метода `create()`, а не только к ресурсу с возвращаемым значением типа `VirtualMachine`.</span><span class="sxs-lookup"><span data-stu-id="b75e3-125">Use the returned `CreatedResources<VirtualMachine>` object to access any resources created in the Azure subscription during the the `create()` method, not just the returned `VirtualMachine` type.</span></span> <span data-ttu-id="b75e3-126">Измените `createdRelatedResources()` на значение надлежащего типа.</span><span class="sxs-lookup"><span data-stu-id="b75e3-126">Cast the returned value from `createdRelatedResources()` to the correct type.</span></span> 

<span data-ttu-id="b75e3-127">Дополнительные сведения о работе с `Creatable<T>` и `CreatedResources` см. в нашей [статье о принципах работы библиотек](java-sdk-azure-concepts.md).</span><span class="sxs-lookup"><span data-stu-id="b75e3-127">Learn more about working with `Creatable<T>` and `CreatedResources` in our [library concepts article](java-sdk-azure-concepts.md).</span></span>

## <a name="delete-the-resource-group"></a><span data-ttu-id="b75e3-128">удаление группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="b75e3-128">Delete the resource group</span></span> 

```java
// finally block deletes the resource group before the code exits
// deleting a resource group deletes all resources created in it
finally {
    try {
        System.out.println("Deleting Resource Group: " + rgName);
        azure.resourceGroups().deleteByName(rgName);
        System.out.println("Deleted Resource Group: " + rgName);
    } catch (NullPointerException npe) {
        System.out.println("Did not create any resources in Azure. No clean up is necessary");
    } catch (Exception g) {
        g.printStackTrace();
    }
}
```

<span data-ttu-id="b75e3-129">Этот блок удаляет ресурсы, созданные в примере, перед выходом из него.</span><span class="sxs-lookup"><span data-stu-id="b75e3-129">This block deletes resources created in the sample before the sample exits.</span></span>

## <a name="sample-explanation"></a><span data-ttu-id="b75e3-130">Описание примера</span><span class="sxs-lookup"><span data-stu-id="b75e3-130">Sample explanation</span></span>

<span data-ttu-id="b75e3-131">См. полный пример кода на [GitHub](https://github.com/Azure-Samples/compute-java-create-virtual-machines-across-regions-in-parallel).</span><span class="sxs-lookup"><span data-stu-id="b75e3-131">View the complete sample code on [Github](https://github.com/Azure-Samples/compute-java-create-virtual-machines-across-regions-in-parallel).</span></span>

<span data-ttu-id="b75e3-132">В примере используются объекты `Creatable`, чтобы определить виртуальную сеть и учетную запись хранения для каждого региона, в котором размещены виртуальные машины.</span><span class="sxs-lookup"><span data-stu-id="b75e3-132">The sample uses `Creatable` objects to define a virtual network and storage account for each region hosting the virtual machines.</span></span> <span data-ttu-id="b75e3-133">Затем определяется объект `Creatable` для общедоступного IP-адреса каждой виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="b75e3-133">`Creatable` objects are then defined for the public IP address for each virtual machine.</span></span> <span data-ttu-id="b75e3-134">В примере с использованием этих объектов `Creatable` определяются виртуальные машины, а их определения добавляются в список `virtualMachineCreatable`.</span><span class="sxs-lookup"><span data-stu-id="b75e3-134">The sample defines the virtual machines using these `Creatable` objects, and sample adds the VM definition to the `virtualMachineCreatable` list.</span></span>

<span data-ttu-id="b75e3-135">Когда в список будут добавлены все определения, `azure.virtualMachines().create(creatableVirtualMachines)` параллельно создаст все виртуальные машины в Azure.</span><span class="sxs-lookup"><span data-stu-id="b75e3-135">After the code adds every virtual machine definition to the list, `azure.virtualMachines().create(creatableVirtualMachines)` creates each virtual machine in parallel in Azure.</span></span>

<span data-ttu-id="b75e3-136">Затем пример кода получает IP-адреса от возвращаемого объекта CreatedResources для всех созданных виртуальных машин. Это позволяет создать [диспетчер трафика](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-overview) для распределения нагрузки между виртуальными машинами.</span><span class="sxs-lookup"><span data-stu-id="b75e3-136">The sample code then gets the IP addresses for all of the created virtual machines from the returned CreatedResources object to create a [Traffic Manager](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-overview) to distribute load across the virtual machines.</span></span> 

<span data-ttu-id="b75e3-137">Блок `finally` удаляет ресурсы из подписки Azure даже в случае ошибки.</span><span class="sxs-lookup"><span data-stu-id="b75e3-137">The `finally` block deletes the resources from your Azure subscription even in the case of an error.</span></span>

| <span data-ttu-id="b75e3-138">Класс, используемый в примере</span><span class="sxs-lookup"><span data-stu-id="b75e3-138">Class used in sample</span></span> | <span data-ttu-id="b75e3-139">Примечания</span><span class="sxs-lookup"><span data-stu-id="b75e3-139">Notes</span></span>
|-------|-------|
| [<span data-ttu-id="b75e3-140">VirtualMachine</span><span class="sxs-lookup"><span data-stu-id="b75e3-140">VirtualMachine</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.compute._virtual_machine) | <span data-ttu-id="b75e3-141">Запрос свойств и управление состоянием виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="b75e3-141">Query properties and manage state of virtual machines.</span></span> <span data-ttu-id="b75e3-142">Извлекается в виде списка из `azure.virtualMachines().list()` или по имени либо идентификатору `azure.virtualMachines().getByResourceGroup()`</span><span class="sxs-lookup"><span data-stu-id="b75e3-142">Retrieved in list form from `azure.virtualMachines().list()` or by name or ID `azure.virtualMachines().getByResourceGroup()`</span></span>
| [<span data-ttu-id="b75e3-143">VirtualMachineSizeTypes</span><span class="sxs-lookup"><span data-stu-id="b75e3-143">VirtualMachineSizeTypes</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.compute._virtual_machine_size_types) | <span data-ttu-id="b75e3-144">Статические значения, которые сопоставляются с [параметрами размера виртуальной машины](https://azure.microsoft.com/pricing/details/virtual-machines/linux/) и используются как параметры для `withSize()` при определении виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="b75e3-144">Static values that map to [virtual machine size options](https://azure.microsoft.com/pricing/details/virtual-machines/linux/) for use as a parameter to `withSize()` when defining a virtual machine.</span></span>
| [<span data-ttu-id="b75e3-145">PublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="b75e3-145">PublicIpAddress</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.network._public_i_p_address) | <span data-ttu-id="b75e3-146">Определяется (но не создается немедленно) для каждой виртуальной машины с помощью `azure.publicIpAddresses().define()`.</span><span class="sxs-lookup"><span data-stu-id="b75e3-146">Defined, but not immediately created, for each virtual machine through `azure.publicIpAddresses().define()`.</span></span> <span data-ttu-id="b75e3-147">Сохраните ключ для каждого `Creatable` и выполните извлечение позднее с помощью `createdRelatedResource()`</span><span class="sxs-lookup"><span data-stu-id="b75e3-147">Store the key for each `Creatable` and retrieve later through `createdRelatedResource()`</span></span>
| [<span data-ttu-id="b75e3-148">KnownLinuxVirtualMachineImage</span><span class="sxs-lookup"><span data-stu-id="b75e3-148">KnownLinuxVirtualMachineImage</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.compute._known_linux_virtual_machine_image) | <span data-ttu-id="b75e3-149">Набор параметров виртуальной машины Linux, которые используются в качестве параметров для метода `withPopularLinuxImage()` при определении виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="b75e3-149">Set of Linux virtual machine options used as a parameter to `withPopularLinuxImage()` method when defining a virtual machine.</span></span>
| [<span data-ttu-id="b75e3-150">Сеть</span><span class="sxs-lookup"><span data-stu-id="b75e3-150">Network</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.network._network) | <span data-ttu-id="b75e3-151">В примере определяется одна виртуальная сеть для каждого региона с помощью `azure.networks().define()`.</span><span class="sxs-lookup"><span data-stu-id="b75e3-151">The sample defines one virtual network for each region through  `azure.networks().define()` .</span></span> 

## <a name="next-steps"></a><span data-ttu-id="b75e3-152">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b75e3-152">Next steps</span></span>

[!INCLUDE [next-steps](includes/java-next-steps.md)]