---
title: "Установка набора средств Azure для IntelliJ"
description: "Узнайте, как установить набор средств Azure для IntelliJ IDEA."
services: 
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
ms.assetid: c6817c7b-f28c-4c06-8216-41c7a8117de3
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 10/19/2017
ms.author: robmcm
ms.openlocfilehash: 497aba02f55383bf0b32461752d6681867cdfac8
ms.sourcegitcommit: 7f8538e41c833deb69c300ad3431a431136a1f3e
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/24/2017
---
# <a name="installing-the-azure-toolkit-for-intellij"></a><span data-ttu-id="cc2a6-103">Установка набора средств Azure для IntelliJ</span><span class="sxs-lookup"><span data-stu-id="cc2a6-103">Installing the Azure Toolkit for IntelliJ</span></span>
<span data-ttu-id="cc2a6-104">В набор средств Azure для IntelliJ входят шаблоны и функциональные возможности для простого создания, разработки, тестирования и развертывания приложений Azure с помощью среды разработки IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="cc2a6-104">The Azure Toolkit for IntelliJ provides templates and functionality that allow you to easily create, develop, test, and deploy Azure applications using the IntelliJ IDEA development environment.</span></span> <span data-ttu-id="cc2a6-105">Набор средств Azure для IntelliJ — это проект с открытым кодом, исходный код которого доступен по лицензии MIT на сайте проекта в GitHub по следующему URL-адресу:</span><span class="sxs-lookup"><span data-stu-id="cc2a6-105">The Azure Toolkit for IntelliJ is an Open Source project, whose source code is available under the MIT License from the project's site on GitHub at the following URL:</span></span>

<span data-ttu-id="cc2a6-106"><https://github.com/microsoft/azure-tools-for-java></span><span class="sxs-lookup"><span data-stu-id="cc2a6-106"><https://github.com/microsoft/azure-tools-for-java></span></span>

<span data-ttu-id="cc2a6-107">Набор средств Azure для IntelliJ можно установить двумя способами — из диалогового окна "Параметры" и их меню "Настройка" на начальном экране; оба способа установки будут продемонстрированы ниже.</span><span class="sxs-lookup"><span data-stu-id="cc2a6-107">There are two methods of installing the Azure Toolkit for IntelliJ, from the Settings dialog box and from the Configure menu on the start screen; both installation methods will be demonstrated in the following steps.</span></span>

