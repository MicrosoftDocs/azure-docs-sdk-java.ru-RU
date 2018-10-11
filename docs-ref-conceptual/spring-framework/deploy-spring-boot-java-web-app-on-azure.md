---
title: Развертывание приложения Spring Boot в облаке с помощью службы приложений Azure
description: В этом руководстве приводятся пошаговые инструкции для разработчиков по развертыванию веб-приложения Spring Boot Getting Started в облаке с помощью службы приложений Azure.
services: app-service
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: ''
ms.assetid: ''
ms.author: asirveda;robmcm
ms.date: 02/01/2018
ms.devlang: java
ms.service: multiple
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: na
ms.openlocfilehash: adf779e2ba6ca73ea3a2406613f9622cc9ecbf99
ms.sourcegitcommit: b64017f119177f97da7a5930489874e67b09c0fc
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/09/2018
ms.locfileid: "48893165"
---
# <a name="deploy-a-spring-boot-application-to-the-cloud-with-azure-app-service"></a><span data-ttu-id="28f44-103">Развертывание приложения Spring Boot в облаке с помощью службы приложений Azure</span><span class="sxs-lookup"><span data-stu-id="28f44-103">Deploy a Spring Boot application to the cloud with Azure App Service</span></span>

<span data-ttu-id="28f44-104">В этом руководстве описано, как создать пример начального веб-приложения [Spring Boot] и развернуть его в [службе приложений Azure].</span><span class="sxs-lookup"><span data-stu-id="28f44-104">This tutorial will walk you though creating a sample [Spring Boot] Getting Started web app and deploying it to [Azure App Service].</span></span>

### <a name="prerequisites"></a><span data-ttu-id="28f44-105">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="28f44-105">Prerequisites</span></span>

<span data-ttu-id="28f44-106">Для работы с этим учебником требуется следующее.</span><span class="sxs-lookup"><span data-stu-id="28f44-106">In order to complete the steps in this tutorial, you need to have the following:</span></span>

* <span data-ttu-id="28f44-107">Подписка Azure; если у вас еще нет подписки Azure, вы можете активировать [преимущества для подписчиков MSDN] или зарегистрироваться для получения [Бесплатная учетная запись Azure].</span><span class="sxs-lookup"><span data-stu-id="28f44-107">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="28f44-108">Актуальная версия [Java Developer Kit (JDK)].</span><span class="sxs-lookup"><span data-stu-id="28f44-108">An up-to-date [Java Developer Kit (JDK)].</span></span>
* <span data-ttu-id="28f44-109">Средство сборки [Maven] (версия 3) от Apache.</span><span class="sxs-lookup"><span data-stu-id="28f44-109">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="28f44-110">Клиент [Git].</span><span class="sxs-lookup"><span data-stu-id="28f44-110">A [Git] client.</span></span>

## <a name="create-the-spring-boot-getting-started-web-app"></a><span data-ttu-id="28f44-111">Создание веб-приложения Spring Boot Getting Started</span><span class="sxs-lookup"><span data-stu-id="28f44-111">Create the Spring Boot Getting Started web app</span></span>

<span data-ttu-id="28f44-112">Ниже приводятся пошаговые инструкции по созданию простого веб-приложения Spring Boot и его локальному тестированию.</span><span class="sxs-lookup"><span data-stu-id="28f44-112">The following steps will walk you through the steps that are required to create a simple Spring Boot web application and test it locally.</span></span>

1. <span data-ttu-id="28f44-113">Откройте командную строку и создайте локальный каталог для размещения приложения, после чего перейдите в этот каталог, например:</span><span class="sxs-lookup"><span data-stu-id="28f44-113">Open a command-prompt and create a local directory to hold your application, and change to that directory; for example:</span></span>
   ```
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="28f44-114">-- или --</span><span class="sxs-lookup"><span data-stu-id="28f44-114">-- or --</span></span>
   ```
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="28f44-115">Клонируйте образец проекта [Spring Boot Getting Started] в созданный каталог, например:</span><span class="sxs-lookup"><span data-stu-id="28f44-115">Clone the [Spring Boot Getting Started] sample project into the directory you just created; for example:</span></span>
   ```
   git clone https://github.com/spring-guides/gs-spring-boot.git
   ```

