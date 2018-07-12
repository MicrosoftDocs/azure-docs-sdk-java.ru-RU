---
title: Управление виртуальными машинами с помощью Azure Explorer для IntelliJ
description: Вы можете узнать, как управлять виртуальными машинами Azure с помощью Azure Explorer для IntelliJ.
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
ms.openlocfilehash: 213efa7fc31705b0ffcba6f2fe40e7186a365fae
ms.sourcegitcommit: 0ed7c5af0152125322ff1d265c179f35028f3c15
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2018
ms.locfileid: "38074534"
---
# <a name="manage-virtual-machines-by-using-the-azure-explorer-for-intellij"></a><span data-ttu-id="341af-103">Управление виртуальными машинами с помощью Azure Explorer для IntelliJ</span><span class="sxs-lookup"><span data-stu-id="341af-103">Manage virtual machines by using the Azure Explorer for IntelliJ</span></span>

<span data-ttu-id="341af-104">Azure Explorer, входящий в состав набора средств Azure для IntelliJ, предоставляет разработчикам на Java удобное решение для управления виртуальными машинами в их учетной записи Azure из интегрированной среды разработки IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="341af-104">The Azure Explorer, which is part of the Azure Toolkit for IntelliJ, provides Java developers with an easy-to-use solution for managing virtual machines in their Azure account from inside the IntelliJ integrated development environment (IDE).</span></span>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-intellij-show-azure-explorer](../includes/azure-toolkit-for-intellij-show-azure-explorer.md)]

## <a name="create-a-virtual-machine-in-intellij"></a><span data-ttu-id="341af-105">Создание виртуальной машины в IntelliJ</span><span class="sxs-lookup"><span data-stu-id="341af-105">Create a virtual machine in IntelliJ</span></span>

<span data-ttu-id="341af-106">Чтобы создать виртуальную машину с помощью Azure Explorer, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="341af-106">To create a virtual machine by using the Azure Explorer, do the following:</span></span> 

1. <span data-ttu-id="341af-107">Войдите в свою учетную запись Azure, следуя инструкциям из статьи [Инструкции по входу для набора средств Azure для IntelliJ].</span><span class="sxs-lookup"><span data-stu-id="341af-107">Sign in to your Azure account by using the steps in the [Sign-in instructions for the Azure Toolkit for IntelliJ] article.</span></span>

2. <span data-ttu-id="341af-108">В представлении **Azure Explorer** разверните узел **Azure**, щелкните правой кнопкой мыши **Виртуальные машины** и выберите **Создать виртуальную машину**.</span><span class="sxs-lookup"><span data-stu-id="341af-108">In the **Azure Explorer** view, expand the **Azure** node, right-click **Virtual Machines**, and then click **Create VM**.</span></span> 

   <span data-ttu-id="341af-109">![Команда "Создать виртуальную машину"][CR01]</span><span class="sxs-lookup"><span data-stu-id="341af-109">![The Create VM command][CR01]</span></span>  
    <span data-ttu-id="341af-110">Откроется мастер **создания виртуальной машины**.</span><span class="sxs-lookup"><span data-stu-id="341af-110">The **Create new Virtual Machine** wizard opens.</span></span>

3. <span data-ttu-id="341af-111">В диалоговом окне **Выбор подписки** выберите подписку и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="341af-111">In the **Choose a Subscription** window, select your subscription, and then click **Next**.</span></span> 

   ![Диалоговое окно "Выбор подписки"][CR02]

