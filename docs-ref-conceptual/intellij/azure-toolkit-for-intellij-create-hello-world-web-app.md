---
title: Создание веб-приложения Hello World для Azure с помощью Eclipse
description: В этом учебнике показано, как с помощью набора средств Azure для IntelliJ создать веб-приложение Hello World для Azure.
services: app-service
documentationcenter: java
author: selvasingh
manager: routlaw
editor: ''
ms.assetid: 75ce7b36-e3ae-491d-8305-4b42ce37db4e
ms.author: robmcm;asirveda
ms.date: 02/01/2018
ms.devlang: java
ms.service: app-service
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: web
ms.openlocfilehash: cc68e16a6940a1f0f2b08f0b63c90c58ec6dbc4e
ms.sourcegitcommit: b64017f119177f97da7a5930489874e67b09c0fc
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/09/2018
ms.locfileid: "48892865"
---
# <a name="create-a-hello-world-web-app-for-azure-using-intellij"></a><span data-ttu-id="56193-103">Создание веб-приложения Hello World для Azure с помощью Eclipse</span><span class="sxs-lookup"><span data-stu-id="56193-103">Create a Hello World web app for Azure using IntelliJ</span></span>

<span data-ttu-id="56193-104">В этом руководстве показано, как создать базовое приложение Hello World для Azure и развернуть его как веб-приложение с помощью [Набор средств Azure для IntelliJ].</span><span class="sxs-lookup"><span data-stu-id="56193-104">This tutorial shows how to create and deploy a basic Hello World application to Azure as a web app by using the [Azure Toolkit for IntelliJ].</span></span>

> [!NOTE]
>
> <span data-ttu-id="56193-105">Дополнительные сведения о версии, в которой используются [Набор средств Azure для Eclipse], см. в статье [Создание веб-приложения Azure (цен. категория "Базовый") с помощью Eclipse][eclipse-hello-world].</span><span class="sxs-lookup"><span data-stu-id="56193-105">For a version of this article that uses the [Azure Toolkit for Eclipse], see [Create a Hello World web app for Azure using Eclipse][eclipse-hello-world].</span></span>
>

> [!IMPORTANT]
> 
> <span data-ttu-id="56193-106">Набор средств Azure для IntelliJ обновлен в августе 2017 года. В него добавлен другой рабочий процесс.</span><span class="sxs-lookup"><span data-stu-id="56193-106">The Azure Toolkit for IntelliJ was updated in August 2017 with a different workflow.</span></span> <span data-ttu-id="56193-107">В этой статье описывается, как создать веб-приложение Hello World с помощью набора средств Azure для IntelliJ версии 3.0.7 (или более поздней).</span><span class="sxs-lookup"><span data-stu-id="56193-107">This article illustrates creating a Hello World web app by using version 3.0.7 (or later) of the Azure Toolkit for IntelliJ.</span></span> <span data-ttu-id="56193-108">Если вы используете набор средств версии 3.0.6 (или более ранней), необходимо выполнить действия, описанные в руководстве по [созданию веб-приложения Hello World для Azure в IntelliJ с помощью набора средств предыдущих версий][Legacy Version].</span><span class="sxs-lookup"><span data-stu-id="56193-108">If you are using the version 3.0.6 (or earlier) of the toolkit, you will need to follow the steps in [Create a Hello World web app for Azure in IntelliJ using the legacy toolkit][Legacy Version].</span></span>
> 

<span data-ttu-id="56193-109">После завершения этого учебника приложение при просмотре в веб-браузере будет выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="56193-109">When you have completed this tutorial, your application will look similar to the following illustration when you view it in a web browser:</span></span>

![Предварительный просмотр приложения Hello World][browse-web-app]

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="create-a-new-web-app-project"></a><span data-ttu-id="56193-111">Создание проекта веб-приложения</span><span class="sxs-lookup"><span data-stu-id="56193-111">Create a new web app project</span></span>

1. <span data-ttu-id="56193-112">Запустите IntelliJ и войдите в свою учетную запись Azure, следуя инструкциям из статьи [Инструкции по входу для набора средств Azure для IntelliJ][intelliJ-sign-in-instructions].</span><span class="sxs-lookup"><span data-stu-id="56193-112">Start IntelliJ, and sign into your Azure account by using the instructions in the [Azure Sign In Instructions for the Azure Toolkit for IntelliJ][intelliJ-sign-in-instructions] article.</span></span>

1. <span data-ttu-id="56193-113">Щелкните меню **File** (Файл), выберите команду **New** (Создать), а затем — **Project** (Проект).</span><span class="sxs-lookup"><span data-stu-id="56193-113">Click the **File** menu, then click **New**, and then click **Project**.</span></span>
   
   ![Создание проекта][file-new-project]