1. <span data-ttu-id="28f44-116">Перейдите в каталог готового проекта, например:</span><span class="sxs-lookup"><span data-stu-id="28f44-116">Change directory to the completed project; for example:</span></span>
   ```
   cd gs-spring-boot
   cd complete
   ```

1. <span data-ttu-id="28f44-117">Выполните сборку файла JAR с помощью Maven, например:</span><span class="sxs-lookup"><span data-stu-id="28f44-117">Build the JAR file using Maven; for example:</span></span>
   ```
   mvn package
   ```

1. <span data-ttu-id="28f44-118">После создания веб-приложения перейдите к JAR-файлу и запустите веб-приложение, например:</span><span class="sxs-lookup"><span data-stu-id="28f44-118">Once the web app has been created, change directory to the JAR file and start the web app; for example:</span></span>
   ```
   cd target
   java -jar gs-spring-boot-0.1.0.jar
   ```

1. <span data-ttu-id="28f44-119">Протестируйте веб-приложение. Для этого перейдите в веб-браузере по адресу http://localhost:8080 или используйте следующий синтаксис в cURL:</span><span class="sxs-lookup"><span data-stu-id="28f44-119">Test the web app by browsing to http://localhost:8080 using a web browser, or use the syntax like the following example if you have curl available:</span></span>
   ```
   curl http://localhost:8080
   ```

1. <span data-ttu-id="28f44-120">Должно появиться следующее сообщение: **Greetings from Spring Boot!**</span><span class="sxs-lookup"><span data-stu-id="28f44-120">You should see the following message displayed: **Greetings from Spring Boot!**</span></span>

   ![Обзор образца приложения][SB01]

## <a name="create-an-azure-web-app-for-use-with-java"></a><span data-ttu-id="28f44-122">Создание веб-приложения Azure для использования с Java</span><span class="sxs-lookup"><span data-stu-id="28f44-122">Create an Azure web app for use with Java</span></span>

<span data-ttu-id="28f44-123">Ниже приведены пошаговые инструкции по созданию веб-приложения Azure, настройке необходимых параметров для Java и настройке учетных данных FTP.</span><span class="sxs-lookup"><span data-stu-id="28f44-123">The following steps will walk you through the steps to create an Azure Web App, configure the required settings for Java, and configure your FTP credentials.</span></span>

1. <span data-ttu-id="28f44-124">Перейдите на [портал Azure] и выполните вход.</span><span class="sxs-lookup"><span data-stu-id="28f44-124">Browse to the [Azure portal] and log in.</span></span>

1. <span data-ttu-id="28f44-125">Войдя в учетную запись на портале Azure, щелкните значок меню **Службы приложений**:</span><span class="sxs-lookup"><span data-stu-id="28f44-125">Once you have logged into your account on the Azure portal, click the menu icon for **App Services**:</span></span>
   
   ![Портал Azure][AZ01]

1. <span data-ttu-id="28f44-127">Когда откроется страница **Службы приложений**, щелкните **+ Добавить**, чтобы создать службу приложений.</span><span class="sxs-lookup"><span data-stu-id="28f44-127">When the **App Services** page is displayed, click **+ Add** to create a new App Service.</span></span>

   ![Создание службы приложений][AZ02]

1. <span data-ttu-id="28f44-129">Когда появится список шаблонов веб-приложений, щелкните ссылку базового веб-приложения Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="28f44-129">When the list of web app templates is displayed, click the link for the basic Microsoft Web App.</span></span>

   ![Шаблоны веб-приложений][AZ03]

1. <span data-ttu-id="28f44-131">Когда появится страница шаблона веб-приложения, нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="28f44-131">When the information page for the Web App template is displayed, click **Create**.</span></span>

   ![Создание веб-приложения][AZ04]

1. <span data-ttu-id="28f44-133">Укажите уникальное имя веб-приложения и задайте дополнительные параметры, после чего нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="28f44-133">Provide a unique name for your web app and specify any additional settings, and then **Create**.</span></span>

   ![Параметры создания веб-приложения][AZ05]

