---
title: "Развертывание приложения Spring Boot Application в службе приложений Azure"
description: "В этом учебнике приводятся пошаговые инструкции для разработчиков по развертыванию веб-приложения Spring Boot Getting Started в службе приложений Azure."
services: app-service
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
keywords: Spring, Spring Boot, Spring Framework
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: java
ms.topic: article
ms.date: 11/01/2017
ms.author: asirveda;robmcm
ms.openlocfilehash: 7a4234aefd4eb33f80c1978fb84721f2dbcb2e4f
ms.sourcegitcommit: 613c1ffd2e0279fc7a96fca98aa1809563f52ee1
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/18/2017
---
# <a name="deploy-a-spring-boot-application-to-the-azure-app-service"></a>Развертывание приложения Spring Boot Application в службе приложений Azure

**[Spring Framework]** — это решение с открытым исходным кодом, которое помогает разработчикам Java создавать приложения корпоративного класса. Одним из самых популярных проектов, созданных на этой платформе, является [Spring Boot]. Он упрощает подход к созданию автономных приложений Java.

В этом учебнике приводятся пошаговые инструкции по созданию образца веб-приложения Spring Boot Getting Started и его развертыванию в [службе приложений Azure].

### <a name="prerequisites"></a>Предварительные требования

Для работы с этим учебником требуется следующее.

* Подписка Azure; если у вас еще нет подписки Azure, вы можете активировать [преимущества для подписчиков MSDN] или зарегистрироваться для получения [бесплатной учетной записи Azure].
* Актуальная версия [Java Developer Kit (JDK)].
* Средство сборки [Maven] (версия 3) от Apache.
* Клиент [Git].

## <a name="create-the-spring-boot-getting-started-web-app"></a>Создание веб-приложения Spring Boot Getting Started

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

1. Клонируйте образец проекта [Spring Boot Getting Started] в созданный каталог, например:
   ```
   git clone https://github.com/spring-guides/gs-spring-boot.git
   ```

1. Перейдите в каталог готового проекта, например:
   ```
   cd gs-spring-boot
   cd complete
   ```

1. Выполните сборку файла JAR с помощью Maven, например:
   ```
   mvn package
   ```

1. После создания веб-приложения перейдите к JAR-файлу и запустите веб-приложение, например:
   ```
   cd target
   java -jar gs-spring-boot-0.1.0.jar
   ```

1. Протестируйте веб-приложение, перейдя по адресу http://localhost:8080 в веб-браузере, или, если имеется программа curl, используйте синтаксис, как в следующем примере:
   ```
   curl http://localhost:8080
   ```

1. Должно появиться следующее сообщение: **Greetings from Spring Boot!**

   ![Обзор образца приложения][SB01]

## <a name="create-an-azure-web-app-for-use-with-java"></a>Создание веб-приложения Azure для использования с Java

Ниже приведены пошаговые инструкции по созданию веб-приложения Azure, настройке необходимых параметров для Java и настройке учетных данных FTP.

1. Перейдите на [портал Azure] и выполните вход.

1. Войдя в учетную запись на портале Azure, щелкните значок меню **Службы приложений**:
   
   ![Портал Azure][AZ01]

1. Когда откроется страница **Службы приложений**, щелкните **+ Добавить**, чтобы создать службу приложений.

   ![Создание службы приложений][AZ02]

1. Когда появится список шаблонов веб-приложений, щелкните ссылку базового веб-приложения Майкрософт.

   ![Шаблоны веб-приложений][AZ03]

1. Когда появится страница шаблона веб-приложения, нажмите кнопку **Создать**.

   ![Создание веб-приложения][AZ04]

1. Укажите уникальное имя веб-приложения и задайте дополнительные параметры, после чего нажмите кнопку **Создать**.

   ![Параметры создания веб-приложения][AZ05]

1. После создания веб-приложения щелкните значок меню **Службы приложений**, а затем выберите только что созданное веб-приложение.

   ![Список веб-приложений][AZ06]

1. Когда веб-приложение отобразится, укажите версию Java, выполнив указанные ниже действия.

   а. Выберите пункт меню **Параметры приложения**.

   b. В качестве версии Java выберите **Java 8**.

   c. В качестве дополнительного номера версии Java выберите **Самые новые**.

   г) В качестве веб-контейнера выберите **Последняя версия Tomcat 8.5**. (Этот контейнер в действительности не будет использоваться; Azure будет использовать контейнер в приложении Spring Boot.)

   д. Щелкните **Сохранить**.

   ![Параметры приложения][AZ07]

