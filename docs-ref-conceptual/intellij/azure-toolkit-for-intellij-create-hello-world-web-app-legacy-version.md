---
title: "Создание веб-приложения Hello World для Azure с помощью набора средств для IntelliJ предыдущих версий"
description: "В этом руководстве показано, как с помощью набора средств Azure для IntelliJ версии 3.0.6 (или более ранней) создать веб-приложение Hello World для Azure."
services: app-service
documentationcenter: java
author: selvasingh
manager: routlaw
editor: 
ms.assetid: 
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: multiple
ms.devlang: java
ms.topic: article
ms.date: 11/15/2017
ms.author: robmcm;asirveda
ms.openlocfilehash: aa0db81ffc9ff3fe44cf3d58a5b77ee447cdb1d1
ms.sourcegitcommit: 613c1ffd2e0279fc7a96fca98aa1809563f52ee1
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/18/2017
---
# <a name="create-a-hello-world-web-app-for-azure-using-the-legacy-toolkit-for-intellij"></a><span data-ttu-id="6fefc-103">Создание веб-приложения Hello World для Azure с помощью набора средств для IntelliJ предыдущих версий</span><span class="sxs-lookup"><span data-stu-id="6fefc-103">Create a Hello World web app for Azure using the legacy toolkit for IntelliJ</span></span>

<span data-ttu-id="6fefc-104">В этом руководстве показано, как создать базовое приложение Hello World для Azure и развернуть его как веб-приложение с помощью [средств Azure для IntelliJ] версии 3.0.6 (или более ранней).</span><span class="sxs-lookup"><span data-stu-id="6fefc-104">This tutorial shows how to create and deploy a basic Hello World application to Azure as a web app by using version 3.0.6 (or earlier) of the [Azure Toolkit for IntelliJ].</span></span>

> [!NOTE]
>
> <span data-ttu-id="6fefc-105">Дополнительные сведения о версии, в которой используются [средства Azure для Eclipse], см. в статье [Создание веб-приложения Azure (цен. категория "Базовый") с помощью Eclipse][eclipse-hello-world].</span><span class="sxs-lookup"><span data-stu-id="6fefc-105">For a version of this article that uses the [Azure Toolkit for Eclipse], see [Create a Hello World web app for Azure using Eclipse][eclipse-hello-world].</span></span>
>

> [!IMPORTANT]
> 
> <span data-ttu-id="6fefc-106">Набор средств Azure для IntelliJ обновлен в августе 2017 года. В него добавлен другой рабочий процесс.</span><span class="sxs-lookup"><span data-stu-id="6fefc-106">The Azure Toolkit for IntelliJ was updated in August 2017 with a different workflow.</span></span> <span data-ttu-id="6fefc-107">В этой статье описывается, как создать веб-приложение Hello World с помощью набора средств Azure для IntelliJ версии 3.0.6 (или более ранней).</span><span class="sxs-lookup"><span data-stu-id="6fefc-107">This article illustrates creating a Hello World web app by using version 3.0.6 (or earlier) of the Azure Toolkit for IntelliJ.</span></span> <span data-ttu-id="6fefc-108">Если вы используете набор средств версии 3.0.7 (или более поздней), необходимо выполнить действия, описанные в руководстве по [созданию веб-приложения Hello World для Azure в IntelliJ][Updated Version].</span><span class="sxs-lookup"><span data-stu-id="6fefc-108">If you are using the version 3.0.7 (or later) of the toolkit, you will need to follow the steps in [Create a Hello World web app for Azure in IntelliJ][Updated Version].</span></span>
>

<span data-ttu-id="6fefc-109">После завершения этого учебника приложение при просмотре в веб-браузере будет выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="6fefc-109">When you have completed this tutorial, your application will look similar to the following illustration when you view it in a web browser:</span></span>

![Предварительный просмотр приложения Hello World][01]

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="create-a-new-web-app-project"></a><span data-ttu-id="6fefc-111">Создание проекта веб-приложения</span><span class="sxs-lookup"><span data-stu-id="6fefc-111">Create a new web app project</span></span>

1. <span data-ttu-id="6fefc-112">Запустите IntelliJ и войдите в свою учетную запись Azure, следуя инструкциям из статьи [Инструкции по входу для набора средств Azure для IntelliJ][intelliJ-sign-in-instructions].</span><span class="sxs-lookup"><span data-stu-id="6fefc-112">Start IntelliJ, and sign into your Azure account by using the instructions in the [Azure Sign In Instructions for the Azure Toolkit for IntelliJ][intelliJ-sign-in-instructions] article.</span></span>

1. <span data-ttu-id="6fefc-113">Щелкните меню **File** (Файл), выберите команду **New** (Создать), а затем — **Project** (Проект).</span><span class="sxs-lookup"><span data-stu-id="6fefc-113">Click the **File** menu, then click **New**, and then click **Project**.</span></span>
   
   ![Файл > Создать > Проект][02]

2. <span data-ttu-id="6fefc-115">В диалоговом окне **New Project** (Создание проекта) выберите **Java**, а затем установите флажок **Web Application** (Веб-приложение) и нажмите кнопку **New** (Создать), чтобы добавить пакет SDK проекта.</span><span class="sxs-lookup"><span data-stu-id="6fefc-115">In the **New Project** dialog box, select **Java**, then **Web Application**, and then click **New** to add a Project SDK.</span></span>
   
   ![Диалоговое окно "Новый проект"][03a]
   
