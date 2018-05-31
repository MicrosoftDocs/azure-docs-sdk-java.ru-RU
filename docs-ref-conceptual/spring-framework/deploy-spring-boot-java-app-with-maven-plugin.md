---
title: Развертывание приложения Spring Boot в облаке с помощью Maven и Azure
description: Узнайте, как развернуть приложение Spring Boot в облаке с помощью подключаемого модуля Maven для веб-приложений Azure.
services: app-service
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: ''
ms.assetid: ''
ms.author: robmcm;kevinzha
ms.date: 02/01/2018
ms.devlang: java
ms.service: app-service
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: web
ms.openlocfilehash: 82cb0da3ce49fa77f888808af14455bf226d5cb0
ms.sourcegitcommit: 024b3127daf396a17bd43d57642e3534ae87f120
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/23/2018
ms.locfileid: "34462754"
---
# <a name="deploy-a-spring-boot-app-to-the-cloud-using-the-maven-plugin-for-azure-web-apps"></a>Развертывание приложения Spring Boot в облаке с помощью подключаемого модуля Maven для веб-приложений Azure

В этой статье демонстрируется использование подключаемого модуля Maven для веб-приложений Azure с целью развертывания примера приложения Spring Boot в службы приложений Azure.

> [!NOTE]
> 
> [Подключаемый модуль Maven для веб-приложений Azure](https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin) для [Apache Maven](http://maven.apache.org/) обеспечивает эффективную интеграцию службы приложений Azure в проекты Maven и упрощает процесс развертывания веб-приложений в службе приложений Azure.
> 
> Подключаемый модуль Maven для веб-приложений Azure в настоящее время доступен в предварительной версии. Сейчас поддерживается только FTP-публикация, но на будущее запланированы дополнительные функции.
> 

## <a name="prerequisites"></a>предварительным требованиям

Для работы с этим руководством требуется следующее:

* Подписка Azure. Если у вас ее еще нет, вы можете активировать [преимущества для подписчиков MSDN] или зарегистрироваться для получения [бесплатной учетной записи Azure].
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
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. Клонируйте образец проекта [Spring Boot Getting Started] в созданный каталог, например:
   ```shell
   git clone https://github.com/microsoft/gs-spring-boot
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

## <a name="create-an-azure-service-principal"></a>Создание субъекта-службы Azure

Из этого раздела вы узнаете, как создать субъект-службу Azure, с помощью которого подключаемый модуль Maven развертывает веб-приложение в Azure.

1. Откройте окно командной строки.

1. Войдите в учетную запись Azure с помощью интерфейса командной строки Azure.
   ```shell
   az login
   ```
   Для завершения процесса входа следуйте инструкциям.

1. Создайте субъект-службу Azure.
   ```shell
   az ad sp create-for-rbac --name "uuuuuuuu" --password "pppppppp"
   ```
   Где `uuuuuuuu` — это имя пользователя и `pppppppp` — пароль для субъекта-службы.

1. В ответ Azure предоставит код JSON, аналогичный приведенному ниже.
   ```json
   {
      "appId": "aaaaaaaa-aaaa-aaaa-aaaa-aaaaaaaaaaaa",
      "displayName": "uuuuuuuu",
      "name": "http://uuuuuuuu",
      "password": "pppppppp",
      "tenant": "tttttttt-tttt-tttt-tttt-tttttttttttt"
   }
   ```

   > [!NOTE]
   >
   > При настройке подключаемого модуля Maven для развертывания веб-приложения в Azure используйте значения из этого ответа JSON. `aaaaaaaa`, `uuuuuuuu`, `pppppppp` и `tttttttt` являются значениями заполнителя, которые используются в этом примере с целью упростить сопоставление этих значений с соответствующими им элементами во время настройки файла Maven `settings.xml` в следующем разделе.
   >
   >

## <a name="configure-maven-to-use-your-azure-service-principal"></a>Настройка Maven для использования субъекта-службы

Из этого раздела вы узнаете, как с помощью значений из субъекта-службы Azure настроить проверку подлинности, с помощью которой Maven развертывает веб-приложение в Azure.

1. Откройте файл Maven `settings.xml` в текстовом редакторе. Путь к этому файлу может быть похож на следующие примеры:
   * `/etc/maven/settings.xml`
   * `%ProgramFiles%\apache-maven\3.5.0\conf\settings.xml`
   * `$HOME/.m2/settings.xml`

1. Добавьте параметры субъекта-службы Azure из предыдущего раздела этого учебника в коллекцию `<servers>` в файле *settings.xml*, например:

   ```xml
   <servers>
      <server>
        <id>azure-auth</id>
         <configuration>
            <client>aaaaaaaa-aaaa-aaaa-aaaa-aaaaaaaaaaaa</client>
            <tenant>tttttttt-tttt-tttt-tttt-tttttttttttt</tenant>
            <key>pppppppp</key>
            <environment>AZURE</environment>
         </configuration>
      </server>
   </servers>
   ```
   Описание
   | Элемент | ОПИСАНИЕ |
   |---|---|
   | `<id>` | Задает уникальное имя, которое Maven использует для поиска параметров безопасности при развертывании веб-приложения в Azure. |
   | `<client>` | Содержит значение `appId` из субъекта-службы. |
   | `<tenant>` | Содержит значение `tenant` из субъекта-службы. |
   | `<key>` | Содержит значение `password` из субъекта-службы. |
   | `<environment>` | Определяет целевую облачную среду Azure, которой в этом примере является `AZURE`. (Полный список сред см. в документации по [Подключаемый модуль Maven для веб-приложений Azure].) |

1. Сохраните и закройте файл *settings.xml*.

## <a name="optional-customize-your-pomxml-before-deploying-your-web-app-to-azure"></a>НЕОБЯЗАТЕЛЬНО. Перед развертыванием веб-приложения в Azure настройте pom.xml.

Откройте файл `pom.xml` для приложения Spring Boot в текстовом редакторе, а затем найдите элемент `<plugin>` для `azure-webapp-maven-plugin`. Этот элемент должен выглядеть примерно следующим образом.

   ```xml
   <plugin>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-webapp-maven-plugin</artifactId>
      <version>0.1.3</version>
      <configuration>
         <authentication>
            <serverId>azure-auth</serverId>
         </authentication>
         <resourceGroup>maven-plugin</resourceGroup>
         <appName>maven-web-app-${maven.build.timestamp}</appName>
         <region>westus</region>
         <javaVersion>1.8</javaVersion>
         <deploymentType>ftp</deploymentType>
         <resources>
            <resource>
               <directory>${project.basedir}/target</directory>
               <targetPath>/</targetPath>
               <includes>
                  <include>*.jar</include>
               </includes>
            </resource>
            <resource>
               <directory>${project.basedir}</directory>
               <targetPath>/</targetPath>
               <includes>
                  <include>web.config</include>
               </includes>
            </resource>
         </resources>
      </configuration>
   </plugin>
   ```

Существует несколько значений, которые можно изменить для подключаемого модуля Maven. Подробное описание каждого из этих элементов см. в документации по [Подключаемый модуль Maven для веб-приложений Azure]. Существует ряд значений, на которые следует обратить внимание в этой статье.

| Элемент | ОПИСАНИЕ |
|---|---|
| `<version>` | Версия [Подключаемый модуль Maven для веб-приложений Azure]. Чтобы убедиться, что вы используете актуальную версию, проверьте, какая версия указана в списке версий в [центральном репозитории Maven](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22). |
| `<authentication>` | Сведения для проверки подлинности для Azure, в которых в данном примере содержится элемент `<serverId>`, который, в свою очередь, содержит `azure-auth`; Maven использует это значение для поиска значений субъекта-службы Azure в файле Maven *settings.xml*, который вы определили в предыдущем разделе этой статьи. |
| `<resourceGroup>` | Целевая группа ресурсов, которой в этом примере является `maven-plugin`. Если эта группа ресурсов не существует, она создается во время развертывания. |
| `<appName>` | Целевое имя веб-приложения. В этом примере целевое имя — `maven-web-app-${maven.build.timestamp}`, к которому в этом примере добавлен суффикс `${maven.build.timestamp}`, чтобы избежать конфликтов. (Метку времени добавлять необязательно; можно указать любую уникальную строку для имени приложения.) |
| `<region>` | Целевой регион, которым в данном примере является `westus`. (Полный список см. в документации по [Подключаемый модуль Maven для веб-приложений Azure].) |
| `<javaVersion>` | Версия среды выполнения Java для веб-приложения. (Полный список см. в документации по [Подключаемый модуль Maven для веб-приложений Azure].) |
| `<deploymentType>` | Тип развертывания для веб-приложения. Сейчас поддерживается только `ftp`, хотя поддержка других типов развертывания находится в разработке. |
| `<resources>` | Ресурсы и целевые назначения, которые Maven использует при развертывании веб-приложения в Azure. В этом примере два элемента `<resource>` указывают, что Maven развернет JAR-файл для веб-приложения и файл *web.config* из проекта Spring Boot. |

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

После развертывания веб-приложения вы сможете управлять им с помощью [портала Azure].

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
[портала Azure]: https://portal.azure.com/
[бесплатной учетной записи Azure]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[Преимущества для подписчиков MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Boot Getting Started]: https://github.com/microsoft/gs-spring-boot
[Spring Framework]: https://spring.io/
[Подключаемый модуль Maven для веб-приложений Azure]: https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin

<!-- IMG List -->

[AP01]: ./media/deploy-spring-boot-java-app-with-maven-plugin/AP01.png
[AP02]: ./media/deploy-spring-boot-java-app-with-maven-plugin/AP02.png
