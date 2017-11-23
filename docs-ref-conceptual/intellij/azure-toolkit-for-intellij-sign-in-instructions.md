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
# <a name="sign-in-instructions-for-the-azure-toolkit-for-intellij"></a>Инструкции по входу для набора средств Azure для IntelliJ

Набор средств Azure для IntelliJ предоставляет два метода для входа в систему с помощью учетной записи Azure:

  * **Автоматический.** Вы создаете файл учетных данных, который можно использовать для автоматического входа в учетную запись Azure.
  * **Интерактивный.** Учетные данные Azure необходимо вводить при каждом входе в учетную запись.

В разделах ниже описано использование каждого из методов.

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="sign-in-to-your-azure-account-automatically"></a>Автоматический вход в учетную запись Azure

В этом разделе показано, как создать файл учетных данных, содержащий данные субъекта-службы. После выполнения этого процесса Eclipse использует файл учетных данных для автоматического входа в Azure при каждом открытии проекта.

1. Откройте проект с помощью IntelliJ IDEA.

1. В меню **Tools** (Средства) наведите указатель мыши на пункт **Azure**, а затем щелкните **Azure Sign In** (Вход в Azure).

   ![Команда Azure Sign In (Вход в Azure) в IntelliJ][A01]

1. В диалоговом окне **Azure Sign In** (Вход в Azure) выберите **Automated** (Автоматически) и щелкните **New** (Создать).

   ![Окно Azure Sign In (Вход в Azure) с выбранным значением Automated (Автоматически)][A02]

1. В диалоговом окне **входа в Azure** введите учетные данные и щелкните **Sign in** (Войти).

   ![Диалоговое окно входа Azure][A03]

1. В диалоговом окне **Create authentication files** (Создание файлов проверки подлинности) выберите нужные подписки, конечный каталог и нажмите кнопку **Start** (Начать).

   ![Окно Create authentication files (Создание файлов проверки подлинности)][A04]

1. В диалоговом окне **Service Principal Creation Status** (Состояние создания субъекта-службы) после успешного создания файлов нажмите кнопку **ОК**.

   ![Диалоговое окно Service Principal Creation Status (Состояние создания субъекта-службы)][A05]

1. В окне **Azure Sign In** (Вход в Azure) щелкните **Sign in** (Войти).

   ![Диалоговое окно входа в Azure][A06]

1. В диалоговом окне **Select Subscriptions** (Выбор подписок) выберите нужные подписки и нажмите кнопку **ОК**.

   ![Диалоговое окно выбора подписок][A07]

## <a name="sign-out-of-your-azure-account-after-you-have-signed-in-automatically"></a>Выход из учетной записи Azure после автоматического входа

После настройки учетной записи с помощью действий, описанных в предыдущем разделе, набор средств Azure автоматически входит в учетную запись Azure при каждом перезапуске IntelliJ IDEA. Чтобы выйти из учетной записи Azure и предотвратить автоматический вход набора средств Azure, сделайте следующее:

1. В IntelliJ IDEA в меню **Tools** (Средства) наведите указатель мыши на пункт **Azure**, а затем щелкните **Azure Sign Out** (Выход из Azure).

   ![Команда Azure Sign Out (Выход из Azure) в IntelliJ][L01]

1. В диалоговом окне подтверждения **выхода из Azure** нажмите кнопку **Да**.

   ![Диалоговое окно подтверждения выхода из Azure][L03]

## <a name="sign-in-to-your-azure-account-automatically-by-using-an-existing-credentials-file"></a>Автоматический вход в учетную запись Azure с помощью имеющегося файла учетных данных

Если вы выходите из учетной записи Azure во время использования IntelliJ IDEA, вам потребуется использовать созданный файл учетных данных для автоматического входа в учетную запись Azure. Чтобы настроить набор средств Azure для Eclipse на использование имеющегося файла учетных данных, сделайте следующее:

1. Откройте проект с помощью IntelliJ IDEA.

1. В меню **Tools** (Средства) наведите указатель мыши на пункт **Azure**, а затем щелкните **Azure Sign In** (Вход в Azure).

   ![Команда Azure Sign In (Вход в Azure) в IntelliJ][A01]

1. В диалоговом окне **Azure Sign In** (Вход в Azure) выберите **Automated** (Автоматически) и щелкните **Browse** (Обзор).

   ![Окно Azure Sign In (Вход в Azure) с выбранным значением Automated (Автоматически)][A02]

1. В диалоговом окне **Select Authentication File** (Выбор файла проверки подлинности) выберите созданный ранее файл учетных данных ранее и нажмите кнопку **Select** (Выбрать).

   ![Диалоговое окно Select Authentication File (Выбор файла проверки подлинности)][A08]

1. В окне **Azure Sign In** (Вход в Azure) щелкните **Sign in** (Войти).

   ![Окно Azure Sign In (Вход в Azure) с выбранным значением Automated (Автоматически)][A06]

1. В диалоговом окне **Select Subscriptions** (Выбор подписок) выберите нужные подписки и нажмите кнопку **ОК**.

   ![Диалоговое окно выбора подписок][A07]

## <a name="sign-in-to-your-azure-account-interactively"></a>Интерактивный вход в учетную запись Azure

Чтобы войти в Azure, вручную введя учетные данные Azure, сделайте следующее:

1. Откройте проект с помощью IntelliJ IDEA.

1. Выберите **Tools** (Средства), наведите указатель мыши на пункт **Azure**, а затем щелкните **Azure Sign In** (Вход в Azure).

   ![Команда Azure Sign In (Вход в Azure) в IntelliJ][I01]

1. В окне **Azure Sign In** (Вход в Azure) выберите **Interactive** (Интерактивный) и щелкните **Sign in** (Войти).

   ![Окно Azure Sign In (Вход в Azure) с выбранным значением Interactive (Интерактивный)][I02]

1. При отображении диалогового окна **Azure Log In** (Вход в Azure) введите учетные данные и щелкните **Sign in** (Войти).

   ![Диалоговое окно входа Azure][I03]

1. В диалоговом окне **Select Subscriptions** (Выбор подписок) выберите нужные подписки и нажмите кнопку **ОК**.

   ![Диалоговое окно выбора подписок][I04]

## <a name="sign-out-of-your-azure-account-after-you-have-signed-in-interactively"></a>Выход из учетной записи Azure после интерактивного входа

После настройки учетной записи с помощью действий, описанных в предыдущем разделе, вы будете автоматически выходить из своей учетной записи Azure при каждом перезапуске IntelliJ IDEA. Но если вы хотите выйти из учетной записи Azure, *не перезапуская* IntelliJ IDEA, сделайте следующее:

1. В IntelliJ IDEA в меню **Tools** (Средства) наведите указатель мыши на пункт **Azure**, а затем щелкните **Azure Sign Out** (Выход из Azure).

   ![Команда Azure Sign Out (Выход из Azure) в IntelliJ][L01]

1. В диалоговом окне подтверждения **выхода из Azure** нажмите кнопку **Да**.

   ![Диалоговое окно подтверждения выхода из Azure][L02]

## <a name="next-steps"></a>Дальнейшие действия

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
