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
ms.openlocfilehash: eb6099ab0c19bf3588cb7fd668f070771e58fe74
ms.sourcegitcommit: b64017f119177f97da7a5930489874e67b09c0fc
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/09/2018
ms.locfileid: "48893625"
---
# <a name="azure-sign-in-instructions-for-the-azure-toolkit-for-eclipse"></a><span data-ttu-id="21c40-103">Инструкции по входу для набора средств Azure для Eclipse</span><span class="sxs-lookup"><span data-stu-id="21c40-103">Azure Sign In Instructions for the Azure Toolkit for Eclipse</span></span>

<span data-ttu-id="21c40-104">Набор средств Azure для Eclipse предоставляет два метода для входа в систему с помощью учетной записи Azure:</span><span class="sxs-lookup"><span data-stu-id="21c40-104">The Azure Toolkit for Eclipse provides two methods for signing into your Azure account:</span></span>

  * <span data-ttu-id="21c40-105">**Автоматически** — при использовании этого метода создается файл учетных данных, содержащий данные субъекта-службы, после чего этот файл можно использовать для автоматического входа в учетную запись Azure.</span><span class="sxs-lookup"><span data-stu-id="21c40-105">**Automated** - when you are using this method, you will create a credentials file which contains your service principal data, after which you can use the credentials file to automatically sign into your Azure account.</span></span>
  * <span data-ttu-id="21c40-106">**Интерактивно** — при использовании этого метода потребуется вводить учетные данные Azure при каждом входе в учетную запись Azure.</span><span class="sxs-lookup"><span data-stu-id="21c40-106">**Interactive** - when you are using this method, you will enter your Azure credentials each time you sign into your Azure account.</span></span>

<span data-ttu-id="21c40-107">В следующих разделах описано использование каждого из методов.</span><span class="sxs-lookup"><span data-stu-id="21c40-107">The steps in the following sections will describe how to use each method.</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="signing-into-your-azure-account-automatically-and-creating-a-credentials-file-to-use-in-the-future"></a><span data-ttu-id="21c40-108">Автоматический вход в учетную запись Azure и создание файла учетных данных для использования в будущем</span><span class="sxs-lookup"><span data-stu-id="21c40-108">Signing into your Azure account automatically and creating a credentials file to use in the future</span></span>

<span data-ttu-id="21c40-109">Описанные ниже действия помогут вам создать файл учетных данных, содержащий данные субъекта-службы.</span><span class="sxs-lookup"><span data-stu-id="21c40-109">The following steps will walk you through creating a credentials file which contains your service principal data.</span></span> <span data-ttu-id="21c40-110">После выполнения этих шагов Eclipse использует файл учетных данных для автоматического входа в Azure при каждом открытии проекта.</span><span class="sxs-lookup"><span data-stu-id="21c40-110">Once you have completed these steps, Eclipse will automatically use the credentials file to automatically sign you into Azure each time you open your project.</span></span>

1. <span data-ttu-id="21c40-111">Откройте проект с помощью Eclipse.</span><span class="sxs-lookup"><span data-stu-id="21c40-111">Open your project with Eclipse.</span></span>

1. <span data-ttu-id="21c40-112">Выберите **Сервис**, **Azure** и затем **Войти**.</span><span class="sxs-lookup"><span data-stu-id="21c40-112">Click **Tools**, then click **Azure**, and then click **Sign In**.</span></span>

   ![Меню Eclipse для входа в систему Azure][A01]

1. <span data-ttu-id="21c40-114">При отображении диалогового окна **Вход в Azure** выберите **Автоматически** и щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="21c40-114">When the **Azure Sign In** dialog box appears, select **Automated**, and then click **New**.</span></span>

   ![Диалоговое окно входа][A02]

1. <span data-ttu-id="21c40-116">При отображении диалогового окна **Вход в Azure** введите учетные данные и щелкните **Войти**.</span><span class="sxs-lookup"><span data-stu-id="21c40-116">When the **Azure Log In** dialog box appears, enter your Azure credentials, and then click **Sign In**.</span></span>

   ![Диалоговое окно входа в Azure][A03]

1. <span data-ttu-id="21c40-118">При отображении диалогового окна **Create authentication files** (Создание файлов проверки подлинности) выберите нужные подписки, конечный каталог и нажмите кнопку **Начать**.</span><span class="sxs-lookup"><span data-stu-id="21c40-118">When the **Create authentication files** dialog box appears, select the subscriptions that you want to use, choose your destination directory, and then click **Start**.</span></span>

   ![Диалоговое окно входа в Azure][A04]

1. <span data-ttu-id="21c40-120">Отображается диалоговое окно **Service Principal Creatation Status** (Состояние создания субъекта-службы). После успешного создания файлов нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="21c40-120">The **Service Principal Creatation Status** dialog box will be displayed, and after your files have been created successfully, click **OK**.</span></span>

   ![Диалоговое окно состояния создания субъекта-службы][A05]

