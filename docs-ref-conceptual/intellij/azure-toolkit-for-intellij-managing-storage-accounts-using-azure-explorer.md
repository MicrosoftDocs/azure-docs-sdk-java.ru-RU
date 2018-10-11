---
title: Управление учетными записями хранения с помощью Azure Explorer для IntelliJ
description: Вы можете узнать, как управлять учетными записями хранения Azure с помощью Azure Explorer для IntelliJ.
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
ms.openlocfilehash: 4edb8c1ceef508dd251db693ccc3b98d77ec452b
ms.sourcegitcommit: b64017f119177f97da7a5930489874e67b09c0fc
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/09/2018
ms.locfileid: "48899409"
---
# <a name="manage-storage-accounts-by-using-the-azure-explorer-for-intellij"></a><span data-ttu-id="26d85-103">Управление учетными записями хранения с помощью Azure Explorer для IntelliJ</span><span class="sxs-lookup"><span data-stu-id="26d85-103">Manage storage accounts by using the Azure Explorer for IntelliJ</span></span>

<span data-ttu-id="26d85-104">Azure Explorer, входящий в состав набора средств Azure для IntelliJ, предоставляет разработчикам на Java удобное решение для управления учетными записями хранения в их учетной записи Azure из интегрированной среды разработки IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="26d85-104">The Azure Explorer, which is part of the Azure Toolkit for IntelliJ, provides Java developers with an easy-to-use solution for managing storage accounts in their Azure account from inside the IntelliJ integrated development environment (IDE).</span></span>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-intellij-show-azure-explorer](../includes/azure-toolkit-for-intellij-show-azure-explorer.md)]

## <a name="create-a-storage-account-in-intellij"></a><span data-ttu-id="26d85-105">Создание учетной записи хранения в IntelliJ</span><span class="sxs-lookup"><span data-stu-id="26d85-105">Create a storage account in IntelliJ</span></span>

<span data-ttu-id="26d85-106">Чтобы создать учетную запись хранения с помощью Azure Explorer, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="26d85-106">To create a storage account by using the Azure Explorer, do the following:</span></span>

1. <span data-ttu-id="26d85-107">Войдите в свою учетную запись Azure, следуя [Инструкции по входу для набора средств Azure для IntelliJ].</span><span class="sxs-lookup"><span data-stu-id="26d85-107">Sign in to your Azure account by using the [Sign-in instructions for the Azure Toolkit for IntelliJ].</span></span> 

2. <span data-ttu-id="26d85-108">В представлении **Azure Explorer** разверните узел **Azure**, щелкните правой кнопкой мыши элемент **Учетные записи хранения** и выберите **Создать учетную запись хранения**.</span><span class="sxs-lookup"><span data-stu-id="26d85-108">In the **Azure Explorer** view, expand the **Azure** node, right-click **Storage Accounts**, and then click **Create Storage Account**.</span></span>

   ![Команда "Создать учетную запись хранения"][CS01]

