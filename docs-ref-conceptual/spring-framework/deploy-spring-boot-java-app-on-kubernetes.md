---
title: Развертывание приложения Spring Boot в Kubernetes в Службе контейнеров Azure
description: В этом руководстве содержатся пошаговые инструкции по развертыванию приложения Spring Boot в кластере Kubernetes в Microsoft Azure.
services: container-service
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: ''
ms.assetid: ''
ms.author: asirveda;robmcm
ms.date: 02/01/2018
ms.devlang: java
ms.service: multiple
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: na
ms.custom: mvc
ms.openlocfilehash: 9eb37f302835ea40e92b5212d5bbc305d1311bc4
ms.sourcegitcommit: 151aaa6ccc64d94ed67f03e846bab953bde15b4a
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/03/2018
ms.locfileid: "28954645"
---
# <a name="deploy-a-spring-boot-application-on-a-kubernetes-cluster-in-the-azure-container-service"></a>Развертывание приложения Spring Boot в кластере Kubernetes в службе контейнеров Azure

**[Kubernetes]** и **[Docker]**  — это решения с открытым кодом, которые помогают разработчикам автоматизировать развертывание и масштабирование выполняемых в контейнере приложений, а также управление ими.

В этом руководстве представлены пошаговые инструкции по объединению этих двух популярных технологий с открытым кодом для разработки и развертывания приложения Spring Boot в Microsoft Azure. В частности, *[Spring Boot]* используется для разработки приложений, *[Kubernetes]* — для развертывания контейнеров, а [Служба контейнеров Azure] — для размещения приложений.

### <a name="prerequisites"></a>предварительным требованиям

* Подписка Azure. Если у вас ее еще нет, вы можете активировать [преимущества для подписчиков MSDN] или зарегистрироваться для получения [бесплатной учетной записи Azure].
* [Интерфейс командной строки Azure (CLI)].
* Актуальная версия [Java Developer Kit (JDK)].
* Средство сборки [Maven] (версия 3) от Apache.
* Клиент [Git].
* Клиент [Docker].

> [!NOTE]
>
> С учетом требований виртуализации для этого руководства изложенные здесь инструкции нельзя выполнять на виртуальной машине. Необходимо использовать физический компьютер с включенными функциями виртуализации.
>

## <a name="create-the-spring-boot-on-docker-getting-started-web-app"></a>Создание веб-приложения Spring Boot on Docker Getting Started

Ниже представлены инструкции по созданию веб-приложения Spring Boot и его локальному тестированию.

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

1. Клонируйте пример проекта [Spring Boot on Docker Getting Started] в каталог.
   ```
   git clone https://github.com/spring-guides/gs-spring-boot-docker.git
   ```

1. Перейдите в каталог готового проекта.
   ```
   cd gs-spring-boot-docker
   cd complete
   ```

1. Используйте Maven для создания и запуска примера приложения.
   ```
   mvn package spring-boot:run
   ```

1. Чтобы протестировать веб-приложение, перейдите по адресу http://localhost:8080 или введите команду `curl`:
   ```
   curl http://localhost:8080
   ```

1. Должно появиться следующее сообщение: **Hello Docker World**.

   ![Просмотр примера приложения в локальной среде][SB01]

## <a name="create-an-azure-container-registry-using-the-azure-cli"></a>Создание реестра контейнеров Azure с помощью Azure CLI

1. Откройте окно командной строки.

1. Войдите в свою учетную запись Azure.
   ```azurecli
   az login
   ```

1. Создайте группу ресурсов Azure, используемых в этом руководстве.
   ```azurecli
   az group create --name=wingtiptoys-kubernetes --location=eastus
   ```

1. Создайте частный реестр контейнеров Azure в группе ресурсов. Позднее в руководстве пример принудительно отправляется в этот реестр как образ Docker. Замените `wingtiptoysregistry` уникальным именем для реестра.
   ```azurecli
   az acr create --admin-enabled --resource-group wingtiptoys-kubernetes--location eastus \
    --name wingtiptoysregistry --sku Basic
   ```