1. <span data-ttu-id="21c40-122">При отображении диалогового окна **Вход в Azure** нажмите кнопку **Войти**.</span><span class="sxs-lookup"><span data-stu-id="21c40-122">When the **Azure Sign In** dialog box appears, click **Sign In**.</span></span>

   ![Диалоговое окно входа в Azure][A06]

1. <span data-ttu-id="21c40-124">При отображении диалогового окна **Выбор подписок** выберите нужные подписки и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="21c40-124">When the **Select Subscriptions** dialog box appears, select the subscriptions that you want to use, and then click **OK**.</span></span>

   ![Диалоговое окно выбора подписок][A07]

## <a name="signing-out-of-your-azure-account-when-you-signed-in-automatically"></a><span data-ttu-id="21c40-126">Выход из учетной записи Azure после автоматического входа</span><span class="sxs-lookup"><span data-stu-id="21c40-126">Signing out of your Azure account when you signed in automatically</span></span>

<span data-ttu-id="21c40-127">После настройки, описанной в предыдущем разделе, набор средств Azure будет автоматически выполнять выход из вашей учетной записи Azure при каждом перезапуске Eclipse.</span><span class="sxs-lookup"><span data-stu-id="21c40-127">After you have configured the steps in the previous section, the Azure Toolkit will automatically sign you into your Azure account each time you restart Eclipse.</span></span> <span data-ttu-id="21c40-128">Чтобы выйти из учетной записи Azure и предотвратить автоматический вход набора средств Azure, сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="21c40-128">However, to sign out of your Azure account and prevent the Azure Toolkit from signing you in automatically, use the following steps.</span></span>

1. <span data-ttu-id="21c40-129">В Eclipse выберите **Сервис**, **Azure** и затем **Выйти**.</span><span class="sxs-lookup"><span data-stu-id="21c40-129">In Eclipse, click **Tools**, then click **Azure**, and then click **Sign Out**.</span></span>

   ![Меню Eclipse для выхода из системы Azure][L01]

1. <span data-ttu-id="21c40-131">При отображении диалогового окна **Выход из Azure** нажмите кнопку **Да**.</span><span class="sxs-lookup"><span data-stu-id="21c40-131">When the **Azure Sign Out** dialog box appears, click **Yes**.</span></span>

   ![Диалоговое окно выхода][L03]

## <a name="signing-into-your-azure-account-automatically-using-a-credentials-file-which-you-have-already-created"></a><span data-ttu-id="21c40-133">Автоматический вход в учетную запись Azure с помощью созданного файла учетных данных</span><span class="sxs-lookup"><span data-stu-id="21c40-133">Signing into your Azure account automatically using a credentials file which you have already created</span></span>

<span data-ttu-id="21c40-134">Если вы выходите из Azure во время применения Eclipse, потребуется перенастроить набор средств Azure для Eclipse, чтобы использовать созданный файл учетных данных для автоматического входа в учетную запись Azure.</span><span class="sxs-lookup"><span data-stu-id="21c40-134">If you sign out of Azure when you are using Eclipse, you will need to reconfigure the Azure Toolkit for Eclipse to use a credentials file which have created before you can automatically sign into your Azure acccount.</span></span> <span data-ttu-id="21c40-135">Указанные ниже шаги помогут настроить набор средств Azure для использования существующего файла учетных данных.</span><span class="sxs-lookup"><span data-stu-id="21c40-135">The following steps will walk you through configuring the Azure Toolkit to use an existing credentials file.</span></span>

1. <span data-ttu-id="21c40-136">Откройте проект с помощью Eclipse.</span><span class="sxs-lookup"><span data-stu-id="21c40-136">Open your project with Eclipse.</span></span>

1. <span data-ttu-id="21c40-137">Выберите **Сервис**, **Azure** и затем **Войти**.</span><span class="sxs-lookup"><span data-stu-id="21c40-137">Click **Tools**, then click **Azure**, and then click **Sign In**.</span></span>

   ![Меню Eclipse для входа в систему Azure][A01]

1. <span data-ttu-id="21c40-139">При отображении диалогового окна **Вход в Azure** выберите **Автоматически** и щелкните **Обзор**.</span><span class="sxs-lookup"><span data-stu-id="21c40-139">When the **Azure Sign In** dialog box appears, select **Automated**, and then click **Browse**.</span></span>

   ![Диалоговое окно входа][A02]

1. <span data-ttu-id="21c40-141">Когда откроется диалоговое окно **Select Authenticated File** (Выбор файла, прошедшего аутентификацию), выберите созданный ранее файл учетных данных и щелкните **Открыть**.</span><span class="sxs-lookup"><span data-stu-id="21c40-141">When the **Select Authenticated File** dialog box appears, select a credentials file which you created earlier, and then click **Open**.</span></span>

   ![Диалоговое окно входа][A08]

