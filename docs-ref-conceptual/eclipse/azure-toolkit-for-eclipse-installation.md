---
title: "Установка набора средств Azure для Eclipse"
description: "Узнайте, как установить набор средств Azure для подключаемого модуля Eclipse, чтобы создавать и развертывать облачные приложения в Azure."
services: 
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
ms.assetid: 9e93ff6a-f42b-4d99-b55b-624136b4a730
ms.author: robmcm
ms.date: 02/01/2018
ms.devlang: Java
ms.service: multiple
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: na
ms.openlocfilehash: 81a784a09c07e0ace4d12989c745c80f55cd70cd
ms.sourcegitcommit: 151aaa6ccc64d94ed67f03e846bab953bde15b4a
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/03/2018
---
# <a name="install-the-azure-toolkit-for-eclipse"></a><span data-ttu-id="b361f-103">Установка набора средств Azure для Eclipse</span><span class="sxs-lookup"><span data-stu-id="b361f-103">Install the Azure Toolkit for Eclipse</span></span>

<span data-ttu-id="b361f-104">В набор средств Azure для Eclipse входят шаблоны и функции для простого создания, разработки, тестирования и развертывания облачных приложений в Azure с помощью среды разработки Eclipse.</span><span class="sxs-lookup"><span data-stu-id="b361f-104">The Azure Toolkit for Eclipse provides templates and functionality that allow you to easily create, develop, test, and deploy cloud applications to Azure from the Eclipse development environment.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="b361f-105">Набор средств Azure для Eclipse — это проект с открытым кодом, исходный код которого доступен по лицензии MIT на сайте проекта в GitHub по следующему URL-адресу:</span><span class="sxs-lookup"><span data-stu-id="b361f-105">The Azure Toolkit for Eclipse is an Open Source project, whose source code is available under the MIT License from the project's site on GitHub at the following URL:</span></span> 
> 
> <span data-ttu-id="b361f-106"><https://github.com/microsoft/azure-tools-for-java></span><span class="sxs-lookup"><span data-stu-id="b361f-106"><https://github.com/microsoft/azure-tools-for-java></span></span> 
> 

<span data-ttu-id="b361f-107">Ниже приведен процесс установки набора средств Azure для Eclipse.</span><span class="sxs-lookup"><span data-stu-id="b361f-107">The following steps show you how to install the Azure Toolkit for Eclipse.</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="to-install-the-azure-toolkit-for-eclipse"></a><span data-ttu-id="b361f-108">Установка набора средств Azure для Eclipse</span><span class="sxs-lookup"><span data-stu-id="b361f-108">To install the Azure Toolkit for Eclipse</span></span>

1. <span data-ttu-id="b361f-109">Запустите Eclipse.</span><span class="sxs-lookup"><span data-stu-id="b361f-109">Start Eclipse.</span></span>

1. <span data-ttu-id="b361f-110">Щелкните меню **Help** (Справка) и выберите пункт **Install New Software** (Установить новое программное обеспечение), как показано на следующем рисунке.</span><span class="sxs-lookup"><span data-stu-id="b361f-110">Click the **Help** menu, and then click **Install New Software**, as shown in the following illustration.</span></span>
   
   ![Установка набора средств Azure для Eclipse][01]

1. <span data-ttu-id="b361f-112">В диалоговом окне **Available Software** (Доступное программное обеспечение) в текстовом поле **Work with** (Работа с) введите `http://dl.microsoft.com/eclipse/` и нажмите клавишу **ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="b361f-112">In the **Available Software** dialog, within the **Work with** text box, type `http://dl.microsoft.com/eclipse/` followed by the **Enter** key.</span></span>

