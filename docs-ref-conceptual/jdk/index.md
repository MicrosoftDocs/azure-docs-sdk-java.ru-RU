---
title: Пакеты JDK и долгосрочная поддержка разработки в Azure
description: Эта статья содержит ссылки для загрузки и заявление о поддержке Azure для разработки и запуска приложений Java.
author: bmitchell287
manager: douge
ms.devlang: java
ms.topic: conceptual
ms.date: 04/09/2019
ms.author: brendm
ms.openlocfilehash: 1bb93f775686b5b0f127c586dda802f4eb5f775d
ms.sourcegitcommit: f8faa4a14c714e148c513fd46f119524f3897abf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/03/2019
ms.locfileid: "67533639"
---
# <a name="java-long-term-support-for-azure-and-azure-stack"></a>Долгосрочная поддержка Java для Azure и Azure Stack

В Microsoft Azure и Azure Stack разработчики Java могут собирать и запускать производственные приложения на Java с помощью коллекции сборок [Azul Zulu Enterprise for Azure](https://www.azul.com/downloads/azure-only/zulu/), не неся при этом дополнительных затрат на поддержку. В Azure можно задействовать любые среды выполнения Java, но при использовании Zulu вы получаете бесплатное обслуживание и обработку запросов службой поддержки Майкрософт.

> [!div class="nextstepaction"]
> [Скачать и установить Java](java-jdk-install.md)

## <a name="long-term-support"></a>Долгосрочная поддержка

* [Java 11](https://www.azul.com/downloads/azure-only/zulu/#java11)
* [Java 8](https://www.azul.com/downloads/azure-only/zulu/#java8);
* [Java 7](https://www.azul.com/downloads/azure-only/zulu/#java7)

## <a name="technical-preview"></a>Техническая предварительная версия

* [Java 12](https://www.azul.com/downloads/azure-only/zulu/#java12)

## <a name="what-is-the-zulu-openjdk-for-azure"></a>Что такое Zulu OpenJDK для Azure?

Сборка OpenJDK типа Azul Zulu Enterprise — это бесплатный мультиплатформенный, готовый дистрибутив OpenJDK для Azure и Azure Stack, который поддерживается корпорацией Майкрософт и Azul Systems. Эти дистрибутивы:

* Являются сборками OpenJDK с полностью открытым кодом, которые упакованы в виде комплектов Java Development Kit (JDK), сред выполнения Java (JRE) и автономных сред JRE. Эти двоичные файлы являются полностью совместимыми коммерческими сборками Java Standard Edition (SE), которые можно использовать с приложениями или компонентами Java в Azure и Azure Stack.
* Предоставляются с долгосрочной поддержкой (LTS), предусматривающей исправление ошибок, улучшение производительности и исправления системы безопасности.
* Доступны для разработки и запуска приложений Java на Windows, Linux и macOS.
* Доступны как образы контейнеров в Docker Hub, а также как виртуальные машины (Windows и Linux) в Azure Marketplace.
* Используются Azure для работы со многими службами Azure, такими как:
  * Служба приложений Azure (Windows)
  * Служба приложений Azure, (Linux)
  * Функции Azure
  * Azure Service Fabric
  * Azure HDInsight
  * Поиск Azure
  * Azure DevOps
  * Azure Cloud Shell  

## <a name="supported-java-versions-and-update-schedule"></a>Поддерживаемые версии Java и график поддержки

Azul Systems предоставляет коллекцию полностью поддерживаемых [сборок OpenJDK под названием Zulu Enterprise для Azure](https://www.azul.com/downloads/azure-only/zulu/) для всех версий Java с долгосрочной поддержкой, начиная с Java SE 7, 8 и 11. Дополнительные сведения см. в [пресс-релизе Azul](https://www.azul.com/press_release/free-java-production-support-for-microsoft-azure-azure-stack).

|Долгосрочная поддержка Java SE  |Поддержка до  |
|---------|----------|
|[![Java 7](../media/jdk/java-7.png)](https://www.azul.com/downloads/azure-only/zulu/#java7) |Июль 2023 г. |
|[![Java 8](../media/jdk/java-8.png)](https://www.azul.com/downloads/azure-only/zulu/#java8) |Март 2025 г.|
|[![Java 11](../media/jdk/java-11.png)](https://www.azul.com/downloads/azure-only/zulu/#java11) |Сентябрь 2026 г.|
|[![Java 12](../media/jdk/java-12.png)]() |**Предварительный просмотр**|

Для этих выпусков JDK выходят ежеквартальные обновления для системы безопасности и исправления ошибок, а также критические внеплановые обновления и исправления при необходимости. Эта поддержка предусматривает обратные порты обновлений безопасности и исправления ошибок для Java 7 и 8, имена которых присутствуют в более новых версиях Java, например Java 11. Эта поддержка гарантирует непрерывную стабильность и безопасность более старых версий Java. Пользователи Azure могут получить эти обновления для системы безопасности и исправления ошибок платформы, не неся при этом незапланированных расходов на подписку на Java SE.

Выпуски от Azul Systems учитывают [график выхода новых версий Java SE](https://www.azul.com/products/azul_support_roadmap/).

## <a name="benefits-for-developers"></a>Преимущества для разработчиков

Выпуски Azul Zulu JDK:

* Поддерживаются корпорацией Майкрософт и Azul Systems.

   * Двоичные файлы Zulu готовы к выпуску и поддерживаются корпорацией Майкрософт и Azul Systems.
   * Zulu поставляется с бесплатной долгосрочной поддержкой для Java 7, 8 и 11 (поддержка LTS будет оказываться и для Java 17). Вы можете обновлять версии Java, только если это необходимо.
   * Java 7 поддерживается до июля 2023 г. Java 8 и 11 поддерживаются до 2024 года и дольше.
   * Корпорация Майкрософт стремится запустить Zulu внутри на компьютерах, которые поддерживают многие службы Azure.

* Готов к выпуску.

   * С полностью открытым кодом для сборок OpenJDK.
   * Упрощенные замены для многих дистрибутивов Java SE.
   * JDK, JRE и автономная JRE.
   * Java 7, 8 и 11.
   * Проверены на соответствие спецификациям Java SE с использованием комплекта технологической совместимости (TCK) сообщества OpenJDK.
   * Разработчики продолжат получать производственные обновления для Java SE, в том числе исправления ошибок, улучшения производительности и исправления системы безопасности для Java SE 7, 8 и 11.

* Поддерживаются для нескольких платформ. Zulu поддерживает двоичные файлы для нескольких платформ и версий, в том числе:

   * Клиент Windows
     * 10
     * 8.1
     * 8, 7
   * Windows Server
     * 2016 R2
     * 2016
     * 2012 R2
     * 2012
     * 2008 R2
   * Linux, включая
     * RHEL
     * CentOS
     * Ubuntu
     * SLES
     * Debian
     * Oracle Linux
   * macOS X
   * Предоставляются в нескольких видах упаковки:
     * MSI, ZIP, TAR, DEB, RPM и DMG.

    В Docker доступны сертифицированные образы контейнеров Docker для Zulu JDK, JRE и автономной среды JRE для нескольких базовых образов ОС.

    Концентратор:

    * [JDK](https://hub.docker.com/_/microsoft-java-jdk).
    * [JRE](https://hub.docker.com/_/microsoft-java-jre)
    * [Автономная среда JRE](https://hub.docker.com/_/microsoft-java-jre-headless).

* Бесплатное использование.

   * Корпорация Майкрософт предоставляет все необходимое для создания и масштабирования приложений Java в Azure бесплатно. Через Zulu вы будете получать бесплатные обновления системы безопасности и исправления ошибок платформы для приложений Java без какой-либо платы.
   * [Java Flight Recorder и Mission Control](java-jdk-flight-recorder-and-mission-control.md) доступны в Zulu Java 8, 11 и 12 (предварительная версия).

* Доступна в виде технической предварительной версии без поддержки LTS.

   * Благодаря технической предварительной версии можно протестировать новые возможности сразу после их внедрения в текущих версиях, и которые со временем перейдут в Java 17 LTS.

* Изменения в OpenJDK отправляются в вышестоящий репозитарий.

   * Разработчики Azul Systems отправляют изменения Zulu в OpenJDK, что делает вышестоящий репозиторий целостным и инклюзивным.

Как обычно, Java-разработчики могут перенести в Azure собственные среды выполнения Java, в том числе Oracle JDK и Red Hat JDK. Можно также использовать безопасную инфраструктуру и многофункциональные службы. Выпуск Oracle Java SE для рабочей среды позволяет выполнять рабочие нагрузки Java на виртуальных машинах Azure (Windows или Linux).

## <a name="use-java-jdks-for-local-development"></a>Использование пакетов Java JDK для локальной разработки 

[Пакеты Java JDK для Azure и Azure Stack можно скачать](https://www.azul.com/downloads/azure-only/zulu/) для использования в локальных средах разработки. Файлы для скачивания доступны для Windows, Linux и macOS. При работе на платформе Linux, можно также получить пакеты с помощью диспетчеров пакетов [yum](https://www.azul.com/downloads/azure-only/zulu/#yum-repo) и [apt](https://www.azul.com/downloads/azure-only/zulu/#apt-repo).

Дополнительные рекомендации см. в статье [Use Docker with a JDK for Azure](java-jdk-docker-images.md) (Использование Docker с JDK для Azure).
