---
title: "Развертывание приложения Spring Boot Application в службе приложений Azure"
description: "В этом учебнике приводятся пошаговые инструкции для разработчиков по развертыванию веб-приложения Spring Boot Getting Started в службе приложений Azure."
services: app-service
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: java
ms.topic: article
ms.date: 12/01/2017
ms.author: asirveda;robmcm
ms.openlocfilehash: b520cc80360f8162c929bb2cc88c24311a7e20f8
ms.sourcegitcommit: fc48e038721e6910cb8b1f8951df765d517e504d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/06/2017
---
# <a name="deploy-a-spring-boot-application-to-the-azure-app-service"></a><span data-ttu-id="937cb-103">Развертывание приложения Spring Boot Application в службе приложений Azure</span><span class="sxs-lookup"><span data-stu-id="937cb-103">Deploy a Spring Boot Application to the Azure App Service</span></span>

<span data-ttu-id="937cb-104">В этом руководстве описано, как создать пример начального веб-приложения [Spring Boot] и развернуть его в [службе приложений Azure].</span><span class="sxs-lookup"><span data-stu-id="937cb-104">This tutorial will walk you though creating a sample [Spring Boot] Getting Started web app and deploying it to [Azure App Service].</span></span>

### <a name="prerequisites"></a><span data-ttu-id="937cb-105">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="937cb-105">Prerequisites</span></span>

<span data-ttu-id="937cb-106">Для работы с этим учебником требуется следующее.</span><span class="sxs-lookup"><span data-stu-id="937cb-106">In order to complete the steps in this tutorial, you need to have the following:</span></span>

* <span data-ttu-id="937cb-107">Подписка Azure; если у вас еще нет подписки Azure, вы можете активировать [преимущества для подписчиков MSDN] или зарегистрироваться для получения [бесплатной учетной записи Azure].</span><span class="sxs-lookup"><span data-stu-id="937cb-107">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="937cb-108">Актуальная версия [Java Developer Kit (JDK)].</span><span class="sxs-lookup"><span data-stu-id="937cb-108">An up-to-date [Java Developer Kit (JDK)].</span></span>
* <span data-ttu-id="937cb-109">Средство сборки [Maven] (версия 3) от Apache.</span><span class="sxs-lookup"><span data-stu-id="937cb-109">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="937cb-110">Клиент [Git].</span><span class="sxs-lookup"><span data-stu-id="937cb-110">A [Git] client.</span></span>

## <a name="create-the-spring-boot-getting-started-web-app"></a><span data-ttu-id="937cb-111">Создание веб-приложения Spring Boot Getting Started</span><span class="sxs-lookup"><span data-stu-id="937cb-111">Create the Spring Boot Getting Started web app</span></span>

<span data-ttu-id="937cb-112">Ниже приводятся пошаговые инструкции по созданию простого веб-приложения Spring Boot и его локальному тестированию.</span><span class="sxs-lookup"><span data-stu-id="937cb-112">The following steps will walk you through the steps that are required to create a simple Spring Boot web application and test it locally.</span></span>

1. <span data-ttu-id="937cb-113">Откройте командную строку и создайте локальный каталог для размещения приложения, после чего перейдите в этот каталог, например:</span><span class="sxs-lookup"><span data-stu-id="937cb-113">Open a command-prompt and create a local directory to hold your application, and change to that directory; for example:</span></span>
   ```
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="937cb-114">-- или --</span><span class="sxs-lookup"><span data-stu-id="937cb-114">-- or --</span></span>
   ```
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="937cb-115">Клонируйте образец проекта [Spring Boot Getting Started] в созданный каталог, например:</span><span class="sxs-lookup"><span data-stu-id="937cb-115">Clone the [Spring Boot Getting Started] sample project into the directory you just created; for example:</span></span>
   ```
   git clone https://github.com/spring-guides/gs-spring-boot.git
   ```

1. <span data-ttu-id="937cb-116">Перейдите в каталог готового проекта, например:</span><span class="sxs-lookup"><span data-stu-id="937cb-116">Change directory to the completed project; for example:</span></span>
   ```
   cd gs-spring-boot
   cd complete
   ```

