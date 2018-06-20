---
title: Управление учетными записями хранения с помощью Azure Explorer для IntelliJ
description: Вы можете узнать, как управлять учетными записями хранения Azure с помощью Azure Explorer для IntelliJ.
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
ms.openlocfilehash: 4edb8c1ceef508dd251db693ccc3b98d77ec452b
ms.sourcegitcommit: 151aaa6ccc64d94ed67f03e846bab953bde15b4a
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/03/2018
ms.locfileid: "28954845"
---
# <a name="manage-storage-accounts-by-using-the-azure-explorer-for-intellij"></a>Управление учетными записями хранения с помощью Azure Explorer для IntelliJ

Azure Explorer, входящий в состав набора средств Azure для IntelliJ, предоставляет разработчикам на Java удобное решение для управления учетными записями хранения в их учетной записи Azure из интегрированной среды разработки IntelliJ.

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-intellij-show-azure-explorer](../includes/azure-toolkit-for-intellij-show-azure-explorer.md)]

## <a name="create-a-storage-account-in-intellij"></a>Создание учетной записи хранения в IntelliJ

Чтобы создать учетную запись хранения с помощью Azure Explorer, сделайте следующее:

1. Войдите в свою учетную запись Azure, следуя [Инструкции по входу для набора средств Azure для IntelliJ]. 

2. В представлении **Azure Explorer** разверните узел **Azure**, щелкните правой кнопкой мыши элемент **Учетные записи хранения** и выберите **Создать учетную запись хранения**.

   ![Команда "Создать учетную запись хранения"][CS01]

3. В диалоговом окне **Создание учетной записи хранения** укажите следующие параметры.

   ![Диалоговое окно "Создание учетной записи хранения"][CS02]

   * **Имя**: указывает имя для новой учетной записи хранения.

   * **Тип учетной записи**: указывает тип создаваемой учетной записи хранения (например, "хранилище BLOB-объектов"). Дополнительные сведения см. в статье [Об учетных записях хранения Azure]. 

   * **Производительность**: определяет, какое предложение по учетной записи хранения выбранного издателя нужно использовать (например, "Премиум"). Дополнительные сведения см. в статье [Целевые показатели масштабируемости и производительности службы хранилища Azure]. 

   * **Репликация**: указывает репликацию для учетной записи хранения (например, "избыточная в пределах зоны"). Дополнительные сведения см. в статье [Репликация службы хранилища Azure]. 

   * **Подписка**: указывает подписку Azure, которую нужно использовать для новой учетной записи хранения.

   * **Расположение**: указывает расположение для создания учетной записи хранения (например, "западная часть США").

   * **Группа ресурсов**: указывает группу ресурсов для виртуальной машины. Выберите один из следующих вариантов:
      * **Создать**: указывает, что нужно создать группу ресурсов.
      * **Использовать существующий**: указывает, что вы выберете группу ресурсов, связанную с учетной записью Azure.

4. Указав все перечисленные выше параметры, нажмите кнопку **ОК**.

## <a name="create-a-storage-container-in-intellij"></a>Создание контейнера хранилища в IntelliJ

Чтобы создать контейнер хранилища с помощью Azure Explorer, сделайте следующее:

1. В представлении Azure Explorer щелкните правой кнопкой мыши учетную запись хранения, для которой нужно создать контейнер, а затем нажмите кнопку **Create blob container** (Создать контейнер BLOB-объектов).

   ![Команда Create blob container (Создать контейнер BLOB-объектов)][CC01]

2. В диалоговом окне **Создание контейнера BLOB-объектов** укажите имя для своего контейнера и нажмите кнопку **ОК**. Дополнительные сведения об именовании контейнеров хранилища см. в статье [Naming and Referencing Containers, Blobs, and Metadata] (Именование контейнеров, больших двоичных объектов и метаданных и ссылка на них).

   ![Диалоговое окно Create Storage Container (Создание контейнера хранилища)][CC02]

## <a name="delete-a-storage-container-in-intellij"></a>Удаление контейнера хранилища в IntelliJ

Чтобы удалить контейнер хранилища с помощью Azure Explorer, сделайте следующее:

1. В представлении Azure Explorer щелкните правой кнопкой мыши контейнер хранилища и выберите **Удалить**.

   ![Команда Delete storage container (Удаление контейнера хранилища)][DC01]

2. В диалоговом окне подтверждения нажмите кнопку **Да**.

   ![Окно подтверждения удаления контейнера хранилища][DC02]

## <a name="delete-a-storage-account-in-intellij"></a>Удаление учетной записи хранения в IntelliJ

Чтобы удалить учетную запись хранения с помощью Azure Explorer, сделайте следующее:

1. В представлении **Azure Explorer** щелкните правой кнопкой мыши учетную запись хранения и выберите пункт **Удалить**.

   ![Меню "Удаление учетной записи хранения"][DS01]

2. В диалоговом окне подтверждения нажмите кнопку **Да**.

   ![Окно подтверждения удаления учетной записи хранения][DS02]

## <a name="next-steps"></a>Дополнительная информация

Дополнительные сведения об учетных записях хранения, размерах и ценах см. в следующих ресурсах:

* [Введение в службу хранилища Microsoft Azure]
* [Об учетных записях хранения Azure]
* Размеры учетных записей хранения Azure
  * [Размеры учетных записей хранения Windows в Azure]
  * [Размеры учетных записей хранения Linux в Azure]
* Цены на учетные записи хранения Azure
  * [Windows storage-account pricing] (Цены на учетные записи хранения Windows)
  * [Linux storage-account pricing] (Цены на учетные записи хранения Linux)

[!INCLUDE [azure-toolkit-for-intellij-additional-resources](../includes/azure-toolkit-for-intellij-additional-resources.md)]

<!-- URL List -->

[Инструкции по входу для набора средств Azure для IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Введение в службу хранилища Microsoft Azure]: /azure/storage/storage-introduction
[Об учетных записях хранения Azure]: /azure/storage/storage-create-storage-account
[Репликация службы хранилища Azure]: /azure/storage/storage-redundancy
[Целевые показатели масштабируемости и производительности службы хранилища Azure]: /azure/storage/storage-scalability-targets
[Naming and Referencing Containers, Blobs, and Metadata]: http://go.microsoft.com/fwlink/?LinkId=255555 (Именование контейнеров, больших двоичных объектов и метаданных и ссылка на них)

[Размеры учетных записей хранения Windows в Azure]: /azure/virtual-machines/virtual-machines-windows-sizes
[Размеры учетных записей хранения Linux в Azure]: /azure/virtual-machines/virtual-machines-linux-sizes
[Windows storage-account pricing]: /pricing/details/virtual-machines/windows/ (Цены на учетные записи хранения Windows)
[Linux storage-account pricing]: /pricing/details/virtual-machines/linux/ (Цены на учетные записи хранения Linux)

<!-- IMG List -->

[CS01]: media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/CS01.png
[CS02]: media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/CS02.png
[CC01]: media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/CC01.png
[CC02]: media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/CC02.png

[DS01]: media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/DS01.png
[DS02]: media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/DS02.png
[DC01]: media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/DC01.png
[DC02]: media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/DC02.png