4. <span data-ttu-id="341af-113">В диалоговом окне **Выбор образа виртуальной машины** введите следующие значения.</span><span class="sxs-lookup"><span data-stu-id="341af-113">In the **Select a Virtual Machine Image** window, enter the following information:</span></span>

   * <span data-ttu-id="341af-114">**Расположение**: указывает расположение для создания виртуальной машины (например, *Западная часть США*).</span><span class="sxs-lookup"><span data-stu-id="341af-114">**Location**: Specifies where your virtual machine will be created (for example, *West US*).</span></span> 

   * <span data-ttu-id="341af-115">**Recommended Image** (Рекомендуемый образ): указывает, что вы выберете образ из сокращенного списка часто используемых образов.</span><span class="sxs-lookup"><span data-stu-id="341af-115">**Recommended image**: Specifies that you will choose an image from an abbreviated list of commonly used images.</span></span>

   * <span data-ttu-id="341af-116">**Пользовательский образ**: указывает, что вы выберете пользовательский образ, указав следующие сведения:</span><span class="sxs-lookup"><span data-stu-id="341af-116">**Custom image**: Specifies that you will choose a custom image by providing the following information:</span></span>

      * <span data-ttu-id="341af-117">**Издатель**: указывает издателя, создавшего образ, который будет использоваться для виртуальной машины (например, *Майкрософт*).</span><span class="sxs-lookup"><span data-stu-id="341af-117">**Publisher**: Specifies the publisher that created the image that you will use for your virtual machine (for example, *Microsoft*).</span></span>

      * <span data-ttu-id="341af-118">**Предложение**: определяет предложение виртуальной машины выбранного издателя (например, *JDK*).</span><span class="sxs-lookup"><span data-stu-id="341af-118">**Offer**: Specifies the virtual machine offering to use from the selected publisher (for example, *JDK*).</span></span>

      * <span data-ttu-id="341af-119">**SKU**: указывает нужный номер SKU из выбранного предложения (например, *JDK_8*).</span><span class="sxs-lookup"><span data-stu-id="341af-119">**Sku**: Specifies the stockkeeping unit (SKU) to use from the selected offering (for example, *JDK_8*).</span></span>

      * <span data-ttu-id="341af-120">**Номер версии**: указывает, какую версию из выбранного номера SKU нужно использовать.</span><span class="sxs-lookup"><span data-stu-id="341af-120">**Version #**: Specifies which version of the selected SKU to use.</span></span>

   ![Диалоговое окно "Выбор образа виртуальной машины"][CR03]

5. <span data-ttu-id="341af-122">Нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="341af-122">Click **Next**.</span></span> 

6. <span data-ttu-id="341af-123">В диалоговом окне **Основные параметры виртуальной машины** введите следующие значения.</span><span class="sxs-lookup"><span data-stu-id="341af-123">In the **Virtual Machine Basic Settings** window, enter the following information:</span></span>

   * <span data-ttu-id="341af-124">**Имя виртуальной машины**: указывает имя новой виртуальной машины, которое должно начинаться с буквы и содержать только буквы, цифры и дефисы.</span><span class="sxs-lookup"><span data-stu-id="341af-124">**Virtual machine name**: Specifies the name for your new virtual machine, which must start with a letter and contain only letters, numbers, and hyphens.</span></span>

   * <span data-ttu-id="341af-125">**Размер**: указывает количество ядер и объем памяти, выделяемые для виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="341af-125">**Size**: Specifies the number of cores and memory to allocate for your virtual machine.</span></span>

   * <span data-ttu-id="341af-126">**Имя пользователя**: указывает учетную запись администратора, создаваемую для управления виртуальной машиной.</span><span class="sxs-lookup"><span data-stu-id="341af-126">**User name**: Specifies the administrator account to create for managing your virtual machine.</span></span>

   * <span data-ttu-id="341af-127">**Пароль** и **Подтверждение**: указывают пароль для учетной записи администратора.</span><span class="sxs-lookup"><span data-stu-id="341af-127">**Password** and **Confirm**: Specifies the password for your administrator account.</span></span>

   ![Диалоговое окно "Основные параметры виртуальной машины"][CR04]

7. <span data-ttu-id="341af-129">Нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="341af-129">Click **Next**.</span></span> 