3. <span data-ttu-id="6fefc-117">В диалоговом окне "Select Home Directory for JDK" (Выбор корневого каталога для JDK) выберите папку для установки JDK, затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="6fefc-117">In the Select Home Directory for JDK dialog box, select the folder where your JDK is installed, and then click **OK**.</span></span> <span data-ttu-id="6fefc-118">Нажмите кнопку **Next** (Далее) в диалоговом окне "New Project" (Создание проекта), чтобы продолжить.</span><span class="sxs-lookup"><span data-stu-id="6fefc-118">Click **Next** in the New Project dialog box to continue.</span></span>
   
   ![Указание корневого каталога JDK][03b]

4. <span data-ttu-id="6fefc-120">Укажите имя проекта **Java-Web-App-On-Azure** и нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="6fefc-120">For purposes of this tutorial, name the project **Java-Web-App-On-Azure**, and then click **Finish**.</span></span>
   
   ![Диалоговое окно "Новый проект"][04]

5. <span data-ttu-id="6fefc-122">В представлении обозревателя проектов IntelliJ разверните **Java-Web-App-On-Azure**, а затем разверните **web** и дважды щелкните **index.jsp**.</span><span class="sxs-lookup"><span data-stu-id="6fefc-122">Within IntelliJ's Project Explorer view, expand **Java-Web-App-On-Azure**, then expand **web**, and then double-click **index.jsp**.</span></span>
   
   ![Открытие страницы индексации][05c]

6. <span data-ttu-id="6fefc-124">При открытии в IntelliJ файла index.jsp добавьте код для динамического отображения фразы **Hello World!**</span><span class="sxs-lookup"><span data-stu-id="6fefc-124">When your index.jsp file opens in IntelliJ, add in text to dynamically display **Hello World!**</span></span> <span data-ttu-id="6fefc-125">в существующий элемент `<body>`.</span><span class="sxs-lookup"><span data-stu-id="6fefc-125">within the existing `<body>` element.</span></span> <span data-ttu-id="6fefc-126">Обновленное содержимое элемента `<body>` должно выглядеть так:</span><span class="sxs-lookup"><span data-stu-id="6fefc-126">Your updated `<body>` content should resemble the following example:</span></span>
   
   ```java
   <body><b><% out.println("Hello World!"); %></b></body>
   ```

7. <span data-ttu-id="6fefc-127">Сохраните index.jsp.</span><span class="sxs-lookup"><span data-stu-id="6fefc-127">Save index.jsp.</span></span>

## <a name="deploy-your-web-app-to-azure"></a><span data-ttu-id="6fefc-128">Развертывание веб-приложения в Azure</span><span class="sxs-lookup"><span data-stu-id="6fefc-128">Deploy your web app to Azure</span></span>

<span data-ttu-id="6fefc-129">Есть несколько способов, с помощью которых можно развернуть веб-приложение Java в Azure.</span><span class="sxs-lookup"><span data-stu-id="6fefc-129">There are several ways by which you can deploy a Java web app to Azure.</span></span> <span data-ttu-id="6fefc-130">В этом учебнике описывается один из самых простых: ваше приложение будет развернуто в контейнер веб-приложения Azure — для этого не нужно выбирать особый тип проекта и не требуются дополнительные инструменты.</span><span class="sxs-lookup"><span data-stu-id="6fefc-130">This tutorial describes one of the simplest: your application will be deployed to an Azure Web App Container - no special project type nor additional tools are needed.</span></span> <span data-ttu-id="6fefc-131">JDK и программное обеспечение веб-контейнера будут предоставлены Azure, поэтому нет необходимости загружать их самостоятельно. Все, что вам нужно — ваше веб-приложение Java.</span><span class="sxs-lookup"><span data-stu-id="6fefc-131">The JDK and the web container software will be provided for you by Azure, so there is no need to upload your own; all you need is your Java Web App.</span></span> <span data-ttu-id="6fefc-132">В результате процесс публикации приложения занимает несколько секунд, а не минут.</span><span class="sxs-lookup"><span data-stu-id="6fefc-132">As a result, the publishing process for your application will take seconds, not minutes.</span></span>

<span data-ttu-id="6fefc-133">Прежде чем публиковать приложение, необходимо сначала настроить параметры модуля.</span><span class="sxs-lookup"><span data-stu-id="6fefc-133">Before you publish your application, you first need to configure your module settings.</span></span> <span data-ttu-id="6fefc-134">Для этого выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="6fefc-134">To do so, use the following steps:</span></span>

1. <span data-ttu-id="6fefc-135">Щелкните правой кнопкой мыши по проекту **Java-Web-App-On-Azure** в обозревателе проектов IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="6fefc-135">In IntelliJ's Project Explorer, right-click the **Java-Web-App-On-Azure** project.</span></span> <span data-ttu-id="6fefc-136">В открывшемся контекстном меню щелкните **Open Module Settings** (Открыть параметры модуля).</span><span class="sxs-lookup"><span data-stu-id="6fefc-136">When the context menu appears, click **Open Module Settings**.</span></span>

   ![Открытие параметров модуля][05a]

