---
title: Управление учетными записями хранения с помощью Azure Explorer для Eclipse
description: Вы можете узнать, как управлять учетными записями хранения Azure с помощью Azure Explorer для Eclipse.
services: ''
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 02/01/2018
ms.devlang: Java
ms.service: multiple
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: na
ms.openlocfilehash: 310d95436189af09f794154f4c9f0e71c47d88c8
ms.sourcegitcommit: b64017f119177f97da7a5930489874e67b09c0fc
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/09/2018
ms.locfileid: "48899444"
---
# <a name="manage-storage-accounts-by-using-the-azure-explorer-for-eclipse"></a><span data-ttu-id="3a8b5-103">Управление учетными записями хранения с помощью Azure Explorer для Eclipse</span><span class="sxs-lookup"><span data-stu-id="3a8b5-103">Manage storage accounts by using the Azure Explorer for Eclipse</span></span>

<span data-ttu-id="3a8b5-104">Azure Explorer, входящий в состав набора средств Azure для Eclipse, предоставляет разработчикам на Java удобное решение для управления учетными записями хранения в их учетной записи Azure из интегрированной среды разработки Eclipse.</span><span class="sxs-lookup"><span data-stu-id="3a8b5-104">The Azure Explorer, which is part of the Azure Toolkit for Eclipse, provides Java developers with an easy-to-use solution for managing storage accounts in their Azure account from inside the Eclipse integrated development environment (IDE).</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-eclipse-show-azure-explorer](../includes/azure-toolkit-for-eclipse-show-azure-explorer.md)]

## <a name="create-a-storage-account-in-eclipse"></a><span data-ttu-id="3a8b5-105">Создание учетной записи хранения в Eclipse</span><span class="sxs-lookup"><span data-stu-id="3a8b5-105">Create a storage account in Eclipse</span></span>

<span data-ttu-id="3a8b5-106">Чтобы создать учетную запись хранения с помощью Azure Explorer, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="3a8b5-106">To create a storage account by using the Azure Explorer, do the following:</span></span>

