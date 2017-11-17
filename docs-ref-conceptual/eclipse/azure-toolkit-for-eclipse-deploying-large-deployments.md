---
title: "Развертывание крупных систем"
description: "Узнайте о развертывании крупных систем с помощью набора средств Azure для Eclipse."
services: 
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
ms.assetid: 5e18bace-5df0-4af8-ad86-6151ea8bd823
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 09/11/2017
ms.author: robmcm
ms.openlocfilehash: 0e367e74d038043f1626dbf19aab87db6451bc02
ms.sourcegitcommit: 256044d7cbce16dcb8dc4e195d0f63c10cb44d4e
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/13/2017
---
# <a name="deploying-large-deployments"></a><span data-ttu-id="5ff49-103">Развертывание крупных систем</span><span class="sxs-lookup"><span data-stu-id="5ff49-103">Deploying Large Deployments</span></span>

<span data-ttu-id="5ff49-104">В случае если развертывание слишком велико для размещения в корневом каталоге приложения, вы можете использовать локальный ресурс хранилища в качестве корневой папки для своего JDK и сервера приложений.</span><span class="sxs-lookup"><span data-stu-id="5ff49-104">If your deployment is too large to be contained in the default approot folder, you can use a local storage resource as the deployment root folder for your JDK and application server.</span></span>

## <a name="to-use-a-local-storage-resource-as-the-deployment-root-folder-for-large-deployments"></a><span data-ttu-id="5ff49-105">Использование локального ресурса хранилища в качестве корневой папки развертывания для крупных развертываний</span><span class="sxs-lookup"><span data-stu-id="5ff49-105">To use a local storage resource as the deployment root folder for large deployments</span></span>

1. <span data-ttu-id="5ff49-106">Создайте новый локальный ресурс хранилища.</span><span class="sxs-lookup"><span data-stu-id="5ff49-106">Create a new local storage resource.</span></span> <span data-ttu-id="5ff49-107">Имя ресурса значения не имеет.</span><span class="sxs-lookup"><span data-stu-id="5ff49-107">The name of the resource does not matter.</span></span> <span data-ttu-id="5ff49-108">Ресурсы хранилища определяются на уровне роли.</span><span class="sxs-lookup"><span data-stu-id="5ff49-108">Storage resources are defined at the role level.</span></span> <span data-ttu-id="5ff49-109">Быстрее всего получить доступ к диалоговому окну настройки локального хранилища, из которого вы можете создать новый локальный ресурс хранилища, можно, сделав следующее: щелкните правой кнопкой мыши роль в представлении **Обозреватель проектов** (разверните узел проекта Azure, если вы не видите роль), выберите **Azure** и **Локальное хранилище**.</span><span class="sxs-lookup"><span data-stu-id="5ff49-109">The quickest way to access the local storage configuration dialog, from which you could create a new local storage resource, is by using the following steps: Right-click the role in the **Project Explorer** view (expand your Azure project node if you don't see the role), click **Azure**, and then click **Local Storage**.</span></span> <span data-ttu-id="5ff49-110">В диалоговом окне **Локальное хранилище** нажмите кнопку **Добавить**, чтобы создать локальный ресурс хранилища.</span><span class="sxs-lookup"><span data-stu-id="5ff49-110">Within the **Local Storage** dialog, click **Add** to create a new local storage resource.</span></span>

1. <span data-ttu-id="5ff49-111">Установите желаемый размер не менее 2048 МБ (меньшее значение может привести к тем же проблемам с размером файлов, что и в корневом каталоге приложения).</span><span class="sxs-lookup"><span data-stu-id="5ff49-111">Set the desired size to at least 2048 MB (anything less may cause the same file size problems as you would encounter in the approot).</span></span>

1. <span data-ttu-id="5ff49-112">Установите флажок **Clean the contents when the role instance is recycled** (Очищать содержимое при перезапуске экземпляра роли). Это поможет предотвратить конфликты логики запуска развертывания с имеющимися файлами в ресурсе при перезапуске экземпляра роли.</span><span class="sxs-lookup"><span data-stu-id="5ff49-112">Ensure that **Clean the contents when the role instance is recycled** is checked; this will help prevent the deployment's startup logic from running into conflicts with pre-existing files in the resource when the role instance is recycled.</span></span>

1. <span data-ttu-id="5ff49-113">Для значения **Environment variable storing the resource's directory path after deployment** (Переменная среды, хранящая путь к каталогу ресурса после развертывания) задайте строку **DEPLOYROOT**.</span><span class="sxs-lookup"><span data-stu-id="5ff49-113">Ensure that the **Environment variable storing the resource's directory path after deployment** value is set to the string **DEPLOYROOT**.</span></span> <span data-ttu-id="5ff49-114">Диалоговое окно локального ресурса хранилища будет выглядеть следующим образом.</span><span class="sxs-lookup"><span data-stu-id="5ff49-114">Your local storage resource dialog will look similar to the following.</span></span>

   ![][ic667943]

<span data-ttu-id="5ff49-115">Кроме того, если вы используете **DEPLOYROOT** в качестве *имени* локального ресурса и не изменяете автоматически созданное имя переменной среды (в данном случае это **DEPLOYROOT_PATH**), этот вариант также подойдет для вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="5ff49-115">Alternatively, if you use **DEPLOYROOT** as the *name* of your local resource and you do not change the automatically-generated environment variable name (which will be set to **DEPLOYROOT_PATH** in that case), that would work for your application as well.</span></span>

<span data-ttu-id="5ff49-116">Дополнительные сведения о создании локального ресурса хранилища вы можете найти в статье [Свойства локального хранилища][Local storage properties].</span><span class="sxs-lookup"><span data-stu-id="5ff49-116">Additional information about creating a local storage resource can be found at [Local storage properties][Local storage properties].</span></span>

## <a name="next-steps"></a><span data-ttu-id="5ff49-117">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5ff49-117">Next steps</span></span>

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing the Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546
[Local storage properties]: http://go.microsoft.com/fwlink/?LinkID=699525#local_storage_properties

<!-- IMG List -->

[ic667943]: media/azure-toolkit-for-eclipse-deploying-large-deployments/ic667943.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/dn268601.aspx -->