2. <span data-ttu-id="6fefc-138">В отобразившемся диалоговом окне "Project Structure" (Структура проекта) выполните следующее.</span><span class="sxs-lookup"><span data-stu-id="6fefc-138">When the Project Structure dialog box appears:</span></span>

   <span data-ttu-id="6fefc-139">а.</span><span class="sxs-lookup"><span data-stu-id="6fefc-139">a.</span></span> <span data-ttu-id="6fefc-140">В списке **Project Settings** (Параметры проекта) щелкните **Artifacts** (Артефакты).</span><span class="sxs-lookup"><span data-stu-id="6fefc-140">Click **Artifacts** in the list of **Project Settings**.</span></span>

   <span data-ttu-id="6fefc-141">b.</span><span class="sxs-lookup"><span data-stu-id="6fefc-141">b.</span></span> <span data-ttu-id="6fefc-142">Измените имя артефакта в поле **Name** (Имя) таким образом, чтобы оно не содержало пробелы или специальные знаки. Это необходимо, так как имя будет использоваться в универсальном коде ресурса (URI).</span><span class="sxs-lookup"><span data-stu-id="6fefc-142">Change the artifact name in the **Name** box so that it doesn't contain whitespace or special characters; this is necessary since the name will be used in the Uniform Resource Identifier (URI).</span></span>

   <span data-ttu-id="6fefc-143">В.</span><span class="sxs-lookup"><span data-stu-id="6fefc-143">c.</span></span> <span data-ttu-id="6fefc-144">Измените значение параметра **Type** (Тип) на **Web Application: Archive** (Веб-приложение: архив).</span><span class="sxs-lookup"><span data-stu-id="6fefc-144">Change the **Type** to **Web Application: Archive**.</span></span>

   <span data-ttu-id="6fefc-145">d.</span><span class="sxs-lookup"><span data-stu-id="6fefc-145">d.</span></span> <span data-ttu-id="6fefc-146">Нажмите кнопку **OK**, чтобы закрыть диалоговое окно "Project Structure" (Структура проекта).</span><span class="sxs-lookup"><span data-stu-id="6fefc-146">Click **OK** to close the Project Structure dialog box.</span></span>

   ![Открытие параметров модуля][05b]

<span data-ttu-id="6fefc-148">После настройки параметров модуля можно опубликовать приложение в Azure, выполнив следующие действия.</span><span class="sxs-lookup"><span data-stu-id="6fefc-148">When you have configured your module settings, you can publish your application to Azure by using the following steps:</span></span>

1. <span data-ttu-id="6fefc-149">Щелкните правой кнопкой мыши по проекту **Java-Web-App-On-Azure** в обозревателе проектов IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="6fefc-149">In IntelliJ's Project Explorer, right-click the **Java-Web-App-On-Azure** project.</span></span> <span data-ttu-id="6fefc-150">В контекстном меню выберите **Azure**, а затем щелкните **Publish as Azure Web App** (Опубликовать как веб-приложение Azure).</span><span class="sxs-lookup"><span data-stu-id="6fefc-150">When the context menu appears, select **Azure**, and then click **Publish as Azure Web App...**</span></span>
   
   ![Контекстное меню публикации в Azure][06]

2. <span data-ttu-id="6fefc-152">Если вы еще не вошли в Azure из IntelliJ, появится запрос на вход в учетную запись Azure.</span><span class="sxs-lookup"><span data-stu-id="6fefc-152">If you have not already signed in to Azure from IntelliJ, you will be prompted to sign in to your Azure account.</span></span> <span data-ttu-id="6fefc-153">При наличии нескольких учетных записей Azure некоторые запросы во время входа в систему могут отображаться несколько раз, даже если они выглядят одинаковыми.</span><span class="sxs-lookup"><span data-stu-id="6fefc-153">(If you have multiple Azure accounts, some of the prompts during the sign-in process may be shown more than once, even if they appear to be the same.</span></span> <span data-ttu-id="6fefc-154">Если это происходит, выполните вход согласно указаниям.</span><span class="sxs-lookup"><span data-stu-id="6fefc-154">When this happens, continue to follow the sign-in instructions.)</span></span>
   
   ![Диалоговое окно входа в Azure][07]