1. <span data-ttu-id="b361f-113">В области **Name** (Имя) установите флажок **Azure Toolkit for Eclipse** (Набор средств Azure для Eclipse) и снимите флажок **Contact all update sites during install to find required software** (Проверить все сайты обновления во время установки для поиска требуемого ПО).</span><span class="sxs-lookup"><span data-stu-id="b361f-113">In the **Name** pane, check **Azure Toolkit for Eclipse**, and uncheck **Contact all update sites during install to find required software**.</span></span> <span data-ttu-id="b361f-114">Экран должен выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="b361f-114">Your screen should appear similar to the following:</span></span>
   
   ![Установка набора средств Azure для Eclipse][02]

1. <span data-ttu-id="b361f-116">Если развернуть **набор средств Azure для Eclipse**, вы увидите список компонентов, которые будут установлены, например:</span><span class="sxs-lookup"><span data-stu-id="b361f-116">If you expand **Azure Toolkit for Eclipse**, you will see a list of components that will be installed; for example:</span></span>

   | <span data-ttu-id="b361f-117">Функция</span><span class="sxs-lookup"><span data-stu-id="b361f-117">Feature</span></span> | <span data-ttu-id="b361f-118">ОПИСАНИЕ</span><span class="sxs-lookup"><span data-stu-id="b361f-118">Description</span></span> | 
   |---|---| 
   | <span data-ttu-id="b361f-119">**Подключаемый модуль Application Insights для Java**</span><span class="sxs-lookup"><span data-stu-id="b361f-119">**Application Insights Plugin for Java**</span></span> | <span data-ttu-id="b361f-120">Этот компонент позволяет использовать службы регистрации и анализа телеметрии Azure для приложений и экземпляров серверов.</span><span class="sxs-lookup"><span data-stu-id="b361f-120">Allows you to use Azure's telemetry logging and analysis services for your applications and server instances.</span></span> | 
   | <span data-ttu-id="b361f-121">**Общий подключаемый модуль Azure**</span><span class="sxs-lookup"><span data-stu-id="b361f-121">**Azure Common Plugin**</span></span> | <span data-ttu-id="b361f-122">Этот компонент предоставляет функциональные возможности, необходимые другим компонентам набора средств.</span><span class="sxs-lookup"><span data-stu-id="b361f-122">provides the common functionality needed by other toolkit components.</span></span> | 
   | <span data-ttu-id="b361f-123">**Набор средств контейнеров Azure для Eclipse**</span><span class="sxs-lookup"><span data-stu-id="b361f-123">**Azure Container Tools for Eclipse**</span></span> | <span data-ttu-id="b361f-124">Этот компонент позволяет создавать и развертывать WAR-файлы как контейнеры Docker в виртуальной машине Docker.</span><span class="sxs-lookup"><span data-stu-id="b361f-124">Enables you to build and deploy a .WAR as a Docker container to a docker machine.</span></span> | 
   | <span data-ttu-id="b361f-125">**Контейнеры Azure для Eclipse**</span><span class="sxs-lookup"><span data-stu-id="b361f-125">**Azure Containers for Eclipse**</span></span> | <span data-ttu-id="b361f-126">Этот компонент позволяет развертывать WAR-файлы или артефакт JAR как контейнер Docker в виртуальной машине Azure.</span><span class="sxs-lookup"><span data-stu-id="b361f-126">Enables you to deploy a .WAR or .JAR artifact as a Docker container to an Azure virtual machine.</span></span> | 
   | <span data-ttu-id="b361f-127">**Azure Explorer для Eclipse**</span><span class="sxs-lookup"><span data-stu-id="b361f-127">**Azure Explorer for Eclipse**</span></span> | <span data-ttu-id="b361f-128">Этот компонент предоставляет интерфейс в виде проводника для управления ресурсами Azure.</span><span class="sxs-lookup"><span data-stu-id="b361f-128">Provides an explorer-style interface for managing your Azure resources.</span></span> | 
   | <span data-ttu-id="b361f-129">**Microsoft JDBC Driver 6.1 для SQL Server**</span><span class="sxs-lookup"><span data-stu-id="b361f-129">**Microsoft JDBC Driver 6.1 for SQL Server**</span></span> | <span data-ttu-id="b361f-130">Этот компонент предоставляет API JDBC для SQL Server и Базу данных SQL Microsoft Azure для платформы Java Enterprise Edition 8.</span><span class="sxs-lookup"><span data-stu-id="b361f-130">Provides JDBC API for SQL Server and Microsoft Azure SQL Database for Java Platform Enterprise Edition 8.</span></span> | 
   | <span data-ttu-id="b361f-131">**Пакет для библиотек Microsoft Azure для Java**</span><span class="sxs-lookup"><span data-stu-id="b361f-131">**Package for Microsoft Azure Libraries for Java**</span></span> | <span data-ttu-id="b361f-132">Этот компонент предоставляет API-интерфейсы для доступа к таким службам Microsoft Azure, как хранилище, служебная шина, среда выполнения службы и т. д.</span><span class="sxs-lookup"><span data-stu-id="b361f-132">Provides APIs for accessing Microsoft Azure services, such as storage, service bus, service runtime, etc.</span></span> | 

