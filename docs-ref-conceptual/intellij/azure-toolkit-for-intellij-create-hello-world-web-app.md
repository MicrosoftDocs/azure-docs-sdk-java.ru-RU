---
title: "Создание веб-приложения Azure (цен. категория \"Базовый\") в IntelliJ"
description: "В этом учебнике показано, как с помощью набора средств Azure для IntelliJ создать веб-приложение Hello World для Azure."
services: app-service
documentationcenter: java
author: selvasingh
manager: routlaw
editor: 
ms.assetid: 75ce7b36-e3ae-491d-8305-4b42ce37db4e
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: multiple
ms.devlang: java
ms.topic: article
ms.date: 10/19/2017
ms.author: robmcm;asirveda
ms.openlocfilehash: 323ce74f2d4dad10460a0c2bc0fb59f2bbdbbf3c
ms.sourcegitcommit: 7f8538e41c833deb69c300ad3431a431136a1f3e
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/24/2017
---
# <a name="create-a-basic-azure-web-app-in-intellij"></a><span data-ttu-id="8e49e-103">Создание веб-приложения Azure (цен. категория "Базовый") в IntelliJ</span><span class="sxs-lookup"><span data-stu-id="8e49e-103">Create a basic Azure web app in IntelliJ</span></span>

<span data-ttu-id="8e49e-104">В этом руководстве показано, как создать базовое приложение Hello World для Azure и развернуть его как веб-приложение с помощью [набора средств Azure для IntelliJ].</span><span class="sxs-lookup"><span data-stu-id="8e49e-104">This tutorial shows how to create and deploy a basic Hello World application to Azure as a web app by using the [Azure Toolkit for IntelliJ].</span></span>

> [!NOTE]
> 
> <span data-ttu-id="8e49e-105">Набор средств Azure для IntelliJ был обновлен в августе 2017 года. В него был добавлен другой рабочий процесс.</span><span class="sxs-lookup"><span data-stu-id="8e49e-105">The Azure Toolkit for IntelliJ was updated in August 2017, with a different workflow.</span></span> <span data-ttu-id="8e49e-106">С учетом этого в этой статье содержатся два различных раздела:</span><span class="sxs-lookup"><span data-stu-id="8e49e-106">With that in mind, this article contains two different sections:</span></span>
>
> * <span data-ttu-id="8e49e-107">В первом разделе показано создание веб-приложения Hello World с помощью набора средств Azure для IntelliJ версии от августа 2017 года (или более поздней).</span><span class="sxs-lookup"><span data-stu-id="8e49e-107">The first section illustrates creating a Hello World web app by using the August 2017 (or later) version of the Azure Toolkit for IntelliJ.</span></span>
>
> * <span data-ttu-id="8e49e-108">Во втором разделе этой статьи показано создание веб-приложения Hello World с помощью набора средств версии от апреля 2017 года (или более ранней).</span><span class="sxs-lookup"><span data-stu-id="8e49e-108">The second section of this article demonstrates creating a Hello World web app by using the April 2017 (or earlier) version of the toolkit.</span></span>
> 

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="create-a-hello-world-web-app-by-using-the-version-307-or-later-toolkit"></a><span data-ttu-id="8e49e-109">Создание веб-приложения Hello World с помощью набора средств версии 3.0.7 или более поздней</span><span class="sxs-lookup"><span data-stu-id="8e49e-109">Create a Hello World web app by using the version 3.0.7 or later toolkit</span></span>

### <a name="create-a-new-web-app-project"></a><span data-ttu-id="8e49e-110">Создание проекта веб-приложения</span><span class="sxs-lookup"><span data-stu-id="8e49e-110">Create a new web app project</span></span>

1. <span data-ttu-id="8e49e-111">Запустите IntelliJ и войдите в свою учетную запись Azure, следуя инструкциям из статьи "Инструкции по входу для набора средств Azure для IntelliJ".</span><span class="sxs-lookup"><span data-stu-id="8e49e-111">Start IntelliJ and sign-in to your Azure account using the steps in the [Sign In Instructions for the Azure Toolkit for IntelliJ] article.</span></span>

1. <span data-ttu-id="8e49e-112">Щелкните меню **File** (Файл), выберите команду **New** (Создать), а затем — **Project** (Проект).</span><span class="sxs-lookup"><span data-stu-id="8e49e-112">Click the **File** menu, then click **New**, and then click **Project**.</span></span>
   
   ![Создание проекта][file-new-project]

1. <span data-ttu-id="8e49e-114">В диалоговом окне **New Project** (Новый проект) выберите **Maven**, а затем **maven-archetype-webapp** и щелкните **Next** (Далее).</span><span class="sxs-lookup"><span data-stu-id="8e49e-114">In the **New Project** dialog box, select **Maven**, then **maven-archetype-webapp**, and then click **Next**.</span></span>
   
   ![Выбор веб-приложения архетипа Maven][maven-archetype-webapp]
   
1. <span data-ttu-id="8e49e-116">Укажите значение **GroupId** (Идентификатор группы) и **ArtifactId** (Идентификатор артефакта) для веб-приложения и щелкните **Next** (Далее).</span><span class="sxs-lookup"><span data-stu-id="8e49e-116">Specify the **GroupId** and **ArtifactId** for your web app, and then click **Next**.</span></span>
   
   ![Указание идентификатора группы и артефакта][groupid-and-artifactid]

1. <span data-ttu-id="8e49e-118">Настройте любые параметры Maven или примите значения по умолчанию и щелкните **Next** (Далее).</span><span class="sxs-lookup"><span data-stu-id="8e49e-118">Customize any Maven settings or accept the defaults, and then click **Next**.</span></span>
   
   ![Указание параметров Maven][maven-options]

1. <span data-ttu-id="8e49e-120">Укажите имя и расположение проекта, а затем щелкните **Finish** (Готово).</span><span class="sxs-lookup"><span data-stu-id="8e49e-120">Specify your project name and location, and then click **Finish**.</span></span>
   
   ![Указание имени проекта][project-name]

1. <span data-ttu-id="8e49e-122">В представлении обозревателя проектов IntelliJ разверните **src**, а затем **main**, **webapp** и дважды щелкните **index.jsp**.</span><span class="sxs-lookup"><span data-stu-id="8e49e-122">Within IntelliJ's Project Explorer view, expand **src**, then **main**, then **webapp**, and then double-click **index.jsp**.</span></span>
   
   ![Открытие страницы индексов][open-index-page]