3. <span data-ttu-id="6fefc-156">После успешного входа в учетную запись Azure в диалоговом окне **Управление подписками** отобразится список подписок, связанных с вашими учетными данными.</span><span class="sxs-lookup"><span data-stu-id="6fefc-156">After you have successfully signed in to your Azure account, the **Manage Subscriptions** dialog box will display a list of subscriptions that are associated with your credentials.</span></span> <span data-ttu-id="6fefc-157">(Если список содержит несколько подписок и вы будете работать только с некоторыми из них, снимите флажки для подписок, которые не будете использовать.) После выбора подписок щелкните **Закрыть**.</span><span class="sxs-lookup"><span data-stu-id="6fefc-157">(If there are multiple subscriptions listed and you want to work with only a specific subset of them, you may optionally uncheck the subscriptions you don't want to use.) When you have selected your subscriptions, click **Close**.</span></span>
   
   ![Управление подписками][08]

4. <span data-ttu-id="6fefc-159">При открытии диалогового окна **Deploy to Azure Web App Container** (Развертывание в контейнер веб-приложения Azure) в нем будут показаны все контейнеры веб-приложений, созданные ранее. Если вы не создали ни одного контейнера, список будет пустым.</span><span class="sxs-lookup"><span data-stu-id="6fefc-159">When the **Deploy to Azure Web App Container** dialog box appears, it will display any Web App containers that you have previously created; if you have not created any containers, the list will be empty.</span></span>
   
   ![Контейнеры приложений][09]

5. <span data-ttu-id="6fefc-161">Если вы не создавали контейнер веб-приложения Azure или хотите опубликовать приложение в новый контейнер, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="6fefc-161">If you have not created an Azure Web App Container before, or if you would like to publish your application to a new container, use the following steps.</span></span> <span data-ttu-id="6fefc-162">В противном случае выберите существующий контейнер веб-приложения и перейдите к шагу 6 ниже.</span><span class="sxs-lookup"><span data-stu-id="6fefc-162">Otherwise, select an existing Web App Container and skip to step 6 below.</span></span>
   
   <span data-ttu-id="6fefc-163">а.</span><span class="sxs-lookup"><span data-stu-id="6fefc-163">a.</span></span> <span data-ttu-id="6fefc-164">Щелкните символ **+**.</span><span class="sxs-lookup"><span data-stu-id="6fefc-164">Click the **+** sign.</span></span>
      
      ![Добавление контейнера приложения][10]

   <span data-ttu-id="6fefc-166">b.</span><span class="sxs-lookup"><span data-stu-id="6fefc-166">b.</span></span> <span data-ttu-id="6fefc-167">Откроется окно **Новый контейнер веб-приложения** , которым мы воспользуемся для нескольких следующих шагов.</span><span class="sxs-lookup"><span data-stu-id="6fefc-167">The **New Web App Container** dialog box will be displayed, which will be used for the next several steps.</span></span>
      
      ![Создание контейнера приложения][11a]
   
   <span data-ttu-id="6fefc-169">c.</span><span class="sxs-lookup"><span data-stu-id="6fefc-169">c.</span></span> <span data-ttu-id="6fefc-170">Укажите **метку DNS** для контейнера веб-приложения. Она образует метку листа DNS для URL-адреса узла веб-приложения в Azure.</span><span class="sxs-lookup"><span data-stu-id="6fefc-170">Enter a **DNS Label** for your Web App Container; this will form the leaf DNS label of the host URL for your web application in Azure.</span></span> <span data-ttu-id="6fefc-171">(Примечание. Имя должно быть доступным и соответствовать требованиям к именованию веб-приложений Azure.)</span><span class="sxs-lookup"><span data-stu-id="6fefc-171">Note that the name must be available and conform to Azure Web App naming requirements.</span></span>

   <span data-ttu-id="6fefc-172">d.</span><span class="sxs-lookup"><span data-stu-id="6fefc-172">d.</span></span> <span data-ttu-id="6fefc-173">В раскрывающемся меню **Веб-контейнер** выберите для своего приложения соответствующее программное обеспечение.</span><span class="sxs-lookup"><span data-stu-id="6fefc-173">In the **Web Container** drop-down menu, select the appropriate software for your application.</span></span>
      
      <span data-ttu-id="6fefc-174">На данный момент можно выбрать Tomcat 8, Tomcat 7 или Jetty 9.</span><span class="sxs-lookup"><span data-stu-id="6fefc-174">Currently, you can choose from Tomcat 8, Tomcat 7 or Jetty 9.</span></span> <span data-ttu-id="6fefc-175">Последний дистрибутив выбранного программного обеспечения, предоставленный Azure, будет запущен в последнем дистрибутиве JDK 8, созданном Oracle и предоставленном Azure.</span><span class="sxs-lookup"><span data-stu-id="6fefc-175">A recent distribution of the selected software will be provided by Azure, and it will run on a recent distribution of JDK 8 created by Oracle and provided by Azure.</span></span>

   <span data-ttu-id="6fefc-176">д.</span><span class="sxs-lookup"><span data-stu-id="6fefc-176">e.</span></span> <span data-ttu-id="6fefc-177">В раскрывающемся меню **Подписка** выберите подписку, которую вы хотите использовать для этого развертывания.</span><span class="sxs-lookup"><span data-stu-id="6fefc-177">In the **Subscription** drop-down menu, select the subscription you want to use for this deployment.</span></span>

   <span data-ttu-id="6fefc-178">f.</span><span class="sxs-lookup"><span data-stu-id="6fefc-178">f.</span></span> <span data-ttu-id="6fefc-179">В раскрывающемся меню **Группа ресурсов** выберите группу ресурсов, с которой вы хотите связать свое веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="6fefc-179">In the **Resource Group** drop-down menu, select the Resource Group with which you want to associate your Web App.</span></span> <span data-ttu-id="6fefc-180">(Группы ресурсов Azure позволяют сгруппировать связанные ресурсы, чтобы, например, удалить их одновременно.)</span><span class="sxs-lookup"><span data-stu-id="6fefc-180">(Azure Resource Groups allow you to group related resources together so that, for example, they can be deleted together.)</span></span>
      
      <span data-ttu-id="6fefc-181">Можно выбрать существующую группу ресурсов (если она есть) и перейти к шагу g ниже, или создать новую, выполнив следующее.</span><span class="sxs-lookup"><span data-stu-id="6fefc-181">You can select an existing Resource Group (if you have any) and skip to step g below, or use the following steps to create a new Resource Group:</span></span>
      
      * <span data-ttu-id="6fefc-182">Из раскрывающегося меню **Группы ресурсов** выберите пункт **&lt;&lt;Создать новую группу ресурсов&gt;&gt;**.</span><span class="sxs-lookup"><span data-stu-id="6fefc-182">Select **&lt;&lt; Create new Resource Group &gt;&gt;** in the **Resource Group** drop-down menu.</span></span>
      * <span data-ttu-id="6fefc-183">Откроется диалоговое окно **Новая группа ресурсов** :</span><span class="sxs-lookup"><span data-stu-id="6fefc-183">The **New Resource Group** dialog box will be displayed:</span></span>
        
         ![Создание группы ресурсов][12]

      * <span data-ttu-id="6fefc-185">В текстовое поле **Name** (Имя) введите имя новой группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="6fefc-185">In the **Name** textbox, specify a name for your new Resource Group.</span></span>
      * <span data-ttu-id="6fefc-186">В раскрывающемся меню **Region** (Регион) выберите расположение центра обработки данных Azure для группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="6fefc-186">In the **Region** drop-down menu, select the appropriate Azure data center location for your Resource Group.</span></span>
      * <span data-ttu-id="6fefc-187">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="6fefc-187">Click **OK**.</span></span>

   <span data-ttu-id="6fefc-188">ж.</span><span class="sxs-lookup"><span data-stu-id="6fefc-188">g.</span></span> <span data-ttu-id="6fefc-189">В раскрывающемся меню **План службы приложений** перечислены планы службы приложений, связанные с выбранной группой ресурсов.</span><span class="sxs-lookup"><span data-stu-id="6fefc-189">The **App Service Plan** drop-down menu lists the app service plans that are associated with the Resource Group that you selected.</span></span> <span data-ttu-id="6fefc-190">В плане службы приложений указываются такие сведения, как расположение веб-приложения, ценовая категория и размер вычислительной операции.</span><span class="sxs-lookup"><span data-stu-id="6fefc-190">(An App Service Plan specifies information such as the location of your Web App, the pricing tier and the compute instance size.</span></span> <span data-ttu-id="6fefc-191">Один план службы приложений можно использовать для нескольких веб-приложений, поэтому он поддерживается отдельно от развертывания конкретного веб-приложения.)</span><span class="sxs-lookup"><span data-stu-id="6fefc-191">A single App Service Plan can be used for multiple Web Apps, which is why it is maintained separately from a specific Web App deployment.)</span></span>
      
      <span data-ttu-id="6fefc-192">Можно выбрать существующий план службы приложений (если он есть) и перейти к шагу h ниже, или создать новый, выполнив следующее.</span><span class="sxs-lookup"><span data-stu-id="6fefc-192">You can select an existing App Service Plan (if you have any) and skip to step h below, or use the following steps to create a new App Service Plan:</span></span>
      
      * <span data-ttu-id="6fefc-193">Из раскрывающегося меню **План службы приложений** выберите пункт **&lt;&lt;Создать новый план службы приложений&gt;&gt;**.</span><span class="sxs-lookup"><span data-stu-id="6fefc-193">Select **&lt;&lt; Create new App Service Plan &gt;&gt;** in the **App Service Plan** drop-down menu.</span></span>
      * <span data-ttu-id="6fefc-194">Откроется диалоговое окно **Новый план службы приложений** :</span><span class="sxs-lookup"><span data-stu-id="6fefc-194">The **New App Service Plan** dialog box will be displayed:</span></span>
        
         ![Новый план службы приложений][13]

      * <span data-ttu-id="6fefc-196">В текстовое поле **Name** (Имя) введите имя нового плана службы приложений.</span><span class="sxs-lookup"><span data-stu-id="6fefc-196">In the **Name** textbox, specify a name for your new App Service Plan.</span></span>
      * <span data-ttu-id="6fefc-197">В раскрывающемся меню **Location** (Расположение) выберите расположение центра обработки данных Azure для плана.</span><span class="sxs-lookup"><span data-stu-id="6fefc-197">In the **Location** drop-down menu, select the appropriate Azure data center location for the plan.</span></span>
      * <span data-ttu-id="6fefc-198">В раскрывающемся меню **Pricing Tier** (Ценовая категория) выберите соответствующую ценовую категорию для плана.</span><span class="sxs-lookup"><span data-stu-id="6fefc-198">In the **Pricing Tier** drop-down menu, select the appropriate pricing for the plan.</span></span> <span data-ttu-id="6fefc-199">Для тестирования можно выбрать категорию **Бесплатный**.</span><span class="sxs-lookup"><span data-stu-id="6fefc-199">For testing purposes you can choose **Free**.</span></span>
      * <span data-ttu-id="6fefc-200">В раскрывающемся меню **Instance Size** (Размер экземпляра) выберите для плана соответствующий размер экземпляра.</span><span class="sxs-lookup"><span data-stu-id="6fefc-200">In the **Instance Size** drop-down menu, select the appropriate instance size for the plan.</span></span> <span data-ttu-id="6fefc-201">Для тестирования можно выбрать **Маленький**.</span><span class="sxs-lookup"><span data-stu-id="6fefc-201">For testing purposes you can choose **Small**.</span></span>
      * <span data-ttu-id="6fefc-202">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="6fefc-202">Click **OK**.</span></span>

   <span data-ttu-id="6fefc-203">h.</span><span class="sxs-lookup"><span data-stu-id="6fefc-203">h.</span></span> <span data-ttu-id="6fefc-204">(Необязательно.) По умолчанию Azure автоматически развернет последний дистрибутив Java 8 в ваш контейнер веб-приложения в качестве виртуальной машины Java.</span><span class="sxs-lookup"><span data-stu-id="6fefc-204">(Optional) By default, a recent distribution of Java 8 will be automatically deployed as your JVM by Azure to your web app container.</span></span> <span data-ttu-id="6fefc-205">Тем не менее можно выбрать другую версию и дистрибутив виртуальной машины Java.</span><span class="sxs-lookup"><span data-stu-id="6fefc-205">However, you can select a different version and distribution of the JVM.</span></span> <span data-ttu-id="6fefc-206">Для этого выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="6fefc-206">To do so, use the following steps:</span></span>
      
      * <span data-ttu-id="6fefc-207">Щелкните вкладку **JDK** в диалоговом окне **New Web App Container** (Создание контейнера веб-приложения).</span><span class="sxs-lookup"><span data-stu-id="6fefc-207">Click the **JDK** tab in the **New Web App Container** dialog box.</span></span>
      * <span data-ttu-id="6fefc-208">Можно выбрать один из следующих вариантов:</span><span class="sxs-lookup"><span data-stu-id="6fefc-208">You can choose from one of the following options:</span></span>
        
         * <span data-ttu-id="6fefc-209">Развернуть пакет JDK по умолчанию, предлагаемый в Azure.</span><span class="sxs-lookup"><span data-stu-id="6fefc-209">Deploy the default JDK which is offered by Azure</span></span>
         * <span data-ttu-id="6fefc-210">Развернуть сторонний пакет JDK из раскрывающегося списка дополнительных пакетов JDK, доступных в Azure.</span><span class="sxs-lookup"><span data-stu-id="6fefc-210">Deploy a 3rd party JDK from a drop-down list of additional JDKs which are available on Azure</span></span>
         * <span data-ttu-id="6fefc-211">Развернуть пользовательский пакет JDK, который должен быть упакован в виде ZIP-файла и быть общедоступным или находиться в учетной записи хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="6fefc-211">Deploy a custom JDK, which must be packaged as a ZIP file and either publicly available or in your Azure storage account</span></span>
        
      ![Вкладка JDK в окне создания контейнера приложения][11b]

   <span data-ttu-id="6fefc-213">i.</span><span class="sxs-lookup"><span data-stu-id="6fefc-213">i.</span></span> <span data-ttu-id="6fefc-214">После завершения всех описанных выше действий диалоговое окно "Новый контейнер веб-приложения" должно выглядеть примерно так, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="6fefc-214">Once you have completed all of the above steps, the New Web App Container dialog box should resemble the following illustration:</span></span>
      
      ![Создание контейнера приложения][14]
   
   <span data-ttu-id="6fefc-216">j.</span><span class="sxs-lookup"><span data-stu-id="6fefc-216">j.</span></span> <span data-ttu-id="6fefc-217">Нажмите кнопку **ОК** , чтобы создать контейнер веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="6fefc-217">Click **OK** to complete the creation of your new Web App container.</span></span>
       
      <span data-ttu-id="6fefc-218">Подождите несколько секунд. Когда список контейнеров веб-приложений обновится, созданный контейнер веб-приложения должен быть выбран в списке.</span><span class="sxs-lookup"><span data-stu-id="6fefc-218">Wait a few seconds for the list of the Web App containers to be refreshed, and your newly-created web app container should now be selected in the list.</span></span>

