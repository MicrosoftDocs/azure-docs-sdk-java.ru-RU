---
title: Установка набора средств Azure для IntelliJ
description: Узнайте, как установить набор средств Azure для подключаемого модуля IntelliJ, чтобы создавать и развертывать облачные приложения в Azure.
services: ''
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: ''
ms.assetid: c6817c7b-f28c-4c06-8216-41c7a8117de3
ms.author: robmcm
ms.date: 02/01/2018
ms.devlang: Java
ms.service: multiple
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: na
ms.openlocfilehash: 86cef07873ae7a2ba75aab1044fe4d241cd5b13e
ms.sourcegitcommit: 394521c47ac9895d00d9f97535cc9d1e27d08fe9
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/28/2019
ms.locfileid: "66270873"
---
# <a name="installing-the-azure-toolkit-for-intellij"></a><span data-ttu-id="b5a68-103">Установка набора средств Azure для IntelliJ</span><span class="sxs-lookup"><span data-stu-id="b5a68-103">Installing the Azure Toolkit for IntelliJ</span></span>

<span data-ttu-id="b5a68-104">В набор средств Azure для IntelliJ входят шаблоны и функции для простого создания, разработки, тестирования и развертывания облачных приложений в Azure с помощью среды разработки IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="b5a68-104">The Azure Toolkit for IntelliJ provides templates and functionality that allow you to easily create, develop, test, and deploy cloud application to Azure using the IntelliJ IDEA development environment.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="b5a68-105">Набор средств Azure для IntelliJ — это проект с открытым кодом, исходный код которого доступен по лицензии MIT на сайте проекта в GitHub по следующему URL-адресу:</span><span class="sxs-lookup"><span data-stu-id="b5a68-105">The Azure Toolkit for IntelliJ is an Open Source project, whose source code is available under the MIT License from the project's site on GitHub at the following URL:</span></span> 
> 
> <https://github.com/microsoft/azure-tools-for-java> 
> 

<span data-ttu-id="b5a68-106">Установить набор средств Azure для IntelliJ можно с помощью диалогового окна **Параметры** или меню **Настройка** на начальном экране.</span><span class="sxs-lookup"><span data-stu-id="b5a68-106">There are two methods of installing the Azure Toolkit for IntelliJ: by using the **Settings** dialog box, and by using the **Configure** menu on the start screen.</span></span> <span data-ttu-id="b5a68-107">Оба способа установки будут описаны ниже.</span><span class="sxs-lookup"><span data-stu-id="b5a68-107">Both installation methods will be demonstrated in the following steps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b5a68-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="b5a68-108">Prerequisites</span></span>

<span data-ttu-id="b5a68-109">Azure Toolkit for IntelliJ требует наличия следующих программных компонентов:</span><span class="sxs-lookup"><span data-stu-id="b5a68-109">The Azure Toolkit for IntelliJ requires to the following software components:</span></span>