1. <span data-ttu-id="21c40-143">При отображении диалогового окна **Вход в Azure** нажмите кнопку **Войти**.</span><span class="sxs-lookup"><span data-stu-id="21c40-143">When the **Azure Sign In** dialog box appears, click **Sign In**.</span></span>

   ![Диалоговое окно входа в Azure][A06]

1. <span data-ttu-id="21c40-145">При отображении диалогового окна **Выбор подписок** выберите нужные подписки и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="21c40-145">When the **Select Subscriptions** dialog box appears, select the subscriptions that you want to use, and then click **OK**.</span></span>

   ![Диалоговое окно выбора подписок][A07]

## <a name="signing-into-your-azure-account-interactively"></a><span data-ttu-id="21c40-147">Интерактивный вход в учетную запись Azure</span><span class="sxs-lookup"><span data-stu-id="21c40-147">Signing into your Azure account interactively</span></span>

<span data-ttu-id="21c40-148">Ниже показано, как войти в Azure, вручную введя учетные данные Azure.</span><span class="sxs-lookup"><span data-stu-id="21c40-148">The following steps will illustrate how to sign into Azure by manually entering your Azure credentials.</span></span>

1. <span data-ttu-id="21c40-149">Откройте проект с помощью Eclipse.</span><span class="sxs-lookup"><span data-stu-id="21c40-149">Open your project with Eclipse.</span></span>

1. <span data-ttu-id="21c40-150">Выберите **Сервис**, **Azure** и затем **Войти**.</span><span class="sxs-lookup"><span data-stu-id="21c40-150">Click **Tools**, then click **Azure**, and then click **Sign In**.</span></span>

   ![Меню Eclipse для входа в систему Azure][I01]

1. <span data-ttu-id="21c40-152">При отображении диалогового окна **Вход в Azure** выберите **Интерактивно** и щелкните **Войти**.</span><span class="sxs-lookup"><span data-stu-id="21c40-152">When the **Azure Sign In** dialog box appears, select **Interactive**, and then click **Sign In**.</span></span>

   ![Диалоговое окно входа][I02]

1. <span data-ttu-id="21c40-154">При отображении диалогового окна **Вход в Azure** введите учетные данные и щелкните **Войти**.</span><span class="sxs-lookup"><span data-stu-id="21c40-154">When the **Azure Log In** dialog box appears, enter your Azure credentials, and then click **Sign In**.</span></span>

   ![Диалоговое окно входа в Azure][I03]

1. <span data-ttu-id="21c40-156">При отображении диалогового окна **Выбор подписок** выберите нужные подписки и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="21c40-156">When the **Select Subscriptions** dialog box appears, select the subscriptions that you want to use, and then click **OK**.</span></span>

   ![Диалоговое окно выбора подписок][I04]

## <a name="signing-out-of-your-azure-account-when-you-signed-in-interactively"></a><span data-ttu-id="21c40-158">Выход из учетной записи Azure после интерактивного входа</span><span class="sxs-lookup"><span data-stu-id="21c40-158">Signing out of your Azure account when you signed in interactively</span></span>

<span data-ttu-id="21c40-159">После настройки, описанной в предыдущем разделе, вы будете автоматически выходить из своей учетной записи Azure при каждом перезапуске Eclipse.</span><span class="sxs-lookup"><span data-stu-id="21c40-159">After you have configured the steps in the previous section, you will automatically signed out of your Azure account each time you restart Eclipse.</span></span> <span data-ttu-id="21c40-160">Однако если вы хотите выйти из учетной записи Azure без перезапуска Eclipse, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="21c40-160">However, if you want to sign out of your Azure account without restarting Eclipse, use the following steps.</span></span>

1. <span data-ttu-id="21c40-161">В Eclipse выберите **Сервис**, **Azure** и затем **Выйти**.</span><span class="sxs-lookup"><span data-stu-id="21c40-161">In Eclipse, click **Tools**, then click **Azure**, and then click **Sign Out**.</span></span>

   ![Меню Eclipse для выхода из системы Azure][L01]

1. <span data-ttu-id="21c40-163">При отображении диалогового окна **Выход из Azure** нажмите кнопку **Да**.</span><span class="sxs-lookup"><span data-stu-id="21c40-163">When the **Azure Sign Out** dialog box appears, click **Yes**.</span></span>

   ![Диалоговое окно выхода][L02]

## <a name="next-steps"></a><span data-ttu-id="21c40-165">Дополнительная информация</span><span class="sxs-lookup"><span data-stu-id="21c40-165">Next steps</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-additional-resources](../includes/azure-toolkit-for-eclipse-additional-resources.md)]

<!-- URL List -->


<!-- IMG List -->

[I01]: media/azure-toolkit-for-eclipse-sign-in-instructions/I01.png
[I02]: media/azure-toolkit-for-eclipse-sign-in-instructions/I02.png
[I03]: media/azure-toolkit-for-eclipse-sign-in-instructions/I03.png
[I04]: media/azure-toolkit-for-eclipse-sign-in-instructions/I04.png

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
