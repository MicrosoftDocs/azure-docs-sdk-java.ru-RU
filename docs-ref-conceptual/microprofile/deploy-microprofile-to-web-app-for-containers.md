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
ms.openlocfilehash: 323ae247c3df8c7d7b180d9d60b9014e4e2d7382
ms.sourcegitcommit: 77dc6c03a2e6264df688d91a04fc6b40950779ef
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2018
ms.locfileid: "43240964"
---
# <a name="deploy-a-java-based-microprofile-service-to-azure-web-app-for-containers"></a><span data-ttu-id="960d4-103">Развертывание службы MicroProfile на основе Java в службе Azure "Веб-приложение для контейнеров"</span><span class="sxs-lookup"><span data-stu-id="960d4-103">Deploy a Java-based MicroProfile service to Azure Web App for Containers</span></span>

<span data-ttu-id="960d4-104">MicroProfile — отличный способ создавать очень компактные приложения Java, которые можно быстро и легко развернуть в различных службах, например в решении Azure [Веб-приложение для контейнеров](https://azure.microsoft.com/services/app-service/containers/).</span><span class="sxs-lookup"><span data-stu-id="960d4-104">MicroProfile is a great way to build exceedingly tiny Java applications that can be quickly and easily deployed to services such as [Azure Web App for Containers](https://azure.microsoft.com/services/app-service/containers/).</span></span> <span data-ttu-id="960d4-105">В этом руководстве мы создадим простую микрослужбу на основе MicroProfile, упакуем ее в контейнер Docker, опубликуем в [Реестре контейнеров Azure](https://azure.microsoft.com/services/container-registry/), а затем развернем с помощью службы Azure "Веб-приложение для контейнеров".</span><span class="sxs-lookup"><span data-stu-id="960d4-105">In this tutorial we will create a simple MicroProfile-based microservice that is then containerized into a Docker container, deployed into an [Azure Container Registry](https://azure.microsoft.com/services/container-registry/), and then hosted using Azure Web App for Containers.</span></span>

> [!NOTE]
>
> <span data-ttu-id="960d4-106">Эта процедура подходит для любой реализации MicroProfile.io при условии, что образ контейнера Docker является самовыполняющимся (т. е. включает среду выполнения).</span><span class="sxs-lookup"><span data-stu-id="960d4-106">This procedure works with any implementation of MicroProfile.io as long the Docker container image is self-executable (i.e. includes the runtime).</span></span>

<span data-ttu-id="960d4-107">Говоря конкретнее, в этом примере мы используем [Payara Micro](https://www.payara.fish/payara_micro) и [MicroProfile 1.3](https://microprofile.io/) для создания компактного файла Java WAR (5085 байт на компьютере авторов), а затем упакуем его в образ Docker (примерно 174 МБ).</span><span class="sxs-lookup"><span data-stu-id="960d4-107">More concretely, this sample makes use of [Payara Micro](https://www.payara.fish/payara_micro) and [MicroProfile 1.3](https://microprofile.io/) to create a tiny Java war file (5,085 bytes on the authors machine), and then packages it up into a Docker image (which is approximately 174 megabytes).</span></span> <span data-ttu-id="960d4-108">Этот образ Docker содержит все компоненты, необходимые для полностью контейнеризированного развертывания нашего веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="960d4-108">This Docker image contains everything necessary for a fully-containerised deployment of this webapp.</span></span>

<span data-ttu-id="960d4-109">В большинстве случаев принцип работы Docker позволяет не развертывать полный образ Docker размером 174 МБ при каждом изменении исходного кода приложения, так как Docker будет отправлять только различия (которые значительно меньше).</span><span class="sxs-lookup"><span data-stu-id="960d4-109">Because of the way Docker works, it is often the case that the entire 174 megabyte Docker image does not need to be redeployed whenever the application source code is changed, as Docker will only upload the differences (which is significantly smaller).</span></span> <span data-ttu-id="960d4-110">Это значительно повышает скорость и эффективность развертывания новой версии приложения MicroProfile с помощью конвейера CI/CD, так как снижается сложность и ускоряется цикл разработки.</span><span class="sxs-lookup"><span data-stu-id="960d4-110">This makes the process of executing a new release of a MicroProfile application via a CI/CD pipeline extremely efficient and quick, reducing friction and enabling rapid development iteration.</span></span>

<span data-ttu-id="960d4-111">В этом руководстве мы сначала создадим и выполним программный код локально, а затем развернем его как веб-приложение в Azure.</span><span class="sxs-lookup"><span data-stu-id="960d4-111">We will work through this tutorial firstly by creating and running the code locally, and then we will deploy this as a web app on Azure.</span></span> <span data-ttu-id="960d4-112">В обоих случаях мы будем использовать Docker для упрощения и стандартизации процедуры.</span><span class="sxs-lookup"><span data-stu-id="960d4-112">In both cases we will depend on Docker to simplify and standardize our efforts.</span></span> <span data-ttu-id="960d4-113">Прежде чем начать, мы создадим Реестр контейнеров Azure для хранения контейнеров Docker.</span><span class="sxs-lookup"><span data-stu-id="960d4-113">Before we begin, we will create an Azure Container Registry to store our Docker containers in.</span></span>

## <a name="creating-an-azure-container-registry"></a><span data-ttu-id="960d4-114">Создание Реестра контейнеров Azure</span><span class="sxs-lookup"><span data-stu-id="960d4-114">Creating an Azure Container Registry</span></span>

<span data-ttu-id="960d4-115">Для создания Реестра контейнеров Azure мы будем использовать [портал Azure](http://portal.azure.com), но есть и другие способы, например, можно применить Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="960d4-115">We will use the [Azure Portal](http://portal.azure.com) for creating the Azure Container Registry, but note that there are alternate choices such as the Azure CLI.</span></span> <span data-ttu-id="960d4-116">Чтобы создать Реестр контейнеров Azure, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="960d4-116">Follow the steps below to create a new Azure Container Registry:</span></span>

1. <span data-ttu-id="960d4-117">Войдите на [портал Azure](http://portal.azure.com) и создайте новый ресурс Реестра контейнеров Azure.</span><span class="sxs-lookup"><span data-stu-id="960d4-117">Log in to the [Azure Portal](http://portal.azure.com) and create a new Azure Container Registry resource.</span></span> <span data-ttu-id="960d4-118">Укажите имя реестра (обратите внимание, что оно должно быть задано как свойство `docker.registry` в файле `pom.xml`).</span><span class="sxs-lookup"><span data-stu-id="960d4-118">Provide a registry name (note that this is the name that should be set as the `docker.registry` property in `pom.xml`).</span></span> <span data-ttu-id="960d4-119">При необходимости измените значения по умолчанию и нажмите кнопку "Создать".</span><span class="sxs-lookup"><span data-stu-id="960d4-119">Change the defaults as you wish, and then click 'create'.</span></span>

1. <span data-ttu-id="960d4-120">Как только реестр контейнеров будет создан (это занимает около 30 секунд после нажатия кнопки "Создать"), выберите его и щелкните ссылку "Ключи доступа" в области меню слева.</span><span class="sxs-lookup"><span data-stu-id="960d4-120">Once the container registry is live (which is about 30 seconds after clicking 'create'), click on the container registry, and click on the 'Access keys' link in the left-menu area.</span></span> <span data-ttu-id="960d4-121">Здесь необходимо включить параметр "администратор", чтобы осуществлять доступ к этому реестру контейнеров с наших компьютеров (для отправки в него контейнеров Docker), а также разрешить доступ из экземпляра службы Azure "Веб-приложение для контейнеров", который мы скоро настроим.</span><span class="sxs-lookup"><span data-stu-id="960d4-121">In here, you need to enable the 'admin user' setting, so that this container registry can be accessed from our machines (to push docker containers into), and also to enable access from the Azure Web Apps for Containers instance we will setup soon.</span></span>

1. <span data-ttu-id="960d4-122">В разделе "Ключи доступа" обратите внимание на значения `username` и `password`.</span><span class="sxs-lookup"><span data-stu-id="960d4-122">Whilst you are in the 'Access keys' area, note the `username` and `password` values.</span></span> <span data-ttu-id="960d4-123">Мы скопируем их и вставим в глобальный файл Maven `settings.xml` (дополнительные сведения о параметрах Maven см. на веб-сайтe [Apache Maven Project](https://maven.apache.org/settings.html)).</span><span class="sxs-lookup"><span data-stu-id="960d4-123">We will copy / paste these into our global Maven `settings.xml` file  (for more information on Maven settings, refer to the [Apache Maven Project](https://maven.apache.org/settings.html) website).</span></span> <span data-ttu-id="960d4-124">Для справки ниже приведена версия файла `${user.home}/.m2/settings.xml` с маскированием в системе авторов:</span><span class="sxs-lookup"><span data-stu-id="960d4-124">For reference, here is an obfuscated version of the `${user.home}/.m2/settings.xml` file on the authors system:</span></span>

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

<span data-ttu-id="960d4-125">После завершения этой процедуры можно перейти к сборке и запуску приложения MicroProfile локально.</span><span class="sxs-lookup"><span data-stu-id="960d4-125">Now that this is complete, we can move on with building and running our MicroProfile application locally.</span></span>

## <a name="creating-our-microprofile-application"></a><span data-ttu-id="960d4-126">Создание приложения MicroProfile</span><span class="sxs-lookup"><span data-stu-id="960d4-126">Creating our MicroProfile application</span></span>

<span data-ttu-id="960d4-127">Наш пример построен на основе демонстрационного приложения, доступного на сайте GitHub, поэтому мы клонируем это приложение и пошагово проанализируем его код.</span><span class="sxs-lookup"><span data-stu-id="960d4-127">This example is based on a sample application available on GitHub, so we will clone that and then step through the code.</span></span> <span data-ttu-id="960d4-128">Чтобы клонировать код на свой компьютер, выполните следующие инструкции:</span><span class="sxs-lookup"><span data-stu-id="960d4-128">Follow the steps below to get the code cloned onto your machine:</span></span>

1. `git clone https://github.com/Azure-Samples/microprofile-docker-helloworld.git`
1. `cd microprofile-docker-helloworld`

<span data-ttu-id="960d4-129">В этой папке есть файл `pom.xml`, который используется для указания настроек проекта в формате инструмента сборки Maven.</span><span class="sxs-lookup"><span data-stu-id="960d4-129">In this directory there is a `pom.xml` file that is used to specify the project in the format used by the Maven build tool.</span></span> <span data-ttu-id="960d4-130">Этот файл можно изменить в соответствии с потребностями.</span><span class="sxs-lookup"><span data-stu-id="960d4-130">This file can be edited to suit your own needs.</span></span> <span data-ttu-id="960d4-131">В частности, значения свойств `docker.registry` и `docker.name` нужно изменить на `docker.registry` и `docker.name`, которые были созданы при настройке Реестра контейнеров Azure.</span><span class="sxs-lookup"><span data-stu-id="960d4-131">In particular, the `docker.registry` and `docker.name` properties should be changed to the `docker.registry` and `docker.name` created when the Azure Container Registry was setup.</span></span>

<span data-ttu-id="960d4-132">В этой папке также следует обратить внимание на файл Dockerfile, который приведен ниже:</span><span class="sxs-lookup"><span data-stu-id="960d4-132">Another file of note in this directory is the Dockerfile, which is reproduced below:</span></span>

```dockerfile
FROM payara/micro

ARG WAR_FILE
COPY target/${WAR_FILE} $DEPLOY_DIR

EXPOSE 8080
```

<span data-ttu-id="960d4-133">С помощью этого файла Dockerfile просто создается новый контейнер Docker на основе контейнера Payara Micro и в новый контейнер копируется файл WAR, созданный в процессе сборки.</span><span class="sxs-lookup"><span data-stu-id="960d4-133">This Dockerfile simply creates a new Docker container based on the Payara Micro Docker Container, and copies in the .war file that is created as part of our build process.</span></span> <span data-ttu-id="960d4-134">Кроме того, с помощью файла открывается порт 8080, чтобы мы могли осуществлять доступ к нашей службе после ее запуска в контейнере Docker.</span><span class="sxs-lookup"><span data-stu-id="960d4-134">It also exposes port 8080 so that we may access the service once it is up and running within a Docker container.</span></span>

<span data-ttu-id="960d4-135">Просматривая папку `src`, мы обнаружим в ней класс `Application`, показанный ниже:</span><span class="sxs-lookup"><span data-stu-id="960d4-135">Diving into the `src` directory, we will eventually discover the `Application` class reproduced below:</span></span>

```java
package com.microsoft.azure.samples.microprofile.docker.helloworld;

import javax.ws.rs.ApplicationPath;

@ApplicationPath("/api")
public class Application extends javax.ws.rs.core.Application { }
```

<span data-ttu-id="960d4-136">В аннотации `@ApplicationPath("/api")` указана базовая конечная точка этой микрослужбы, т. е. URL-адреса для доступа к каждой конечной точке REST будут иметь префикс `/api`.</span><span class="sxs-lookup"><span data-stu-id="960d4-136">The `@ApplicationPath("/api")` annotation specifies the base endpoint for this microservice - that is, that all endpoints will have `/api` preceed the rest of the URL required to access any specific REST endpoint.</span></span>

<span data-ttu-id="960d4-137">Внутри пакета `api` находится класс с именем `API`, код которого приведен ниже:</span><span class="sxs-lookup"><span data-stu-id="960d4-137">Inside the `api` package is a class named `API`, which contains the following code:</span></span>

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

<span data-ttu-id="960d4-138">За счет использования аннотации `@Path("/helloworld")` путь этой конечной точки, образованный путем добавления префикса `/api`, указанного в классе `Application`, будет равен `/api/helloworld`.</span><span class="sxs-lookup"><span data-stu-id="960d4-138">Through the use of the `@Path("/helloworld")` annotation, we can see that this REST endpoint, when combined with the `/api` specified in the `Application` class, will be `/api/helloworld`.</span></span> <span data-ttu-id="960d4-139">При вызове этой конечной точки с помощью запроса HTTP GET приведенный выше метод возвращает содержимое с типом "text/html". В нашем случае это просто жестко закодированная строка "Hello, world!".</span><span class="sxs-lookup"><span data-stu-id="960d4-139">When this endpoint is called using an HTTP GET request, we can see that the method will produce text/html, and in fact it is simply a hard-coded string "Hello, world!".</span></span>

<span data-ttu-id="960d4-140">Теперь мы описали весь программный код, необходимый для создания микрослужбы с помощью MicroProfile.</span><span class="sxs-lookup"><span data-stu-id="960d4-140">We have now covered all the code required to create a microservice using MicroProfile.</span></span> <span data-ttu-id="960d4-141">Далее мы используем Maven, чтобы собрать нашу службу, упаковать ее в контейнер Docker и запустить локально.</span><span class="sxs-lookup"><span data-stu-id="960d4-141">We can now use Maven to build it, containerize it into a Docker container, and run it locally.</span></span> <span data-ttu-id="960d4-142">Это можно сделать, выполнив следующие действия:</span><span class="sxs-lookup"><span data-stu-id="960d4-142">We can do that with the following steps:</span></span>

1. <span data-ttu-id="960d4-143">Выполните команду `mvn clean package` и дождитесь ее успешного завершения.</span><span class="sxs-lookup"><span data-stu-id="960d4-143">Run `mvn clean package` and wait until it successfully completes.</span></span>

1. <span data-ttu-id="960d4-144">Выполните команду `docker run -it --rm -p 8080:8080 <docker.registry>/<docker.name>:latest`, например `docker run -it --rm -p 8080:8080 jogilescr.azurecr.io/samples/docker-helloworld:latest`, если параметр `docker.registry` равен `jogilescr.azurecr.io` и параметр `docker.name` равен `samples/docker-helloworld`.</span><span class="sxs-lookup"><span data-stu-id="960d4-144">Run `docker run -it --rm -p 8080:8080 <docker.registry>/<docker.name>:latest`, for example, `docker run -it --rm -p 8080:8080 jogilescr.azurecr.io/samples/docker-helloworld:latest`, if your `docker.registry` is `jogilescr.azurecr.io` and `docker.name` is `samples/docker-helloworld`.</span></span>

1. <span data-ttu-id="960d4-145">Попробуйте открыть адреса [http://localhost:8080/microprofile/api/helloworld](http://localhost:8080/microprofile/api/helloworld) и [http://localhost:8080/health](http://localhost:8080/health) в веб-браузере.</span><span class="sxs-lookup"><span data-stu-id="960d4-145">Try accessing [http://localhost:8080/microprofile/api/helloworld](http://localhost:8080/microprofile/api/helloworld) and [http://localhost:8080/health](http://localhost:8080/health) in your web browser.</span></span> <span data-ttu-id="960d4-146">Если вы видите ожидаемый ответ "Hello, world!"</span><span class="sxs-lookup"><span data-stu-id="960d4-146">If you see the expected "Hello, world!"</span></span> <span data-ttu-id="960d4-147">(и сведения о состоянии из конечной точки [/health](http://localhost:8080/health)), значит вы успешно развернули приложение MicroProfile на своем локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="960d4-147">response (and health-related information for the [/health](http://localhost:8080/health) endpoint), you have successfully deployed the MicroProfile application on your local machine.</span></span>

## <a name="pushing-to-the-azure-container-registry"></a><span data-ttu-id="960d4-148">Отправка в Реестр контейнеров Azure</span><span class="sxs-lookup"><span data-stu-id="960d4-148">Pushing to the Azure Container Registry</span></span>

<span data-ttu-id="960d4-149">После успешной сборки и запуска приложения MicroProfile на локальном компьютере следующим шагом станет отправка этого контейнера в созданный ранее реестр.</span><span class="sxs-lookup"><span data-stu-id="960d4-149">Now that we have successfully built and run our MicroProfile application on our local machine, the next step is to push this container into our container registry.</span></span> <span data-ttu-id="960d4-150">Для выполнения задач нашего руководства мы используем Реестр контейнеров Azure, но вы можете использовать любой реестр контейнеров (при условии, что в файле `pom.xml` будет указано соответствующее расположение).</span><span class="sxs-lookup"><span data-stu-id="960d4-150">In this tutorial we are using the Azure Container Registry, but any container registry will work (as long as the `pom.xml` file is edited to point to the relevant location).</span></span>

1. <span data-ttu-id="960d4-151">Выполните `mvn clean package`, чтобы очистить, скомпилировать и создать локальный образ Docker.</span><span class="sxs-lookup"><span data-stu-id="960d4-151">Run `mvn clean package` to clean, compile, and create a local docker image.</span></span>
2. <span data-ttu-id="960d4-152">Выполните `mvn dockerfile:push`, чтобы отправить его в Реестр контейнеров Azure.</span><span class="sxs-lookup"><span data-stu-id="960d4-152">Run `mvn dockerfile:push` to push to the Azure Container Repository.</span></span>

<span data-ttu-id="960d4-153">На этом этапе мы отправили образ контейнера Docker в Реестр контейнеров Azure, но он еще не запущен, потому что образ необходимо развернуть в экземпляре службы Azure "Веб-приложение для контейнеров".</span><span class="sxs-lookup"><span data-stu-id="960d4-153">At this stage you now have your docker container image uploaded to the Azure Container Registry, but it is not yet running as we now have to deploy it into an Azure Web App for Containers instance.</span></span> <span data-ttu-id="960d4-154">Сейчас мы этим займемся.</span><span class="sxs-lookup"><span data-stu-id="960d4-154">We will now do that.</span></span>

## <a name="creating-an-azure-web-app-for-containers-instance"></a><span data-ttu-id="960d4-155">Создание экземпляра службы Azure "Веб-приложение для контейнеров"</span><span class="sxs-lookup"><span data-stu-id="960d4-155">Creating an Azure Web App for Containers instance</span></span>

1. <span data-ttu-id="960d4-156">Вернитесь на [портал Azure](http://portal.azure.com) и создайте новый экземпляр службы Azure "Веб-приложение для контейнеров" (эта функция находится в меню под заголовком "Интернет и мобильные устройства").</span><span class="sxs-lookup"><span data-stu-id="960d4-156">Return to the [Azure Portal](http://portal.azure.com) and create a new Web App for Containers instance (located under the 'Web + Mobile' heading in the menu).</span></span> <span data-ttu-id="960d4-157">Несколько советов:</span><span class="sxs-lookup"><span data-stu-id="960d4-157">A few pointers:</span></span>

   1. <span data-ttu-id="960d4-158">Указанное здесь имя станет общедоступным URL-адресом веб-приложения (хотя позже при необходимости можно добавить личный домен), потому стоит выбрать имя, которое легко запомнить.</span><span class="sxs-lookup"><span data-stu-id="960d4-158">The name you specify here will be the public URL of the web app (although a custom domain can be added later if desired), so it is a good idea to pick a name that you can easily remember.</span></span>

   1. <span data-ttu-id="960d4-159">В разделе "Настроить контейнер" в качестве источника образа можно указать "Реестр контейнеров Azure", а затем выбрать нужный образ в раскрывающихся списках.</span><span class="sxs-lookup"><span data-stu-id="960d4-159">When you get to the 'Configure container' section, you can select 'Azure Container Registry' for the 'Image source', and then select the correct image from the drop-down lists.</span></span>

   1. <span data-ttu-id="960d4-160">Поле "Загрузочный файл" нужно оставить пустым.</span><span class="sxs-lookup"><span data-stu-id="960d4-160">You do not need to specify any value in the 'Startup File' field.</span></span>

1. <span data-ttu-id="960d4-161">После создания экземпляра (это также очень быстрый процесс), щелкните его и выберите пункт меню "Параметры приложения".</span><span class="sxs-lookup"><span data-stu-id="960d4-161">Once the instance is created (again, it is very quick), click on it and then click on the 'Application Settings' menu item.</span></span> <span data-ttu-id="960d4-162">Здесь нужно добавить новый параметр приложения с именем `WEBSITES_PORT` и значением `8080`.</span><span class="sxs-lookup"><span data-stu-id="960d4-162">In here you need to add a new application setting, where the key is `WEBSITES_PORT` and the value is `8080`.</span></span> <span data-ttu-id="960d4-163">Это указывает Azure, какой порт нужно открыть в контейнере, и этот порт будет привязан к порту 80 извне.</span><span class="sxs-lookup"><span data-stu-id="960d4-163">This tells Azure which port you want to expose in the container, and it will be mapped to port 80 externally.</span></span>

1. <span data-ttu-id="960d4-164">Дополнительно можно щелкнуть ссылку "Контейнер Docker" и включить "Непрерывное развертывание", чтобы при каждом обновлении образа в Реестре контейнеров Azure он автоматически обновлялся в экземпляре службы Azure "Веб-приложение для контейнеров".</span><span class="sxs-lookup"><span data-stu-id="960d4-164">Optionally, click on the 'Docker Container' link, and enable 'Continuous Deployment', so that whenever you update the Azure Container Registry image it is automatically updated in the Azure Web App for Containers instance.</span></span>

1. <span data-ttu-id="960d4-165">Экземпляры веб-приложений, развернутых в Azure, должны быть доступны по адресам `http://<appname>.azurewebsites.net/microprofile/api/helloworld` и `http://<appname>.azurewebsites.net/health`.</span><span class="sxs-lookup"><span data-stu-id="960d4-165">You should be able to access the Azure-hosted instances at `http://<appname>.azurewebsites.net/microprofile/api/helloworld` and `http://<appname>.azurewebsites.net/health`.</span></span>

## <a name="summary"></a><span data-ttu-id="960d4-166">Сводка</span><span class="sxs-lookup"><span data-stu-id="960d4-166">Summary</span></span>

<span data-ttu-id="960d4-167">В этом руководстве мы продемонстрировали пошаговый процесс создания простой микрослужбы MicroProfile, которую мы упаковали в контейнер Docker, запустили локально и опубликовали в Azure.</span><span class="sxs-lookup"><span data-stu-id="960d4-167">Through this tutorial we have stepped through the process of creating a simple MicroProfile-based microservice, containerized it into a Docker container, and we have run it locally and published it to Azure.</span></span> <span data-ttu-id="960d4-168">Расширение нашей микрослужбы для добавления более полезных функций выходит за рамки этого руководства, но в Интернете можно найти множество руководств и советов по MicroProfile. Мы рекомендуем читателям посетить веб-сайт [MicroProfile.io](https://microprofile.io/), на котором можно найти дополнительные материалы.</span><span class="sxs-lookup"><span data-stu-id="960d4-168">Extending our microservice to provide more useful functionality is outside the scope of this tutorial, but there is a wealth of tutorials and advice on MicroProfile on the internet, and readers are encouraged to review [MicroProfile.io](https://microprofile.io/) for more content.</span></span>