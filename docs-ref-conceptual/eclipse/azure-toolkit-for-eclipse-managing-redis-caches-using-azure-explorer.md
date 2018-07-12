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
ms.openlocfilehash: 2d3f2363bd0b41808cd409417327b924cb86d85b
ms.sourcegitcommit: 0ed7c5af0152125322ff1d265c179f35028f3c15
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2018
ms.locfileid: "38075423"
---
# <a name="managing-redis-caches-using-the-azure-explorer-for-eclipse"></a><span data-ttu-id="670e2-103">Управление кэшами Redis с помощью Azure Explorer для Eclipse</span><span class="sxs-lookup"><span data-stu-id="670e2-103">Managing Redis Caches using the Azure Explorer for Eclipse</span></span>

<span data-ttu-id="670e2-104">Обозреватель Azure Explorer, входящий в состав набора средств Azure для Eclipse, предоставляет разработчикам Java удобное решение для управления кэшами Redis в учетной записи Azure из интегрированной среды разработки Eclipse.</span><span class="sxs-lookup"><span data-stu-id="670e2-104">The Azure Explorer, which is part of the Azure Toolkit for Eclipse, provides Java developers with an easy-to-use solution for managing redis caches in their Azure account from inside the Eclipse IDE.</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-eclipse-show-azure-explorer](../includes/azure-toolkit-for-eclipse-show-azure-explorer.md)]

## <a name="create-a-redis-cache-by-using-eclipse"></a><span data-ttu-id="670e2-105">Создание кэша Redis с помощью Eclipse</span><span class="sxs-lookup"><span data-stu-id="670e2-105">Create a Redis Cache by using Eclipse</span></span>

<span data-ttu-id="670e2-106">Приведенные ниже пошаговые инструкции помогут вам создать кэш Redis с использованием Azure Explorer.</span><span class="sxs-lookup"><span data-stu-id="670e2-106">The following steps walk you through the steps to create a redis cache using the Azure Explorer.</span></span>

1. <span data-ttu-id="670e2-107">Войдите в свою учетную запись Azure, следуя [инструкциям по входу для набора средств Azure для Eclipse].</span><span class="sxs-lookup"><span data-stu-id="670e2-107">Sign in to your Azure account using the steps in the [Sign In Instructions for the Azure Toolkit for Eclipse] article.</span></span>

1. <span data-ttu-id="670e2-108">В окне средства **Azure Explorer** разверните узел **Azure**, щелкните правой кнопкой мыши элемент **Кэши Redis** и выберите пункт **Create Redis Cache** (Создать кэш Redis).</span><span class="sxs-lookup"><span data-stu-id="670e2-108">In the **Azure Explorer** tool window, expand the **Azure** node, right-click **Redis Caches**, and then click **Create Redis Cache**.</span></span>

   ![Меню создания кэша Redis][CR01]

