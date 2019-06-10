---
title: Установка Azul Zulu JDK для Azure и Azure Stack
description: Установка пакетов средств разработки Azul Zulu Java (JDK) для разработки в Azure на платформах Windows, Linux и Mac
author: erickson-doug
manager: douge
ms.author: douge
ms.date: 4/19/2019
ms.devlang: java
ms.topic: conceptual
ms.openlocfilehash: 33d2206f9a0a1cc9fadc60b17c1a93f66c592fe3
ms.sourcegitcommit: 04cff6e3c6d3a9c15f7d88d5d3c238f0bdc787fd
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2019
ms.locfileid: "64568597"
---
# <a name="install-the-jdk-for-azure-and-azure-stack"></a>Установка JDK для Azure и Azure Stack

Сборка OpenJDK типа Azul Zulu Enterprise — это бесплатный мультиплатформенный, готовый дистрибутив OpenJDK для Azure и Azure Stack, который поддерживается корпорацией Майкрософт и Azul Systems. Они содержат все компоненты для сборки и запуска приложений Java SE.

Существует [несколько типов пакетов для скачивания, поддерживаемых для каждой клиентской ОС](https://www.azul.com/downloads/azure-only/zulu/). Вы также можете получить образ виртуальной машины из коллекции Azure Marketplace для следующих платформ:

  * [Azul Zulu: Java 8 на Ubuntu 18.04](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/azul.azul-zulu8-ubuntu-1804)
  * [Azul Zulu: Java 8 на Windows Server 2019](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/azul.azul-zulu8-windows-2019)
  
  * [Azul Zulu: Java 11 на Ubuntu 18.04](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/azul.azul-zulu11-ubuntu-1804)
  * [Azul Zulu: Java 11 на Windows Server 2019](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/azul.azul-zulu11-windows-2019)


> [!NOTE]
> Эти инструкции предназначены для 64-разрядной версии Java 8 JDK. Azul также предоставляет среду выполнения Java (JRE) в виде автономной установки. JRE входит в состав установки JDK.
>
>  Пакеты Java 11 также предоставляются на [странице загрузки Azure на сайте Azul](https://www.azul.com/downloads/azure-only/zulu/).

## <a name="download-and-install-the-azul-zulu-jdks-for-windows"></a>Скачивание и установка пакетов Azul Zulu JDK для Windows 

1. [Скачайте 64-разрядный пакет Azul Zulu JDK 8 как MSI-файл](https://repos.azul.com/azure-only/zulu/packages/zulu-11/11.0.3/zulu-11-azure-jdk_11.31.11-11.0.3-win_x64.msi) в расположение на клиенте, например `C:\Users\<your_login>\Downloads`. (Пакеты ZIP также предоставляются на [странице загрузки Azure на сайте Azul](https://www.azul.com/downloads/azure-only/zulu/).)

2. Перейдите в каталог и дважды щелкните скачанный MSI-файл, чтобы начать установку.

## <a name="download-and-install-the-azul-zulu-jdks-for-mac"></a>Скачивание и установка пакетов Azul Zulu JDK для Mac 

По приведенной ниже ссылке можно скачать ZIP-файл на компьютер Mac. Доступна также версия DMG.

1. [Скачайте 64-разрядный пакет Azul Zulu JDK 8 как ZIP-файл](https://repos.azul.com/azure-only/zulu/packages/zulu-11/11.0.3/zulu-11-azure-jdk_11.31.11-11.0.3-macosx_x64.zip) в расположение на клиенте, например `/Library/Java/JavaVirtualMachines/`. (Пакеты DMG также предоставляются на [странице загрузки Azure на сайте Azul](https://www.azul.com/downloads/azure-only/zulu/).)

2. Запустите Finder, перейдите в каталог скачивания и дважды щелкните ZIP-файл. Кроме того, вы можете запустить окно команды терминала, перейти в каталог и запустить:

```cli
unzip <name_of_zulu_package>.zip
```

## <a name="download-and-install-the-azul-zulu-jdks-for-alpine-linux"></a>Скачивание и установка пакетов Azul Zulu JDK для Alpine Linux

1. [Скачайте 64-разрядный пакет Azul Zulu JDK 8 как TAR-файл](https://repos.azul.com/azure-only/zulu/packages/zulu-11/11.0.3/zulu-11-azure-jdk_11.31.11-11.0.3-linux_x64.tar.gz) в расположение на клиенте, например `/usr/lib/jvm`. (Пакеты RPM и DEB также предоставляются на [странице загрузки Azure на сайте Azul](https://www.azul.com/downloads/azure-only/zulu/).)

2. Перейдите в каталог и запустите следующую команду, чтобы распаковать и развернуть файл:

    ```cli
    tar -xvf <name_of_zulu_package>.tar
    ```

## <a name="confirm-your-installation"></a>Подтверждение установки

Чтобы подтвердить установку, перейдите в командную строку и запустите команду `java -version`.

Результат выполнения команды должен выглядеть следующим образом:

```cli
$ java -version

openjdk version "1.8.0_212"
OpenJDK Runtime Environment (Zulu 8.38.0.13-macosx)-Microsoft-Azure-restricted (build 1.8.0_212-b04)
OpenJDK 64-Bit Server VM (Zulu 8.38.0.13-macosx)-Microsoft-Azure-restricted (build 25.212-b04, mixed mode)

```

## <a name="download-and-install-the-azul-zulu-jdks-from-a-yum-repository"></a>Скачивание и установка пакетов Azul Zulu JDK из репозитория Yum

Azul размещает пакеты Azul Zulu JDK в [репозитории Yum](http://repos.azul.com/azure-only/zulu-azure.repo).

**Чтобы установить пакет Azul Zulu JDK для Java 8, запустите следующие команды из CLI:**

```cli
sudo rpm --import http://repos.azul.com/azul-repo.key
sudo curl http://repos.azul.com/azure-only/zulu-azure.repo -o /etc/yum.repos.d/zulu-azure.repo
sudo yum -q -y update
sudo yum -q -y install zulu-8-azure-jdk
```

Для Java 11 запустите:

```cli
sudo rpm --import http://repos.azul.com/azul-repo.key
sudo curl http://repos.azul.com/azure-only/zulu-azure.repo -o /etc/yum.repos.d/zulu-azure.repo
sudo yum -q -y update
sudo yum -q -y install zulu-11-azure-jdk
```

Для Java 12 (предварительная версия) запустите:

```cli
sudo rpm --import http://repos.azul.com/azul-repo.key
sudo curl http://repos.azul.com/azure-only/zulu-azure.repo -o /etc/yum.repos.d/zulu-azure.repo
sudo yum -q -y update
sudo yum -q -y install zulu-12-azure-jdk
```

**Чтобы обновить пакет Zulu JDK 8 из репозитория Yum:**

```cli
sudo yum -q -y install zulu-8-azure-jdk
```

(Измените номер версии в приведенной выше команде, если вы используете версии 11 или 12.)

**Чтобы удалить пакет Zulu JDK 8 из репозитория Yum:**

```cli
sudo yum -y erase zulu-8-azure-jdk
```
(Измените номер версии в приведенной выше команде, если вы используете версии 11 или 12.)

## <a name="download-and-install-the-azul-zulu-jdks-from-an-apt-get-repository"></a>Скачивание и установка пакетов Azul Zulu JDK из репозитория apt-get

Azul также размещает пакеты Azul Zulu JDK в [репозитории apt-get](http://repos.azul.com/azure-only/zulu/apt).

**Чтобы установить пакет Azul Zulu JDK для Java 8 из репозитория apt-get, запустите следующие команды из CLI:**

```cli
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 0xB1998361219BD9C9
sudo apt-add-repository "deb http://repos.azul.com/azure-only/zulu/apt stable main"
sudo apt-get -q update
sudo apt-get -y install zulu-8-azure-jdk
```

Для Java 11 запустите:

```cli
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 0xB1998361219BD9C9
sudo apt-add-repository "deb http://repos.azul.com/azure-only/zulu/apt stable main"
sudo apt-get -q update
sudo apt-get -y install zulu-11-azure-jdk
```

Для Java 12 (предварительная версия) запустите:

```cli
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 0xB1998361219BD9C9
sudo apt-add-repository "deb http://repos.azul.com/azure-only/zulu/apt stable main"
sudo apt-get -q update
sudo apt-get -y install zulu-12-azure-jdk
```

**Чтобы обновить пакет Zulu JDK 8 из репозитория apt-get:**

```cli
sudo apt-get -q update
sudo apt-get -y install zulu-8-azure-jdk
```

Предыдущий выпуск будет автоматически удален.
(Измените номер версии в приведенной выше команде, если вы используете версии 11 или 12.)

**Чтобы удалить пакет Zulu JDK 8 из репозитория apt-get:**

```cli
sudo apt-get -y purge zulu-8-azure-jdk
```

(Измените номер версии в приведенной выше команде, если вы используете версии 11 или 12.)

Дополнительные сведения о подготовке, установке пакетов Azul Zulu JDK для разработки в Azure и об управлении ими см. в [официальных документах Zulu](https://docs.azul.com/zulu/zuludocs/index.htm).