## <a name="push-your-app-to-the-container-registry"></a>Принудительная отправка приложения в реестр контейнеров

1. Перейдите в каталог конфигурации для установки Maven (по умолчанию ~/.m2/ или C:\Users\username\.m2) и откройте файл *settings.xml* в текстовом редакторе.

1. Получите пароль для реестра контейнеров из Azure CLI.
   ```azurecli
   az acr credential show --name wingtiptoysregistry --query passwords[0]
   ```

   ```json
   {
     "name": "password",
     "value": "AbCdEfGhIjKlMnOpQrStUvWxYz"
   }
   ```

1. Добавьте идентификатор и пароль реестра контейнеров Azure для новой коллекции `<server>` в файле *settings.xml*.
`id` и `username` — это имена реестра. Используйте значение `password` из предыдущей команды (без кавычек).

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

1. Обновите коллекцию `<properties>` в файле *pom.xml*, добавив значение сервера входа для реестра контейнеров Azure.

   ```xml
   <properties>
      <docker.image.prefix>wingtiptoysregistry.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
   </properties>
   ```

1. Обновите коллекцию `<plugins>` в файле *pom.xml* таким образом, чтобы в `<plugin>` содержались адрес сервера входа и имя реестра контейнеров Azure.

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

1. Перейдите в каталог завершенного проекта для приложения Spring Boot и выполните указанную ниже команду для создания контейнера Docker и отправки образа в реестр:

   ```
   mvn package docker:build -DpushImage
   ```

> [!NOTE]
>
>  При отправке образа из Maven в Azure может появиться сообщение об ошибке такого типа:
>
> * `[ERROR] Failed to execute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: no basic auth credentials`
>
> * `[ERROR] Failed to execute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: Incomplete Docker registry authorization credentials. Please provide all of username, password, and email or none.`
>
> При возникновении этой ошибки войдите в Azure из командной строки Docker.
>
> `docker login -u wingtiptoysregistry -p "AbCdEfGhIjKlMnOpQrStUvWxYz" wingtiptoysregistry.azurecr.io`
>
> Затем принудительно отправьте контейнер:
>
> `docker push wingtiptoysregistry.azurecr.io/gs-spring-boot-docker`

## <a name="create-a-kubernetes-cluster-on-aks-using-the-azure-cli"></a>Создание в Службе контейнеров Azure кластера Kubernetes с помощью Azure CLI

1. Создайте кластер Kubernetes в службе контейнеров Azure. Следующая команда отвечает за создание кластера *kubernetes* в группе ресурсов *wingtiptoys-kubernetes* с именем кластера *wingtiptoys-containerservice* и префиксом DNS *wingtiptoys kubernetes*:
   ```azurecli
   az acs create --orchestrator-type=kubernetes --resource-group=wingtiptoys-kubernetes \ 
    --name=wingtiptoys-containerservice --dns-prefix=wingtiptoys-kubernetes
   ```
   Выполнение этой команды может занять некоторое время.

1. Установите `kubectl` с использованием Azure CLI. Пользователи Linux могут добавить к этой команде префикс `sudo`, так как она развертывает интерфейс командной строки Kubernetes в `/usr/local/bin`.
   ```azurecli
   az acs kubernetes install-cli
   ```

1. Скачайте сведения о конфигурации кластера, чтобы управлять им из веб-интерфейса Kubernetes и `kubectl`. 
   ```azurecli
   az acs kubernetes get-credentials --resource-group=wingtiptoys-kubernetes  \ 
    --name=wingtiptoys-containerservice
   ```

## <a name="deploy-the-image-to-your-kubernetes-cluster"></a>Развертывание образа в кластере Kubernetes

В этом руководстве с помощью `kubectl` развертывается приложение, а затем предоставляется возможность изучить развертывание с помощью веб-интерфейса Kubernetes.

### <a name="deploy-with-the-kubernetes-web-interface"></a>Развертывание с помощью веб-интерфейса Kubernetes

1. Откройте окно командной строки.

