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
ms.openlocfilehash: e78987a05527aef739bc1467511381665513a3ab
ms.sourcegitcommit: e017de4677c5bedd6ef88c8c1b6da279dc973efe
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/15/2018
ms.locfileid: "45639737"
---
# <a name="configure-a-spring-boot-initializer-app-to-use-application-insights"></a>Настройка Application Insights в инициализаторе Spring Boot

Из этой статьи вы узнаете, как с помощью **[Spring Initializr]** создать приложение Spring Boot, в котором используется начальное приложение Spring Boot для Azure Application Insights. Созданное приложение будет применяться для комплексного мониторинга приложений Java в облаке.

> [!NOTE]
> 
> *Начальное приложение находится на этапе **бета-версии (предварительная версия)*<em>.</em>

## <a name="prerequisites"></a>Предварительные требования

Чтобы выполнить действия, описанные в этой статье, необходимо следующее:

* Подписка Azure. Если у вас ее еще нет, вы можете активировать [Преимущества для подписчиков MSDN] или зарегистрироваться для получения [бесплатной учетной записи Azure].
* Пакет SDK для Java (JDK) версии 1.7 или 1.8.
* [Apache Maven](http://maven.apache.org/) версии 3.0 или более поздней.

## <a name="create-a-custom-application-using-the-spring-initializr"></a>Создание пользовательского приложения с помощью Spring Initializr

1. Перейдите по ссылке [https://start.spring.io/](https://start.spring.io/).

1. Укажите, что вам нужно создать проект **Maven** с **Java**, введите имена **группы** и **артефакта** для своего приложения и в разделе зависимостей выберите веб-зависимости.

   ![Основные параметры Spring Initializr][SI01]

   > [!NOTE]
   >
   > Spring Initializr использует имена **группы** и **артефакта** для создания имени пакета, например *com.example.demo*.
   >

1. Нажмите кнопку **создания проекта**.

1. При появлении запроса скачайте проект на локальный компьютер.

1. После извлечения файлов в локальной системе пользовательское приложение Spring Boot можно будет редактировать.

   ![Пользовательские файлы проекта Spring Boot][SI02]

## <a name="create-an-application-insights-resource-on-azure"></a>Создание ресурса Application Insights в Azure

1. Перейдите на портал Azure по адресу <https://portal.azure.com/> и щелкните **+Создать**.

   ![Портал Azure][AZ01]

1. Щелкните **Средства управления** и выберите **Application Insights**.

   ![Портал Azure][AZ02]

1. На странице **Новый ресурс Application Insights** укажите следующие сведения:

   * Введите **имя** ресурса Application Insights.
   * При выборе **типа приложения** укажите веб-приложение Java.
   * Выберите **подписку**, **группу ресурсов** и **расположение**.
   * Щелкните "Закрепить на панели мониторинга", если хотите закрепить плитку ресурса на портале Azure.

   Указав все эти параметры, нажмите кнопку **Создать**, чтобы создать ресурс Application Insights.

   ![Портал Azure][AZ03]

1. Когда ресурс будет создан, вы увидите его на **панели мониторинга** Azure, а также на странице **Все ресурсы**. В любом из этих расположений щелкните свой ресурс, чтобы открыть страницу обзора ресурса Application Insights. На странице обзора скопируйте **ключ инструментирования**.

   ![Портал Azure][AZ04]

## <a name="configure-your-downloaded-spring-boot-application-to-use-application-insights"></a>Настройка Application Insights в скачанном приложении Spring Boot

1. В корневом каталоге приложения найдите файл *POM.xml* и в разделе зависимостей добавьте следующую зависимость: 

```XML
 <dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>applicationinsights-spring-boot-starter</artifactId>
    <version>1.0.1-BETA</version>
</dependency>
```

1. Найдите файл *application.properties* в каталоге *resources* приложения или создайте файл, если он еще не существует.

   ![Поиск файла application.properties][RE01]

1. Откройте файл *application.properties* в текстовом редакторе, добавьте в него указанные ниже строки и замените примеры значений соответствующими свойствами с соответствующими учетными данными.

   ```yaml
   # Specify the instrumentation key of your Application Insights resource.
   azure.application-insights.instrumentation-key=[your ikey from the resource]
   # Specify the name of your springboot application. This can be any logical name you would like to give to your app.
   spring.application.name=[your app name]
   ```

   Дополнительные способы точной настройки Application Insights см.[здесь](https://github.com/Microsoft/ApplicationInsights-Java/blob/master/azure-application-insights-spring-boot-starter/README.md).

   > [!NOTE]
   > 
   > Для разных профилей (например, PROD, DEV и др.) можно использовать разные ключи инструментирования Application Insights. Дополнительные сведения см. [Свойства профилей Spring Boot]. 

1. Сохраните и закройте файл *application.properties*.

1. Создайте папку с именем *controller* в исходной папке пакета, например:

   `D:\Microsoft\demo\src\main\java\com\example\demo\controller`

   -или-

   `/users/example/home/demo/src/main/java/com/example/demo/controller`

1. В папке *controller* создайте файл с именем *TestController.java*. Откройте файл в текстовом редакторе и добавьте в него следующий код:

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

   В этом примере кода необходимо заменить `com.example.demo` именем пакета проекта.

1. Сохраните и закройте файл *TestController.java*.

1. Создайте приложение Spring Boot с помощью Maven и запустите его, например, следующим образом:

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

1. Протестируйте веб-приложение. Для этого перейдите в веб-браузере по адресу http://localhost:8080/sample/hello или используйте следующий синтаксис в cURL:

   ```shell
   curl http://localhost:8080/sample/hello
   ```

   Контроллер должен отобразить сообщение "hello!". Application Insights автоматически сохранит этот запрос и отправит его как элемент данных телеметрии вместе со связанным пользовательским событием, пользовательской метрикой, пользовательской зависимостью и пользовательской трассировкой (как указано в логике контроллера). 

   Через несколько секунд вы должны увидеть эти данные на портале Azure. 

   ![Портал Azure][AZ05]

   Щелкнув плитку "Схема приложений", можно просмотреть высокоуровневые компоненты и их взаимодействие друг с другом. Именно так мы рекомендуем получать общие сведения обо всем приложении. Каждая микрослужба Spring Boot распознается по имени приложения spring. Не забудьте указать его.

   ![Портал Azure][AZ08] 

## <a name="configure-springboot-application-to-send-log4j-logs-to-application-insights"></a>Настройка отправки журналов log4j приложения Springboot в Application Insights

1. Измените в проекте файл POM.xml, добавив в раздел зависимостей следующий код: 

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
        <version>1.0.1-BETA</version>
    </dependency>

    <dependency>
        <groupId>com.microsoft.azure</groupId>
        <artifactId>applicationinsights-logging-log4j2</artifactId>
        <version>2.1.1</version>
    </dependency>
</dependencies>
```

2. Сохраните и закройте файл *POM.xml*.

3. В папке \src\main\resources создайте файл *log4j2.xml* и настройте его. Например: 

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
4. Скомпилируйте и запустите приложения Spring Boot еще раз, как показано выше. 

Через несколько секунд вы должны увидеть все журналы spring на портале Azure. 

![Портал Azure][AZ06]

Можно даже просмотреть подробные сообщения журналов и проанализировать их на портале Analytics. 

![Портал Azure][AZ07]

## <a name="next-steps"></a>Дополнительная информация

Дополнительные сведения об использовании приложений Spring Boot в Azure см. в следующих статьях:

* [Развертывание приложения Spring Boot Application в службе приложений Azure](deploy-spring-boot-java-web-app-on-azure.md)

* [Запуск приложения Spring Boot в кластере Kubernetes в Службе контейнеров Azure](deploy-spring-boot-java-app-on-kubernetes.md)

Application Insights поддерживает автоматический сбор внешних зависимостей и его корреляцию с входящими запросами. Автоматический сбор сейчас поддерживается для Oracle, MsSQL, MySQL и Redis. Дополнительные сведения о включении автоматического сбора см. в статье [Мониторинг зависимостей, перехваченных исключений и времени выполнения методов в веб-приложениях Java](https://docs.microsoft.com/azure/application-insights/app-insights-java-agent).

Дополнительные сведения о службе Azure Application Insights и ее возможностях мониторинга см. **[Application Insights]**.

Дополнительные сведения о других настройках начального приложения Spring Boot для Application Insights см. по [этой ссылке](https://github.com/Microsoft/ApplicationInsights-Java/blob/master/azure-application-insights-spring-boot-starter/README.md).

Запросы на новые функции и сообщения о потенциальных ошибках оставляйте в нашем репозитории [GitHub](https://github.com/Microsoft/ApplicationInsights-Java/issues).

Дополнительные сведения об использовании Azure с Java см. в руководствах по [Azure для разработчиков Java] и [инструментах Java для Visual Studio Team Services].

**[Spring Framework]** — это решение с открытым кодом, которое помогает разработчикам Java создавать приложения корпоративного класса. Одним из самых популярных проектов, созданных на этой платформе, является проект [Spring Boot]. Он упрощает подход к созданию автономных приложений Java. В помощь разработчикам, начинающим работать со Spring Boot, по адресу [https://github.com/spring-guides/](https://github.com/spring-guides/) доступно несколько примеров пакетов этого приложения. Помимо выбора из списка основных проектов Spring Boot, **[Spring Initializr]** помогает разработчикам создавать пользовательские приложения Spring Boot.

<!-- URL List -->

[Azure для разработчиков Java]: https://docs.microsoft.com/java/azure/
[бесплатной учетной записи Azure]: https://azure.microsoft.com/pricing/free-trial/
[инструментах Java для Visual Studio Team Services]: https://java.visualstudio.com/
[Преимущества для подписчиков MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Свойства профилей Spring Boot]: https://docs.spring.io/spring-boot/docs/current/reference/html/boot-features-external-config.html#boot-features-external-config-profile-specific-properties
[Spring Initializr]: https://start.spring.io/
[Spring Framework]: https://spring.io/
[Application Insights]: https://docs.microsoft.com/azure/application-insights/

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