1. <span data-ttu-id="56193-115">В диалоговом окне **New Project** (Новый проект) выберите **Maven**, а затем **maven-archetype-webapp** и щелкните **Next** (Далее).</span><span class="sxs-lookup"><span data-stu-id="56193-115">In the **New Project** dialog box, select **Maven**, then **maven-archetype-webapp**, and then click **Next**.</span></span>
   
   ![Выбор веб-приложения архетипа Maven][maven-archetype-webapp]
   
1. <span data-ttu-id="56193-117">Укажите значение **GroupId** (Идентификатор группы) и **ArtifactId** (Идентификатор артефакта) для веб-приложения и щелкните **Next** (Далее).</span><span class="sxs-lookup"><span data-stu-id="56193-117">Specify the **GroupId** and **ArtifactId** for your web app, and then click **Next**.</span></span>
   
   ![Указание идентификатора группы и артефакта][groupid-and-artifactid]

1. <span data-ttu-id="56193-119">Настройте любые параметры Maven или примите значения по умолчанию и щелкните **Next** (Далее).</span><span class="sxs-lookup"><span data-stu-id="56193-119">Customize any Maven settings or accept the defaults, and then click **Next**.</span></span>
   
   ![Указание параметров Maven][maven-options]

1. <span data-ttu-id="56193-121">Укажите имя и расположение проекта, а затем щелкните **Finish** (Готово).</span><span class="sxs-lookup"><span data-stu-id="56193-121">Specify your project name and location, and then click **Finish**.</span></span>
   
   ![Указание имени проекта][project-name]

1. <span data-ttu-id="56193-123">В представлении обозревателя проектов IntelliJ разверните **src**, а затем **main**, **webapp** и дважды щелкните **index.jsp**.</span><span class="sxs-lookup"><span data-stu-id="56193-123">Within IntelliJ's Project Explorer view, expand **src**, then **main**, then **webapp**, and then double-click **index.jsp**.</span></span>
   
   ![Открытие страницы индексов][open-index-page]

1. <span data-ttu-id="56193-125">При открытии в IntelliJ файла index.jsp добавьте код для динамического отображения фразы **Hello World!**</span><span class="sxs-lookup"><span data-stu-id="56193-125">When your index.jsp file opens in IntelliJ, add in text to dynamically display **Hello World!**</span></span> <span data-ttu-id="56193-126">в существующий элемент `<body>`.</span><span class="sxs-lookup"><span data-stu-id="56193-126">within the existing `<body>` element.</span></span> <span data-ttu-id="56193-127">Обновленное содержимое элемента `<body>` должно выглядеть так:</span><span class="sxs-lookup"><span data-stu-id="56193-127">Your updated `<body>` content should resemble the following example:</span></span>
   
   ```java
   <body><b><% out.println("Hello World!"); %></b></body>
   ``` 

   ![Изменение страницы индексов][edit-index-page]

1. <span data-ttu-id="56193-129">Сохраните index.jsp.</span><span class="sxs-lookup"><span data-stu-id="56193-129">Save index.jsp.</span></span>

## <a name="deploy-your-web-app-to-azure"></a><span data-ttu-id="56193-130">Развертывание веб-приложения в Azure</span><span class="sxs-lookup"><span data-stu-id="56193-130">Deploy your web app to Azure</span></span>

1. <span data-ttu-id="56193-131">В представлении обозревателя проектов IntelliJ щелкните правой кнопкой мыши проект, выберите **Azure**, а затем — **Run on Web App** (Выполнить в веб-приложении).</span><span class="sxs-lookup"><span data-stu-id="56193-131">Within IntelliJ's Project Explorer view, right-click your project, choose **Azure**, and then choose **Run on Web App**.</span></span>
   
   ![Пункт меню Run on web app (Выполнить в веб-приложении)][run-on-web-app-menu]

1. <span data-ttu-id="56193-133">В диалоговом окне Run on Web App (Выполнение в веб-приложении) можно выбрать один из таких вариантов:</span><span class="sxs-lookup"><span data-stu-id="56193-133">In the Run on Web App dialog box, you can choose one of the following options:</span></span>

   * <span data-ttu-id="56193-134">Выберите имеющееся веб-приложение (если оно есть) и нажмите кнопку **Run** (Выполнить).</span><span class="sxs-lookup"><span data-stu-id="56193-134">Choose an existing web app (if one exists), and then click **Run**.</span></span>

      ![Диалоговое окно Run on Web App (Выполнение в веб-приложении)][run-on-web-app-dialog]

   * <span data-ttu-id="56193-136">Щелкните **Create New Web App** (Создать веб-приложение).</span><span class="sxs-lookup"><span data-stu-id="56193-136">Click **Create New Web App**.</span></span> <span data-ttu-id="56193-137">Если вы решите создать веб-приложение, укажите требуемую информацию для веб-приложения и нажмите кнопку **Run** (Выполнить).</span><span class="sxs-lookup"><span data-stu-id="56193-137">If you choose to create a new web app, specify the requisite information for your web app, and then click **Run**.</span></span>

      ![Создание веб-приложения][create-new-web-app-dialog]