1. <span data-ttu-id="28f44-135">После создания веб-приложения щелкните значок меню **Службы приложений**, а затем выберите только что созданное веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="28f44-135">Once your web app has been created, click the menu icon for **App Services**, and then click your newly-created web app:</span></span>

   ![Список веб-приложений][AZ06]

1. <span data-ttu-id="28f44-137">Когда веб-приложение отобразится, укажите версию Java, выполнив указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="28f44-137">When your web app is displayed, specify the Java version by using the following steps:</span></span>

   <span data-ttu-id="28f44-138">a.</span><span class="sxs-lookup"><span data-stu-id="28f44-138">a.</span></span> <span data-ttu-id="28f44-139">Выберите пункт меню **Параметры приложения**.</span><span class="sxs-lookup"><span data-stu-id="28f44-139">Click the **Application Settings** menu item.</span></span>

   <span data-ttu-id="28f44-140">b.</span><span class="sxs-lookup"><span data-stu-id="28f44-140">b.</span></span> <span data-ttu-id="28f44-141">В качестве версии Java выберите **Java 8**.</span><span class="sxs-lookup"><span data-stu-id="28f44-141">Choose **Java 8** for the Java version.</span></span>

   <span data-ttu-id="28f44-142">c.</span><span class="sxs-lookup"><span data-stu-id="28f44-142">c.</span></span> <span data-ttu-id="28f44-143">В качестве дополнительного номера версии Java выберите **Самые новые**.</span><span class="sxs-lookup"><span data-stu-id="28f44-143">Choose **Newest** for the minor Java version.</span></span>

   <span data-ttu-id="28f44-144">d.</span><span class="sxs-lookup"><span data-stu-id="28f44-144">d.</span></span> <span data-ttu-id="28f44-145">В качестве веб-контейнера выберите **Последняя версия Tomcat 8.5**.</span><span class="sxs-lookup"><span data-stu-id="28f44-145">Choose **Newest Tomcat 8.5** for the web container.</span></span> <span data-ttu-id="28f44-146">(Этот контейнер в действительности не будет использоваться; Azure будет использовать контейнер в приложении Spring Boot.)</span><span class="sxs-lookup"><span data-stu-id="28f44-146">(This container will not actually be used; Azure will use the container from your Spring Boot application.)</span></span>

   <span data-ttu-id="28f44-147">д.</span><span class="sxs-lookup"><span data-stu-id="28f44-147">e.</span></span> <span data-ttu-id="28f44-148">Выберите команду **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="28f44-148">Click **Save**.</span></span>

   ![Параметры приложения][AZ07]

1. <span data-ttu-id="28f44-150">Укажите учетные данные FTP, выполнив указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="28f44-150">Specify your FTP deployment credentials by using the following steps:</span></span>

   <span data-ttu-id="28f44-151">a.</span><span class="sxs-lookup"><span data-stu-id="28f44-151">a.</span></span> <span data-ttu-id="28f44-152">Выберите пункт меню **Учетные данные развертывания**.</span><span class="sxs-lookup"><span data-stu-id="28f44-152">Click the **Deployment Credentials** menu item.</span></span>

   <span data-ttu-id="28f44-153">b.</span><span class="sxs-lookup"><span data-stu-id="28f44-153">b.</span></span> <span data-ttu-id="28f44-154">Укажите имя пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="28f44-154">Specify your username and password.</span></span>

   <span data-ttu-id="28f44-155">c.</span><span class="sxs-lookup"><span data-stu-id="28f44-155">c.</span></span> <span data-ttu-id="28f44-156">Выберите команду **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="28f44-156">Click **Save**.</span></span>

   ![Указание учетных данных развертывания][AZ08]