1. <span data-ttu-id="8e49e-124">При открытии в IntelliJ файла index.jsp добавьте код для динамического отображения фразы **Hello World!**</span><span class="sxs-lookup"><span data-stu-id="8e49e-124">When your index.jsp file opens in IntelliJ, add in text to dynamically display **Hello World!**</span></span> <span data-ttu-id="8e49e-125">в существующий элемент `<body>`.</span><span class="sxs-lookup"><span data-stu-id="8e49e-125">within the existing `<body>` element.</span></span> <span data-ttu-id="8e49e-126">Обновленное содержимое элемента `<body>` должно выглядеть так:</span><span class="sxs-lookup"><span data-stu-id="8e49e-126">Your updated `<body>` content should resemble the following example:</span></span>
   
   ```java
   <body><b><% out.println("Hello World!"); %></b></body>
   ``` 

   ![Изменение страницы индексов][edit-index-page]

1. <span data-ttu-id="8e49e-128">Сохраните index.jsp.</span><span class="sxs-lookup"><span data-stu-id="8e49e-128">Save index.jsp.</span></span>

### <a name="deploy-your-web-app-to-azure"></a><span data-ttu-id="8e49e-129">Развертывание веб-приложения в Azure</span><span class="sxs-lookup"><span data-stu-id="8e49e-129">Deploy your web app to Azure</span></span>

1. <span data-ttu-id="8e49e-130">В представлении обозревателя проектов IntelliJ щелкните правой кнопкой мыши проект, выберите **Azure**, а затем — **Run on Web App** (Выполнить в веб-приложении).</span><span class="sxs-lookup"><span data-stu-id="8e49e-130">Within IntelliJ's Project Explorer view, right-click your project, choose **Azure**, and then choose **Run on Web App**.</span></span>
   
   ![Пункт меню Run on web app (Выполнить в веб-приложении)][run-on-web-app-menu]

1. <span data-ttu-id="8e49e-132">В диалоговом окне Run on Web App (Выполнение в веб-приложении) можно выбрать один из таких вариантов:</span><span class="sxs-lookup"><span data-stu-id="8e49e-132">In the Run on Web App dialog box, you can choose one of the following options:</span></span>

   * <span data-ttu-id="8e49e-133">Выберите имеющееся веб-приложение (если оно есть) и нажмите кнопку **Run** (Выполнить).</span><span class="sxs-lookup"><span data-stu-id="8e49e-133">Choose an existing web app (if one exists), and then click **Run**.</span></span>

      ![Диалоговое окно Run on Web App (Выполнение в веб-приложении)][run-on-web-app-dialog]

   * <span data-ttu-id="8e49e-135">Щелкните **Create New Web App** (Создать веб-приложение).</span><span class="sxs-lookup"><span data-stu-id="8e49e-135">Click **Create New Web App**.</span></span> <span data-ttu-id="8e49e-136">Если вы решите создать веб-приложение, укажите требуемую информацию для веб-приложения и нажмите кнопку **Run** (Выполнить).</span><span class="sxs-lookup"><span data-stu-id="8e49e-136">If you choose to create a new web app, specify the requisite information for your web app, and then click **Run**.</span></span>

      ![Создание веб-приложения][create-new-web-app-dialog]

1. <span data-ttu-id="8e49e-138">Набор средств отобразит сообщение о состоянии при успешном развертывании веб-приложения, где будет содержаться URL-адрес развернутого веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="8e49e-138">The toolkit will display a status message when it has successfully deployed your web app, which will also display the URL of your deployed web app.</span></span>

   ![Развертывание завершено успешно][successfully-deployed]

1. <span data-ttu-id="8e49e-140">Перейти к своему веб-приложению можно с помощью ссылки, предоставленной в сообщении о состоянии.</span><span class="sxs-lookup"><span data-stu-id="8e49e-140">You can browse to your web app using the link provided in the status message.</span></span>

   ![Просмотр веб-приложения][browse-web-app]

1. <span data-ttu-id="8e49e-142">После публикации веб-приложения параметры будут сохранены в качестве параметров по умолчанию. Приложение можно запустить в Azure, щелкнув значок зеленой стрелки на панели инструментов.</span><span class="sxs-lookup"><span data-stu-id="8e49e-142">After you have published your web app, your settings will be saved as the default, and you can run your application on Azure by clicking the green arrow icon on the toolbar.</span></span> <span data-ttu-id="8e49e-143">Вы можете изменить параметры, щелкнув раскрывающееся меню для веб-приложения, а затем — **Edit Configurations** (Изменить конфигурации).</span><span class="sxs-lookup"><span data-stu-id="8e49e-143">You can modify your settings by clicking the drop-down menu for your web app and click **Edit Configurations**.</span></span>

   ![Пункт меню Edit configuration (Изменить конфигурацию)][edit-configuration-menu]

1. <span data-ttu-id="8e49e-145">При отображении диалогового окна **Run/Debug Configurations** (Конфигурации выполнения и отладки) можно изменить любые параметры по умолчанию, а затем нажать кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="8e49e-145">When the **Run/Debug Configurations** dialog box is displayed, you can modify any of the default settings, and then click **OK**.</span></span>

   ![Диалоговое окно Edit configuration (Изменение конфигурации)][edit-configuration-dialog]

<hr />

## <a name="create-a-hello-world-web-app-by-using-the-version-306-or-earlier-toolkit"></a><span data-ttu-id="8e49e-147">Создание веб-приложения Hello World с помощью набора средств версии 3.0.6 или более ранних</span><span class="sxs-lookup"><span data-stu-id="8e49e-147">Create a Hello World web app by using the version 3.0.6 or earlier toolkit</span></span>

### <a name="create-a-new-web-app-project"></a><span data-ttu-id="8e49e-148">Создание проекта веб-приложения</span><span class="sxs-lookup"><span data-stu-id="8e49e-148">Create a new web app project</span></span>

1. <span data-ttu-id="8e49e-149">Запустите IntelliJ и щелкните меню **File** (Файл), затем щелкните **New** (Создать) и **Project** (Проект).</span><span class="sxs-lookup"><span data-stu-id="8e49e-149">Start IntelliJ and click the **File** menu, then click **New**, and then click **Project**.</span></span>
   
   ![Файл > Создать > Проект][02]