1. Откройте веб-сайт конфигурации кластера Kubernetes в браузере по умолчанию:
   ```
   az acs kubernetes browse --resource-group=wingtiptoys-kubernetes --name=wingtiptoys-containerservice
   ```

1. Когда в браузере откроется веб-сайт конфигурации Kubernetes, щелкните ссылку, чтобы **развернуть контейнерное приложение**:

   ![Веб-сайт конфигурации Kubernetes][KB01]

1. Когда отобразится страница **Deploy a containerized app** (Развернуть контейнерное приложение), укажите следующие параметры:

   a. Выберите **Specify app details below** (Указать сведения о приложении ниже).

   Б. Укажите имя приложения Spring Boot в поле **Имя приложения** (например, *gs-spring-boot-docker*).

   c. Укажите сервер входа и образ контейнера, заданные ранее, в поле **Образ контейнера** (например, *wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest*).

   d. Для параметра **Служба** выберите значение **Внешняя**.

   д. Укажите внешний и внутренний порты в текстовых полях **Порт** и **Целевой порт**.

   ![Веб-сайт конфигурации Kubernetes][KB02]


1. Нажмите кнопку **Развернуть**, чтобы развернуть контейнер.

   ![Развертывание контейнера][KB05]

1. После развертывания приложение Spring Boot отобразится в списке **Службы**.

   ![Службы Kubernetes][KB06]

1. Щелкнув ссылку для **внешних конечных точек**, можно просмотреть сведения о выполнении приложения Spring Boot в Azure.

   ![Службы Kubernetes][KB07]

   ![Просмотр примера приложения в Azure][SB02]


### <a name="deploy-with-kubectl"></a>Развертывание с помощью kubectl

1. Откройте окно командной строки.

1. Запустите контейнер в кластере Kubernetes с помощью команды `kubectl run`. Присвойте приложению имя службы в Kubernetes и полное имя образа. Например: 
   ```
   kubectl run gs-spring-boot-docker --image=wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest
   ```
   В этой команде:

   * Имя контейнера `gs-spring-boot-docker` указано сразу после команды `run`.

   * Параметр `--image` указывает объединенное имя сервера входа и образа как `wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest`.

1. Предоставьте кластер Kubernetes извне с помощью команды `kubectl expose`. Укажите имя службы, общедоступный TCP-порт, используемый для доступа к приложению, и внутренний целевой порт, прослушиваемый приложением. Например: 
   ```
   kubectl expose deployment gs-spring-boot-docker --type=LoadBalancer --port=80 --target-port=8080
   ```
   В этой команде:

   * Имя контейнера `gs-spring-boot-docker` указано сразу после команды `expose deployment`.

   * Параметр `--type` указывает, что кластер использует подсистему балансировки нагрузки.

   * Параметр `--port` указывает общедоступный TCP-порт 80. Через этот порт вы осуществляете доступ к приложению.

   * Параметр `--target-port` указывает общедоступный TCP-порт 8080. Через этот порт подсистема балансировки нагрузки переадресовывает запросы к приложению.

1. После развертывания приложения в кластере подайте запрос на внешний IP-адрес и откройте его в своем веб-браузере:

   ```
   kubectl get services -o jsonpath={.items[*].status.loadBalancer.ingress[0].ip} --namespace=${namespace}
   ```

   ![Просмотр примера приложения в Azure][SB02]


## <a name="next-steps"></a>Дополнительная информация

Дополнительные сведения об использовании Spring Boot в Azure см. в следующих статьях:

* [Развертывание приложения Spring Boot Application в службе приложений Azure](deploy-spring-boot-java-web-app-on-azure.md)
* [Развертывание приложения Spring Boot в Linux в службе контейнеров Azure](deploy-spring-boot-java-app-on-linux.md)

Дополнительные сведения об использовании Azure с Java см. в руководствах по [Azure для разработчиков Java] и [инструментах Java для Visual Studio Team Services].

Дополнительные сведения о примере проекта Spring Boot в Docker см. в разделе [Spring Boot on Docker Getting Started].

По следующим ссылкам представлены дополнительные сведения о создании приложений Spring Boot:

* Дополнительные сведения о создании простого приложения Spring Boot см. на странице Spring Initializr по адресу https://start.spring.io/.

По следующим ссылкам представлены дополнительные сведения об использовании Kubernetes с Azure:

* [Развертывание кластера Kubernetes для контейнеров Linux](https://docs.microsoft.com/azure/container-service/container-service-kubernetes-walkthrough)
* [Использование веб-интерфейса Kubernetes со службой контейнеров Azure](https://docs.microsoft.com/azure/container-service/container-service-kubernetes-ui)

Дополнительные сведения об использовании интерфейса командной строки Kubernetes доступны в руководстве пользователя **kubectl** по адресу <https://kubernetes.io/docs/user-guide/kubectl/>.

На сайте Kubernetes содержится несколько статей, посвященных использованию образов в частных реестрах:

* [Configure Service Accounts for Pods] (Настройка учетных записей службы для модулей Pod)
* [Namespaces] (Пространства имен)
* [Pull an Image from a Private Registry] (Извлечение образа из частного реестра)

Дополнительные примеры использования пользовательских образов Docker в Azure см. в разделе [Применение пользовательского образа Docker для веб-приложения Azure на платформе Linux].

<!-- URL List -->

[Интерфейс командной строки Azure (CLI)]: /cli/azure/overview
[Служба контейнеров Azure]: https://azure.microsoft.com/services/container-service/
[Azure для разработчиков Java]: https://docs.microsoft.com/java/azure/
[Azure portal]: https://portal.azure.com/
[Create a private Docker container registry using the Azure portal]: /azure/container-registry/container-registry-get-started-portal
[Применение пользовательского образа Docker для веб-приложения Azure на платформе Linux]: /azure/app-service-web/app-service-linux-using-custom-docker-image
[Docker]: https://www.docker.com/
[бесплатной учетной записи Azure]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[инструментах Java для Visual Studio Team Services]: https://java.visualstudio.com/ (Инструменты Java для Visual Studio Team Services)
[Kubernetes]: https://kubernetes.io/
[Kubernetes Command-Line Interface (kubectl)]: https://kubernetes.io/docs/user-guide/kubectl-overview/
[Maven]: http://maven.apache.org/
[преимущества для подписчиков MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Boot on Docker Getting Started]: https://github.com/spring-guides/gs-spring-boot-docker
[Spring Framework]: https://spring.io/
[Configure Service Accounts for Pods]: https://kubernetes.io/docs/tasks/configure-pod-container/configure-service-account/ (Настройка учетных записей службы для модулей Pod)
[Namespaces]: https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/ (Пространства имен)
[Pull an Image from a Private Registry]: https://kubernetes.io/docs/tasks/configure-pod-container/pull-image-private-registry/ (Извлечение образа из частного реестра)

<!-- IMG List -->

[SB01]: ./media/deploy-spring-boot-java-app-on-kubernetes/SB01.png
[SB02]: ./media/deploy-spring-boot-java-app-on-kubernetes/SB02.png

[AR01]: ./media/deploy-spring-boot-java-app-on-kubernetes/AR01.png
[AR02]: ./media/deploy-spring-boot-java-app-on-kubernetes/AR02.png
[AR03]: ./media/deploy-spring-boot-java-app-on-kubernetes/AR03.png
[AR04]: ./media/deploy-spring-boot-java-app-on-kubernetes/AR04.png

[KB01]: ./media/deploy-spring-boot-java-app-on-kubernetes/KB01.png
[KB02]: ./media/deploy-spring-boot-java-app-on-kubernetes/KB02.png
[KB03]: ./media/deploy-spring-boot-java-app-on-kubernetes/KB03.png
[KB04]: ./media/deploy-spring-boot-java-app-on-kubernetes/KB04.png
[KB05]: ./media/deploy-spring-boot-java-app-on-kubernetes/KB05.png
[KB06]: ./media/deploy-spring-boot-java-app-on-kubernetes/KB06.png
[KB07]: ./media/deploy-spring-boot-java-app-on-kubernetes/KB07.png
