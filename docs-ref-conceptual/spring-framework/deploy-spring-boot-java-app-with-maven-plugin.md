---
title: Развертывание приложения Spring Boot в виде файла JAR в облаке с помощью Maven и Azure
description: Узнайте, как развернуть приложение Spring Boot в облаке с помощью подключаемого модуля Maven для веб-приложений Azure на платформе Linux.
services: app-service
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: brborges
ms.author: robmcm
ms.date: 12/19/2018
ms.devlang: java
ms.service: app-service
ms.topic: article
ms.openlocfilehash: 5df4ca6ae9f307d937d7dfa0f2c1765f2efde1a1
ms.sourcegitcommit: 733115fe0a7b5109b511b4a32490f8264cf91217
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/15/2019
ms.locfileid: "65625702"
---
# <a name="deploy-a-spring-boot-jar-file-web-app-to-azure-app-service-on-linux"></a>Развертывание веб-приложения Spring Boot в виде файла JAR в Службе приложений Azure на платформе Linux

В этой статье показано, как использовать [подключаемый модуль Maven для веб-приложений службы приложений Azure](/java/api/overview/azure/maven/azure-webapp-maven-plugin/readme), чтобы развернуть приложение Spring Boot, упакованное в виде файла JAR Java SE, в [Службе приложений Azure на платформе Linux](/azure/app-service/containers/). Развертывание Java SE является предпочтительным по сравнению с [Tomcat и файлами WAR](/azure/app-service/containers/quickstart-java) в тех случаях, когда нужно объединить зависимости, среду выполнения и файлы конфигурации приложения в единый артефакт, пригодный для развертывания.