2. <span data-ttu-id="8e49e-151">В диалоговом окне **New Project** (Создание проекта) выберите **Java**, а затем установите флажок **Web Application** (Веб-приложение) и нажмите кнопку **New** (Создать), чтобы добавить пакет SDK проекта.</span><span class="sxs-lookup"><span data-stu-id="8e49e-151">In the **New Project** dialog box, select **Java**, then **Web Application**, and then click **New** to add a Project SDK.</span></span>
   
   ![Диалоговое окно "Новый проект"][03a]
   
3. <span data-ttu-id="8e49e-153">В диалоговом окне "Select Home Directory for JDK" (Выбор корневого каталога для JDK) выберите папку для установки JDK, затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="8e49e-153">In the Select Home Directory for JDK dialog box, select the folder where your JDK is installed, and then click **OK**.</span></span> <span data-ttu-id="8e49e-154">Нажмите кнопку **Next** (Далее) в диалоговом окне "New Project" (Создание проекта), чтобы продолжить.</span><span class="sxs-lookup"><span data-stu-id="8e49e-154">Click **Next** in the New Project dialog box to continue.</span></span>
   
   ![Указание корневого каталога JDK][03b]

4. <span data-ttu-id="8e49e-156">Укажите имя проекта **Java-Web-App-On-Azure** и нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="8e49e-156">For purposes of this tutorial, name the project **Java-Web-App-On-Azure**, and then click **Finish**.</span></span>
   
   ![Диалоговое окно "Новый проект"][04]

5. <span data-ttu-id="8e49e-158">В представлении обозревателя проектов IntelliJ разверните **Java-Web-App-On-Azure**, а затем разверните **web** и дважды щелкните **index.jsp**.</span><span class="sxs-lookup"><span data-stu-id="8e49e-158">Within IntelliJ's Project Explorer view, expand **Java-Web-App-On-Azure**, then expand **web**, and then double-click **index.jsp**.</span></span>
   
   ![Открытие страницы индексации][05c]

6. <span data-ttu-id="8e49e-160">При открытии в IntelliJ файла index.jsp добавьте код для динамического отображения фразы **Hello World!**</span><span class="sxs-lookup"><span data-stu-id="8e49e-160">When your index.jsp file opens in IntelliJ, add in text to dynamically display **Hello World!**</span></span> <span data-ttu-id="8e49e-161">в существующий элемент `<body>`.</span><span class="sxs-lookup"><span data-stu-id="8e49e-161">within the existing `<body>` element.</span></span> <span data-ttu-id="8e49e-162">Обновленное содержимое элемента `<body>` должно выглядеть так:</span><span class="sxs-lookup"><span data-stu-id="8e49e-162">Your updated `<body>` content should resemble the following example:</span></span>
   
   ```java
   <body><b><% out.println("Hello World!"); %></b></body>
   ```

7. <span data-ttu-id="8e49e-163">Сохраните index.jsp.</span><span class="sxs-lookup"><span data-stu-id="8e49e-163">Save index.jsp.</span></span>

### <a name="deploy-your-web-app-to-azure"></a><span data-ttu-id="8e49e-164">Развертывание веб-приложения в Azure</span><span class="sxs-lookup"><span data-stu-id="8e49e-164">Deploy your web app to Azure</span></span>
<span data-ttu-id="8e49e-165">Есть несколько способов, с помощью которых можно развернуть веб-приложение Java в Azure.</span><span class="sxs-lookup"><span data-stu-id="8e49e-165">There are several ways by which you can deploy a Java web app to Azure.</span></span> <span data-ttu-id="8e49e-166">В этом учебнике описывается один из самых простых: ваше приложение будет развернуто в контейнер веб-приложения Azure — для этого не нужно выбирать особый тип проекта и не требуются дополнительные инструменты.</span><span class="sxs-lookup"><span data-stu-id="8e49e-166">This tutorial describes one of the simplest: your application will be deployed to an Azure Web App Container - no special project type nor additional tools are needed.</span></span> <span data-ttu-id="8e49e-167">JDK и программное обеспечение веб-контейнера будут предоставлены Azure, поэтому нет необходимости загружать их самостоятельно. Все, что вам нужно — ваше веб-приложение Java.</span><span class="sxs-lookup"><span data-stu-id="8e49e-167">The JDK and the web container software will be provided for you by Azure, so there is no need to upload your own; all you need is your Java Web App.</span></span> <span data-ttu-id="8e49e-168">В результате процесс публикации приложения занимает несколько секунд, а не минут.</span><span class="sxs-lookup"><span data-stu-id="8e49e-168">As a result, the publishing process for your application will take seconds, not minutes.</span></span>

<span data-ttu-id="8e49e-169">Прежде чем публиковать приложение, необходимо сначала настроить параметры модуля.</span><span class="sxs-lookup"><span data-stu-id="8e49e-169">Before you publish your application, you first need to configure your module settings.</span></span> <span data-ttu-id="8e49e-170">Для этого выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="8e49e-170">To do so, use the following steps:</span></span>

1. <span data-ttu-id="8e49e-171">Щелкните правой кнопкой мыши по проекту **Java-Web-App-On-Azure** в обозревателе проектов IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="8e49e-171">In IntelliJ's Project Explorer, right-click the **Java-Web-App-On-Azure** project.</span></span> <span data-ttu-id="8e49e-172">В открывшемся контекстном меню щелкните **Open Module Settings** (Открыть параметры модуля).</span><span class="sxs-lookup"><span data-stu-id="8e49e-172">When the context menu appears, click **Open Module Settings**.</span></span>

   ![Открытие параметров модуля][05a]