6. <span data-ttu-id="6fefc-219">Теперь все готово для начального развертывания веб-приложения в Azure. Нажмите кнопку **ОК**, чтобы развернуть приложение Java в выбранный контейнер веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="6fefc-219">You are now ready to complete the initial deployment of your Web App to Azure; click **OK** to deploy your Java application to the selected Web App container.</span></span> <span data-ttu-id="6fefc-220">По умолчанию приложение будет развернуто в подкаталог сервера приложений.</span><span class="sxs-lookup"><span data-stu-id="6fefc-220">By default, your application will be deployed as a subdirectory of the application server.</span></span> <span data-ttu-id="6fefc-221">Чтобы развернуть приложение в качестве корневого приложения, установите флажок **Deploy to root** (Развернуть в корень) перед нажатием кнопки **ОК**.</span><span class="sxs-lookup"><span data-stu-id="6fefc-221">If you want it to be deployed as the root application, check the **Deploy to root** checkbox before clicking **OK**.</span></span>
   
   ![Развертывание в Azure][15]

7. <span data-ttu-id="6fefc-223">После этого вы должны увидеть представление **Журнал действий Azure** , в котором будет отображаться состояние развертывания веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="6fefc-223">Next, you should see the **Azure Activity Log** view, which will indicate the deployment status of your Web App.</span></span>
   
   ![Индикатор хода выполнения][16]
   
   <span data-ttu-id="6fefc-225">Процесс развертывания веб-приложения в Azure занимает всего несколько секунд.</span><span class="sxs-lookup"><span data-stu-id="6fefc-225">The process of deploying your Web App to Azure should take only a few seconds to complete.</span></span> <span data-ttu-id="6fefc-226">Когда процесс будет завершен, вы увидите ссылку **Published** (Опубликовано) в колонке **Status** (Состояние).</span><span class="sxs-lookup"><span data-stu-id="6fefc-226">When your application is ready, you will see a link named **Published** in the **Status** column.</span></span> <span data-ttu-id="6fefc-227">При щелчке по ссылке вы перейдете на домашнюю страницу развернутого веб-приложения. Вы также можете найти свое веб-приложение, выполнив действия, описанные в следующем разделе.</span><span class="sxs-lookup"><span data-stu-id="6fefc-227">When you click the link, it will take you to your deployed Web App's home page, or you can use the steps in the following section to browse to your web app.</span></span>

