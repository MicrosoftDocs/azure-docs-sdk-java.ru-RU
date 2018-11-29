---
title: Пакеты JDK и долгосрочная поддержка разработки в Azure
description: Файлы для скачивания и заявление о поддержке разработки и выполнения приложений на Java в Azure.
author: rloutlaw
manager: angerobe
ms.devlang: java
ms.topic: article
ms.date: 11/13/2018
ms.author: routlaw
ms.openlocfilehash: 0ced17eb17c9d2eda7b1fcc12ffff27b303e8d7e
ms.sourcegitcommit: 8d0c59ae7c91adbb9be3c3e6d4a3429ffe51519d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/27/2018
ms.locfileid: "52339038"
---
# <a name="get-java-jdk-downloads-and-support-when-developing-for-azure"></a>При разработке для Azure вы получаете доступ к пакетам JDK и поддержку

В Azure и Azure Stack разработчики Java могут собирать и запускать производственные приложения на Java с помощью коллекции сборок [Azul Zulu Enterprise for Azure](https://www.azul.com/downloads/azure-only/zulu/), не неся при этом дополнительных затрат на поддержку. В Azure можно использовать любые среды выполнения Java, но при использовании Zulu вы получаете бесплатное обслуживание и можете направлять запросы в службу поддержки Майкрософт в рамках [плана поддержки Azure](https://azure.microsoft.com/support/plans/).

Разработчики могут использовать собственные среды выполнения Java, включая Oracle JDK и Red Hat JDK, чтобы выполнять приложения в Azure и подключаться к службам и функциям Azure. Выпуск Oracle Java SE для рабочей среды по-прежнему доступен для разработчиков Java, выполняющих рабочие нагрузки в на виртуальных машинах Azure (Windows или Linux).

## <a name="supported-java-versions-and-update-schedule"></a>Поддерживаемые версии Java и график поддержки

Azul Systems предоставляет коллекцию полностью поддерживаемых [сборок OpenJDK под названием Zulu Enterprise для Microsoft Azure](https://www.azul.com/downloads/azure-only/zulu/) для всех версий Java с долгосрочной поддержкой, начиная с Java SE 7, 8 и 11. Дополнительные сведения см. в [пресс-релизе Azul](https://www.azul.com/press_release/free-java-production-support-for-microsoft-azure-azure-stack).


Для этих выпусков JDK будут выходить ежеквартальные обновления для системы безопасности и исправления ошибок, а также критические внеплановые обновления и исправления при необходимости.  Поддержка включает в себя обратное портирование обновлений для системы безопасности и исправлений ошибок для Java 7 и 8, обнаруженных в более новых версиях Java, например Java 11, и гарантирует стабильную работу и безопасность приложений на старых версиях Java.  Пользователи Azure имеют право на получение этих обновлений для системы безопасности и исправлений ошибок платформы, не неся при этом незапланированных расходов на подписку на Java SE. Ниже показан график поддержки каждой версии Java SE.

![График поддержки JDK для Azure](media/azure-jdk-support.png)

Выпуски от Azul Systems учитывают [график выхода новых версий Java SE](https://www.azul.com/products/azul_support_roadmap/).

## <a name="use-for-local-development"></a>Использование в локальной разработке 

Пакеты JDK для Azure и Azure Stack доступны для [скачивания](https://www.azul.com/downloads/azure-only/zulu/) разработчиками для использования в локальных средах разработки. Файлы для скачивания доступны для Windows, Linux и macOS. Разработчики, работающие на платформе Linux, могут также получить пакеты с помощью диспетчеров пакетов [yum](https://www.azul.com/downloads/azure-only/zulu/#yum-repo) и [apt](https://www.azul.com/downloads/azure-only/zulu/#apt-repo).

Поддержка возможностей локальной разработки для JDK в Azure или Azure Stack реализована в рамках [соответствующего плана поддержки Azure](https://azure.microsoft.com/support/plans/).

## <a name="use-in-docker-containers"></a>Использование в контейнерах Docker

Вы можете создавать неограниченное количество образов Docker с помощью сборок OpenJDK Zulu Enterprise на базе любых дистрибутивов на свое усмотрение. Образы Zulu Docker на основе Azul Zulu Enterprise для Azure JDK доступны в [общедоступном репозитории Docker корпорации Майкрософт](https://hub.docker.com/r/microsoft/java-jdk/). Файлы Dockerfile, которые использовались при создании этих образов, доступны в [репозитории GitHub корпорации Майкрософт для Java](https://github.com/Microsoft/java/tree/master/docker).

Чтобы упаковать приложение в контейнер с помощью этих образов, вам потребуется задать оператор `FROM` в файле Dockerfile и затем настроить контейнер, установив зависимости приложения. Например, чтобы запустить приложение на Java SE, упакованное в JAR-файл, с привязкой к порту 8080, укажите следующее:

```Dockerfile
FROM  microsoft/java-jdk:<tag>
EXPOSE 8080
ADD target/hello.jar hello.jar
ENTRYPOINT ["java", "-jar","/hello.jar"]
```

## <a name="azure-service-runtime-support"></a>Поддержка среды выполнения службами Azure

Службы платформы Azure, такие как [Служба приложений Azure](/azure/app-service/containers/), [Функции Azure](/azure/azure-functions/functions-create-first-java-maven), [Service Fabric](/azure/service-fabric/) и [HDInsight](/azure/hdinsight/) используют сборки OpenJDK Zulu Enterprise со встроенной функцией автоматического обновления системы безопасности и исправления ошибок для промежуточных версий Java.