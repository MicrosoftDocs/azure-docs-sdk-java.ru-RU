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
# <a name="deploy-a-java-based-microprofile-service-to-azure-web-app-for-containers"></a><span data-ttu-id="1b073-103">Развертывание службы MicroProfile на основе Java в службе Azure "Веб-приложение для контейнеров"</span><span class="sxs-lookup"><span data-stu-id="1b073-103">Deploy a Java-based MicroProfile service to Azure Web App for Containers</span></span>

<span data-ttu-id="1b073-104">MicroProfile — отличный способ создавать компактные приложения Java, которые можно быстро и легко развернуть в различных службах, например в решении Azure [Веб-приложение для контейнеров](https://azure.microsoft.com/services/app-service/containers/).</span><span class="sxs-lookup"><span data-stu-id="1b073-104">MicroProfile is a great way to build exceedingly small Java applications that you can quickly and easily deploy to services such as [Azure Web App for Containers](https://azure.microsoft.com/services/app-service/containers/).</span></span> <span data-ttu-id="1b073-105">В этом учебнике мы создадим простую микрослужбу на основе MicroProfile, упакуем ее в контейнер Docker, опубликуем в [экземпляре Реестра контейнеров Azure](https://azure.microsoft.com/services/container-registry/), а затем развернем с помощью службы Azure "Веб-приложение для контейнеров".</span><span class="sxs-lookup"><span data-stu-id="1b073-105">In this tutorial, you create a simple, MicroProfile-based microservice that you containerize into a Docker container, deploy to an [Azure container registry instance](https://azure.microsoft.com/services/container-registry/), and then host by using Azure Web App for Containers.</span></span>

> [!NOTE]
> <span data-ttu-id="1b073-106">Эта процедура подходит для любой реализации MicroProfile.io при условии, что образ контейнера Docker является самовыполняющимся (т. е. образ содержит среду выполнения).</span><span class="sxs-lookup"><span data-stu-id="1b073-106">This procedure works with any implementation of MicroProfile.io, as long the Docker container image is self-executable (that is, the image includes the runtime).</span></span>

<span data-ttu-id="1b073-107">В этом примере мы используем [Payara Micro](https://www.payara.fish/payara_micro) и [MicroProfile 1.3](https://microprofile.io/) для создания небольшого WAR-файла (примерно 5000 байт) веб-приложения Java, а затем упакуем этот файл в образ Docker размером примерно 174 МБ.</span><span class="sxs-lookup"><span data-stu-id="1b073-107">In this sample, you use [Payara Micro](https://www.payara.fish/payara_micro) and [MicroProfile 1.3](https://microprofile.io/) to create a small (approximately 5,000 bytes) Java web application requirement (WAR) file, and then package it into a Docker image of approximately 174 megabytes (MB).</span></span> <span data-ttu-id="1b073-108">Этот образ Docker содержит все компоненты, необходимые для полностью контейнеризированного развертывания нашего веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="1b073-108">The Docker image contains everything necessary for a fully containerized deployment of the web app.</span></span>

<span data-ttu-id="1b073-109">При каждом изменении исходного кода приложения не нужно повторно развертывать весь образ Docker размером 174 МБ, так как Docker отправляет только различия (которые значительно меньшего размера).</span><span class="sxs-lookup"><span data-stu-id="1b073-109">An entire 174 MB Docker image doesn't need to be redeployed whenever the application source code is changed, because Docker uploads only the differences (which are significantly smaller).</span></span> <span data-ttu-id="1b073-110">Это значительно повышает скорость и эффективность развертывания новой версии приложения MicroProfile с помощью конвейера CI/CD, так как снижается сложность и ускоряется цикл разработки.</span><span class="sxs-lookup"><span data-stu-id="1b073-110">Consequently, the process of executing a new release of a MicroProfile application via a CI/CD pipeline is extremely efficient and quick, reducing friction and enabling rapid development iteration.</span></span>

<span data-ttu-id="1b073-111">В этом учебнике мы сначала создадим и выполним программный код локально, а затем развернем его как веб-приложение в Azure.</span><span class="sxs-lookup"><span data-stu-id="1b073-111">You'll work through this tutorial by first creating and running the code locally and then deploying it as a web app on Azure.</span></span> <span data-ttu-id="1b073-112">На обоих стадиях мы будем использовать Docker для упрощения и стандартизации процедуры.</span><span class="sxs-lookup"><span data-stu-id="1b073-112">In both phases, you can depend on Docker to simplify and standardize your efforts.</span></span> <span data-ttu-id="1b073-113">Прежде чем приступить к этой процедуре, вы создадите экземпляр Реестра контейнеров Azure, где будут храниться контейнеры Docker.</span><span class="sxs-lookup"><span data-stu-id="1b073-113">Before you begin, you'll create an Azure container registry instance for storing your Docker containers.</span></span>

## <a name="create-an-azure-container-registry-instance"></a><span data-ttu-id="1b073-114">Создание экземпляра Реестра контейнеров Azure</span><span class="sxs-lookup"><span data-stu-id="1b073-114">Create an Azure container registry instance</span></span>

<span data-ttu-id="1b073-115">Вы можете создать экземпляр Реестра контейнеров Azure на [портале Azure](http://portal.azure.com), но существуют и другие варианты, например использование Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="1b073-115">You can use the [Azure portal](http://portal.azure.com) to create the Azure container registry instance, but there are other choices also, such as the Azure CLI.</span></span> <span data-ttu-id="1b073-116">Чтобы создать экземпляр Реестра контейнеров Azure, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="1b073-116">To create a new Azure container registry instance, do the following:</span></span>

1. <span data-ttu-id="1b073-117">Войдите на [портал Azure](http://portal.azure.com) и создайте ресурс Реестра контейнеров Azure.</span><span class="sxs-lookup"><span data-stu-id="1b073-117">Sign in to the [Azure portal](http://portal.azure.com) and create a new Azure container registry resource.</span></span> <span data-ttu-id="1b073-118">Укажите имя реестра (оно должно быть задано как свойство `docker.registry` в файле *pom.xml*).</span><span class="sxs-lookup"><span data-stu-id="1b073-118">Provide a registry name (this name should be set as the `docker.registry` property in the *pom.xml* file).</span></span> <span data-ttu-id="1b073-119">При необходимости измените значения по умолчанию, а затем нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="1b073-119">Change the defaults as you want, and then select **Create**.</span></span>

1. <span data-ttu-id="1b073-120">Через 30 секунд, когда экземпляр реестра контейнеров станет активным, выберите его, а затем в области слева щелкните ссылку **Ключи доступа**.</span><span class="sxs-lookup"><span data-stu-id="1b073-120">In about 30 seconds, when the container registry instance is live, select the container registry instance and then, in the left pane, select the **Access keys** link.</span></span> 

    <span data-ttu-id="1b073-121">Включите параметр *администратор*, чтобы вы могли получать доступ к этому экземпляру реестра контейнеров со своих компьютеров и отправлять в него контейнеры Docker.</span><span class="sxs-lookup"><span data-stu-id="1b073-121">Be sure to enable the *admin user* setting, so that you can access this container registry instance from your machines and push Docker containers into it.</span></span> <span data-ttu-id="1b073-122">Благодаря этому вы также сможете получать доступ к экземпляру решения Azure "Веб-приложение для контейнеров", который вы вскоре настроите.</span><span class="sxs-lookup"><span data-stu-id="1b073-122">Doing so also enables access from the Azure Web App for Containers instance that you'll set up soon.</span></span>

1. <span data-ttu-id="1b073-123">В области **Ключи доступа** скопируйте значения **username** и **password**, а затем вставьте их в глобальный файл Maven под названием *settings.xml*.</span><span class="sxs-lookup"><span data-stu-id="1b073-123">In the **Access keys** pane, copy the **username** and **password** values and paste them into your global Maven *settings.xml* file.</span></span> <span data-ttu-id="1b073-124">Дополнительные сведения о параметрах Maven см. на веб-сайте [Apache Maven Project](https://maven.apache.org/settings.html).</span><span class="sxs-lookup"><span data-stu-id="1b073-124">For more information about Maven settings, go to the [Apache Maven Project](https://maven.apache.org/settings.html) website.</span></span> 

   <span data-ttu-id="1b073-125">Для справки ниже приведен пример файла *${user.home}/.m2/settings.xml*.</span><span class="sxs-lookup"><span data-stu-id="1b073-125">For your reference, here's an example of the *${user.home}/.m2/settings.xml* file:</span></span>

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

<span data-ttu-id="1b073-126">Теперь, когда вы создали экземпляр реестра контейнеров, можно перейти к созданию и запуску приложения MicroProfile в локальной среде.</span><span class="sxs-lookup"><span data-stu-id="1b073-126">Now that you've created your container registry instance, you can move on to building and running your MicroProfile application locally.</span></span>

## <a name="create-your-microprofile-application"></a><span data-ttu-id="1b073-127">Создание приложения MicroProfile</span><span class="sxs-lookup"><span data-stu-id="1b073-127">Create your MicroProfile application</span></span>

<span data-ttu-id="1b073-128">Этот пример кода основан на примере приложения, который доступен на сайте GitHub.</span><span class="sxs-lookup"><span data-stu-id="1b073-128">This example code is based on a sample application that's available on GitHub.</span></span> <span data-ttu-id="1b073-129">Чтобы клонировать код на свой компьютер, введите следующие команды:</span><span class="sxs-lookup"><span data-stu-id="1b073-129">To clone the code onto your machine, enter the following commands:</span></span>

```
git clone https://github.com/Azure-Samples/microprofile-docker-helloworld.git

cd microprofile-docker-helloworld
```

<span data-ttu-id="1b073-130">В этом каталоге есть файл *pom.xml*, который используется для указания настроек проекта в формате инструмента сборки Maven.</span><span class="sxs-lookup"><span data-stu-id="1b073-130">This directory contains a *pom.xml* file that you use to specify the project in the format that's used by the Maven build tool.</span></span> <span data-ttu-id="1b073-131">Вы можете изменить этот файл в соответствии со своими потребностями.</span><span class="sxs-lookup"><span data-stu-id="1b073-131">You can edit the file to suit your own needs.</span></span> <span data-ttu-id="1b073-132">В частности, свойства `docker.registry` и `docker.name` нужно изменить на `docker.registry` и `docker.name`, которые были созданы при настройке экземпляра Реестра контейнеров Azure.</span><span class="sxs-lookup"><span data-stu-id="1b073-132">In particular, the `docker.registry` and `docker.name` properties should be changed to the `docker.registry` and `docker.name` properties that were created when you set up the Azure container registry instance.</span></span>

<span data-ttu-id="1b073-133">В этой папке также следует обратить внимание на файл Dockerfile, который приведен ниже:</span><span class="sxs-lookup"><span data-stu-id="1b073-133">Another file of note in this directory is the Dockerfile, which is reproduced below:</span></span>

```dockerfile
FROM payara/micro

ARG WAR_FILE
COPY target/${WAR_FILE} $DEPLOY_DIR

EXPOSE 8080
```

<span data-ttu-id="1b073-134">Dockerfile создает контейнер Docker, основанный на контейнере Payara Micro Docker.</span><span class="sxs-lookup"><span data-stu-id="1b073-134">The Dockerfile creates a new Docker container that's based on the Payara Micro Docker Container.</span></span> <span data-ttu-id="1b073-135">Он копирует WAR-файл, который был создан как часть процесса сборки.</span><span class="sxs-lookup"><span data-stu-id="1b073-135">It copies in the WAR file that was created as part of your build process.</span></span> <span data-ttu-id="1b073-136">Кроме того, с помощью файла открывается порт 8080, чтобы вы могли осуществлять доступ к службе после ее запуска в контейнере Docker.</span><span class="sxs-lookup"><span data-stu-id="1b073-136">It also exposes port 8080 so that you can access the service after it's up and running within a Docker container.</span></span>

<span data-ttu-id="1b073-137">Открыв каталог *src*, вы обнаружите в нем класс `Application`, показанный ниже:</span><span class="sxs-lookup"><span data-stu-id="1b073-137">When you open the *src* directory, you'll eventually discover the `Application` class that's reproduced here:</span></span>

```java
package com.microsoft.azure.samples.microprofile.docker.helloworld;

import javax.ws.rs.ApplicationPath;

@ApplicationPath("/api")
public class Application extends javax.ws.rs.core.Application { }
```

<span data-ttu-id="1b073-138">В аннотации *@ApplicationPath("/api")* указана базовая конечная точка этой микрослужбы.</span><span class="sxs-lookup"><span data-stu-id="1b073-138">The *@ApplicationPath("/api")* annotation specifies the base endpoint for this microservice.</span></span> <span data-ttu-id="1b073-139">Таким образом, остальные URL-адреса для доступа к каждой конечной точке REST будут иметь префикс */api*.</span><span class="sxs-lookup"><span data-stu-id="1b073-139">That is, for all endpoints, */api* precedes the rest of the URL that's required to access any specific REST endpoint.</span></span>

<span data-ttu-id="1b073-140">Внутри пакета *api* находится класс с именем `API`, код которого приведен ниже:</span><span class="sxs-lookup"><span data-stu-id="1b073-140">Inside the *api* package is a class named `API`, which contains the following code:</span></span>

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

<span data-ttu-id="1b073-141">За счет использования аннотации *@Path("/helloworld")* путь этой конечной точки REST, образованный путем добавления префикса */api*, указанного в классе `Application`, будет равен */api/helloworld*.</span><span class="sxs-lookup"><span data-stu-id="1b073-141">Through the use of the *@Path("/helloworld")* annotation, you can see that this REST endpoint, when it's combined with the */api* that's specified in the `Application` class, will be */api/helloworld*.</span></span> <span data-ttu-id="1b073-142">При вызове этой конечной точки с помощью запроса HTTP GET приведенный выше метод возвращает содержимое с типом text/html. В нашем случае это просто жестко закодированная строка "Hello, world!".</span><span class="sxs-lookup"><span data-stu-id="1b073-142">When you call this endpoint by using an HTTP GET request, you can see that the method produces text/html and, in fact, it's simply a hard-coded string, "Hello, world!"</span></span>

<span data-ttu-id="1b073-143">В этой статье уже подробно рассмотрен весь код, необходимый для создания микрослужбы с помощью MicroProfile.</span><span class="sxs-lookup"><span data-stu-id="1b073-143">So far, this article has covered all the code that's required for you to create a microservice by using MicroProfile.</span></span> <span data-ttu-id="1b073-144">Теперь вы можете использовать Maven, чтобы собрать нашу службу, упаковать ее в контейнер Docker и запустить локально. Для этого сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="1b073-144">You can now use Maven to build it, containerize it into a Docker container, and run it locally by doing the following:</span></span>

1. <span data-ttu-id="1b073-145">Запустите команду `mvn clean package` и дождитесь ее завершения.</span><span class="sxs-lookup"><span data-stu-id="1b073-145">Run `mvn clean package`, and wait until it is complete.</span></span>

1. <span data-ttu-id="1b073-146">Запустите `docker run -it --rm -p 8080:8080 <docker.registry>/<docker.name>:latest`.</span><span class="sxs-lookup"><span data-stu-id="1b073-146">Run `docker run -it --rm -p 8080:8080 <docker.registry>/<docker.name>:latest`.</span></span> <span data-ttu-id="1b073-147">Например, *docker run -it --rm -p 8080:8080 jogilescr.azurecr.io/samples/docker-helloworld:latest*, где *\<docker.registry>* соответствует *jogilescr.azurecr.io*, а *\<docker.name>*  — *samples/docker-helloworld*.</span><span class="sxs-lookup"><span data-stu-id="1b073-147">For example, *docker run -it --rm -p 8080:8080 jogilescr.azurecr.io/samples/docker-helloworld:latest*, where *\<docker.registry>* is *jogilescr.azurecr.io* and *\<docker.name>* is *samples/docker-helloworld*.</span></span>

1. <span data-ttu-id="1b073-148">Попробуйте открыть адреса [http://localhost:8080/microprofile/api/helloworld](http://localhost:8080/microprofile/api/helloworld) и [http://localhost:8080/health](http://localhost:8080/health) в веб-браузере.</span><span class="sxs-lookup"><span data-stu-id="1b073-148">Try to access [http://localhost:8080/microprofile/api/helloworld](http://localhost:8080/microprofile/api/helloworld) and [http://localhost:8080/health](http://localhost:8080/health) in your web browser.</span></span> <span data-ttu-id="1b073-149">Если вы видите ожидаемый ответ "Hello, world!"</span><span class="sxs-lookup"><span data-stu-id="1b073-149">If you see the expected "Hello, world!"</span></span> <span data-ttu-id="1b073-150">(и сведения о состоянии из конечной точки [/health](http://localhost:8080/health)), значит вы успешно развернули приложение MicroProfile на своем локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="1b073-150">response (and health-related information for the [/health](http://localhost:8080/health) endpoint), you've successfully deployed the MicroProfile application on your local machine.</span></span>

## <a name="push-the-container-to-the-azure-container-registry-instance"></a><span data-ttu-id="1b073-151">Передача контейнера в экземпляр Реестра контейнеров Azure.</span><span class="sxs-lookup"><span data-stu-id="1b073-151">Push the container to the Azure container registry instance</span></span>

<span data-ttu-id="1b073-152">После успешной сборки и запуска приложения MicroProfile на локальном компьютере отправьте этот контейнер в созданный ранее экземпляр реестра контейнеров.</span><span class="sxs-lookup"><span data-stu-id="1b073-152">Now that you've successfully built and run your MicroProfile application on your local machine, push this container to your container registry instance.</span></span> 

> [!NOTE]
> <span data-ttu-id="1b073-153">Несмотря на то что в этой статье используется экземпляр Реестра контейнеров Azure, любой экземпляр реестра контейнеров подойдет. Нужно лишь указать в файле *pom.xml* путь к соответствующему расположению.</span><span class="sxs-lookup"><span data-stu-id="1b073-153">Although this article uses an Azure container registry instance, any container registry instance should work, as long as the *pom.xml* file is edited to point to the relevant location.</span></span>

1. <span data-ttu-id="1b073-154">Чтобы очистить, скомпилировать и создать локальный образ Docker, выполните команду `mvn clean package`.</span><span class="sxs-lookup"><span data-stu-id="1b073-154">To clean, compile, and create a local Docker image, run `mvn clean package`.</span></span>
2. <span data-ttu-id="1b073-155">Чтобы отправить контейнер в экземпляр Реестра контейнеров Azure, выполните команду `mvn dockerfile:push`.</span><span class="sxs-lookup"><span data-stu-id="1b073-155">To push the container to the Azure container registry instance, run `mvn dockerfile:push`.</span></span>

<span data-ttu-id="1b073-156">Теперь ваш образ контейнера Docker передан в экземпляр Реестра контейнеров Azure.</span><span class="sxs-lookup"><span data-stu-id="1b073-156">You now have your Docker container image uploaded to the Azure container registry instance.</span></span> <span data-ttu-id="1b073-157">Однако этот образ еще не запущен.</span><span class="sxs-lookup"><span data-stu-id="1b073-157">However, it's not yet running.</span></span> <span data-ttu-id="1b073-158">Теперь нужно развернуть его в экземпляре решения Azure "Веб-приложение для контейнеров".</span><span class="sxs-lookup"><span data-stu-id="1b073-158">You now have to deploy it to an Azure Web App for Containers instance.</span></span> 

## <a name="create-an-azure-web-app-for-containers-instance"></a><span data-ttu-id="1b073-159">Создание экземпляра решения Azure "Веб-приложение для контейнеров"</span><span class="sxs-lookup"><span data-stu-id="1b073-159">Create an Azure Web App for Containers instance</span></span>

1. <span data-ttu-id="1b073-160">На [портале Azure](http://portal.azure.com) в левой области выберите **Интернет и мобильные устройства**, а затем сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="1b073-160">In the [Azure portal](http://portal.azure.com), in the left pane, select **Web + Mobile**, and then do the following:</span></span>

   <span data-ttu-id="1b073-161">a.</span><span class="sxs-lookup"><span data-stu-id="1b073-161">a.</span></span> <span data-ttu-id="1b073-162">Задайте имя.</span><span class="sxs-lookup"><span data-stu-id="1b073-162">Specify a name.</span></span> <span data-ttu-id="1b073-163">Оно станет общедоступным URL-адресом веб-приложения, поэтому рекомендуется выбрать имя, которое легко запомнить.</span><span class="sxs-lookup"><span data-stu-id="1b073-163">The name will become the public URL of the web app, so it's a good idea to pick a name that you can easily remember.</span></span> <span data-ttu-id="1b073-164">Позже вы можете добавить имя личного домена.</span><span class="sxs-lookup"><span data-stu-id="1b073-164">You can add a custom domain name later, if you want.</span></span>

   <span data-ttu-id="1b073-165">b.</span><span class="sxs-lookup"><span data-stu-id="1b073-165">b.</span></span> <span data-ttu-id="1b073-166">В разделе **Настроить контейнер** в качестве **источника образа** выберите **Реестр контейнеров Azure**, а затем выберите нужный образ в раскрывающемся списке.</span><span class="sxs-lookup"><span data-stu-id="1b073-166">In the **Configure container** section, under **Image source**, select **Azure Container Registry** and then, in the drop-down list, select the correct image.</span></span>

   <span data-ttu-id="1b073-167">c.</span><span class="sxs-lookup"><span data-stu-id="1b073-167">c.</span></span> <span data-ttu-id="1b073-168">Поле **Загрузочный файл** нужно оставить пустым.</span><span class="sxs-lookup"><span data-stu-id="1b073-168">You don't need to specify a value in the **Startup File** field.</span></span>

1. <span data-ttu-id="1b073-169">После создания экземпляра выберите его и щелкните **Параметры приложения**.</span><span class="sxs-lookup"><span data-stu-id="1b073-169">After you've created the instance, select it, and then select **Application Settings**.</span></span> <span data-ttu-id="1b073-170">Для параметра **Ключ** введите **WEBSITES_PORT**, а для параметра **Значение** — **8080**.</span><span class="sxs-lookup"><span data-stu-id="1b073-170">For **Key**, enter **WEBSITES_PORT**, and for **Value**, enter **8080**.</span></span> <span data-ttu-id="1b073-171">Из этих параметров Azure узнает, какой порт нужно открыть в контейнере и с каким внешним портом его нужно сопоставить (80).</span><span class="sxs-lookup"><span data-stu-id="1b073-171">These settings tell Azure which port to expose in the container and to map it to port 80 externally.</span></span>

1. <span data-ttu-id="1b073-172">(Необязательно.) Выберите ссылку **Контейнер Docker**, а затем включите параметр **Непрерывное развертывание**.</span><span class="sxs-lookup"><span data-stu-id="1b073-172">(Optional) Select the **Docker Container** link, and then enable **Continuous Deployment**.</span></span> <span data-ttu-id="1b073-173">Таким образом, при каждом обновлении образа экземпляра Реестра контейнеров Azure он будет автоматически обновляться в экземпляре решения Azure "Веб-приложение для контейнеров".</span><span class="sxs-lookup"><span data-stu-id="1b073-173">By doing so, whenever you update the Azure container registry instance image, it's automatically updated in the Azure Web App for Containers instance.</span></span>

1. <span data-ttu-id="1b073-174">Теперь экземпляры веб-приложений, развернутых в Azure, должны быть доступны по адресам `http://<appname>.azurewebsites.net/microprofile/api/helloworld` и `http://<appname>.azurewebsites.net/health`.</span><span class="sxs-lookup"><span data-stu-id="1b073-174">You should now be able to access the Azure-hosted instances at `http://<appname>.azurewebsites.net/microprofile/api/helloworld` and `http://<appname>.azurewebsites.net/health`.</span></span>

## <a name="summary"></a><span data-ttu-id="1b073-175">Сводка</span><span class="sxs-lookup"><span data-stu-id="1b073-175">Summary</span></span>

<span data-ttu-id="1b073-176">Работая с этим учебником, вы выполнили пошаговый процесс создания простой микрослужбы MicroProfile, которую вы упаковали в контейнер Docker, запустили локально и опубликовали в Azure.</span><span class="sxs-lookup"><span data-stu-id="1b073-176">In this tutorial, you've stepped through the process of creating a simple MicroProfile-based microservice, containerized it into a Docker container, run it locally, and published it to Azure.</span></span> <span data-ttu-id="1b073-177">Вы можете расширить микрослужбу, добавив в нее дополнительные полезные функции.</span><span class="sxs-lookup"><span data-stu-id="1b073-177">You can extend your microservice to provide additional useful functionality.</span></span> <span data-ttu-id="1b073-178">Дополнительные сведения см. на сайте [MicroProfile.io](https://microprofile.io/).</span><span class="sxs-lookup"><span data-stu-id="1b073-178">For more information, go to [MicroProfile.io](https://microprofile.io/).</span></span>
