---
title: Развертывание веб-приложения Spring Boot в Linux в Службе контейнеров Azure
description: В этом руководстве содержатся пошаговые инструкции по развертыванию приложения Spring Boot в качестве веб-приложения Linux в Microsoft Azure.
services: container-service
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: ''
ms.assetid: ''
ms.author: asirveda;robmcm
ms.date: 02/01/2018
ms.devlang: java
ms.service: container-service
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: web
ms.custom: mvc
ms.openlocfilehash: 49d94d11ad6a4e103ded849e477d99f01955c693
ms.sourcegitcommit: 5282a51bf31771671df01af5814df1d2b8e4620c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/28/2018
ms.locfileid: "37090867"
---
# <a name="deploy-a-spring-boot-application-on-linux-in-the-azure-container-service"></a>Развертывание приложения Spring Boot в Linux в службе контейнеров Azure

В этом руководстве описано, как использовать [Docker] для разработки и развертывания приложения [Spring Boot] на узле Linux в [Служба контейнеров Azure].

## <a name="prerequisites"></a>предварительным требованиям

Для работы с этим руководством требуется следующее.

* Подписка Azure. Если у вас ее еще нет, вы можете активировать [Преимущества для подписчиков MSDN] или зарегистрироваться для получения [бесплатной учетной записи Azure].
* [Интерфейс командной строки Azure (CLI)].
* Актуальная версия [Java Developer Kit (JDK)].
* Средство сборки [Maven] (версия 3) от Apache.
* Клиент [Git].
* Клиент [Docker].

> [!NOTE]
>
> С учетом требований виртуализации для этого руководства изложенные здесь инструкции нельзя выполнять на виртуальной машине. Необходимо использовать физический компьютер с включенными функциями виртуализации.
>

## <a name="create-the-spring-boot-on-docker-getting-started-web-app"></a>Создание веб-приложения Spring Boot в Docker

Ниже приводятся пошаговые инструкции по созданию простого веб-приложения Spring Boot и его локальному тестированию.

1. Откройте командную строку и создайте локальный каталог для размещения приложения, после чего перейдите в этот каталог, например:
   ```
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   -- или --
   ```
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. Клонируйте образец проекта [Spring Boot on Docker Getting Started] (Запуск Spring Boot в Docker) в созданный каталог, например:
   ```
   git clone https://github.com/spring-guides/gs-spring-boot-docker.git
   ```

1. Перейдите в каталог готового проекта, например:
   ```
   cd gs-spring-boot-docker/complete
   ```

1. Выполните сборку файла JAR с помощью Maven, например:
   ```
   mvn package
   ```

1. После создания веб-приложения перейдите в каталог `target`, где находится JAR-файл, и запустите веб-приложение, например:
   ```
   cd target
   java -jar gs-spring-boot-docker-0.1.0.jar
   ```

1. Проверьте веб-приложение, перейдя к нему локально с помощью веб-браузера. Например, если у вас установлен CuRL и сервер Tomcat настроен для работы с использованием порта 80:
   ```
   curl http://localhost
   ```

1. Должно появиться следующее сообщение: **Hello Docker World!**

   ![Локальный просмотр образца приложения][SB01]

## <a name="create-an-azure-container-registry-to-use-as-a-private-docker-registry"></a>Создание реестра контейнеров Azure для использования в качестве частного реестра Docker

Ниже рассмотрена процедура использования портала Azure для создания реестра контейнеров Azure.

> [!NOTE]
>
> Если вы хотите использовать Azure CLI, а не портал Azure, выполните процедуру, описанную в разделе [Создание частного реестра контейнеров Docker с помощью Azure CLI 2.0](/azure/container-registry/container-registry-get-started-azure-cli).
>

1. Перейдите на [портал Azure] и выполните вход.

   После входа в свою учетную запись на портале Azure можно выполнить процедуру, описанную в статье [Создание частного реестра контейнеров Docker с помощью портала Azure], которую здесь полезно представить еще раз.

1. Щелкните значок меню **+ Создать**, нажмите кнопку **Контейнеры**, а затем нажмите кнопку **Реестр контейнеров Azure**.
   
   ![Создание нового реестра контейнеров Azure][AR01]

1. При появлении страницы сведений о шаблоне реестра контейнеров Azure нажмите кнопку **Создать**. 

   ![Создание нового реестра контейнеров Azure][AR02]

1. При появлении страницы **Создать реестр контейнеров** введите данные в поля **Имя реестра** и **Группа ресурсов**, выберите **Включить** для параметра **Пользователь-администратор** и нажмите кнопку **Создать**.

   ![Настройка параметров реестра контейнеров Azure][AR03]