* <span data-ttu-id="b5a68-110">Установленный Пакет SDK для Java (JDK) 8+, например: [OpenJDK](https://openjdk.java.net/) или [Oracle JDK](https://www.oracle.com/technetwork/java/javase/downloads/index.html).</span><span class="sxs-lookup"><span data-stu-id="b5a68-110">An Java Development Kit (JDK) 8+ installed, for example: [OpenJDK](https://openjdk.java.net/) or [Oracle JDK](https://www.oracle.com/technetwork/java/javase/downloads/index.html)</span></span>
* <span data-ttu-id="b5a68-111">Установленный [IntelliJ IDEA](https://www.jetbrains.com/idea/download/) Ultimate Edition или Community Edition.</span><span class="sxs-lookup"><span data-stu-id="b5a68-111">An [IntelliJ IDEA](https://www.jetbrains.com/idea/download/) Ultimate Edition or Community Edition installed</span></span>

> [!NOTE]
> 
> <span data-ttu-id="b5a68-112">На сайте репозитория подключаемых модулей JetBrains на странице [Azure Toolkit for IntelliJ](https://plugins.jetbrains.com/plugin/8053) приведен список сборок, совместимых с набором средств.</span><span class="sxs-lookup"><span data-stu-id="b5a68-112">The [Azure Toolkit for IntelliJ](https://plugins.jetbrains.com/plugin/8053) page at the JetBrains Plugin Repository lists the builds that are compatible with the toolkit.</span></span>
> 

<!--
> [!IMPORTANT]
> 
> If you are using the Azure Toolkit for IntelliJ on Windows, the toolkit requires installing the Azure SDK 2.9.6 or later in order to use the Azure emulator. You have two options for installing the Azure SDK:
> 
> * You can download and install the Azure SDK by using the [Web Platform Installer (WebPI)](http://go.microsoft.com/fwlink/?LinkID=252838).
> * If you do not have the Azure SDK installed when you create your first Azure deployment project, you will be prompted to automatically download install the requisite version of the Azure SDK.
> 
> Note that the Azure SDK is only required on Windows.
> 
-->


## <a name="to-install-the-azure-toolkit-for-intellij-from-the-settings-dialog-box"></a><span data-ttu-id="b5a68-113">Установка набора средств Azure для IntelliJ из диалогового окна параметров</span><span class="sxs-lookup"><span data-stu-id="b5a68-113">To install the Azure Toolkit for IntelliJ from the settings dialog box</span></span>

1. <span data-ttu-id="b5a68-114">Запустите IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="b5a68-114">Start IntelliJ IDEA.</span></span>

1. <span data-ttu-id="b5a68-115">Когда откроется IntelliJ IDEA, щелкните **Файл** и выберите **Параметры**.</span><span class="sxs-lookup"><span data-stu-id="b5a68-115">When the IntelliJ IDEA opens, click **File**, then click **Settings**.</span></span>
   
   ![Откройте диалоговое окно параметров IntelliJ IDEA][01a]

1. <span data-ttu-id="b5a68-117">В диалоговом окне "Параметры" нажмите кнопку **Подключаемые модули**, а затем **Browse repositories** (Обзор репозиториев).</span><span class="sxs-lookup"><span data-stu-id="b5a68-117">In the Settings dialog box, click **Plugins**, and then click **Browse repositories**.</span></span>
   
   ![Диалоговое окно параметров IntelliJ IDEA][02a]

1. <span data-ttu-id="b5a68-119">В диалоговом окне **Обзор репозиториев** введите "Azure" в поле поиска.</span><span class="sxs-lookup"><span data-stu-id="b5a68-119">In the **Browse Repositories** dialog box, type "Azure" in the search box.</span></span> <span data-ttu-id="b5a68-120">Выделите **Azure Toolkit for IntelliJ** (Набор средств Azure для IntelliJ) и нажмите кнопку **Установить**.</span><span class="sxs-lookup"><span data-stu-id="b5a68-120">Highlight **Azure Toolkit for IntelliJ**, and then click **Install**.</span></span>
   
   ![Поиск набора средств Azure для IntelliJ][03]
   
   <span data-ttu-id="b5a68-122">Ход установки IntelliJ IDEA отобразится в диалоговом окне.</span><span class="sxs-lookup"><span data-stu-id="b5a68-122">IntelliJ IDEA displays the installation progress in a dialog box.</span></span>
   
   ![Ход установки][04]

1. <span data-ttu-id="b5a68-124">После завершения установки нажмите кнопку **Перезапуск IntelliJ IDEA**.</span><span class="sxs-lookup"><span data-stu-id="b5a68-124">When the installation has completed, click **Restart IntelliJ IDEA**.</span></span>
   
   ![Перезапуск IntelliJ IDEA][05]

1. <span data-ttu-id="b5a68-126">Нажмите кнопку **ОК** , чтобы закрыть диалоговое окно параметров.</span><span class="sxs-lookup"><span data-stu-id="b5a68-126">Click **OK** to close the Settings dialog box.</span></span>
   
   ![Закройте диалоговое окно параметров IntelliJ IDEA][06]

1. <span data-ttu-id="b5a68-128">При появлении запроса на перезапуск или приостановку IntelliJ IDEA нажмите кнопку **Перезагрузить**.</span><span class="sxs-lookup"><span data-stu-id="b5a68-128">When prompted to restart IntelliJ IDEA or postpone, click **Restart**.</span></span>
   
<span data-ttu-id="b5a68-129">1</span><span class="sxs-lookup"><span data-stu-id="b5a68-129">1</span></span>   ![Перезапуск IntelliJ IDEA][07]

## <a name="to-install-the-azure-toolkit-for-intellij-from-the-start-screen"></a><span data-ttu-id="b5a68-131">Установка набора средств Azure для IntelliJ с начального экрана</span><span class="sxs-lookup"><span data-stu-id="b5a68-131">To install the Azure Toolkit for IntelliJ from the start screen</span></span>

1. <span data-ttu-id="b5a68-132">Запустите IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="b5a68-132">Start IntelliJ IDEA.</span></span>

1. <span data-ttu-id="b5a68-133">Когда откроется начальный экран IntelliJ IDEA, нажмите кнопку **Настройка** и выберите **Подключаемые модули**.</span><span class="sxs-lookup"><span data-stu-id="b5a68-133">When the IntelliJ IDEA start screen appears, click **Configure**, then click **Plugins**.</span></span>
   
   ![Подключаемые модули IntelliJ IDEA][01b]

1. <span data-ttu-id="b5a68-135">В диалоговом окне **Подключаемые модули** нажмите кнопку **Browse repositories** (Обзор репозиториев).</span><span class="sxs-lookup"><span data-stu-id="b5a68-135">In the **Plugins** dialog box, click **Browse repositories**.</span></span>
   
   ![Обзор репозиториев подключаемых модулей IntelliJ IDEA][02b]

1. <span data-ttu-id="b5a68-137">В диалоговом окне **Обзор репозиториев** введите "Azure" в поле поиска.</span><span class="sxs-lookup"><span data-stu-id="b5a68-137">In the **Browse Repositories** dialog box, type "Azure" in the search box.</span></span> <span data-ttu-id="b5a68-138">Выделите **Azure Toolkit for IntelliJ** (Набор средств Azure для IntelliJ) и нажмите кнопку **Установить**.</span><span class="sxs-lookup"><span data-stu-id="b5a68-138">Highlight **Azure Toolkit for IntelliJ**, and then click **Install**.</span></span>
   
   ![Поиск набора средств Azure для IntelliJ][03]
   
   <span data-ttu-id="b5a68-140">Ход установки IntelliJ IDEA отобразится в диалоговом окне.</span><span class="sxs-lookup"><span data-stu-id="b5a68-140">IntelliJ IDEA will display the installation progress in a dialog box.</span></span>
   
   ![Ход установки][04]

1. <span data-ttu-id="b5a68-142">После завершения установки нажмите кнопку **Перезапуск IntelliJ IDEA**.</span><span class="sxs-lookup"><span data-stu-id="b5a68-142">When the installation has completed, click **Restart IntelliJ IDEA**.</span></span>
   
   ![Перезапуск IntelliJ IDEA][05]

1. <span data-ttu-id="b5a68-144">При появлении запроса на перезапуск или приостановку IntelliJ IDEA нажмите кнопку **Перезагрузить**.</span><span class="sxs-lookup"><span data-stu-id="b5a68-144">When prompted to restart IntelliJ IDEA or postpone, click **Restart**.</span></span>
   
   ![Перезапуск IntelliJ IDEA][07]

## <a name="next-steps"></a><span data-ttu-id="b5a68-146">Дополнительная информация</span><span class="sxs-lookup"><span data-stu-id="b5a68-146">Next steps</span></span>

[!INCLUDE [azure-toolkit-for-intellij-additional-resources](../includes/azure-toolkit-for-intellij-additional-resources.md)]

<!-- URL List -->

<!-- IMG List -->

[01a]: media/azure-toolkit-for-intellij-installation/01-intellij-file-settings.png
[01b]: media/azure-toolkit-for-intellij-installation/01-intellij-configure-dropdown.png
[02a]: media/azure-toolkit-for-intellij-installation/02-intellij-settings-dialog.png
[02b]: media/azure-toolkit-for-intellij-installation/02-intellij-plugins-dialog.png
[03]: media/azure-toolkit-for-intellij-installation/03-intellij-browse-repositories.png
[04]: media/azure-toolkit-for-intellij-installation/04-install-progress.png
[05]: media/azure-toolkit-for-intellij-installation/05-restart-intellij.png
[06]: media/azure-toolkit-for-intellij-installation/06-intellij-settings-dialog.png
[07]: media/azure-toolkit-for-intellij-installation/07-restart-intellij.png
