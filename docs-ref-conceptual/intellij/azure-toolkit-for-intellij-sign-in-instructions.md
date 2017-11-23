---
title: "Инструкции по входу для набора средств Azure для IntelliJ"
description: "Сведения о входе в Microsoft Azure с помощью набора средств Azure для IntelliJ."
services: 
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 11/01/2017
ms.author: robmcm
ms.openlocfilehash: 25c25e58b079c1e08d62feff389b899b26e82b5e
ms.sourcegitcommit: 613c1ffd2e0279fc7a96fca98aa1809563f52ee1
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/18/2017
---
# <a name="sign-in-instructions-for-the-azure-toolkit-for-intellij"></a><span data-ttu-id="677de-103">Инструкции по входу для набора средств Azure для IntelliJ</span><span class="sxs-lookup"><span data-stu-id="677de-103">Sign-in instructions for the Azure Toolkit for IntelliJ</span></span>

<span data-ttu-id="677de-104">Набор средств Azure для IntelliJ предоставляет два метода для входа в систему с помощью учетной записи Azure:</span><span class="sxs-lookup"><span data-stu-id="677de-104">The Azure Toolkit for IntelliJ provides two methods for signing in to your Azure account:</span></span>

  * <span data-ttu-id="677de-105">**Автоматический.** Вы создаете файл учетных данных, который можно использовать для автоматического входа в учетную запись Azure.</span><span class="sxs-lookup"><span data-stu-id="677de-105">**Automated**: You create a credentials file that you can use to automatically sign in to your Azure account.</span></span>
  * <span data-ttu-id="677de-106">**Интерактивный.** Учетные данные Azure необходимо вводить при каждом входе в учетную запись.</span><span class="sxs-lookup"><span data-stu-id="677de-106">**Interactive**: You enter your Azure credentials each time you sign in to your Azure account.</span></span>

<span data-ttu-id="677de-107">В разделах ниже описано использование каждого из методов.</span><span class="sxs-lookup"><span data-stu-id="677de-107">The following sections describe how to use each method.</span></span>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="sign-in-to-your-azure-account-automatically"></a><span data-ttu-id="677de-108">Автоматический вход в учетную запись Azure</span><span class="sxs-lookup"><span data-stu-id="677de-108">Sign in to your Azure account automatically</span></span>

<span data-ttu-id="677de-109">В этом разделе показано, как создать файл учетных данных, содержащий данные субъекта-службы.</span><span class="sxs-lookup"><span data-stu-id="677de-109">This section walks you through creating a credentials file that contains your service principal data.</span></span> <span data-ttu-id="677de-110">После выполнения этого процесса Eclipse использует файл учетных данных для автоматического входа в Azure при каждом открытии проекта.</span><span class="sxs-lookup"><span data-stu-id="677de-110">After you have completed this process, Eclipse uses the credentials file to automatically sign you in to Azure each time you open your project.</span></span>

1. <span data-ttu-id="677de-111">Откройте проект с помощью IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="677de-111">Open your project with IntelliJ IDEA.</span></span>

1. <span data-ttu-id="677de-112">В меню **Tools** (Средства) наведите указатель мыши на пункт **Azure**, а затем щелкните **Azure Sign In** (Вход в Azure).</span><span class="sxs-lookup"><span data-stu-id="677de-112">On the **Tools** menu, point to **Azure**, and then click **Azure Sign In**.</span></span>

   ![Команда Azure Sign In (Вход в Azure) в IntelliJ][A01]

1. <span data-ttu-id="677de-114">В диалоговом окне **Azure Sign In** (Вход в Azure) выберите **Automated** (Автоматически) и щелкните **New** (Создать).</span><span class="sxs-lookup"><span data-stu-id="677de-114">In the **Azure Sign In** window, select **Automated**, and then click **New**.</span></span>

   ![Окно Azure Sign In (Вход в Azure) с выбранным значением Automated (Автоматически)][A02]

1. <span data-ttu-id="677de-116">В диалоговом окне **входа в Azure** введите учетные данные и щелкните **Sign in** (Войти).</span><span class="sxs-lookup"><span data-stu-id="677de-116">In the **Azure Login Dialog** window, enter your Azure credentials, and then click **Sign in**.</span></span>

   ![Диалоговое окно входа Azure][A03]

