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
# <a name="install-the-jdk-for-azure-and-azure-stack"></a><span data-ttu-id="36d69-103">Установка JDK для Azure и Azure Stack</span><span class="sxs-lookup"><span data-stu-id="36d69-103">Install the JDK for Azure and Azure Stack</span></span>

<span data-ttu-id="36d69-104">Сборка OpenJDK типа Azul Zulu Enterprise — это бесплатный мультиплатформенный, готовый дистрибутив OpenJDK для Azure и Azure Stack, который поддерживается корпорацией Майкрософт и Azul Systems.</span><span class="sxs-lookup"><span data-stu-id="36d69-104">Azul Zulu Enterprise builds of OpenJDK are a no-cost, multi-platform, production-ready distribution of the OpenJDK for Azure and Azure Stack backed by Microsoft and Azul Systems.</span></span> <span data-ttu-id="36d69-105">Они содержат все компоненты для сборки и запуска приложений Java SE.</span><span class="sxs-lookup"><span data-stu-id="36d69-105">They contain all the components for building and running Java SE applications.</span></span>

<span data-ttu-id="36d69-106">Существует [несколько типов пакетов для скачивания, поддерживаемых для каждой клиентской ОС](https://www.azul.com/downloads/azure-only/zulu/).</span><span class="sxs-lookup"><span data-stu-id="36d69-106">There are [multiple download package types supported for each client OS](https://www.azul.com/downloads/azure-only/zulu/).</span></span> <span data-ttu-id="36d69-107">Вы также можете получить образ виртуальной машины из коллекции Azure Marketplace для следующих платформ:</span><span class="sxs-lookup"><span data-stu-id="36d69-107">You can also get a virtual machine image from the Azure Marketplace Gallery for the following platforms:</span></span>

  * [<span data-ttu-id="36d69-108">Azul Zulu: Java 8 на Ubuntu 18.04</span><span class="sxs-lookup"><span data-stu-id="36d69-108">Azul Zulu: Java 8 on Ubuntu 18.04</span></span>](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/azul.azul-zulu8-ubuntu-1804)
  * [<span data-ttu-id="36d69-109">Azul Zulu: Java 8 на Windows Server 2019</span><span class="sxs-lookup"><span data-stu-id="36d69-109">Azul Zulu: Java 8 on Windows Server 2019</span></span>](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/azul.azul-zulu8-windows-2019)
  
  * [<span data-ttu-id="36d69-110">Azul Zulu: Java 11 на Ubuntu 18.04</span><span class="sxs-lookup"><span data-stu-id="36d69-110">Azul Zulu: Java 11 on Ubuntu 18.04</span></span>](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/azul.azul-zulu11-ubuntu-1804)
  * [<span data-ttu-id="36d69-111">Azul Zulu: Java 11 на Windows Server 2019</span><span class="sxs-lookup"><span data-stu-id="36d69-111">Azul Zulu: Java 11 on Windows Server 2019</span></span>](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/azul.azul-zulu11-windows-2019)


> [!NOTE]
> <span data-ttu-id="36d69-112">Эти инструкции предназначены для 64-разрядной версии Java 8 JDK.</span><span class="sxs-lookup"><span data-stu-id="36d69-112">These instructions target the 64-bit Java 8 version of the JDK.</span></span> <span data-ttu-id="36d69-113">Azul также предоставляет среду выполнения Java (JRE) в виде автономной установки.</span><span class="sxs-lookup"><span data-stu-id="36d69-113">Azul also provides the Java Run-time Environment (JRE) as a stand-alone installation.</span></span> <span data-ttu-id="36d69-114">JRE входит в состав установки JDK.</span><span class="sxs-lookup"><span data-stu-id="36d69-114">The JRE is included with the JDK install.</span></span>
>
>  <span data-ttu-id="36d69-115">Пакеты Java 11 также предоставляются на [странице загрузки Azure на сайте Azul](https://www.azul.com/downloads/azure-only/zulu/).</span><span class="sxs-lookup"><span data-stu-id="36d69-115">Java 11 packages are also provided on [Azul's Azure downloads page](https://www.azul.com/downloads/azure-only/zulu/).</span></span>

## <a name="download-and-install-the-azul-zulu-jdks-for-windows"></a><span data-ttu-id="36d69-116">Скачивание и установка пакетов Azul Zulu JDK для Windows</span><span class="sxs-lookup"><span data-stu-id="36d69-116">Download and install the Azul Zulu JDKs for Windows</span></span> 

1. <span data-ttu-id="36d69-117">[Скачайте 64-разрядный пакет Azul Zulu JDK 8 как MSI-файл](https://repos.azul.com/azure-only/zulu/packages/zulu-11/11.0.3/zulu-11-azure-jdk_11.31.11-11.0.3-win_x64.msi) в расположение на клиенте, например `C:\Users\<your_login>\Downloads`.</span><span class="sxs-lookup"><span data-stu-id="36d69-117">[Download the 64-bit Azul Zulu JDK 8 as an MSI](https://repos.azul.com/azure-only/zulu/packages/zulu-11/11.0.3/zulu-11-azure-jdk_11.31.11-11.0.3-win_x64.msi) to a location on your client, such as `C:\Users\<your_login>\Downloads`.</span></span> <span data-ttu-id="36d69-118">(Пакеты ZIP также предоставляются на [странице загрузки Azure на сайте Azul](https://www.azul.com/downloads/azure-only/zulu/).)</span><span class="sxs-lookup"><span data-stu-id="36d69-118">(.ZIP packages are also provided on [Azul's Azure downloads page](https://www.azul.com/downloads/azure-only/zulu/).)</span></span>

2. <span data-ttu-id="36d69-119">Перейдите в каталог и дважды щелкните скачанный MSI-файл, чтобы начать установку.</span><span class="sxs-lookup"><span data-stu-id="36d69-119">Navigate to the directory and double-click the downloaded MSI file to begin installation.</span></span>

## <a name="download-and-install-the-azul-zulu-jdks-for-mac"></a><span data-ttu-id="36d69-120">Скачивание и установка пакетов Azul Zulu JDK для Mac</span><span class="sxs-lookup"><span data-stu-id="36d69-120">Download and install the Azul Zulu JDKs for Mac</span></span> 

<span data-ttu-id="36d69-121">По приведенной ниже ссылке можно скачать ZIP-файл на компьютер Mac.</span><span class="sxs-lookup"><span data-stu-id="36d69-121">These steps download a ZIP file to your Mac.</span></span> <span data-ttu-id="36d69-122">Доступна также версия DMG.</span><span class="sxs-lookup"><span data-stu-id="36d69-122">There is also a DMG version available.</span></span>

1. <span data-ttu-id="36d69-123">[Скачайте 64-разрядный пакет Azul Zulu JDK 8 как ZIP-файл](https://repos.azul.com/azure-only/zulu/packages/zulu-11/11.0.3/zulu-11-azure-jdk_11.31.11-11.0.3-macosx_x64.zip) в расположение на клиенте, например `/Library/Java/JavaVirtualMachines/`.</span><span class="sxs-lookup"><span data-stu-id="36d69-123">[Download the 64-bit Azul Zulu JDK 8 as a ZIP file](https://repos.azul.com/azure-only/zulu/packages/zulu-11/11.0.3/zulu-11-azure-jdk_11.31.11-11.0.3-macosx_x64.zip) to a location on your client, such as `/Library/Java/JavaVirtualMachines/`.</span></span> <span data-ttu-id="36d69-124">(Пакеты DMG также предоставляются на [странице загрузки Azure на сайте Azul](https://www.azul.com/downloads/azure-only/zulu/).)</span><span class="sxs-lookup"><span data-stu-id="36d69-124">(.DMG packages are also provided on [Azul's Azure downloads page](https://www.azul.com/downloads/azure-only/zulu/).)</span></span>

2. <span data-ttu-id="36d69-125">Запустите Finder, перейдите в каталог скачивания и дважды щелкните ZIP-файл.</span><span class="sxs-lookup"><span data-stu-id="36d69-125">Launch Finder, navigate to the download directory, and double-click the ZIP file.</span></span> <span data-ttu-id="36d69-126">Кроме того, вы можете запустить окно команды терминала, перейти в каталог и запустить:</span><span class="sxs-lookup"><span data-stu-id="36d69-126">Alternatively, you can launch a terminal command window, navigate to the directory, and run:</span></span>

```cli
unzip <name_of_zulu_package>.zip
```

## <a name="download-and-install-the-azul-zulu-jdks-for-alpine-linux"></a><span data-ttu-id="36d69-127">Скачивание и установка пакетов Azul Zulu JDK для Alpine Linux</span><span class="sxs-lookup"><span data-stu-id="36d69-127">Download and install the Azul Zulu JDKs for Alpine Linux</span></span>

1. <span data-ttu-id="36d69-128">[Скачайте 64-разрядный пакет Azul Zulu JDK 8 как TAR-файл](https://repos.azul.com/azure-only/zulu/packages/zulu-11/11.0.3/zulu-11-azure-jdk_11.31.11-11.0.3-linux_x64.tar.gz) в расположение на клиенте, например `/usr/lib/jvm`.</span><span class="sxs-lookup"><span data-stu-id="36d69-128">[Download the 64-bit Azul Zulu JDK 8 as a TAR file](https://repos.azul.com/azure-only/zulu/packages/zulu-11/11.0.3/zulu-11-azure-jdk_11.31.11-11.0.3-linux_x64.tar.gz) to a location on your client, such as `/usr/lib/jvm`.</span></span> <span data-ttu-id="36d69-129">(Пакеты RPM и DEB также предоставляются на [странице загрузки Azure на сайте Azul](https://www.azul.com/downloads/azure-only/zulu/).)</span><span class="sxs-lookup"><span data-stu-id="36d69-129">(.RPM and .DEB packages are also provided on [Azul's Azure downloads page](https://www.azul.com/downloads/azure-only/zulu/).)</span></span>

2. <span data-ttu-id="36d69-130">Перейдите в каталог и запустите следующую команду, чтобы распаковать и развернуть файл:</span><span class="sxs-lookup"><span data-stu-id="36d69-130">Go to your directory and run the following command to unzip and expand the file:</span></span>

    ```cli
    tar -xvf <name_of_zulu_package>.tar
    ```

## <a name="confirm-your-installation"></a><span data-ttu-id="36d69-131">Подтверждение установки</span><span class="sxs-lookup"><span data-stu-id="36d69-131">Confirm your installation</span></span>

<span data-ttu-id="36d69-132">Чтобы подтвердить установку, перейдите в командную строку и запустите команду `java -version`.</span><span class="sxs-lookup"><span data-stu-id="36d69-132">To confirm your installation, go to the command-line and run `java -version`.</span></span>

<span data-ttu-id="36d69-133">Результат выполнения команды должен выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="36d69-133">The output of the command should be:</span></span>

```cli
$ java -version

openjdk version "1.8.0_212"
OpenJDK Runtime Environment (Zulu 8.38.0.13-macosx)-Microsoft-Azure-restricted (build 1.8.0_212-b04)
OpenJDK 64-Bit Server VM (Zulu 8.38.0.13-macosx)-Microsoft-Azure-restricted (build 25.212-b04, mixed mode)

```

## <a name="download-and-install-the-azul-zulu-jdks-from-a-yum-repository"></a><span data-ttu-id="36d69-134">Скачивание и установка пакетов Azul Zulu JDK из репозитория Yum</span><span class="sxs-lookup"><span data-stu-id="36d69-134">Download and install the Azul Zulu JDKs from a Yum repository</span></span>

<span data-ttu-id="36d69-135">Azul размещает пакеты Azul Zulu JDK в [репозитории Yum](http://repos.azul.com/azure-only/zulu-azure.repo).</span><span class="sxs-lookup"><span data-stu-id="36d69-135">The Azul Zulu JDKs are provided in a [Yum repository](http://repos.azul.com/azure-only/zulu-azure.repo) by Azul.</span></span>

<span data-ttu-id="36d69-136">**Чтобы установить пакет Azul Zulu JDK для Java 8, запустите следующие команды из CLI:**</span><span class="sxs-lookup"><span data-stu-id="36d69-136">**To install the Azul Zulu JDK for Java 8, run the following commands from your CLI:**</span></span>

```cli
sudo rpm --import http://repos.azul.com/azul-repo.key
sudo curl http://repos.azul.com/azure-only/zulu-azure.repo -o /etc/yum.repos.d/zulu-azure.repo
sudo yum -q -y update
sudo yum -q -y install zulu-8-azure-jdk
```

<span data-ttu-id="36d69-137">Для Java 11 запустите:</span><span class="sxs-lookup"><span data-stu-id="36d69-137">For Java 11, run:</span></span>

```cli
sudo rpm --import http://repos.azul.com/azul-repo.key
sudo curl http://repos.azul.com/azure-only/zulu-azure.repo -o /etc/yum.repos.d/zulu-azure.repo
sudo yum -q -y update
sudo yum -q -y install zulu-11-azure-jdk
```

<span data-ttu-id="36d69-138">Для Java 12 (предварительная версия) запустите:</span><span class="sxs-lookup"><span data-stu-id="36d69-138">For Java 12 (Preview), run:</span></span>

```cli
sudo rpm --import http://repos.azul.com/azul-repo.key
sudo curl http://repos.azul.com/azure-only/zulu-azure.repo -o /etc/yum.repos.d/zulu-azure.repo
sudo yum -q -y update
sudo yum -q -y install zulu-12-azure-jdk
```

<span data-ttu-id="36d69-139">**Чтобы обновить пакет Zulu JDK 8 из репозитория Yum:**</span><span class="sxs-lookup"><span data-stu-id="36d69-139">**To update a Zulu JDK 8 package from a Yum repository:**</span></span>

```cli
sudo yum -q -y install zulu-8-azure-jdk
```

<span data-ttu-id="36d69-140">(Измените номер версии в приведенной выше команде, если вы используете версии 11 или 12.)</span><span class="sxs-lookup"><span data-stu-id="36d69-140">(Change the version number in the command above if you are using versions 11 or 12.)</span></span>

<span data-ttu-id="36d69-141">**Чтобы удалить пакет Zulu JDK 8 из репозитория Yum:**</span><span class="sxs-lookup"><span data-stu-id="36d69-141">**To remove a Zulu JDK 8 package from a Yum repository:**</span></span>

```cli
sudo yum -y erase zulu-8-azure-jdk
```
<span data-ttu-id="36d69-142">(Измените номер версии в приведенной выше команде, если вы используете версии 11 или 12.)</span><span class="sxs-lookup"><span data-stu-id="36d69-142">(Change the version number in the command above if you are using versions 11 or 12.)</span></span>

## <a name="download-and-install-the-azul-zulu-jdks-from-an-apt-get-repository"></a><span data-ttu-id="36d69-143">Скачивание и установка пакетов Azul Zulu JDK из репозитория apt-get</span><span class="sxs-lookup"><span data-stu-id="36d69-143">Download and install the Azul Zulu JDKs from an apt-get repository</span></span>

<span data-ttu-id="36d69-144">Azul также размещает пакеты Azul Zulu JDK в [репозитории apt-get](http://repos.azul.com/azure-only/zulu/apt).</span><span class="sxs-lookup"><span data-stu-id="36d69-144">The Azul Zulu JDKs are also provided in an [apt-get repository](http://repos.azul.com/azure-only/zulu/apt) by Azul.</span></span>

<span data-ttu-id="36d69-145">**Чтобы установить пакет Azul Zulu JDK для Java 8 из репозитория apt-get, запустите следующие команды из CLI:**</span><span class="sxs-lookup"><span data-stu-id="36d69-145">**To install the Azul Zulu JDK for Java 8 with apt-get, run the following commands from your CLI:**</span></span>

```cli
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 0xB1998361219BD9C9
sudo apt-add-repository "deb http://repos.azul.com/azure-only/zulu/apt stable main"
sudo apt-get -q update
sudo apt-get -y install zulu-8-azure-jdk
```

<span data-ttu-id="36d69-146">Для Java 11 запустите:</span><span class="sxs-lookup"><span data-stu-id="36d69-146">For Java 11, run:</span></span>

```cli
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 0xB1998361219BD9C9
sudo apt-add-repository "deb http://repos.azul.com/azure-only/zulu/apt stable main"
sudo apt-get -q update
sudo apt-get -y install zulu-11-azure-jdk
```

<span data-ttu-id="36d69-147">Для Java 12 (предварительная версия) запустите:</span><span class="sxs-lookup"><span data-stu-id="36d69-147">For Java 12 (Preview), run:</span></span>

```cli
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 0xB1998361219BD9C9
sudo apt-add-repository "deb http://repos.azul.com/azure-only/zulu/apt stable main"
sudo apt-get -q update
sudo apt-get -y install zulu-12-azure-jdk
```

<span data-ttu-id="36d69-148">**Чтобы обновить пакет Zulu JDK 8 из репозитория apt-get:**</span><span class="sxs-lookup"><span data-stu-id="36d69-148">**To update a Zulu JDK 8 package from an apt-get repository:**</span></span>

```cli
sudo apt-get -q update
sudo apt-get -y install zulu-8-azure-jdk
```

<span data-ttu-id="36d69-149">Предыдущий выпуск будет автоматически удален.</span><span class="sxs-lookup"><span data-stu-id="36d69-149">The previous release will be automatically removed.</span></span>
<span data-ttu-id="36d69-150">(Измените номер версии в приведенной выше команде, если вы используете версии 11 или 12.)</span><span class="sxs-lookup"><span data-stu-id="36d69-150">(Change the version number in the command above if you are using versions 11 or 12.)</span></span>

<span data-ttu-id="36d69-151">**Чтобы удалить пакет Zulu JDK 8 из репозитория apt-get:**</span><span class="sxs-lookup"><span data-stu-id="36d69-151">**To remove a Zulu JDK 8 package from an apt-get repository:**</span></span>

```cli
sudo apt-get -y purge zulu-8-azure-jdk
```

<span data-ttu-id="36d69-152">(Измените номер версии в приведенной выше команде, если вы используете версии 11 или 12.)</span><span class="sxs-lookup"><span data-stu-id="36d69-152">(Change the version number in the command above if you are using versions 11 or 12.)</span></span>

<span data-ttu-id="36d69-153">Дополнительные сведения о подготовке, установке пакетов Azul Zulu JDK для разработки в Azure и об управлении ими см. в [официальных документах Zulu](https://docs.azul.com/zulu/zuludocs/index.htm).</span><span class="sxs-lookup"><span data-stu-id="36d69-153">For more detailed guidance on preparing, installing, and managing your Azul Zulu JDKs for Azure development, read [the official Zulu docs](https://docs.azul.com/zulu/zuludocs/index.htm).</span></span>

