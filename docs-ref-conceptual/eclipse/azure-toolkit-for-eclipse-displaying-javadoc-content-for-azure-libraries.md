---
title: Отображение в Eclipse содержимого Javadoc для пакета библиотек Azure для Java
description: Узнайте, как отобразить содержимое Javadoc для библиотек Azure в Eclipse.
services: ''
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: ''
ms.assetid: 30f8b6a1-1d76-4d1c-861b-1db478c46e6b
ms.author: robmcm
ms.date: 02/01/2018
ms.devlang: Java
ms.service: multiple
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: na
ms.openlocfilehash: bfed1a879bacf82436b71654c0ceca2826381eed
ms.sourcegitcommit: 115f4c8ad07a11f17d79e9d945d63917836b11c8
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "61590622"
---
# <a name="displaying-javadoc-content-in-eclipse-for-the-azure-libraries-package-for-java"></a><span data-ttu-id="e9bd5-103">Отображение в Eclipse содержимого Javadoc для пакета библиотек Azure для Java</span><span class="sxs-lookup"><span data-stu-id="e9bd5-103">Displaying Javadoc Content in Eclipse for the Azure Libraries Package for Java</span></span>

<span data-ttu-id="e9bd5-104">Содержимое Javadoc для библиотек Azure для Java можно просмотреть в среде Eclipse, сопоставив его с библиотеками Azure для Java.</span><span class="sxs-lookup"><span data-stu-id="e9bd5-104">The Javadoc content for the Azure Libraries for Java can be viewed within your Eclipse environment by associating the Javadoc content to the Azure Libraries for Java.</span></span> <span data-ttu-id="e9bd5-105">Ниже показано, как использовать эту функциональность в Eclipse.</span><span class="sxs-lookup"><span data-stu-id="e9bd5-105">The following steps show you how to use this functionality within Eclipse.</span></span>

<span data-ttu-id="e9bd5-106">В данной процедуре подразумевается, что вы уже добавили библиотеку Azure для Java в путь сборки.</span><span class="sxs-lookup"><span data-stu-id="e9bd5-106">This procedure assumes you have already added the Azure Library for Java to your build path.</span></span>

## <a name="to-display-javadoc-content-in-eclipse-for-the-azure-libraries-for-java"></a><span data-ttu-id="e9bd5-107">Порядок отображения в Eclipse содержимого Javadoc для библиотек Azure для Java</span><span class="sxs-lookup"><span data-stu-id="e9bd5-107">To display Javadoc content in Eclipse for the Azure Libraries for Java</span></span>

1. <span data-ttu-id="e9bd5-108">В разделе проекта **Referenced Libraries** (Ссылки на библиотеки) обозревателя проектов Eclipse откройте контекстное меню для JAR-файла библиотеки Azure для Java.</span><span class="sxs-lookup"><span data-stu-id="e9bd5-108">Within Eclipse's Project Explorer, in the **Referenced Libraries** section of your project, open the context menu for the Azure Library for Java JAR.</span></span> <span data-ttu-id="e9bd5-109">Например, **microsoft windowsazure-api 0.1.0.jar** (номер версии может отличаться в зависимости от установленной версии).</span><span class="sxs-lookup"><span data-stu-id="e9bd5-109">For example, **microsoft-windowsazure-api-0.1.0.jar** (the version number may be different, dependent upon which version you have installed).</span></span>

1. <span data-ttu-id="e9bd5-110">Щелкните **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="e9bd5-110">Click **Properties**.</span></span>

1. <span data-ttu-id="e9bd5-111">В левой области диалогового окна **Свойства** щелкните **Javadoc Location** (Расположение Javadoc).</span><span class="sxs-lookup"><span data-stu-id="e9bd5-111">Within the **Properties** dialog, in the left-hand pane, click **Javadoc Location**.</span></span> <span data-ttu-id="e9bd5-112">Отображается диалоговое окно **Javadoc Location** (Расположение Javadoc).</span><span class="sxs-lookup"><span data-stu-id="e9bd5-112">The **Javadoc Location** dialog is displayed.</span></span>