[!INCLUDE [azure-toolkit-for-IntelliJ-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="to-install-the-azure-toolkit-for-intellij-from-the-settings-dialog-box"></a><span data-ttu-id="cc2a6-108">Установка набора средств Azure для IntelliJ из диалогового окна параметров</span><span class="sxs-lookup"><span data-stu-id="cc2a6-108">To install the Azure Toolkit for IntelliJ from the settings dialog box</span></span>

1. <span data-ttu-id="cc2a6-109">Запустите IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="cc2a6-109">Start IntelliJ IDEA.</span></span>

1. <span data-ttu-id="cc2a6-110">Когда откроется IntelliJ IDEA, щелкните **Файл** и выберите **Параметры**.</span><span class="sxs-lookup"><span data-stu-id="cc2a6-110">When the IntelliJ IDEA opens, click **File**, then click **Settings**.</span></span>
   
   ![Откройте диалоговое окно параметров IntelliJ IDEA][01a]

1. <span data-ttu-id="cc2a6-112">В диалоговом окне "Параметры" нажмите кнопку **Подключаемые модули**, а затем **Browse repositories** (Обзор репозиториев).</span><span class="sxs-lookup"><span data-stu-id="cc2a6-112">In the Settings dialog box, click **Plugins**, and then click **Browse repositories**.</span></span>
   
   ![Диалоговое окно параметров IntelliJ IDEA][02a]

1. <span data-ttu-id="cc2a6-114">В диалоговом окне **Обзор репозиториев** введите "Azure" в поле поиска.</span><span class="sxs-lookup"><span data-stu-id="cc2a6-114">In the **Browse Repositories** dialog box, type "Azure" in the search box.</span></span> <span data-ttu-id="cc2a6-115">Выделите **Azure Toolkit for IntelliJ** (Набор средств Azure для IntelliJ) и нажмите кнопку **Установить**.</span><span class="sxs-lookup"><span data-stu-id="cc2a6-115">Highlight **Azure Toolkit for IntelliJ**, and then click **Install**.</span></span>
   
   ![Поиск набора средств Azure для IntelliJ][03]
   
   <span data-ttu-id="cc2a6-117">Ход установки IntelliJ IDEA отобразится в диалоговом окне.</span><span class="sxs-lookup"><span data-stu-id="cc2a6-117">IntelliJ IDEA displays the installation progress in a dialog box.</span></span>
   
   ![Ход установки][04]

1. <span data-ttu-id="cc2a6-119">После завершения установки нажмите кнопку **Перезапуск IntelliJ IDEA**.</span><span class="sxs-lookup"><span data-stu-id="cc2a6-119">When the installation has completed, click **Restart IntelliJ IDEA**.</span></span>
   
   ![Перезапуск IntelliJ IDEA][05]

1. <span data-ttu-id="cc2a6-121">Нажмите кнопку **ОК** , чтобы закрыть диалоговое окно параметров.</span><span class="sxs-lookup"><span data-stu-id="cc2a6-121">Click **OK** to close the Settings dialog box.</span></span>
   
   ![Закройте диалоговое окно параметров IntelliJ IDEA][06]

1. <span data-ttu-id="cc2a6-123">При появлении запроса на перезапуск или приостановку IntelliJ IDEA нажмите кнопку **Перезагрузить**.</span><span class="sxs-lookup"><span data-stu-id="cc2a6-123">When prompted to restart IntelliJ IDEA or postpone, click **Restart**.</span></span>
   
<span data-ttu-id="cc2a6-124">1</span><span class="sxs-lookup"><span data-stu-id="cc2a6-124">1</span></span>   ![Перезапуск IntelliJ IDEA][07]

## <a name="to-install-the-azure-toolkit-for-intellij-from-the-start-screen"></a><span data-ttu-id="cc2a6-126">Установка набора средств Azure для IntelliJ с начального экрана</span><span class="sxs-lookup"><span data-stu-id="cc2a6-126">To install the Azure Toolkit for IntelliJ from the start screen</span></span>

1. <span data-ttu-id="cc2a6-127">Запустите IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="cc2a6-127">Start IntelliJ IDEA.</span></span>

1. <span data-ttu-id="cc2a6-128">Когда откроется начальный экран IntelliJ IDEA, нажмите кнопку **Настройка** и выберите **Подключаемые модули**.</span><span class="sxs-lookup"><span data-stu-id="cc2a6-128">When the IntelliJ IDEA start screen appears, click **Configure**, then click **Plugins**.</span></span>
   
   ![Подключаемые модули IntelliJ IDEA][01b]

1. <span data-ttu-id="cc2a6-130">В диалоговом окне **Подключаемые модули** нажмите кнопку **Browse repositories** (Обзор репозиториев).</span><span class="sxs-lookup"><span data-stu-id="cc2a6-130">In the **Plugins** dialog box, click **Browse repositories**.</span></span>
   
   ![Обзор репозиториев подключаемых модулей IntelliJ IDEA][02b]

1. <span data-ttu-id="cc2a6-132">В диалоговом окне **Обзор репозиториев** введите "Azure" в поле поиска.</span><span class="sxs-lookup"><span data-stu-id="cc2a6-132">In the **Browse Repositories** dialog box, type "Azure" in the search box.</span></span> <span data-ttu-id="cc2a6-133">Выделите **Azure Toolkit for IntelliJ** (Набор средств Azure для IntelliJ) и нажмите кнопку **Установить**.</span><span class="sxs-lookup"><span data-stu-id="cc2a6-133">Highlight **Azure Toolkit for IntelliJ**, and then click **Install**.</span></span>
   
   ![Поиск набора средств Azure для IntelliJ][03]
   
   <span data-ttu-id="cc2a6-135">Ход установки IntelliJ IDEA отобразится в диалоговом окне.</span><span class="sxs-lookup"><span data-stu-id="cc2a6-135">IntelliJ IDEA will display the installation progress in a dialog box.</span></span>
   
   ![Ход установки][04]

1. <span data-ttu-id="cc2a6-137">После завершения установки нажмите кнопку **Перезапуск IntelliJ IDEA**.</span><span class="sxs-lookup"><span data-stu-id="cc2a6-137">When the installation has completed, click **Restart IntelliJ IDEA**.</span></span>
   
   ![Перезапуск IntelliJ IDEA][05]

1. <span data-ttu-id="cc2a6-139">При появлении запроса на перезапуск или приостановку IntelliJ IDEA нажмите кнопку **Перезагрузить**.</span><span class="sxs-lookup"><span data-stu-id="cc2a6-139">When prompted to restart IntelliJ IDEA or postpone, click **Restart**.</span></span>
   
   ![Перезапуск IntelliJ IDEA][07]

## <a name="next-steps"></a><span data-ttu-id="cc2a6-141">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="cc2a6-141">Next steps</span></span>

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

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