1. <span data-ttu-id="677de-118">В диалоговом окне **Create authentication files** (Создание файлов проверки подлинности) выберите нужные подписки, конечный каталог и нажмите кнопку **Start** (Начать).</span><span class="sxs-lookup"><span data-stu-id="677de-118">In the **Create Authentication Files** window, select the subscriptions that you want to use, choose your destination directory, and then click **Start**.</span></span>

   ![Окно Create authentication files (Создание файлов проверки подлинности)][A04]

1. <span data-ttu-id="677de-120">В диалоговом окне **Service Principal Creation Status** (Состояние создания субъекта-службы) после успешного создания файлов нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="677de-120">In the **Service Principal Creation Status** dialog box, after your files have been created successfully, click **OK**.</span></span>

   ![Диалоговое окно Service Principal Creation Status (Состояние создания субъекта-службы)][A05]

1. <span data-ttu-id="677de-122">В окне **Azure Sign In** (Вход в Azure) щелкните **Sign in** (Войти).</span><span class="sxs-lookup"><span data-stu-id="677de-122">In the **Azure Sign In** window, click **Sign in**.</span></span>

   ![Диалоговое окно входа в Azure][A06]

1. <span data-ttu-id="677de-124">В диалоговом окне **Select Subscriptions** (Выбор подписок) выберите нужные подписки и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="677de-124">In the **Select Subscriptions** dialog box, select the subscriptions that you want to use, and then click **OK**.</span></span>

   ![Диалоговое окно выбора подписок][A07]

## <a name="sign-out-of-your-azure-account-after-you-have-signed-in-automatically"></a><span data-ttu-id="677de-126">Выход из учетной записи Azure после автоматического входа</span><span class="sxs-lookup"><span data-stu-id="677de-126">Sign out of your Azure account after you have signed in automatically</span></span>

<span data-ttu-id="677de-127">После настройки учетной записи с помощью действий, описанных в предыдущем разделе, набор средств Azure автоматически входит в учетную запись Azure при каждом перезапуске IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="677de-127">After you have configured your account by using the preceding steps, the Azure Toolkit automatically signs you in to your Azure account each time you restart IntelliJ IDEA.</span></span> <span data-ttu-id="677de-128">Чтобы выйти из учетной записи Azure и предотвратить автоматический вход набора средств Azure, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="677de-128">However, to sign out of your Azure account and prevent the Azure Toolkit from signing you in automatically, do the following:</span></span>

1. <span data-ttu-id="677de-129">В IntelliJ IDEA в меню **Tools** (Средства) наведите указатель мыши на пункт **Azure**, а затем щелкните **Azure Sign Out** (Выход из Azure).</span><span class="sxs-lookup"><span data-stu-id="677de-129">In IntelliJ IDEA, on the **Tools** menu, point to **Azure**, and then click **Azure Sign Out**.</span></span>

   ![Команда Azure Sign Out (Выход из Azure) в IntelliJ][L01]

1. <span data-ttu-id="677de-131">В диалоговом окне подтверждения **выхода из Azure** нажмите кнопку **Да**.</span><span class="sxs-lookup"><span data-stu-id="677de-131">In the **Azure Sign Out** confirmation window, click **Yes**.</span></span>

   ![Диалоговое окно подтверждения выхода из Azure][L03]

## <a name="sign-in-to-your-azure-account-automatically-by-using-an-existing-credentials-file"></a><span data-ttu-id="677de-133">Автоматический вход в учетную запись Azure с помощью имеющегося файла учетных данных</span><span class="sxs-lookup"><span data-stu-id="677de-133">Sign in to your Azure account automatically by using an existing credentials file</span></span>