2. <span data-ttu-id="8e49e-174">В отобразившемся диалоговом окне "Project Structure" (Структура проекта) выполните следующее.</span><span class="sxs-lookup"><span data-stu-id="8e49e-174">When the Project Structure dialog box appears:</span></span>

   <span data-ttu-id="8e49e-175">а.</span><span class="sxs-lookup"><span data-stu-id="8e49e-175">a.</span></span> <span data-ttu-id="8e49e-176">В списке **Project Settings** (Параметры проекта) щелкните **Artifacts** (Артефакты).</span><span class="sxs-lookup"><span data-stu-id="8e49e-176">Click **Artifacts** in the list of **Project Settings**.</span></span>

   <span data-ttu-id="8e49e-177">b.</span><span class="sxs-lookup"><span data-stu-id="8e49e-177">b.</span></span> <span data-ttu-id="8e49e-178">Измените имя артефакта в поле **Name** (Имя) таким образом, чтобы оно не содержало пробелы или специальные знаки. Это необходимо, так как имя будет использоваться в универсальном коде ресурса (URI).</span><span class="sxs-lookup"><span data-stu-id="8e49e-178">Change the artifact name in the **Name** box so that it doesn't contain whitespace or special characters; this is necessary since the name will be used in the Uniform Resource Identifier (URI).</span></span>

   <span data-ttu-id="8e49e-179">В.</span><span class="sxs-lookup"><span data-stu-id="8e49e-179">c.</span></span> <span data-ttu-id="8e49e-180">Измените значение параметра **Type** (Тип) на **Web Application: Archive** (Веб-приложение: архив).</span><span class="sxs-lookup"><span data-stu-id="8e49e-180">Change the **Type** to **Web Application: Archive**.</span></span>

   <span data-ttu-id="8e49e-181">d.</span><span class="sxs-lookup"><span data-stu-id="8e49e-181">d.</span></span> <span data-ttu-id="8e49e-182">Нажмите кнопку **OK**, чтобы закрыть диалоговое окно "Project Structure" (Структура проекта).</span><span class="sxs-lookup"><span data-stu-id="8e49e-182">Click **OK** to close the Project Structure dialog box.</span></span>

   ![Открытие параметров модуля][05b]

<span data-ttu-id="8e49e-184">После настройки параметров модуля можно опубликовать приложение в Azure, выполнив следующие действия.</span><span class="sxs-lookup"><span data-stu-id="8e49e-184">When you have configured your module settings, you can publish your application to Azure by using the following steps:</span></span>

1. <span data-ttu-id="8e49e-185">Щелкните правой кнопкой мыши по проекту **Java-Web-App-On-Azure** в обозревателе проектов IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="8e49e-185">In IntelliJ's Project Explorer, right-click the **Java-Web-App-On-Azure** project.</span></span> <span data-ttu-id="8e49e-186">В контекстном меню выберите **Azure**, а затем щелкните **Publish as Azure Web App** (Опубликовать как веб-приложение Azure).</span><span class="sxs-lookup"><span data-stu-id="8e49e-186">When the context menu appears, select **Azure**, and then click **Publish as Azure Web App...**</span></span>
   
   ![Контекстное меню публикации в Azure][06]

2. <span data-ttu-id="8e49e-188">Если вы еще не вошли в Azure из IntelliJ, появится запрос на вход в учетную запись Azure.</span><span class="sxs-lookup"><span data-stu-id="8e49e-188">If you have not already signed in to Azure from IntelliJ, you will be prompted to sign in to your Azure account.</span></span> <span data-ttu-id="8e49e-189">При наличии нескольких учетных записей Azure некоторые запросы во время входа в систему могут отображаться несколько раз, даже если они выглядят одинаковыми.</span><span class="sxs-lookup"><span data-stu-id="8e49e-189">(If you have multiple Azure accounts, some of the prompts during the sign-in process may be shown more than once, even if they appear to be the same.</span></span> <span data-ttu-id="8e49e-190">Если это происходит, выполните вход согласно указаниям.</span><span class="sxs-lookup"><span data-stu-id="8e49e-190">When this happens, continue to follow the sign-in instructions.)</span></span>
   
   ![Диалоговое окно входа в Azure][07]

