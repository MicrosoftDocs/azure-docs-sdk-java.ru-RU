---
title: ''
description: В этом руководстве показано, как с помощью набора средств Azure для Eclipse версии 3.0.6 (или более ранней) создать веб-приложение Hello World для Azure.
services: app-service
documentationcenter: java
author: selvasingh
manager: routlaw
editor: ''
ms.assetid: ''
ms.author: robmcm;asirveda
ms.date: 02/01/2018
ms.devlang: java
ms.service: app-service
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: web
ms.openlocfilehash: 8b831f4545be9162d28f8ba86eb7271ffa4391af
ms.sourcegitcommit: 151aaa6ccc64d94ed67f03e846bab953bde15b4a
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/03/2018
ms.locfileid: "28954745"
---
# <a name="create-a-hello-world-web-app-for-azure-using-the-legacy-toolkit-for-eclipse"></a><span data-ttu-id="4aa36-102">Создание веб-приложения Hello World для Azure с помощью набора средств для Eclipse предыдущих версий</span><span class="sxs-lookup"><span data-stu-id="4aa36-102">Create a Hello World web app for Azure using the legacy toolkit for Eclipse</span></span>

<span data-ttu-id="4aa36-103">В этом руководстве показано, как создать базовое приложение Hello World для Azure и развернуть его как веб-приложение с помощью [средств Azure для Eclipse] версии 3.0.6 (или более ранней).</span><span class="sxs-lookup"><span data-stu-id="4aa36-103">This tutorial shows how to create and deploy a basic Hello World application to Azure as a web app by using version 3.0.6 (or earlier) of the [Azure Toolkit for Eclipse].</span></span>

> [!NOTE]
>
> <span data-ttu-id="4aa36-104">Дополнительные сведения о версии, в которой используются [средства Azure для IntelliJ], см. в статье [Создание веб-приложения Azure (цен. категория "Базовый") с помощью IntelliJ][intellij-hello-world].</span><span class="sxs-lookup"><span data-stu-id="4aa36-104">For a version of this article that uses the [Azure Toolkit for IntelliJ], see [Create a Hello World web app for Azure using IntelliJ][intellij-hello-world].</span></span>
>

> [!IMPORTANT]
> 
> <span data-ttu-id="4aa36-105">Набор средств Azure для Eclipse обновлен в августе 2017 года. В него добавлен другой рабочий процесс.</span><span class="sxs-lookup"><span data-stu-id="4aa36-105">The Azure Toolkit for Eclipse was updated in August 2017 with a different workflow.</span></span> <span data-ttu-id="4aa36-106">В этой статье описывается, как создать веб-приложение Hello World с помощью набора средств Azure для Eclipse версии 3.0.6 (или более ранней).</span><span class="sxs-lookup"><span data-stu-id="4aa36-106">This article illustrates creating a Hello World web app by using version 3.0.6 (or earlier) of the Azure Toolkit for Eclipse.</span></span> <span data-ttu-id="4aa36-107">Если вы используете набор средств версии 3.0.7 (или более поздней), необходимо выполнить действия, описанные в руководстве по [созданию веб-приложения Hello World для Azure в Eclipse][Updated Version].</span><span class="sxs-lookup"><span data-stu-id="4aa36-107">If you are using the version 3.0.7 (or later) of the toolkit, you will need to follow the steps in [Create a Hello World web app for Azure in Eclipse][Updated Version].</span></span>
>

<span data-ttu-id="4aa36-108">После завершения этого учебника приложение при просмотре в веб-браузере будет выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="4aa36-108">When you have completed this tutorial, your application will look similar to the following illustration when you view it in a web browser:</span></span>

![Предварительный просмотр приложения Hello World][01]

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="create-a-new-web-app-project"></a><span data-ttu-id="4aa36-110">Создание проекта веб-приложения</span><span class="sxs-lookup"><span data-stu-id="4aa36-110">Create a new web app project</span></span>

1. <span data-ttu-id="4aa36-111">Запустите Eclipse и войдите в свою учетную запись Azure, следуя инструкциям из статьи [Инструкции по входу для набора средств Azure для Eclipse][eclipse-sign-in-instructions].</span><span class="sxs-lookup"><span data-stu-id="4aa36-111">Start Eclipse, and sign into your Azure account by using the instructions in the [Azure Sign In Instructions for the Azure Toolkit for Eclipse][eclipse-sign-in-instructions] article.</span></span>