1. <span data-ttu-id="670e2-110">Когда отобразится диалоговое окно **Новый кэш Redis**, укажите значения для следующих параметров:</span><span class="sxs-lookup"><span data-stu-id="670e2-110">When the **New Redis Cache** dialog box appears, specify the following options:</span></span>

   ![Диалоговое окно создания кэша Redis][CR02]

   <span data-ttu-id="670e2-112">a.</span><span class="sxs-lookup"><span data-stu-id="670e2-112">a.</span></span> <span data-ttu-id="670e2-113">**DNS-имя**: определяет поддомен DNS для нового кэша Redis, который добавляется перед адресом redis.cache.windows.net, например: *wingtiptoys.redis.cache.windows.net*.</span><span class="sxs-lookup"><span data-stu-id="670e2-113">**DNS Name**: Specifies the DNS subdomain for the new redis cache, which is prepended to ".redis.cache.windows.net"; for example: *wingtiptoys.redis.cache.windows.net*.</span></span>

   <span data-ttu-id="670e2-114">Б.</span><span class="sxs-lookup"><span data-stu-id="670e2-114">b.</span></span> <span data-ttu-id="670e2-115">**Подписка**: указывает подписку Azure, которую нужно использовать для нового кэша Redis.</span><span class="sxs-lookup"><span data-stu-id="670e2-115">**Subscription**: Specifies the Azure subscription you want to use for the new redis cache.</span></span>

   <span data-ttu-id="670e2-116">c.</span><span class="sxs-lookup"><span data-stu-id="670e2-116">c.</span></span> <span data-ttu-id="670e2-117">**Группа ресурсов**: указывает группу ресурсов для кэша Redis. Нужно выбрать один из следующих параметров:</span><span class="sxs-lookup"><span data-stu-id="670e2-117">**Resource Group**: Specifies the resource group for your redis cache; you need to choose one of the following options:</span></span>
      * <span data-ttu-id="670e2-118">**Создать**: указывает, что нужно создать группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="670e2-118">**Create New**: Specifies that you want to create a new resource group.</span></span>
      * <span data-ttu-id="670e2-119">**Использовать существующую**: указывает, что будет выбрана группа ресурсов, связанная с учетной записью Azure.</span><span class="sxs-lookup"><span data-stu-id="670e2-119">**Use Existing**: Specifies that you will choose from a list of resource groups associated with your Azure account.</span></span>

   <span data-ttu-id="670e2-120">d.</span><span class="sxs-lookup"><span data-stu-id="670e2-120">d.</span></span> <span data-ttu-id="670e2-121">**Расположение**: указывает расположение, в котором создается кэш Redis (например, *западная часть США*).</span><span class="sxs-lookup"><span data-stu-id="670e2-121">**Location**: Specifies the location where your redis cache is created; for example, *West US*.</span></span>

   <span data-ttu-id="670e2-122">д.</span><span class="sxs-lookup"><span data-stu-id="670e2-122">e.</span></span> <span data-ttu-id="670e2-123">**Ценовая категория**: указывает ценовую категорию для кэша Redis. Этот параметр ограничивает количество клиентских подключений.</span><span class="sxs-lookup"><span data-stu-id="670e2-123">**Pricing Tier**: Specifies which pricing tier your redis cache uses; this setting determines the number of client connections.</span></span> <span data-ttu-id="670e2-124">(Дополнительные сведения см. на [странице с ценами на кэш Redis].)</span><span class="sxs-lookup"><span data-stu-id="670e2-124">(For more information, see [Redis Cache Pricing].)</span></span>

   <span data-ttu-id="670e2-125">f.</span><span class="sxs-lookup"><span data-stu-id="670e2-125">f.</span></span> <span data-ttu-id="670e2-126">**Порт без SSL**: указывает, разрешает ли кэш Redis подключения без использования SSL. По умолчанию разрешены только SSL-подключения.</span><span class="sxs-lookup"><span data-stu-id="670e2-126">**Non-SSL port**: Specifies whether your redis cache allows non-SSL connections; by default, only SSL connections are allowed.</span></span>

1. <span data-ttu-id="670e2-127">Когда вы введете значения для всех параметров кэша Redis, нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="670e2-127">When you have specified all your redis cache settings, click **OK**.</span></span>

<span data-ttu-id="670e2-128">После создания кэш Redis отобразится в Azure Explorer.</span><span class="sxs-lookup"><span data-stu-id="670e2-128">After your redis cache has been created, it will be displayed in the Azure Explorer.</span></span>

   ![Кэш Redis в Azure Explorer][CR03]

> [!NOTE]
>
> <span data-ttu-id="670e2-130">Дополнительные сведения о настройке кэша Redis для Azure см. в статье [Настройка кэша Redis для Azure].</span><span class="sxs-lookup"><span data-stu-id="670e2-130">For more information about configuring your Azure redis cache settings, see [How to configure Azure Redis Cache].</span></span>
>

## <a name="display-the-properties-for-your-redis-cache-in-eclipse"></a><span data-ttu-id="670e2-131">Отображение свойств кэша Redis в Eclipse</span><span class="sxs-lookup"><span data-stu-id="670e2-131">Display the properties for your Redis Cache in Eclipse</span></span>