1. <span data-ttu-id="b361f-133">Нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="b361f-133">Click **Next**.</span></span> <span data-ttu-id="b361f-134">(Если при установке набора средств возникают необычные задержки, убедитесь, что снят флажок **Contact all update sites during install to find required software** [Проверить все сайты обновления во время установки для поиска требуемого ПО].)</span><span class="sxs-lookup"><span data-stu-id="b361f-134">(If you experience unusual delays when installing the toolkit, ensure that **Contact all update sites during install to find required software** is unchecked.)</span></span>

1. <span data-ttu-id="b361f-135">В диалоговом окне **Install Details** (Сведения об установке) нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="b361f-135">In the **Install Details** dialog, click **Next**.</span></span>
   
   ![Просмотр сведений об установке][03]

1. <span data-ttu-id="b361f-137">В диалоговом окне **Review Licenses** (Просмотр лицензий) ознакомьтесь с условиями лицензионного соглашения.</span><span class="sxs-lookup"><span data-stu-id="b361f-137">In the **Review Licenses** dialog, review the terms of the license agreements.</span></span> <span data-ttu-id="b361f-138">Если вы принимаете условия лицензионных соглашений, установите переключатель **I accept the terms of the license agreements** (Я принимаю условия лицензионных соглашений), а затем нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="b361f-138">If you accept the terms of the license agreements, click **I accept the terms of the license agreements** and then click **Finish**.</span></span> <span data-ttu-id="b361f-139">(В следующих действиях предполагается, что вы принимаете условия лицензионных соглашений.</span><span class="sxs-lookup"><span data-stu-id="b361f-139">(The remaining steps assume you do accept the terms of the license agreements.</span></span> <span data-ttu-id="b361f-140">Если вы не принимаете эти условия, завершите процесс установки.)</span><span class="sxs-lookup"><span data-stu-id="b361f-140">If you do not accept the terms of the license agreements, exit the installation process.)</span></span>
   
   ![Review Licenses][04]
   
   <span data-ttu-id="b361f-142">Eclipse скачает и установит необходимые пакеты.</span><span class="sxs-lookup"><span data-stu-id="b361f-142">Eclipse will download and install the requisite packages.</span></span>
   
   ![Ход установки][05]

1. <span data-ttu-id="b361f-144">Если отображается запрос на перезапуск Eclipse для завершения установки, нажмите кнопку **Yes**(Да).</span><span class="sxs-lookup"><span data-stu-id="b361f-144">If prompted to restart Eclipse to complete installation, click **Yes**.</span></span>
   
   ![Запрос перезапуска][06]

## <a name="next-steps"></a><span data-ttu-id="b361f-146">Дополнительная информация</span><span class="sxs-lookup"><span data-stu-id="b361f-146">Next steps</span></span>

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