1. <span data-ttu-id="28f44-158">Получите сведения о подключении по FTP, выполнив указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="28f44-158">Retrieve your FTP connection information by using the following steps:</span></span>

   <span data-ttu-id="28f44-159">a.</span><span class="sxs-lookup"><span data-stu-id="28f44-159">a.</span></span> <span data-ttu-id="28f44-160">Выберите пункт меню **Учетные данные развертывания**.</span><span class="sxs-lookup"><span data-stu-id="28f44-160">Click the **Deployment Credentials** menu item.</span></span>

   <span data-ttu-id="28f44-161">b.</span><span class="sxs-lookup"><span data-stu-id="28f44-161">b.</span></span> <span data-ttu-id="28f44-162">Скопируйте полное имя пользователя и URL-адрес FTP, а затем сохраните их. Они понадобятся в следующем разделе этого учебника.</span><span class="sxs-lookup"><span data-stu-id="28f44-162">Copy your full FTP username and URL and save them for the next section of this tutorial.</span></span>

   ![URL-адрес и учетные данные FTP][AZ09]

## <a name="deploy-your-spring-boot-web-app-to-azure"></a><span data-ttu-id="28f44-164">Развертывание веб-приложения Spring Boot в Azure</span><span class="sxs-lookup"><span data-stu-id="28f44-164">Deploy your Spring Boot web app to Azure</span></span>

<span data-ttu-id="28f44-165">Ниже приведены пошаговые инструкции по развертыванию веб-приложения Spring Boot в Azure.</span><span class="sxs-lookup"><span data-stu-id="28f44-165">The following steps will walk you through the steps to deploy your Spring Boot web app to Azure.</span></span>

1. <span data-ttu-id="28f44-166">Откройте текстовый редактор, например Блокнот, и вставьте следующий текст в новый документ, а затем сохраните файл с именем *web.config*:</span><span class="sxs-lookup"><span data-stu-id="28f44-166">Open a text editor such as Windows Notepad and paste the following text into a new document, then save the file as *web.config*:</span></span>
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

1. <span data-ttu-id="28f44-167">После сохранения файла *web.config* в системе подключитесь к веб-приложению по FTP, используя URL-адрес, имя пользователя и пароль из предыдущего раздела этого учебника.</span><span class="sxs-lookup"><span data-stu-id="28f44-167">After you have saved the *web.config* file to your system, connect to your web app via FTP using the URL, username, and password from the preceding section of this tutorial.</span></span> <span data-ttu-id="28f44-168">Например: </span><span class="sxs-lookup"><span data-stu-id="28f44-168">For example:</span></span>
   ```
   ftp
   open waws-prod-sn0-000.ftp.azurewebsites.windows.net
   user wingtiptoys-springboot\wingtiptoysuser
   pass ********
   ```

1. <span data-ttu-id="28f44-169">Измените удаленный каталог на корневую папку веб-приложения (находящуюся по адресу */site/wwwroot*), а затем скопируйте JAR-файл приложения Spring Boot и файл *web.config*, созданный ранее.</span><span class="sxs-lookup"><span data-stu-id="28f44-169">Change the remote directory to the root folder of your web app, (which is at */site/wwwroot*), then copy the JAR file from your Spring Boot application and the *web.config* from earlier.</span></span> <span data-ttu-id="28f44-170">Например: </span><span class="sxs-lookup"><span data-stu-id="28f44-170">For example:</span></span>
   ```
   cd site/wwwroot
   put gs-spring-boot-0.1.0.jar
   put web.config
   ```

1. <span data-ttu-id="28f44-171">После развертывания файлов JAR и *web.config* в веб-приложении необходимо перезапустить его с помощью портала Azure:</span><span class="sxs-lookup"><span data-stu-id="28f44-171">After you have deployed your JAR and *web.config* files to your web app, you need to restart your web app using the Azure portal:</span></span>

   ![Перезапуск веб-приложения][AZ10]

1. <span data-ttu-id="28f44-173">Протестируйте веб-приложение, перейдя по его URL-адресу в веб-браузере, или, если имеется программа curl, используйте синтаксис, как в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="28f44-173">Test the web app by browsing to your web app's URL using a web browser, or use the syntax like the following example if you have curl available:</span></span>
   ```
   curl http://wingtiptoys-springboot.azurewebsites.net/
   ```

