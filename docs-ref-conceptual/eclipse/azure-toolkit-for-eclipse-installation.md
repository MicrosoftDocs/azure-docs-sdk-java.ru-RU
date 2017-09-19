---
title: "Установка набора средств Azure для Eclipse"
description: "Узнайте, как установить набор средств Azure для Eclipse."
services: 
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
ms.assetid: 9e93ff6a-f42b-4d99-b55b-624136b4a730
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 09/11/2017
ms.author: robmcm
ms.openlocfilehash: 59a8bfb6ab4db8ea8c6c9025ca3ced8a13192628
ms.sourcegitcommit: 256044d7cbce16dcb8dc4e195d0f63c10cb44d4e
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/13/2017
---
# <a name="installing-the-azure-toolkit-for-eclipse"></a><span data-ttu-id="7d8b6-103">Установка набора средств Azure для Eclipse</span><span class="sxs-lookup"><span data-stu-id="7d8b6-103">Installing the Azure Toolkit for Eclipse</span></span>

<span data-ttu-id="7d8b6-104">В набор средств Azure для Eclipse входят шаблоны и функциональные возможности для простого создания, разработки, тестирования и развертывания приложений Azure с помощью среды разработки Eclipse.</span><span class="sxs-lookup"><span data-stu-id="7d8b6-104">The Azure Toolkit for Eclipse provides templates and functionality that allow you to easily create, develop, test, and deploy Azure applications using the Eclipse development environment.</span></span> <span data-ttu-id="7d8b6-105">Набор средств Azure для Eclipse является проектом с открытым кодом.</span><span class="sxs-lookup"><span data-stu-id="7d8b6-105">The Azure Toolkit for Eclipse is an Open Source project.</span></span> <span data-ttu-id="7d8b6-106">Исходный код доступен по лицензии MIT по адресу: <https://github.com/microsoft/azure-tools-for-java>.</span><span class="sxs-lookup"><span data-stu-id="7d8b6-106">The source code is available under the MIT License from <https://github.com/microsoft/azure-tools-for-java>.</span></span>

<span data-ttu-id="7d8b6-107">Ниже приведен процесс установки набора средств Azure для Eclipse.</span><span class="sxs-lookup"><span data-stu-id="7d8b6-107">The following steps show you how to install the Azure Toolkit for Eclipse.</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="to-install-the-azure-toolkit-for-eclipse"></a><span data-ttu-id="7d8b6-108">Установка набора средств Azure для Eclipse</span><span class="sxs-lookup"><span data-stu-id="7d8b6-108">To install the Azure Toolkit for Eclipse</span></span>

1. <span data-ttu-id="7d8b6-109">Запустите Eclipse.</span><span class="sxs-lookup"><span data-stu-id="7d8b6-109">Start Eclipse.</span></span>

1. <span data-ttu-id="7d8b6-110">Щелкните меню **Help** (Справка) и выберите пункт **Install New Software** (Установить новое программное обеспечение), как показано на следующем рисунке.</span><span class="sxs-lookup"><span data-stu-id="7d8b6-110">Click the **Help** menu, and then click **Install New Software**, as shown in the following illustration.</span></span>
   
   ![Установка набора средств Azure для Eclipse][01]

1. <span data-ttu-id="7d8b6-112">В диалоговом окне **Available Software** (Доступное программное обеспечение) в текстовом поле **Work with** (Работа с) введите `http://dl.microsoft.com/eclipse/` и нажмите клавишу **ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="7d8b6-112">In the **Available Software** dialog, within the **Work with** text box, type `http://dl.microsoft.com/eclipse/` followed by the **Enter** key.</span></span>

1. <span data-ttu-id="7d8b6-113">В области **Name** (Имя) установите флажок **Azure Toolkit for Eclipse** (Набор средств Azure для Eclipse) и снимите флажок **Contact all update sites during install to find required software** (Проверить все сайты обновления во время установки для поиска требуемого ПО).</span><span class="sxs-lookup"><span data-stu-id="7d8b6-113">In the **Name** pane, check **Azure Toolkit for Eclipse**, and uncheck **Contact all update sites during install to find required software**.</span></span> <span data-ttu-id="7d8b6-114">Экран должен выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="7d8b6-114">Your screen should appear similar to the following:</span></span>
   
   ![Установка набора средств Azure для Eclipse][02]

