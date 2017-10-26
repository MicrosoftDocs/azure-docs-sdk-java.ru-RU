---
title: "Создание веб-приложения Azure (цен. категория \"Базовый\") с помощью Eclipse"
description: "В этом учебнике показано, как с помощью набора средств Azure для Eclipse создать веб-приложение Hello World для Azure."
services: app-service
documentationcenter: java
author: selvasingh
manager: routlaw
editor: 
ms.assetid: 20d41e88-9eab-462e-8ee3-89da71e7a33f
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: multiple
ms.devlang: java
ms.topic: article
ms.date: 10/19/2017
ms.author: robmcm;asirveda
ms.openlocfilehash: dcab31ad99fb79a91374d95c2b8b0d9d10346f5f
ms.sourcegitcommit: 7f8538e41c833deb69c300ad3431a431136a1f3e
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/24/2017
---
# <a name="create-a-basic-azure-web-app-using-eclipse"></a><span data-ttu-id="9c4ed-103">Создание веб-приложения Azure (цен. категория "Базовый") с помощью Eclipse</span><span class="sxs-lookup"><span data-stu-id="9c4ed-103">Create a basic Azure web app using Eclipse</span></span>
<span data-ttu-id="9c4ed-104">В этом учебнике показано, как создать базовое приложение Hello World для Azure и развернуть его как веб-приложение с помощью [средств Azure для Eclipse].</span><span class="sxs-lookup"><span data-stu-id="9c4ed-104">This tutorial shows how to create and deploy a basic Hello World application to Azure as a Web App by using the [Azure Toolkit for Eclipse].</span></span> <span data-ttu-id="9c4ed-105">Для простоты мы приводим базовый пример на JSP, но схожие действия подойдут и для сервлета Java, если речь идет о развертывании в Azure.</span><span class="sxs-lookup"><span data-stu-id="9c4ed-105">A basic JSP example is shown for simplicity, but similar steps would be appropriate for a Java servlet, as far as Azure deployment is concerned.</span></span>

<span data-ttu-id="9c4ed-106">После завершения этого учебника приложение при просмотре в веб-браузере будет выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="9c4ed-106">When you have completed this tutorial, your application will look similar to the following illustration when you view it in a web browser:</span></span>

![Предварительный просмотр приложения Hello World][01]

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="to-create-a-hello-world-application"></a><span data-ttu-id="9c4ed-108">Создание приложения Hello World</span><span class="sxs-lookup"><span data-stu-id="9c4ed-108">To create a Hello World application</span></span>
<span data-ttu-id="9c4ed-109">Сначала необходимо создать проект Java.</span><span class="sxs-lookup"><span data-stu-id="9c4ed-109">First, we'll start off with creating a Java project.</span></span>