1. Укажите учетные данные FTP, выполнив указанные ниже действия.

   а. Выберите пункт меню **Учетные данные развертывания**.

   b. Укажите имя пользователя и пароль.

   c. Щелкните **Сохранить**.

   ![Указание учетных данных развертывания][AZ08]

1. Получите сведения о подключении по FTP, выполнив указанные ниже действия.

   а. Выберите пункт меню **Учетные данные развертывания**.

   b. Скопируйте полное имя пользователя и URL-адрес FTP, а затем сохраните их. Они понадобятся в следующем разделе этого учебника.

   ![URL-адрес и учетные данные FTP][AZ09]

## <a name="deploy-your-spring-boot-web-app-to-azure"></a>Развертывание веб-приложения Spring Boot в Azure

Ниже приведены пошаговые инструкции по развертыванию веб-приложения Spring Boot в Azure.

1. Откройте текстовый редактор, например Блокнот, и вставьте следующий текст в новый документ, а затем сохраните файл с именем *web.config*:
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

1. После сохранения файла *web.config* в системе подключитесь к веб-приложению по FTP, используя URL-адрес, имя пользователя и пароль из предыдущего раздела этого учебника. Например:
   ```
   ftp
   open waws-prod-sn0-000.ftp.azurewebsites.windows.net
   user wingtiptoys-springboot\wingtiptoysuser
   pass ********
   ```

1. Измените удаленный каталог на корневую папку веб-приложения (находящуюся по адресу */site/wwwroot*), а затем скопируйте JAR-файл приложения Spring Boot и файл *web.config*, созданный ранее. Например:
   ```
   cd site/wwwroot
   put gs-spring-boot-0.1.0.jar
   put web.config
   ```

1. После развертывания файлов JAR и *web.config* в веб-приложении необходимо перезапустить его с помощью портала Azure:

   ![][AZ10]

1. Протестируйте веб-приложение, перейдя по его URL-адресу в веб-браузере, или, если имеется программа curl, используйте синтаксис, как в следующем примере:
   ```
   curl http://wingtiptoys-springboot.azurewebsites.net/
   ```

1. Должно появиться следующее сообщение: **Greetings from Spring Boot!**

   ![Обзор образца приложения][SB02]

## <a name="next-steps"></a>Дальнейшие действия

Дополнительные сведения об использовании приложений Spring Boot в Azure см. в следующих статьях:

* [Развертывание приложения Spring Boot в Linux в службе контейнеров Azure](deploy-spring-boot-java-app-on-linux.md)

* [Развертывание приложения Spring Boot в кластере Kubernetes в службе контейнеров Azure](deploy-spring-boot-java-app-on-kubernetes.md)

Дополнительные сведения об использовании Azure см. в [центре разработчиков Java для Azure] и на странице [инструментов Java для Visual Studio Team Services].

Дополнительные сведения о развертывании веб-приложений в Azure по FTP см. в статье [Развертывание приложения в службе приложений Azure с помощью FTP или FTPS].

Дополнительные сведения об образце проекта Spring Boot см. на странице [Spring Boot Getting Started].

Справку по началу работы с собственными приложениями Spring Boot см. на странице **Spring Initializr** по адресу https://start.spring.io/.

Дополнительные сведения о настройке дополнительных параметров для веб-приложения см. в статье [Настройка веб-приложений в службе приложений Azure].

<!-- URL List -->

[службе приложений Azure]: https://azure.microsoft.com/services/app-service/
[Azure Container Service]: https://azure.microsoft.com/services/container-service/
[центре разработчиков Java для Azure]: https://azure.microsoft.com/develop/java/
[портал Azure]: https://portal.azure.com/
[Настройка веб-приложений в службе приложений Azure]: /azure/app-service/web-sites-configure
[Развертывание приложения в службе приложений Azure с помощью FTP или FTPS]: https://docs.microsoft.com/azure/app-service/app-service-deploy-ftp
[бесплатной учетной записи Azure]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[инструментов Java для Visual Studio Team Services]: https://java.visualstudio.com/ (Инструменты Java для Visual Studio Team Services)
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