Если у вас еще нет подписки Azure, [создайте бесплатную учетную запись Azure](https://azure.microsoft.com/free/?WT.mc_id=A261C142F), прежде чем начинать работу.

## <a name="prerequisites"></a>Предварительные требования

Для выполнения шагов, описанных в этом руководстве, вам понадобиться установить и настроить следующие компоненты:

* [Azure CLI](/cli/azure/) на локальном компьютере или в [Azure Cloud Shell](https://shell.azure.com).
* Поддерживаемая версия Java Development Kit (JDK). Дополнительные сведения о версиях JDK, доступных для разработки в Azure, см. в статье <https://aka.ms/azure-jdks>.
* Apache [Maven](https://maven.apache.org/) версии 3.
* Клиент [Git](https://git-scm.com/downloads).

## <a name="install-and-sign-in-to-azure-cli"></a>Установка и вход в Azure CLI

[Azure CLI](/cli/azure/) — самый простой и наиболее удобный способ развернуть приложение Spring Boot с помощью подключаемого модуля Maven.

Войдите в учетную запись Azure с помощью интерфейса командной строки Azure.
   
   ```shell
   az login
   ```
   
Для завершения процесса входа следуйте инструкциям.

## <a name="clone-the-sample-app"></a>Клонирования примера приложения

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

## <a name="configure-maven-plugin-for-azure-app-service"></a>Настройка подключаемого модуля Maven для Службы приложений Azure

В этом разделе вы настроите проект Spring Boot `pom.xml`, чтобы развернуть приложение в Службе приложений Azure на платформе Linux с помощью Maven.

1. Откройте файл `pom.xml` в редакторе кода.

2. В разделе `<build>` файла pom.xml добавьте следующую запись `<plugin>` внутри тега `<plugins>`.

   ```xml
   <plugin>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-webapp-maven-plugin</artifactId>
    <version>1.5.4</version>
    <configuration>
      <deploymentType>jar</deploymentType>

      <!-- configure app to run on port 80, required by App Service -->
      <appSettings>
        <property> 
          <name>JAVA_OPTS</name> 
          <value>-Dserver.port=80</value> 
        </property> 
      </appSettings>

      <!-- Web App information -->
      <resourceGroup>${RESOURCEGROUP_NAME}</resourceGroup>
      <appName>${WEBAPP_NAME}</appName>
      <region>${REGION}</region>  

      <!-- Java Runtime Stack for Web App on Linux-->
      <linuxRuntime>jre8</linuxRuntime>
    </configuration>
   </plugin>
   ```

3. Укажите нужные значения вместо следующих заполнителей в конфигурации подключаемого модуля:

| Placeholder | ОПИСАНИЕ |
| ----------- | ----------- |
| `RESOURCEGROUP_NAME` | Имя новой группы ресурсов, в которой создается веб-приложение. Поместив все ресурсы для приложения в группу, вы можете управлять ими совместно. Например, при удалении группы ресурсов все ресурсы, связанные с приложением, также удаляются. Укажите вместо этого значения уникальное имя новой группы ресурсов, например *TestResources*. Это имя группы ресурсов будет использоваться для удаления всех ресурсов Azure в следующем разделе. |
| `WEBAPP_NAME` | Имя приложения будет частью имени узла для веб-приложения, которое будет развернуто в Azure (WEBAPP_NAME.azurewebsites.net). Измените значение этого параметра на уникальное имя нового веб-приложения Azure, в котором будет размещено ваше приложение Java, например *contoso*. |
| `REGION` | Регион Azure, в котором размещено веб-приложение, например `westus2`. Список регионов можно получить из Cloud Shell или CLI с помощью команды `az account list-locations`. |

Полный список параметров конфигурации см. в [справочном руководстве по подключаемому модулю Maven на сайте GitHub](https://github.com/Microsoft/azure-maven-plugins/tree/develop/azure-webapp-maven-plugin).

## <a name="deploy-the-app-to-azure"></a>Развертывание приложения в Azure

После настройки всех параметров в предыдущих разделах этой статьи можно приступать к развертыванию веб-приложения в Azure. Для этого выполните следующие действия.

1. В командной строке или в окне терминала, которые вы использовали ранее, перестройте JAR-файл, используя Maven, если вы внесли изменения в файл *pom.xml*; например:
   ```shell
   mvn clean package
   ```

1. Разверните веб-приложение в Azure с помощью Maven; например:
   ```shell
   mvn azure-webapp:deploy
   ```

Maven развернет веб-приложение в Azure. Если веб-приложение или план службы приложений отсутствуют, они будут созданы.

После развертывания веб-приложения вы сможете управлять им с помощью [портал Azure].

* Веб-приложение будет указано в разделе **Службы приложений**:

   ![Веб-приложение в разделе "Службы приложений" на портале Azure][AP01]

* URL-адрес веб-приложения будет указан в разделе **Обзор** для вашего веб-приложения:

   ![Определение URL-адреса для веб-приложения][AP02]

Убедитесь, что развертывание прошло успешно, воспользовавшись описанной выше командой cURL. При этом вместо `localhost` введите URL-адрес веб-приложения, указанный на портале. Должно появиться следующее сообщение: **Greetings from Spring Boot!** 

## <a name="next-steps"></a>Дополнительная информация

Дополнительные сведения о Spring и Azure см. в центре документации об использовании Spring в Azure.

> [!div class="nextstepaction"]
> [Spring в Azure](/java/azure/spring-framework)

### <a name="additional-resources"></a>Дополнительные ресурсы

Дополнительные сведения о различных технологиях, рассматриваемых в данной статье, см. в следующих статьях.

* [Подключаемый модуль Maven для веб-приложений Azure]

* [Развертывание приложения Spring Boot в Azure с помощью подключаемого модуля Maven для веб-приложений Azure](deploy-containerized-spring-boot-java-app-with-maven-plugin.md)

* [Создание субъекта-службы Azure с помощью Azure CLI 2.0](/cli/azure/create-an-azure-service-principal-azure-cli)

* [Справочник по параметрам Maven](https://maven.apache.org/settings.html)

<!-- URL List -->

[Azure Command-Line Interface (CLI)]: /cli/azure/overview
[Azure for Java Developers]: /java/azure/
[портал Azure]: https://portal.azure.com/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Working with Azure DevOps and Java]: /azure/devops/
[Maven]: http://maven.apache.org/
[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Boot Getting Started]: https://github.com/spring-guides/gs-spring-boot
[Spring Framework]: https://spring.io/
[Подключаемый модуль Maven для веб-приложений Azure]: /java/api/overview/azure/maven/azure-webapp-maven-plugin/readme

[Java Development Kit (JDK)]: https://aka.ms/azure-jdks
<!-- http://www.oracle.com/technetwork/java/javase/downloads/ -->

<!-- IMG List -->

[AP01]: ./media/deploy-spring-boot-java-app-with-maven-plugin/AP01.png
[AP02]: ./media/deploy-spring-boot-java-app-with-maven-plugin/AP02.png