1. <span data-ttu-id="e9bd5-113">Вы можете указать **Javadoc URL** (URL-адрес Javadoc) или **Javadoc in archive** (Javadoc в архиве) в соответствующих полях.</span><span class="sxs-lookup"><span data-stu-id="e9bd5-113">You can specify a **Javadoc URL**, or a **Javadoc in archive**.</span></span>

   * <span data-ttu-id="e9bd5-114">Если вам требуется указать **URL-адрес Javadoc**, используйте URL-адреса в следующем формате: **http://dl.windowsazure.com/javadoc** или **http://dl.windowsazure.com/storage/javadoc**.</span><span class="sxs-lookup"><span data-stu-id="e9bd5-114">If you choose to specify a **Javadoc URL**, use the URLs such as **http://dl.windowsazure.com/javadoc** or **http://dl.windowsazure.com/storage/javadoc**.</span></span>

   * <span data-ttu-id="e9bd5-115">Если вы решите использовать **Javadoc in archive**(Javadoc в архиве), можете указать внешний файл или файл рабочей области.</span><span class="sxs-lookup"><span data-stu-id="e9bd5-115">If you choose to use **Javadoc in archive**, you can specify an external file, or a workspace file.</span></span>

   <span data-ttu-id="e9bd5-116">Выберите нужный вариант и при необходимости выполните переход или проверку.</span><span class="sxs-lookup"><span data-stu-id="e9bd5-116">Make your choice and browse/validate as needed.</span></span> <span data-ttu-id="e9bd5-117">В следующем примере библиотеки Azure для Java сопоставляются с соответствующим JAR-файлом Javadoc, скачанным в локальную папку с именем **c:\MyAzureJARs**.</span><span class="sxs-lookup"><span data-stu-id="e9bd5-117">The following example associates the Azure Libraries for Java with the corresponding Javadoc JAR that has been downloaded locally to a folder named **c:\MyAzureJARs**.</span></span>

   ![Отображение содержимого Javadoc.][ic553487]

1. <span data-ttu-id="e9bd5-119">*Необязательный шаг*. Щелкните **Проверить**.</span><span class="sxs-lookup"><span data-stu-id="e9bd5-119">*Optional Step*: Click **Validate**.</span></span> <span data-ttu-id="e9bd5-120">При этом могут отображаться потенциальные проблемы с JAR-файлом Javadoc.</span><span class="sxs-lookup"><span data-stu-id="e9bd5-120">Potential issues with the Javadoc JAR could be displayed here.</span></span>

1. <span data-ttu-id="e9bd5-121">Последовательно выберите **ОК**.</span><span class="sxs-lookup"><span data-stu-id="e9bd5-121">Click **OK**.</span></span>

<span data-ttu-id="e9bd5-122">После сопоставления с библиотекой содержимое Javadoc должно отображаться в Eclipse IDE.</span><span class="sxs-lookup"><span data-stu-id="e9bd5-122">Once associated with the library, the Javadoc content should display within your Eclipse IDE.</span></span> <span data-ttu-id="e9bd5-123">Например, если `blob` определен в коде с типом `CloudBlockBlob`, ниже приведен пример содержимого Javadoc, которое появляется при вводе `blob.acquireLease` в коде:</span><span class="sxs-lookup"><span data-stu-id="e9bd5-123">For example, if `blob` is defined of type `CloudBlockBlob` within your code, the following is an example of Javadoc content that appears when you type `blob.acquireLease` in code:</span></span>

![Отображение содержимого Javadoc.][ic553488]

## <a name="next-steps"></a><span data-ttu-id="e9bd5-125">Дополнительная информация</span><span class="sxs-lookup"><span data-stu-id="e9bd5-125">Next steps</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-additional-resources](../includes/azure-toolkit-for-eclipse-additional-resources.md)]

<!-- URL List -->

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh698319.aspx -->

<!-- IMG List -->

[ic553487]: media/azure-toolkit-for-eclipse-displaying-javadoc-content-for-azure-libraries/ic553487.png
[ic553488]: media/azure-toolkit-for-eclipse-displaying-javadoc-content-for-azure-libraries/ic553488.png
