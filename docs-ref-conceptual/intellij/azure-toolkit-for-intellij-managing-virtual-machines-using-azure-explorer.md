---
title: Управление виртуальными машинами с помощью Azure Explorer для IntelliJ
description: Вы можете узнать, как управлять виртуальными машинами Azure с помощью Azure Explorer для IntelliJ.
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
ms.openlocfilehash: 213efa7fc31705b0ffcba6f2fe40e7186a365fae
ms.sourcegitcommit: b64017f119177f97da7a5930489874e67b09c0fc
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/09/2018
ms.locfileid: "48893525"
---
# <a name="manage-virtual-machines-by-using-the-azure-explorer-for-intellij"></a>Управление виртуальными машинами с помощью Azure Explorer для IntelliJ

Azure Explorer, входящий в состав набора средств Azure для IntelliJ, предоставляет разработчикам на Java удобное решение для управления виртуальными машинами в их учетной записи Azure из интегрированной среды разработки IntelliJ.

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-intellij-show-azure-explorer](../includes/azure-toolkit-for-intellij-show-azure-explorer.md)]

## <a name="create-a-virtual-machine-in-intellij"></a>Создание виртуальной машины в IntelliJ

Чтобы создать виртуальную машину с помощью Azure Explorer, сделайте следующее: 

1. Войдите в свою учетную запись Azure, следуя инструкциям из статьи [Инструкции по входу для набора средств Azure для IntelliJ].

2. В представлении **Azure Explorer** разверните узел **Azure**, щелкните правой кнопкой мыши **Виртуальные машины** и выберите **Создать виртуальную машину**. 

   ![Команда "Создать виртуальную машину"][CR01]  
    Откроется мастер **создания виртуальной машины**.

3. В диалоговом окне **Выбор подписки** выберите подписку и нажмите кнопку **Далее**. 

   ![Диалоговое окно "Выбор подписки"][CR02]

4. В диалоговом окне **Выбор образа виртуальной машины** введите следующие значения.

   * **Расположение**: указывает расположение для создания виртуальной машины (например, *Западная часть США*). 

   * **Recommended Image** (Рекомендуемый образ): указывает, что вы выберете образ из сокращенного списка часто используемых образов.

   * **Пользовательский образ**: указывает, что вы выберете пользовательский образ, указав следующие сведения:

      * **Издатель**: указывает издателя, создавшего образ, который будет использоваться для виртуальной машины (например, *Майкрософт*).

      * **Предложение**: определяет предложение виртуальной машины выбранного издателя (например, *JDK*).

      * **SKU**: указывает нужный номер SKU из выбранного предложения (например, *JDK_8*).

      * **Номер версии**: указывает, какую версию из выбранного номера SKU нужно использовать.

   ![Диалоговое окно "Выбор образа виртуальной машины"][CR03]

5. Щелкните **Далее**. 

6. В диалоговом окне **Основные параметры виртуальной машины** введите следующие значения.

   * **Имя виртуальной машины**: указывает имя новой виртуальной машины, которое должно начинаться с буквы и содержать только буквы, цифры и дефисы.

   * **Размер**: указывает количество ядер и объем памяти, выделяемые для виртуальной машины.

   * **Имя пользователя**: указывает учетную запись администратора, создаваемую для управления виртуальной машиной.

   * **Пароль** и **Подтверждение**: указывают пароль для учетной записи администратора.

   ![Диалоговое окно "Основные параметры виртуальной машины"][CR04]

7. Щелкните **Далее**. 

8. В диалоговом окне **Связанные ресурсы** введите следующие значения.

   * **Группа ресурсов**: указывает группу ресурсов для виртуальной машины. Выберите один из следующих вариантов:
      * **Создать**: определяет, что нужно создать группу ресурсов.
      * **Использовать существующий**: указывает, что нужно выбрать группу ресурсов, связанную с учетной записью Azure.

       ![Диалоговое окно "Связанные ресурсы"][CR07]

   * **Учетная запись хранения**: указывает учетную запись хранения, используемую для хранения виртуальной машины. Вы можете выбрать имеющуюся учетную запись хранения или создать ее. При выборе элемента **Создать** отображается следующее диалоговое окно.

      ![Диалоговое окно "Создание учетной записи хранения"][CR05]

   * **Виртуальная сеть** и **Подсеть**: указывают виртуальную сеть и подсеть, к которым будет подключена виртуальная машина. Вы можете выбрать имеющуюся сеть и подсеть или создать их. При выборе элемента **Создать** отображается следующее диалоговое окно.

      ![Диалоговое окно "Создание виртуальной сети"][CR06]

   * **Общедоступный IP-адрес**: указывает внешний IP-адрес для виртуальной машины. Вы можете создать IP-адрес или выбрать значение **(Нет)**, если у виртуальной машины не будет общедоступного IP-адреса. 

   * **Группа безопасности сети**: определяет необязательный брандмауэр для виртуальной машины. Вы можете выбрать имеющийся брандмауэр или задать значение **(Нет)**, чтобы не использовать брандмауэр. 

   * **Группа доступности**: указывает необязательную группу доступности, в которую может входить виртуальная машина. Вы можете выбрать имеющуюся группу доступности, создать ее или задать значение **(Нет)**, если виртуальная машина не будет входить в группу доступности.