1. <span data-ttu-id="9c4ed-110">Запустите Eclipse и в меню **Файл** щелкните **Создать**, а затем — **Dynamic Web Project** (Динамический веб-проект).</span><span class="sxs-lookup"><span data-stu-id="9c4ed-110">Start Eclipse, and at the menu click **File**, click **New**, and then click **Dynamic Web Project**.</span></span> <span data-ttu-id="9c4ed-111">(Если элемента **Динамический веб-проект** нет в списке доступных проектов после выбора пунктов **Файл** и **Создать**, сделайте следующее: последовательно щелкните **Файл**, **Создать**, **Проект...**, разверните узел **Интернет**, щелкните **Dynamic Web Project** (Динамический веб-проект) и нажмите кнопку **Далее**.)</span><span class="sxs-lookup"><span data-stu-id="9c4ed-111">(If you don't see **Dynamic Web Project** listed as an available project after clicking **File** and **New**, then do the following: click **File**, click **New**, click **Project...**, expand **Web**, click **Dynamic Web Project**, and click **Next**.)</span></span>

2. <span data-ttu-id="9c4ed-112">Для целей данного учебника присвойте проекту имя **MyWebApp**.</span><span class="sxs-lookup"><span data-stu-id="9c4ed-112">For purposes of this tutorial, name the project **MyWebApp**.</span></span> <span data-ttu-id="9c4ed-113">Экран будет выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="9c4ed-113">Your screen will appear similar to the following:</span></span>
   
   ![Создание динамического веб-проекта][02]

3. <span data-ttu-id="9c4ed-115">Нажмите кнопку **Готово**</span><span class="sxs-lookup"><span data-stu-id="9c4ed-115">Click **Finish**.</span></span>

4. <span data-ttu-id="9c4ed-116">В представлении обозревателя проектов в Eclipse разверните узел **MyWebApp**.</span><span class="sxs-lookup"><span data-stu-id="9c4ed-116">Within Eclipse's Project Explorer view, expand **MyWebApp**.</span></span> <span data-ttu-id="9c4ed-117">Щелкните правой кнопкой мыши **WebContent**, выберите **Создать**, затем щелкните **JSP File** (JSP-файл).</span><span class="sxs-lookup"><span data-stu-id="9c4ed-117">Right-click **WebContent**, click **New**, and then click **JSP File**.</span></span>

5. <span data-ttu-id="9c4ed-118">В диалоговом окне **New JSP File** (Новый JSP-файл) укажите имя файла **index.jsp**, оставьте родительскую папку **MyWebApp/WebContent** без изменений, а затем нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="9c4ed-118">In the **New JSP File** dialog box, name the file **index.jsp**, keep the parent folder as **MyWebApp/WebContent**, and then click **Next**.</span></span>

6. <span data-ttu-id="9c4ed-119">Для нашего примера в диалоговом окне **Select JSP Template** (Выбор шаблона JSP) щелкните **New JSP File (html)** (Создать JSP-файл (html)) и нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="9c4ed-119">In the **Select JSP Template** dialog box, for purposes of this tutorial select **New JSP File (html)**, and then click **Finish**.</span></span>

7. <span data-ttu-id="9c4ed-120">При открытии в Eclipse файла index.jsp добавьте код для динамического отображения фразы **Hello World!**</span><span class="sxs-lookup"><span data-stu-id="9c4ed-120">When your index.jsp file opens in Eclipse, add in text to dynamically display **Hello World!**</span></span> <span data-ttu-id="9c4ed-121">в существующий элемент `<body>`.</span><span class="sxs-lookup"><span data-stu-id="9c4ed-121">within the existing `<body>` element.</span></span> <span data-ttu-id="9c4ed-122">Обновленное содержимое элемента `<body>` должно выглядеть так:</span><span class="sxs-lookup"><span data-stu-id="9c4ed-122">Your updated `<body>` content should resemble the following example:</span></span>
   
   ```jsp
   <body><b><% out.println("Hello World!"); %></b></body>
   ```

8. <span data-ttu-id="9c4ed-123">Сохраните index.jsp.</span><span class="sxs-lookup"><span data-stu-id="9c4ed-123">Save index.jsp.</span></span>

## <a name="to-deploy-your-application-to-an-azure-web-app-container"></a><span data-ttu-id="9c4ed-124">Развертывание приложения в контейнере веб-приложения Azure</span><span class="sxs-lookup"><span data-stu-id="9c4ed-124">To deploy your application to an Azure Web App Container</span></span>
<span data-ttu-id="9c4ed-125">Существует несколько способов, с помощью которых можно развернуть веб-приложение Java в Azure.</span><span class="sxs-lookup"><span data-stu-id="9c4ed-125">There are several ways by which you can deploy a Java web application to Azure.</span></span> <span data-ttu-id="9c4ed-126">В этом учебнике описывается один из самых простых: ваше приложение будет развернуто в контейнер веб-приложения Azure — для этого не нужно выбирать особый тип проекта и не требуются дополнительные инструменты.</span><span class="sxs-lookup"><span data-stu-id="9c4ed-126">This tutorial describes one of the simplest: your application will be deployed to an Azure Web App Container - no special project type nor additional tools are needed.</span></span> <span data-ttu-id="9c4ed-127">JDK и программное обеспечение веб-контейнера будут предоставлены Azure, поэтому нет необходимости загружать их самостоятельно. Все, что вам нужно — ваше веб-приложение Java.</span><span class="sxs-lookup"><span data-stu-id="9c4ed-127">The JDK and the web container software will be provided for you by Azure, so there is no need to upload your own; all you need is your Java Web App.</span></span> <span data-ttu-id="9c4ed-128">В результате процесс публикации приложения занимает несколько секунд, а не минут.</span><span class="sxs-lookup"><span data-stu-id="9c4ed-128">As a result, the publishing process for your application will take seconds, not minutes.</span></span>

1. <span data-ttu-id="9c4ed-129">В обозревателе проектов Eclipse щелкните правой кнопкой мыши **MyWebApp**.</span><span class="sxs-lookup"><span data-stu-id="9c4ed-129">In Eclipse's Project Explorer, right-click **MyWebApp**.</span></span>

2. <span data-ttu-id="9c4ed-130">В контекстном меню выберите **Azure**, затем щелкните **Опубликовать как веб-приложение Azure**.</span><span class="sxs-lookup"><span data-stu-id="9c4ed-130">In the context menu, select **Azure**, then click **Publish as Azure Web App...**</span></span>
   
   ![Опубликовать как веб-приложение Azure][03]
   
   <span data-ttu-id="9c4ed-132">Кроме того, выбирая проект веб-приложения в обозревателе проектов, вы можете нажать на панели инструментов кнопку с раскрывающимся списком **Опубликовать** и выбрать в списке **Publish as Azure Web App** (Опубликовать как веб-приложение Azure).</span><span class="sxs-lookup"><span data-stu-id="9c4ed-132">Alternatively, while your web application project is selected in the Project Explorer, you can click the **Publish** dropdown button on the toolbar and select **Publish as Azure Web App** from there:</span></span>
   
   ![Опубликовать как веб-приложение Azure][14]

3. <span data-ttu-id="9c4ed-134">Если вы еще не вошли в систему Azure из Eclipse, появится запрос на вход в учетную запись Azure:</span><span class="sxs-lookup"><span data-stu-id="9c4ed-134">If you have not already signed into Azure from Eclipse, you will be prompted to sign into your Azure account:</span></span>
   
   ![Диалоговое окно входа в Azure][04]
   
   <span data-ttu-id="9c4ed-136">При наличии нескольких учетных записей Azure некоторые запросы во время входа в систему могут отображаться несколько раз, даже если они выглядят одинаковыми.</span><span class="sxs-lookup"><span data-stu-id="9c4ed-136">If you have multiple Azure accounts, some of the prompts during the sign in process may be shown more than once, even if they appear to be the same.</span></span> <span data-ttu-id="9c4ed-137">Если это происходит, выполните вход.</span><span class="sxs-lookup"><span data-stu-id="9c4ed-137">When this happens, continue following the sign in instructions.</span></span>

4. <span data-ttu-id="9c4ed-138">После успешного входа в учетную запись Azure в диалоговом окне **Управление подписками** отобразится список подписок, связанных с вашими учетными данными.</span><span class="sxs-lookup"><span data-stu-id="9c4ed-138">After you have successfully signed into your Azure account, the **Manage Subscriptions** dialog box will display a list of subscriptions that are associated with your credentials.</span></span> <span data-ttu-id="9c4ed-139">Если список содержит несколько подписок и вы будете работать только с некоторыми из них, снимите флажки с подписок, которые не будете использовать.</span><span class="sxs-lookup"><span data-stu-id="9c4ed-139">If there are multiple subscriptions listed and you want to work with only a specific subset of them, you may optionally uncheck the ones you do want to use.</span></span> <span data-ttu-id="9c4ed-140">После выбора подписок щелкните **Закрыть**.</span><span class="sxs-lookup"><span data-stu-id="9c4ed-140">When you have selected your subscriptions, click **Close**.</span></span>
   
   ![Диалоговое окно управления подписками][05]

5. <span data-ttu-id="9c4ed-142">При открытии диалогового окна **Deploy to Azure Web App Container** (Развертывание в контейнер веб-приложения Azure) в нем будут показаны все контейнеры веб-приложений, созданные ранее. Если вы не создали ни одного контейнера, список будет пустым.</span><span class="sxs-lookup"><span data-stu-id="9c4ed-142">When the **Deploy to Azure Web App Container** dialog box appears, it will display any Web App containers that you have previously created; if you have not created any containers, the list will be empty.</span></span>
   
   ![Диалоговое окно развертывания в контейнер веб-приложения Azure][06]

6. <span data-ttu-id="9c4ed-144">Если вы не создавали контейнер веб-приложения Azure или хотите опубликовать приложение в новый контейнер, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="9c4ed-144">If you have not created an Azure Web App Container before, or if you would like to publish your application to a new container, use the following steps.</span></span> <span data-ttu-id="9c4ed-145">В противном случае выберите существующий контейнер веб-приложения и перейдите к шагу 7 ниже.</span><span class="sxs-lookup"><span data-stu-id="9c4ed-145">Otherwise, select an existing Web App Container and skip to step 7 below.</span></span>
   
   <span data-ttu-id="9c4ed-146">а.</span><span class="sxs-lookup"><span data-stu-id="9c4ed-146">a.</span></span> <span data-ttu-id="9c4ed-147">Нажмите кнопку **Создать**</span><span class="sxs-lookup"><span data-stu-id="9c4ed-147">Click **New...**</span></span>
      
      ![Диалоговое окно развертывания в контейнер веб-приложения Azure][15]

   <span data-ttu-id="9c4ed-149">b.</span><span class="sxs-lookup"><span data-stu-id="9c4ed-149">b.</span></span> <span data-ttu-id="9c4ed-150">Откроется диалоговое окно **New Web App Container** (Новый контейнер веб-приложения):</span><span class="sxs-lookup"><span data-stu-id="9c4ed-150">The **New Web App Container** dialog box will be displayed:</span></span>
      
      ![Диалоговое окно нового контейнера веб-приложения][07a]

   <span data-ttu-id="9c4ed-152">c.</span><span class="sxs-lookup"><span data-stu-id="9c4ed-152">c.</span></span> <span data-ttu-id="9c4ed-153">Укажите **метку DNS** для контейнера веб-приложения. Она образует метку листа DNS для URL-адреса узла веб-приложения в Azure.</span><span class="sxs-lookup"><span data-stu-id="9c4ed-153">Enter a **DNS Label** for your Web App Container; this will form the leaf DNS label of the host URL for your web application in Azure.</span></span> <span data-ttu-id="9c4ed-154">(Примечание. Имя должно быть доступным и соответствовать требованиям к именованию веб-приложений Azure.)</span><span class="sxs-lookup"><span data-stu-id="9c4ed-154">(Note that the name must be available and conform to Azure Web App naming requirements.)</span></span>

   <span data-ttu-id="9c4ed-155">d.</span><span class="sxs-lookup"><span data-stu-id="9c4ed-155">d.</span></span> <span data-ttu-id="9c4ed-156">В раскрывающемся меню **Веб-контейнер** выберите для своего приложения соответствующее программное обеспечение.</span><span class="sxs-lookup"><span data-stu-id="9c4ed-156">In the **Web Container** drop-down menu, select the appropriate software for your application.</span></span>
      
      <span data-ttu-id="9c4ed-157">На данный момент можно выбрать Tomcat 8, Tomcat 7 или Jetty 9.</span><span class="sxs-lookup"><span data-stu-id="9c4ed-157">Currently, you can choose from Tomcat 8, Tomcat 7 or Jetty 9.</span></span> <span data-ttu-id="9c4ed-158">Последний дистрибутив выбранного программного обеспечения, предоставленный Azure, будет запущен в последнем дистрибутиве JDK 8, созданном Oracle и предоставленном Azure.</span><span class="sxs-lookup"><span data-stu-id="9c4ed-158">A recent distribution of the selected software will be provided by Azure, and it will run on a recent distribution of JDK 8 created by Oracle and provided by Azure.</span></span>

   <span data-ttu-id="9c4ed-159">д.</span><span class="sxs-lookup"><span data-stu-id="9c4ed-159">e.</span></span> <span data-ttu-id="9c4ed-160">В раскрывающемся меню **Подписка** выберите подписку, которую вы хотите использовать для этого развертывания.</span><span class="sxs-lookup"><span data-stu-id="9c4ed-160">In the **Subscription** drop-down menu, select the subscription you want to use for this deployment.</span></span>

   <span data-ttu-id="9c4ed-161">f.</span><span class="sxs-lookup"><span data-stu-id="9c4ed-161">f.</span></span> <span data-ttu-id="9c4ed-162">В раскрывающемся меню **Группа ресурсов** выберите группу ресурсов, с которой вы хотите связать свое веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="9c4ed-162">In the **Resource Group** drop-down menu, select the Resource Group with which you want to associate your Web App.</span></span> <span data-ttu-id="9c4ed-163">(Группы ресурсов Azure позволяют сгруппировать связанные ресурсы, чтобы, например, удалить их одновременно.)</span><span class="sxs-lookup"><span data-stu-id="9c4ed-163">(Azure Resource Groups allow you to group related resources together so that, for example, they can be deleted together.)</span></span>
      
      <span data-ttu-id="9c4ed-164">Можно выбрать существующую группу ресурсов (если она есть) и перейти к шагу g ниже, или создать новую, сделав следующее:</span><span class="sxs-lookup"><span data-stu-id="9c4ed-164">You can select an existing Resource Group (if you have any) and skip to step g below, or use the following these steps to create a new Resource Group:</span></span>
      
      * <span data-ttu-id="9c4ed-165">Нажмите кнопку **Создать**</span><span class="sxs-lookup"><span data-stu-id="9c4ed-165">Click **New...**</span></span>
      * <span data-ttu-id="9c4ed-166">Откроется диалоговое окно **Новая группа ресурсов** :</span><span class="sxs-lookup"><span data-stu-id="9c4ed-166">The **New Resource Group** dialog box will be displayed:</span></span>
        
          ![Диалоговое окно новой группы ресурсов][08]
      * <span data-ttu-id="9c4ed-168">В текстовое поле **Имя** введите имя новой группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="9c4ed-168">In the the **Name** textbox, specify a name for your new Resource Group.</span></span>
      * <span data-ttu-id="9c4ed-169">В раскрывающемся меню **Регион** выберите расположение центра обработки данных Azure для группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="9c4ed-169">In the the **Region** drop-down menu, select the appropriate Azure data center location for your Resource Group.</span></span>
      * <span data-ttu-id="9c4ed-170">Необязательно. По умолчанию Azure автоматически развернет последний дистрибутив Java 8 в ваш контейнер веб-приложения в качестве виртуальной машины Java.</span><span class="sxs-lookup"><span data-stu-id="9c4ed-170">OPTIONAL: By default, a recent distribution of Java 8 will be deployed by Azure automatically to your web app container as your JVM.</span></span> <span data-ttu-id="9c4ed-171">Тем не менее, если это нужно веб-приложению, то можно указать другую версию и дистрибутив виртуальной машины Java.</span><span class="sxs-lookup"><span data-stu-id="9c4ed-171">However, you can specify a different version and distribution of the JVM if your Web App requires it.</span></span> <span data-ttu-id="9c4ed-172">Чтобы указать пакет JDK для веб-приложения, щелкните **JDK** и выберите один из следующих параметров.</span><span class="sxs-lookup"><span data-stu-id="9c4ed-172">To specify the JDK for your Web App, click the **JDK** tab, and select one of the following options:</span></span>
         * <span data-ttu-id="9c4ed-173">**Deploy the default JDK offered by Azure Web Apps service** (Развернуть пакет JDK по умолчанию, предлагаемый службой веб-приложений Azure). Этот параметр позволит развернуть последний дистрибутив Java 8.</span><span class="sxs-lookup"><span data-stu-id="9c4ed-173">**Deploy the default JDK offered by Azure Web Apps service**: This option will deploy a recent distribution of Java 8.</span></span>
         * <span data-ttu-id="9c4ed-174">**Deploy a 3rd party JDK available on Azure** (Развернуть сторонний пакет JDK, доступный в Azure). Этот параметр позволяет выбрать из списка пакетов JDK, предоставляемых Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="9c4ed-174">**Deploy a 3rd party JDK available on Azure**: This option allows you to choose from the list of JDKs which are provided by Microsoft Azure.</span></span>
         * <span data-ttu-id="9c4ed-175">**Deploy my own JDK from this download location** (Развернуть собственный пакет JDK из этого расположения для скачивания). Этот параметр позволяет указать собственный дистрибутив JDK, который должен быть упакован в ZIP-файл и передан либо в общедоступное расположение для скачивания, либо в учетную запись хранения Azure, к которой у вас есть доступ.</span><span class="sxs-lookup"><span data-stu-id="9c4ed-175">**Deploy my own JDK from this download location**: This option allows you to specify your own JDK distribution, which must be packaged as a ZIP file and uploaded to either a publicly available download location or an Azure storage account for which you have access.</span></span>
          
         ![Диалоговое окно нового контейнера веб-приложения][07b]

   <span data-ttu-id="9c4ed-177">ж.</span><span class="sxs-lookup"><span data-stu-id="9c4ed-177">g.</span></span> <span data-ttu-id="9c4ed-178">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="9c4ed-178">Click **OK**.</span></span>

   <span data-ttu-id="9c4ed-179">h.</span><span class="sxs-lookup"><span data-stu-id="9c4ed-179">h.</span></span> <span data-ttu-id="9c4ed-180">В раскрывающемся меню **План службы приложений** перечислены планы службы приложений, связанные с выбранной группой ресурсов.</span><span class="sxs-lookup"><span data-stu-id="9c4ed-180">The **App Service Plan** drop-down menu lists the app service plans that are associated with the Resource Group that you selected.</span></span> <span data-ttu-id="9c4ed-181">(В планах службы приложений указываются такие сведения, как расположение веб-приложения, ценовая категория и размер вычислительной операции.</span><span class="sxs-lookup"><span data-stu-id="9c4ed-181">(App Service Plans specify information such as the location of your Web App, the pricing tier and the compute instance size.</span></span> <span data-ttu-id="9c4ed-182">Один план службы приложений можно использовать для нескольких веб-приложений, поэтому он поддерживается отдельно от развертывания конкретного веб-приложения.)</span><span class="sxs-lookup"><span data-stu-id="9c4ed-182">A single App Service Plan can be used for multiple Web Apps, which is why it is maintained separately from a specific Web App deployment.)</span></span>
      
       You can select an existing App Service Plan (if you have any) and skip to step h below, or use the following these steps to create a new App Service Plan:
      
      * <span data-ttu-id="9c4ed-183">Нажмите кнопку **Создать**</span><span class="sxs-lookup"><span data-stu-id="9c4ed-183">Click **New...**</span></span>
      * <span data-ttu-id="9c4ed-184">Откроется диалоговое окно **Новый план службы приложений** :</span><span class="sxs-lookup"><span data-stu-id="9c4ed-184">The **New App Service Plan** dialog box will be displayed:</span></span>
        
          ![Диалоговое окно нового плана службы приложений][09]
      * <span data-ttu-id="9c4ed-186">В текстовое поле **Имя** введите имя нового плана службы приложений.</span><span class="sxs-lookup"><span data-stu-id="9c4ed-186">In the the **Name** textbox, specify a name for your new App Service Plan.</span></span>
      * <span data-ttu-id="9c4ed-187">В раскрывающемся меню **Расположение** выберите расположение центра обработки данных Azure для плана.</span><span class="sxs-lookup"><span data-stu-id="9c4ed-187">In the the **Location** drop-down menu, select the appropriate Azure data center location for the plan.</span></span>
      * <span data-ttu-id="9c4ed-188">В раскрывающемся меню **Ценовая категория** выберите соответствующую ценовую категорию для плана.</span><span class="sxs-lookup"><span data-stu-id="9c4ed-188">In the the **Pricing Tier** drop-down menu, select the appropriate pricing for the plan.</span></span> <span data-ttu-id="9c4ed-189">Для тестирования можно выбрать категорию **Бесплатный**.</span><span class="sxs-lookup"><span data-stu-id="9c4ed-189">For testing purposes you can choose **Free**.</span></span>
      * <span data-ttu-id="9c4ed-190">В раскрывающемся меню **Размер экземпляра** выберите для плана соответствующий размер экземпляра.</span><span class="sxs-lookup"><span data-stu-id="9c4ed-190">In the the **Instance Size** drop-down menu, select the appropriate instance size for the plan.</span></span> <span data-ttu-id="9c4ed-191">Для тестирования можно выбрать **Маленький**.</span><span class="sxs-lookup"><span data-stu-id="9c4ed-191">For testing purposes you can choose **Small**.</span></span>

   <span data-ttu-id="9c4ed-192">i.</span><span class="sxs-lookup"><span data-stu-id="9c4ed-192">i.</span></span> <span data-ttu-id="9c4ed-193">После завершения всех описанных выше действий диалоговое окно "Новый контейнер веб-приложения" должно выглядеть примерно так, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="9c4ed-193">Once you have completed all of the above steps, the New Web App Container dialog box should resemble the following illustration:</span></span>
      
      ![Диалоговое окно нового контейнера веб-приложения][10]

   <span data-ttu-id="9c4ed-195">j.</span><span class="sxs-lookup"><span data-stu-id="9c4ed-195">j.</span></span> <span data-ttu-id="9c4ed-196">Нажмите кнопку **ОК** , чтобы создать контейнер веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="9c4ed-196">Click **OK** to complete the creation of your new Web App container.</span></span>
       
      <span data-ttu-id="9c4ed-197">Подождите несколько секунд. Когда список контейнеров веб-приложений обновится, созданный контейнер веб-приложения должен быть выбран в списке.</span><span class="sxs-lookup"><span data-stu-id="9c4ed-197">Wait a few seconds for the list of the Web App containers to be refreshed, and your newly-created web app container should now be selected in the list.</span></span>

7. <span data-ttu-id="9c4ed-198">Теперь все готово для начального развертывания вашего веб-приложения в Azure:</span><span class="sxs-lookup"><span data-stu-id="9c4ed-198">You are now ready to complete the initial deployment of your Web App to Azure:</span></span>
   
   ![Диалоговое окно развертывания в контейнер веб-приложения Azure][11]
   
   <span data-ttu-id="9c4ed-200">Нажмите кнопку **ОК** , чтобы развернуть приложение Java в выбранный контейнер веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="9c4ed-200">Click **OK** to deploy your Java application to the selected Web App container.</span></span>
   
   <span data-ttu-id="9c4ed-201">По умолчанию приложение будет развернуто в подкаталог сервера приложений.</span><span class="sxs-lookup"><span data-stu-id="9c4ed-201">By default, your application will be deployed as a subdirectory of the application server.</span></span> <span data-ttu-id="9c4ed-202">Чтобы развернуть приложение в качестве корневого приложения, установите флажок **Deploy to root** (Развернуть в корень) перед нажатием кнопки **ОК**.</span><span class="sxs-lookup"><span data-stu-id="9c4ed-202">If you want it to be deployed as the root application, check the **Deploy to root** checkbox before clicking **OK**.</span></span>

8. <span data-ttu-id="9c4ed-203">После этого вы должны увидеть представление **Журнал действий Azure** , в котором будет отображаться состояние развертывания веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="9c4ed-203">Next, you should see the **Azure Activity Log** view, which will indicate the deployment status of your Web App.</span></span>
   
   ![Журнал действий Azure][12]
   
   <span data-ttu-id="9c4ed-205">Процесс развертывания веб-приложения в Azure занимает всего несколько секунд.</span><span class="sxs-lookup"><span data-stu-id="9c4ed-205">The process of deploying your Web App to Azure should take only a few seconds to complete.</span></span> <span data-ttu-id="9c4ed-206">Когда процесс будет завершен, вы увидите ссылку **Опубликовано** in the **Состояние** .</span><span class="sxs-lookup"><span data-stu-id="9c4ed-206">When your application ready, you will see a link named **Published** in the **Status** column.</span></span> <span data-ttu-id="9c4ed-207">Если щелкнуть по ней, откроется домашняя страница развернутого веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="9c4ed-207">When you click the link, it will take you to your deployed Web App's home page.</span></span>

## <a name="updating-your-web-app"></a><span data-ttu-id="9c4ed-208">Обновление веб-приложения</span><span class="sxs-lookup"><span data-stu-id="9c4ed-208">Updating your web app</span></span>
<span data-ttu-id="9c4ed-209">Обновить существующее и запущенное веб-приложение Azure быстро и просто. Сделать это можно двумя способами:</span><span class="sxs-lookup"><span data-stu-id="9c4ed-209">Updating an existing running Azure Web App is a quick and easy process, and you have two options for updating:</span></span>

* <span data-ttu-id="9c4ed-210">Можно обновить развертывание существующего веб-приложения Java.</span><span class="sxs-lookup"><span data-stu-id="9c4ed-210">You can update the deployment of an existing Java Web App.</span></span>
* <span data-ttu-id="9c4ed-211">Можно опубликовать дополнительное приложение Java в тот же контейнер веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="9c4ed-211">You can publish an additional Java application to the same Web App Container.</span></span>

<span data-ttu-id="9c4ed-212">Процесс в каждом случае идентичен и занимает несколько секунд.</span><span class="sxs-lookup"><span data-stu-id="9c4ed-212">In either case, the process is identical and takes only a few seconds:</span></span>

1. <span data-ttu-id="9c4ed-213">В обозревателе проектов Eclipse щелкните правой кнопкой мыши приложение Java, которое вы хотите обновить или добавить в существующий контейнер веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="9c4ed-213">In the Eclipse project explorer, right-click the Java application you want to update or add to an existing Web App Container.</span></span>

2. <span data-ttu-id="9c4ed-214">В контекстном меню выберите **Azure**, а затем щелкните **Опубликовать как веб-приложение Azure**.</span><span class="sxs-lookup"><span data-stu-id="9c4ed-214">When the context menu appears, select **Azure** and then **Publish as Azure Web App...**</span></span>

3. <span data-ttu-id="9c4ed-215">Так как ранее вы уже вошли в систему, вы увидите список существующих контейнеров веб-приложений.</span><span class="sxs-lookup"><span data-stu-id="9c4ed-215">Since you have already logged in previously, you will see a list of your existing Web App containers.</span></span> <span data-ttu-id="9c4ed-216">Выберите контейнер, в котором вы хотите опубликовать или повторно опубликовать приложение Java, и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="9c4ed-216">Select the one you want to publish or re-publish your Java application to and click **OK**.</span></span>

<span data-ttu-id="9c4ed-217">Через несколько секунд в представлении **Журнал действий Azure** состояние обновленного развертывания изменится на **Опубликовано**, и вы сможете проверить свое обновленное приложение в веб-браузере.</span><span class="sxs-lookup"><span data-stu-id="9c4ed-217">A few seconds later, the **Azure Activity Log** view will show your updated deployment as **Published** and you will be able to verify your updated application in a web browser.</span></span>

## <a name="starting-stopping-or-restarting-an-existing-web-app"></a><span data-ttu-id="9c4ed-218">Запуск, остановка или перезапуск существующего веб-приложения</span><span class="sxs-lookup"><span data-stu-id="9c4ed-218">Starting, stopping, or restarting an existing web app</span></span>
<span data-ttu-id="9c4ed-219">Запустить или остановить существующий контейнер веб-приложения Azure (включая все развернутые в нем приложения Java) можно в представлении **Обозреватель Azure** .</span><span class="sxs-lookup"><span data-stu-id="9c4ed-219">To start or stop an existing Azure Web App container, (including all the deployed Java applications in it), you can use the **Azure Explorer** view.</span></span>

<span data-ttu-id="9c4ed-220">Если представление **Azure Explorer** еще не открыто, это можно сделать, щелкнув в Eclipse меню **Окно** и последовательно выбрав **Show View** (Показать представление), **Other** (Другие), **Azure**, **Azure Explorer**.</span><span class="sxs-lookup"><span data-stu-id="9c4ed-220">If the **Azure Explorer** view is not already open, you can open it by clicking then **Window** menu in Eclipse, then click **Show View**, then **Other...**, then **Azure**, and then click **Azure Explorer**.</span></span> <span data-ttu-id="9c4ed-221">Если ранее вы не вошли в систему, вам будет предложено это сделать.</span><span class="sxs-lookup"><span data-stu-id="9c4ed-221">If you have not previously logged in, it will prompt you to do so.</span></span>

<span data-ttu-id="9c4ed-222">Когда представление **Обозреватель Azure** откроется, выполните следующие действия для запуска или остановки веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="9c4ed-222">When the **Azure Explorer** view is displayed, use follow these steps to start or stop your Web App:</span></span> 

1. <span data-ttu-id="9c4ed-223">Разверните узел **Azure** .</span><span class="sxs-lookup"><span data-stu-id="9c4ed-223">Expand the **Azure** node.</span></span>

2. <span data-ttu-id="9c4ed-224">Разверните узел **Web Apps** (Веб-приложения).</span><span class="sxs-lookup"><span data-stu-id="9c4ed-224">Expand the **Web Apps** node.</span></span> 

3. <span data-ttu-id="9c4ed-225">Щелкните правой кнопкой мыши необходимое веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="9c4ed-225">Right-click the desired Web App.</span></span>

4. <span data-ttu-id="9c4ed-226">В открывшемся контекстном меню выберите **Запустить**, **Остановить** или **Перезапустить**.</span><span class="sxs-lookup"><span data-stu-id="9c4ed-226">When the context menu appears, click **Start**, **Stop**, or **Restart**.</span></span> <span data-ttu-id="9c4ed-227">Обратите внимание, что доступные меню контекстно зависимы, поэтому можно только остановить веб-приложение или запустить веб-приложение, которое в данный момент не запущено.</span><span class="sxs-lookup"><span data-stu-id="9c4ed-227">Note that the menu choices are context-aware, so you can only stop a running web app or start a web app which is not currently running.</span></span>
   
   ![Остановка существующего веб-приложения][13]

## <a name="next-steps"></a><span data-ttu-id="9c4ed-229">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9c4ed-229">Next steps</span></span>

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

<span data-ttu-id="9c4ed-230">Дополнительные сведения о создании веб-приложений Azure см. в разделе [Обзор веб-приложений].</span><span class="sxs-lookup"><span data-stu-id="9c4ed-230">For additional information about creating Azure Web Apps, see the [Web Apps Overview].</span></span>

<!-- URL List -->

[средств Azure для Eclipse]: azure-toolkit-for-eclipse.md
[Обзор веб-приложений]: /azure/app-service/app-service-web-overview
[Apache Tomcat]: http://tomcat.apache.org/
[Jetty]: http://www.eclipse.org/jetty/

<!-- IMG List -->

[01]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/01-Web-Page.png
[02]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/02-Dynamic-Web-Project.png
[03]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/03-Context-Menu.png
[04]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/04-Log-In-Dialog.png
[05]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/05-Manage-Subscriptions-Dialog.png
[06]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/06-Deploy-To-Azure-Web-Container.png
[07a]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/07a-New-Web-App-Container-Dialog.png
[07b]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/07b-New-Web-App-Container-Dialog.png
[08]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/08-New-Resource-Group-Dialog.png
[09]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/09-New-Service-Plan-Dialog.png
[10]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/10-Completed-Web-App-Container-Dialog.png
[11]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/11-Completed-Deploy-Dialog.png
[12]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/12-Activity-Log-View.png
[13]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/13-Azure-Explorer-Web-App.png
[14]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/14-publishDropdownButton.png
[15]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/15-New-Azure-Web-Container.png