## <a name="browsing-to-your-web-app-on-azure"></a><span data-ttu-id="6fefc-228">Переход к веб-приложению в Azure</span><span class="sxs-lookup"><span data-stu-id="6fefc-228">Browsing to your Web App on Azure</span></span>

<span data-ttu-id="6fefc-229">Чтобы перейти к веб-приложению в Azure, можно использовать представление **Azure Explorer**.</span><span class="sxs-lookup"><span data-stu-id="6fefc-229">To browse to your Web App on Azure, you can use the **Azure Explorer** view.</span></span>

<span data-ttu-id="6fefc-230">Если представление **Обозреватель Azure** еще не открыто, его можно открыть, щелкнув меню **View** (Представление) в IntelliJ и последовательно выбрав **Tool Windows** (Окна инструментов) и **Service Explorer** (Обозреватель служб).</span><span class="sxs-lookup"><span data-stu-id="6fefc-230">If the **Azure Explorer** view is not already open, you can open it by clicking then **View** menu in IntelliJ, then click **Tool Windows**, and then click **Service Explorer**.</span></span> <span data-ttu-id="6fefc-231">Если ранее вы не вошли в систему, вам будет предложено это сделать.</span><span class="sxs-lookup"><span data-stu-id="6fefc-231">If you have not previously logged in, it will prompt you to do so.</span></span>