3. <span data-ttu-id="8e49e-192">После успешного входа в учетную запись Azure в диалоговом окне **Управление подписками** отобразится список подписок, связанных с вашими учетными данными.</span><span class="sxs-lookup"><span data-stu-id="8e49e-192">After you have successfully signed in to your Azure account, the **Manage Subscriptions** dialog box will display a list of subscriptions that are associated with your credentials.</span></span> <span data-ttu-id="8e49e-193">(Если список содержит несколько подписок и вы будете работать только с некоторыми из них, снимите флажки для подписок, которые не будете использовать.) После выбора подписок щелкните **Закрыть**.</span><span class="sxs-lookup"><span data-stu-id="8e49e-193">(If there are multiple subscriptions listed and you want to work with only a specific subset of them, you may optionally uncheck the subscriptions you don't want to use.) When you have selected your subscriptions, click **Close**.</span></span>
   
   ![Управление подписками][08]

4. <span data-ttu-id="8e49e-195">При открытии диалогового окна **Deploy to Azure Web App Container** (Развертывание в контейнер веб-приложения Azure) в нем будут показаны все контейнеры веб-приложений, созданные ранее. Если вы не создали ни одного контейнера, список будет пустым.</span><span class="sxs-lookup"><span data-stu-id="8e49e-195">When the **Deploy to Azure Web App Container** dialog box appears, it will display any Web App containers that you have previously created; if you have not created any containers, the list will be empty.</span></span>
   
   ![Контейнеры приложений][09]

5. <span data-ttu-id="8e49e-197">Если вы не создавали контейнер веб-приложения Azure или хотите опубликовать приложение в новый контейнер, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="8e49e-197">If you have not created an Azure Web App Container before, or if you would like to publish your application to a new container, use the following steps.</span></span> <span data-ttu-id="8e49e-198">В противном случае выберите существующий контейнер веб-приложения и перейдите к шагу 6 ниже.</span><span class="sxs-lookup"><span data-stu-id="8e49e-198">Otherwise, select an existing Web App Container and skip to step 6 below.</span></span>
   
   <span data-ttu-id="8e49e-199">а.</span><span class="sxs-lookup"><span data-stu-id="8e49e-199">a.</span></span> <span data-ttu-id="8e49e-200">Щелкните символ **+**.</span><span class="sxs-lookup"><span data-stu-id="8e49e-200">Click the **+** sign.</span></span>
      
      ![Добавление контейнера приложения][10]

   <span data-ttu-id="8e49e-202">b.</span><span class="sxs-lookup"><span data-stu-id="8e49e-202">b.</span></span> <span data-ttu-id="8e49e-203">Откроется окно **Новый контейнер веб-приложения** , которым мы воспользуемся для нескольких следующих шагов.</span><span class="sxs-lookup"><span data-stu-id="8e49e-203">The **New Web App Container** dialog box will be displayed, which will be used for the next several steps.</span></span>
      
      ![Создание контейнера приложения][11a]
   
   <span data-ttu-id="8e49e-205">c.</span><span class="sxs-lookup"><span data-stu-id="8e49e-205">c.</span></span> <span data-ttu-id="8e49e-206">Укажите **метку DNS** для контейнера веб-приложения. Она образует метку листа DNS для URL-адреса узла веб-приложения в Azure.</span><span class="sxs-lookup"><span data-stu-id="8e49e-206">Enter a **DNS Label** for your Web App Container; this will form the leaf DNS label of the host URL for your web application in Azure.</span></span> <span data-ttu-id="8e49e-207">(Примечание. Имя должно быть доступным и соответствовать требованиям к именованию веб-приложений Azure.)</span><span class="sxs-lookup"><span data-stu-id="8e49e-207">Note that the name must be available and conform to Azure Web App naming requirements.</span></span>

   <span data-ttu-id="8e49e-208">d.</span><span class="sxs-lookup"><span data-stu-id="8e49e-208">d.</span></span> <span data-ttu-id="8e49e-209">В раскрывающемся меню **Веб-контейнер** выберите для своего приложения соответствующее программное обеспечение.</span><span class="sxs-lookup"><span data-stu-id="8e49e-209">In the **Web Container** drop-down menu, select the appropriate software for your application.</span></span>
      
      <span data-ttu-id="8e49e-210">На данный момент можно выбрать Tomcat 8, Tomcat 7 или Jetty 9.</span><span class="sxs-lookup"><span data-stu-id="8e49e-210">Currently, you can choose from Tomcat 8, Tomcat 7 or Jetty 9.</span></span> <span data-ttu-id="8e49e-211">Последний дистрибутив выбранного программного обеспечения, предоставленный Azure, будет запущен в последнем дистрибутиве JDK 8, созданном Oracle и предоставленном Azure.</span><span class="sxs-lookup"><span data-stu-id="8e49e-211">A recent distribution of the selected software will be provided by Azure, and it will run on a recent distribution of JDK 8 created by Oracle and provided by Azure.</span></span>

   <span data-ttu-id="8e49e-212">д.</span><span class="sxs-lookup"><span data-stu-id="8e49e-212">e.</span></span> <span data-ttu-id="8e49e-213">В раскрывающемся меню **Подписка** выберите подписку, которую вы хотите использовать для этого развертывания.</span><span class="sxs-lookup"><span data-stu-id="8e49e-213">In the **Subscription** drop-down menu, select the subscription you want to use for this deployment.</span></span>

   <span data-ttu-id="8e49e-214">f.</span><span class="sxs-lookup"><span data-stu-id="8e49e-214">f.</span></span> <span data-ttu-id="8e49e-215">В раскрывающемся меню **Группа ресурсов** выберите группу ресурсов, с которой вы хотите связать свое веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="8e49e-215">In the **Resource Group** drop-down menu, select the Resource Group with which you want to associate your Web App.</span></span> <span data-ttu-id="8e49e-216">(Группы ресурсов Azure позволяют сгруппировать связанные ресурсы, чтобы, например, удалить их одновременно.)</span><span class="sxs-lookup"><span data-stu-id="8e49e-216">(Azure Resource Groups allow you to group related resources together so that, for example, they can be deleted together.)</span></span>
      
      <span data-ttu-id="8e49e-217">Можно выбрать существующую группу ресурсов (если она есть) и перейти к шагу g ниже, или создать новую, выполнив следующее.</span><span class="sxs-lookup"><span data-stu-id="8e49e-217">You can select an existing Resource Group (if you have any) and skip to step g below, or use the following steps to create a new Resource Group:</span></span>
      
      * <span data-ttu-id="8e49e-218">Из раскрывающегося меню **Группы ресурсов** выберите пункт **&lt;&lt;Создать новую группу ресурсов&gt;&gt;**.</span><span class="sxs-lookup"><span data-stu-id="8e49e-218">Select **&lt;&lt; Create new Resource Group &gt;&gt;** in the **Resource Group** drop-down menu.</span></span>
      * <span data-ttu-id="8e49e-219">Откроется диалоговое окно **Новая группа ресурсов** :</span><span class="sxs-lookup"><span data-stu-id="8e49e-219">The **New Resource Group** dialog box will be displayed:</span></span>
        
         ![Создание группы ресурсов][12]

      * <span data-ttu-id="8e49e-221">В текстовое поле **Name** (Имя) введите имя новой группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="8e49e-221">In the **Name** textbox, specify a name for your new Resource Group.</span></span>
      * <span data-ttu-id="8e49e-222">В раскрывающемся меню **Region** (Регион) выберите расположение центра обработки данных Azure для группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="8e49e-222">In the **Region** drop-down menu, select the appropriate Azure data center location for your Resource Group.</span></span>
      * <span data-ttu-id="8e49e-223">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="8e49e-223">Click **OK**.</span></span>

   <span data-ttu-id="8e49e-224">ж.</span><span class="sxs-lookup"><span data-stu-id="8e49e-224">g.</span></span> <span data-ttu-id="8e49e-225">В раскрывающемся меню **План службы приложений** перечислены планы службы приложений, связанные с выбранной группой ресурсов.</span><span class="sxs-lookup"><span data-stu-id="8e49e-225">The **App Service Plan** drop-down menu lists the app service plans that are associated with the Resource Group that you selected.</span></span> <span data-ttu-id="8e49e-226">В плане службы приложений указываются такие сведения, как расположение веб-приложения, ценовая категория и размер вычислительной операции.</span><span class="sxs-lookup"><span data-stu-id="8e49e-226">(An App Service Plan specifies information such as the location of your Web App, the pricing tier and the compute instance size.</span></span> <span data-ttu-id="8e49e-227">Один план службы приложений можно использовать для нескольких веб-приложений, поэтому он поддерживается отдельно от развертывания конкретного веб-приложения.)</span><span class="sxs-lookup"><span data-stu-id="8e49e-227">A single App Service Plan can be used for multiple Web Apps, which is why it is maintained separately from a specific Web App deployment.)</span></span>
      
      <span data-ttu-id="8e49e-228">Можно выбрать существующий план службы приложений (если он есть) и перейти к шагу h ниже, или создать новый, выполнив следующее.</span><span class="sxs-lookup"><span data-stu-id="8e49e-228">You can select an existing App Service Plan (if you have any) and skip to step h below, or use the following steps to create a new App Service Plan:</span></span>
      
      * <span data-ttu-id="8e49e-229">Из раскрывающегося меню **План службы приложений** выберите пункт **&lt;&lt;Создать новый план службы приложений&gt;&gt;**.</span><span class="sxs-lookup"><span data-stu-id="8e49e-229">Select **&lt;&lt; Create new App Service Plan &gt;&gt;** in the **App Service Plan** drop-down menu.</span></span>
      * <span data-ttu-id="8e49e-230">Откроется диалоговое окно **Новый план службы приложений** :</span><span class="sxs-lookup"><span data-stu-id="8e49e-230">The **New App Service Plan** dialog box will be displayed:</span></span>
        
         ![Новый план службы приложений][13]

      * <span data-ttu-id="8e49e-232">В текстовое поле **Name** (Имя) введите имя нового плана службы приложений.</span><span class="sxs-lookup"><span data-stu-id="8e49e-232">In the **Name** textbox, specify a name for your new App Service Plan.</span></span>
      * <span data-ttu-id="8e49e-233">В раскрывающемся меню **Location** (Расположение) выберите расположение центра обработки данных Azure для плана.</span><span class="sxs-lookup"><span data-stu-id="8e49e-233">In the **Location** drop-down menu, select the appropriate Azure data center location for the plan.</span></span>
      * <span data-ttu-id="8e49e-234">В раскрывающемся меню **Pricing Tier** (Ценовая категория) выберите соответствующую ценовую категорию для плана.</span><span class="sxs-lookup"><span data-stu-id="8e49e-234">In the **Pricing Tier** drop-down menu, select the appropriate pricing for the plan.</span></span> <span data-ttu-id="8e49e-235">Для тестирования можно выбрать категорию **Бесплатный**.</span><span class="sxs-lookup"><span data-stu-id="8e49e-235">For testing purposes you can choose **Free**.</span></span>
      * <span data-ttu-id="8e49e-236">В раскрывающемся меню **Instance Size** (Размер экземпляра) выберите для плана соответствующий размер экземпляра.</span><span class="sxs-lookup"><span data-stu-id="8e49e-236">In the **Instance Size** drop-down menu, select the appropriate instance size for the plan.</span></span> <span data-ttu-id="8e49e-237">Для тестирования можно выбрать **Маленький**.</span><span class="sxs-lookup"><span data-stu-id="8e49e-237">For testing purposes you can choose **Small**.</span></span>
      * <span data-ttu-id="8e49e-238">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="8e49e-238">Click **OK**.</span></span>

   <span data-ttu-id="8e49e-239">h.</span><span class="sxs-lookup"><span data-stu-id="8e49e-239">h.</span></span> <span data-ttu-id="8e49e-240">(Необязательно.) По умолчанию Azure автоматически развернет последний дистрибутив Java 8 в ваш контейнер веб-приложения в качестве виртуальной машины Java.</span><span class="sxs-lookup"><span data-stu-id="8e49e-240">(Optional) By default, a recent distribution of Java 8 will be automatically deployed as your JVM by Azure to your web app container.</span></span> <span data-ttu-id="8e49e-241">Тем не менее можно выбрать другую версию и дистрибутив виртуальной машины Java.</span><span class="sxs-lookup"><span data-stu-id="8e49e-241">However, you can select a different version and distribution of the JVM.</span></span> <span data-ttu-id="8e49e-242">Для этого выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="8e49e-242">To do so, use the following steps:</span></span>
      
      * <span data-ttu-id="8e49e-243">Щелкните вкладку **JDK** в диалоговом окне **New Web App Container** (Создание контейнера веб-приложения).</span><span class="sxs-lookup"><span data-stu-id="8e49e-243">Click the **JDK** tab in the **New Web App Container** dialog box.</span></span>
      * <span data-ttu-id="8e49e-244">Можно выбрать один из следующих вариантов:</span><span class="sxs-lookup"><span data-stu-id="8e49e-244">You can choose from one of the following options:</span></span>
        
         * <span data-ttu-id="8e49e-245">Развернуть пакет JDK по умолчанию, предлагаемый в Azure.</span><span class="sxs-lookup"><span data-stu-id="8e49e-245">Deploy the default JDK which is offered by Azure</span></span>
         * <span data-ttu-id="8e49e-246">Развернуть сторонний пакет JDK из раскрывающегося списка дополнительных пакетов JDK, доступных в Azure.</span><span class="sxs-lookup"><span data-stu-id="8e49e-246">Deploy a 3rd party JDK from a drop-down list of additional JDKs which are available on Azure</span></span>
         * <span data-ttu-id="8e49e-247">Развернуть пользовательский пакет JDK, который должен быть упакован в виде ZIP-файла и быть общедоступным или находиться в учетной записи хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="8e49e-247">Deploy a custom JDK, which must be packaged as a ZIP file and either publicly available or in your Azure storage account</span></span>
        
      ![Вкладка JDK в окне создания контейнера приложения][11b]

   <span data-ttu-id="8e49e-249">i.</span><span class="sxs-lookup"><span data-stu-id="8e49e-249">i.</span></span> <span data-ttu-id="8e49e-250">После завершения всех описанных выше действий диалоговое окно "Новый контейнер веб-приложения" должно выглядеть примерно так, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="8e49e-250">Once you have completed all of the above steps, the New Web App Container dialog box should resemble the following illustration:</span></span>
      
      ![Создание контейнера приложения][14]
   
   <span data-ttu-id="8e49e-252">j.</span><span class="sxs-lookup"><span data-stu-id="8e49e-252">j.</span></span> <span data-ttu-id="8e49e-253">Нажмите кнопку **ОК** , чтобы создать контейнер веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="8e49e-253">Click **OK** to complete the creation of your new Web App container.</span></span>
       
      <span data-ttu-id="8e49e-254">Подождите несколько секунд. Когда список контейнеров веб-приложений обновится, созданный контейнер веб-приложения должен быть выбран в списке.</span><span class="sxs-lookup"><span data-stu-id="8e49e-254">Wait a few seconds for the list of the Web App containers to be refreshed, and your newly-created web app container should now be selected in the list.</span></span>