1. После создания реестра контейнеров перейдите в реестр контейнеров на портале Azure и нажмите кнопку **Ключи доступа**. Запишите имя пользователя и пароль для последующих шагов.

   ![Ключи доступа к реестру контейнеров Azure][AR04]

## <a name="configure-maven-to-use-your-azure-container-registry-access-keys"></a>Настройка Maven для использования ключей доступа к реестру контейнеров Azure

1. Перейдите в каталог конфигурации для установки Maven и откройте файл *settings.xml* в текстовом редакторе.

1. Добавьте параметры доступа к реестру контейнеров Azure из предыдущего раздела этого учебника в коллекцию `<servers>` в файле *settings.xml*, например:

   ```xml
   <servers>
      <server>
         <id>wingtiptoysregistry</id>
         <username>wingtiptoysregistry</username>
         <password>AbCdEfGhIjKlMnOpQrStUvWxYz</password>
      </server>
   </servers>
   ```

1. Перейдите в каталог завершенного проекта для приложения Spring Boot (например, *C:\SpringBoot\gs-spring-boot-docker\complete* или */users/robert/SpringBoot/gs-spring-boot-docker/complete*) и откройте файл *pom.xml* в текстовом редакторе.

1. Обновите коллекцию `<properties>` в файле *pom.xml*, добавив значение сервера входа для реестра контейнеров Azure из предыдущего раздела данного учебника, например:

   ```xml
   <properties>
      <docker.image.prefix>wingtiptoysregistry.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
   </properties>
   ```

1. Обновите коллекцию `<plugins>` в файле *pom.xml* таким образом, чтобы в `<plugin>` содержались адрес сервера входа и имя для реестра контейнеров Azure из предыдущего раздела данного учебника. Например: 

   ```xml
   <plugin>
      <groupId>com.spotify</groupId>
      <artifactId>docker-maven-plugin</artifactId>
      <version>0.4.11</version>
      <configuration>
         <imageName>${docker.image.prefix}/${project.artifactId}</imageName>
         <dockerDirectory>src/main/docker</dockerDirectory>
         <resources>
            <resource>
               <targetPath>/</targetPath>
               <directory>${project.build.directory}</directory>
               <include>${project.build.finalName}.jar</include>
            </resource>
         </resources>
         <serverId>wingtiptoysregistry</serverId>
         <registryUrl>https://wingtiptoysregistry.azurecr.io</registryUrl>
      </configuration>
   </plugin>
   ```

1. Перейдите в каталог завершенного проекта для приложения Spring Boot и выполните команду ниже для перестроения приложения и отправки контейнера в реестр контейнеров Azure:

   ```
   mvn package docker:build -DpushImage 
   ```

> [!NOTE]
>
> При отправке контейнера Docker в Azure может появиться сообщение об ошибке, похожее на одно из показанных ниже, даже если контейнер Docker был успешно создан:
>
> * `[ERROR] Failed to execute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: no basic auth credentials`
>
> * `[ERROR] Failed to execute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: Incomplete Docker registry authorization credentials. Please provide all of username, password, and email or none.`
>
> В этом случае, возможно, потребуется войти в учетную запись Azure из командной строки Docker, например, выполнив следующую команду.
>
> `docker login -u wingtiptoysregistry -p "AbCdEfGhIjKlMnOpQrStUvWxYz" wingtiptoysregistry.azurecr.io`
>
> Затем контейнер можно передать из командной строки, например:
>
> `docker push wingtiptoysregistry.azurecr.io/gs-spring-boot-docker`
>

## <a name="create-a-web-app-on-linux-on-azure-app-service-using-your-container-image"></a>Создание веб-приложения в Linux в службе приложений Azure с помощью образа контейнера

1. Перейдите на [портал Azure] и выполните вход.

2. Щелкните значок меню **+ Создать**, нажмите кнопку **Интернет + мобильные устройства**, а затем нажмите кнопку **веб-приложения на платформе Linux**.
   
   ![Создание веб-приложения на портале Azure][LX01]

