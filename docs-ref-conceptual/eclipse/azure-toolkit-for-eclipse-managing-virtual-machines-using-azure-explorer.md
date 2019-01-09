---
title: Управление виртуальными машинами с помощью Azure Explorer для Eclipse
description: Вы можете узнать, как управлять виртуальными машинами Azure с помощью Azure Explorer для Eclipse.
services: ''
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 11/13/2018
ms.devlang: Java
ms.service: multiple
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: na
ms.openlocfilehash: 7f3b4a6adb4234bbf11f0f7cddafbe99fa0ff3df
ms.sourcegitcommit: 24f037d133875f86761ec893dfa74e723de040b9
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/19/2018
ms.locfileid: "53636700"
---
# <a name="manage-virtual-machines-by-using-the-azure-explorer-for-eclipse"></a><span data-ttu-id="82dbd-103">Управление виртуальными машинами с помощью Azure Explorer для Eclipse</span><span class="sxs-lookup"><span data-stu-id="82dbd-103">Manage virtual machines by using the Azure Explorer for Eclipse</span></span>

<span data-ttu-id="82dbd-104">Средство Azure Explorer, входящее в состав набора средств Azure для Eclipse, предоставляет разработчикам на Java удобное решение для управления виртуальными машинами в их учетной записи Azure из интегрированной среды разработки Eclipse.</span><span class="sxs-lookup"><span data-stu-id="82dbd-104">The Azure Explorer, which is part of the Azure Toolkit for Eclipse, provides Java developers with an easy-to-use solution for managing virtual machines in their Azure account from inside the Eclipse integrated development environment (IDE).</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-eclipse-show-azure-explorer](../includes/azure-toolkit-for-eclipse-show-azure-explorer.md)]

## <a name="create-a-virtual-machine-in-eclipse"></a><span data-ttu-id="82dbd-105">Создание виртуальной машины в Eclipse</span><span class="sxs-lookup"><span data-stu-id="82dbd-105">Create a virtual machine in Eclipse</span></span>

<span data-ttu-id="82dbd-106">Чтобы создать виртуальную машину с помощью Azure Explorer, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="82dbd-106">To create a virtual machine by using the Azure Explorer, do the following:</span></span>