1. <span data-ttu-id="7d8b6-116">Если вы развернете узел **Набор средств Azure для Eclipse**, вы увидите следующие элементы:</span><span class="sxs-lookup"><span data-stu-id="7d8b6-116">If you expand the **Azure Toolkit for Eclipse**, you will see a list of items like following example:</span></span>
   
   * <span data-ttu-id="7d8b6-117">**Application Insights Plugin for Java**(Подключаемый модуль Application Insights для Java) — этот компонент позволяет использовать службы регистрации и анализа телеметрии Azure для приложений и экземпляров серверов.</span><span class="sxs-lookup"><span data-stu-id="7d8b6-117">**Application Insights Plugin for Java**: This component allows you to use Azure's telemetry logging and analysis services for your applications and server instances.</span></span>
   * <span data-ttu-id="7d8b6-118">**Фильтр служб контроля доcтупа Azure**— этот компонент обеспечивает поддержку проверки подлинности пользователей приложения с помощью Azure ACS, используя сценарии единого входа и перемещая логику удостоверений из приложения.</span><span class="sxs-lookup"><span data-stu-id="7d8b6-118">**Azure Access Control Services Filter**: This component provides support for authenticating application users with Azure ACS, enabling single sign-on scenarios and externalizing identity logic from the application.</span></span>
   * <span data-ttu-id="7d8b6-119">**Общий подключаемый модуль Azure**— этот компонент предоставляет функциональные возможности, необходимые другим компонентам набора средств.</span><span class="sxs-lookup"><span data-stu-id="7d8b6-119">**Azure Common Plugin**: This component provides the common functionality needed by other toolkit components.</span></span>
   * <span data-ttu-id="7d8b6-120">**Обозреватель Azure для Eclipse**— этот компонент предоставляет функциональные возможности, необходимые другим компонентам набора средств.</span><span class="sxs-lookup"><span data-stu-id="7d8b6-120">**Azure Explorer for Eclipse**: This component provides the common functionality needed by other toolkit components.</span></span>
   * <span data-ttu-id="7d8b6-121">**Подключаемый модуль Azure для Eclipse с Java**— этот компонент обеспечивает поддержку проектов, помогающих собирать, тестировать и развертывать приложения Java для облака Microsoft Azure в Eclipse и с помощью командной строки.</span><span class="sxs-lookup"><span data-stu-id="7d8b6-121">**Azure Plugin for Eclipse with Java**: This component provides support for developing projects that help build, test and deploy Java applications for the Microsoft Azure cloud in Eclipse and via command line.</span></span>
   * <span data-ttu-id="7d8b6-122">**Подключаемый модуль веб- приложений Azure с Java**— этот компонент обеспечивает поддержку развертывания веб-приложений Java в контейнерах веб-приложений Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="7d8b6-122">**Azure Web Apps Plugin with Java**: This component provides support for deploying Java web applications to Microsoft Azure Web App containers.</span></span>
   * <span data-ttu-id="7d8b6-123">**Драйвер Microsoft JDBC 4.2 для SQL Server**— этот компонент предоставляет API JDBC для SQL Server и Базу данных SQL Microsoft Azure для платформы Java Enterprise Edition 8.</span><span class="sxs-lookup"><span data-stu-id="7d8b6-123">**Microsoft JDBC Driver 4.2 for SQL Server**: This component provides JDBC API for SQL Server and Microsoft Azure SQL Database for Java Platform Enterprise Edition 8.</span></span>
   * <span data-ttu-id="7d8b6-124">**Package for Apache Qpid Client Libraries for JMS**(Пакет для клиентских библиотек Apache Qpid для JMS) — этот компонент предоставляет клиентские компоненты JMS из проекта Apache Qpid, чтобы ваше приложение могло использовать обмен сообщениями на основе протокола AMQP в Azure.</span><span class="sxs-lookup"><span data-stu-id="7d8b6-124">**Package for Apache Qpid Client Libraries for JMS**: This component provides the JMS client component from the Apache Qpid project to enable your application to use AMQP messaging in Microsoft Azure.</span></span>
   * <span data-ttu-id="7d8b6-125">**Пакет для библиотек Microsoft Azure для Java** — этот компонент предоставляет API для доступа к службам Microsoft Azure, таким как хранилище, служебная шина, среда выполнения службы и т. д.</span><span class="sxs-lookup"><span data-stu-id="7d8b6-125">**Package for Microsoft Azure Libraries for Java**: This component provides APIs for accessing Microsoft Azure services, such as storage, service bus, service runtime, etc.</span></span>

