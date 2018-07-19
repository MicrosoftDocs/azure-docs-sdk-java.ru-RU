---
title: Развертывание приложения Spring Boot в облаке с помощью Maven и Azure
description: Узнайте, как развернуть приложение Spring Boot в облаке с помощью подключаемого модуля Maven для Веб-приложений Azure.
services: app-service
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: brborges
ms.assetid: ''
ms.author: robmcm;kevinzha;brborges
ms.date: 06/01/2018
ms.devlang: java
ms.service: app-service
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: web
ms.openlocfilehash: 3610312ed17301131967bd2c047c86656de070e7
ms.sourcegitcommit: f313c14e92f38c54a3a583270ee85cc928cd39d7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/04/2018
ms.locfileid: "34689427"
---
# <a name="deploy-a-spring-boot-app-to-the-cloud-using-the-maven-plugin-for-azure-app-service"></a>Развертывание приложения Spring Boot в облаке с помощью подключаемого модуля Maven для Службы приложений Azure

В этой статье демонстрируется использование подключаемого модуля Maven для Веб-приложений Службы приложений Azure с целью развертывания примера приложения Spring Boot.

> [!NOTE]
> 
> [Подключаемый модуль Maven для Веб-приложений Службы приложений Azure](https://docs.microsoft.com/java/api/overview/azure/maven/azure-webapp-maven-plugin/readme) для [Apache Maven](http://maven.apache.org/) обеспечивает эффективную интеграцию Службы приложений Azure в проекты Maven и упрощает разработчикам развертывание веб-приложений в этой службе.

Прежде чем использовать подключаемый модуль Maven, проверьте центральный репозиторий Maven на наличие новой версии: [![Maven Central](https://img.shields.io/maven-central/v/com.microsoft.azure/azure-webapp-maven-plugin.svg)](http://search.maven.org/#search%7Cga%7C1%7Cg%3A%22com.microsoft.azure%22%20AND%20a%3A%22azure-webapp-maven-plugin%22). 

## <a name="prerequisites"></a>предварительным требованиям

Для работы с этим руководством требуется следующее:

* Подписка Azure. Если у вас ее еще нет, создайте [бесплатной учетной записи Azure].
* [Интерфейс командной строки Azure (CLI)].
* Актуальный [пакет разработчиков Java (JDK)] версии 1.7 или более поздней.
* Средство сборки [Maven] (версия 3) от Apache.
* Клиент [Git].

## <a name="clone-the-sample-spring-boot-web-app"></a>Клонирование примера "Веб-приложение Spring Boot"

Из этого раздела вы узнаете, как клонировать готовое приложение Spring Boot и протестировать его на локальном компьютере.

1. Откройте командную строку или окно терминала и создайте локальный каталог для размещения приложения Spring Boot, после чего перейдите в этот каталог, например:
   ```shell
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   -- или --
   ```shell
   md ~/SpringBoot
   cd ~/SpringBoot
   ```

1. Клонируйте образец проекта [Spring Boot Getting Started] в созданный каталог, например:
   ```shell
   git clone https://github.com/spring-guides/gs-spring-boot
   ```

1. Перейдите в каталог готового проекта, например:
   ```shell
   cd gs-spring-boot/complete
   ```

1. Выполните сборку файла JAR с помощью Maven, например:
   ```shell
   mvn clean package
   ```

1. При создании веб-приложения запустите веб-приложение с помощью Maven; например:
   ```shell
   mvn spring-boot:run
   ```

1. Проверьте веб-приложение, перейдя к нему локально с помощью веб-браузера. Например, если имеется Curl, можно использовать следующую команду:
   ```shell
   curl http://localhost:8080
   ```

1. Должно появиться следующее сообщение: **Greetings from Spring Boot!**

## <a name="adjust-project-for-war-based-deployment-on-azure-app-service"></a>Настройка проекта для развертывания из WAR-файла в Службе приложений Azure

В этом разделе мы быстро настроим развертывание проекта Spring Boot в Службе приложений Azure из WAR-файла. По умолчанию используется среда выполнения Tomcat. Для этого нам нужно изменить два файла:

- файл Maven `pom.xml`;
- класс Java `Application`.

Начнем с настроек Maven.

1. Откройте файл `pom.xml`.

1. В начале файла сразу после определения `<artifactId>` добавьте `<packaging>war</packaging>`.
   ```xml
    <modelVersion>4.0.0</modelVersion>
    <groupId>org.springframework</groupId>
    <artifactId>gs-spring-boot</artifactId>

    <packaging>war</packaging>
   ```

1. Добавьте следующую зависимость:
   ```xml
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-tomcat</artifactId>
            <scope>provided</scope>
        </dependency>
   ```

Теперь откройте класс `Application` (будем надеяться, что интегрированная среда разработки уже считала новые зависимости) и внесите в него следующие изменения:

1. Сделайте класс Application подклассом `SpringBootServletInitializer`.
   ```java
   @SpringBootApplication
   public class Application extends SpringBootServletInitializer {
     // ...
   }
   ```

1. Добавьте в класс Application следующий метод:
   ```java
       @Override
       protected SpringApplicationBuilder configure(SpringApplicationBuilder application) {
           return application.sources(Application.class);
       }
   ```

Теперь ваше приложение готово к развертыванию в Tomcat или любой другой среде выполнения сервлетов (например, Jetty).

## <a name="add-the-maven-plugin-for-azure-app-service-web-apps"></a>Добавление подключаемого модуля Maven для Веб-приложений Службы приложений Azure

В этом разделе мы добавим подключаемый модуль Maven, который автоматизирует весь процесс развертывания этого приложения в Веб-приложения Службы приложений Azure.

1. Откройте файл `pom.xml` еще раз.

1. В элементе `<properties>` укажите настраиваемый формат метки времени, используя свойство `maven.build.timestamp.format`. Так как Служба приложений Azure создает для вашего приложения общедоступный URL-адрес, этот параметр будет использоваться для создания имени развертывания, что позволит избежать конфликтов с развертываниями других пользователей.
   ```xml
    <properties>
        <java.version>1.8</java.version>
        <maven.build.timestamp.format>yyyyMMddHHmmssSSS</maven.build.timestamp.format>
    </properties>
   ```

1. В элементе `<plugins>` добавьте следующий код:
   ```xml
    <plugin>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-webapp-maven-plugin</artifactId>
      <!-- Check latest version on Maven Central -->
      <version>1.1.0</version>
    </plugin>
   ```

С такими параметрами проект Maven можно развертывать в Веб-приложениях Службы приложений Azure.

## <a name="install-and-log-in-to-azure-cli"></a>Установка и вход в Azure CLI

[Azure CLI](https://docs.microsoft.com/cli/azure/) — самый простой и наиболее удобный способ развернуть приложение Spring Boot с помощью подключаемого модуля Maven. Установите этот компонент.

1. Войдите в учетную запись Azure с помощью интерфейса командной строки Azure.
   ```shell
   az login
   ```
   Для завершения процесса входа следуйте инструкциям.

## <a name="optionally-customize-pomxml-before-deploying"></a>Настройка файла pom.xml перед развертыванием (необязательный этап)

Откройте файл `pom.xml` для приложения Spring Boot в текстовом редакторе, а затем найдите элемент `<plugin>` для `azure-webapp-maven-plugin`. Этот элемент должен выглядеть примерно следующим образом.

   ```xml
  <plugins>
    <plugin>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-webapp-maven-plugin</artifactId>
      <!-- Check latest version on Maven Central -->
      <version>1.1.0</version>
      <configuration>
         <resourceGroup>maven-projects</resourceGroup>
         <appName>${project.artifactId}-${maven.build.timestamp}</appName>
         <region>westus</region>
         <javaVersion>1.8</javaVersion>
         <deploymentType>war</deploymentType>
      </configuration>
    </plugin>
  </plugins>
   ```

Существует несколько значений, которые можно изменить для подключаемого модуля Maven. Подробное описание каждого из этих элементов см. в документации по [Подключаемый модуль Maven для веб-приложений Azure]. Существует ряд значений, на которые следует обратить внимание в этой статье.

| Элемент | ОПИСАНИЕ |
|---|---|
| `<version>` | Версия [Подключаемый модуль Maven для веб-приложений Azure]. Чтобы убедиться, что вы используете актуальную версию, проверьте, какая версия указана в списке версий в [центральном репозитории Maven](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22). |
| `<resourceGroup>` | Целевая группа ресурсов, которой в этом примере является `maven-plugin`. Если эта группа ресурсов не существует, она создается во время развертывания. |
| `<appName>` | Целевое имя веб-приложения. В этом примере целевое имя — `maven-web-app-${maven.build.timestamp}`, к которому в этом примере добавлен суффикс `${maven.build.timestamp}`, чтобы избежать конфликтов. (Метку времени добавлять необязательно; можно указать любую уникальную строку для имени приложения.) |
| `<region>` | Целевой регион, которым в данном примере является `westus`. (Полный список см. в документации по [Подключаемый модуль Maven для веб-приложений Azure].) |
| `<javaVersion>` | Версия среды выполнения Java для веб-приложения. (Полный список см. в документации по [Подключаемый модуль Maven для веб-приложений Azure].) |
| `<deploymentType>` | Тип развертывания для веб-приложения. Значение по умолчанию — `war`. |

## <a name="build-and-deploy-your-web-app-to-azure"></a>Сборка и развертывание веб-приложения в Azure

После настройки всех параметров в предыдущих разделах этой статьи можно приступать к развертыванию веб-приложения в Azure. Для этого выполните следующие действия.

1. В командной строке или в окне терминала, которые вы использовали ранее, перестройте JAR-файл, используя Maven, если вы внесли изменения в файл *pom.xml*; например:
   ```shell
   mvn clean package
   ```

1. Разверните веб-приложение в Azure с помощью Maven; например:
   ```shell
   mvn azure-webapp:deploy
   ```

Maven выполнит развертывание веб-приложения в Azure; если веб-приложение еще не существует, оно будет создано.

После развертывания веб-приложения вы сможете управлять им с помощью [портал Azure].

* Веб-приложение будет указано в разделе **Службы приложений**:

   ![Веб-приложение в разделе "Службы приложений" на портале Azure][AP01]

* URL-адрес веб-приложения будет указан в разделе **Обзор** для вашего веб-приложения:

   ![Определение URL-адреса для веб-приложения][AP02]

<!--
##  OPTIONAL: Configure the embedded Tomcat server to run on a different port

The embedded Tomcat server in the sample Spring Boot application is configured to run on port 8080 by default. However, if you want to run the embedded Tomcat server to run on a different port, such as port 80 for local testing, you can configure the port by using the following steps.

1. Go to the *resources* directory (or create the directory if it does not exist); for example:
   ```shell
   cd src/main/resources
   ```

1. Open the *application.yml* file in a text editor if it exists, or create a new YAML file if it does not exist.

1. Modify the **server** setting so that the server runs on port 80; for example:
   ```yaml
   server:
      port: 80
   ```

1. Save and close the *application.yml* file.
-->

## <a name="next-steps"></a>Дополнительная информация

Дополнительные сведения о различных технологиях, рассматриваемых в данной статье, см. в следующих статьях.

* [Подключаемый модуль Maven для веб-приложений Azure]

* [Вход в Azure из интерфейса командной строки Azure](/azure/xplat-cli-connect)

* [Развертывание приложения Spring Boot в Azure с помощью подключаемого модуля Maven для веб-приложений Azure](deploy-containerized-spring-boot-java-app-with-maven-plugin.md)

* [Создание субъекта-службы Azure с помощью Azure CLI 2.0](/cli/azure/create-an-azure-service-principal-azure-cli)

* [Справочник по параметрам Maven](https://maven.apache.org/settings.html)

<!-- URL List -->

[Интерфейс командной строки Azure (CLI)]: /cli/azure/overview
[Azure for Java Developers]: https://docs.microsoft.com/java/azure/
[портал Azure]: https://portal.azure.com/
[бесплатной учетной записи Azure]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Boot Getting Started]: https://github.com/spring-guides/gs-spring-boot
[Spring Framework]: https://spring.io/
[Подключаемый модуль Maven для веб-приложений Azure]: https://docs.microsoft.com/java/api/overview/azure/maven/azure-webapp-maven-plugin/readme

<!-- IMG List -->

[AP01]: ./media/deploy-spring-boot-java-app-with-maven-plugin/AP01.png
[AP02]: ./media/deploy-spring-boot-java-app-with-maven-plugin/AP02.png