6. <span data-ttu-id="8e49e-255">Теперь все готово для начального развертывания веб-приложения в Azure. Нажмите кнопку **ОК**, чтобы развернуть приложение Java в выбранный контейнер веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="8e49e-255">You are now ready to complete the initial deployment of your Web App to Azure; click **OK** to deploy your Java application to the selected Web App container.</span></span> <span data-ttu-id="8e49e-256">По умолчанию приложение будет развернуто в подкаталог сервера приложений.</span><span class="sxs-lookup"><span data-stu-id="8e49e-256">By default, your application will be deployed as a subdirectory of the application server.</span></span> <span data-ttu-id="8e49e-257">Чтобы развернуть приложение в качестве корневого приложения, установите флажок **Deploy to root** (Развернуть в корень) перед нажатием кнопки **ОК**.</span><span class="sxs-lookup"><span data-stu-id="8e49e-257">If you want it to be deployed as the root application, check the **Deploy to root** checkbox before clicking **OK**.</span></span>
   
   ![Развертывание в Azure][15]

7. <span data-ttu-id="8e49e-259">После этого вы должны увидеть представление **Журнал действий Azure** , в котором будет отображаться состояние развертывания веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="8e49e-259">Next, you should see the **Azure Activity Log** view, which will indicate the deployment status of your Web App.</span></span>
   
   ![Индикатор хода выполнения][16]
   
   <span data-ttu-id="8e49e-261">Процесс развертывания веб-приложения в Azure занимает всего несколько секунд.</span><span class="sxs-lookup"><span data-stu-id="8e49e-261">The process of deploying your Web App to Azure should take only a few seconds to complete.</span></span> <span data-ttu-id="8e49e-262">Когда процесс будет завершен, вы увидите ссылку **Published** (Опубликовано) в колонке **Status** (Состояние).</span><span class="sxs-lookup"><span data-stu-id="8e49e-262">When your application is ready, you will see a link named **Published** in the **Status** column.</span></span> <span data-ttu-id="8e49e-263">При щелчке по ссылке вы перейдете на домашнюю страницу развернутого веб-приложения. Вы также можете найти свое веб-приложение, выполнив действия, описанные в следующем разделе.</span><span class="sxs-lookup"><span data-stu-id="8e49e-263">When you click the link, it will take you to your deployed Web App's home page, or you can use the steps in the following section to browse to your web app.</span></span>