8. <span data-ttu-id="341af-130">В диалоговом окне **Связанные ресурсы** введите следующие значения.</span><span class="sxs-lookup"><span data-stu-id="341af-130">In the **Associated Resources** window, enter the following information:</span></span>

   * <span data-ttu-id="341af-131">**Группа ресурсов**: указывает группу ресурсов для виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="341af-131">**Resource group**: Specifies the resource group for your virtual machine.</span></span> <span data-ttu-id="341af-132">Выберите один из следующих вариантов:</span><span class="sxs-lookup"><span data-stu-id="341af-132">Select one of the following options:</span></span>
      * <span data-ttu-id="341af-133">**Создать**: определяет, что нужно создать группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="341af-133">**Create new**: Specifies that you want to create a new resource group.</span></span>
      * <span data-ttu-id="341af-134">**Использовать существующий**: указывает, что нужно выбрать группу ресурсов, связанную с учетной записью Azure.</span><span class="sxs-lookup"><span data-stu-id="341af-134">**Use existing**: Specifies that you want to select from a list of resource groups that are associated with your Azure account.</span></span>

       ![Диалоговое окно "Связанные ресурсы"][CR07]

   * <span data-ttu-id="341af-136">**Учетная запись хранения**: указывает учетную запись хранения, используемую для хранения виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="341af-136">**Storage account**: Specifies the storage account to use for storing your virtual machine.</span></span> <span data-ttu-id="341af-137">Вы можете выбрать имеющуюся учетную запись хранения или создать ее.</span><span class="sxs-lookup"><span data-stu-id="341af-137">You can choose an existing storage account or create a new account.</span></span> <span data-ttu-id="341af-138">При выборе элемента **Создать** отображается следующее диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="341af-138">If you choose **Create New**, the following dialog box appears:</span></span>

      ![Диалоговое окно "Создание учетной записи хранения"][CR05]

   * <span data-ttu-id="341af-140">**Виртуальная сеть** и **Подсеть**: указывают виртуальную сеть и подсеть, к которым будет подключена виртуальная машина.</span><span class="sxs-lookup"><span data-stu-id="341af-140">**Virtual Network** and **Subnet**: Specifies the virtual network and subnet that your virtual machine will connect to.</span></span> <span data-ttu-id="341af-141">Вы можете выбрать имеющуюся сеть и подсеть или создать их.</span><span class="sxs-lookup"><span data-stu-id="341af-141">You can use an existing network and subnet, or you can create a new network and subnet.</span></span> <span data-ttu-id="341af-142">При выборе элемента **Создать** отображается следующее диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="341af-142">If you select **Create new**, the following dialog box appears:</span></span>

      ![Диалоговое окно "Создание виртуальной сети"][CR06]

   * <span data-ttu-id="341af-144">**Общедоступный IP-адрес**: указывает внешний IP-адрес для виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="341af-144">**Public IP address**: Specifies an external-facing IP address for your virtual machine.</span></span> <span data-ttu-id="341af-145">Вы можете создать IP-адрес или выбрать значение **(Нет)**, если у виртуальной машины не будет общедоступного IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="341af-145">You can choose to create a new IP address or, if your virtual machine will not have a public IP address, you can select **(None)**.</span></span> 

   * <span data-ttu-id="341af-146">**Группа безопасности сети**: определяет необязательный брандмауэр для виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="341af-146">**Network security group**: Specifies an optional networking firewall for your virtual machine.</span></span> <span data-ttu-id="341af-147">Вы можете выбрать имеющийся брандмауэр или задать значение **(Нет)**, чтобы не использовать брандмауэр.</span><span class="sxs-lookup"><span data-stu-id="341af-147">You can select an existing firewall or, if your virtual machine will not use a network firewall, you can select **(None)**.</span></span> 

   * <span data-ttu-id="341af-148">**Группа доступности**: указывает необязательную группу доступности, в которую может входить виртуальная машина.</span><span class="sxs-lookup"><span data-stu-id="341af-148">**Availability set**: Specifies an optional availability set that your virtual machine can belong to.</span></span> <span data-ttu-id="341af-149">Вы можете выбрать имеющуюся группу доступности, создать ее или задать значение **(Нет)**, если виртуальная машина не будет входить в группу доступности.</span><span class="sxs-lookup"><span data-stu-id="341af-149">You can select an existing availability set, create a new availability set or, if your virtual machine will not belong to an availability set, select **(None)**.</span></span>