1. <span data-ttu-id="3a8b5-107">Войдите в свою учетную запись Azure, следуя инструкциям из статьи [Инструкции по входу для набора средств Azure для Eclipse](https://docs.microsoft.com/java/azure/eclipse/azure-toolkit-for-eclipse-sign-in-instructions).</span><span class="sxs-lookup"><span data-stu-id="3a8b5-107">Sign in to your Azure account by using the [Sign-in instructions for the Azure Toolkit for Eclipse](https://docs.microsoft.com/java/azure/eclipse/azure-toolkit-for-eclipse-sign-in-instructions).</span></span>

1. <span data-ttu-id="3a8b5-108">В представлении **Azure Explorer** разверните узел **Azure**, щелкните правой кнопкой мыши элемент **Учетные записи хранения** и выберите **Создать учетную запись хранения**.</span><span class="sxs-lookup"><span data-stu-id="3a8b5-108">In the **Azure Explorer** view, expand the **Azure** node, right-click **Storage Accounts**, and then click **Create Storage Account**.</span></span>

   ![Команда "Создать учетную запись хранения"][CS01]

1. <span data-ttu-id="3a8b5-110">В диалоговом окне **Создание учетной записи хранения** укажите следующие параметры.</span><span class="sxs-lookup"><span data-stu-id="3a8b5-110">In the **Create Storage Account** dialog box, specify the following options:</span></span>

   ![Диалоговое окно "Создание учетной записи хранения"][CS02]

   * <span data-ttu-id="3a8b5-112">**Имя**: указывает имя для новой учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="3a8b5-112">**Name**: Specifies the name for the new storage account.</span></span>

   * <span data-ttu-id="3a8b5-113">**Подписка**: указывает подписку Azure, которую нужно использовать для новой учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="3a8b5-113">**Subscription**: Specifies the Azure subscription that you want to use for the new storage account.</span></span>

   * <span data-ttu-id="3a8b5-114">**Группа ресурсов**: определяет группу ресурсов для виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="3a8b5-114">**Resource Group**: Specifies the resource group for your virtual machine.</span></span> <span data-ttu-id="3a8b5-115">Выберите один из следующих вариантов:</span><span class="sxs-lookup"><span data-stu-id="3a8b5-115">Select one of the following options:</span></span>
      * <span data-ttu-id="3a8b5-116">**Создать**: указывает, что нужно создать группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="3a8b5-116">**Create New**: Specifies that you want to create a new resource group.</span></span>
      * <span data-ttu-id="3a8b5-117">**Использовать существующий**: указывает, что вы выберете группу ресурсов, связанную с учетной записью Azure.</span><span class="sxs-lookup"><span data-stu-id="3a8b5-117">**Use Existing**: Specifies that you will select from a list of resource groups that are associated with your Azure account.</span></span>

   * <span data-ttu-id="3a8b5-118">**Регион**: указывает расположение для создания учетной записи хранения, например "западная часть США".</span><span class="sxs-lookup"><span data-stu-id="3a8b5-118">**Region**: Specifies the location where your storage account will be created (for example, "West US").</span></span>

   * <span data-ttu-id="3a8b5-119">**Тип учетной записи**: указывает тип создаваемой учетной записи хранения (например, "хранилище BLOB-объектов").</span><span class="sxs-lookup"><span data-stu-id="3a8b5-119">**Account kind**: Specifies the type of storage account to create (for example, "Blob storage").</span></span> <span data-ttu-id="3a8b5-120">Дополнительные сведения см. в статье [Об учетных записях хранения Azure].</span><span class="sxs-lookup"><span data-stu-id="3a8b5-120">For more information, see [About Azure storage accounts].</span></span>

   * <span data-ttu-id="3a8b5-121">**Производительность**: определяет, какое предложение по учетной записи хранения выбранного издателя нужно использовать (например, "Премиум").</span><span class="sxs-lookup"><span data-stu-id="3a8b5-121">**Performance**: Specifies which storage account offering to use from the selected publisher (for example, "Premium").</span></span> <span data-ttu-id="3a8b5-122">Дополнительные сведения см. в статье [Целевые показатели масштабируемости и производительности службы хранилища Azure].</span><span class="sxs-lookup"><span data-stu-id="3a8b5-122">For more information, see [Azure storage scalability and performance targets].</span></span>

   * <span data-ttu-id="3a8b5-123">**Репликация**: указывает репликацию для учетной записи хранения (например, "избыточная в пределах зоны").</span><span class="sxs-lookup"><span data-stu-id="3a8b5-123">**Replication**: Specifies the replication for the storage account (for example, "Zone-Redundant").</span></span> <span data-ttu-id="3a8b5-124">Дополнительные сведения см. в статье [Репликация службы хранилища Azure].</span><span class="sxs-lookup"><span data-stu-id="3a8b5-124">For more information, see [Azure storage replication].</span></span>

1. <span data-ttu-id="3a8b5-125">Указав все перечисленные выше параметры, нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="3a8b5-125">When you have specified all of the preceding options, click **Create**.</span></span>

## <a name="create-a-storage-container-in-eclipse"></a><span data-ttu-id="3a8b5-126">Создание контейнера хранилища в Eclipse</span><span class="sxs-lookup"><span data-stu-id="3a8b5-126">Create a storage container in Eclipse</span></span>

<span data-ttu-id="3a8b5-127">Чтобы создать контейнер хранилища с помощью Azure Explorer, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="3a8b5-127">To create a storage container by using the Azure Explorer, do the following:</span></span>

1. <span data-ttu-id="3a8b5-128">В представлении **Azure Explorer** щелкните правой кнопкой мыши учетную запись хранения, для которой нужно создать контейнер, а затем нажмите кнопку **Создать контейнер BLOB-объектов**.</span><span class="sxs-lookup"><span data-stu-id="3a8b5-128">In the **Azure Explorer** view, right-click the storage account where you want to create a container, and then click **Create blob container**.</span></span>

   ![Команда "Создать контейнер BLOB-объектов"][CC01]

1. <span data-ttu-id="3a8b5-130">В диалоговом окне **Создание контейнера BLOB-объектов** укажите имя для своего контейнера и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="3a8b5-130">In the **Create blob container** dialog box, specify the name for your container, and then click **OK**.</span></span> <span data-ttu-id="3a8b5-131">Дополнительные сведения об именовании контейнеров хранилища см. в статье [Naming and Referencing Containers, Blobs, and Metadata] (Именование контейнеров, больших двоичных объектов и метаданных и ссылка на них).</span><span class="sxs-lookup"><span data-stu-id="3a8b5-131">For more information about naming storage containers, see [Naming and referencing containers, blobs, and metadata].</span></span>

   ![Диалоговое окно "Создание контейнера BLOB-объектов"][CC02]

## <a name="delete-a-storage-container-in-eclipse"></a><span data-ttu-id="3a8b5-133">Удаление контейнера хранилища в Eclipse</span><span class="sxs-lookup"><span data-stu-id="3a8b5-133">Delete a storage container in Eclipse</span></span>

<span data-ttu-id="3a8b5-134">Чтобы удалить контейнер хранилища с помощью Azure Explorer, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="3a8b5-134">To delete a storage container by using the Azure Explorer, do the following:</span></span>

1. <span data-ttu-id="3a8b5-135">В представлении **Azure Explorer** щелкните правой кнопкой мыши контейнер хранилища и выберите **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="3a8b5-135">In the **Azure Explorer** view, right-click the storage container, and then click **Delete**.</span></span>

   ![Команда "Удалить контейнер хранилища"][DC01]

1. <span data-ttu-id="3a8b5-137">В диалоговом окне подтверждения нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="3a8b5-137">In the confirmation window, click **OK**.</span></span>

   ![Окно подтверждения удаления контейнера хранилища][DC02]

## <a name="delete-a-storage-account-in-eclipse"></a><span data-ttu-id="3a8b5-139">Удаление учетной записи хранения в Eclipse</span><span class="sxs-lookup"><span data-stu-id="3a8b5-139">Delete a storage account in Eclipse</span></span>

<span data-ttu-id="3a8b5-140">Чтобы удалить учетную запись хранения с помощью Azure Explorer, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="3a8b5-140">To delete a storage account by using the Azure Explorer, do the following:</span></span>

1. <span data-ttu-id="3a8b5-141">В представлении **Azure Explorer** щелкните правой кнопкой мыши учетную запись хранения и выберите пункт **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="3a8b5-141">In the **Azure Explorer** view, right-click the storage account, and then click **Delete**.</span></span>

   ![Команда "Удалить учетную запись хранения"][DS01]

1. <span data-ttu-id="3a8b5-143">В диалоговом окне подтверждения нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="3a8b5-143">In the confirmation window, click **OK**.</span></span>

   ![Окно подтверждения удаления учетной записи хранения][DS02]

## <a name="next-steps"></a><span data-ttu-id="3a8b5-145">Дополнительная информация</span><span class="sxs-lookup"><span data-stu-id="3a8b5-145">Next steps</span></span>

<span data-ttu-id="3a8b5-146">Дополнительные сведения об учетных записях хранения, размерах и ценах см. в следующих ресурсах:</span><span class="sxs-lookup"><span data-stu-id="3a8b5-146">For more information about Azure storage accounts, sizes, and pricing, see the following resources:</span></span>

* <span data-ttu-id="3a8b5-147">[Введение в службу хранилища Microsoft Azure]</span><span class="sxs-lookup"><span data-stu-id="3a8b5-147">[Introduction to Microsoft Azure Storage]</span></span>
* <span data-ttu-id="3a8b5-148">[Об учетных записях хранения Azure]</span><span class="sxs-lookup"><span data-stu-id="3a8b5-148">[About Azure storage accounts]</span></span>
* <span data-ttu-id="3a8b5-149">Размеры учетных записей хранения Azure</span><span class="sxs-lookup"><span data-stu-id="3a8b5-149">Azure storage-account sizes</span></span>
  * <span data-ttu-id="3a8b5-150">[Размеры учетных записей хранения Windows в Azure]</span><span class="sxs-lookup"><span data-stu-id="3a8b5-150">[Sizes for Windows storage accounts in Azure]</span></span>
  * <span data-ttu-id="3a8b5-151">[Размеры учетных записей хранения Linux в Azure]</span><span class="sxs-lookup"><span data-stu-id="3a8b5-151">[Sizes for Linux storage accounts in Azure]</span></span>
* <span data-ttu-id="3a8b5-152">Цены на учетные записи хранения Azure</span><span class="sxs-lookup"><span data-stu-id="3a8b5-152">Azure storage-account pricing</span></span>
  * <span data-ttu-id="3a8b5-153">[Windows storage-account pricing] (Цены на учетные записи хранения Windows)</span><span class="sxs-lookup"><span data-stu-id="3a8b5-153">[Windows storage-account pricing]</span></span>
  * <span data-ttu-id="3a8b5-154">[Linux storage-account pricing] (Цены на учетные записи хранения Linux)</span><span class="sxs-lookup"><span data-stu-id="3a8b5-154">[Linux storage-account pricing]</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-additional-resources](../includes/azure-toolkit-for-eclipse-additional-resources.md)]