### <a name="browsing-to-your-web-app-on-azure"></a><span data-ttu-id="8e49e-264">Переход к веб-приложению в Azure</span><span class="sxs-lookup"><span data-stu-id="8e49e-264">Browsing to your Web App on Azure</span></span>
<span data-ttu-id="8e49e-265">Чтобы перейти к веб-приложению в Azure, можно использовать представление **Azure Explorer**.</span><span class="sxs-lookup"><span data-stu-id="8e49e-265">To browse to your Web App on Azure, you can use the **Azure Explorer** view.</span></span>

<span data-ttu-id="8e49e-266">Если представление **Обозреватель Azure** еще не открыто, его можно открыть, щелкнув меню **View** (Представление) в IntelliJ и последовательно выбрав **Tool Windows** (Окна инструментов) и **Service Explorer** (Обозреватель служб).</span><span class="sxs-lookup"><span data-stu-id="8e49e-266">If the **Azure Explorer** view is not already open, you can open it by clicking then **View** menu in IntelliJ, then click **Tool Windows**, and then click **Service Explorer**.</span></span> <span data-ttu-id="8e49e-267">Если ранее вы не вошли в систему, вам будет предложено это сделать.</span><span class="sxs-lookup"><span data-stu-id="8e49e-267">If you have not previously logged in, it will prompt you to do so.</span></span>

<span data-ttu-id="8e49e-268">Когда представление **Azure Explorer** откроется, выполните следующие действия, чтобы перейти к своему веб-приложению:</span><span class="sxs-lookup"><span data-stu-id="8e49e-268">When the **Azure Explorer** view is displayed, follow these steps to browse to your Web App:</span></span> 

1. <span data-ttu-id="8e49e-269">Разверните узел **Azure** .</span><span class="sxs-lookup"><span data-stu-id="8e49e-269">Expand the **Azure** node.</span></span>
2. <span data-ttu-id="8e49e-270">Разверните узел **Web Apps** (Веб-приложения).</span><span class="sxs-lookup"><span data-stu-id="8e49e-270">Expand the **Web Apps** node.</span></span> 
3. <span data-ttu-id="8e49e-271">Щелкните правой кнопкой мыши необходимое веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="8e49e-271">Right-click the desired Web App.</span></span>
4. <span data-ttu-id="8e49e-272">В открывшемся контекстном меню выберите пункт **Открыть в браузере**.</span><span class="sxs-lookup"><span data-stu-id="8e49e-272">When the context menu appears, click **Open in Browser**.</span></span>
   
   ![Просмотр веб-приложения][17]

### <a name="updating-your-web-app"></a><span data-ttu-id="8e49e-274">Обновление веб-приложения</span><span class="sxs-lookup"><span data-stu-id="8e49e-274">Updating your web app</span></span>
<span data-ttu-id="8e49e-275">Обновить существующее и запущенное веб-приложение Azure быстро и просто. Сделать это можно двумя способами:</span><span class="sxs-lookup"><span data-stu-id="8e49e-275">Updating an existing running Azure Web App is a quick and easy process, and you have two options for updating:</span></span>

* <span data-ttu-id="8e49e-276">Можно обновить развертывание существующего веб-приложения Java.</span><span class="sxs-lookup"><span data-stu-id="8e49e-276">You can update the deployment of an existing Java Web App.</span></span>
* <span data-ttu-id="8e49e-277">Можно опубликовать дополнительное приложение Java в тот же контейнер веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="8e49e-277">You can publish an additional Java application to the same Web App Container.</span></span>

<span data-ttu-id="8e49e-278">Процесс в каждом случае идентичен и занимает несколько секунд.</span><span class="sxs-lookup"><span data-stu-id="8e49e-278">In either case, the process is identical and takes only a few seconds:</span></span>