1. <span data-ttu-id="7d8b6-126">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="7d8b6-126">Click **Next**.</span></span> <span data-ttu-id="7d8b6-127">(Если при установке набора средств возникают необычные задержки, убедитесь, что снят флажок **Contact all update sites during install to find required software** [Проверить все сайты обновления во время установки для поиска требуемого ПО].)</span><span class="sxs-lookup"><span data-stu-id="7d8b6-127">(If you experience unusual delays when installing the toolkit, ensure that **Contact all update sites during install to find required software** is unchecked.)</span></span>

1. <span data-ttu-id="7d8b6-128">В диалоговом окне **Install Details** (Сведения об установке) нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="7d8b6-128">In the **Install Details** dialog, click **Next**.</span></span>
   
   ![Просмотр сведений об установке][03]

1. <span data-ttu-id="7d8b6-130">В диалоговом окне **Review Licenses** (Просмотр лицензий) ознакомьтесь с условиями лицензионного соглашения.</span><span class="sxs-lookup"><span data-stu-id="7d8b6-130">In the **Review Licenses** dialog, review the terms of the license agreements.</span></span> <span data-ttu-id="7d8b6-131">Если вы принимаете условия лицензионных соглашений, установите переключатель **I accept the terms of the license agreements** (Я принимаю условия лицензионных соглашений), а затем нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="7d8b6-131">If you accept the terms of the license agreements, click **I accept the terms of the license agreements** and then click **Finish**.</span></span> <span data-ttu-id="7d8b6-132">(В следующих действиях предполагается, что вы принимаете условия лицензионных соглашений.</span><span class="sxs-lookup"><span data-stu-id="7d8b6-132">(The remaining steps assume you do accept the terms of the license agreements.</span></span> <span data-ttu-id="7d8b6-133">Если вы не принимаете эти условия, завершите процесс установки.)</span><span class="sxs-lookup"><span data-stu-id="7d8b6-133">If you do not accept the terms of the license agreements, exit the installation process.)</span></span>
   
   ![Review Licenses][04]
   
   <span data-ttu-id="7d8b6-135">Eclipse скачает и установит необходимые пакеты.</span><span class="sxs-lookup"><span data-stu-id="7d8b6-135">Eclipse will download and install the requisite packages.</span></span>
   
   ![Ход установки][05]

1. <span data-ttu-id="7d8b6-137">Если отображается запрос на перезапуск Eclipse для завершения установки, нажмите кнопку **Yes**(Да).</span><span class="sxs-lookup"><span data-stu-id="7d8b6-137">If prompted to restart Eclipse to complete installation, click **Yes**.</span></span>
   
   ![Запрос перезапуска][06]

## <a name="next-steps"></a><span data-ttu-id="7d8b6-139">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7d8b6-139">Next steps</span></span>

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

<!-- URL List -->

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690946.aspx -->

<!-- IMG List -->

[01]: media/azure-toolkit-for-eclipse-installation/eclipse-installation-01.png
[02]: media/azure-toolkit-for-eclipse-installation/eclipse-installation-02.png
[03]: media/azure-toolkit-for-eclipse-installation/eclipse-installation-03.png
[04]: media/azure-toolkit-for-eclipse-installation/eclipse-installation-04.png
[05]: media/azure-toolkit-for-eclipse-installation/eclipse-installation-05.png
[06]: media/azure-toolkit-for-eclipse-installation/eclipse-installation-06.png
