---
title: Управление масштабируемыми наборами виртуальных машин с помощью Java | Документация Майкрософт
description: Пример кода для управления масштабируемыми наборами виртуальных машин Azure с помощью пакета Azure SDK для Java
author: rloutlaw
manager: douge
ms.assetid: b55923b7-d60a-460d-b77c-af5fac67f1cc
ms.devlang: java
ms.topic: article
ms.service: Azure
ms.technology: Azure
ms.date: 3/30/2017
ms.author: routlaw;asirveda
ms.openlocfilehash: 4653726b387369c18942b6c11392f15b9f0351f3
ms.sourcegitcommit: 1500f341a96d9da461c288abf4baf79f494ae662
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/28/2017
ms.locfileid: "21931160"
---
# <a name="manage-azure-virtual-machine-scale-sets-from-your-java-applications"></a><span data-ttu-id="d198e-103">Управление масштабируемыми наборами виртуальных машин Azure из приложений Java</span><span class="sxs-lookup"><span data-stu-id="d198e-103">Manage Azure virtual machine scale sets from your Java applications</span></span>

<span data-ttu-id="d198e-104">[Этот пример](https://github.com/Azure-Samples/compute-java-manage-virtual-machine-scale-sets) создает [масштабируемый набор виртуальных машин](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-overview) с помощью [библиотек управления Java](https://github.com/Azure/azure-sdk-for-java).</span><span class="sxs-lookup"><span data-stu-id="d198e-104">[This sample](https://github.com/Azure-Samples/compute-java-manage-virtual-machine-scale-sets) creates a  [virtual machine scale set](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-overview) using the [Java management libraries](https://github.com/Azure/azure-sdk-for-java).</span></span> 

## <a name="run-the-sample"></a><span data-ttu-id="d198e-105">Запуск примера</span><span class="sxs-lookup"><span data-stu-id="d198e-105">Run the sample</span></span>

<span data-ttu-id="d198e-106">Создайте [файл проверки подлинности](https://github.com/Azure/azure-sdk-for-java/blob/master/AUTH.md), задайте переменную среды `AZURE_AUTH_LOCATION` и укажите полный путь к файлу на компьютере.</span><span class="sxs-lookup"><span data-stu-id="d198e-106">Create an [authentication file](https://github.com/Azure/azure-sdk-for-java/blob/master/AUTH.md) and set an environment variable `AZURE_AUTH_LOCATION` with the full path to the file on your computer.</span></span> <span data-ttu-id="d198e-107">Далее выполните:</span><span class="sxs-lookup"><span data-stu-id="d198e-107">Then run:</span></span>

```
git clone https://github.com/Azure-Samples/compute-java-manage-virtual-machine-scale-sets.git
cd compute-java-manage-virtual-machine-scale-sets
mvn clean compile exec:java
```

<span data-ttu-id="d198e-108">Просмотрите [полный пример кода на GitHub](https://github.com/Azure-Samples/compute-java-manage-virtual-machine-scale-sets/blob/master/src/main/java/com/microsoft/azure/management/compute/samples/ManageVirtualMachineScaleSet.java).</span><span class="sxs-lookup"><span data-stu-id="d198e-108">View the [complete code sample on GitHub](https://github.com/Azure-Samples/compute-java-manage-virtual-machine-scale-sets/blob/master/src/main/java/com/microsoft/azure/management/compute/samples/ManageVirtualMachineScaleSet.java).</span></span>

## <a name="authenticate-with-azure"></a><span data-ttu-id="d198e-109">Проверка подлинности с помощью Azure</span><span class="sxs-lookup"><span data-stu-id="d198e-109">Authenticate with Azure</span></span>

[!INCLUDE [auth-include](includes/java-auth-include.md)]

## <a name="create-a-virtual-network-for-the-scale-set"></a><span data-ttu-id="d198e-110">Создание виртуальной сети для масштабируемого набора</span><span class="sxs-lookup"><span data-stu-id="d198e-110">Create a virtual network for the scale set</span></span>

```java
Network network = azure.networks().define(vnetName)
                    .withRegion(region)
                    .withNewResourceGroup(rgName)
                    .withAddressSpace("172.16.0.0/16")
                    .defineSubnet("Front-end")
                    .withAddressPrefix("172.16.1.0/24")
                    .attach()
                    .create();
```

<span data-ttu-id="d198e-111">Настройте виртуальную сеть и подсистему балансировки нагрузки, прежде чем создавать определение масштабируемого набора.</span><span class="sxs-lookup"><span data-stu-id="d198e-111">Set up a virtual network and load balancer before creating the scale set definition.</span></span> <span data-ttu-id="d198e-112">Масштабируемый набор использует эти ресурсы для начальной конфигурации.</span><span class="sxs-lookup"><span data-stu-id="d198e-112">The scale set uses these resources for its initial configuration.</span></span>

## <a name="create-a-load-balancer-to-distribute-load-across-the-scale-set"></a><span data-ttu-id="d198e-113">Создание подсистемы балансировки нагрузки для распределения нагрузки по всему масштабируемому набору</span><span class="sxs-lookup"><span data-stu-id="d198e-113">Create a load balancer to distribute load across the scale set</span></span>

```java
LoadBalancer loadBalancer1 = azure.loadBalancers().define(loadBalancerName1)
                    .withRegion(region)
                    .withExistingResourceGroup(rgName)
                    // assign a public IP address to the load balancer
                    .definePublicFrontend(frontendName)
                        .withExistingPublicIPAddress(publicIPAddress)
                        .attach()
                    // Add two backend address pools
                    .defineBackend(backendPoolName1)
                        .attach()
                    .defineBackend(backendPoolName2)
                        .attach()
                    // Add two health probes on 80 and 443
                    .defineHttpProbe(httpProbe)
                        .withRequestPath("/")
                        .withPort(80)
                        .attach()
                    .defineHttpProbe(httpsProbe)
                        .withRequestPath("/")
                        .withPort(443)
                        .attach()

                    // balance HTTP and HTTPs traffic
                    .defineLoadBalancingRule(httpLoadBalancingRule)
                        .withProtocol(TransportProtocol.TCP)
                        .withFrontend(frontendName)
                        .withFrontendPort(80)
                        .withProbe(httpProbe)
                        .withBackend(backendPoolName1)
                        .attach()
                    .defineLoadBalancingRule(httpsLoadBalancingRule)
                        .withProtocol(TransportProtocol.TCP)
                        .withFrontend(frontendName)
                        .withFrontendPort(443)
                        .withProbe(httpsProbe)
                        .withBackend(backendPoolName2)
                        .attach()

                    // Add NAT definitions to enable SSH and telnet to the VMs 
                    .defineInboundNatPool(natPool50XXto22)
                        .withProtocol(TransportProtocol.TCP)
                        .withFrontend(frontendName)
                        .withFrontendPortRange(5000, 5099)
                        .withBackendPort(22)
                        .attach()
                    .defineInboundNatPool(natPool60XXto23)
                        .withProtocol(TransportProtocol.TCP)
                        .withFrontend(frontendName)
                        .withFrontendPortRange(6000, 6099)
                        .withBackendPort(23)
                        .attach()
                    .create();
```

 <span data-ttu-id="d198e-114">Подсистема балансировки нагрузки определяет два пула внутренних сетевых адресов: один для балансировки нагрузки по протоколу HTTP (`backendPoolName1`), другой — для балансировки нагрузки по протоколу HTTPS (`backendPoolName2`).</span><span class="sxs-lookup"><span data-stu-id="d198e-114">The load balancer defines two backend network address pools-one to balance load across HTTP (`backendPoolName1`) and the other to balance load across HTTPS (`backendPoolName2`).</span></span>  <span data-ttu-id="d198e-115">Методы `defineHttpProbe()` настраивают [конечные точки проверки работоспособности](https://docs.microsoft.com/azure/load-balancer/load-balancer-custom-probe-overview) в подсистемах балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="d198e-115">The `defineHttpProbe()` methods set up [health probe endpoints](https://docs.microsoft.com/azure/load-balancer/load-balancer-custom-probe-overview) on the load balancers.</span></span> <span data-ttu-id="d198e-116">Правила преобразования сетевых адресов предоставляют порты 22 и 23 на виртуальных машинах масштабируемых наборов для доступа с помощью telnet и SSH.</span><span class="sxs-lookup"><span data-stu-id="d198e-116">NAT rules expose ports 22 and 23 on the scale set virtual machines for telnet and SSH access.</span></span>

## <a name="create-a-scale-set"></a><span data-ttu-id="d198e-117">Создание масштабируемого набора</span><span class="sxs-lookup"><span data-stu-id="d198e-117">Create a scale set</span></span>
 
```java
 // Create a virtual machine scale set with three virtual machines
 // And, install Apache Web servers on them
VirtualMachineScaleSet virtualMachineScaleSet = azure.virtualMachineScaleSets()
       .define(vmssName)
                .withRegion(region)
                .withExistingResourceGroup(rgName)
                .withSku(VirtualMachineScaleSetSkuTypes.STANDARD_D3_V2)
                .withExistingPrimaryNetworkSubnet(network, "Front-end")
                .withExistingPrimaryInternetFacingLoadBalancer(loadBalancer1)
                .withPrimaryInternetFacingLoadBalancerBackends(backendPoolName1, backendPoolName2)
                .withPrimaryInternetFacingLoadBalancerInboundNatPools(natPool50XXto22, natPool60XXto23)
                .withoutPrimaryInternalLoadBalancer()
                .withPopularLinuxImage(KnownLinuxVirtualMachineImage.UBUNTU_SERVER_16_04_LTS)
                .withRootUsername(userName)
                .withSsh(sshKey)
                .withNewDataDisk(100)
                .withNewDataDisk(100, 1, CachingTypes.READ_WRITE)
                .withNewDataDisk(100, 2, 
                     CachingTypes.READ_WRITE, StorageAccountTypes.STANDARD_LRS)
                .withCapacity(3)
                // Use a VM extension to install Apache Web servers
                .defineNewExtension("CustomScriptForLinux")
                    .withPublisher("Microsoft.OSTCExtensions")
                    .withType("CustomScriptForLinux")
                    .withVersion("1.4")
                    .withMinorVersionAutoUpgrade()
                    .withPublicSetting("fileUris", fileUris)
                    .withPublicSetting("commandToExecute", installCommand)
                    .attach()
                .create();
```

<span data-ttu-id="d198e-118">Используйте определение виртуальной сети и определения подсистемы балансировки нагрузки, созданные на предыдущем шаге, чтобы создать масштабируемый набор с тремя экземплярами Linux (`withCapacity(3)`) и тремя дисками данных размером по 100 ГБ.</span><span class="sxs-lookup"><span data-stu-id="d198e-118">Use the virtual network definition and load balancer definitions created in the previous step to create a scale set with three Linux instances (`withCapacity(3)`) and three 100GB data disks each.</span></span> <span data-ttu-id="d198e-119">Цепочка методов `defineNewExtension()` устанавливает веб-сервер Apache на каждой виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="d198e-119">The `defineNewExtension()` method chain installs the Apache web server on each VM.</span></span>

## <a name="list-virtual-machine-scale-set-network-interfaces"></a><span data-ttu-id="d198e-120">Получение списка сетевых интерфейсов масштабируемого набора виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="d198e-120">List virtual machine scale set network interfaces</span></span>

```java
// List network interfaces on the scale set and iterate through them
PagedList<VirtualMachineScaleSetNetworkInterface> vmssNics = 
     virtualMachineScaleSet.listNetworkInterfaces();
for (VirtualMachineScaleSetNetworkInterface vmssNic : vmssNics) {
    System.out.println(vmssNic.id());
}
```

## <a name="get-ssh-connection-strings-for-each-scale-set-virtual-machine"></a><span data-ttu-id="d198e-121">Получение строк подключения SSH для каждой виртуальной машины в масштабируемом наборе</span><span class="sxs-lookup"><span data-stu-id="d198e-121">Get SSH connection strings for each scale set virtual machine</span></span>

```java
for (VirtualMachineScaleSetVM instance : virtualMachineScaleSet.virtualMachines().list()) {
    System.out.println("Scale set virtual machine instance #" + instance.instanceId());
    System.out.println(instance.id());
    PagedList<VirtualMachineScaleSetNetworkInterface> networkInterfaces = 
         instance.listNetworkInterfaces();
    // Pick the first NIC on the instance and use its primary IP address
    VirtualMachineScaleSetNetworkInterface networkInterface = networkInterfaces.get(0);
    for (VirtualMachineScaleSetNicIPConfiguration ipConfig : networkInterface.ipConfigurations().values()) {
        if (ipConfig.isPrimary()) {
            List<LoadBalancerInboundNatRule> natRules = ipConfig.listAssociatedLoadBalancerInboundNatRules();
            for (LoadBalancerInboundNatRule natRule : natRules) {
                // find rule matching the inbound SSH port on the backend for the IP address
                // and return the SSH connection string to that port on the load balancer
                if (natRule.backendPort() == 22) {
                    System.out.println("SSH connection string: " + userName + 
                        "@" + publicIPAddress.fqdn() + ":" + natRule.frontendPort());
                break;
                }
            }
            break;
        }
    }
}
```

<span data-ttu-id="d198e-122">Пул преобразования сетевых адресов, созданный ранее, сопоставляет порты SSH и telnet (22 и 23 соответственно) на виртуальных машинах с портами в подсистеме балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="d198e-122">The NAT pool created earlier mapped the SSH and telnet ports (22 and 23, respectively) on the virtual machines to ports on the load balancer.</span></span> <span data-ttu-id="d198e-123">Этот код создает строку подключения SSH для каждой виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="d198e-123">This code builds the SSH connection string for each virtual machine.</span></span>

## <a name="stop-the-virtual-machine-scale-set"></a><span data-ttu-id="d198e-124">Остановка масштабируемого набора виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="d198e-124">Stop the virtual machine scale set</span></span>

```java
// stop (not deallocate) all scale set instances
virtualMachineScaleSet.powerOff();
```

<span data-ttu-id="d198e-125">Остановленные виртуальные машины по-прежнему потребляют зарезервированные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="d198e-125">Stopped virtual machines continue to consume reserved resources.</span></span> <span data-ttu-id="d198e-126">Используйте команду `deallocate()`, чтобы остановить операционную систему на виртуальных машинах и освободить соответствующие вычислительные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="d198e-126">Use `deallocate()` to stop the operating system on the virtual machines and release their compute resources.</span></span>

## <a name="deallocate-the-virtual-machine-scale-set"></a><span data-ttu-id="d198e-127">Отмена распределения ресурсов для масштабируемого набора виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="d198e-127">Deallocate the virtual machine scale set</span></span>

```java
// deallocate the virtual machine scale set
virtualMachineScaleSet.deallocate();
```

<span data-ttu-id="d198e-128">Команда deallocate() завершает работу операционной системы на виртуальных машинах и освобождает вычислительные и сетевые ресурсы (например, IP-адреса), которые использовались экземплярами масштабируемого набора.</span><span class="sxs-lookup"><span data-stu-id="d198e-128">Deallocate() shuts down the operating system on the virtual machines and frees up the compute and network resources (such as IP addresses) used by the scale set instances.</span></span> <span data-ttu-id="d198e-129">Плата за хранение на дисках, подключенных к виртуальным машинам (в том числе на дисках с ОС), будет продолжать начисляться.</span><span class="sxs-lookup"><span data-stu-id="d198e-129">You continue to accrue storage charges for any disks (including the OS) attached to the virtual machines.</span></span>

## <a name="start-a-virtual-machine-scale-set"></a><span data-ttu-id="d198e-130">Запуск масштабируемого набора виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="d198e-130">Start a virtual machine scale set</span></span>

```java
// start a deallocated or stopped virtual machine scale set
virtualMachineScaleSet.start();
```

## <a name="update-the-number-of-virtual-machines-instances-in-the-scale-set"></a><span data-ttu-id="d198e-131">Обновление количества экземпляров виртуальных машин в масштабируемом наборе</span><span class="sxs-lookup"><span data-stu-id="d198e-131">Update the number of virtual machines instances in the scale set</span></span>
```java
// increase the number of virtual machine scale set instances from three to six
virtualMachineScaleSet.update()
                    .withCapacity(6)
                    .apply();
```

<span data-ttu-id="d198e-132">Чтобы изменить количество виртуальных машин в масштабируемом наборе, используйте команду `withCapacity()`. Масштабировать емкость каждой виртуальной машины можно с помощью команды `withSku()`.</span><span class="sxs-lookup"><span data-stu-id="d198e-132">Scale the number of virtual machines in the scale set using `withCapacity()` and scale the capacity of each virtual machine using `withSku()`.</span></span>

## <a name="sample-explanation"></a><span data-ttu-id="d198e-133">Описание примера</span><span class="sxs-lookup"><span data-stu-id="d198e-133">Sample explanation</span></span>

<span data-ttu-id="d198e-134">[Пример кода](https://github.com/Azure-Samples/compute-java-manage-virtual-machine-scale-sets/blob/master/src/main/java/com/microsoft/azure/management/compute/samples/ManageVirtualMachineScaleSet.java) сначала создает виртуальную сеть для масштабируемого набора для обмена данными и подсистему балансировки нагрузки для распределения трафика между виртуальными машинами.</span><span class="sxs-lookup"><span data-stu-id="d198e-134">[The sample code](https://github.com/Azure-Samples/compute-java-manage-virtual-machine-scale-sets/blob/master/src/main/java/com/microsoft/azure/management/compute/samples/ManageVirtualMachineScaleSet.java) first creates a virtual network for the scale set to communicate across and a load balancer to distribute traffic across the virtual machines.</span></span> <span data-ttu-id="d198e-135">Цепочка методов `azure.virtualMachineScaleSets().define()...create()` создает масштабируемый набор с тремя экземплярами Linux, которые работают на веб-сервере Apache.</span><span class="sxs-lookup"><span data-stu-id="d198e-135">The `azure.virtualMachineScaleSets().define()...create()` method chain creates the scale set with three Linux instances running the Apache web server.</span></span>    
   
| <span data-ttu-id="d198e-136">Класс, используемый в примере</span><span class="sxs-lookup"><span data-stu-id="d198e-136">Class used in sample</span></span> | <span data-ttu-id="d198e-137">Примечания</span><span class="sxs-lookup"><span data-stu-id="d198e-137">Notes</span></span>
|-------|-------|
| [<span data-ttu-id="d198e-138">VirtualMachineScaleSet</span><span class="sxs-lookup"><span data-stu-id="d198e-138">VirtualMachineScaleSet</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.compute._virtual_machine_scale_set) | <span data-ttu-id="d198e-139">Запуск, остановка, обновление и удаление всех виртуальных машин в масштабируемом наборе, а также выполнение запросов к ним.</span><span class="sxs-lookup"><span data-stu-id="d198e-139">Query, start, stop, update and delete all virtual machines in the scale set.</span></span>
| [<span data-ttu-id="d198e-140">VirtualMachineScaleSetVM</span><span class="sxs-lookup"><span data-stu-id="d198e-140">VirtualMachineScaleSetVM</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.compute._virtual_machine_scale_set_v_m) | <span data-ttu-id="d198e-141">Класс получен из `virtualMachineScaleSet.virtualMachines().get()` или `list()`. Он позволяет запускать, останавливать, настраивать и удалять виртуальные машины в масштабируемом наборе, а также выполнять запросы к ним.</span><span class="sxs-lookup"><span data-stu-id="d198e-141">Retrieved from `virtualMachineScaleSet.virtualMachines().get()` or `list()`, allows you to query, start, stop, configure and delete virtual machines in the scale set.</span></span>
| [<span data-ttu-id="d198e-142">VirtualMachineScaleSetNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="d198e-142">VirtualMachineScaleSetNetworkInterface</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.network._virtual_machine_scale_set_network_interface) | <span data-ttu-id="d198e-143">Класс возвращен из `virtualMachineScaleSet.listNetworkInterfaces()`. Представление только для чтения сетевого интерфейса на виртуальной машине в масштабируемом наборе.</span><span class="sxs-lookup"><span data-stu-id="d198e-143">Returned from `virtualMachineScaleSet.listNetworkInterfaces()`, read-only representation of a network interface on a virtual machine in a scale set.</span></span>
| [<span data-ttu-id="d198e-144">VirtualMachineScaleSetSkuTypes</span><span class="sxs-lookup"><span data-stu-id="d198e-144">VirtualMachineScaleSetSkuTypes</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.compute._virtual_machine_scale_set_sku_types) | <span data-ttu-id="d198e-145">Класс статических полей, используемый для задания [уровня масштабируемого набора виртуальных машин](https://azure.microsoft.com/pricing/details/virtual-machine-scale-sets/linux/). Этот уровень определяет количество ресурсов, которые могут использовать элементы масштабируемого набора.</span><span class="sxs-lookup"><span data-stu-id="d198e-145">Class of static fields used to set the [virtual machine scale set tier](https://azure.microsoft.com/pricing/details/virtual-machine-scale-sets/linux/) used to define how much resources scale set members can consume.</span></span>
| [<span data-ttu-id="d198e-146">VirtualMachineScaleSetNicIpConfiguration</span><span class="sxs-lookup"><span data-stu-id="d198e-146">VirtualMachineScaleSetNicIpConfiguration</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.network._virtual_machine_scale_set_nic_i_p_configuration) | <span data-ttu-id="d198e-147">Используется для запроса IP-конфигурации, связанной с сетевым интерфейсом в масштабируемом наборе виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="d198e-147">Used to query the IP configuration associated with a network interface on a scale set virtual machine.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d198e-148">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d198e-148">Next steps</span></span>

[!INCLUDE [next-steps](includes/java-next-steps.md)]