3. <span data-ttu-id="26d85-110">В диалоговом окне **Создание учетной записи хранения** укажите следующие параметры.</span><span class="sxs-lookup"><span data-stu-id="26d85-110">In the **Create Storage Account** dialog box, specify the following options:</span></span>

   ![Диалоговое окно "Создание учетной записи хранения"][CS02]

   * <span data-ttu-id="26d85-112">**Имя**: указывает имя для новой учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="26d85-112">**Name**: Specifies the name for the new storage account.</span></span>

   * <span data-ttu-id="26d85-113">**Тип учетной записи**: указывает тип создаваемой учетной записи хранения (например, "хранилище BLOB-объектов").</span><span class="sxs-lookup"><span data-stu-id="26d85-113">**Account kind**: Specifies the type of storage account to create (for example, "Blob storage").</span></span> <span data-ttu-id="26d85-114">Дополнительные сведения см. в статье [Об учетных записях хранения Azure].</span><span class="sxs-lookup"><span data-stu-id="26d85-114">For more information, see [About Azure storage accounts].</span></span> 

   * <span data-ttu-id="26d85-115">**Производительность**: определяет, какое предложение по учетной записи хранения выбранного издателя нужно использовать (например, "Премиум").</span><span class="sxs-lookup"><span data-stu-id="26d85-115">**Performance**: Specifies which storage account offering to use from the selected publisher (for example, "Premium").</span></span> <span data-ttu-id="26d85-116">Дополнительные сведения см. в статье [Целевые показатели масштабируемости и производительности службы хранилища Azure].</span><span class="sxs-lookup"><span data-stu-id="26d85-116">For more information, see [Azure storage scalability and performance targets].</span></span> 

   * <span data-ttu-id="26d85-117">**Репликация**: указывает репликацию для учетной записи хранения (например, "избыточная в пределах зоны").</span><span class="sxs-lookup"><span data-stu-id="26d85-117">**Replication**: Specifies the replication for the storage account (for example, "Zone-Redundant").</span></span> <span data-ttu-id="26d85-118">Дополнительные сведения см. в статье [Репликация службы хранилища Azure].</span><span class="sxs-lookup"><span data-stu-id="26d85-118">For more information, see [Azure storage replication].</span></span> 

   * <span data-ttu-id="26d85-119">**Подписка**: указывает подписку Azure, которую нужно использовать для новой учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="26d85-119">**Subscription**: Specifies the Azure subscription that you want to use for the new storage account.</span></span>

   * <span data-ttu-id="26d85-120">**Расположение**: указывает расположение для создания учетной записи хранения (например, "западная часть США").</span><span class="sxs-lookup"><span data-stu-id="26d85-120">**Location**: Specifies the location where your storage account will be created (for example, "West US").</span></span>

   * <span data-ttu-id="26d85-121">**Группа ресурсов**: указывает группу ресурсов для виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="26d85-121">**Resource Group**: Specifies the resource group for your virtual machine.</span></span> <span data-ttu-id="26d85-122">Выберите один из следующих вариантов:</span><span class="sxs-lookup"><span data-stu-id="26d85-122">Select one of the following options:</span></span>
      * <span data-ttu-id="26d85-123">**Создать**: указывает, что нужно создать группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="26d85-123">**Create new**: Specifies that you want to create a new resource group.</span></span>
      * <span data-ttu-id="26d85-124">**Использовать существующий**: указывает, что вы выберете группу ресурсов, связанную с учетной записью Azure.</span><span class="sxs-lookup"><span data-stu-id="26d85-124">**Use existing**: Specifies that you will select from a list of resource groups that are associated with your Azure account.</span></span>

4. <span data-ttu-id="26d85-125">Указав все перечисленные выше параметры, нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="26d85-125">When you have specified all of the preceding options, click **OK**.</span></span>

## <a name="create-a-storage-container-in-intellij"></a><span data-ttu-id="26d85-126">Создание контейнера хранилища в IntelliJ</span><span class="sxs-lookup"><span data-stu-id="26d85-126">Create a storage container in IntelliJ</span></span>

<span data-ttu-id="26d85-127">Чтобы создать контейнер хранилища с помощью Azure Explorer, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="26d85-127">To create a storage container by using the Azure Explorer, do the following:</span></span>

1. <span data-ttu-id="26d85-128">В представлении Azure Explorer щелкните правой кнопкой мыши учетную запись хранения, для которой нужно создать контейнер, а затем нажмите кнопку **Create blob container** (Создать контейнер BLOB-объектов).</span><span class="sxs-lookup"><span data-stu-id="26d85-128">In the Azure Explorer view, right-click the storage account where you want to create a container, and then click **Create blob container**.</span></span>

   ![Команда Create blob container (Создать контейнер BLOB-объектов)][CC01]

2. <span data-ttu-id="26d85-130">В диалоговом окне **Создание контейнера BLOB-объектов** укажите имя для своего контейнера и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="26d85-130">In the **Create blob container** dialog box, specify the name for your container, and then click **OK**.</span></span> <span data-ttu-id="26d85-131">Дополнительные сведения об именовании контейнеров хранилища см. в статье [Naming and Referencing Containers, Blobs, and Metadata] (Именование контейнеров, больших двоичных объектов и метаданных и ссылка на них).</span><span class="sxs-lookup"><span data-stu-id="26d85-131">For more information about naming storage containers, see [Naming and referencing containers, blobs, and metadata].</span></span>

   ![Диалоговое окно Create Storage Container (Создание контейнера хранилища)][CC02]

## <a name="delete-a-storage-container-in-intellij"></a><span data-ttu-id="26d85-133">Удаление контейнера хранилища в IntelliJ</span><span class="sxs-lookup"><span data-stu-id="26d85-133">Delete a storage container in IntelliJ</span></span>

<span data-ttu-id="26d85-134">Чтобы удалить контейнер хранилища с помощью Azure Explorer, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="26d85-134">To delete a storage container by using the Azure Explorer, do the following:</span></span>