1. <span data-ttu-id="28f44-174">Должно появиться следующее сообщение: **Greetings from Spring Boot!**</span><span class="sxs-lookup"><span data-stu-id="28f44-174">You should see the following message displayed: **Greetings from Spring Boot!**</span></span>

   ![Обзор образца приложения][SB02]

## <a name="next-steps"></a><span data-ttu-id="28f44-176">Дополнительная информация</span><span class="sxs-lookup"><span data-stu-id="28f44-176">Next steps</span></span>

<span data-ttu-id="28f44-177">Дополнительные сведения об использовании приложений Spring Boot в Azure см. в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="28f44-177">For more information about using Spring Boot applications on Azure, see the following articles:</span></span>

* [<span data-ttu-id="28f44-178">Развертывание приложения Spring Boot в Linux в службе контейнеров Azure</span><span class="sxs-lookup"><span data-stu-id="28f44-178">Deploy a Spring Boot Application on Linux in the Azure Container Service</span></span>](deploy-spring-boot-java-app-on-linux.md)

* [<span data-ttu-id="28f44-179">Развертывание приложения Spring Boot в кластере Kubernetes в службе контейнеров Azure</span><span class="sxs-lookup"><span data-stu-id="28f44-179">Deploy a Spring Boot Application on a Kubernetes Cluster in the Azure Container Service</span></span>](deploy-spring-boot-java-app-on-kubernetes.md)

<span data-ttu-id="28f44-180">Дополнительные сведения об использовании Azure с Java см. в руководствах по [Azure для разработчиков Java] и [инструментах Java для Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="28f44-180">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="28f44-181">Дополнительные сведения о развертывании веб-приложений в Azure по FTP см. в статье [Развертывание приложения в службе приложений Azure с помощью FTP или FTPS].</span><span class="sxs-lookup"><span data-stu-id="28f44-181">For additional information about depoying web apps to Azure using FTP, see [Deploy your app to Azure App Service using FTP/S].</span></span>

<span data-ttu-id="28f44-182">Дополнительные сведения об образце проекта Spring Boot см. на странице [Spring Boot Getting Started].</span><span class="sxs-lookup"><span data-stu-id="28f44-182">For further details about the Spring Boot sample project, see [Spring Boot Getting Started].</span></span>

<span data-ttu-id="28f44-183">Справку по началу работы с собственными приложениями Spring Boot см. на странице **Spring Initializr**: https://start.spring.io/.</span><span class="sxs-lookup"><span data-stu-id="28f44-183">For help with getting started with your own Spring Boot applications, see the **Spring Initializr** at https://start.spring.io/.</span></span>

<span data-ttu-id="28f44-184">Дополнительные сведения о настройке дополнительных параметров для веб-приложения см. в статье [Настройка веб-приложений в службе приложений Azure].</span><span class="sxs-lookup"><span data-stu-id="28f44-184">For more information about configuring additional settings for your web app, see [Configure web apps in Azure App Service].</span></span>

<!-- URL List -->

[службе приложений Azure]: https://azure.microsoft.com/services/app-service/
[Azure App Service]: https://azure.microsoft.com/services/app-service/
[Azure Container Service]: https://azure.microsoft.com/services/container-service/
[Azure для разработчиков Java]: https://docs.microsoft.com/java/azure/
[Azure for Java Developers]: https://docs.microsoft.com/java/azure/
[портал Azure]: https://portal.azure.com/
[Azure portal]: https://portal.azure.com/
[Настройка веб-приложений в службе приложений Azure]: /azure/app-service/web-sites-configure
[Configure web apps in Azure App Service]: /azure/app-service/web-sites-configure
[Развертывание приложения в службе приложений Azure с помощью FTP или FTPS]: https://docs.microsoft.com/azure/app-service/app-service-deploy-ftp
[Deploy your app to Azure App Service using FTP/S]: https://docs.microsoft.com/azure/app-service/app-service-deploy-ftp
[Бесплатная учетная запись Azure]: https://azure.microsoft.com/pricing/free-trial/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[инструментах Java для Visual Studio Team Services]: https://java.visualstudio.com/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[Преимущества для подписчиков MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
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