1. <span data-ttu-id="937cb-117">Выполните сборку файла JAR с помощью Maven, например:</span><span class="sxs-lookup"><span data-stu-id="937cb-117">Build the JAR file using Maven; for example:</span></span>
   ```
   mvn package
   ```

1. <span data-ttu-id="937cb-118">После создания веб-приложения перейдите к JAR-файлу и запустите веб-приложение, например:</span><span class="sxs-lookup"><span data-stu-id="937cb-118">Once the web app has been created, change directory to the JAR file and start the web app; for example:</span></span>
   ```
   cd target
   java -jar gs-spring-boot-0.1.0.jar
   ```

1. <span data-ttu-id="937cb-119">Протестируйте веб-приложение, перейдя по адресу http://localhost:8080 в веб-браузере, или, если имеется программа curl, используйте синтаксис, как в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="937cb-119">Test the web app by browsing to http://localhost:8080 using a web browser, or use the syntax like the following example if you have curl available:</span></span>
   ```
   curl http://localhost:8080
   ```

1. <span data-ttu-id="937cb-120">Должно появиться следующее сообщение: **Greetings from Spring Boot!**</span><span class="sxs-lookup"><span data-stu-id="937cb-120">You should see the following message displayed: **Greetings from Spring Boot!**</span></span>

   ![Обзор образца приложения][SB01]

## <a name="create-an-azure-web-app-for-use-with-java"></a><span data-ttu-id="937cb-122">Создание веб-приложения Azure для использования с Java</span><span class="sxs-lookup"><span data-stu-id="937cb-122">Create an Azure web app for use with Java</span></span>

<span data-ttu-id="937cb-123">Ниже приведены пошаговые инструкции по созданию веб-приложения Azure, настройке необходимых параметров для Java и настройке учетных данных FTP.</span><span class="sxs-lookup"><span data-stu-id="937cb-123">The following steps will walk you through the steps to create an Azure Web App, configure the required settings for Java, and configure your FTP credentials.</span></span>

1. <span data-ttu-id="937cb-124">Перейдите на [портал Azure] и выполните вход.</span><span class="sxs-lookup"><span data-stu-id="937cb-124">Browse to the [Azure portal] and log in.</span></span>

1. <span data-ttu-id="937cb-125">Войдя в учетную запись на портале Azure, щелкните значок меню **Службы приложений**:</span><span class="sxs-lookup"><span data-stu-id="937cb-125">Once you have logged into your account on the Azure portal, click the menu icon for **App Services**:</span></span>
   
   ![Портал Azure][AZ01]

1. <span data-ttu-id="937cb-127">Когда откроется страница **Службы приложений**, щелкните **+ Добавить**, чтобы создать службу приложений.</span><span class="sxs-lookup"><span data-stu-id="937cb-127">When the **App Services** page is displayed, click **+ Add** to create a new App Service.</span></span>

   ![Создание службы приложений][AZ02]

1. <span data-ttu-id="937cb-129">Когда появится список шаблонов веб-приложений, щелкните ссылку базового веб-приложения Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="937cb-129">When the list of web app templates is displayed, click the link for the basic Microsoft Web App.</span></span>

   ![Шаблоны веб-приложений][AZ03]

1. <span data-ttu-id="937cb-131">Когда появится страница шаблона веб-приложения, нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="937cb-131">When the information page for the Web App template is displayed, click **Create**.</span></span>

   ![Создание веб-приложения][AZ04]

1. <span data-ttu-id="937cb-133">Укажите уникальное имя веб-приложения и задайте дополнительные параметры, после чего нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="937cb-133">Provide a unique name for your web app and specify any additional settings, and then **Create**.</span></span>

   ![Параметры создания веб-приложения][AZ05]

1. <span data-ttu-id="937cb-135">После создания веб-приложения щелкните значок меню **Службы приложений**, а затем выберите только что созданное веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="937cb-135">Once your web app has been created, click the menu icon for **App Services**, and then click your newly-created web app:</span></span>

   ![Список веб-приложений][AZ06]