<span data-ttu-id="677de-134">Если вы выходите из учетной записи Azure во время использования IntelliJ IDEA, вам потребуется использовать созданный файл учетных данных для автоматического входа в учетную запись Azure.</span><span class="sxs-lookup"><span data-stu-id="677de-134">If you sign out of your Azure account when you are using IntelliJ IDEA, you must use an existing credentials file to automatically sign back in to the account.</span></span> <span data-ttu-id="677de-135">Чтобы настроить набор средств Azure для Eclipse на использование имеющегося файла учетных данных, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="677de-135">To configure the Azure Toolkit for Eclipse to use an existing credentials file, do the following:</span></span>

1. <span data-ttu-id="677de-136">Откройте проект с помощью IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="677de-136">Open your project with IntelliJ IDEA.</span></span>

1. <span data-ttu-id="677de-137">В меню **Tools** (Средства) наведите указатель мыши на пункт **Azure**, а затем щелкните **Azure Sign In** (Вход в Azure).</span><span class="sxs-lookup"><span data-stu-id="677de-137">On the **Tools** menu, point to **Azure**, and then click **Azure Sign In**.</span></span>

   ![Команда Azure Sign In (Вход в Azure) в IntelliJ][A01]

1. <span data-ttu-id="677de-139">В диалоговом окне **Azure Sign In** (Вход в Azure) выберите **Automated** (Автоматически) и щелкните **Browse** (Обзор).</span><span class="sxs-lookup"><span data-stu-id="677de-139">In the **Azure Sign In** window, select **Automated**, and then click **Browse**.</span></span>

   ![Окно Azure Sign In (Вход в Azure) с выбранным значением Automated (Автоматически)][A02]

1. <span data-ttu-id="677de-141">В диалоговом окне **Select Authentication File** (Выбор файла проверки подлинности) выберите созданный ранее файл учетных данных ранее и нажмите кнопку **Select** (Выбрать).</span><span class="sxs-lookup"><span data-stu-id="677de-141">In the **Select Authentication File** dialog box, select a previously created credentials file, and then click **Select**.</span></span>

   ![Диалоговое окно Select Authentication File (Выбор файла проверки подлинности)][A08]

1. <span data-ttu-id="677de-143">В окне **Azure Sign In** (Вход в Azure) щелкните **Sign in** (Войти).</span><span class="sxs-lookup"><span data-stu-id="677de-143">In the **Azure Sign In** window, click **Sign in**.</span></span>

   ![Окно Azure Sign In (Вход в Azure) с выбранным значением Automated (Автоматически)][A06]

1. <span data-ttu-id="677de-145">В диалоговом окне **Select Subscriptions** (Выбор подписок) выберите нужные подписки и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="677de-145">In the **Select Subscriptions** dialog box, select the subscriptions that you want to use, and then click **OK**.</span></span>

   ![Диалоговое окно выбора подписок][A07]

## <a name="sign-in-to-your-azure-account-interactively"></a><span data-ttu-id="677de-147">Интерактивный вход в учетную запись Azure</span><span class="sxs-lookup"><span data-stu-id="677de-147">Sign in to your Azure account interactively</span></span>

<span data-ttu-id="677de-148">Чтобы войти в Azure, вручную введя учетные данные Azure, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="677de-148">To sign in to Azure by manually entering your Azure credentials, do the following:</span></span>

1. <span data-ttu-id="677de-149">Откройте проект с помощью IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="677de-149">Open your project with IntelliJ IDEA.</span></span>

1. <span data-ttu-id="677de-150">Выберите **Tools** (Средства), наведите указатель мыши на пункт **Azure**, а затем щелкните **Azure Sign In** (Вход в Azure).</span><span class="sxs-lookup"><span data-stu-id="677de-150">Click **Tools**, point to **Azure**, and then click **Azure Sign In**.</span></span>

   ![Команда Azure Sign In (Вход в Azure) в IntelliJ][I01]

1. <span data-ttu-id="677de-152">В окне **Azure Sign In** (Вход в Azure) выберите **Interactive** (Интерактивный) и щелкните **Sign in** (Войти).</span><span class="sxs-lookup"><span data-stu-id="677de-152">In the **Azure Sign In** window, select **Interactive**, and then click **Sign in**.</span></span>

   ![Окно Azure Sign In (Вход в Azure) с выбранным значением Interactive (Интерактивный)][I02]