3. Когда отобразится страница **Веб-приложение в Linux**, введите следующие сведения.

   a. Введите уникальное имя в поле **Имя приложения**, например "*wingtiptoyslinux*."

   Б. В раскрывающемся списке выберите свою **подписку**.

   c. Выберите существующую **группу ресурсов** или укажите имя, чтобы создать новую группу ресурсов.

   d. Нажмите кнопку **Настройка контейнера** и введите следующие сведения.

   * Выберите **Частный реестр**.

   * **Образ и дополнительный тег**: задайте имя контейнера из более ранней версии, например "*wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest*"

   * **URL-адрес сервера**: укажите URL-адрес реестра из более ранней версии, например *<https://wingtiptoysregistry.azurecr.io>*.

   * **Имя входа пользователя** и **Пароль**: укажите учетные данные для входа из своих **ключей доступа**, которые использовались на предыдущих шагах.
   
   д. После ввода всех этих данных нажмите кнопку **ОК**.

   ![Настройка параметров веб-приложения][LX02]

4. Нажмите кнопку **Создать**.

> [!NOTE]
>
> Azure будет автоматически сопоставлять интернет-запросы со встроенным сервером Tomcat, который использует стандартный порт 80 или 8080. Однако, если вы настроили свой встроенный сервер Tomcat так, чтобы он работал с пользовательским портом, в веб-приложение необходимо добавить переменную среды, которая определяет порт для вашего встроенного сервера Tomcat. Для этого выполните следующие действия.
>
> 1. Перейдите на [портал Azure] и выполните вход.
> 
> 2. Щелкните значок для **служб приложений**. (См. элемент ном. 1 на рисунке ниже.)
>
> 3. Выберите веб-приложение в списке. (Элемент ном. 2 на рисунке ниже.)
>
> 4. Щелкните **Параметры приложения**. (Элемент ном. 3 на рисунке ниже.)
>
> 5. В разделе **Параметры приложения** добавьте новую переменную среды с именем **PORT** и введите номер пользовательского порта в качестве значения. (Элемент ном. 4 на рисунке ниже.)
>
> 6. Выберите команду **Сохранить**. (Элемент ном. 5 на рисунке ниже.)
>
> ![Сохранение номера пользовательского порта на портале Azure][LX03]
>

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

Дополнительные сведения об использовании приложений Spring Boot в Azure см. в следующих статьях:

* [Развертывание приложения Spring Boot Application в службе приложений Azure](deploy-spring-boot-java-web-app-on-azure.md)
* [Развертывание приложения Spring Boot в кластере Kubernetes в службе контейнеров Azure](deploy-spring-boot-java-app-on-kubernetes.md)

Дополнительные сведения об использовании Azure с Java см. в руководствах по [Azure для разработчиков Java] и [Java Tools for Visual Studio Team Services].

Дополнительные сведения о Spring Boot в образце проекта Docker см. в разделе [Spring Boot on Docker Getting Started] (Начало работы с Spring Boot в Docker).

Справку по началу работы с собственными приложениями Spring Boot см. на странице **Spring Initializr**: https://start.spring.io/.

Дополнительные сведения о создании простого приложения Spring Boot см. на странице Spring Initializr: https://start.spring.io/.

Дополнительные примеры использования пользовательских образов Docker в Azure см. в разделе [Применение пользовательского образа Docker для веб-приложения Azure на платформе Linux].

<!-- URL List -->

[Интерфейс командной строки Azure (CLI)]: /cli/azure/overview
[Служба контейнеров Azure]: https://azure.microsoft.com/services/container-service/
[Azure для разработчиков Java]: https://docs.microsoft.com/java/azure/
[портал Azure]: https://portal.azure.com/
[Создание частного реестра контейнеров Docker с помощью портала Azure]: /azure/container-registry/container-registry-get-started-portal
[Применение пользовательского образа Docker для веб-приложения Azure на платформе Linux]: /azure/app-service-web/app-service-linux-using-custom-docker-image
[Docker]: https://www.docker.com/
[бесплатной учетной записи Azure]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/ (Инструменты Java для Visual Studio Team Services)
[Maven]: http://maven.apache.org/
[Преимущества для подписчиков MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Boot on Docker Getting Started]: https://github.com/spring-guides/gs-spring-boot-docker
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[SB01]: ./media/deploy-spring-boot-java-app-on-linux/SB01.png
[SB02]: ./media/deploy-spring-boot-java-app-on-linux/SB02.png

[AR01]: ./media/deploy-spring-boot-java-app-on-linux/AR01.png
[AR02]: ./media/deploy-spring-boot-java-app-on-linux/AR02.png
[AR03]: ./media/deploy-spring-boot-java-app-on-linux/AR03.png
[AR04]: ./media/deploy-spring-boot-java-app-on-linux/AR04.png

[LX01]: ./media/deploy-spring-boot-java-app-on-linux/LX01.png
[LX02]: ./media/deploy-spring-boot-java-app-on-linux/LX02.png
[LX03]: ./media/deploy-spring-boot-java-app-on-linux/LX03.png