1. <span data-ttu-id="82dbd-107">Войдите в свою учетную запись Azure, следуя [инструкциям по входу для набора средств Azure для Eclipse](https://docs.microsoft.com/java/azure/eclipse/azure-toolkit-for-eclipse-sign-in-instructions).</span><span class="sxs-lookup"><span data-stu-id="82dbd-107">Sign in to your Azure account by using the [Sign-in instructions for the Azure Toolkit for Eclipse](https://docs.microsoft.com/java/azure/eclipse/azure-toolkit-for-eclipse-sign-in-instructions).</span></span>

2. <span data-ttu-id="82dbd-108">В представлении **Azure Explorer** разверните узел **Azure**, щелкните правой кнопкой мыши **Виртуальные машины** и выберите **Создать виртуальную машину**.</span><span class="sxs-lookup"><span data-stu-id="82dbd-108">In the **Azure Explorer** view, expand the **Azure** node, right-click **Virtual Machines**, and then click **Create VM**.</span></span>

   ![Команда "Создать виртуальную машину"][CR01]  

   <span data-ttu-id="82dbd-110">Откроется мастер **создания виртуальной машины**.</span><span class="sxs-lookup"><span data-stu-id="82dbd-110">The **Create new Virtual Machine** wizard opens.</span></span>

3. <span data-ttu-id="82dbd-111">В диалоговом окне **Выбор подписки** выберите подписку и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="82dbd-111">In the **Choose a Subscription** window, select your subscription, and then click **Next**.</span></span>

   ![Диалоговое окно "Выбор подписки"][CR02]

4. <span data-ttu-id="82dbd-113">В диалоговом окне **Выбор образа виртуальной машины** введите следующие значения.</span><span class="sxs-lookup"><span data-stu-id="82dbd-113">In the **Select a Virtual Machine Image** window, enter the following information:</span></span>

   * <span data-ttu-id="82dbd-114">**Расположение.** Указывает расположение для создания виртуальной машины (например, *Западная часть США*).</span><span class="sxs-lookup"><span data-stu-id="82dbd-114">**Location**: Specifies where your virtual machine will be created (for example, *West US*).</span></span>

   * <span data-ttu-id="82dbd-115">**Издатель**: Указывает издателя, создавшего образ, который будет использоваться для создания виртуальной машины (например, *Майкрософт*).</span><span class="sxs-lookup"><span data-stu-id="82dbd-115">**Publisher**: Specifies the publisher that created the image you'll use to create your virtual machine (for example, *Microsoft*).</span></span>

   * <span data-ttu-id="82dbd-116">**Предложение**: Определяет предложение виртуальной машины выбранного издателя (например, *JDK*).</span><span class="sxs-lookup"><span data-stu-id="82dbd-116">**Offer**: Specifies the virtual machine offering to use from the selected publisher (for example, *JDK*).</span></span>

   * <span data-ttu-id="82dbd-117">**SKU**. Указывает нужный номер SKU из выбранного предложения (например, *JDK_8*).</span><span class="sxs-lookup"><span data-stu-id="82dbd-117">**Sku**: Specifies the stockkeeping unit (SKU) to use from the selected offering (for example, *JDK_8*).</span></span>

   * <span data-ttu-id="82dbd-118">**Номер версии**. Указывает, какую версию из выбранного номера SKU нужно использовать.</span><span class="sxs-lookup"><span data-stu-id="82dbd-118">**Version #**: Specifies which version of the selected SKU to use.</span></span>

   ![Диалоговое окно "Выбор образа виртуальной машины"][CR03]

5. <span data-ttu-id="82dbd-120">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="82dbd-120">Click **Next**.</span></span>

6. <span data-ttu-id="82dbd-121">В диалоговом окне **Основные параметры виртуальной машины** введите следующие значения.</span><span class="sxs-lookup"><span data-stu-id="82dbd-121">In the **Virtual Machine Basic Settings** window, enter the following information:</span></span>

   * <span data-ttu-id="82dbd-122">**Имя виртуальной машины**. Указывает имя новой виртуальной машины, которое должно начинаться с буквы и содержать только буквы, цифры и дефисы.</span><span class="sxs-lookup"><span data-stu-id="82dbd-122">**Virtual Machine Name**: Specifies the name for your new virtual machine, which must start with a letter and contain only letters, numbers, and hyphens.</span></span>

   * <span data-ttu-id="82dbd-123">**Размер**: Указывает количество ядер и объем памяти, выделяемые для виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="82dbd-123">**Size**: Specifies the number of cores and memory to allocate for your virtual machine.</span></span>

   * <span data-ttu-id="82dbd-124">**Имя пользователя**. Указывает учетную запись администратора, создаваемую для управления виртуальной машиной.</span><span class="sxs-lookup"><span data-stu-id="82dbd-124">**User name**: Specifies the administrator account to create for managing your virtual machine.</span></span>

   * <span data-ttu-id="82dbd-125">**Пароль** и **Подтверждение**. Указывают пароль для учетной записи администратора.</span><span class="sxs-lookup"><span data-stu-id="82dbd-125">**Password** and **Confirm**: Specifies the password for your administrator account.</span></span>

   ![Диалоговое окно "Основные параметры виртуальной машины"][CR04]

7. <span data-ttu-id="82dbd-127">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="82dbd-127">Click **Next**.</span></span>

8. <span data-ttu-id="82dbd-128">В окне **Создание учетной записи хранения** введите следующие сведения.</span><span class="sxs-lookup"><span data-stu-id="82dbd-128">In the **Create New Storage Account** window, enter the following information:</span></span>

   * <span data-ttu-id="82dbd-129">**Группа ресурсов**. Определяет группу ресурсов для виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="82dbd-129">**Resource Group**: Specifies the resource group for your virtual machine.</span></span> <span data-ttu-id="82dbd-130">Выберите один из следующих вариантов:</span><span class="sxs-lookup"><span data-stu-id="82dbd-130">Select one of the following options:</span></span>
     * <span data-ttu-id="82dbd-131">**Create new** (Создать). Определяет, что нужно создать группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="82dbd-131">**Create new**: Specifies that you want to create a new resource group.</span></span>
     * <span data-ttu-id="82dbd-132">**Использовать существующий**. Указывает, что нужно выбрать группу ресурсов, связанную с учетной записью Azure.</span><span class="sxs-lookup"><span data-stu-id="82dbd-132">**Use existing**: Specifies that you want to select a resource group that is already associated with your Azure account.</span></span>

       ![Диалоговое окно "Создание учетной записи хранения"][CR05]

   * <span data-ttu-id="82dbd-134">**Учетная запись хранения**. Определяет учетную запись хранения, используемую для хранения виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="82dbd-134">**Storage account**: Specifies the storage account to use for storing your virtual machine.</span></span> <span data-ttu-id="82dbd-135">Можно использовать существующую учетную запись хранения или создать новую.</span><span class="sxs-lookup"><span data-stu-id="82dbd-135">You can use an existing storage account or create a new account.</span></span>

   * <span data-ttu-id="82dbd-136">**Виртуальная сеть** и **Подсеть**. Определяют виртуальную сеть и подсеть, к которым будет подключена виртуальная машина.</span><span class="sxs-lookup"><span data-stu-id="82dbd-136">**Virtual Network** and **Subnet**: Specifies the virtual network and subnet that your virtual machine will connect to.</span></span> <span data-ttu-id="82dbd-137">Вы можете выбрать имеющуюся сеть и подсеть или создать их.</span><span class="sxs-lookup"><span data-stu-id="82dbd-137">You can use an existing network and subnet, or you can create a new network and subnet.</span></span> <span data-ttu-id="82dbd-138">При выборе элемента **Создать** отображается следующее диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="82dbd-138">If you select **Create new**, the following dialog box is displayed:</span></span>

      ![Диалоговое окно "Создание виртуальной сети"][CR06]

9. <span data-ttu-id="82dbd-140">В диалоговом окне **Связанные ресурсы** введите следующие значения.</span><span class="sxs-lookup"><span data-stu-id="82dbd-140">In the **Associated Resources** window, enter the following information:</span></span>

   * <span data-ttu-id="82dbd-141">**Общедоступный IP-адрес**. Указывает внешний IP-адрес для виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="82dbd-141">**Public IP address**: Specifies an external-facing IP address for your virtual machine.</span></span> <span data-ttu-id="82dbd-142">Вы можете создать IP-адрес или выбрать значение **(Нет)**, если у виртуальной машины не будет общедоступного IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="82dbd-142">You can choose to create a new IP address or, if your virtual machine will not have a public IP address, you can select **(None)**.</span></span>

   * <span data-ttu-id="82dbd-143">**Группа безопасности сети**. Определяет необязательный сетевой брандмауэр для виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="82dbd-143">**Network security group**: Specifies an optional networking firewall for your virtual machine.</span></span> <span data-ttu-id="82dbd-144">Вы можете выбрать имеющийся брандмауэр или задать значение **(Нет)**, чтобы не использовать брандмауэр.</span><span class="sxs-lookup"><span data-stu-id="82dbd-144">You can select an existing firewall or, if your virtual machine will not use a network firewall, you can select **(None)**.</span></span>

   * <span data-ttu-id="82dbd-145">**Группа доступности**. Определяет необязательную группу доступности, в которую может входить виртуальная машина.</span><span class="sxs-lookup"><span data-stu-id="82dbd-145">**Availability set**: Specifies an optional availability set that your virtual machine can belong to.</span></span> <span data-ttu-id="82dbd-146">Вы можете выбрать существующую группу доступности, создать ее или задать значение **(Нет)**, если виртуальная машина не входит в группу доступности.</span><span class="sxs-lookup"><span data-stu-id="82dbd-146">You can select an existing availability set or create a new availability set or, if your virtual machine will not belong to an availability set, you can select **(None)**.</span></span>

   ![Диалоговое окно "Связанные ресурсы"][CR07]

10. <span data-ttu-id="82dbd-148">Нажмите кнопку **Готово**</span><span class="sxs-lookup"><span data-stu-id="82dbd-148">Click **Finish**.</span></span>  

    <span data-ttu-id="82dbd-149">Новая виртуальная машина отобразится в окне средства Azure Explorer.</span><span class="sxs-lookup"><span data-stu-id="82dbd-149">Your new virtual machine is displayed in the Azure Explorer tool window.</span></span>

    ![Новая виртуальная машина][CR08]

## <a name="restart-a-virtual-machine-in-eclipse"></a><span data-ttu-id="82dbd-151">Перезапуск виртуальной машины в Eclipse</span><span class="sxs-lookup"><span data-stu-id="82dbd-151">Restart a virtual machine in Eclipse</span></span>

<span data-ttu-id="82dbd-152">Чтобы перезапустить виртуальную машину с помощью Azure Explorer в Eclipse, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="82dbd-152">To restart a virtual machine by using the Azure Explorer in Eclipse, do the following:</span></span>

1. <span data-ttu-id="82dbd-153">В представлении **Azure Explorer** щелкните правой кнопкой мыши виртуальную машину и выберите **Перезапустить**.</span><span class="sxs-lookup"><span data-stu-id="82dbd-153">In the **Azure Explorer** view, right-click the virtual machine, and then select **Restart**.</span></span>

   ![Команда перезапуска виртуальной машины][RE01]

1. <span data-ttu-id="82dbd-155">В диалоговом окне подтверждения нажмите кнопку **Да**.</span><span class="sxs-lookup"><span data-stu-id="82dbd-155">In the confirmation window, click **Yes**.</span></span>

   ![Окно подтверждения перезапуска][RE02]

## <a name="shut-down-a-virtual-machine-in-eclipse"></a><span data-ttu-id="82dbd-157">Завершение работы виртуальной машины в Eclipse</span><span class="sxs-lookup"><span data-stu-id="82dbd-157">Shut down a virtual machine in Eclipse</span></span>

<span data-ttu-id="82dbd-158">Чтобы завершить работу виртуальной машины с помощью Azure Explorer в Eclipse, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="82dbd-158">To shut down a running virtual machine by using the Azure Explorer in Eclipse, do the following:</span></span>

1. <span data-ttu-id="82dbd-159">В представлении **Azure Explorer** щелкните правой кнопкой мыши виртуальную машину и выберите **Завершить работу**.</span><span class="sxs-lookup"><span data-stu-id="82dbd-159">In the **Azure Explorer** view, right-click the virtual machine, and then select **Shutdown**.</span></span>

   ![Команда завершения работы виртуальной машины][SH01]

1. <span data-ttu-id="82dbd-161">В диалоговом окне подтверждения нажмите кнопку **Да**.</span><span class="sxs-lookup"><span data-stu-id="82dbd-161">In the confirmation window, click **Yes**.</span></span>

   ![Окно подтверждения завершения работы виртуальной машины][SH02]

## <a name="delete-a-virtual-machine-in-eclipse"></a><span data-ttu-id="82dbd-163">Удаление виртуальной машины в Eclipse</span><span class="sxs-lookup"><span data-stu-id="82dbd-163">Delete a virtual machine in Eclipse</span></span>

<span data-ttu-id="82dbd-164">Чтобы удалить виртуальную машину с помощью Azure Explorer в Eclipse, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="82dbd-164">To delete a virtual machine by using the Azure Explorer in Eclipse, do the following:</span></span>

1. <span data-ttu-id="82dbd-165">В представлении **Azure Explorer** щелкните правой кнопкой мыши виртуальную машину и выберите **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="82dbd-165">In the **Azure Explorer** view, right-click the virtual machine, and then select **Delete**.</span></span>

   ![Команда удаления виртуальной машины][DE01]

1. <span data-ttu-id="82dbd-167">В диалоговом окне подтверждения нажмите кнопку **Да**.</span><span class="sxs-lookup"><span data-stu-id="82dbd-167">In the confirmation window, click **Yes**.</span></span>

   ![Окно подтверждения удаления виртуальной машины][DE02]

## <a name="next-steps"></a><span data-ttu-id="82dbd-169">Дополнительная информация</span><span class="sxs-lookup"><span data-stu-id="82dbd-169">Next steps</span></span>

<span data-ttu-id="82dbd-170">Дополнительные сведения о размерах виртуальных машин Azure и ценах на них см. в следующих ресурсах:</span><span class="sxs-lookup"><span data-stu-id="82dbd-170">For more information about Azure virtual-machine sizes and pricing, see the following resources:</span></span>

* <span data-ttu-id="82dbd-171">Размеры виртуальных машин Azure</span><span class="sxs-lookup"><span data-stu-id="82dbd-171">Azure virtual-machine sizes</span></span>
  * <span data-ttu-id="82dbd-172">[Размеры виртуальных машин Windows в Azure]</span><span class="sxs-lookup"><span data-stu-id="82dbd-172">[Sizes for Windows virtual machines in Azure]</span></span>
  * <span data-ttu-id="82dbd-173">[Размеры виртуальных машин Linux в Azure]</span><span class="sxs-lookup"><span data-stu-id="82dbd-173">[Sizes for Linux virtual machines in Azure]</span></span>
* <span data-ttu-id="82dbd-174">Цены на виртуальные машины Azure</span><span class="sxs-lookup"><span data-stu-id="82dbd-174">Azure virtual-machine pricing</span></span>
  * <span data-ttu-id="82dbd-175">[Цены на виртуальные машины Windows]</span><span class="sxs-lookup"><span data-stu-id="82dbd-175">[Windows virtual-machine pricing]</span></span>
  * <span data-ttu-id="82dbd-176">[Цены на виртуальные машины Linux]</span><span class="sxs-lookup"><span data-stu-id="82dbd-176">[Linux virtual-machine pricing]</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-additional-resources](../includes/azure-toolkit-for-eclipse-additional-resources.md)]