1. <span data-ttu-id="8e49e-279">В обозревателе проектов IntelliJ щелкните правой кнопкой мыши приложение Java, которое вы хотите обновить или добавить в существующий контейнер веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="8e49e-279">In the IntelliJ project explorer, right-click the Java application you want to update or add to an existing Web App Container.</span></span>
2. <span data-ttu-id="8e49e-280">В контекстном меню выберите **Azure**, а затем щелкните **Опубликовать как веб-приложение Azure**.</span><span class="sxs-lookup"><span data-stu-id="8e49e-280">When the context menu appears, select **Azure** and then **Publish as Azure Web App...**</span></span>
3. <span data-ttu-id="8e49e-281">Так как ранее вы уже вошли в систему, вы увидите список существующих контейнеров веб-приложений.</span><span class="sxs-lookup"><span data-stu-id="8e49e-281">Since you have already logged in previously, you will see a list of your existing Web App containers.</span></span> <span data-ttu-id="8e49e-282">Выберите контейнер, в котором вы хотите опубликовать или повторно опубликовать приложение Java, и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="8e49e-282">Select the one you want to publish or re-publish your Java application to and click **OK**.</span></span>

<span data-ttu-id="8e49e-283">Через несколько секунд в представлении **Журнал действий Azure** состояние обновленного развертывания изменится на **Опубликовано**, и вы сможете проверить свое обновленное приложение в веб-браузере.</span><span class="sxs-lookup"><span data-stu-id="8e49e-283">A few seconds later, the **Azure Activity Log** view will show your updated deployment as **Published** and you will be able to verify your updated application in a web browser.</span></span>

### <a name="starting-stopping-or-restarting-an-existing-web-app"></a><span data-ttu-id="8e49e-284">Запуск, остановка или перезапуск существующего веб-приложения</span><span class="sxs-lookup"><span data-stu-id="8e49e-284">Starting, stopping, or restarting an existing web app</span></span>
<span data-ttu-id="8e49e-285">Запустить или остановить существующий контейнер веб-приложения Azure (включая все развернутые в нем приложения Java) можно в представлении **Обозреватель Azure** .</span><span class="sxs-lookup"><span data-stu-id="8e49e-285">To start or stop an existing Azure Web App container, (including all the deployed Java applications in it), you can use the **Azure Explorer** view.</span></span>

<span data-ttu-id="8e49e-286">Если представление **Обозреватель Azure** еще не открыто, его можно открыть, щелкнув меню **View** (Представление) в IntelliJ и последовательно выбрав **Tool Windows** (Окна инструментов) и **Service Explorer** (Обозреватель служб).</span><span class="sxs-lookup"><span data-stu-id="8e49e-286">If the **Azure Explorer** view is not already open, you can open it by clicking then **View** menu in IntelliJ, then click **Tool Windows**, and then click **Service Explorer**.</span></span> <span data-ttu-id="8e49e-287">Если ранее вы не вошли в систему, вам будет предложено это сделать.</span><span class="sxs-lookup"><span data-stu-id="8e49e-287">If you have not previously logged in, it will prompt you to do so.</span></span>

<span data-ttu-id="8e49e-288">Когда представление **Azure Explorer** откроется, выполните следующие действия для запуска или остановки веб-приложения:</span><span class="sxs-lookup"><span data-stu-id="8e49e-288">When the **Azure Explorer** view is displayed, follow these steps to start or stop your Web App:</span></span> 

1. <span data-ttu-id="8e49e-289">Разверните узел **Azure** .</span><span class="sxs-lookup"><span data-stu-id="8e49e-289">Expand the **Azure** node.</span></span>
2. <span data-ttu-id="8e49e-290">Разверните узел **Web Apps** (Веб-приложения).</span><span class="sxs-lookup"><span data-stu-id="8e49e-290">Expand the **Web Apps** node.</span></span> 
3. <span data-ttu-id="8e49e-291">Щелкните правой кнопкой мыши необходимое веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="8e49e-291">Right-click the desired Web App.</span></span>
4. <span data-ttu-id="8e49e-292">В открывшемся контекстном меню выберите **Запустить**, **Остановить** или **Перезапустить**.</span><span class="sxs-lookup"><span data-stu-id="8e49e-292">When the context menu appears, click **Start**, **Stop**, or **Restart**.</span></span> <span data-ttu-id="8e49e-293">Обратите внимание, что доступные меню контекстно зависимы, поэтому можно только остановить веб-приложение или запустить веб-приложение, которое в данный момент не запущено.</span><span class="sxs-lookup"><span data-stu-id="8e49e-293">Note that the menu choices are context-aware, so you can only stop a running web app or start a web app which is not currently running.</span></span>
   
   ![Остановка веб-приложения][18]

## <a name="next-steps"></a><span data-ttu-id="8e49e-295">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8e49e-295">Next steps</span></span>

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

<span data-ttu-id="8e49e-296">Дополнительные сведения о создании веб-приложений Azure см. в разделе [Обзор веб-приложений].</span><span class="sxs-lookup"><span data-stu-id="8e49e-296">For additional information about creating Azure Web Apps, see the [Web Apps Overview].</span></span>

<!-- URL List -->

[набора средств Azure для IntelliJ]: azure-toolkit-for-intellij.md
[Обзор веб-приложений]: /azure/app-service/app-service-web-overview
[Apache Tomcat]: http://tomcat.apache.org/
[Jetty]: http://www.eclipse.org/jetty/

<!-- IMG List -->

[01]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/01-Web-Page.png
[02]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/02-File-New-Project.png
[03a]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/03-New-Project-Dialog.png
[03b]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/03-New-Project-SDK-Dialog.png
[04]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/04-New-Project-Dialog.png
[05a]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/05-Open-Module-Settings.png
[05b]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/05-Project-Structure-Dialog.png
[05c]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/05-Open-Index-Page.png
[06]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/06-Azure-Publish-Context-Menu.png
[07]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/07-Azure-Log-In-Dialog.png
[08]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/08-Manage-Subscriptions.png
[09]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/09-App-Containers.png
[10]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/10-Add-App-Container.png
[11a]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/11-New-App-Container.png
[11b]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/11-New-App-Container-JDK-Tab.png
[12]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/12-New-Resource-Group.png
[13]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/13-New-App-Service-Plan.png
[14]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/14-New-App-Container.png
[15]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/15-Deploy-To-Azure.png
[16]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/16-Progress-Indicator.png
[17]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/17-Browse-Web-App.png
[18]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/18-Stop-Web-App.png

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
