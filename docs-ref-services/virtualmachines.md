---
title: "Библиотеки виртуальных машин Azure для Java"
description: 
keywords: Azure, Java, SDK, API, Compute, Virtual Machines
author: douge
ms.author: douge
manager: douge
ms.date: 05/17/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: compute
ms.openlocfilehash: b414f4dc9289958c2562ddc6d41133279f47a45e
ms.sourcegitcommit: ae39830d5a54fedceac78d8df1718e77741e03fa
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/09/2017
---
# <a name="azure-virtual-machine-libraries"></a><span data-ttu-id="f88e4-103">Библиотеки виртуальных машин Azure</span><span class="sxs-lookup"><span data-stu-id="f88e4-103">Azure virtual machine libraries</span></span>

## <a name="overview"></a><span data-ttu-id="f88e4-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="f88e4-104">Overview</span></span>

<span data-ttu-id="f88e4-105">Выполняемые по запросу масштабируемые вычислительные ресурсы под управлением Windows или Linux.</span><span class="sxs-lookup"><span data-stu-id="f88e4-105">On-demand, scalable computing resources running Linux or Windows.</span></span>

<span data-ttu-id="f88e4-106">Чтобы приступить к работе с виртуальными машинами Azure, см. инструкции по [созданию виртуальной машины Linux на портале Azure](/azure/virtual-machines/linux/quick-create-portal).</span><span class="sxs-lookup"><span data-stu-id="f88e4-106">To get started with Azure virtual machines, see [Create a Linux virtual machine with the Azure portal](/azure/virtual-machines/linux/quick-create-portal).</span></span>

## <a name="management-api"></a><span data-ttu-id="f88e4-107">API управления</span><span class="sxs-lookup"><span data-stu-id="f88e4-107">Management API</span></span>

<span data-ttu-id="f88e4-108">Создавайте, настраивайте и масштабируйте виртуальные машины Windows и Linux в Azure с использованием кода и API управления.</span><span class="sxs-lookup"><span data-stu-id="f88e4-108">Create, configure, and scale out Windows and Linux virtual machines in Azure from your code with the management API.</span></span>

<span data-ttu-id="f88e4-109">[Добавьте зависимость](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) в файл Maven `pom.xml`, чтобы использовать API управления в проекте.</span><span class="sxs-lookup"><span data-stu-id="f88e4-109">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the management API in your project.</span></span>  

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-compute</artifactId>
    <version>1.2.1</version>
</dependency>
```   


## <a name="example"></a><span data-ttu-id="f88e4-110">Пример</span><span class="sxs-lookup"><span data-stu-id="f88e4-110">Example</span></span>

<span data-ttu-id="f88e4-111">Создайте виртуальную машину Linux в новой группе ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="f88e4-111">Create a new Linux virtual machine in a new Azure resource group.</span></span>

```java
VirtualMachine newLinuxVm = azure.virtualMachines().define(linuxVmName)
            .withRegion(Region.US_EAST)
            .withNewResourceGroup("myResourceGroup")
            .withNewPrimaryNetwork("10.0.0.0/28")
            .withPrimaryPrivateIpAddressDynamic()
            .withoutPrimaryPublicIpAddress()
            .withPopularLinuxImage(KnownLinuxVirtualMachineImage.UBUNTU_SERVER_16_04_LTS)
            .withRootUsername(userName)
            .withSshKey(key)
            .withSize(VirtualMachineSizeTypes.STANDARD_D3_V2)
            .create();
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="f88e4-112">Обзор API-интерфейсов управления</span><span class="sxs-lookup"><span data-stu-id="f88e4-112">Explore the Management APIs</span></span>](/java/api/overview/azure/virtualmachines/managementapi)


## <a name="samples"></a><span data-ttu-id="f88e4-113">Примеры</span><span class="sxs-lookup"><span data-stu-id="f88e4-113">Samples</span></span>

<span data-ttu-id="f88e4-114">[Управление виртуальными машинами][1] </span><span class="sxs-lookup"><span data-stu-id="f88e4-114">[Manage virtual machines][1] </span></span>  
<span data-ttu-id="f88e4-115">[Управление виртуальными сетями][6] </span><span class="sxs-lookup"><span data-stu-id="f88e4-115">[Manage virtual networks][6] </span></span>  
<span data-ttu-id="f88e4-116">[Создание виртуальной машины из настраиваемого образа][2] </span><span class="sxs-lookup"><span data-stu-id="f88e4-116">[Create a virtual machine from a custom image][2] </span></span>  
<span data-ttu-id="f88e4-117">[Создание виртуальных машин в разных регионах в параллельном режиме][5]  </span><span class="sxs-lookup"><span data-stu-id="f88e4-117">[Create virtual machines across regions in parallel][5]  </span></span>  
<span data-ttu-id="f88e4-118">[Создание масштабируемого набора виртуальных машин с использованием подсистемы балансировки нагрузки][7]</span><span class="sxs-lookup"><span data-stu-id="f88e4-118">[Create a virtual machine scale set with a load balancer][7]</span></span>    

[1]: ../docs-ref-conceptual/java-sdk-manage-virtual-machines.md
[2]: https://azure.microsoft.com/resources/samples/managed-disk-java-create-virtual-machine-using-custom-image/
[5]: ../docs-ref-conceptual/java-sdk-virtual-machines-in-parallel.md
[6]: ../docs-ref-conceptual/java-sdk-manage-virtual-networks.md
[7]: ../docs-ref-conceptual/java-sdk-manage-vm-scalesets.md

<span data-ttu-id="f88e4-119">Ознакомьтесь с [примерами кода Java для виртуальных машин Azure](https://azure.microsoft.com/resources/samples/?platform=java&term=VM), которые можно использовать в своих приложениях.</span><span class="sxs-lookup"><span data-stu-id="f88e4-119">Explore more [sample Java code for Azure virtual machines](https://azure.microsoft.com/resources/samples/?platform=java&term=VM) you can use in your apps.</span></span>