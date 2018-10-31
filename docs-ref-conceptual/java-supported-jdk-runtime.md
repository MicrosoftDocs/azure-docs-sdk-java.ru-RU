---
title: Пакеты JDK и долгосрочная поддержка разработки в Azure
description: Файлы для скачивания и заявление о поддержке разработки и выполнения приложений на Java в Azure.
author: rloutlaw
manager: angerobe
ms.devlang: java
ms.topic: article
ms.date: 10/15/2017
ms.author: routlaw
ms.openlocfilehash: 2865219f350990e8b07f7d2cd99f536168a6b8d4
ms.sourcegitcommit: 7df2d442ad7cbdb235e5dd35302a9b73379c23d5
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/25/2018
ms.locfileid: "50027000"
---
# <a name="get-java-jdk-downloads-and-support-when-developing-for-azure"></a>При разработке для Azure вы получаете доступ к пакетам JDK и поддержку

В Azure и Azure Stack разработчики Java могут собирать и запускать производственные приложения на Java с помощью [сборок OpenJDK от Azul Systems под названием Zulu Enterprise](https://www.azul.com/downloads/azure-only/zulu/), не неся при этом дополнительных затрат на поддержку. В Azure можно использовать любые среды выполнения Java, но при использовании Zulu вы получаете бесплатное обслуживание и можете направлять запросы в службу поддержки Майкрософт в рамках [плана поддержки Azure](https://azure.microsoft.com/support/plans/).

## <a name="supported-java-versions-and-update-schedule"></a>Поддерживаемые версии Java и график поддержки

Azul Systems предоставляет коллекцию полностью поддерживаемых [сборок OpenJDK под названием Zulu Enterprise для Microsoft Azure](https://www.azul.com/downloads/azure-only/zulu/) для всех версий Java с долгосрочной поддержкой, начиная с Java SE 7, 8 и 11. Дополнительные сведения см. в [пресс-релизе Azul](https://www.azul.com/press_release/free-java-production-support-for-microsoft-azure-azure-stack).


Для этих выпусков JDK будут выходить ежеквартальные обновления для системы безопасности и исправления ошибок, а также критические внеплановые обновления и исправления при необходимости.  Поддержка включает в себя обратное портирование обновлений для системы безопасности и исправлений ошибок для Java 7 и 8, обнаруженных в более новых версиях Java, например Java 11, и гарантирует стабильную работу и безопасность приложений на старых версиях Java.  Пользователи Azure имеют право на получение этих обновлений для системы безопасности и исправлений ошибок платформы, не неся при этом незапланированных расходов на подписку на Java SE. Ниже показан график поддержки каждой версии Java SE.

![График поддержки JDK для Azure](media/azure-jdk-support.png)

Выпуски от Azul Systems учитывают [график выхода новых версий Java SE](https://www.azul.com/products/azul_support_roadmap/).

## <a name="use-for-local-development"></a>Использование в локальной разработке 

Пакеты JDK для Azure и Azure Stack доступны для скачивания разработчиками на [веб-сайте Azul Systems](https://www.azul.com/downloads/azure-only/zulu/). Файлы для скачивания доступны для Windows, Linux и macOS. Разработчики, работающие на платформе Linux, могут также получить пакеты с помощью диспетчеров пакетов [yum](https://www.azul.com/downloads/azure-only/zulu/#yum-repo) и [apt](https://www.azul.com/downloads/azure-only/zulu/#apt-repo).

Техническая поддержка пакета Azul Zulu JDK при разработке в Azure или Azure Stack предоставляется в рамках [плана поддержки Azure](https://azure.microsoft.com/support/plans/).

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