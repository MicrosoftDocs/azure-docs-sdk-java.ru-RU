---
title: Развертывание приложения MicroProfile в облаке с помощью Docker и Azure
description: Узнайте, как развернуть приложение MicroProfile в облаке с помощью Docker и службы "Экземпляры контейнеров Azure".
services: container-instances;container-registry
documentationcenter: java
author: brunoborges
manager: routlaw
editor: brunoborges
ms.assetid: ''
ms.author: brborges
ms.date: 11/21/2018
ms.devlang: java
ms.service: container-instances
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: web
ms.openlocfilehash: 6ba12bb183969103676fa988199603df6cf36bba
ms.sourcegitcommit: f8faa4a14c714e148c513fd46f119524f3897abf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/03/2019
ms.locfileid: "67533606"
---
# <a name="deploy-a-microprofile-app-to-the-cloud-by-using-docker-and-azure"></a>Развертывание приложения MicroProfile в облаке с помощью Docker и Azure

В этой статье показано, как упаковать приложение [MicroProfile.io] в контейнер Docker и запустить его в службе "Экземпляры контейнеров Azure".

> [!NOTE]
> Эта процедура подходит для любой реализации MicroProfile.io при условии, что образ контейнера Docker является самовыполняющимся (т. е. образ содержит среду выполнения).

## <a name="prerequisites"></a>Предварительные требования

Для работы с данным руководством вам потребуется:

* Подписка Azure. Если у вас ее еще нет, создайте [бесплатной учетной записи Azure].
* Установленный [Интерфейс командной строки Azure].
* Поддерживаемая версия Java Development Kit (JDK). Дополнительные сведения о пакетах JDK, которые можно использовать при разработке в Azure, см. в статье [Долгосрочная поддержка Java для Azure и Azure Stack](https://aka.ms/azure-jdks).
* Средство сборки [Apache Maven] (версии 3 или более поздней).
* Клиент [Git].

## <a name="microprofile-hello-azure-sample"></a>Пример приложения MicroProfile Hello Azure

В этой статье мы используем пример приложения [MicroProfile Hello Azure](https://github.com/azure-samples/microprofile-hello-azure). Клонируйте это приложение, выполните его сборку и запустите локально с помощью следующих команд:

```bash
$ git clone https://github.com/Azure-Samples/microprofile-hello-azure.git
$ mvn clean package
...
[INFO] BUILD SUCCESS
...
$ mvn payara-micro:start
...
[2018-07-30T13:34:51.553-0700] [] [INFO] [] [PayaraMicro] [tid: _ThreadID=1 _ThreadName=main] [timeMillis: 1532982891553] [levelValue: 800] Payara Micro  5.182 #badassmicrofish (build 303) ready in 10,304 (ms)
...
```

Приложение можно протестировать с помощью команды `curl` или [веб-браузера](http://localhost:8080/api/hello):

```bash
$ curl http://localhost:8080/api/hello
Hello, Azure!
```

## <a name="deploy-the-app-to-azure"></a>Развертывание приложения в Azure

Теперь развернем это приложение в Azure с помощью служб [Экземпляры контейнеров Azure] и [Реестр контейнеров Azure].

### <a name="build-a-docker-image"></a>Создание образа Docker

Пример проекта содержит файл Dockerfile, который можно использовать. Вам не нужно устанавливать Docker, так как мы воспользуемся функцией сборки Реестра контейнеров Azure для выполнения сборки образа в облаке.

Чтобы создать образ и подготовить его для запуска в Azure, сделайте следующее:

1. Установите Azure CLI и войдите в его систему.
1. Создание группы ресурсов Azure.
1. Создайте экземпляр Реестра контейнеров Azure.
1. Создайте образ Docker.
1. Опубликуйте образ Docker в ранее созданном экземпляре реестра контейнеров.
1. (Необязательно.) Выполните сборку образа и опубликуйте его в экземпляре реестра контейнеров с помощью одной команды.


#### <a name="set-up-the-azure-cli"></a>Настройка Azure CLI

Убедитесь, что у вас есть подписка Azure, установлен [Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest) и вы выполнили проверку подлинности в своей учетной записи.

```bash
az login
```

#### <a name="create-a-resource-group"></a>Создание группы ресурсов

```bash
export ARG=microprofileRG
export ADCL=eastus
az group create --name $ARG --location $ADCL
```

#### <a name="create-a-container-registry-instance"></a>Создание экземпляра реестра контейнеров

С помощью этой команды должен быть создан глобальный уникальный экземпляр реестра контейнеров с простым именем и случайным числом.

```bash
export RANDINT=`date +"%m%d%y$RANDOM"`
export ACR=mydockerrepo$RANDINT
az acr create --name $ACR -g $ARG --sku Basic --admin-enabled
```

#### <a name="build-the-docker-image"></a>Создание образа Docker

Хотя можно легко выполнить сборку образа Docker локально с помощью самого средства Docker, рекомендуем выполнить ее в облаке по ряду причин:

* Нет необходимости устанавливать Docker локально.
* Скорость значительно увеличивается, потому что сборка выполняется в другом расположении (это не влияет на время, требующееся для отправки контекста).
* Для процесса в облаке используется более скоростной интернет-канал, вследствие чего загрузка происходит быстрее.
* Образ попадает непосредственно в экземпляр реестра контейнеров.

Поэтому мы выполнили сборку образа с помощью функции сборки [Служба "Сборка Реестра контейнеров Azure"]:

```bash
export IMG_NAME="mympapp:latest"
az acr build -r $ACR -t $IMG_NAME -g $ARG .
...
Build complete
Build ID: aa1 was successful after 1m2.674577892s
```

#### <a name="deploy-the-docker-image-from-the-azure-container-registry-instance-to-container-instances"></a>Развертывание образа Docker из экземпляра Реестра контейнеров Azure в службе "Экземпляры контейнеров"

Теперь, когда этот образ доступен в экземпляре реестра контейнеров, отправьте его и создайте экземпляр контейнера в службе "Экземпляры контейнеров". Но сначала убедитесь, что вы можете выполнить проверку подлинности в экземпляре реестра контейнеров:

```bash
export ACR_REPO=`az acr show --name $ACR -g $ARG --query loginServer -o tsv`
export ACR_PASS=`az acr credential show --name $ACR -g $ARG --query "passwords[0].value" -o tsv`
export ACI_INSTANCE=myapp`date +"%m%d%y$RANDOM"`

az container create --resource-group $ARG --name $ACR --image $ACR_REPO/$IMG_NAME --cpu 1 --memory 1 --registry-login-server $ACR_REPO --registry-username $ACR --registry-password $ACR_PASS --dns-name-label $ACI_INSTANCE --ports 8080
```

#### <a name="test-your-deployed-microprofile-application"></a>Тестирование развернутого приложения MicroProfile

На этом этапе ваше приложение должно быть запущено. Чтобы протестировать его с помощью интерфейса командной строки, выполните следующую команду:

```bash
curl http://$ACI_INSTANCE.$ADCL.azurecontainer.io:8080/api/hello
````

Поздравляем! Вы успешно собрали приложение MicroProfile в виде контейнера Docker и развернули его в Azure.

## <a name="next-steps"></a>Дополнительная информация

Дополнительные сведения о различных технологиях, рассматриваемых в данной статье, см. по следующим ссылкам.

* [Вход в Azure с помощью Azure CLI](/azure/xplat-cli-connect)

<!-- URL List -->

[Служба "Сборка Реестра контейнеров Azure"]: https://docs.microsoft.com/azure/container-registry/container-registry-build-overview
[MicroProfile.io]: https://microprofile.io
[Интерфейс командной строки Azure]: /cli/azure/overview
[Azure for Java Developers]: https://docs.microsoft.com/java/azure/
[Azure portal]: https://portal.azure.com/
[бесплатной учетной записи Azure]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Apache Maven]: http://maven.apache.org/
[Java Development Kit (JDK)]: https://aka.ms/azure-jdks
<!-- http://www.oracle.com/technetwork/java/javase/downloads/ -->
[Экземпляры контейнеров Azure]: https://docs.microsoft.com/azure/container-instances/;
[Реестр контейнеров Azure]:  https://docs.microsoft.com/azure/container-registry
