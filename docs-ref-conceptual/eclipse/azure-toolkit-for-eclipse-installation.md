---
title: Установка набора средств Azure для Eclipse
description: Узнайте, как установить набор средств Azure для подключаемого модуля Eclipse, чтобы создавать и развертывать облачные приложения в Azure.
services: ''
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: ''
ms.assetid: 9e93ff6a-f42b-4d99-b55b-624136b4a730
ms.author: robmcm
ms.date: 02/01/2018
ms.devlang: Java
ms.service: multiple
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: na
ms.openlocfilehash: 8e6630f7e019d950249e7e84024ac800a0f2f136
ms.sourcegitcommit: 394521c47ac9895d00d9f97535cc9d1e27d08fe9
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/28/2019
ms.locfileid: "66270847"
---
# <a name="installing-the-azure-toolkit-for-eclipse"></a><span data-ttu-id="31d16-103">Установка набора средств Azure для Eclipse</span><span class="sxs-lookup"><span data-stu-id="31d16-103">Installing the Azure Toolkit for Eclipse</span></span>

<span data-ttu-id="31d16-104">Существует два способа для установки Azure Toolkit for Eclipse:</span><span class="sxs-lookup"><span data-stu-id="31d16-104">There are two ways to install Azure Toolkit for Eclipse:</span></span>

  - [<span data-ttu-id="31d16-105">Eclipse Marketplace.</span><span class="sxs-lookup"><span data-stu-id="31d16-105">Eclipse marketplace</span></span>](#eclipse-marketplace)
  - [<span data-ttu-id="31d16-106">Установка нового программного обеспечения.</span><span class="sxs-lookup"><span data-stu-id="31d16-106">Install new software</span></span>](#install-new-software)

> [!NOTE] 
> 
> <span data-ttu-id="31d16-107">Набор средств Azure для Eclipse — это проект с открытым кодом, исходный код которого доступен по лицензии MIT на сайте проекта в GitHub по следующему URL-адресу:</span><span class="sxs-lookup"><span data-stu-id="31d16-107">The Azure Toolkit for Eclipse is an Open Source project, whose source code is available under the MIT License from the project's site on GitHub at the following URL:</span></span> 
> 
> <https://github.com/microsoft/azure-tools-for-java> 
> 

[!INCLUDE [azure-toolkit-for-eclipse-basic-prerequisites](../includes/azure-toolkit-for-eclipse-basic-prerequisites.md)]

## <a name="eclipse-marketplace"></a><span data-ttu-id="31d16-108">Eclipse Marketplace</span><span class="sxs-lookup"><span data-stu-id="31d16-108">Eclipse marketplace</span></span>

1. <span data-ttu-id="31d16-109">Перетащите кнопку ниже в запущенную рабочую область Eclipse.</span><span class="sxs-lookup"><span data-stu-id="31d16-109">Drag the following button to your running Eclipse workspace.</span></span>

    <span data-ttu-id="31d16-110">[![Перетащите в запущенную рабочую область Eclipse*. * Требуется клиент Eclipse Marketplace](https://marketplace.eclipse.org/sites/all/themes/solstice/public/images/marketplace/btn-install.png)](http://marketplace.eclipse.org/marketplace-client-intro?mpc_install=1919278 "Перетащите в запущенную рабочую область Eclipse*. * Требуется клиент Eclipse Marketplace")</span><span class="sxs-lookup"><span data-stu-id="31d16-110">[![Drag to your running Eclipse* workspace. *Requires Eclipse Marketplace Client](https://marketplace.eclipse.org/sites/all/themes/solstice/public/images/marketplace/btn-install.png)](http://marketplace.eclipse.org/marketplace-client-intro?mpc_install=1919278 "Drag to your running Eclipse* workspace. *Requires Eclipse Marketplace Client")</span></span>

2. <span data-ttu-id="31d16-111">Кроме того, вы можете найти и установить **подключаемый модуль Azure Toolkit for Eclipse** в **разделе справки или в Eclipse Marketplace**.</span><span class="sxs-lookup"><span data-stu-id="31d16-111">Otherwise, it is also possible to search and install the **Azure Toolkit for Eclipse plugin** at **Help/Eclipse Marketplace**.</span></span>

    ![Marketplace](./media/azure-toolkit-for-eclipse-installation/marketplace.png)

## <a name="install-new-software"></a><span data-ttu-id="31d16-113">Установка нового программного обеспечения</span><span class="sxs-lookup"><span data-stu-id="31d16-113">Install new software</span></span>

1. <span data-ttu-id="31d16-114">Запустите Eclipse.</span><span class="sxs-lookup"><span data-stu-id="31d16-114">Start Eclipse.</span></span>

1. <span data-ttu-id="31d16-115">Щелкните меню **Help** (Справка) и выберите пункт **Install New Software** (Установить новое программное обеспечение), как показано на следующем рисунке.</span><span class="sxs-lookup"><span data-stu-id="31d16-115">Click the **Help** menu, and then click **Install New Software**, as shown in the following illustration.</span></span>

   ![Установка набора средств Azure для Eclipse][01]

1. <span data-ttu-id="31d16-117">В диалоговом окне **Available Software** (Доступное программное обеспечение) в текстовом поле **Work with** (Работа с) введите `http://dl.microsoft.com/eclipse/` и нажмите клавишу **ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="31d16-117">In the **Available Software** dialog, within the **Work with** text box, type `http://dl.microsoft.com/eclipse/` followed by the **Enter** key.</span></span>

1. <span data-ttu-id="31d16-118">В области **Name** (Имя) установите флажок **Azure Toolkit for Java** (Набор средств Azure для Java) и снимите флажок **Contact all update sites during install to find required software** (Проверить все сайты обновления во время установки для поиска требуемого ПО).</span><span class="sxs-lookup"><span data-stu-id="31d16-118">In the **Name** pane, check **Azure Toolkit for Java**, and uncheck **Contact all update sites during install to find required software**.</span></span> <span data-ttu-id="31d16-119">Экран должен выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="31d16-119">Your screen should appear similar to the following:</span></span>

   ![Установка набора средств Azure для Eclipse][02]

1. <span data-ttu-id="31d16-121">Если развернуть **набор средств Azure для Eclipse**, вы увидите список компонентов, которые будут установлены, например:</span><span class="sxs-lookup"><span data-stu-id="31d16-121">If you expand **Azure Toolkit for Eclipse**, you will see a list of components that will be installed; for example:</span></span>

   | <span data-ttu-id="31d16-122">Функция</span><span class="sxs-lookup"><span data-stu-id="31d16-122">Feature</span></span> | <span data-ttu-id="31d16-123">ОПИСАНИЕ</span><span class="sxs-lookup"><span data-stu-id="31d16-123">Description</span></span> | 
   |---|---| 
   | <span data-ttu-id="31d16-124">**Подключаемый модуль Application Insights для Java**</span><span class="sxs-lookup"><span data-stu-id="31d16-124">**Application Insights Plugin for Java**</span></span> | <span data-ttu-id="31d16-125">Этот компонент позволяет использовать службы регистрации и анализа телеметрии Azure для приложений и экземпляров серверов.</span><span class="sxs-lookup"><span data-stu-id="31d16-125">Allows you to use Azure's telemetry logging and analysis services for your applications and server instances.</span></span> | 
   | <span data-ttu-id="31d16-126">**Общий подключаемый модуль Azure**</span><span class="sxs-lookup"><span data-stu-id="31d16-126">**Azure Common Plugin**</span></span> | <span data-ttu-id="31d16-127">Этот компонент предоставляет функциональные возможности, необходимые другим компонентам набора средств.</span><span class="sxs-lookup"><span data-stu-id="31d16-127">provides the common functionality needed by other toolkit components.</span></span> | 
   | <span data-ttu-id="31d16-128">**Набор средств контейнеров Azure для Eclipse**</span><span class="sxs-lookup"><span data-stu-id="31d16-128">**Azure Container Tools for Eclipse**</span></span> | <span data-ttu-id="31d16-129">Этот компонент позволяет создавать и развертывать WAR-файлы как контейнеры Docker в виртуальной машине Docker.</span><span class="sxs-lookup"><span data-stu-id="31d16-129">Enables you to build and deploy a .WAR as a Docker container to a docker machine.</span></span> | 
   | <span data-ttu-id="31d16-130">**Контейнеры Azure для Eclipse**</span><span class="sxs-lookup"><span data-stu-id="31d16-130">**Azure Containers for Eclipse**</span></span> | <span data-ttu-id="31d16-131">Этот компонент позволяет развертывать WAR-файлы или артефакт JAR как контейнер Docker в виртуальной машине Azure.</span><span class="sxs-lookup"><span data-stu-id="31d16-131">Enables you to deploy a .WAR or .JAR artifact as a Docker container to an Azure virtual machine.</span></span> | 
   | <span data-ttu-id="31d16-132">**Azure Explorer для Eclipse**</span><span class="sxs-lookup"><span data-stu-id="31d16-132">**Azure Explorer for Eclipse**</span></span> | <span data-ttu-id="31d16-133">Этот компонент предоставляет интерфейс в виде проводника для управления ресурсами Azure.</span><span class="sxs-lookup"><span data-stu-id="31d16-133">Provides an explorer-style interface for managing your Azure resources.</span></span> | 
   | <span data-ttu-id="31d16-134">**Microsoft JDBC Driver 6.1 для SQL Server**</span><span class="sxs-lookup"><span data-stu-id="31d16-134">**Microsoft JDBC Driver 6.1 for SQL Server**</span></span> | <span data-ttu-id="31d16-135">Этот компонент предоставляет API JDBC для SQL Server и Базу данных SQL Microsoft Azure для платформы Java Enterprise Edition 8.</span><span class="sxs-lookup"><span data-stu-id="31d16-135">Provides JDBC API for SQL Server and Microsoft Azure SQL Database for Java Platform Enterprise Edition 8.</span></span> | 
   | <span data-ttu-id="31d16-136">**Пакет для библиотек Microsoft Azure для Java**</span><span class="sxs-lookup"><span data-stu-id="31d16-136">**Package for Microsoft Azure Libraries for Java**</span></span> | <span data-ttu-id="31d16-137">Этот компонент предоставляет API-интерфейсы для доступа к таким службам Microsoft Azure, как хранилище, служебная шина, среда выполнения службы и т. д.</span><span class="sxs-lookup"><span data-stu-id="31d16-137">Provides APIs for accessing Microsoft Azure services, such as storage, service bus, service runtime, etc.</span></span> | 

1. <span data-ttu-id="31d16-138">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="31d16-138">Click **Next**.</span></span> <span data-ttu-id="31d16-139">(Если при установке набора средств возникают необычные задержки, убедитесь, что снят флажок **Contact all update sites during install to find required software** [Проверить все сайты обновления во время установки для поиска требуемого ПО].)</span><span class="sxs-lookup"><span data-stu-id="31d16-139">(If you experience unusual delays when installing the toolkit, ensure that **Contact all update sites during install to find required software** is unchecked.)</span></span>

1. <span data-ttu-id="31d16-140">В диалоговом окне **Install Details** (Сведения об установке) нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="31d16-140">In the **Install Details** dialog, click **Next**.</span></span>

   ![Просмотр сведений об установке][03]

1. <span data-ttu-id="31d16-142">В диалоговом окне **Review Licenses** (Просмотр лицензий) ознакомьтесь с условиями лицензионного соглашения.</span><span class="sxs-lookup"><span data-stu-id="31d16-142">In the **Review Licenses** dialog, review the terms of the license agreements.</span></span> <span data-ttu-id="31d16-143">Если вы принимаете условия лицензионных соглашений, установите переключатель **I accept the terms of the license agreements** (Я принимаю условия лицензионных соглашений), а затем нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="31d16-143">If you accept the terms of the license agreements, click **I accept the terms of the license agreements** and then click **Finish**.</span></span> <span data-ttu-id="31d16-144">(В следующих действиях предполагается, что вы принимаете условия лицензионных соглашений.</span><span class="sxs-lookup"><span data-stu-id="31d16-144">(The remaining steps assume you do accept the terms of the license agreements.</span></span> <span data-ttu-id="31d16-145">Если вы не принимаете эти условия, завершите процесс установки.)</span><span class="sxs-lookup"><span data-stu-id="31d16-145">If you do not accept the terms of the license agreements, exit the installation process.)</span></span>

   ![Review Licenses][04]

   <span data-ttu-id="31d16-147">Eclipse скачает и установит необходимые пакеты.</span><span class="sxs-lookup"><span data-stu-id="31d16-147">Eclipse will download and install the requisite packages.</span></span>

   ![Ход установки][05]

1. <span data-ttu-id="31d16-149">Если отображается запрос на перезапуск Eclipse для завершения установки, нажмите кнопку **Yes**(Да).</span><span class="sxs-lookup"><span data-stu-id="31d16-149">If prompted to restart Eclipse to complete installation, click **Yes**.</span></span>

   ![Запрос перезапуска][06]

## <a name="next-steps"></a><span data-ttu-id="31d16-151">Дополнительная информация</span><span class="sxs-lookup"><span data-stu-id="31d16-151">Next steps</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-additional-resources](../includes/azure-toolkit-for-eclipse-additional-resources.md)]

<!-- URL List -->

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690946.aspx -->

<!-- IMG List -->
[01]: media/azure-toolkit-for-eclipse-installation/eclipse-installation-01.png
[02]: media/azure-toolkit-for-eclipse-installation/eclipse-installation-02.png
[03]: media/azure-toolkit-for-eclipse-installation/eclipse-installation-03.png
[04]: media/azure-toolkit-for-eclipse-installation/eclipse-installation-04.png
[05]: media/azure-toolkit-for-eclipse-installation/eclipse-installation-05.png
[06]: media/azure-toolkit-for-eclipse-installation/eclipse-installation-06.png