1. <span data-ttu-id="670e2-132">В Azure Explorer щелкните правой кнопкой мыши кэш Redis и выберите пункт **Показать свойства**.</span><span class="sxs-lookup"><span data-stu-id="670e2-132">In the Azure Explorer, right-click your redis cache and click **Show properties**.</span></span>

   ![Контекстное меню Azure Explorer для отображения свойств кэша Redis][SP01]

1. <span data-ttu-id="670e2-134">В Azure Explorer отобразятся свойства кэша Redis.</span><span class="sxs-lookup"><span data-stu-id="670e2-134">The Azure Explorer displays the properties for your redis cache.</span></span>

   ![Свойства кэша Redis][SP02]

## <a name="delete-your-redis-cache-by-using-eclipse"></a><span data-ttu-id="670e2-136">Удаление кэша Redis с помощью Eclipse</span><span class="sxs-lookup"><span data-stu-id="670e2-136">Delete your Redis Cache by using Eclipse</span></span>

1. <span data-ttu-id="670e2-137">В Azure Explorer щелкните правой кнопкой мыши кэш Redis и выберите пункт **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="670e2-137">In the Azure Explorer, right-click your redis cache and click **Delete**.</span></span>

   ![Контекстное меню Azure Explorer для удаления кэша Redis][DE01]

1. <span data-ttu-id="670e2-139">Когда появится запрос на подтверждение, щелкните **Да**, чтобы удалить кэш Redis.</span><span class="sxs-lookup"><span data-stu-id="670e2-139">Click **OK** when prompted to delete your redis cache.</span></span>

   ![Запрос на удаление кэша Redis][DE02]

## <a name="next-steps"></a><span data-ttu-id="670e2-141">Дополнительная информация</span><span class="sxs-lookup"><span data-stu-id="670e2-141">Next steps</span></span>

<span data-ttu-id="670e2-142">Дополнительные сведения о кэшах Redis для Azure, параметрах конфигурации и ценах см. по следующим ссылкам:</span><span class="sxs-lookup"><span data-stu-id="670e2-142">For more information about Azure redis caches, configuration settings and pricing, see the following links:</span></span>

* <span data-ttu-id="670e2-143">[кэш Azure Redis]</span><span class="sxs-lookup"><span data-stu-id="670e2-143">[Azure Redis Cache]</span></span>
* <span data-ttu-id="670e2-144">[Документация по кэшу Redis]</span><span class="sxs-lookup"><span data-stu-id="670e2-144">[Redis Cache Documentation]</span></span>
* <span data-ttu-id="670e2-145">[странице с ценами на кэш Redis]</span><span class="sxs-lookup"><span data-stu-id="670e2-145">[Redis Cache Pricing]</span></span>
* <span data-ttu-id="670e2-146">[Настройка кэша Redis для Azure]</span><span class="sxs-lookup"><span data-stu-id="670e2-146">[How to configure Azure Redis Cache]</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-additional-resources](../includes/azure-toolkit-for-eclipse-additional-resources.md)]

<!-- URL List -->

[странице с ценами на кэш Redis]: https://azure.microsoft.com/pricing/details/cache/
[Redis Cache Pricing]: https://azure.microsoft.com/pricing/details/cache/
[кэш Azure Redis]: https://azure.microsoft.com/services/cache/
[Azure Redis Cache]: https://azure.microsoft.com/services/cache/
[Документация по кэшу Redis]: /azure/redis-cache/
[Redis Cache Documentation]: /azure/redis-cache/
[Настройка кэша Redis для Azure]: /azure/redis-cache/cache-configure
[How to configure Azure Redis Cache]: /azure/redis-cache/cache-configure

<!-- IMG List -->

[CR01]: media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/CR01.png
[CR02]: media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/CR02.png
[CR03]: media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/CR03.png

[SP01]: media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/SP01.png
[SP02]: media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/SP02.png

[DE01]: media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/DE01.png
[DE02]: media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/DE02.png
