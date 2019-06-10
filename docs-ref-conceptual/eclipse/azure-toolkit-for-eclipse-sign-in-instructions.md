---
title: Инструкции по входу для набора средств Azure в Eclipse
description: Узнайте, как войти в Microsoft Azure с помощью набора средств Azure для Eclipse.
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
ms.openlocfilehash: b4b13de38913ae6e7ae2bb09210ac742efc9d0ad
ms.sourcegitcommit: d18d9dce22b7f7af178f756bd341433d24e3c3b5
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/04/2019
ms.locfileid: "66575316"
---
# <a name="sign-in-instructions-for-the-azure-toolkit-for-eclipse"></a><span data-ttu-id="4928d-103">Инструкции по входу для набора средств Azure в Eclipse</span><span class="sxs-lookup"><span data-stu-id="4928d-103">Sign-in instructions for the Azure Toolkit for Eclipse</span></span>

<span data-ttu-id="4928d-104">Набор средств Azure для Eclipse предоставляет два метода для входа в систему с помощью учетной записи Azure:</span><span class="sxs-lookup"><span data-stu-id="4928d-104">The Azure Toolkit for Eclipse provides two methods for signing into your Azure account:</span></span>

  - <span data-ttu-id="4928d-105">[вход в учетную запись Azure с помощью имени пользователя устройства](#sign-in-to-your-azure-account-by-device-login);</span><span class="sxs-lookup"><span data-stu-id="4928d-105">[Sign in to your Azure account by Device Login](#sign-in-to-your-azure-account-by-device-login)</span></span>
  - <span data-ttu-id="4928d-106">[вход в учетную запись Azure с помощью субъекта-службы](#sign-in-to-your-azure-account-by-service-principal).</span><span class="sxs-lookup"><span data-stu-id="4928d-106">[Sign in to your Azure account by Service Principal](#sign-in-to-your-azure-account-by-service-principal)</span></span>

<span data-ttu-id="4928d-107">Предоставляются также методы [**выхода из системы**](#sign-out-of-your-azure-account).</span><span class="sxs-lookup"><span data-stu-id="4928d-107">[**Sign out**](#sign-out-of-your-azure-account) methods are also provided.</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="sign-in-to-your-azure-account-by-device-login"></a><span data-ttu-id="4928d-108">Вход в учетную запись Azure с помощью имени пользователя устройства</span><span class="sxs-lookup"><span data-stu-id="4928d-108">Sign in to your Azure account by Device Login</span></span>

<span data-ttu-id="4928d-109">Чтобы войти в Azure с помощью имени пользователя устройства, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="4928d-109">To sign in Azure by device login, do the following:</span></span>

1. <span data-ttu-id="4928d-110">Откройте проект с помощью Eclipse.</span><span class="sxs-lookup"><span data-stu-id="4928d-110">Open your project with Eclipse.</span></span>

2. <span data-ttu-id="4928d-111">Выберите **Сервис**, **Azure** и затем **Войти**.</span><span class="sxs-lookup"><span data-stu-id="4928d-111">Click **Tools**, then click **Azure**, and then click **Sign In**.</span></span>
   <span data-ttu-id="4928d-112">![Меню Eclipse для входа в систему Azure][I01]</span><span class="sxs-lookup"><span data-stu-id="4928d-112">![Eclipse Menu for Azure Sign In][I01]</span></span>

3. <span data-ttu-id="4928d-113">В окне **Azure Sign In** (Вход в Azure) выберите **Device Login** (Имя пользователя устройства) и щелкните **Sign in** (Вход).</span><span class="sxs-lookup"><span data-stu-id="4928d-113">In the **Azure Sign In** window, select **Device Login**, and then click **Sign in**.</span></span>

   ![Окно Azure Sign In (Вход в Azure) с выбранным именем пользователя устройства][I02]

4. <span data-ttu-id="4928d-115">В диалоговом окне **Azure Device Login** (Вход в систему устройства Azure) щелкните **Copy&Open** (Копировать и открыть).</span><span class="sxs-lookup"><span data-stu-id="4928d-115">Click **Copy&Open** in **Azure Device Login** dialog .</span></span>

   ![Диалоговое окно входа Azure][I03]

> [!NOTE]
>
> <span data-ttu-id="4928d-117">Если браузер не открывается, настройте Eclipse, чтобы использовать внешний браузер, например Internet Explorer, Firefox или Chrome:</span><span class="sxs-lookup"><span data-stu-id="4928d-117">If the browser doesn't open, configure Eclipse to use an external browser like Internet Explorer, Firefox, or Chrome:</span></span>
>
> 1. <span data-ttu-id="4928d-118">Откройте Preferences > General > Web Browser > Use external web browser in Eclipse (Предпочтения > Общие > Веб-браузер > Использование внешнего веб-браузера в Eclipse).</span><span class="sxs-lookup"><span data-stu-id="4928d-118">Open Preferences -> General -> Web Browser -> Use external web browser in Eclipse</span></span>
>
> 2. <span data-ttu-id="4928d-119">Выберите предпочитаемый браузер.</span><span class="sxs-lookup"><span data-stu-id="4928d-119">Select the browser you prefer to use</span></span>
>

5. <span data-ttu-id="4928d-120">В браузере вставьте код устройства (скопированный при нажатии **Copy&Open** (Копировать и открыть) на последнем шаге), а затем нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="4928d-120">In the browser, paste your device code (which has been copied when you clicked **Copy&Open** in last step) and then click **Next**.</span></span>

   ![Вход в систему устройства в браузере][I04]

6. <span data-ttu-id="4928d-122">Наконец, в диалоговом окне **Select Subscriptions** (Выбор подписок) выберите нужные подписки и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="4928d-122">Finally, in the **Select Subscriptions** dialog box, select the subscriptions that you want to use, then click **OK**.</span></span>

   ![Диалоговое окно выбора подписок][I05]

## <a name="sign-in-to-your-azure-account-by-service-principal"></a><span data-ttu-id="4928d-124">Вход в учетную запись Azure с помощью субъекта-службы</span><span class="sxs-lookup"><span data-stu-id="4928d-124">Sign in to your Azure account by Service Principal</span></span>

<span data-ttu-id="4928d-125">В этом разделе показано, как создать файл учетных данных, содержащий данные субъекта-службы.</span><span class="sxs-lookup"><span data-stu-id="4928d-125">This section walks you through creating a credentials file that contains your service principal data.</span></span> <span data-ttu-id="4928d-126">После выполнения этого процесса Eclipse использует файл учетных данных для автоматического входа в Azure при открытии проекта.</span><span class="sxs-lookup"><span data-stu-id="4928d-126">After you have completed this process, Eclipse uses the credentials file to automatically sign you in to Azure when open your project.</span></span>

1. <span data-ttu-id="4928d-127">Откройте проект с помощью Eclipse.</span><span class="sxs-lookup"><span data-stu-id="4928d-127">Open your project with Eclipse.</span></span>

2. <span data-ttu-id="4928d-128">Выберите **Сервис**, **Azure** и затем **Войти**.</span><span class="sxs-lookup"><span data-stu-id="4928d-128">Click **Tools**, then click **Azure**, and then click **Sign In**.</span></span>
   <span data-ttu-id="4928d-129">![Команда Azure Sign In (Вход в Azure) в Eclipse][A01]</span><span class="sxs-lookup"><span data-stu-id="4928d-129">![The Eclipse Azure Sign In command][A01]</span></span>

3. <span data-ttu-id="4928d-130">В окне **Azure Sign In** (Вход в Azure) выберите **Service Principal** (Субъект-служба).</span><span class="sxs-lookup"><span data-stu-id="4928d-130">In the **Azure Sign In** window, select **Service Principal**.</span></span> <span data-ttu-id="4928d-131">Если у вас еще нет файла проверки подлинности с помощью субъекта-службы, щелкните **New** (Создать), чтобы создать его.</span><span class="sxs-lookup"><span data-stu-id="4928d-131">If you do not have the service principal authentication file yet, click **New** to create one.</span></span> <span data-ttu-id="4928d-132">В противном случае вы можете щелкнуть **Browse** (Обзор), чтобы открыть нужный файл и перейти к шагу 8.</span><span class="sxs-lookup"><span data-stu-id="4928d-132">Otherwise you can click **Browse** to open it and jump to step 8.</span></span>

   ![Окно Azure Sign In (Вход в Azure) с выбранным субъектом-службы][A02]

4. <span data-ttu-id="4928d-134">В диалоговом окне **Azure Device Login** (Вход в систему устройства Azure) щелкните **Copy&Open** (Копировать и открыть).</span><span class="sxs-lookup"><span data-stu-id="4928d-134">Click **Copy&Open** in **Azure Device Login** dialog.</span></span>

   ![Диалоговое окно входа Azure][A08]

> [!NOTE]
>
> <span data-ttu-id="4928d-136">Если браузер не открывается, настройте Eclipse, чтобы использовать внешний браузер, например IE или Chrome:</span><span class="sxs-lookup"><span data-stu-id="4928d-136">If the browser doesn't open, configure eclipse to use an external browser like IE or Chrome:</span></span>
>
> 1. <span data-ttu-id="4928d-137">Откройте Preferences > General > Web Browser > Use external web browser in Eclipse (Предпочтения > Общие > Веб-браузер > Использование внешнего веб-браузера в Eclipse).</span><span class="sxs-lookup"><span data-stu-id="4928d-137">Open Preferences -> General -> Web Browser -> Use external web browser in Eclipse</span></span>
>
> 2. <span data-ttu-id="4928d-138">Выберите предпочитаемый браузер.</span><span class="sxs-lookup"><span data-stu-id="4928d-138">Select the browser you prefer to use</span></span>
>

5. <span data-ttu-id="4928d-139">В браузере вставьте код устройства (скопированный при нажатии **Copy&Open** (Копировать и открыть) на последнем шаге), а затем нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="4928d-139">In the browser, paste your device code (which has been copied when you click **Copy&Open** in last step) and then click **Next**.</span></span>

   ![Вход в систему устройства в браузере][A03]

6. <span data-ttu-id="4928d-141">В диалоговом окне **Create authentication files** (Создание файлов проверки подлинности) выберите нужные подписки, конечный каталог и нажмите кнопку **Start** (Начать).</span><span class="sxs-lookup"><span data-stu-id="4928d-141">In the **Create Authentication Files** window, select the subscriptions that you want to use, choose your destination directory, and then click **Start**.</span></span>

   ![Окно Create authentication files (Создание файлов проверки подлинности)][A04]

7. <span data-ttu-id="4928d-143">В диалоговом окне **Service Principal Creation Status** (Состояние создания субъекта-службы) после успешного создания файлов нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="4928d-143">In the **Service Principal Creation Status** dialog box, click **OK** after your files have been created successfully.</span></span>

   ![Диалоговое окно Service Principal Creation Status (Состояние создания субъекта-службы)][A05]

8. <span data-ttu-id="4928d-145">Адрес созданного файла будет автоматически заполнен в окне **Azure Sign In** (Вход в Azure). Теперь щелкните **Sign in** (Вход).</span><span class="sxs-lookup"><span data-stu-id="4928d-145">Address of the created file will be automatically filled in the **Azure Sign In** window, now click **Sign in**.</span></span>

   ![Диалоговое окно входа в Azure][A06]

9. <span data-ttu-id="4928d-147">Наконец, в диалоговом окне **Select Subscriptions** (Выбор подписок) выберите нужные подписки и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="4928d-147">Finally, in the **Select Subscriptions** dialog box, select the subscriptions that you want to use, then click **OK**.</span></span>

   ![Диалоговое окно выбора подписок][A07]

## <a name="sign-out-of-your-azure-account"></a><span data-ttu-id="4928d-149">Выход из учетной записи Azure</span><span class="sxs-lookup"><span data-stu-id="4928d-149">Sign out of your Azure account</span></span>

<span data-ttu-id="4928d-150">После настройки учетной записи путем выполнения действий, описанных в предыдущем разделе, при каждом перезапуске Eclipse будет автоматически выполняться вход.</span><span class="sxs-lookup"><span data-stu-id="4928d-150">After you have configured your account by preceding steps, you will be automatically signed in each time you start Eclipse.</span></span> <span data-ttu-id="4928d-151">Однако если вы хотите выйти из учетной записи Azure, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="4928d-151">However, if you want to sign out of your Azure account, use the following steps.</span></span>

1. <span data-ttu-id="4928d-152">В Eclipse выберите **Сервис**, **Azure** и затем **Выйти**.</span><span class="sxs-lookup"><span data-stu-id="4928d-152">In Eclipse, click **Tools**, then click **Azure**, and then click **Sign Out**.</span></span>

   ![Меню Eclipse для выхода из системы Azure][L01]

2. <span data-ttu-id="4928d-154">При отображении диалогового окна **Выход из Azure** нажмите кнопку **Да**.</span><span class="sxs-lookup"><span data-stu-id="4928d-154">When the **Azure Sign Out** dialog box appears, click **Yes**.</span></span>

   ![Диалоговое окно выхода][L02]

## <a name="next-steps"></a><span data-ttu-id="4928d-156">Дополнительная информация</span><span class="sxs-lookup"><span data-stu-id="4928d-156">Next steps</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-additional-resources](../includes/azure-toolkit-for-eclipse-additional-resources.md)]

<!-- URL List -->


<!-- IMG List -->

[I01]: media/azure-toolkit-for-eclipse-sign-in-instructions/I01.png
[I02]: media/azure-toolkit-for-eclipse-sign-in-instructions/I02.png
[I03]: media/azure-toolkit-for-eclipse-sign-in-instructions/I03.png
[I04]: media/azure-toolkit-for-eclipse-sign-in-instructions/I04.png
[I05]: media/azure-toolkit-for-eclipse-sign-in-instructions/I05.png

[A01]: media/azure-toolkit-for-eclipse-sign-in-instructions/A01.png
[A02]: media/azure-toolkit-for-eclipse-sign-in-instructions/A02.png
[A03]: media/azure-toolkit-for-eclipse-sign-in-instructions/A03.png
[A04]: media/azure-toolkit-for-eclipse-sign-in-instructions/A04.png
[A05]: media/azure-toolkit-for-eclipse-sign-in-instructions/A05.png
[A06]: media/azure-toolkit-for-eclipse-sign-in-instructions/A06.png
[A07]: media/azure-toolkit-for-eclipse-sign-in-instructions/A07.png
[A08]: media/azure-toolkit-for-eclipse-sign-in-instructions/A08.png

[L01]: media/azure-toolkit-for-eclipse-sign-in-instructions/L01.png
[L02]: media/azure-toolkit-for-eclipse-sign-in-instructions/L02.png
[L03]: media/azure-toolkit-for-eclipse-sign-in-instructions/L03.png
