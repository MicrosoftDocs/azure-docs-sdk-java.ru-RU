---
title: Управление виртуальными сетями Azure с помощью Java | Документация Майкрософт
description: Пример кода для управления виртуальными сетями Azure из кода Java
author: rloutlaw
manager: douge
ms.assetid: 92736911-3df6-46e7-b751-25bb36bf89b9
ms.devlang: java
ms.topic: article
ms.service: Azure
ms.technology: Azure
ms.date: 3/30/2017
ms.author: routlaw;asirveda
ms.openlocfilehash: 6989c5184d09ac011cb39eb21ad8d96db3f0c107
ms.sourcegitcommit: 115f4c8ad07a11f17d79e9d945d63917836b11c8
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "61592559"
---
# <a name="create-and-manage-azure-virtual-networks-from-your-java-apps"></a><span data-ttu-id="e2cb6-103">Создание виртуальных сетей Azure и управление ими с помощью приложений Java</span><span class="sxs-lookup"><span data-stu-id="e2cb6-103">Create and manage Azure virtual networks from your Java apps</span></span>

<span data-ttu-id="e2cb6-104">[Этот пример](https://github.com/Azure-Samples/network-java-manage-virtual-network) создает [виртуальную сеть](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview) для изоляции ресурсов Azure в сегменте сети, которым вы управляете.</span><span class="sxs-lookup"><span data-stu-id="e2cb6-104">[This sample](https://github.com/Azure-Samples/network-java-manage-virtual-network) creates a [virtual network](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview) to isolate your Azure resources on network segment you control.</span></span>

## <a name="run-the-sample"></a><span data-ttu-id="e2cb6-105">Запуск примера</span><span class="sxs-lookup"><span data-stu-id="e2cb6-105">Run the sample</span></span>

<span data-ttu-id="e2cb6-106">Создайте [файл проверки подлинности](https://github.com/Azure/azure-sdk-for-java/blob/master/AUTH.md), задайте переменную среды `AZURE_AUTH_LOCATION` и укажите полный путь к файлу на компьютере.</span><span class="sxs-lookup"><span data-stu-id="e2cb6-106">Create an [authentication file](https://github.com/Azure/azure-sdk-for-java/blob/master/AUTH.md) and set an environment variable `AZURE_AUTH_LOCATION` with the full path to the file on your computer.</span></span> <span data-ttu-id="e2cb6-107">Далее выполните:</span><span class="sxs-lookup"><span data-stu-id="e2cb6-107">Then run:</span></span>

```
git clone https://github.com/Azure-Samples/network-java-manage-virtual-network.git
cd network-java-manage-virtual-network
mvn clean compile exec:java
```

<span data-ttu-id="e2cb6-108">Просмотрите [полный пример кода на GitHub](https://github.com/Azure-Samples/network-java-manage-virtual-network/blob/master/src/main/java/com/microsoft/azure/management/network/samples/ManageVirtualNetwork.java).</span><span class="sxs-lookup"><span data-stu-id="e2cb6-108">View the [complete code sample on GitHub](https://github.com/Azure-Samples/network-java-manage-virtual-network/blob/master/src/main/java/com/microsoft/azure/management/network/samples/ManageVirtualNetwork.java).</span></span>

## <a name="authenticate-with-azure"></a><span data-ttu-id="e2cb6-109">Проверка подлинности с помощью Azure</span><span class="sxs-lookup"><span data-stu-id="e2cb6-109">Authenticate with Azure</span></span>

[!INCLUDE [auth-include](includes/java-auth-include.md)]

## <a name="create-a-network-security-group-to-block-internet-traffic"></a><span data-ttu-id="e2cb6-110">Создание группы безопасности сети для блокирования интернет-трафика</span><span class="sxs-lookup"><span data-stu-id="e2cb6-110">Create a network security group to block Internet traffic</span></span>

```java
// this NSG definition block traffic to and from the public Internet
NetworkSecurityGroup backEndSubnetNsg = azure.networkSecurityGroups()
              .define(vnet1BackEndSubnetNsgName)
                    .withRegion(Region.US_EAST)
                    .withNewResourceGroup(rgName)
                    .defineRule("DenyInternetInComing")
                        .denyInbound()
                        .fromAddress("INTERNET")
                        .fromAnyPort()
                        .toAnyAddress()
                        .toAnyPort()
                        .withAnyProtocol()
                        .attach()
                    .defineRule("DenyInternetOutGoing")
                        .denyOutbound()
                        .fromAnyAddress()
                        .fromAnyPort()
                        .toAddress("INTERNET")
                        .toAnyPort()
                        .withAnyProtocol()
                        .attach()
                    .create();
```

<span data-ttu-id="e2cb6-111">Это [правило безопасности сети](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg) блокирует входящий и исходящий интернет-трафик.</span><span class="sxs-lookup"><span data-stu-id="e2cb6-111">This [network security rule](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg) blocks both inbound and outbound public Internet traffic.</span></span> <span data-ttu-id="e2cb6-112">Эта группа безопасности сети не будет действовать, пока вы не примените ее к подсети в виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="e2cb6-112">This network security group will not have an effect until applied to a subnet in your virtual network.</span></span>

## <a name="create-a-virtual-network-with-two-subnets"></a><span data-ttu-id="e2cb6-113">Создание виртуальной сети с двумя подсетями</span><span class="sxs-lookup"><span data-stu-id="e2cb6-113">Create a virtual network with two subnets</span></span>

```java
// create the a virtual network with two subnets
// assign the backend subnet a rule blocking public internet traffic
Network virtualNetwork1 = azure.networks().define(vnetName1)
                    .withRegion(Region.US_EAST)
                    .withExistingResourceGroup(rgName)
                    .withAddressSpace("192.168.0.0/16")
                    .withSubnet(vnet1FrontEndSubnetName, "192.168.1.0/24")
                    .defineSubnet(vnet1BackEndSubnetName)
                        .withAddressPrefix("192.168.2.0/24")
                        .withExistingNetworkSecurityGroup(backEndSubnetNsg)
                        .attach()
                    .create();
```

<span data-ttu-id="e2cb6-114">Внутренняя подсеть запрещает доступ из Интернета, используя следующий набор правил в группе безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="e2cb6-114">The backend subnet denies Internet access usingfollowing the rules set in the network security group.</span></span> <span data-ttu-id="e2cb6-115">Внешняя подсеть использует [правила по умолчанию](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg), которые разрешают исходящий трафик в Интернет.</span><span class="sxs-lookup"><span data-stu-id="e2cb6-115">The front end subnet uses the [default rules](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg) which allow outbound traffic to the Internet.</span></span>

## <a name="create-a-network-security-group-to-allow-inbound-http-traffic"></a><span data-ttu-id="e2cb6-116">Создание группы безопасности сети, разрешающей входящий трафик HTTP</span><span class="sxs-lookup"><span data-stu-id="e2cb6-116">Create a network security group to allow inbound HTTP traffic</span></span>
```java
// create a rule that allows inbound HTTP and blocks outbound Internet traffic
NetworkSecurityGroup frontEndSubnetNsg = azure.networkSecurityGroups()
               .define(vnet1FrontEndSubnetNsgName)
                    .withRegion(Region.US_EAST)
                    .withExistingResourceGroup(rgName)
                    .defineRule("AllowHttpInComing")
                        .allowInbound()
                        .fromAddress("INTERNET")
                        .fromAnyPort()
                        .toAnyAddress()
                        .toPort(80)
                        .withProtocol(SecurityRuleProtocol.TCP)
                        .attach()
                    .defineRule("DenyInternetOutGoing")
                        .denyOutbound()
                        .fromAnyAddress()
                        .fromAnyPort()
                        .toAddress("INTERNET")
                        .toAnyPort()
                        .withAnyProtocol()
                        .attach()
                    .create();
```

<span data-ttu-id="e2cb6-117">Это правило безопасности сети открывает входящий трафик через порт 80 из общедоступного Интернета и блокирует весь исходящий трафик из сети в Интернет.</span><span class="sxs-lookup"><span data-stu-id="e2cb6-117">This network security rule opens up inbound traffic on port 80 from the public Internet, and blocks all outbound traffic from inside the network to the public Internet.</span></span> 

## <a name="update-a-virtual-network"></a><span data-ttu-id="e2cb6-118">Обновление виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="e2cb6-118">Update a virtual network</span></span>
```java
// update the front end subnet to use the rules in the new network security group
virtualNetwork1.update()
          .updateSubnet(vnet1FrontEndSubnetName)
          .withExistingNetworkSecurityGroup(frontEndSubnetNsg)
          .parent()
          .apply();
```

<span data-ttu-id="e2cb6-119">Обновите внешнюю подсеть, чтобы разрешить входящий трафик HTTP, используя правило безопасности сети, созданное на предыдущем шаге.</span><span class="sxs-lookup"><span data-stu-id="e2cb6-119">Update the front end subnet to allow inbound HTTP traffic using the network security rule created in the previous step.</span></span>

## <a name="create-a-virtual-machine-on-a-subnet"></a><span data-ttu-id="e2cb6-120">Создание виртуальной машины в подсети</span><span class="sxs-lookup"><span data-stu-id="e2cb6-120">Create a virtual machine on a subnet</span></span>
```java
// attach the new VM to the front end subnet on the virtual network
VirtualMachine frontEndVM = azure.virtualMachines().define(frontEndVmName)
                    .withRegion(Region.US_EAST)
                    .withExistingResourceGroup(rgName)
                    .withExistingPrimaryNetwork(virtualNetwork1) 
                    .withSubnet(vnet1FrontEndSubnetName)
                    .withPrimaryPrivateIpAddressDynamic()
                    .withNewPrimaryPublicIpAddress(publicIpAddressLeafDnsForFrontEndVm)
                    .withPopularLinuxImage(KnownLinuxVirtualMachineImage.UBUNTU_SERVER_16_04_LTS)
                    .withRootUsername(userName)
                    .withSsh(sshKey)
                    .withSize(VirtualMachineSizeTypes.STANDARD_D3_V2)
                    .create();
```

<span data-ttu-id="e2cb6-121">Параметры `withExistingPrimaryNetwork()` и `withSubnet()` настраивают виртуальную машину для использования внешней подсети в виртуальной сети, созданной на предыдущих шагах.</span><span class="sxs-lookup"><span data-stu-id="e2cb6-121">`withExistingPrimaryNetwork()` and `withSubnet()` configure the virtual machine to use the front-end subnet on the virtual network created in the previous steps.</span></span>

## <a name="list-virtual-networks-in-a-resource-group"></a><span data-ttu-id="e2cb6-122">Получение списка виртуальных сетей в группе ресурсов</span><span class="sxs-lookup"><span data-stu-id="e2cb6-122">List virtual networks in a resource group</span></span>
```java
// iterate over every virtual network in the resource group 
for (Network virtualNetwork : azure.networks().listByResourceGroup(rgName)) {
    // for each subnet on the virtual network, log the network address prefix 
    for (Map.Entry<String, Subnet> entry : virtualNetwork.subnets().entrySet()) {
        String subnetName = entry.getKey();
        Subnet subnet = entry.getValue();
        System.out.println("Address prefix for subnet " + subnetName + 
             " is " + subnet.addressPrefix());
    }
}
```       

<span data-ttu-id="e2cb6-123">Вы можете получить список объектов `Network` и проверить их с помощью внешней коллекции или выполнить итерацию каждого дочернего ресурса для каждой сети с помощью вложенного цикла, как показано в этом примере.</span><span class="sxs-lookup"><span data-stu-id="e2cb6-123">You can list and inspect `Network` object using the outer collection or iterate through each child resource for each network using the nested for-each loop as seen in this example.</span></span>

## <a name="delete-a-virtual-network"></a><span data-ttu-id="e2cb6-124">Удаление виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="e2cb6-124">Delete a virtual network</span></span>
```java
// if you already have the virtual network object it is easiest to delete by ID
azure.networks().deleteById(virtualNetwork1.id());

// Delete by resource group and name if you don't have the VirtualMachine object
azure.networks().deleteByResourceGroup(rgName,vnetName1);
```

<span data-ttu-id="e2cb6-125">Если удалить виртуальную сеть, удаляются также подсети внутри нее, но правила группы безопасности сети, применяемые к подсетям, не удаляются.</span><span class="sxs-lookup"><span data-stu-id="e2cb6-125">Removing a virtual network deletes the subnets on the network but does not delete the network security group rules applied to the subnets.</span></span> <span data-ttu-id="e2cb6-126">Эти определения можно повторно применить к другим подсетям.</span><span class="sxs-lookup"><span data-stu-id="e2cb6-126">Those definitions can be reapplied to other subnets.</span></span>

## <a name="sample-explanation"></a><span data-ttu-id="e2cb6-127">Описание примера</span><span class="sxs-lookup"><span data-stu-id="e2cb6-127">Sample explanation</span></span>

<span data-ttu-id="e2cb6-128">Этот пример создает виртуальную сеть с двумя подсетями и по одной виртуальной машине в каждой подсети.</span><span class="sxs-lookup"><span data-stu-id="e2cb6-128">This sample creates a virtual network with two subnets and with one virtual machine on each subnet.</span></span> <span data-ttu-id="e2cb6-129">Внутренняя подсеть изолирована от общедоступного Интернета.</span><span class="sxs-lookup"><span data-stu-id="e2cb6-129">The back subnet is cut off from the public Internet.</span></span> <span data-ttu-id="e2cb6-130">Внешняя подсеть принимает входящий трафик HTTP из Интернета.</span><span class="sxs-lookup"><span data-stu-id="e2cb6-130">The front-facing subnet accepts inbound HTTP traffic from the Internet.</span></span> <span data-ttu-id="e2cb6-131">Обе виртуальные машины в виртуальной сети обмениваются данными с помощью стандартных правил групп безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="e2cb6-131">Both virtual machines in the virtual network communicate with each other through the default network security group rules.</span></span>

| <span data-ttu-id="e2cb6-132">Класс, используемый в примере</span><span class="sxs-lookup"><span data-stu-id="e2cb6-132">Class used in sample</span></span> | <span data-ttu-id="e2cb6-133">Примечания</span><span class="sxs-lookup"><span data-stu-id="e2cb6-133">Notes</span></span>
|-------|-------|
| [<span data-ttu-id="e2cb6-134">Сеть</span><span class="sxs-lookup"><span data-stu-id="e2cb6-134">Network</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.network._network) | <span data-ttu-id="e2cb6-135">Представление локального объекта виртуальной сети, созданной с помощью `azure.networks().define()...create()`.</span><span class="sxs-lookup"><span data-stu-id="e2cb6-135">Local object representation of the virtual network created from `azure.networks().define()...create()` .</span></span> <span data-ttu-id="e2cb6-136">Используйте текучую цепочку `update()...apply()` для обновления существующей виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="e2cb6-136">Use the `update()...apply()` fluent chain to update an existing virtual network.</span></span>
| [<span data-ttu-id="e2cb6-137">Подсеть</span><span class="sxs-lookup"><span data-stu-id="e2cb6-137">Subnet</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.network._subnet) | <span data-ttu-id="e2cb6-138">Создание подсетей в виртуальной сети при определении или обновлении сети с помощью `withSubnet()`.</span><span class="sxs-lookup"><span data-stu-id="e2cb6-138">Create subnets on the virtual network when defining or updating the network using `withSubnet()`.</span></span> <span data-ttu-id="e2cb6-139">Получение представлений объекта подсети с помощью `Network.subnets().get()` или `Network.subnets().entrySet()`.</span><span class="sxs-lookup"><span data-stu-id="e2cb6-139">Get object representations of a subnet from `Network.subnets().get()` or `Network.subnets().entrySet()`.</span></span> <span data-ttu-id="e2cb6-140">Эти объекты содержат методы для запроса свойств подсети.</span><span class="sxs-lookup"><span data-stu-id="e2cb6-140">These objects have methods to query subnet properties.</span></span>
| [<span data-ttu-id="e2cb6-141">NetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="e2cb6-141">NetworkSecurityGroup</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.network._network_security_group) | <span data-ttu-id="e2cb6-142">Создан с помощью текучей цепочки `azure.networkSecurityGroups().define()...create()`. Применяется к подсетям при обновлении или создании подсетей в виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="e2cb6-142">Created using the `azure.networkSecurityGroups().define()...create()` fluent chain and then applied to subnets through the updating or creating subnets in a virtual network.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="e2cb6-143">Дополнительная информация</span><span class="sxs-lookup"><span data-stu-id="e2cb6-143">Next steps</span></span>

[!INCLUDE [next-steps](includes/java-next-steps.md)]