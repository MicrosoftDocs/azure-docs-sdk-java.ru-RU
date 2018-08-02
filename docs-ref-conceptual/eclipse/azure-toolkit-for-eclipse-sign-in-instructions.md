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
ms.sourcegitcommit: 8230cf6b15ac51a9f8a209e9b76411a0385029aa
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/16/2018
ms.locfileid: "34216028"
---
# <a name="azure-sign-in-instructions-for-the-azure-toolkit-for-eclipse"></a>Инструкции по входу для набора средств Azure для Eclipse

Набор средств Azure для Eclipse предоставляет два метода для входа в систему с помощью учетной записи Azure:

  * **Автоматически** — при использовании этого метода создается файл учетных данных, содержащий данные субъекта-службы, после чего этот файл можно использовать для автоматического входа в учетную запись Azure.
  * **Интерактивно** — при использовании этого метода потребуется вводить учетные данные Azure при каждом входе в учетную запись Azure.

В следующих разделах описано использование каждого из методов.

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="signing-into-your-azure-account-automatically-and-creating-a-credentials-file-to-use-in-the-future"></a>Автоматический вход в учетную запись Azure и создание файла учетных данных для использования в будущем

Описанные ниже действия помогут вам создать файл учетных данных, содержащий данные субъекта-службы. После выполнения этих шагов Eclipse использует файл учетных данных для автоматического входа в Azure при каждом открытии проекта.

1. Откройте проект с помощью Eclipse.

1. Выберите **Сервис**, **Azure** и затем **Войти**.

   ![Меню Eclipse для входа в систему Azure][A01]

1. При отображении диалогового окна **Вход в Azure** выберите **Автоматически** и щелкните **Создать**.

   ![Диалоговое окно входа][A02]

1. При отображении диалогового окна **Вход в Azure** введите учетные данные и щелкните **Войти**.

   ![Диалоговое окно входа в Azure][A03]

1. При отображении диалогового окна **Create authentication files** (Создание файлов проверки подлинности) выберите нужные подписки, конечный каталог и нажмите кнопку **Начать**.

   ![Диалоговое окно входа в Azure][A04]

1. Отображается диалоговое окно **Service Principal Creatation Status** (Состояние создания субъекта-службы). После успешного создания файлов нажмите кнопку **ОК**.

   ![Диалоговое окно состояния создания субъекта-службы][A05]

1. При отображении диалогового окна **Вход в Azure** нажмите кнопку **Войти**.

   ![Диалоговое окно входа в Azure][A06]

1. При отображении диалогового окна **Выбор подписок** выберите нужные подписки и нажмите кнопку **ОК**.

   ![Диалоговое окно выбора подписок][A07]

## <a name="signing-out-of-your-azure-account-when-you-signed-in-automatically"></a>Выход из учетной записи Azure после автоматического входа

После настройки, описанной в предыдущем разделе, набор средств Azure будет автоматически выполнять выход из вашей учетной записи Azure при каждом перезапуске Eclipse. Чтобы выйти из учетной записи Azure и предотвратить автоматический вход набора средств Azure, сделайте следующее.

1. В Eclipse выберите **Сервис**, **Azure** и затем **Выйти**.

   ![Меню Eclipse для выхода из системы Azure][L01]

1. При отображении диалогового окна **Выход из Azure** нажмите кнопку **Да**.

   ![Диалоговое окно выхода][L03]

## <a name="signing-into-your-azure-account-automatically-using-a-credentials-file-which-you-have-already-created"></a>Автоматический вход в учетную запись Azure с помощью созданного файла учетных данных

Если вы выходите из Azure во время применения Eclipse, потребуется перенастроить набор средств Azure для Eclipse, чтобы использовать созданный файл учетных данных для автоматического входа в учетную запись Azure. Указанные ниже шаги помогут настроить набор средств Azure для использования существующего файла учетных данных.

1. Откройте проект с помощью Eclipse.

1. Выберите **Сервис**, **Azure** и затем **Войти**.

   ![Меню Eclipse для входа в систему Azure][A01]

1. При отображении диалогового окна **Вход в Azure** выберите **Автоматически** и щелкните **Обзор**.

   ![Диалоговое окно входа][A02]

1. Когда откроется диалоговое окно **Select Authenticated File** (Выбор файла, прошедшего аутентификацию), выберите созданный ранее файл учетных данных и щелкните **Открыть**.

   ![Диалоговое окно входа][A08]

1. При отображении диалогового окна **Вход в Azure** нажмите кнопку **Войти**.

   ![Диалоговое окно входа в Azure][A06]

1. При отображении диалогового окна **Выбор подписок** выберите нужные подписки и нажмите кнопку **ОК**.

   ![Диалоговое окно выбора подписок][A07]

## <a name="signing-into-your-azure-account-interactively"></a>Интерактивный вход в учетную запись Azure

Ниже показано, как войти в Azure, вручную введя учетные данные Azure.

1. Откройте проект с помощью Eclipse.

1. Выберите **Сервис**, **Azure** и затем **Войти**.

   ![Меню Eclipse для входа в систему Azure][I01]

1. При отображении диалогового окна **Вход в Azure** выберите **Интерактивно** и щелкните **Войти**.

   ![Диалоговое окно входа][I02]

1. При отображении диалогового окна **Вход в Azure** введите учетные данные и щелкните **Войти**.

   ![Диалоговое окно входа в Azure][I03]

1. При отображении диалогового окна **Выбор подписок** выберите нужные подписки и нажмите кнопку **ОК**.

   ![Диалоговое окно выбора подписок][I04]

## <a name="signing-out-of-your-azure-account-when-you-signed-in-interactively"></a>Выход из учетной записи Azure после интерактивного входа

После настройки, описанной в предыдущем разделе, вы будете автоматически выходить из своей учетной записи Azure при каждом перезапуске Eclipse. Однако если вы хотите выйти из учетной записи Azure без перезапуска Eclipse, выполните указанные ниже действия.

1. В Eclipse выберите **Сервис**, **Azure** и затем **Выйти**.

   ![Меню Eclipse для выхода из системы Azure][L01]

1. При отображении диалогового окна **Выход из Azure** нажмите кнопку **Да**.

   ![Диалоговое окно выхода][L02]

## <a name="next-steps"></a>Дополнительная информация

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
