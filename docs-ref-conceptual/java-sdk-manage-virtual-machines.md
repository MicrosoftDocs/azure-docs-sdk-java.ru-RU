---
title: Управление виртуальными машинами Azure с помощью Java | Документация Майкрософт
description: Пример кода для управления виртуальными машинами Azure с помощью пакета Azure SDK для Java
author: rloutlaw
manager: douge
ms.assetid: 88629aee-6279-433e-a08b-4f8e290446d0
ms.devlang: java
ms.topic: article
ms.service: Azure
ms.technology: Azure
ms.date: 3/30/2017
ms.author: routlaw;asirveda
ms.openlocfilehash: 388b68bfb0fdac70efed5ad5d0f7c957ce915449
ms.sourcegitcommit: 115f4c8ad07a11f17d79e9d945d63917836b11c8
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "61592569"
---
# <a name="manage-azure-virtual-machines-from-your-java-applications"></a><span data-ttu-id="b94a9-103">Управление виртуальными машинами Azure из приложений Java</span><span class="sxs-lookup"><span data-stu-id="b94a9-103">Manage Azure virtual machines from your Java applications</span></span>

<span data-ttu-id="b94a9-104">[Этот пример](https://github.com/Azure-Samples/compute-java-manage-vm/) использует [библиотеки управления Azure для Java](https://github.com/Azure/azure-sdk-for-java) для создания виртуальных машин Azure и управления ими.</span><span class="sxs-lookup"><span data-stu-id="b94a9-104">[This sample](https://github.com/Azure-Samples/compute-java-manage-vm/) uses the [Azure management libraries for Java](https://github.com/Azure/azure-sdk-for-java) to create and work with Azure virtual machines.</span></span>

## <a name="run-the-sample"></a><span data-ttu-id="b94a9-105">Запуск примера</span><span class="sxs-lookup"><span data-stu-id="b94a9-105">Run the sample</span></span>

<span data-ttu-id="b94a9-106">Создайте [файл проверки подлинности](https://github.com/Azure/azure-sdk-for-java/blob/master/AUTH.md), задайте переменную среды `AZURE_AUTH_LOCATION` и укажите полный путь к файлу на компьютере.</span><span class="sxs-lookup"><span data-stu-id="b94a9-106">Create an [authentication file](https://github.com/Azure/azure-sdk-for-java/blob/master/AUTH.md) and set an environment variable `AZURE_AUTH_LOCATION` with the full path to the file on your computer.</span></span> <span data-ttu-id="b94a9-107">Далее выполните:</span><span class="sxs-lookup"><span data-stu-id="b94a9-107">Then run:</span></span>

```
git clone https://github.com/Azure-Samples/compute-java-manage-vm.git
cd compute-java-manage-vm
mvn clean compile exec:java
```

<span data-ttu-id="b94a9-108">Просмотрите [полный пример кода на GitHub](https://github.com/Azure-Samples/compute-java-manage-vm/blob/master/src/main/java/com/microsoft/azure/management/compute/samples/ManageVirtualMachine.java).</span><span class="sxs-lookup"><span data-stu-id="b94a9-108">View the [complete code sample on GitHub](https://github.com/Azure-Samples/compute-java-manage-vm/blob/master/src/main/java/com/microsoft/azure/management/compute/samples/ManageVirtualMachine.java).</span></span>

## <a name="authenticate-with-azure"></a><span data-ttu-id="b94a9-109">Проверка подлинности с помощью Azure</span><span class="sxs-lookup"><span data-stu-id="b94a9-109">Authenticate with Azure</span></span>

[!INCLUDE [auth-include](includes/java-auth-include.md)]

## <a name="create-a-windows-virtual-machine"></a><span data-ttu-id="b94a9-110">Создание виртуальной машины Windows</span><span class="sxs-lookup"><span data-stu-id="b94a9-110">Create a Windows virtual machine</span></span>

```java
// Prepare a data disk for VM
Disk dataDisk = azure.disks().define(SdkContext.randomResourceName("dsk", 30))
            .withRegion(region)
            .withNewResourceGroup(rgName)
            .withData()
            .withSizeInGB(50)
            .create();

// create the windows virtual machine with the data disk            
VirtualMachine windowsVM = azure.virtualMachines().define(windowsVmName)
            .withRegion(region)
            .withNewResourceGroup(rgName)
            .withNewPrimaryNetwork("10.0.0.0/28")
            .withPrimaryPrivateIpAddressDynamic()
            .withoutPrimaryPublicIpAddress()
            .withPopularWindowsImage(KnownWindowsVirtualMachineImage.WINDOWS_SERVER_2012_R2_DATACENTER)
            .withAdminUsername(userName)
            .withAdminPassword(password)
            .withNewDataDisk(10)
            .withNewDataDisk(dataDiskCreatable)
            .withExistingDataDisk(dataDisk)
            .withSize(VirtualMachineSizeTypes.STANDARD_D3_V2)
            .create();
```

<span data-ttu-id="b94a9-111">Этот код выполняет следующие действия:</span><span class="sxs-lookup"><span data-stu-id="b94a9-111">This code:</span></span>   

0. <span data-ttu-id="b94a9-112">Определяет создаваемый объект `Disk` с произвольным именем и размером 50 ГБ, который будет использоваться с виртуальной машиной.</span><span class="sxs-lookup"><span data-stu-id="b94a9-112">Defines a `Disk` Creatable with a 50GB size and random name for use with a virtual machine.</span></span>
0. <span data-ttu-id="b94a9-113">Использует цепочку `azure.virtualMachines().define()..create()` для создания виртуальной машины Windows Server 2012.</span><span class="sxs-lookup"><span data-stu-id="b94a9-113">Uses the `azure.virtualMachines().define()..create()` chain to create the Windows Server 2012 virtual machine.</span></span> <span data-ttu-id="b94a9-114">API создает `Disk`, определенный на предыдущем шаге одновременно с виртуальной машиной.</span><span class="sxs-lookup"><span data-stu-id="b94a9-114">The API creates the `Disk` defined in the previous step the same time as the virtual machine.</span></span> <span data-ttu-id="b94a9-115">С помощью `withNewDataDisk(10)` к виртуальной машине также подключается диск данных размером 10 ГБ.</span><span class="sxs-lookup"><span data-stu-id="b94a9-115">A 10GB data disk is also attached to the virtual machine through `withNewDataDisk(10)`.</span></span>

<span data-ttu-id="b94a9-116">См. дополнительные сведения об использовании [создаваемых<T> объектов](java-sdk-azure-concepts.md#Creatables), чтобы определить локальные представления ресурсов и создавать их, когда он будут нужны другим ресурсам Azure.</span><span class="sxs-lookup"><span data-stu-id="b94a9-116">Learn more about using [Creatable<T> objects](java-sdk-azure-concepts.md#Creatables) to define local representations of resources and create them just as other Azure resources need them.</span></span>

## <a name="stop-start-and-restart-a-virtual-machine"></a><span data-ttu-id="b94a9-117">Остановка, запуск и перезапуск виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="b94a9-117">Stop, start, and restart a virtual machine</span></span>

```java
// look up a virtual machine by its ID and then restart, stop, and start it
azureVM = azure.getVirtualMachine.getById(windowsVM.id());

azureVM.restart();
azureVM.powerOff();
azureVM.start();
```

<span data-ttu-id="b94a9-118">`powerOff()` останавливает операционную систему виртуальной машины, но не освобождает ее ресурсы.</span><span class="sxs-lookup"><span data-stu-id="b94a9-118">`powerOff()` stops the virtual machine operating system but does not deallocate its resources.</span></span>

## <a name="add-a-virtual-machine-to-an-existing-network"></a><span data-ttu-id="b94a9-119">Добавление виртуальной машины в существующую сеть</span><span class="sxs-lookup"><span data-stu-id="b94a9-119">Add a virtual machine to an existing network</span></span>

```java
// Get the virtual network the current virtual machine is using
Network network = windowsVM.getPrimaryNetworkInterface().primaryIPConfiguration().getNetwork();

// Create a Linux VM in the same subnet
VirtualMachine linuxVM = azure.virtualMachines().define(linuxVmName)
           .withRegion(region)
           .withExistingResourceGroup(rgName)
           .withExistingPrimaryNetwork(network)
           .withSubnet("subnet1") // default subnet name when no name specified at creation
           .withPrimaryPrivateIPAddressDynamic()
           .withoutPrimaryPublicIPAddress()
           .withPopularLinuxImage(KnownLinuxVirtualMachineImage.UBUNTU_SERVER_16_04_LTS)
           .withRootUsername(userName)
           .withRootPassword(password)
           .withSize(VirtualMachineSizeTypes.STANDARD_D3_V2)
           .create();
```

<span data-ttu-id="b94a9-120">Используйте `withPopularLinuxImage`, чтобы определить виртуальную машину Linux вместо Windows.</span><span class="sxs-lookup"><span data-stu-id="b94a9-120">Use `withPopularLinuxImage` to define a Linux VM instead of a Windows one.</span></span>


## <a name="list-virtual-machines"></a><span data-ttu-id="b94a9-121">Отображение списка виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="b94a9-121">List virtual machines</span></span>

```java
// get a list of VMs in the same resource group as an existing VM
String resourceGroupName = windowsVM.resourceGroupName();
PagedList<VirtualMachine> resourceGroupVMs = azure.virtualMachines()
        .listByResourceGroup(resourceGroupName); 

// for each vitual machine in the resource group, log their name and plan
for (VirtualMachine virtualMachine : azure.virtualMachines().listByResourceGroup(resourceGroupName)) {
    System.out.println("VM " + virtualMachine.computerName() + 
        " has plan " + virtualMachine.plan());
}
```

<span data-ttu-id="b94a9-122">Чтобы отобразить список всех виртуальных машин в подписке, используйте `azure.virtualMachines().list()`. Выполните итерацию по схеме, возвращенной с помощью `tags()`, чтобы управлять помеченными тегами коллекциями виртуальных машин в группах ресурсов.</span><span class="sxs-lookup"><span data-stu-id="b94a9-122">List all virtual machines for a subscription using `azure.virtualMachines().list()` and iterate through the Map returned by `tags()` to manage tagged collections of virtual machines across resource groups.</span></span>

## <a name="update-a-virtual-machine"></a><span data-ttu-id="b94a9-123">Обновление виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="b94a9-123">Update a virtual machine</span></span>

```java
// add a 10GB data disk to the virtual machine
windowsVM.update()
     .withNewDataDisk(10)
     .apply();
```

<span data-ttu-id="b94a9-124">Обновите конфигурацию виртуальной машины с помощью `update()...apply()` и методов, которые использовались для настройки виртуальной машины при создании с помощью `define()...create()`.</span><span class="sxs-lookup"><span data-stu-id="b94a9-124">Update the virtual machine configuration using `update()...apply()` and the same methods used to configure the virtual machine when created through `define()...create()`.</span></span>

## <a name="delete-a-virtual-machine"></a><span data-ttu-id="b94a9-125">удаление виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="b94a9-125">Delete a virtual machine</span></span>

```java
// delete by ID if you already are working with the VM object
azure.virtualMachines().deleteById(windowsVM.id());

// delete by resource group and name
azure.virtualMachines().deleteByResourceGroup(rgName,windowsVmName);
```

## <a name="sample-explanation"></a><span data-ttu-id="b94a9-126">Описание примера</span><span class="sxs-lookup"><span data-stu-id="b94a9-126">Sample explanation</span></span>

<span data-ttu-id="b94a9-127">[Пример кода](https://github.com/Azure-Samples/compute-java-manage-vm/blob/master/src/main/java/com/microsoft/azure/management/compute/samples/ManageVirtualMachine.java) создает виртуальную машину Windows с диском данных размером 50 ГБ.</span><span class="sxs-lookup"><span data-stu-id="b94a9-127">[The sample code](https://github.com/Azure-Samples/compute-java-manage-vm/blob/master/src/main/java/com/microsoft/azure/management/compute/samples/ManageVirtualMachine.java) creates a Windows virtual machine with a 50GB data disk.</span></span> <span data-ttu-id="b94a9-128">Затем пример создает второй диск данных размером 10 ГБ и подключает его к этой виртуальной машине Windows.</span><span class="sxs-lookup"><span data-stu-id="b94a9-128">The sample then creates a second 10GB data disk and attaches it to this Windows virtual machine.</span></span>
<span data-ttu-id="b94a9-129">Затем пример создает виртуальную машину Linux в той же виртуальной сети, в которой создана виртуальная машина Windows.</span><span class="sxs-lookup"><span data-stu-id="b94a9-129">Then the sample creates a Linux virtual machine in the same virtual network as the Windows virtual machine.</span></span>

<span data-ttu-id="b94a9-130">Пример записывает сведения о виртуальных машинах и в завершение удаляет обе машины.</span><span class="sxs-lookup"><span data-stu-id="b94a9-130">The sample logs information about both virtual machines and deletes them both before completing.</span></span>

| <span data-ttu-id="b94a9-131">Класс, используемый в примере</span><span class="sxs-lookup"><span data-stu-id="b94a9-131">Class used in sample</span></span> | <span data-ttu-id="b94a9-132">Примечания</span><span class="sxs-lookup"><span data-stu-id="b94a9-132">Notes</span></span>
|-------|-------|
| [<span data-ttu-id="b94a9-133">VirtualMachine</span><span class="sxs-lookup"><span data-stu-id="b94a9-133">VirtualMachine</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.compute._virtual_machine) | <span data-ttu-id="b94a9-134">Запрос свойств и управление состоянием виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="b94a9-134">Query properties and manage state of virtual machines.</span></span> <span data-ttu-id="b94a9-135">Извлекается в виде списка с помощью `azure.virtualMachines().list()` или по имени либо идентификатору `azure.virtualMachines().getByResourceGroup()`</span><span class="sxs-lookup"><span data-stu-id="b94a9-135">Retrieved in list form  with`azure.virtualMachines().list()` or by name or ID `azure.virtualMachines().getByResourceGroup()`</span></span>
| [<span data-ttu-id="b94a9-136">VirtualMachineSizeTypes</span><span class="sxs-lookup"><span data-stu-id="b94a9-136">VirtualMachineSizeTypes</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.compute._virtual_machine_size_types) | <span data-ttu-id="b94a9-137">Класс со статическими значениями, сопоставленными с [параметрами размера виртуальной машины](https://azure.microsoft.com/pricing/details/virtual-machines/linux/), используемыми в методе `withSize()` для определения ресурсов, выделенных для виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="b94a9-137">Class with static values that map to [virtual machine size options](https://azure.microsoft.com/pricing/details/virtual-machines/linux/), used by the `withSize()` method to define the resources allocated to the VM.</span></span>
| [<span data-ttu-id="b94a9-138">Диск</span><span class="sxs-lookup"><span data-stu-id="b94a9-138">Disk</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.compute._disk) | <span data-ttu-id="b94a9-139">Создание диска для хранения данных с помощью `withData()` или образа операционной системы с помощью соответствующего метода `withLinux` либо `withWindows` при определении диска.</span><span class="sxs-lookup"><span data-stu-id="b94a9-139">Create a disk to store data using `withData()` or operating system image using the appropriate `withLinux` or `withWindows` method when defining the disk.</span></span> <span data-ttu-id="b94a9-140">Подключение дисков к виртуальным машинам во время создания (`using withNewDataDisk` или `withExistingDataDisk`) или после создания с помощью `update()..apply()` в объекте VirtualMachine.</span><span class="sxs-lookup"><span data-stu-id="b94a9-140">Attach disks to virtual machines either at the time of creation (`using withNewDataDisk` or `withExistingDataDisk`) or after creation by `update()..apply()` on the VirtualMachine object.</span></span>
| [<span data-ttu-id="b94a9-141">DiskSkuTypes</span><span class="sxs-lookup"><span data-stu-id="b94a9-141">DiskSkuTypes</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.compute._disk_sku_types) | <span data-ttu-id="b94a9-142">Класс статических значений для определения диска с помощью тарифного плана хранилища уровня "Стандартный" или ["Премиум"](https://docs.microsoft.com/azure/storage/storage-premium-storage).</span><span class="sxs-lookup"><span data-stu-id="b94a9-142">Class with static values to define a disk with a standard or [premium](https://docs.microsoft.com/azure/storage/storage-premium-storage) storage plan.</span></span>
| [<span data-ttu-id="b94a9-143">KnownLinuxVirtualMachineImage</span><span class="sxs-lookup"><span data-stu-id="b94a9-143">KnownLinuxVirtualMachineImage</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.compute._known_linux_virtual_machine_image) | <span data-ttu-id="b94a9-144">Класс с набором параметров виртуальной машины Linux, используемых с методом `withPopularLinuxImage()` при определении виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="b94a9-144">Class with a set of Linux virtual machine options for use with the `withPopularLinuxImage()` method when defining a virtual machine.</span></span>
| [<span data-ttu-id="b94a9-145">KnownWindowsVirtualMachineImage</span><span class="sxs-lookup"><span data-stu-id="b94a9-145">KnownWindowsVirtualMachineImage</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.compute._known_windows_virtual_machine_image) | <span data-ttu-id="b94a9-146">Класс с набором параметров виртуальной машины Windows, используемых с методом `withPopularWindowsImage()` при определении виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="b94a9-146">Class with a set of Windows virtual machine image options for use with the `withPopularWindowsImage()` method when defining a virtual machine.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b94a9-147">Дополнительная информация</span><span class="sxs-lookup"><span data-stu-id="b94a9-147">Next steps</span></span>

[!INCLUDE [next-steps](includes/java-next-steps.md)]