---
title: Настройка начального приложения SpringBoot для Azure Application Insights в инициализаторе Spring Boot
description: Настройка начального приложения SpringBoot для Application Insights в приложении Spring Boot, созданном с помощью Spring Initializr.
services: Application-Insights
documentationcenter: java
author: dhaval24
manager: alexklim
editor: ''
ms.assetid: ''
ms.author: dhdoshi
ms.date: 05/19/2018
ms.devlang: java
ms.service: Azure Monitor
ms.tgt_pltfrm: application-insights
ms.topic: article
ms.workload: na
ms.openlocfilehash: 0e57bfb304185b8b98dedfdecb2e0374c4a72fe5
ms.sourcegitcommit: 5282a51bf31771671df01af5814df1d2b8e4620c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/28/2018
ms.locfileid: "37090777"
---
# <a name="configure-a-spring-boot-initializer-app-to-use-application-insights"></a><span data-ttu-id="4f035-103">Настройка Application Insights в инициализаторе Spring Boot</span><span class="sxs-lookup"><span data-stu-id="4f035-103">Configure a Spring Boot Initializer app to use Application Insights</span></span>

<span data-ttu-id="4f035-104">Из этой статьи вы узнаете, как с помощью **[Spring Initializr]** создать приложение Spring Boot, в котором используется начальное приложение Spring Boot для Azure Application Insights. Созданное приложение будет применяться для комплексного мониторинга приложений Java в облаке.</span><span class="sxs-lookup"><span data-stu-id="4f035-104">This article walks you through creating a Spring Boot application using **[Spring Initializr]**, that uses Azure Application Insights Spring Boot Starter for end-to-end monitoring of Java applications on cloud.</span></span>

> [!NOTE]
> 
> <span data-ttu-id="4f035-105">*Начальное приложение находится на этапе **бета-версии (предварительная версия)*<em>.</em></span><span class="sxs-lookup"><span data-stu-id="4f035-105">*This starter is currently in **BETA (public preview)*<em>.</em></span></span>

## <a name="prerequisites"></a><span data-ttu-id="4f035-106">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="4f035-106">Prerequisites</span></span>

<span data-ttu-id="4f035-107">Чтобы выполнить действия, описанные в этой статье, необходимо следующее:</span><span class="sxs-lookup"><span data-stu-id="4f035-107">The following prerequisites are required in order to complete the steps in this article:</span></span>