1. <span data-ttu-id="937cb-137">Когда веб-приложение отобразится, укажите версию Java, выполнив указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="937cb-137">When your web app is displayed, specify the Java version by using the following steps:</span></span>

   <span data-ttu-id="937cb-138">а.</span><span class="sxs-lookup"><span data-stu-id="937cb-138">a.</span></span> <span data-ttu-id="937cb-139">Выберите пункт меню **Параметры приложения**.</span><span class="sxs-lookup"><span data-stu-id="937cb-139">Click the **Application Settings** menu item.</span></span>

   <span data-ttu-id="937cb-140">b.</span><span class="sxs-lookup"><span data-stu-id="937cb-140">b.</span></span> <span data-ttu-id="937cb-141">В качестве версии Java выберите **Java 8**.</span><span class="sxs-lookup"><span data-stu-id="937cb-141">Choose **Java 8** for the Java version.</span></span>

   <span data-ttu-id="937cb-142">c.</span><span class="sxs-lookup"><span data-stu-id="937cb-142">c.</span></span> <span data-ttu-id="937cb-143">В качестве дополнительного номера версии Java выберите **Самые новые**.</span><span class="sxs-lookup"><span data-stu-id="937cb-143">Choose **Newest** for the minor Java version.</span></span>

   <span data-ttu-id="937cb-144">г)</span><span class="sxs-lookup"><span data-stu-id="937cb-144">d.</span></span> <span data-ttu-id="937cb-145">В качестве веб-контейнера выберите **Последняя версия Tomcat 8.5**.</span><span class="sxs-lookup"><span data-stu-id="937cb-145">Choose **Newest Tomcat 8.5** for the web container.</span></span> <span data-ttu-id="937cb-146">(Этот контейнер в действительности не будет использоваться; Azure будет использовать контейнер в приложении Spring Boot.)</span><span class="sxs-lookup"><span data-stu-id="937cb-146">(This container will not actually be used; Azure will use the container from your Spring Boot application.)</span></span>

   <span data-ttu-id="937cb-147">д.</span><span class="sxs-lookup"><span data-stu-id="937cb-147">e.</span></span> <span data-ttu-id="937cb-148">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="937cb-148">Click **Save**.</span></span>

   ![Параметры приложения][AZ07]

1. <span data-ttu-id="937cb-150">Укажите учетные данные FTP, выполнив указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="937cb-150">Specify your FTP deployment credentials by using the following steps:</span></span>

   <span data-ttu-id="937cb-151">а.</span><span class="sxs-lookup"><span data-stu-id="937cb-151">a.</span></span> <span data-ttu-id="937cb-152">Выберите пункт меню **Учетные данные развертывания**.</span><span class="sxs-lookup"><span data-stu-id="937cb-152">Click the **Deployment Credentials** menu item.</span></span>

   <span data-ttu-id="937cb-153">b.</span><span class="sxs-lookup"><span data-stu-id="937cb-153">b.</span></span> <span data-ttu-id="937cb-154">Укажите имя пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="937cb-154">Specify your username and password.</span></span>

   <span data-ttu-id="937cb-155">c.</span><span class="sxs-lookup"><span data-stu-id="937cb-155">c.</span></span> <span data-ttu-id="937cb-156">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="937cb-156">Click **Save**.</span></span>

   ![Указание учетных данных развертывания][AZ08]

1. <span data-ttu-id="937cb-158">Получите сведения о подключении по FTP, выполнив указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="937cb-158">Retrieve your FTP connection information by using the following steps:</span></span>

   <span data-ttu-id="937cb-159">а.</span><span class="sxs-lookup"><span data-stu-id="937cb-159">a.</span></span> <span data-ttu-id="937cb-160">Выберите пункт меню **Учетные данные развертывания**.</span><span class="sxs-lookup"><span data-stu-id="937cb-160">Click the **Deployment Credentials** menu item.</span></span>

   <span data-ttu-id="937cb-161">b.</span><span class="sxs-lookup"><span data-stu-id="937cb-161">b.</span></span> <span data-ttu-id="937cb-162">Скопируйте полное имя пользователя и URL-адрес FTP, а затем сохраните их. Они понадобятся в следующем разделе этого учебника.</span><span class="sxs-lookup"><span data-stu-id="937cb-162">Copy your full FTP username and URL and save them for the next section of this tutorial.</span></span>

   ![URL-адрес и учетные данные FTP][AZ09]

## <a name="deploy-your-spring-boot-web-app-to-azure"></a><span data-ttu-id="937cb-164">Развертывание веб-приложения Spring Boot в Azure</span><span class="sxs-lookup"><span data-stu-id="937cb-164">Deploy your Spring Boot web app to Azure</span></span>