<!-- URL List -->

[Размеры виртуальных машин Windows в Azure]: /azure/virtual-machines/virtual-machines-windows-sizes
[Sizes for Windows virtual machines in Azure]: /azure/virtual-machines/virtual-machines-windows-sizes
[Размеры виртуальных машин Linux в Azure]: /azure/virtual-machines/virtual-machines-linux-sizes
[Sizes for Linux virtual machines in Azure]: /azure/virtual-machines/virtual-machines-linux-sizes
[Цены на виртуальные машины Windows]: https://azure.microsoft.com/pricing/details/virtual-machines/windows/
[Windows virtual-machine pricing]: https://azure.microsoft.com/pricing/details/virtual-machines/windows/
[Цены на виртуальные машины Linux]: https://azure.microsoft.com/pricing/details/virtual-machines/linux/
[Linux virtual-machine pricing]: https://azure.microsoft.com/pricing/details/virtual-machines/linux/

<!-- IMG List -->

[RE01]: media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/RE01.png
[RE02]: media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/RE02.png

[SH01]: media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/SH01.png
[SH02]: media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/SH02.png

[DE01]: media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/DE01.png
[DE02]: media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/DE02.png

[CR01]: media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR01.png
[CR02]: media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR02.png
[CR03]: media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR03.png
[CR04]: media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR04.png
[CR05]: media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR05.png
[CR06]: media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR06.png
[CR07]: media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR07.png
[CR08]: media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR08.png