1. <span data-ttu-id="56193-139">Набор средств отобразит сообщение о состоянии при успешном развертывании веб-приложения, где будет содержаться URL-адрес развернутого веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="56193-139">The toolkit will display a status message when it has successfully deployed your web app, which will also display the URL of your deployed web app.</span></span>

   ![Развертывание завершено успешно][successfully-deployed]

1. <span data-ttu-id="56193-141">Перейти к своему веб-приложению можно с помощью ссылки, предоставленной в сообщении о состоянии.</span><span class="sxs-lookup"><span data-stu-id="56193-141">You can browse to your web app using the link provided in the status message.</span></span>

   ![Просмотр веб-приложения][browse-web-app]

1. <span data-ttu-id="56193-143">После публикации веб-приложения параметры будут сохранены в качестве параметров по умолчанию. Приложение можно запустить в Azure, щелкнув значок зеленой стрелки на панели инструментов.</span><span class="sxs-lookup"><span data-stu-id="56193-143">After you have published your web app, your settings will be saved as the default, and you can run your application on Azure by clicking the green arrow icon on the toolbar.</span></span> <span data-ttu-id="56193-144">Вы можете изменить параметры, щелкнув раскрывающееся меню для веб-приложения, а затем — **Edit Configurations** (Изменить конфигурации).</span><span class="sxs-lookup"><span data-stu-id="56193-144">You can modify your settings by clicking the drop-down menu for your web app and click **Edit Configurations**.</span></span>

   ![Пункт меню Edit configuration (Изменить конфигурацию)][edit-configuration-menu]

1. <span data-ttu-id="56193-146">При отображении диалогового окна **Run/Debug Configurations** (Конфигурации выполнения и отладки) можно изменить любые параметры по умолчанию, а затем нажать кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="56193-146">When the **Run/Debug Configurations** dialog box is displayed, you can modify any of the default settings, and then click **OK**.</span></span>

   ![Диалоговое окно Edit configuration (Изменение конфигурации)][edit-configuration-dialog]

## <a name="next-steps"></a><span data-ttu-id="56193-148">Дополнительная информация</span><span class="sxs-lookup"><span data-stu-id="56193-148">Next steps</span></span>

[!INCLUDE [azure-toolkit-for-intellij-additional-resources](../includes/azure-toolkit-for-intellij-additional-resources.md)]

<span data-ttu-id="56193-149">Дополнительные сведения о создании веб-приложений Azure см. в разделе [Обзор веб-приложений].</span><span class="sxs-lookup"><span data-stu-id="56193-149">For additional information about creating Azure Web Apps, see the [Web Apps Overview].</span></span>

<!-- URL List -->

[Набор средств Azure для IntelliJ]: azure-toolkit-for-intellij.md
[Azure Toolkit for IntelliJ]: azure-toolkit-for-intellij.md
[Набор средств Azure для Eclipse]: ../eclipse/azure-toolkit-for-eclipse.md
[Azure Toolkit for Eclipse]: ../eclipse/azure-toolkit-for-eclipse.md
[eclipse-hello-world]: ../eclipse/azure-toolkit-for-eclipse-create-hello-world-web-app.md
[Обзор веб-приложений]: /azure/app-service/app-service-web-overview
[Web Apps Overview]: /azure/app-service/app-service-web-overview
[Apache Tomcat]: http://tomcat.apache.org/
[Jetty]: http://www.eclipse.org/jetty/
[Legacy Version]: azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version.md
[intelliJ-sign-in-instructions]: azure-toolkit-for-intellij-sign-in-instructions.md

<!-- IMG List -->

[file-new-project]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/file-new-project.png
[maven-archetype-webapp]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/maven-archetype-webapp.png
[groupid-and-artifactid]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/groupid-and-artifactid.png
[maven-options]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/maven-options.png
[project-name]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/project-name.png
[open-index-page]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/open-index-page.png
[edit-index-page]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/edit-index-page.png
[run-on-web-app-menu]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/run-on-web-app-menu.png
[run-on-web-app-dialog]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/run-on-web-app-dialog.png
[create-new-web-app-dialog]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/create-new-web-app-dialog.png
[successfully-deployed]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/successfully-deployed.png
[browse-web-app]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/browse-web-app.png
[edit-configuration-menu]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/edit-configuration-menu.png
[edit-configuration-dialog]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/edit-configuration-dialog.png