1. <span data-ttu-id="4aa36-112">Выберите **File** (Файл), **New** (Создать), а затем — **Dynamic Web Project** (Динамический веб-проект).</span><span class="sxs-lookup"><span data-stu-id="4aa36-112">Click **File**, click **New**, and then click **Dynamic Web Project**.</span></span> <span data-ttu-id="4aa36-113">(Если элемента **Динамический веб-проект** нет в списке доступных проектов после выбора пунктов **Файл** и **Создать**, сделайте следующее: последовательно щелкните **Файл**, **Создать**, **Проект...**, разверните узел **Интернет**, щелкните **Dynamic Web Project** (Динамический веб-проект) и нажмите кнопку **Далее**.)</span><span class="sxs-lookup"><span data-stu-id="4aa36-113">(If you don't see **Dynamic Web Project** listed as an available project after clicking **File** and **New**, then do the following: click **File**, click **New**, click **Project...**, expand **Web**, click **Dynamic Web Project**, and click **Next**.)</span></span>

2. <span data-ttu-id="4aa36-114">Для целей данного учебника присвойте проекту имя **MyWebApp**.</span><span class="sxs-lookup"><span data-stu-id="4aa36-114">For purposes of this tutorial, name the project **MyWebApp**.</span></span> <span data-ttu-id="4aa36-115">Экран будет выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="4aa36-115">Your screen will appear similar to the following:</span></span>
   
   ![Создание динамического веб-проекта][02]

3. <span data-ttu-id="4aa36-117">Нажмите кнопку **Готово**</span><span class="sxs-lookup"><span data-stu-id="4aa36-117">Click **Finish**.</span></span>

4. <span data-ttu-id="4aa36-118">В представлении **обозревателя проектов** в Eclipse разверните узел **MyWebApp**.</span><span class="sxs-lookup"><span data-stu-id="4aa36-118">Within Eclipse's **Project Explorer** view, expand **MyWebApp**.</span></span> <span data-ttu-id="4aa36-119">Щелкните правой кнопкой мыши **WebContent**, выберите **Создать**, затем щелкните **JSP File** (JSP-файл).</span><span class="sxs-lookup"><span data-stu-id="4aa36-119">Right-click **WebContent**, click **New**, and then click **JSP File**.</span></span>

5. <span data-ttu-id="4aa36-120">В диалоговом окне **New JSP File** (Новый JSP-файл) укажите имя файла **index.jsp**, оставьте родительскую папку **MyWebApp/WebContent** без изменений, а затем нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="4aa36-120">In the **New JSP File** dialog box, name the file **index.jsp**, keep the parent folder as **MyWebApp/WebContent**, and then click **Next**.</span></span>

6. <span data-ttu-id="4aa36-121">Для нашего примера в диалоговом окне **Select JSP Template** (Выбор шаблона JSP) щелкните **New JSP File (html)** (Создать JSP-файл (html)) и нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="4aa36-121">In the **Select JSP Template** dialog box, for purposes of this tutorial select **New JSP File (html)**, and then click **Finish**.</span></span>

7. <span data-ttu-id="4aa36-122">При открытии в Eclipse файла index.jsp добавьте код для динамического отображения фразы **Hello World!**</span><span class="sxs-lookup"><span data-stu-id="4aa36-122">When your index.jsp file opens in Eclipse, add in text to dynamically display **Hello World!**</span></span> <span data-ttu-id="4aa36-123">в существующий элемент `<body>`.</span><span class="sxs-lookup"><span data-stu-id="4aa36-123">within the existing `<body>` element.</span></span> <span data-ttu-id="4aa36-124">Обновленное содержимое элемента `<body>` должно выглядеть так:</span><span class="sxs-lookup"><span data-stu-id="4aa36-124">Your updated `<body>` content should resemble the following example:</span></span>
   
   ```jsp
   <body><b><% out.println("Hello World!"); %></b></body>
   ```

8. <span data-ttu-id="4aa36-125">Сохраните index.jsp.</span><span class="sxs-lookup"><span data-stu-id="4aa36-125">Save index.jsp.</span></span>

## <a name="deploy-your-web-app-to-azure"></a><span data-ttu-id="4aa36-126">Развертывание веб-приложения в Azure</span><span class="sxs-lookup"><span data-stu-id="4aa36-126">Deploy your web app to Azure</span></span>

<span data-ttu-id="4aa36-127">Существует несколько способов, с помощью которых можно развернуть веб-приложение Java в Azure.</span><span class="sxs-lookup"><span data-stu-id="4aa36-127">There are several ways by which you can deploy a Java web application to Azure.</span></span> <span data-ttu-id="4aa36-128">В этом учебнике описывается один из самых простых: ваше приложение будет развернуто в контейнер веб-приложения Azure — для этого не нужно выбирать особый тип проекта и не требуются дополнительные инструменты.</span><span class="sxs-lookup"><span data-stu-id="4aa36-128">This tutorial describes one of the simplest: your application will be deployed to an Azure Web App Container - no special project type nor additional tools are needed.</span></span> <span data-ttu-id="4aa36-129">JDK и программное обеспечение веб-контейнера будут предоставлены Azure, поэтому нет необходимости загружать их самостоятельно. Все, что вам нужно — ваше веб-приложение Java.</span><span class="sxs-lookup"><span data-stu-id="4aa36-129">The JDK and the web container software will be provided for you by Azure, so there is no need to upload your own; all you need is your Java Web App.</span></span> <span data-ttu-id="4aa36-130">В результате процесс публикации приложения занимает несколько секунд, а не минут.</span><span class="sxs-lookup"><span data-stu-id="4aa36-130">As a result, the publishing process for your application will take seconds, not minutes.</span></span>

1. <span data-ttu-id="4aa36-131">В обозревателе проектов Eclipse щелкните правой кнопкой мыши **MyWebApp**.</span><span class="sxs-lookup"><span data-stu-id="4aa36-131">In Eclipse's Project Explorer, right-click **MyWebApp**.</span></span>

2. <span data-ttu-id="4aa36-132">В контекстном меню выберите **Azure**, затем щелкните **Опубликовать как веб-приложение Azure**.</span><span class="sxs-lookup"><span data-stu-id="4aa36-132">In the context menu, select **Azure**, then click **Publish as Azure Web App...**</span></span>
   
   ![Опубликовать как веб-приложение Azure][03]
   
   <span data-ttu-id="4aa36-134">Кроме того, выбирая проект веб-приложения в обозревателе проектов, вы можете нажать на панели инструментов кнопку с раскрывающимся списком **Опубликовать** и выбрать в списке **Publish as Azure Web App** (Опубликовать как веб-приложение Azure).</span><span class="sxs-lookup"><span data-stu-id="4aa36-134">Alternatively, while your web application project is selected in the Project Explorer, you can click the **Publish** dropdown button on the toolbar and select **Publish as Azure Web App** from there:</span></span>
   
   ![Опубликовать как веб-приложение Azure][14]

3. <span data-ttu-id="4aa36-136">Если вы еще не вошли в систему Azure из Eclipse, появится запрос на вход в учетную запись Azure:</span><span class="sxs-lookup"><span data-stu-id="4aa36-136">If you have not already signed into Azure from Eclipse, you will be prompted to sign into your Azure account:</span></span>
   
   ![Диалоговое окно входа в Azure][04]
   
   <span data-ttu-id="4aa36-138">При наличии нескольких учетных записей Azure некоторые запросы во время входа в систему могут отображаться несколько раз, даже если они выглядят одинаковыми.</span><span class="sxs-lookup"><span data-stu-id="4aa36-138">If you have multiple Azure accounts, some of the prompts during the sign in process may be shown more than once, even if they appear to be the same.</span></span> <span data-ttu-id="4aa36-139">Если это происходит, выполните вход.</span><span class="sxs-lookup"><span data-stu-id="4aa36-139">When this happens, continue following the sign in instructions.</span></span>

4. <span data-ttu-id="4aa36-140">После успешного входа в учетную запись Azure в диалоговом окне **Управление подписками** отобразится список подписок, связанных с вашими учетными данными.</span><span class="sxs-lookup"><span data-stu-id="4aa36-140">After you have successfully signed into your Azure account, the **Manage Subscriptions** dialog box will display a list of subscriptions that are associated with your credentials.</span></span> <span data-ttu-id="4aa36-141">Если список содержит несколько подписок и вы будете работать только с некоторыми из них, снимите флажки с подписок, которые не будете использовать.</span><span class="sxs-lookup"><span data-stu-id="4aa36-141">If there are multiple subscriptions listed and you want to work with only a specific subset of them, you may optionally uncheck the ones you do want to use.</span></span> <span data-ttu-id="4aa36-142">После выбора подписок щелкните **Закрыть**.</span><span class="sxs-lookup"><span data-stu-id="4aa36-142">When you have selected your subscriptions, click **Close**.</span></span>
   
   ![Диалоговое окно управления подписками][05]

5. <span data-ttu-id="4aa36-144">При открытии диалогового окна **Deploy to Azure Web App Container** (Развертывание в контейнер веб-приложения Azure) в нем будут показаны все контейнеры веб-приложений, созданные ранее. Если вы не создали ни одного контейнера, список будет пустым.</span><span class="sxs-lookup"><span data-stu-id="4aa36-144">When the **Deploy to Azure Web App Container** dialog box appears, it will display any Web App containers that you have previously created; if you have not created any containers, the list will be empty.</span></span>
   
   ![Диалоговое окно развертывания в контейнер веб-приложения Azure][06]

6. <span data-ttu-id="4aa36-146">Если вы не создавали контейнер веб-приложения Azure или хотите опубликовать приложение в новый контейнер, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="4aa36-146">If you have not created an Azure Web App Container before, or if you would like to publish your application to a new container, use the following steps.</span></span> <span data-ttu-id="4aa36-147">В противном случае выберите существующий контейнер веб-приложения и перейдите к шагу 7 ниже.</span><span class="sxs-lookup"><span data-stu-id="4aa36-147">Otherwise, select an existing Web App Container and skip to step 7 below.</span></span>
   
   <span data-ttu-id="4aa36-148">a.</span><span class="sxs-lookup"><span data-stu-id="4aa36-148">a.</span></span> <span data-ttu-id="4aa36-149">Нажмите кнопку **Создать**</span><span class="sxs-lookup"><span data-stu-id="4aa36-149">Click **New...**</span></span>
      
      ![Диалоговое окно развертывания в контейнер веб-приложения Azure][15]

   <span data-ttu-id="4aa36-151">Б.</span><span class="sxs-lookup"><span data-stu-id="4aa36-151">b.</span></span> <span data-ttu-id="4aa36-152">Откроется диалоговое окно **New Web App Container** (Новый контейнер веб-приложения):</span><span class="sxs-lookup"><span data-stu-id="4aa36-152">The **New Web App Container** dialog box will be displayed:</span></span>
      
      ![Диалоговое окно нового контейнера веб-приложения][07a]

   <span data-ttu-id="4aa36-154">c.</span><span class="sxs-lookup"><span data-stu-id="4aa36-154">c.</span></span> <span data-ttu-id="4aa36-155">Укажите **метку DNS** для контейнера веб-приложения. Она образует метку листа DNS для URL-адреса узла веб-приложения в Azure.</span><span class="sxs-lookup"><span data-stu-id="4aa36-155">Enter a **DNS Label** for your Web App Container; this will form the leaf DNS label of the host URL for your web application in Azure.</span></span> <span data-ttu-id="4aa36-156">(Примечание. Имя должно быть доступным и соответствовать требованиям к именованию веб-приложений Azure.)</span><span class="sxs-lookup"><span data-stu-id="4aa36-156">(Note that the name must be available and conform to Azure Web App naming requirements.)</span></span>

   <span data-ttu-id="4aa36-157">d.</span><span class="sxs-lookup"><span data-stu-id="4aa36-157">d.</span></span> <span data-ttu-id="4aa36-158">В раскрывающемся меню **Веб-контейнер** выберите для своего приложения соответствующее программное обеспечение.</span><span class="sxs-lookup"><span data-stu-id="4aa36-158">In the **Web Container** drop-down menu, select the appropriate software for your application.</span></span>
      
      <span data-ttu-id="4aa36-159">На данный момент можно выбрать Tomcat 8, Tomcat 7 или Jetty 9.</span><span class="sxs-lookup"><span data-stu-id="4aa36-159">Currently, you can choose from Tomcat 8, Tomcat 7 or Jetty 9.</span></span> <span data-ttu-id="4aa36-160">Последний дистрибутив выбранного программного обеспечения, предоставленный Azure, будет запущен в последнем дистрибутиве JDK 8, созданном Oracle и предоставленном Azure.</span><span class="sxs-lookup"><span data-stu-id="4aa36-160">A recent distribution of the selected software will be provided by Azure, and it will run on a recent distribution of JDK 8 created by Oracle and provided by Azure.</span></span>

   <span data-ttu-id="4aa36-161">д.</span><span class="sxs-lookup"><span data-stu-id="4aa36-161">e.</span></span> <span data-ttu-id="4aa36-162">В раскрывающемся меню **Подписка** выберите подписку, которую вы хотите использовать для этого развертывания.</span><span class="sxs-lookup"><span data-stu-id="4aa36-162">In the **Subscription** drop-down menu, select the subscription you want to use for this deployment.</span></span>

   <span data-ttu-id="4aa36-163">f.</span><span class="sxs-lookup"><span data-stu-id="4aa36-163">f.</span></span> <span data-ttu-id="4aa36-164">В раскрывающемся меню **Группа ресурсов** выберите группу ресурсов, с которой вы хотите связать свое веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="4aa36-164">In the **Resource Group** drop-down menu, select the Resource Group with which you want to associate your Web App.</span></span> <span data-ttu-id="4aa36-165">(Группы ресурсов Azure позволяют сгруппировать связанные ресурсы, чтобы, например, удалить их одновременно.)</span><span class="sxs-lookup"><span data-stu-id="4aa36-165">(Azure Resource Groups allow you to group related resources together so that, for example, they can be deleted together.)</span></span>
      
      <span data-ttu-id="4aa36-166">Можно выбрать существующую группу ресурсов (если она есть) и перейти к шагу g ниже, или создать новую, сделав следующее:</span><span class="sxs-lookup"><span data-stu-id="4aa36-166">You can select an existing Resource Group (if you have any) and skip to step g below, or use the following these steps to create a new Resource Group:</span></span>
      
      * <span data-ttu-id="4aa36-167">Нажмите кнопку **Создать**</span><span class="sxs-lookup"><span data-stu-id="4aa36-167">Click **New...**</span></span>
      * <span data-ttu-id="4aa36-168">Откроется диалоговое окно **Новая группа ресурсов** :</span><span class="sxs-lookup"><span data-stu-id="4aa36-168">The **New Resource Group** dialog box will be displayed:</span></span>
        
          ![Диалоговое окно новой группы ресурсов][08]
      * <span data-ttu-id="4aa36-170">В текстовое поле **Имя** введите имя новой группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="4aa36-170">In the the **Name** textbox, specify a name for your new Resource Group.</span></span>
      * <span data-ttu-id="4aa36-171">В раскрывающемся меню **Регион** выберите расположение центра обработки данных Azure для группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="4aa36-171">In the the **Region** drop-down menu, select the appropriate Azure data center location for your Resource Group.</span></span>
      * <span data-ttu-id="4aa36-172">Необязательно. По умолчанию Azure автоматически развернет последний дистрибутив Java 8 в ваш контейнер веб-приложения в качестве виртуальной машины Java.</span><span class="sxs-lookup"><span data-stu-id="4aa36-172">OPTIONAL: By default, a recent distribution of Java 8 will be deployed by Azure automatically to your web app container as your JVM.</span></span> <span data-ttu-id="4aa36-173">Тем не менее, если это нужно веб-приложению, то можно указать другую версию и дистрибутив виртуальной машины Java.</span><span class="sxs-lookup"><span data-stu-id="4aa36-173">However, you can specify a different version and distribution of the JVM if your Web App requires it.</span></span> <span data-ttu-id="4aa36-174">Чтобы указать пакет JDK для веб-приложения, щелкните **JDK** и выберите один из следующих параметров.</span><span class="sxs-lookup"><span data-stu-id="4aa36-174">To specify the JDK for your Web App, click the **JDK** tab, and select one of the following options:</span></span>
         * <span data-ttu-id="4aa36-175">**Deploy the default JDK offered by Azure Web Apps service** (Развернуть пакет JDK по умолчанию, предлагаемый службой веб-приложений Azure). Этот параметр позволит развернуть последний дистрибутив Java 8.</span><span class="sxs-lookup"><span data-stu-id="4aa36-175">**Deploy the default JDK offered by Azure Web Apps service**: This option will deploy a recent distribution of Java 8.</span></span>
         * <span data-ttu-id="4aa36-176">**Deploy a 3rd party JDK available on Azure** (Развернуть сторонний пакет JDK, доступный в Azure). Этот параметр позволяет выбрать из списка пакетов JDK, предоставляемых Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="4aa36-176">**Deploy a 3rd party JDK available on Azure**: This option allows you to choose from the list of JDKs which are provided by Microsoft Azure.</span></span>
         * <span data-ttu-id="4aa36-177">**Deploy my own JDK from this download location** (Развернуть собственный пакет JDK из этого расположения для скачивания). Этот параметр позволяет указать собственный дистрибутив JDK, который должен быть упакован в ZIP-файл и передан либо в общедоступное расположение для скачивания, либо в учетную запись хранения Azure, к которой у вас есть доступ.</span><span class="sxs-lookup"><span data-stu-id="4aa36-177">**Deploy my own JDK from this download location**: This option allows you to specify your own JDK distribution, which must be packaged as a ZIP file and uploaded to either a publicly available download location or an Azure storage account for which you have access.</span></span>
          
         ![Диалоговое окно нового контейнера веб-приложения][07b]

   <span data-ttu-id="4aa36-179">ж.</span><span class="sxs-lookup"><span data-stu-id="4aa36-179">g.</span></span> <span data-ttu-id="4aa36-180">Последовательно выберите **ОК**.</span><span class="sxs-lookup"><span data-stu-id="4aa36-180">Click **OK**.</span></span>

   <span data-ttu-id="4aa36-181">h.</span><span class="sxs-lookup"><span data-stu-id="4aa36-181">h.</span></span> <span data-ttu-id="4aa36-182">В раскрывающемся меню **План службы приложений** перечислены планы службы приложений, связанные с выбранной группой ресурсов.</span><span class="sxs-lookup"><span data-stu-id="4aa36-182">The **App Service Plan** drop-down menu lists the app service plans that are associated with the Resource Group that you selected.</span></span> <span data-ttu-id="4aa36-183">(В планах службы приложений указываются такие сведения, как расположение веб-приложения, ценовая категория и размер вычислительной операции.</span><span class="sxs-lookup"><span data-stu-id="4aa36-183">(App Service Plans specify information such as the location of your Web App, the pricing tier and the compute instance size.</span></span> <span data-ttu-id="4aa36-184">Один план службы приложений можно использовать для нескольких веб-приложений, поэтому он поддерживается отдельно от развертывания конкретного веб-приложения.)</span><span class="sxs-lookup"><span data-stu-id="4aa36-184">A single App Service Plan can be used for multiple Web Apps, which is why it is maintained separately from a specific Web App deployment.)</span></span>
      
       You can select an existing App Service Plan (if you have any) and skip to step h below, or use the following these steps to create a new App Service Plan:
      
      * <span data-ttu-id="4aa36-185">Нажмите кнопку **Создать**</span><span class="sxs-lookup"><span data-stu-id="4aa36-185">Click **New...**</span></span>
      * <span data-ttu-id="4aa36-186">Откроется диалоговое окно **Новый план службы приложений** :</span><span class="sxs-lookup"><span data-stu-id="4aa36-186">The **New App Service Plan** dialog box will be displayed:</span></span>
        
          ![Диалоговое окно нового плана службы приложений][09]
      * <span data-ttu-id="4aa36-188">В текстовое поле **Имя** введите имя нового плана службы приложений.</span><span class="sxs-lookup"><span data-stu-id="4aa36-188">In the the **Name** textbox, specify a name for your new App Service Plan.</span></span>
      * <span data-ttu-id="4aa36-189">В раскрывающемся меню **Расположение** выберите расположение центра обработки данных Azure для плана.</span><span class="sxs-lookup"><span data-stu-id="4aa36-189">In the the **Location** drop-down menu, select the appropriate Azure data center location for the plan.</span></span>
      * <span data-ttu-id="4aa36-190">В раскрывающемся меню **Ценовая категория** выберите соответствующую ценовую категорию для плана.</span><span class="sxs-lookup"><span data-stu-id="4aa36-190">In the the **Pricing Tier** drop-down menu, select the appropriate pricing for the plan.</span></span> <span data-ttu-id="4aa36-191">Для тестирования можно выбрать категорию **Бесплатный**.</span><span class="sxs-lookup"><span data-stu-id="4aa36-191">For testing purposes you can choose **Free**.</span></span>
      * <span data-ttu-id="4aa36-192">В раскрывающемся меню **Размер экземпляра** выберите для плана соответствующий размер экземпляра.</span><span class="sxs-lookup"><span data-stu-id="4aa36-192">In the the **Instance Size** drop-down menu, select the appropriate instance size for the plan.</span></span> <span data-ttu-id="4aa36-193">Для тестирования можно выбрать **Маленький**.</span><span class="sxs-lookup"><span data-stu-id="4aa36-193">For testing purposes you can choose **Small**.</span></span>

   <span data-ttu-id="4aa36-194">i.</span><span class="sxs-lookup"><span data-stu-id="4aa36-194">i.</span></span> <span data-ttu-id="4aa36-195">После завершения всех описанных выше действий диалоговое окно "Новый контейнер веб-приложения" должно выглядеть примерно так, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="4aa36-195">Once you have completed all of the above steps, the New Web App Container dialog box should resemble the following illustration:</span></span>
      
      ![Диалоговое окно нового контейнера веб-приложения][10]

   <span data-ttu-id="4aa36-197">j.</span><span class="sxs-lookup"><span data-stu-id="4aa36-197">j.</span></span> <span data-ttu-id="4aa36-198">Нажмите кнопку **ОК** , чтобы создать контейнер веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="4aa36-198">Click **OK** to complete the creation of your new Web App container.</span></span>
       
      <span data-ttu-id="4aa36-199">Подождите несколько секунд. Когда список контейнеров веб-приложений обновится, созданный контейнер веб-приложения должен быть выбран в списке.</span><span class="sxs-lookup"><span data-stu-id="4aa36-199">Wait a few seconds for the list of the Web App containers to be refreshed, and your newly-created web app container should now be selected in the list.</span></span>

7. <span data-ttu-id="4aa36-200">Теперь все готово для начального развертывания вашего веб-приложения в Azure:</span><span class="sxs-lookup"><span data-stu-id="4aa36-200">You are now ready to complete the initial deployment of your Web App to Azure:</span></span>
   
   ![Диалоговое окно развертывания в контейнер веб-приложения Azure][11]
   
   <span data-ttu-id="4aa36-202">Нажмите кнопку **ОК** , чтобы развернуть приложение Java в выбранный контейнер веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="4aa36-202">Click **OK** to deploy your Java application to the selected Web App container.</span></span>
   
   <span data-ttu-id="4aa36-203">По умолчанию приложение будет развернуто в подкаталог сервера приложений.</span><span class="sxs-lookup"><span data-stu-id="4aa36-203">By default, your application will be deployed as a subdirectory of the application server.</span></span> <span data-ttu-id="4aa36-204">Чтобы развернуть приложение в качестве корневого приложения, установите флажок **Deploy to root** (Развернуть в корень) перед нажатием кнопки **ОК**.</span><span class="sxs-lookup"><span data-stu-id="4aa36-204">If you want it to be deployed as the root application, check the **Deploy to root** checkbox before clicking **OK**.</span></span>

8. <span data-ttu-id="4aa36-205">После этого вы должны увидеть представление **Журнал действий Azure** , в котором будет отображаться состояние развертывания веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="4aa36-205">Next, you should see the **Azure Activity Log** view, which will indicate the deployment status of your Web App.</span></span>
   
   ![Журнал действий Azure][12]
   
   <span data-ttu-id="4aa36-207">Процесс развертывания веб-приложения в Azure занимает всего несколько секунд.</span><span class="sxs-lookup"><span data-stu-id="4aa36-207">The process of deploying your Web App to Azure should take only a few seconds to complete.</span></span> <span data-ttu-id="4aa36-208">Когда процесс будет завершен, вы увидите ссылку **Опубликовано** in the **Состояние** .</span><span class="sxs-lookup"><span data-stu-id="4aa36-208">When your application ready, you will see a link named **Published** in the **Status** column.</span></span> <span data-ttu-id="4aa36-209">Если щелкнуть по ней, откроется домашняя страница развернутого веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="4aa36-209">When you click the link, it will take you to your deployed Web App's home page.</span></span>

## <a name="updating-your-web-app"></a><span data-ttu-id="4aa36-210">Обновление веб-приложения</span><span class="sxs-lookup"><span data-stu-id="4aa36-210">Updating your web app</span></span>

<span data-ttu-id="4aa36-211">Обновить существующее и запущенное веб-приложение Azure быстро и просто. Сделать это можно двумя способами:</span><span class="sxs-lookup"><span data-stu-id="4aa36-211">Updating an existing running Azure Web App is a quick and easy process, and you have two options for updating:</span></span>

* <span data-ttu-id="4aa36-212">Можно обновить развертывание существующего веб-приложения Java.</span><span class="sxs-lookup"><span data-stu-id="4aa36-212">You can update the deployment of an existing Java Web App.</span></span>
* <span data-ttu-id="4aa36-213">Можно опубликовать дополнительное приложение Java в тот же контейнер веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="4aa36-213">You can publish an additional Java application to the same Web App Container.</span></span>

<span data-ttu-id="4aa36-214">Процесс в каждом случае идентичен и занимает несколько секунд.</span><span class="sxs-lookup"><span data-stu-id="4aa36-214">In either case, the process is identical and takes only a few seconds:</span></span>

1. <span data-ttu-id="4aa36-215">В обозревателе проектов Eclipse щелкните правой кнопкой мыши приложение Java, которое вы хотите обновить или добавить в существующий контейнер веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="4aa36-215">In the Eclipse project explorer, right-click the Java application you want to update or add to an existing Web App Container.</span></span>

2. <span data-ttu-id="4aa36-216">В контекстном меню выберите **Azure**, а затем щелкните **Опубликовать как веб-приложение Azure**.</span><span class="sxs-lookup"><span data-stu-id="4aa36-216">When the context menu appears, select **Azure** and then **Publish as Azure Web App...**</span></span>

3. <span data-ttu-id="4aa36-217">Так как ранее вы уже вошли в систему, вы увидите список существующих контейнеров веб-приложений.</span><span class="sxs-lookup"><span data-stu-id="4aa36-217">Since you have already logged in previously, you will see a list of your existing Web App containers.</span></span> <span data-ttu-id="4aa36-218">Выберите контейнер, в котором вы хотите опубликовать или повторно опубликовать приложение Java, и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="4aa36-218">Select the one you want to publish or re-publish your Java application to and click **OK**.</span></span>

<span data-ttu-id="4aa36-219">Через несколько секунд в представлении **Журнал действий Azure** состояние обновленного развертывания изменится на **Опубликовано**, и вы сможете проверить свое обновленное приложение в веб-браузере.</span><span class="sxs-lookup"><span data-stu-id="4aa36-219">A few seconds later, the **Azure Activity Log** view will show your updated deployment as **Published** and you will be able to verify your updated application in a web browser.</span></span>

## <a name="starting-stopping-or-restarting-an-existing-web-app"></a><span data-ttu-id="4aa36-220">Запуск, остановка или перезапуск существующего веб-приложения</span><span class="sxs-lookup"><span data-stu-id="4aa36-220">Starting, stopping, or restarting an existing web app</span></span>

<span data-ttu-id="4aa36-221">Запустить или остановить существующий контейнер веб-приложения Azure (включая все развернутые в нем приложения Java) можно в представлении **Обозреватель Azure** .</span><span class="sxs-lookup"><span data-stu-id="4aa36-221">To start or stop an existing Azure Web App container, (including all the deployed Java applications in it), you can use the **Azure Explorer** view.</span></span>

<span data-ttu-id="4aa36-222">Если представление **Azure Explorer** еще не открыто, это можно сделать, щелкнув в Eclipse меню **Окно** и последовательно выбрав **Show View** (Показать представление), **Other** (Другие), **Azure**, **Azure Explorer**.</span><span class="sxs-lookup"><span data-stu-id="4aa36-222">If the **Azure Explorer** view is not already open, you can open it by clicking then **Window** menu in Eclipse, then click **Show View**, then **Other...**, then **Azure**, and then click **Azure Explorer**.</span></span> <span data-ttu-id="4aa36-223">Если ранее вы не вошли в систему, вам будет предложено это сделать.</span><span class="sxs-lookup"><span data-stu-id="4aa36-223">If you have not previously logged in, it will prompt you to do so.</span></span>

<span data-ttu-id="4aa36-224">Когда представление **Обозреватель Azure** откроется, выполните следующие действия для запуска или остановки веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="4aa36-224">When the **Azure Explorer** view is displayed, use follow these steps to start or stop your Web App:</span></span> 

1. <span data-ttu-id="4aa36-225">Разверните узел **Azure** .</span><span class="sxs-lookup"><span data-stu-id="4aa36-225">Expand the **Azure** node.</span></span>

2. <span data-ttu-id="4aa36-226">Разверните узел **Web Apps** (Веб-приложения).</span><span class="sxs-lookup"><span data-stu-id="4aa36-226">Expand the **Web Apps** node.</span></span> 

3. <span data-ttu-id="4aa36-227">Щелкните правой кнопкой мыши необходимое веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="4aa36-227">Right-click the desired Web App.</span></span>

4. <span data-ttu-id="4aa36-228">В открывшемся контекстном меню выберите **Запустить**, **Остановить** или **Перезапустить**.</span><span class="sxs-lookup"><span data-stu-id="4aa36-228">When the context menu appears, click **Start**, **Stop**, or **Restart**.</span></span> <span data-ttu-id="4aa36-229">Обратите внимание, что доступные меню контекстно зависимы, поэтому можно только остановить веб-приложение или запустить веб-приложение, которое в данный момент не запущено.</span><span class="sxs-lookup"><span data-stu-id="4aa36-229">Note that the menu choices are context-aware, so you can only stop a running web app or start a web app which is not currently running.</span></span>
   
   ![Остановка существующего веб-приложения][13]

## <a name="next-steps"></a><span data-ttu-id="4aa36-231">Дополнительная информация</span><span class="sxs-lookup"><span data-stu-id="4aa36-231">Next steps</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-additional-resources](../includes/azure-toolkit-for-eclipse-additional-resources.md)]

<span data-ttu-id="4aa36-232">Дополнительные сведения о создании веб-приложений Azure см. в разделе [Обзор веб-приложений].</span><span class="sxs-lookup"><span data-stu-id="4aa36-232">For additional information about creating Azure Web Apps, see the [Web Apps Overview].</span></span>

<!-- URL List -->

[средств Azure для Eclipse]: azure-toolkit-for-eclipse.md
[Azure Toolkit for Eclipse]: azure-toolkit-for-eclipse.md
[средства Azure для IntelliJ]: ../intellij/azure-toolkit-for-intellij.md
[Azure Toolkit for IntelliJ]: ../intellij/azure-toolkit-for-intellij.md
[intellij-hello-world]: ../intellij/azure-toolkit-for-intellij-create-hello-world-web-app.md
[Обзор веб-приложений]: /azure/app-service/app-service-web-overview
[Web Apps Overview]: /azure/app-service/app-service-web-overview
[Apache Tomcat]: http://tomcat.apache.org/
[Jetty]: http://www.eclipse.org/jetty/
[Updated Version]: azure-toolkit-for-eclipse-create-hello-world-web-app.md
[eclipse-sign-in-instructions]: azure-toolkit-for-eclipse-sign-in-instructions.md


<!-- IMG List -->

[01]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version/01-Web-Page.png
[02]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version/02-Dynamic-Web-Project.png
[03]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version/03-Context-Menu.png
[04]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version/04-Log-In-Dialog.png
[05]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version/05-Manage-Subscriptions-Dialog.png
[06]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version/06-Deploy-To-Azure-Web-Container.png
[07a]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version/07a-New-Web-App-Container-Dialog.png
[07b]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version/07b-New-Web-App-Container-Dialog.png
[08]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version/08-New-Resource-Group-Dialog.png
[09]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version/09-New-Service-Plan-Dialog.png
[10]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version/10-Completed-Web-App-Container-Dialog.png
[11]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version/11-Completed-Deploy-Dialog.png
[12]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version/12-Activity-Log-View.png
[13]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version/13-Azure-Explorer-Web-App.png
[14]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version/14-publishDropdownButton.png
[15]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version/15-New-Azure-Web-Container.png