9. Нажмите кнопку **Готово**  
    Новая виртуальная машина отобразится в окне средства Azure Explorer. 

   ![Новая виртуальная машина в представлении Azure Explorer][CR08]

## <a name="restart-a-virtual-machine-in-intellij"></a>Перезапуск виртуальной машины в IntelliJ

Чтобы перезапустить виртуальную машину с помощью Azure Explorer в IntelliJ, сделайте следующее:

1. В представлении **Azure Explorer** щелкните правой кнопкой мыши виртуальную машину и выберите **Перезапустить**.

   ![Команда перезапуска виртуальной машины][RE01]

2. В диалоговом окне подтверждения нажмите кнопку **Да**. 

   ![Диалоговое окно подтверждения перезапуска виртуальной машины][RE02]

## <a name="shut-down-a-virtual-machine-in-intellij"></a>Завершение работы виртуальной машины в IntelliJ

Чтобы завершить работу виртуальной машины с помощью Azure Explorer в IntelliJ, сделайте следующее:

1. В представлении **Azure Explorer** щелкните правой кнопкой мыши виртуальную машину и выберите **Завершить работу**.

   ![Команда завершения работы виртуальной машины][SH01]

2. В диалоговом окне подтверждения нажмите кнопку **Да**. 

   ![Диалоговое окно подтверждения завершения работы виртуальной машины][SH02]

## <a name="delete-a-virtual-machine-in-intellij"></a>Удаление виртуальной машины в IntelliJ

Чтобы удалить виртуальную машину с помощью Azure Explorer в IntelliJ, сделайте следующее:

1. В представлении **Azure Explorer** щелкните правой кнопкой мыши виртуальную машину и выберите **Удалить**.

   ![Команда удаления виртуальной машины][DE01]

2. В диалоговом окне подтверждения нажмите кнопку **Да**. 

   ![Диалоговое окно подтверждения удаления виртуальной машины][DE02]

## <a name="next-steps"></a>Дополнительная информация

Дополнительные сведения о размерах виртуальных машин Azure и ценах на них см. в следующих ресурсах:

* Размеры виртуальных машин Azure
  * [Размеры виртуальных машин Windows в Azure]
  * [Размеры виртуальных машин Linux в Azure]
* Цены на виртуальные машины Azure
  * [Цены на виртуальные машины Windows]
  * [Цены на виртуальные машины Linux]

[!INCLUDE [azure-toolkit-for-intellij-additional-resources](../includes/azure-toolkit-for-intellij-additional-resources.md)]

<!-- URL List -->

[Инструкции по входу для набора средств Azure для IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Размеры виртуальных машин Windows в Azure]: /azure/virtual-machines/virtual-machines-windows-sizes
[Размеры виртуальных машин Linux в Azure]: /azure/virtual-machines/virtual-machines-linux-sizes
[Цены на виртуальные машины Windows]: /pricing/details/virtual-machines/windows/
[Цены на виртуальные машины Linux]: /pricing/details/virtual-machines/linux/

<!-- IMG List -->

[RE01]: media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/RE01.png
[RE02]: media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/RE02.png

[SH01]: media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/SH01.png
[SH02]: media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/SH02.png

[DE01]: media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/DE01.png
[DE02]: media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/DE02.png

[CR01]: media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR01.png
[CR02]: media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR02.png
[CR03]: media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR03.png
[CR04]: media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR04.png
[CR05]: media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR05.png
[CR06]: media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR06.png
[CR07]: media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR07.png
[CR08]: media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR08.png