9. <span data-ttu-id="341af-150">Нажмите кнопку **Готово**</span><span class="sxs-lookup"><span data-stu-id="341af-150">Click **Finish**.</span></span>  
    <span data-ttu-id="341af-151">Новая виртуальная машина отобразится в окне средства Azure Explorer.</span><span class="sxs-lookup"><span data-stu-id="341af-151">Your new virtual machine appears in the Azure Explorer tool window.</span></span> 

   ![Новая виртуальная машина в представлении Azure Explorer][CR08]

## <a name="restart-a-virtual-machine-in-intellij"></a><span data-ttu-id="341af-153">Перезапуск виртуальной машины в IntelliJ</span><span class="sxs-lookup"><span data-stu-id="341af-153">Restart a virtual machine in IntelliJ</span></span>

<span data-ttu-id="341af-154">Чтобы перезапустить виртуальную машину с помощью Azure Explorer в IntelliJ, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="341af-154">To restart a virtual machine by using the Azure Explorer in IntelliJ, do the following:</span></span>

1. <span data-ttu-id="341af-155">В представлении **Azure Explorer** щелкните правой кнопкой мыши виртуальную машину и выберите **Перезапустить**.</span><span class="sxs-lookup"><span data-stu-id="341af-155">In the **Azure Explorer** view, right-click the virtual machine, and then select **Restart**.</span></span>

   ![Команда перезапуска виртуальной машины][RE01]

2. <span data-ttu-id="341af-157">В диалоговом окне подтверждения нажмите кнопку **Да**.</span><span class="sxs-lookup"><span data-stu-id="341af-157">In the confirmation window, click **Yes**.</span></span> 

   ![Диалоговое окно подтверждения перезапуска виртуальной машины][RE02]

## <a name="shut-down-a-virtual-machine-in-intellij"></a><span data-ttu-id="341af-159">Завершение работы виртуальной машины в IntelliJ</span><span class="sxs-lookup"><span data-stu-id="341af-159">Shut down a virtual machine in IntelliJ</span></span>

<span data-ttu-id="341af-160">Чтобы завершить работу виртуальной машины с помощью Azure Explorer в IntelliJ, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="341af-160">To shut down a running virtual machine by using the Azure Explorer in IntelliJ, do the following:</span></span>

1. <span data-ttu-id="341af-161">В представлении **Azure Explorer** щелкните правой кнопкой мыши виртуальную машину и выберите **Завершить работу**.</span><span class="sxs-lookup"><span data-stu-id="341af-161">In the **Azure Explorer** view, right-click the virtual machine, and then select **Shutdown**.</span></span>

   ![Команда завершения работы виртуальной машины][SH01]

2. <span data-ttu-id="341af-163">В диалоговом окне подтверждения нажмите кнопку **Да**.</span><span class="sxs-lookup"><span data-stu-id="341af-163">In the confirmation window, click **Yes**.</span></span> 

   ![Диалоговое окно подтверждения завершения работы виртуальной машины][SH02]

## <a name="delete-a-virtual-machine-in-intellij"></a><span data-ttu-id="341af-165">Удаление виртуальной машины в IntelliJ</span><span class="sxs-lookup"><span data-stu-id="341af-165">Delete a virtual machine in IntelliJ</span></span>

<span data-ttu-id="341af-166">Чтобы удалить виртуальную машину с помощью Azure Explorer в IntelliJ, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="341af-166">To delete a virtual machine by using the Azure Explorer in IntelliJ, do the following:</span></span>

