---
title: "Управление кэшами Redis с помощью Azure Explorer для IntelliJ"
description: "Узнайте, как управлять кэшами Redis Azure с помощью Azure Explorer для IntelliJ."
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
ms.date: 10/19/2017
ms.author: robmcm
ms.openlocfilehash: 6d7a28bb98c945f9471a590681514c128f567b3f
ms.sourcegitcommit: 7f8538e41c833deb69c300ad3431a431136a1f3e
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/24/2017
---
# <a name="managing-redis-caches-using-the-azure-explorer-for-intellij"></a>Управление кэшами Redis с помощью Azure Explorer для IntelliJ

Azure Explorer, входящий в состав набора средств Azure для IntelliJ, предоставляет разработчикам на Java удобное решение для управления кэшами Redis в их учетной записи Azure из интегрированной среды разработки IntelliJ.

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-intellij-show-azure-explorer](../includes/azure-toolkit-for-intellij-show-azure-explorer.md)]

## <a name="create-a-redis-cache-by-using-intellij"></a>Создание кэша Redis с помощью IntelliJ

Приведенные ниже инструкции помогут вам поэтапно создать кэш Redis с использованием Azure Explorer.

1. Войдите в свою учетную запись Azure, следуя инструкциям из статьи [Инструкции по входу для набора средств Azure для IntelliJ].

1. В окне средства **Azure Explorer** разверните узел **Azure**, щелкните правой кнопкой мыши элемент **Кэши Redis** и выберите **Create Redis Cache** (Создать кэш Redis).

   ![Меню создания кэша Redis][CR01]

1. Когда отобразится диалоговое окно **New Redis Cache** (Новый кэш Redis), укажите значения для параметров ниже.

   ![Диалоговое окно New Redis Cache (Новый кэш Redis)][CR02]

   а. **DNS-имя**: определяет поддомен DNS для нового кэша Redis, который добавляется в начало redis.cache.windows.net, например: *wingtiptoys.redis.cache.windows.net*.

   b. **Подписка**: указывает подписку Azure, которую нужно использовать для нового кэша Redis.

   c. **Группа ресурсов**: указывает группу ресурсов для кэша Redis. Нужно выбрать один из следующих параметров: 
      * **Создать**: указывает, что нужно создать группу ресурсов. 
      * **Использовать существующую**: указывает, что будет выбрана группа ресурсов, связанная с учетной записью Azure. 

   d. **Расположение**: указывает расположение, в котором создается кэш Redis (например, *западная часть США*).

   д. **Ценовая категория**: указывает ценовую категорию для кэша Redis. Этот параметр ограничивает количество клиентских подключений. (Дополнительные сведения см. на [странице с ценами на кэш Redis].)

   f. **Порт без SSL**: указывает, разрешает ли кэш Redis подключения без использования SSL. По умолчанию разрешены только SSL-подключения.

1. Когда вы введете значения для всех параметров кэша Redis, нажмите кнопку **ОК**.

После создания кэш Redis отобразится в Azure Explorer.

   ![Кэш Redis в Azure Explorer][CR03]

> [!NOTE]
>
> Дополнительные сведения о настройке кэша Redis для Azure см. в статье [Настройка кэша Redis для Azure].
>

## <a name="display-the-properties-for-your-redis-cache-in-intellij"></a>Отображение свойств для кэша Redis в IntelliJ

1. В обозревателе Azure щелкните правой кнопкой мыши кэш Redis и выберите **Показать свойства**.

   ![Контекстное меню Azure Explorer для отображения свойств кэша Redis][SP01]

1. В Azure Explorer отобразятся свойства кэша Redis.

   ![Свойства кэша Redis][SP02]

## <a name="delete-your-redis-cache-by-using-intellij"></a>Удаление кэша Redis с помощью IntelliJ

1. В обозревателе Azure щелкните правой кнопкой мыши кэш Redis и выберите **Удалить**.

   ![Контекстное меню обозревателя Azure для удаления кэша Redis][DE01]

1. При появлении запроса выберите **Да**, чтобы удалить кэш Redis.

   ![Запрос на удаление кэша Redis][DE02]

## <a name="next-steps"></a>Дальнейшие действия

Дополнительные сведения о кэшах Redis для Azure, параметрах конфигурации и ценах см. по следующим ссылкам:

* [кэш Azure Redis]
* [Документация по кэшу Redis]
* [странице с ценами на кэш Redis]
* [Настройка кэша Redis для Azure]

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

<!-- URL List -->

[странице с ценами на кэш Redis]: https://azure.microsoft.com/pricing/details/cache/
[кэш Azure Redis]: https://azure.microsoft.com/services/cache/
[Документация по кэшу Redis]: /azure/redis-cache
[Настройка кэша Redis для Azure]: /azure/redis-cache/cache-configure
[Инструкции по входу для набора средств Azure для IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md

<!-- IMG List -->

[CR01]: media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/CR01.png
[CR02]: media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/CR02.png
[CR03]: media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/CR03.png

[SP01]: media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/SP01.png
[SP02]: media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/SP02.png

[DE01]: media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/DE01.png
[DE02]: media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/DE02.png