* <span data-ttu-id="4f035-108">Подписка Azure. Если у вас ее еще нет, вы можете активировать [Преимущества для подписчиков MSDN] или зарегистрироваться для получения [бесплатной учетной записи Azure].</span><span class="sxs-lookup"><span data-stu-id="4f035-108">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="4f035-109">Пакет SDK для Java (JDK) версии 1.7 или 1.8.</span><span class="sxs-lookup"><span data-stu-id="4f035-109">A Java Development Kit (JDK), version 1.7 and 1.8.</span></span>
* <span data-ttu-id="4f035-110">[Apache Maven](http://maven.apache.org/) версии 3.0 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="4f035-110">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>

## <a name="create-a-custom-application-using-the-spring-initializr"></a><span data-ttu-id="4f035-111">Создание пользовательского приложения с помощью Spring Initializr</span><span class="sxs-lookup"><span data-stu-id="4f035-111">Create a custom application using the Spring Initializr</span></span>

1. <span data-ttu-id="4f035-112">Перейдите по ссылке [https://start.spring.io/](https://start.spring.io/).</span><span class="sxs-lookup"><span data-stu-id="4f035-112">Browse to [https://start.spring.io/](https://start.spring.io/).</span></span>

1. <span data-ttu-id="4f035-113">Укажите, что вам нужно создать проект **Maven** с **Java**, введите имена **группы** и **артефакта** для своего приложения и в разделе зависимостей выберите веб-зависимости.</span><span class="sxs-lookup"><span data-stu-id="4f035-113">Specify that you want to generate a **Maven** project with **Java**, enter the **Group** and **Artifact** names for your application, and then select web dependency in the dependenies section.</span></span>

   ![Основные параметры Spring Initializr][SI01]

   > [!NOTE]
   >
   > <span data-ttu-id="4f035-115">Spring Initializr использует имена **группы** и **артефакта** для создания имени пакета, например *com.example.demo*.</span><span class="sxs-lookup"><span data-stu-id="4f035-115">The Spring Initializr will use the **Group** and **Artifact** names to create the package name; for example: *com.example.demo*.</span></span>
   >

1. <span data-ttu-id="4f035-116">Нажмите кнопку **создания проекта**.</span><span class="sxs-lookup"><span data-stu-id="4f035-116">Click the button to **Generate Project**.</span></span>

1. <span data-ttu-id="4f035-117">При появлении запроса скачайте проект на локальный компьютер.</span><span class="sxs-lookup"><span data-stu-id="4f035-117">When prompted, download the project to a path on your local computer.</span></span>

1. <span data-ttu-id="4f035-118">После извлечения файлов в локальной системе пользовательское приложение Spring Boot можно будет редактировать.</span><span class="sxs-lookup"><span data-stu-id="4f035-118">After you have extracted the files on your local system, your custom Spring Boot application will be ready for editing.</span></span>

   ![Пользовательские файлы проекта Spring Boot][SI02]

## <a name="create-an-application-insights-resource-on-azure"></a><span data-ttu-id="4f035-120">Создание ресурса Application Insights в Azure</span><span class="sxs-lookup"><span data-stu-id="4f035-120">Create an Application Insights Resource on Azure</span></span>

1. <span data-ttu-id="4f035-121">Перейдите на портал Azure по адресу <https://portal.azure.com/> и щелкните **+Создать**.</span><span class="sxs-lookup"><span data-stu-id="4f035-121">Browse to the Azure portal at <https://portal.azure.com/> and click **+New**.</span></span>

   ![Портал Azure][AZ01]

1. <span data-ttu-id="4f035-123">Щелкните **Средства управления** и выберите **Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="4f035-123">Click **Management Tools**, and then click **Application Insights**.</span></span>

   ![Портал Azure][AZ02]

1. <span data-ttu-id="4f035-125">На странице **Новый ресурс Application Insights** укажите следующие сведения:</span><span class="sxs-lookup"><span data-stu-id="4f035-125">On the **New Application Insights Resource** page, specify the following information:</span></span>

   * <span data-ttu-id="4f035-126">Введите **имя** ресурса Application Insights.</span><span class="sxs-lookup"><span data-stu-id="4f035-126">Enter the **Name** for your Application Insights resource.</span></span>
   * <span data-ttu-id="4f035-127">При выборе **типа приложения** укажите веб-приложение Java.</span><span class="sxs-lookup"><span data-stu-id="4f035-127">Choose the **Application Type** to Java Web Application.</span></span>
   * <span data-ttu-id="4f035-128">Выберите **подписку**, **группу ресурсов** и **расположение**.</span><span class="sxs-lookup"><span data-stu-id="4f035-128">Specify your **Subscription**, **Resource group** and **Location**.</span></span>
   * <span data-ttu-id="4f035-129">Щелкните "Закрепить на панели мониторинга", если хотите закрепить плитку ресурса на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="4f035-129">Select Pin to dashboard option, if you would like to pin the resource on your Azure portal.</span></span>

   <span data-ttu-id="4f035-130">Указав все эти параметры, нажмите кнопку **Создать**, чтобы создать ресурс Application Insights.</span><span class="sxs-lookup"><span data-stu-id="4f035-130">When you have specified these options, click **Create** to create your Application Insights resource.</span></span>

   ![Портал Azure][AZ03]

1. <span data-ttu-id="4f035-132">Когда ресурс будет создан, вы увидите его на **панели мониторинга** Azure, а также на странице **Все ресурсы**.</span><span class="sxs-lookup"><span data-stu-id="4f035-132">Once your resource has been created, you will see it listed on your Azure **Dashboard**, as well as under the **All Resources** pages.</span></span> <span data-ttu-id="4f035-133">В любом из этих расположений щелкните свой ресурс, чтобы открыть страницу обзора ресурса Application Insights.</span><span class="sxs-lookup"><span data-stu-id="4f035-133">You can click on your resource on any of those locations to open the overview page of the Application Insights resource.</span></span> <span data-ttu-id="4f035-134">На странице обзора скопируйте **ключ инструментирования**.</span><span class="sxs-lookup"><span data-stu-id="4f035-134">From this overview page please copy the **instrumentation key**.</span></span>

   ![Портал Azure][AZ04]

## <a name="configure-your-downloaded-spring-boot-application-to-use-application-insights"></a><span data-ttu-id="4f035-136">Настройка Application Insights в скачанном приложении Spring Boot</span><span class="sxs-lookup"><span data-stu-id="4f035-136">Configure your downloaded Spring Boot Application to use Application Insights</span></span>

1. <span data-ttu-id="4f035-137">В корневом каталоге приложения найдите файл *POM.xml* и в разделе зависимостей добавьте следующую зависимость:</span><span class="sxs-lookup"><span data-stu-id="4f035-137">Locate the *POM.xml* file in the root directory of your app, and add the following dependency in its dependencies section.</span></span> 

```XML
 <dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>applicationinsights-spring-boot-starter</artifactId>
    <version>1.0.0-BETA</version>
</dependency>
```

1. <span data-ttu-id="4f035-138">В программном каталоге *resources* найдите файл *application.properties*. Если такой файл не существует, создайте его.</span><span class="sxs-lookup"><span data-stu-id="4f035-138">Locate the *application.properties* file in the *resources* directory of your app, or create the file if it does not already exist.</span></span>

   ![Поиск файла application.properties][RE01]

1. <span data-ttu-id="4f035-140">Откройте файл *application.properties* в текстовом редакторе, добавьте в него указанные ниже строки и замените примеры значений соответствующими свойствами с соответствующими учетными данными.</span><span class="sxs-lookup"><span data-stu-id="4f035-140">Open the *application.properties* file in a text editor, and add the following lines to the file, and replace the sample values with the appropriate properties with appropriate credentials:</span></span>

   ```yaml
   # Specify the instrumentation key of your Application Insights resource.
   azure.application-insights.instrumentation-key=[your ikey from the resource]
   # Specify the name of your springboot application. This can be any logical name you would like to give to your app.
   spring.application.name=[your app name]
   ```

   <span data-ttu-id="4f035-141">Дополнительные способы точной настройки Application Insights см.[здесь](https://github.com/Microsoft/ApplicationInsights-Java/blob/master/azure-application-insights-spring-boot-starter/README.md).</span><span class="sxs-lookup"><span data-stu-id="4f035-141">For more ways to fine tune Application Insights please refer to [Application Insights Springboot starter readme](https://github.com/Microsoft/ApplicationInsights-Java/blob/master/azure-application-insights-spring-boot-starter/README.md).</span></span>

   > [!NOTE]
   > 
   > <span data-ttu-id="4f035-142">Для разных профилей (например, PROD, DEV и др.) можно использовать разные ключи инструментирования</span><span class="sxs-lookup"><span data-stu-id="4f035-142">You can use different Application Insights instrumentation keys (i.e</span></span> <span data-ttu-id="4f035-143">Application Insights. Дополнительные сведения см. [Свойства профилей Spring Boot].</span><span class="sxs-lookup"><span data-stu-id="4f035-143">different resources) for different profiles like PROD, DEV etc. Please refer to [Spring Boot Profile Specific Properties] for additional information.</span></span> 

1. <span data-ttu-id="4f035-144">Сохраните и закройте файл *application.properties*.</span><span class="sxs-lookup"><span data-stu-id="4f035-144">Save and close the *application.properties* file.</span></span>

1. <span data-ttu-id="4f035-145">Создайте папку с именем *controller* в исходной папке пакета, например:</span><span class="sxs-lookup"><span data-stu-id="4f035-145">Create a folder named *controller* under the source folder for your package; for example:</span></span>

   `D:\Microsoft\demo\src\main\java\com\example\demo\controller`

   <span data-ttu-id="4f035-146">-или-</span><span class="sxs-lookup"><span data-stu-id="4f035-146">-or-</span></span>

   `/users/example/home/demo/src/main/java/com/example/demo/controller`

1. <span data-ttu-id="4f035-147">В папке *controller* создайте файл с именем *TestController.java*.</span><span class="sxs-lookup"><span data-stu-id="4f035-147">Create a new file named *TestController.java* in the *controller* folder.</span></span> <span data-ttu-id="4f035-148">Откройте файл в текстовом редакторе и добавьте в него следующий код:</span><span class="sxs-lookup"><span data-stu-id="4f035-148">Open the file in a text editor and add the following code to it:</span></span>

   ```java
    package com.example.demo;

    import com.microsoft.applicationinsights.TelemetryClient;
    import java.io.IOException;
    import org.springframework.beans.factory.annotation.Autowired;
    import org.springframework.web.bind.annotation.GetMapping;
    import org.springframework.web.bind.annotation.RequestMapping;
    import org.springframework.web.bind.annotation.RestController;
    import com.microsoft.applicationinsights.telemetry.Duration;

    @RestController
    @RequestMapping("/sample")
    public class TestController {

        @Autowired
        TelemetryClient telemetryClient;

        @GetMapping("/hello")
        public String hello() {

            //track a custom event  
            telemetryClient.trackEvent("Sending a custom event...");

            //trace a custom trace
            telemetryClient.trackTrace("Sending a custom trace....");

            //track a custom metric
            telemetryClient.trackMetric("custom metric", 1.0);

            //track a custom dependency
            telemetryClient.trackDependency("SQL", "Insert", new Duration(0, 0, 1, 1, 1), true);

            return "hello";
        }
    }
   ```

   <span data-ttu-id="4f035-149">В этом примере кода необходимо заменить `com.example.demo` именем пакета проекта.</span><span class="sxs-lookup"><span data-stu-id="4f035-149">Where you will need to replace `com.example.demo` with the package name for your project.</span></span>

1. <span data-ttu-id="4f035-150">Сохраните и закройте файл *TestController.java*.</span><span class="sxs-lookup"><span data-stu-id="4f035-150">Save and close the *TestController.java* file.</span></span>

1. <span data-ttu-id="4f035-151">Создайте приложение Spring Boot с помощью Maven и запустите его, например, следующим образом:</span><span class="sxs-lookup"><span data-stu-id="4f035-151">Build your Spring Boot application with Maven and run it; for example:</span></span>

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

1. <span data-ttu-id="4f035-152">Протестируйте веб-приложение. Для этого перейдите в веб-браузере по адресу http://localhost:8080/sample/hello или используйте следующий синтаксис в cURL:</span><span class="sxs-lookup"><span data-stu-id="4f035-152">Test the web app by browsing to http://localhost:8080/sample/hello using a web browser, or use the syntax like the following example if you have curl available:</span></span>

   ```shell
   curl http://localhost:8080/sample/hello
   ```

   <span data-ttu-id="4f035-153">Контроллер должен отобразить сообщение</span><span class="sxs-lookup"><span data-stu-id="4f035-153">You should see the "hello!"</span></span> <span data-ttu-id="4f035-154">"hello!".</span><span class="sxs-lookup"><span data-stu-id="4f035-154">message from your sample controller displayed.</span></span> <span data-ttu-id="4f035-155">Application Insights автоматически сохранит этот запрос и отправит его как элемент данных телеметрии вместе со связанным пользовательским событием, пользовательской метрикой, пользовательской зависимостью и пользовательской трассировкой (как указано в логике контроллера).</span><span class="sxs-lookup"><span data-stu-id="4f035-155">Application Insights will automatically collect this request and send it as a telemetry item with it's associated custom event, custom metric, custom dependency and custom trace as specified in the controller logic.</span></span> 

   <span data-ttu-id="4f035-156">Через несколько секунд вы должны увидеть эти данные на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="4f035-156">After a few seconds you should see the data on Azure portal.</span></span> 

   ![Портал Azure][AZ05]

   <span data-ttu-id="4f035-158">Щелкнув плитку "Схема приложений", можно просмотреть высокоуровневые компоненты и их взаимодействие друг с другом.</span><span class="sxs-lookup"><span data-stu-id="4f035-158">You can click on Application Map tile to view high level components and their interaction with each other.</span></span> <span data-ttu-id="4f035-159">Именно так мы рекомендуем получать общие сведения обо всем приложении.</span><span class="sxs-lookup"><span data-stu-id="4f035-159">This is a recommended place to get a high level overview of entire application.</span></span> <span data-ttu-id="4f035-160">Каждая микрослужба Spring Boot распознается по имени приложения spring.</span><span class="sxs-lookup"><span data-stu-id="4f035-160">Each Spring Boot Microservice is recognized by the spring application name.</span></span> <span data-ttu-id="4f035-161">Не забудьте указать его.</span><span class="sxs-lookup"><span data-stu-id="4f035-161">Please remember to set it.</span></span>

   ![Портал Azure][AZ08] 

## <a name="configure-springboot-application-to-send-log4j-logs-to-application-insights"></a><span data-ttu-id="4f035-163">Настройка отправки журналов log4j приложения Springboot в Application Insights</span><span class="sxs-lookup"><span data-stu-id="4f035-163">Configure Springboot Application to send log4j logs to Application Insights</span></span>

1. <span data-ttu-id="4f035-164">Измените в проекте файл POM.xml, добавив в раздел зависимостей следующий код:</span><span class="sxs-lookup"><span data-stu-id="4f035-164">Modify the POM.xml file of the project and add/modify the dependencies section with following.</span></span> 

```xml
<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
        <exclusions>
            <exclusion>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-starter-logging</artifactId>
            </exclusion>
        </exclusions>
    </dependency>

    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-test</artifactId>
        <scope>test</scope>
    </dependency>

    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-log4j2</artifactId>
    </dependency>

    <dependency>
        <groupId>com.microsoft.azure</groupId>
        <artifactId>applicationinsights-spring-boot-starter</artifactId>
        <version>1.0.0-BETA</version>
    </dependency>

    <dependency>
        <groupId>com.microsoft.azure</groupId>
        <artifactId>applicationinsights-logging-log4j2</artifactId>
        <version>2.1.1</version>
    </dependency>
</dependencies>
```

2. <span data-ttu-id="4f035-165">Сохраните и закройте файл *POM.xml*.</span><span class="sxs-lookup"><span data-stu-id="4f035-165">Save and close the *POM.xml* file.</span></span>

3. <span data-ttu-id="4f035-166">В папке \src\main\resources создайте файл *log4j2.xml* и настройте его.</span><span class="sxs-lookup"><span data-stu-id="4f035-166">In \src\main\resources folder, create a new file *log4j2.xml* and configure it.</span></span> <span data-ttu-id="4f035-167">Например: </span><span class="sxs-lookup"><span data-stu-id="4f035-167">For example:</span></span>

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<Configuration packages="com.microsoft.applicationinsights.log4j.v2">
  <Properties>
    <Property name="LOG_PATTERN">
      %d{yyyy-MM-dd HH:mm:ss.SSS} %5p ${hostName} --- [%15.15t] %-40.40c{1.} : %m%n%ex
    </Property>
  </Properties>
  <Appenders>
    <Console name="Console" target="SYSTEM_OUT">
      <PatternLayout pattern="%d{HH:mm:ss.SSS} [%t] %-5level %logger{36} - %msg%n"/>
    </Console>
    <ApplicationInsightsAppender name="aiAppender">
    </ApplicationInsightsAppender>
  </Appenders>
  <Loggers>
    <Root level="trace">
      <AppenderRef ref="Console"  />
      <AppenderRef ref="aiAppender"  />
    </Root>
  </Loggers>
</Configuration>
```
4. <span data-ttu-id="4f035-168">Скомпилируйте и запустите приложения Spring Boot еще раз, как показано выше.</span><span class="sxs-lookup"><span data-stu-id="4f035-168">Build and run the Spring Boot application again as shown above.</span></span> 

<span data-ttu-id="4f035-169">Через несколько секунд вы должны увидеть все журналы spring на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="4f035-169">Within few seconds, you should see all the spring logs being available on Azure Portal.</span></span> 

![Портал Azure][AZ06]

<span data-ttu-id="4f035-171">Можно даже просмотреть подробные сообщения журналов и проанализировать их на портале Analytics.</span><span class="sxs-lookup"><span data-stu-id="4f035-171">You can even look at the detailed log messages and do analysis on Analytics Portal.</span></span> 

![Портал Azure][AZ07]

## <a name="next-steps"></a><span data-ttu-id="4f035-173">Дополнительная информация</span><span class="sxs-lookup"><span data-stu-id="4f035-173">Next steps</span></span>

<span data-ttu-id="4f035-174">Дополнительные сведения об использовании приложений Spring Boot в Azure см. в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="4f035-174">For more information about using Spring Boot applications on Azure, see the following articles:</span></span>

* [<span data-ttu-id="4f035-175">Развертывание приложения Spring Boot Application в службе приложений Azure</span><span class="sxs-lookup"><span data-stu-id="4f035-175">Deploy a Spring Boot Application to the Azure App Service</span></span>](deploy-spring-boot-java-web-app-on-azure.md)

* [<span data-ttu-id="4f035-176">Запуск приложения Spring Boot в кластере Kubernetes в Службе контейнеров Azure</span><span class="sxs-lookup"><span data-stu-id="4f035-176">Running a Spring Boot Application on a Kubernetes Cluster in the Azure Container Service</span></span>](deploy-spring-boot-java-app-on-kubernetes.md)

<span data-ttu-id="4f035-177">Application Insights поддерживает автоматический сбор внешних зависимостей и его корреляцию с входящими запросами.</span><span class="sxs-lookup"><span data-stu-id="4f035-177">Application Insights supports automatic collection of external dependencies and its correlation with incoming requests.</span></span> <span data-ttu-id="4f035-178">Автоматический сбор сейчас поддерживается для Oracle, MsSQL, MySQL и Redis.</span><span class="sxs-lookup"><span data-stu-id="4f035-178">Currently we support autocollection of Oracle, MsSQL, MySQL and Redis.</span></span> <span data-ttu-id="4f035-179">Дополнительные сведения о включении автоматического сбора см. в статье [Мониторинг зависимостей, перехваченных исключений и времени выполнения методов в веб-приложениях Java](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-java-agent).</span><span class="sxs-lookup"><span data-stu-id="4f035-179">For more details on enabling autocollection please follow the article [how to use Application Insights Java agent](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-java-agent).</span></span>

<span data-ttu-id="4f035-180">Дополнительные сведения о службе Azure Application Insights и ее возможностях мониторинга см. **[Application Insights]**.</span><span class="sxs-lookup"><span data-stu-id="4f035-180">For more information about Azure Application Insights, and it's monitoring capabilities, see the **[Application Insights]** home page.</span></span>

<span data-ttu-id="4f035-181">Дополнительные сведения о других настройках начального приложения Spring Boot для Application Insights см. по [этой ссылке](https://github.com/Microsoft/ApplicationInsights-Java/blob/master/azure-application-insights-spring-boot-starter/README.md).</span><span class="sxs-lookup"><span data-stu-id="4f035-181">For more information about additional configuration details of Application Insights Spring Boot Starter, please refer to this [link](https://github.com/Microsoft/ApplicationInsights-Java/blob/master/azure-application-insights-spring-boot-starter/README.md).</span></span>

<span data-ttu-id="4f035-182">Запросы на новые функции и сообщения о потенциальных ошибках оставляйте в нашем репозитории [GitHub](https://github.com/Microsoft/ApplicationInsights-Java/issues).</span><span class="sxs-lookup"><span data-stu-id="4f035-182">For feature requests and potential bugs, please open issues on our [GitHub](https://github.com/Microsoft/ApplicationInsights-Java/issues) repository.</span></span>

<span data-ttu-id="4f035-183">Дополнительные сведения об использовании Azure с Java см. в руководствах по [Azure для разработчиков Java] и [Java Tools for Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="4f035-183">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="4f035-184">**[Spring Framework]** — это решение с открытым кодом, которое помогает разработчикам Java создавать приложения корпоративного класса.</span><span class="sxs-lookup"><span data-stu-id="4f035-184">The **[Spring Framework]** is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="4f035-185">Одним из самых популярных проектов, созданных на этой платформе, является проект [Spring Boot]. Он упрощает подход к созданию автономных приложений Java.</span><span class="sxs-lookup"><span data-stu-id="4f035-185">One of the more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating stand-alone Java applications.</span></span> <span data-ttu-id="4f035-186">В помощь разработчикам, начинающим работать со Spring Boot, по адресу [https://github.com/spring-guides/](https://github.com/spring-guides/) доступно несколько примеров пакетов этого приложения.</span><span class="sxs-lookup"><span data-stu-id="4f035-186">To help developers get started with Spring Boot, several sample Spring Boot packages are available at [https://github.com/spring-guides/](https://github.com/spring-guides/).</span></span> <span data-ttu-id="4f035-187">Помимо выбора из списка основных проектов Spring Boot, **[Spring Initializr]** помогает разработчикам создавать пользовательские приложения Spring Boot.</span><span class="sxs-lookup"><span data-stu-id="4f035-187">In addition to choosing from the list of basic Spring Boot projects, the **[Spring Initializr]** helps developers get started with creating custom Spring Boot applications.</span></span>

<!-- URL List -->

[Azure для разработчиков Java]: https://docs.microsoft.com/java/azure/
[Azure for Java Developers]: https://docs.microsoft.com/java/azure/
[бесплатной учетной записи Azure]: https://azure.microsoft.com/pricing/free-trial/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/ (Инструменты Java для Visual Studio Team Services)
[Преимущества для подписчиков MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Свойства профилей Spring Boot]: https://docs.spring.io/spring-boot/docs/current/reference/html/boot-features-external-config.html#boot-features-external-config-profile-specific-properties
[Spring Boot Profile Specific Properties]: https://docs.spring.io/spring-boot/docs/current/reference/html/boot-features-external-config.html#boot-features-external-config-profile-specific-properties
[Spring Initializr]: https://start.spring.io/
[Spring Framework]: https://spring.io/
[Application Insights]: https://docs.microsoft.com/en-us/azure/application-insights/

<!-- IMG List -->

[AZ01]: ./media/configure-spring-boot-starter-java-app-with-azure-application-insights/Create_resource.png
[AZ02]: ./media/configure-spring-boot-starter-java-app-with-azure-application-insights/Create_resource_2.png
[AZ03]: ./media/configure-spring-boot-starter-java-app-with-azure-application-insights/Create_resource_3.png
[AZ04]: ./media/configure-spring-boot-starter-java-app-with-azure-application-insights/Get_IKey.png
[AZ05]: ./media/configure-spring-boot-starter-java-app-with-azure-application-insights/OverviewBladeResults.png
[AZ06]: ./media/configure-spring-boot-starter-java-app-with-azure-application-insights/Search_and_traces.png
[AZ07]: ./media/configure-spring-boot-starter-java-app-with-azure-application-insights/traces_details.png
[AZ08]: ./media/configure-spring-boot-starter-java-app-with-azure-application-insights/AppMap.png

[SI01]: ./media/configure-spring-boot-starter-java-app-with-azure-application-insights/spring_start.png
[SI02]: ./media/configure-spring-boot-starter-java-app-with-azure-application-insights/After_extract.png

[RE01]: ./media/configure-spring-boot-starter-java-app-with-azure-application-insights/applicationproperties_loc.png
[RE02]: ./media/configure-spring-boot-starter-java-app-with-azure-application-insights/applicationinsightsproperties.png