<span data-ttu-id="6fefc-232">Когда представление **Azure Explorer** откроется, выполните следующие действия, чтобы перейти к своему веб-приложению:</span><span class="sxs-lookup"><span data-stu-id="6fefc-232">When the **Azure Explorer** view is displayed, follow these steps to browse to your Web App:</span></span> 

1. <span data-ttu-id="6fefc-233">Разверните узел **Azure** .</span><span class="sxs-lookup"><span data-stu-id="6fefc-233">Expand the **Azure** node.</span></span>
2. <span data-ttu-id="6fefc-234">Разверните узел **Web Apps** (Веб-приложения).</span><span class="sxs-lookup"><span data-stu-id="6fefc-234">Expand the **Web Apps** node.</span></span> 
3. <span data-ttu-id="6fefc-235">Щелкните правой кнопкой мыши необходимое веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="6fefc-235">Right-click the desired Web App.</span></span>
4. <span data-ttu-id="6fefc-236">В открывшемся контекстном меню выберите пункт **Открыть в браузере**.</span><span class="sxs-lookup"><span data-stu-id="6fefc-236">When the context menu appears, click **Open in Browser**.</span></span>
   
   ![Просмотр веб-приложения][17]

## <a name="updating-your-web-app"></a><span data-ttu-id="6fefc-238">Обновление веб-приложения</span><span class="sxs-lookup"><span data-stu-id="6fefc-238">Updating your web app</span></span>

<span data-ttu-id="6fefc-239">Обновить существующее и запущенное веб-приложение Azure быстро и просто. Сделать это можно двумя способами:</span><span class="sxs-lookup"><span data-stu-id="6fefc-239">Updating an existing running Azure Web App is a quick and easy process, and you have two options for updating:</span></span>

* <span data-ttu-id="6fefc-240">Можно обновить развертывание существующего веб-приложения Java.</span><span class="sxs-lookup"><span data-stu-id="6fefc-240">You can update the deployment of an existing Java Web App.</span></span>
* <span data-ttu-id="6fefc-241">Можно опубликовать дополнительное приложение Java в тот же контейнер веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="6fefc-241">You can publish an additional Java application to the same Web App Container.</span></span>

<span data-ttu-id="6fefc-242">Процесс в каждом случае идентичен и занимает несколько секунд.</span><span class="sxs-lookup"><span data-stu-id="6fefc-242">In either case, the process is identical and takes only a few seconds:</span></span>

1. <span data-ttu-id="6fefc-243">В обозревателе проектов IntelliJ щелкните правой кнопкой мыши приложение Java, которое вы хотите обновить или добавить в существующий контейнер веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="6fefc-243">In the IntelliJ project explorer, right-click the Java application you want to update or add to an existing Web App Container.</span></span>
2. <span data-ttu-id="6fefc-244">В контекстном меню выберите **Azure**, а затем щелкните **Опубликовать как веб-приложение Azure**.</span><span class="sxs-lookup"><span data-stu-id="6fefc-244">When the context menu appears, select **Azure** and then **Publish as Azure Web App...**</span></span>
3. <span data-ttu-id="6fefc-245">Так как ранее вы уже вошли в систему, вы увидите список существующих контейнеров веб-приложений.</span><span class="sxs-lookup"><span data-stu-id="6fefc-245">Since you have already logged in previously, you will see a list of your existing Web App containers.</span></span> <span data-ttu-id="6fefc-246">Выберите контейнер, в котором вы хотите опубликовать или повторно опубликовать приложение Java, и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="6fefc-246">Select the one you want to publish or re-publish your Java application to and click **OK**.</span></span>

<span data-ttu-id="6fefc-247">Через несколько секунд в представлении **Журнал действий Azure** состояние обновленного развертывания изменится на **Опубликовано**, и вы сможете проверить свое обновленное приложение в веб-браузере.</span><span class="sxs-lookup"><span data-stu-id="6fefc-247">A few seconds later, the **Azure Activity Log** view will show your updated deployment as **Published** and you will be able to verify your updated application in a web browser.</span></span>