1. <span data-ttu-id="677de-154">При отображении диалогового окна **Azure Log In** (Вход в Azure) введите учетные данные и щелкните **Sign in** (Войти).</span><span class="sxs-lookup"><span data-stu-id="677de-154">In the **Azure Log In** dialog box appears, enter your Azure credentials, and then click **Sign in**.</span></span>

   ![Диалоговое окно входа Azure][I03]

1. <span data-ttu-id="677de-156">В диалоговом окне **Select Subscriptions** (Выбор подписок) выберите нужные подписки и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="677de-156">In the **Select Subscriptions** dialog box, select the subscriptions that you want to use, and then click **OK**.</span></span>

   ![Диалоговое окно выбора подписок][I04]

## <a name="sign-out-of-your-azure-account-after-you-have-signed-in-interactively"></a><span data-ttu-id="677de-158">Выход из учетной записи Azure после интерактивного входа</span><span class="sxs-lookup"><span data-stu-id="677de-158">Sign out of your Azure account after you have signed in interactively</span></span>

<span data-ttu-id="677de-159">После настройки учетной записи с помощью действий, описанных в предыдущем разделе, вы будете автоматически выходить из своей учетной записи Azure при каждом перезапуске IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="677de-159">After you have configured your account by using the preceding steps, you will be automatically signed out of your Azure account each time you restart IntelliJ IDEA.</span></span> <span data-ttu-id="677de-160">Но если вы хотите выйти из учетной записи Azure, *не перезапуская* IntelliJ IDEA, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="677de-160">However, if you want to sign out of your Azure account *without* restarting IntelliJ IDEA, do the following.</span></span>

1. <span data-ttu-id="677de-161">В IntelliJ IDEA в меню **Tools** (Средства) наведите указатель мыши на пункт **Azure**, а затем щелкните **Azure Sign Out** (Выход из Azure).</span><span class="sxs-lookup"><span data-stu-id="677de-161">In IntelliJ IDEA, on the **Tools** menu, point to **Azure**, and then click **Azure Sign Out**.</span></span>

   ![Команда Azure Sign Out (Выход из Azure) в IntelliJ][L01]

1. <span data-ttu-id="677de-163">В диалоговом окне подтверждения **выхода из Azure** нажмите кнопку **Да**.</span><span class="sxs-lookup"><span data-stu-id="677de-163">In the **Azure Sign Out** confirmation window, click **Yes**.</span></span>

   ![Диалоговое окно подтверждения выхода из Azure][L02]

## <a name="next-steps"></a><span data-ttu-id="677de-165">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="677de-165">Next steps</span></span>

[!INCLUDE [azure-toolkit-for-intellij-additional-resources](../includes/azure-toolkit-for-intellij-additional-resources.md)]

<!-- URL List -->

<!-- IMG List -->

[I01]: media/azure-toolkit-for-intellij-sign-in-instructions/I01.png
[I02]: media/azure-toolkit-for-intellij-sign-in-instructions/I02.png
[I03]: media/azure-toolkit-for-intellij-sign-in-instructions/I03.png
[I04]: media/azure-toolkit-for-intellij-sign-in-instructions/I04.png

[A01]: media/azure-toolkit-for-intellij-sign-in-instructions/A01.png
[A02]: media/azure-toolkit-for-intellij-sign-in-instructions/A02.png
[A03]: media/azure-toolkit-for-intellij-sign-in-instructions/A03.png
[A04]: media/azure-toolkit-for-intellij-sign-in-instructions/A04.png
[A05]: media/azure-toolkit-for-intellij-sign-in-instructions/A05.png
[A06]: media/azure-toolkit-for-intellij-sign-in-instructions/A06.png
[A07]: media/azure-toolkit-for-intellij-sign-in-instructions/A07.png
[A08]: media/azure-toolkit-for-intellij-sign-in-instructions/A08.png

[L01]: media/azure-toolkit-for-intellij-sign-in-instructions/L01.png
[L02]: media/azure-toolkit-for-intellij-sign-in-instructions/L02.png
[L03]: media/azure-toolkit-for-intellij-sign-in-instructions/L03.png