1. <span data-ttu-id="341af-167">В представлении **Azure Explorer** щелкните правой кнопкой мыши виртуальную машину и выберите **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="341af-167">In the **Azure Explorer** view, right-click the virtual machine, and then select **Delete**.</span></span>

   ![Команда удаления виртуальной машины][DE01]

2. <span data-ttu-id="341af-169">В диалоговом окне подтверждения нажмите кнопку **Да**.</span><span class="sxs-lookup"><span data-stu-id="341af-169">In the confirmation window, click **Yes**.</span></span> 

   ![Диалоговое окно подтверждения удаления виртуальной машины][DE02]

## <a name="next-steps"></a><span data-ttu-id="341af-171">Дополнительная информация</span><span class="sxs-lookup"><span data-stu-id="341af-171">Next steps</span></span>

<span data-ttu-id="341af-172">Дополнительные сведения о размерах виртуальных машин Azure и ценах на них см. в следующих ресурсах:</span><span class="sxs-lookup"><span data-stu-id="341af-172">For more information about Azure virtual-machine sizes and pricing, see the following resources:</span></span>

* <span data-ttu-id="341af-173">Размеры виртуальных машин Azure</span><span class="sxs-lookup"><span data-stu-id="341af-173">Azure virtual-machine sizes</span></span>
  * <span data-ttu-id="341af-174">[Размеры виртуальных машин Windows в Azure]</span><span class="sxs-lookup"><span data-stu-id="341af-174">[Sizes for Windows virtual machines in Azure]</span></span>
  * <span data-ttu-id="341af-175">[Размеры виртуальных машин Linux в Azure]</span><span class="sxs-lookup"><span data-stu-id="341af-175">[Sizes for Linux virtual machines in Azure]</span></span>
* <span data-ttu-id="341af-176">Цены на виртуальные машины Azure</span><span class="sxs-lookup"><span data-stu-id="341af-176">Azure virtual-machine pricing</span></span>
  * <span data-ttu-id="341af-177">[Цены на виртуальные машины Windows]</span><span class="sxs-lookup"><span data-stu-id="341af-177">[Windows virtual-machine pricing]</span></span>
  * <span data-ttu-id="341af-178">[Цены на виртуальные машины Linux]</span><span class="sxs-lookup"><span data-stu-id="341af-178">[Linux virtual-machine pricing]</span></span>

[!INCLUDE [azure-toolkit-for-intellij-additional-resources](../includes/azure-toolkit-for-intellij-additional-resources.md)]

<!-- URL List -->

[Инструкции по входу для набора средств Azure для IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Sign-in instructions for the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Размеры виртуальных машин Windows в Azure]: /azure/virtual-machines/virtual-machines-windows-sizes
[Sizes for Windows virtual machines in Azure]: /azure/virtual-machines/virtual-machines-windows-sizes
[Размеры виртуальных машин Linux в Azure]: /azure/virtual-machines/virtual-machines-linux-sizes
[Sizes for Linux virtual machines in Azure]: /azure/virtual-machines/virtual-machines-linux-sizes
[Цены на виртуальные машины Windows]: /pricing/details/virtual-machines/windows/
[Windows virtual-machine pricing]: /pricing/details/virtual-machines/windows/
[Цены на виртуальные машины Linux]: /pricing/details/virtual-machines/linux/
[Linux virtual-machine pricing]: /pricing/details/virtual-machines/linux/

<!-- IMG List -->

[RE01]: media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/RE01.png
[RE02]: media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/RE02.png

[SH01]: media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/SH01.png
[SH02]: media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/SH02.png

[DE01]: media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/DE01.png
[DE02]: media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/DE02.png

[CR01]: media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR01.png
[CR02]: media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR02.png
[CR03]: media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR03.png
[CR04]: media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR04.png
[CR05]: media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR05.png
[CR06]: media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR06.png
[CR07]: media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR07.png
[CR08]: media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR08.png