<span data-ttu-id="937cb-165">Ниже приведены пошаговые инструкции по развертыванию веб-приложения Spring Boot в Azure.</span><span class="sxs-lookup"><span data-stu-id="937cb-165">The following steps will walk you through the steps to deploy your Spring Boot web app to Azure.</span></span>

1. <span data-ttu-id="937cb-166">Откройте текстовый редактор, например Блокнот, и вставьте следующий текст в новый документ, а затем сохраните файл с именем *web.config*:</span><span class="sxs-lookup"><span data-stu-id="937cb-166">Open a text editor such as Windows Notepad and paste the following text into a new document, then save the file as *web.config*:</span></span>
   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <configuration>
     <system.webServer>
       <handlers>
         <add name="httpPlatformHandler" path="*" verb="*" modules="httpPlatformHandler" resourceType="Unspecified" />
       </handlers>
       <httpPlatform processPath="%JAVA_HOME%\bin\java.exe"
           arguments="-Djava.net.preferIPv4Stack=true -Dserver.port=%HTTP_PLATFORM_PORT% -jar &quot;%HOME%\site\wwwroot\gs-spring-boot-0.1.0.jar&quot;">
       </httpPlatform>
     </system.webServer>
   </configuration>
   ```

1. <span data-ttu-id="937cb-167">После сохранения файла *web.config* в системе подключитесь к веб-приложению по FTP, используя URL-адрес, имя пользователя и пароль из предыдущего раздела этого учебника.</span><span class="sxs-lookup"><span data-stu-id="937cb-167">After you have saved the *web.config* file to your system, connect to your web app via FTP using the URL, username, and password from the preceding section of this tutorial.</span></span> <span data-ttu-id="937cb-168">Например:</span><span class="sxs-lookup"><span data-stu-id="937cb-168">For example:</span></span>
   ```
   ftp
   open waws-prod-sn0-000.ftp.azurewebsites.windows.net
   user wingtiptoys-springboot\wingtiptoysuser
   pass ********
   ```

1. <span data-ttu-id="937cb-169">Измените удаленный каталог на корневую папку веб-приложения (находящуюся по адресу */site/wwwroot*), а затем скопируйте JAR-файл приложения Spring Boot и файл *web.config*, созданный ранее.</span><span class="sxs-lookup"><span data-stu-id="937cb-169">Change the remote directory to the root folder of your web app, (which is at */site/wwwroot*), then copy the JAR file from your Spring Boot application and the *web.config* from earlier.</span></span> <span data-ttu-id="937cb-170">Например:</span><span class="sxs-lookup"><span data-stu-id="937cb-170">For example:</span></span>
   ```
   cd site/wwwroot
   put gs-spring-boot-0.1.0.jar
   put web.config
   ```

1. <span data-ttu-id="937cb-171">После развертывания файлов JAR и *web.config* в веб-приложении необходимо перезапустить его с помощью портала Azure:</span><span class="sxs-lookup"><span data-stu-id="937cb-171">After you have deployed your JAR and *web.config* files to your web app, you need to restart your web app using the Azure portal:</span></span>

   ![][AZ10]

1. <span data-ttu-id="937cb-172">Протестируйте веб-приложение, перейдя по его URL-адресу в веб-браузере, или, если имеется программа curl, используйте синтаксис, как в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="937cb-172">Test the web app by browsing to your web app's URL using a web browser, or use the syntax like the following example if you have curl available:</span></span>
   ```
   curl http://wingtiptoys-springboot.azurewebsites.net/
   ```

1. <span data-ttu-id="937cb-173">Должно появиться следующее сообщение: **Greetings from Spring Boot!**</span><span class="sxs-lookup"><span data-stu-id="937cb-173">You should see the following message displayed: **Greetings from Spring Boot!**</span></span>

   ![Обзор образца приложения][SB02]

## <a name="next-steps"></a><span data-ttu-id="937cb-175">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="937cb-175">Next steps</span></span>

<span data-ttu-id="937cb-176">Дополнительные сведения об использовании приложений Spring Boot в Azure см. в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="937cb-176">For more information about using Spring Boot applications on Azure, see the following articles:</span></span>

* [<span data-ttu-id="937cb-177">Развертывание приложения Spring Boot в Linux в службе контейнеров Azure</span><span class="sxs-lookup"><span data-stu-id="937cb-177">Deploy a Spring Boot Application on Linux in the Azure Container Service</span></span>](deploy-spring-boot-java-app-on-linux.md)

* [<span data-ttu-id="937cb-178">Развертывание приложения Spring Boot в кластере Kubernetes в службе контейнеров Azure</span><span class="sxs-lookup"><span data-stu-id="937cb-178">Deploy a Spring Boot Application on a Kubernetes Cluster in the Azure Container Service</span></span>](deploy-spring-boot-java-app-on-kubernetes.md)

<span data-ttu-id="937cb-179">Дополнительные сведения об использовании Azure с Java см. в руководствах по [Azure для разработчиков Java] и [инструментах Java для Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="937cb-179">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="937cb-180">Дополнительные сведения о развертывании веб-приложений в Azure по FTP см. в статье [Развертывание приложения в службе приложений Azure с помощью FTP или FTPS].</span><span class="sxs-lookup"><span data-stu-id="937cb-180">For additional information about depoying web apps to Azure using FTP, see [Deploy your app to Azure App Service using FTP/S].</span></span>

<span data-ttu-id="937cb-181">Дополнительные сведения об образце проекта Spring Boot см. на странице [Spring Boot Getting Started].</span><span class="sxs-lookup"><span data-stu-id="937cb-181">For further details about the Spring Boot sample project, see [Spring Boot Getting Started].</span></span>

<span data-ttu-id="937cb-182">Справку по началу работы с собственными приложениями Spring Boot см. на странице **Spring Initializr** по адресу https://start.spring.io/.</span><span class="sxs-lookup"><span data-stu-id="937cb-182">For help with getting started with your own Spring Boot applications, see the **Spring Initializr** at https://start.spring.io/.</span></span>

<span data-ttu-id="937cb-183">Дополнительные сведения о настройке дополнительных параметров для веб-приложения см. в статье [Настройка веб-приложений в службе приложений Azure].</span><span class="sxs-lookup"><span data-stu-id="937cb-183">For more information about configuring additional settings for your web app, see [Configure web apps in Azure App Service].</span></span>

<!-- URL List -->

[службе приложений Azure]: https://azure.microsoft.com/services/app-service/
[Azure Container Service]: https://azure.microsoft.com/services/container-service/
[Azure для разработчиков Java]: https://docs.microsoft.com/java/azure/
[портал Azure]: https://portal.azure.com/
[Настройка веб-приложений в службе приложений Azure]: /azure/app-service/web-sites-configure
[Развертывание приложения в службе приложений Azure с помощью FTP или FTPS]: https://docs.microsoft.com/azure/app-service/app-service-deploy-ftp
[бесплатной учетной записи Azure]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[инструментах Java для Visual Studio Team Services]: https://java.visualstudio.com/ (Инструменты Java для Visual Studio Team Services)
[Maven]: http://maven.apache.org/
[преимущества для подписчиков MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Boot Getting Started]: https://github.com/spring-guides/gs-spring-boot
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[SB01]: ./media/deploy-spring-boot-java-web-app-on-azure/SB01.png
[SB02]: ./media/deploy-spring-boot-java-web-app-on-azure/SB02.png

[AZ01]: ./media/deploy-spring-boot-java-web-app-on-azure/AZ01.png
[AZ02]: ./media/deploy-spring-boot-java-web-app-on-azure/AZ02.png
[AZ03]: ./media/deploy-spring-boot-java-web-app-on-azure/AZ03.png
[AZ04]: ./media/deploy-spring-boot-java-web-app-on-azure/AZ04.png
[AZ05]: ./media/deploy-spring-boot-java-web-app-on-azure/AZ05.png
[AZ06]: ./media/deploy-spring-boot-java-web-app-on-azure/AZ06.png
[AZ07]: ./media/deploy-spring-boot-java-web-app-on-azure/AZ07.png
[AZ08]: ./media/deploy-spring-boot-java-web-app-on-azure/AZ08.png
[AZ09]: ./media/deploy-spring-boot-java-web-app-on-azure/AZ09.png
[AZ10]: ./media/deploy-spring-boot-java-web-app-on-azure/AZ10.png
