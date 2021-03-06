---
title: Управление кэшами Redis с помощью Azure Explorer для Eclipse
description: Узнайте, как управлять кэшами Redis для Azure с помощью Azure Explorer для Eclipse.
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
ms.openlocfilehash: 00f363e5dacc9c494b01eaa479db7e9e1aff6952
ms.sourcegitcommit: 4f1acf05e3bbb7eb6bca9b65300c1c5b9772185a
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/24/2019
ms.locfileid: "63456057"
---
# <a name="managing-redis-caches-using-the-azure-explorer-for-eclipse"></a>Управление кэшами Redis с помощью Azure Explorer для Eclipse

Обозреватель Azure Explorer, входящий в состав набора средств Azure для Eclipse, предоставляет разработчикам Java удобное решение для управления кэшами Redis в учетной записи Azure из интегрированной среды разработки Eclipse.

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-eclipse-show-azure-explorer](../includes/azure-toolkit-for-eclipse-show-azure-explorer.md)]

## <a name="create-a-redis-cache-by-using-eclipse"></a>Создание кэша Redis с помощью Eclipse

Приведенные ниже пошаговые инструкции помогут вам создать кэш Redis с использованием Azure Explorer.

1. Войдите в свою учетную запись Azure, следуя [инструкциям по входу для набора средств Azure для Eclipse].

1. В окне средства **Azure Explorer** разверните узел **Azure**, щелкните правой кнопкой мыши элемент **Кэши Redis** и выберите пункт **Create Redis Cache** (Создать кэш Redis).

   ![Меню создания кэша Redis][CR01]

1. Когда отобразится диалоговое окно **Новый кэш Redis**, укажите значения для следующих параметров:

   ![Диалоговое окно создания кэша Redis][CR02]

   a. **DNS-имя**. Определяет поддомен DNS для нового кэша Redis, который добавляется перед адресом redis.cache.windows.net, например *wingtiptoys.redis.cache.windows.net*.

   b. **Подписка**: Определяет подписку Azure, которую нужно использовать для нового кэша Redis.

   c. **Группа ресурсов**. Указывает группу ресурсов для кэша Redis. Нужно выбрать один из следующих параметров:
      * **Создать**. Определяет, что нужно создать группу ресурсов.
      * **Использовать существующую**. Указывает, что будет выбрана группа ресурсов, связанная с учетной записью Azure.

   d. **Расположение.** Определяет расположение, в котором создается кэш Redis (например *Западная часть США*).

   д. **Ценовая категория**. Указывает ценовую категорию для кэша Redis. Этот параметр определяет количество клиентских подключений. (Дополнительные сведения см. на [странице с ценами на кэш Redis].)

   Е. **Порт без SSL**. Указывает, разрешает ли кэш Redis подключения без использования SSL. По умолчанию разрешены только SSL-подключения.

1. Когда вы введете значения для всех параметров кэша Redis, нажмите кнопку **ОК**.

После создания кэш Redis отобразится в Azure Explorer.

   ![Кэш Redis в Azure Explorer][CR03]

> [!NOTE]
>
> Дополнительные сведения о настройке кэша Redis для Azure см. в статье [Настройка кэша Redis для Azure].
>

## <a name="display-the-properties-for-your-redis-cache-in-eclipse"></a>Отображение свойств кэша Redis в Eclipse

1. В Azure Explorer щелкните правой кнопкой мыши кэш Redis и выберите пункт **Показать свойства**.

   ![Контекстное меню Azure Explorer для отображения свойств кэша Redis][SP01]

1. В Azure Explorer отобразятся свойства кэша Redis.

   ![Свойства кэша Redis][SP02]

## <a name="delete-your-redis-cache-by-using-eclipse"></a>Удаление кэша Redis с помощью Eclipse

1. В Azure Explorer щелкните правой кнопкой мыши кэш Redis и выберите пункт **Удалить**.

   ![Контекстное меню Azure Explorer для удаления кэша Redis][DE01]

1. Когда появится запрос на подтверждение, щелкните **Да**, чтобы удалить кэш Redis.

   ![Запрос на удаление кэша Redis][DE02]

## <a name="next-steps"></a>Дополнительная информация

Дополнительные сведения о кэшах Redis для Azure, параметрах конфигурации и ценах см. по следующим ссылкам:

* [кэш Azure Redis]
* [Документация по кэшу Redis]
* [странице с ценами на кэш Redis]
* [Настройка кэша Redis для Azure]

[!INCLUDE [azure-toolkit-for-eclipse-additional-resources](../includes/azure-toolkit-for-eclipse-additional-resources.md)]

<!-- URL List -->

[странице с ценами на кэш Redis]: https://azure.microsoft.com/pricing/details/cache/
[кэш Azure Redis]: https://azure.microsoft.com/services/cache/
[Документация по кэшу Redis]: /azure/redis-cache/
[Настройка кэша Redis для Azure]: /azure/redis-cache/cache-configure

<!-- IMG List -->

[CR01]: media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/CR01.png
[CR02]: media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/CR02.png
[CR03]: media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/CR03.png

[SP01]: media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/SP01.png
[SP02]: media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/SP02.png

[DE01]: media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/DE01.png
[DE02]: media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/DE02.png