1. <span data-ttu-id="26d85-135">В представлении Azure Explorer щелкните правой кнопкой мыши контейнер хранилища и выберите **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="26d85-135">In the Azure Explorer view, right-click the storage container, and then click **Delete**.</span></span>

   ![Команда Delete storage container (Удаление контейнера хранилища)][DC01]

2. <span data-ttu-id="26d85-137">В диалоговом окне подтверждения нажмите кнопку **Да**.</span><span class="sxs-lookup"><span data-stu-id="26d85-137">In the confirmation window, click **Yes**.</span></span>

   ![Окно подтверждения удаления контейнера хранилища][DC02]

## <a name="delete-a-storage-account-in-intellij"></a><span data-ttu-id="26d85-139">Удаление учетной записи хранения в IntelliJ</span><span class="sxs-lookup"><span data-stu-id="26d85-139">Delete a storage account in IntelliJ</span></span>

<span data-ttu-id="26d85-140">Чтобы удалить учетную запись хранения с помощью Azure Explorer, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="26d85-140">To delete a storage account by using the Azure Explorer, do the following:</span></span>

1. <span data-ttu-id="26d85-141">В представлении **Azure Explorer** щелкните правой кнопкой мыши учетную запись хранения и выберите пункт **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="26d85-141">In the **Azure Explorer** view, right-click the storage account, and then select **Delete**.</span></span>

   ![Меню "Удаление учетной записи хранения"][DS01]

2. <span data-ttu-id="26d85-143">В диалоговом окне подтверждения нажмите кнопку **Да**.</span><span class="sxs-lookup"><span data-stu-id="26d85-143">In the confirmation window, click **Yes**.</span></span>

   ![Окно подтверждения удаления учетной записи хранения][DS02]

## <a name="next-steps"></a><span data-ttu-id="26d85-145">Дополнительная информация</span><span class="sxs-lookup"><span data-stu-id="26d85-145">Next steps</span></span>

<span data-ttu-id="26d85-146">Дополнительные сведения об учетных записях хранения, размерах и ценах см. в следующих ресурсах:</span><span class="sxs-lookup"><span data-stu-id="26d85-146">For more information about Azure storage accounts, sizes, and pricing, see the following resources:</span></span>

* <span data-ttu-id="26d85-147">[Введение в службу хранилища Microsoft Azure]</span><span class="sxs-lookup"><span data-stu-id="26d85-147">[Introduction to Microsoft Azure Storage]</span></span>
* <span data-ttu-id="26d85-148">[Об учетных записях хранения Azure]</span><span class="sxs-lookup"><span data-stu-id="26d85-148">[About Azure storage accounts]</span></span>
* <span data-ttu-id="26d85-149">Размеры учетных записей хранения Azure</span><span class="sxs-lookup"><span data-stu-id="26d85-149">Azure storage-account sizes</span></span>
  * <span data-ttu-id="26d85-150">[Размеры учетных записей хранения Windows в Azure]</span><span class="sxs-lookup"><span data-stu-id="26d85-150">[Sizes for Windows storage accounts in Azure]</span></span>
  * <span data-ttu-id="26d85-151">[Размеры учетных записей хранения Linux в Azure]</span><span class="sxs-lookup"><span data-stu-id="26d85-151">[Sizes for Linux storage accounts in Azure]</span></span>
* <span data-ttu-id="26d85-152">Цены на учетные записи хранения Azure</span><span class="sxs-lookup"><span data-stu-id="26d85-152">Azure storage-account pricing</span></span>
  * <span data-ttu-id="26d85-153">[Windows storage-account pricing] (Цены на учетные записи хранения Windows)</span><span class="sxs-lookup"><span data-stu-id="26d85-153">[Windows storage-account pricing]</span></span>
  * <span data-ttu-id="26d85-154">[Linux storage-account pricing] (Цены на учетные записи хранения Linux)</span><span class="sxs-lookup"><span data-stu-id="26d85-154">[Linux storage-account pricing]</span></span>

[!INCLUDE [azure-toolkit-for-intellij-additional-resources](../includes/azure-toolkit-for-intellij-additional-resources.md)]

<!-- URL List -->

[Инструкции по входу для набора средств Azure для IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Sign-in instructions for the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
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

[CS01]: media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/CS01.png
[CS02]: media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/CS02.png
[CC01]: media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/CC01.png
[CC02]: media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/CC02.png

[DS01]: media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/DS01.png
[DS02]: media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/DS02.png
[DC01]: media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/DC01.png
[DC02]: media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/DC02.png