<!-- URL List -->

[Введение в службу хранилища Microsoft Azure]: /azure/storage/storage-introduction
[Introduction to Microsoft Azure Storage]: /azure/storage/storage-introduction
[Об учетных записях хранения Azure]: /azure/storage/storage-create-storage-account
[About Azure storage accounts]: /azure/storage/storage-create-storage-account
[Репликация службы хранилища Azure]: /azure/storage/storage-redundancy
[Azure storage replication]: /azure/storage/storage-redundancy
[Целевые показатели масштабируемости и производительности службы хранилища Azure]: /azure/storage/storage-scalability-targets
[Azure storage scalability and Performance Targets]: /azure/storage/storage-scalability-targets
[Naming and Referencing Containers, Blobs, and Metadata]: http://go.microsoft.com/fwlink/?LinkId=255555 (Именование контейнеров, больших двоичных объектов и метаданных и ссылка на них)
[Naming and referencing containers, blobs, and metadata]: http://go.microsoft.com/fwlink/?LinkId=255555

[Размеры учетных записей хранения Windows в Azure]: /azure/virtual-machines/virtual-machines-windows-sizes
[Sizes for Windows storage accounts in Azure]: /azure/virtual-machines/virtual-machines-windows-sizes
[Размеры учетных записей хранения Linux в Azure]: /azure/virtual-machines/virtual-machines-linux-sizes
[Sizes for Linux storage accounts in Azure]: /azure/virtual-machines/virtual-machines-linux-sizes
[Windows storage-account pricing]: /pricing/details/virtual-machines/windows/ (Цены на учетные записи хранения Windows)
[Linux storage-account pricing]: /pricing/details/virtual-machines/linux/ (Цены на учетные записи хранения Linux)

<!-- IMG List -->

[CS01]: media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/CS01.png
[CS02]: media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/CS02.png
[CC01]: media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/CC01.png
[CC02]: media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/CC02.png

[DS01]: media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/DS01.png
[DS02]: media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/DS02.png
[DC01]: media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/DC01.png
[DC02]: media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/DC02.png
