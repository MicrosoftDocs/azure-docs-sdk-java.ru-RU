---
title: Развертывание службы MicroProfile на основе Java в службе Azure "Веб-приложение для контейнеров"
description: Узнайте, как развернуть службу MicroProfile с помощью Docker и службы Azure "Веб-приложение для контейнеров"
services: container-registry;app-service
documentationcenter: java
author: jonathangiles
manager: routlaw
editor: jonathangiles
ms.assetid: ''
ms.author: jogiles
ms.date: 09/07/2018
ms.devlang: java
ms.service: container-registry;app-service
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: web
ms.openlocfilehash: 4ecfbf92bc30bc491c991e30111cce8375da7f1a
ms.sourcegitcommit: f8faa4a14c714e148c513fd46f119524f3897abf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/03/2019
ms.locfileid: "67533593"
---
# <a name="deploy-a-java-based-microprofile-service-to-azure-web-app-for-containers"></a>Развертывание службы MicroProfile на основе Java в службе Azure "Веб-приложение для контейнеров"

MicroProfile — отличный способ создавать компактные приложения Java, которые можно быстро и легко развернуть в различных службах, например в решении Azure [Веб-приложение для контейнеров](https://azure.microsoft.com/services/app-service/containers/). В этом учебнике мы создадим простую микрослужбу на основе MicroProfile, упакуем ее в контейнер Docker, опубликуем в [экземпляре Реестра контейнеров Azure](https://azure.microsoft.com/services/container-registry/), а затем развернем с помощью службы Azure "Веб-приложение для контейнеров".

> [!NOTE]
> Эта процедура подходит для любой реализации MicroProfile.io при условии, что образ контейнера Docker является самовыполняющимся (т. е. образ содержит среду выполнения).

В этом примере мы используем [Payara Micro](https://www.payara.fish/payara_micro) и [MicroProfile 1.3](https://microprofile.io/) для создания небольшого WAR-файла (примерно 5000 байт) веб-приложения Java, а затем упакуем этот файл в образ Docker размером примерно 174 МБ. Этот образ Docker содержит все компоненты, необходимые для полностью контейнеризированного развертывания нашего веб-приложения.

При каждом изменении исходного кода приложения не нужно повторно развертывать весь образ Docker размером 174 МБ, так как Docker отправляет только различия (которые значительно меньшего размера). Это значительно повышает скорость и эффективность развертывания новой версии приложения MicroProfile с помощью конвейера CI/CD, так как снижается сложность и ускоряется цикл разработки.

В этом учебнике мы сначала создадим и выполним программный код локально, а затем развернем его как веб-приложение в Azure. На обоих стадиях мы будем использовать Docker для упрощения и стандартизации процедуры. Прежде чем приступить к этой процедуре, вы создадите экземпляр Реестра контейнеров Azure, где будут храниться контейнеры Docker.

## <a name="create-an-azure-container-registry-instance"></a>Создание экземпляра Реестра контейнеров Azure

Вы можете создать экземпляр Реестра контейнеров Azure на [портале Azure](http://portal.azure.com), но существуют и другие варианты, например использование Azure CLI. Чтобы создать экземпляр Реестра контейнеров Azure, сделайте следующее:

1. Войдите на [портал Azure](http://portal.azure.com) и создайте ресурс Реестра контейнеров Azure. Укажите имя реестра (оно должно быть задано как свойство `docker.registry` в файле *pom.xml*). При необходимости измените значения по умолчанию, а затем нажмите кнопку **Создать**.

1. Через 30 секунд, когда экземпляр реестра контейнеров станет активным, выберите его, а затем в области слева щелкните ссылку **Ключи доступа**. 

    Включите параметр *администратор*, чтобы вы могли получать доступ к этому экземпляру реестра контейнеров со своих компьютеров и отправлять в него контейнеры Docker. Благодаря этому вы также сможете получать доступ к экземпляру решения Azure "Веб-приложение для контейнеров", который вы вскоре настроите.

1. В области **Ключи доступа** скопируйте значения **username** и **password**, а затем вставьте их в глобальный файл Maven под названием *settings.xml*. Дополнительные сведения о параметрах Maven см. на веб-сайте [Apache Maven Project](https://maven.apache.org/settings.html). 

   Для справки ниже приведен пример файла *${user.home}/.m2/settings.xml*.

    ```xml
    <settings xmlns="http://maven.apache.org/SETTINGS/1.0.0"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
      xsi:schemaLocation="http://maven.apache.org/SETTINGS/1.0.0
                          https://maven.apache.org/xsd/settings-1.0.0.xsd">
        <servers>
          <server>
            <id>jogilescr.azurecr.io</id>
            <username>jogilescr</username>
            <password>ojoirshois.this-isn't-real.hrihslirhlishrglih</password>
          </server>
        </servers>
    </settings>
    ```

Теперь, когда вы создали экземпляр реестра контейнеров, можно перейти к созданию и запуску приложения MicroProfile в локальной среде.

## <a name="create-your-microprofile-application"></a>Создание приложения MicroProfile

Этот пример кода основан на примере приложения, который доступен на сайте GitHub. Чтобы клонировать код на свой компьютер, введите следующие команды:

```
git clone https://github.com/Azure-Samples/microprofile-docker-helloworld.git

cd microprofile-docker-helloworld
```

В этом каталоге есть файл *pom.xml*, который используется для указания настроек проекта в формате инструмента сборки Maven. Вы можете изменить этот файл в соответствии со своими потребностями. В частности, свойства `docker.registry` и `docker.name` нужно изменить на `docker.registry` и `docker.name`, которые были созданы при настройке экземпляра Реестра контейнеров Azure.

В этой папке также следует обратить внимание на файл Dockerfile, который приведен ниже:

```dockerfile
FROM payara/micro

ARG WAR_FILE
COPY target/${WAR_FILE} $DEPLOY_DIR

EXPOSE 8080
```

Dockerfile создает контейнер Docker, основанный на контейнере Payara Micro Docker. Он копирует WAR-файл, который был создан как часть процесса сборки. Кроме того, с помощью файла открывается порт 8080, чтобы вы могли осуществлять доступ к службе после ее запуска в контейнере Docker.

Открыв каталог *src*, вы обнаружите в нем класс `Application`, показанный ниже:

```java
package com.microsoft.azure.samples.microprofile.docker.helloworld;

import javax.ws.rs.ApplicationPath;

@ApplicationPath("/api")
public class Application extends javax.ws.rs.core.Application { }
```

В аннотации *@ApplicationPath("/api")* указана базовая конечная точка этой микрослужбы. Таким образом, остальные URL-адреса для доступа к каждой конечной точке REST будут иметь префикс */api*.

Внутри пакета *api* находится класс с именем `API`, код которого приведен ниже:

```java
package com.microsoft.azure.samples.microprofile.docker.helloworld.api;

import javax.enterprise.context.ApplicationScoped;
import javax.ws.rs.GET;
import javax.ws.rs.Path;
import javax.ws.rs.Produces;

import static javax.ws.rs.core.MediaType.TEXT_HTML;

@ApplicationScoped
@Path("/")
public class API {

    @GET
    @Path("/helloworld")
    @Produces(TEXT_HTML)
    public String info() {
        return "Hello, world!";
    }
}
```

За счет использования аннотации *@Path("/helloworld")* путь этой конечной точки REST, образованный путем добавления префикса */api*, указанного в классе `Application`, будет равен */api/helloworld*. При вызове этой конечной точки с помощью запроса HTTP GET приведенный выше метод возвращает содержимое с типом text/html. В нашем случае это просто жестко закодированная строка "Hello, world!".

В этой статье уже подробно рассмотрен весь код, необходимый для создания микрослужбы с помощью MicroProfile. Теперь вы можете использовать Maven, чтобы собрать нашу службу, упаковать ее в контейнер Docker и запустить локально. Для этого сделайте следующее:

1. Запустите команду `mvn clean package` и дождитесь ее завершения.

1. Запустите `docker run -it --rm -p 8080:8080 <docker.registry>/<docker.name>:latest`. Например, *docker run -it --rm -p 8080:8080 jogilescr.azurecr.io/samples/docker-helloworld:latest*, где *\<docker.registry>* соответствует *jogilescr.azurecr.io*, а *\<docker.name>*  — *samples/docker-helloworld*.

1. Попробуйте открыть адреса [http://localhost:8080/microprofile/api/helloworld](http://localhost:8080/microprofile/api/helloworld) и [http://localhost:8080/health](http://localhost:8080/health) в веб-браузере. Если вы видите ожидаемый ответ "Hello, world!" (и сведения о состоянии из конечной точки [/health](http://localhost:8080/health)), значит вы успешно развернули приложение MicroProfile на своем локальном компьютере.

## <a name="push-the-container-to-the-azure-container-registry-instance"></a>Передача контейнера в экземпляр Реестра контейнеров Azure.

После успешной сборки и запуска приложения MicroProfile на локальном компьютере отправьте этот контейнер в созданный ранее экземпляр реестра контейнеров. 

> [!NOTE]
> Несмотря на то что в этой статье используется экземпляр Реестра контейнеров Azure, любой экземпляр реестра контейнеров подойдет. Нужно лишь указать в файле *pom.xml* путь к соответствующему расположению.

1. Чтобы очистить, скомпилировать и создать локальный образ Docker, выполните команду `mvn clean package`.
2. Чтобы отправить контейнер в экземпляр Реестра контейнеров Azure, выполните команду `mvn dockerfile:push`.

Теперь ваш образ контейнера Docker передан в экземпляр Реестра контейнеров Azure. Однако этот образ еще не запущен. Теперь нужно развернуть его в экземпляре решения Azure "Веб-приложение для контейнеров". 

## <a name="create-an-azure-web-app-for-containers-instance"></a>Создание экземпляра решения Azure "Веб-приложение для контейнеров"

1. На [портале Azure](http://portal.azure.com) в левой области выберите **Интернет и мобильные устройства**, а затем сделайте следующее:

   a. Задайте имя. Оно станет общедоступным URL-адресом веб-приложения, поэтому рекомендуется выбрать имя, которое легко запомнить. Позже вы можете добавить имя личного домена.

   b. В разделе **Настроить контейнер** в качестве **источника образа** выберите **Реестр контейнеров Azure**, а затем выберите нужный образ в раскрывающемся списке.

   c. Поле **Загрузочный файл** нужно оставить пустым.

1. После создания экземпляра выберите его и щелкните **Параметры приложения**. Для параметра **Ключ** введите **WEBSITES_PORT**, а для параметра **Значение** — **8080**. Из этих параметров Azure узнает, какой порт нужно открыть в контейнере и с каким внешним портом его нужно сопоставить (80).

1. (Необязательно.) Выберите ссылку **Контейнер Docker**, а затем включите параметр **Непрерывное развертывание**. Таким образом, при каждом обновлении образа экземпляра Реестра контейнеров Azure он будет автоматически обновляться в экземпляре решения Azure "Веб-приложение для контейнеров".

1. Теперь экземпляры веб-приложений, развернутых в Azure, должны быть доступны по адресам `http://<appname>.azurewebsites.net/microprofile/api/helloworld` и `http://<appname>.azurewebsites.net/health`.

## <a name="summary"></a>Сводка

Работая с этим учебником, вы выполнили пошаговый процесс создания простой микрослужбы MicroProfile, которую вы упаковали в контейнер Docker, запустили локально и опубликовали в Azure. Вы можете расширить микрослужбу, добавив в нее дополнительные полезные функции. Дополнительные сведения см. на сайте [MicroProfile.io](https://microprofile.io/).