## <a name="starting-stopping-or-restarting-an-existing-web-app"></a><span data-ttu-id="6fefc-248">Запуск, остановка или перезапуск существующего веб-приложения</span><span class="sxs-lookup"><span data-stu-id="6fefc-248">Starting, stopping, or restarting an existing web app</span></span>

<span data-ttu-id="6fefc-249">Запустить или остановить существующий контейнер веб-приложения Azure (включая все развернутые в нем приложения Java) можно в представлении **Обозреватель Azure** .</span><span class="sxs-lookup"><span data-stu-id="6fefc-249">To start or stop an existing Azure Web App container, (including all the deployed Java applications in it), you can use the **Azure Explorer** view.</span></span>

<span data-ttu-id="6fefc-250">Если представление **Обозреватель Azure** еще не открыто, его можно открыть, щелкнув меню **View** (Представление) в IntelliJ и последовательно выбрав **Tool Windows** (Окна инструментов) и **Service Explorer** (Обозреватель служб).</span><span class="sxs-lookup"><span data-stu-id="6fefc-250">If the **Azure Explorer** view is not already open, you can open it by clicking then **View** menu in IntelliJ, then click **Tool Windows**, and then click **Service Explorer**.</span></span> <span data-ttu-id="6fefc-251">Если ранее вы не вошли в систему, вам будет предложено это сделать.</span><span class="sxs-lookup"><span data-stu-id="6fefc-251">If you have not previously logged in, it will prompt you to do so.</span></span>

<span data-ttu-id="6fefc-252">Когда представление **Azure Explorer** откроется, выполните следующие действия для запуска или остановки веб-приложения:</span><span class="sxs-lookup"><span data-stu-id="6fefc-252">When the **Azure Explorer** view is displayed, follow these steps to start or stop your Web App:</span></span> 

1. <span data-ttu-id="6fefc-253">Разверните узел **Azure** .</span><span class="sxs-lookup"><span data-stu-id="6fefc-253">Expand the **Azure** node.</span></span>
2. <span data-ttu-id="6fefc-254">Разверните узел **Web Apps** (Веб-приложения).</span><span class="sxs-lookup"><span data-stu-id="6fefc-254">Expand the **Web Apps** node.</span></span> 
3. <span data-ttu-id="6fefc-255">Щелкните правой кнопкой мыши необходимое веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="6fefc-255">Right-click the desired Web App.</span></span>
4. <span data-ttu-id="6fefc-256">В открывшемся контекстном меню выберите **Запустить**, **Остановить** или **Перезапустить**.</span><span class="sxs-lookup"><span data-stu-id="6fefc-256">When the context menu appears, click **Start**, **Stop**, or **Restart**.</span></span> <span data-ttu-id="6fefc-257">Обратите внимание, что доступные меню контекстно зависимы, поэтому можно только остановить веб-приложение или запустить веб-приложение, которое в данный момент не запущено.</span><span class="sxs-lookup"><span data-stu-id="6fefc-257">Note that the menu choices are context-aware, so you can only stop a running web app or start a web app which is not currently running.</span></span>
   
   ![Остановка веб-приложения][18]

## <a name="next-steps"></a><span data-ttu-id="6fefc-259">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6fefc-259">Next steps</span></span>

[!INCLUDE [azure-toolkit-for-intellij-additional-resources](../includes/azure-toolkit-for-intellij-additional-resources.md)]

<span data-ttu-id="6fefc-260">Дополнительные сведения о создании веб-приложений Azure см. в разделе [Обзор веб-приложений].</span><span class="sxs-lookup"><span data-stu-id="6fefc-260">For additional information about creating Azure Web Apps, see the [Web Apps Overview].</span></span>

<!-- URL List -->

[средств Azure для IntelliJ]: azure-toolkit-for-intellij.md
[средства Azure для Eclipse]: ../eclipse/azure-toolkit-for-eclipse.md
[eclipse-hello-world]: ../eclipse/azure-toolkit-for-eclipse-create-hello-world-web-app.md
[Обзор веб-приложений]: /azure/app-service/app-service-web-overview
[Apache Tomcat]: http://tomcat.apache.org/
[Jetty]: http://www.eclipse.org/jetty/
[Updated Version]: azure-toolkit-for-intellij-create-hello-world-web-app.md
[intelliJ-sign-in-instructions]: azure-toolkit-for-intellij-sign-in-instructions.md

<!-- IMG List -->

[01]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/01-Web-Page.png
[02]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/02-File-New-Project.png
[03a]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/03-New-Project-Dialog.png
[03b]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/03-New-Project-SDK-Dialog.png
[04]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/04-New-Project-Dialog.png
[05a]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/05-Open-Module-Settings.png
[05b]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/05-Project-Structure-Dialog.png
[05c]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/05-Open-Index-Page.png
[06]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/06-Azure-Publish-Context-Menu.png
[07]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/07-Azure-Log-In-Dialog.png
[08]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/08-Manage-Subscriptions.png
[09]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/09-App-Containers.png
[10]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/10-Add-App-Container.png
[11a]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/11-New-App-Container.png
[11b]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/11-New-App-Container-JDK-Tab.png
[12]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/12-New-Resource-Group.png
[13]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/13-New-App-Service-Plan.png
[14]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/14-New-App-Container.png
[15]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/15-Deploy-To-Azure.png
[16]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/16-Progress-Indicator.png
[17]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/17-Browse-Web-App.png
[18]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/18-Stop-Web-App.png
