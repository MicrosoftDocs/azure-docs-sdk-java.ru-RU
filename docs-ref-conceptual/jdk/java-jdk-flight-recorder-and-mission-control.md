---
title: Инструмент Java Flight Recorder и сборка Mission Control
description: Руководство по использованию инструмента Java Flight Recorder и сборки Mission Control для сбора и просмотра данных приложения.
author: bmitchell287
manager: douge
ms.author: brendm
ms.date: 4/9/2019
ms.devlang: java
ms.topic: conceptual
ms.openlocfilehash: b27e0f741f1322b7e8e1df363dbb2f40a3d34d53
ms.sourcegitcommit: 04cff6e3c6d3a9c15f7d88d5d3c238f0bdc787fd
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2019
ms.locfileid: "64568567"
---
# <a name="using-java-flight-recorder-jfr-and-mission-control"></a><span data-ttu-id="cc411-103">Использование инструмента Java Flight Recorder (JFR) и сборки Mission Control</span><span class="sxs-lookup"><span data-stu-id="cc411-103">Using Java Flight Recorder (JFR) and Mission Control</span></span>

<span data-ttu-id="cc411-104">Zulu Mission Control — это полностью проверенная сборка JDK Mission Control, представленная с открытым кодом компанией Oracle в 2018 году. Управление сборкой осуществляется как управление проектом на базе OpenJDK.</span><span class="sxs-lookup"><span data-stu-id="cc411-104">Zulu Mission Control is a fully-tested build of JDK Mission Control, which was open sourced by Oracle in 2018 and is managed as a project under the OpenJDK umbrella.</span></span> <span data-ttu-id="cc411-105">Flight Recorder и Mission Control вместе предоставляют интерактивные возможности управления и мониторинга с минимальными затратами для рабочих нагрузок Java.</span><span class="sxs-lookup"><span data-stu-id="cc411-105">Coupled with Flight Recorder, Mission Control delivers low-overhead, interactive monitoring and management capabilities for Java workloads.</span></span>

<span data-ttu-id="cc411-106">Сборка Zulu Mission Control совместима со следующими пакетами JDK и средами JRE:</span><span class="sxs-lookup"><span data-stu-id="cc411-106">Zulu Mission Control is compatible with the following JDKs/JREs:</span></span>

* <span data-ttu-id="cc411-107">Zulu 12.1 и более поздние версии;</span><span class="sxs-lookup"><span data-stu-id="cc411-107">Zulu 12.1 and later</span></span>
* <span data-ttu-id="cc411-108">Zulu 11.0 и более поздние версии;</span><span class="sxs-lookup"><span data-stu-id="cc411-108">Zulu 11.0 and later</span></span>
* <span data-ttu-id="cc411-109">Zulu 8u202 (8.36) и более поздние версии;</span><span class="sxs-lookup"><span data-stu-id="cc411-109">Zulu 8u202 (8.36) and later</span></span>
* <span data-ttu-id="cc411-110">Oracle OpenJDK 11+15 и более поздние версии;</span><span class="sxs-lookup"><span data-stu-id="cc411-110">Oracle OpenJDK 11+15 and later</span></span>
* <span data-ttu-id="cc411-111">Oracle Java 11.0 и более поздние версии;</span><span class="sxs-lookup"><span data-stu-id="cc411-111">Oracle Java 11.0 and later</span></span>
* <span data-ttu-id="cc411-112">Oracle Java 8.0 и более поздние версии.</span><span class="sxs-lookup"><span data-stu-id="cc411-112">Oracle Java 8.0 and later</span></span>

<span data-ttu-id="cc411-113">Выполните приведенные ниже действия, чтобы установить Zulu Mission Control, подключиться к виртуальной машине Java (JVM) и получать представление обо всех аспектах запущенного приложения в режиме реального времени.</span><span class="sxs-lookup"><span data-stu-id="cc411-113">Follow the steps below to install Zulu Mission Control, connect to a Java Virtual Machine (JVM), and gain real-time visibility into all aspects of a running application.</span></span>

1.  <span data-ttu-id="cc411-114">[Установите экземпляр JDK/JRE, совместимый с Zulu Mission Control](java-jdk-install.md).</span><span class="sxs-lookup"><span data-stu-id="cc411-114">[Install a Zulu Mission Control compatible JDK/JRE](java-jdk-install.md).</span></span>

2.  <span data-ttu-id="cc411-115">Скачайте Zulu Mission Control из [сайта загрузки Azul](https://www.azul.com/products/zulu-mission-control/), выберите необходимую версию для системы, сохраните ее в локальном расположении и перейдите к этому каталогу.</span><span class="sxs-lookup"><span data-stu-id="cc411-115">Download Zulu Mission Control from [the Azul download site](https://www.azul.com/products/zulu-mission-control/), choose the appropriate version for your system, save it locally, and change to that directory.</span></span>

3.  <span data-ttu-id="cc411-116">Разверните скачанный файл.</span><span class="sxs-lookup"><span data-stu-id="cc411-116">Expand the downloaded file.</span></span>

    <span data-ttu-id="cc411-117">**Linux:**</span><span class="sxs-lookup"><span data-stu-id="cc411-117">**Linux:**</span></span>

    ```cli
    tar -xzvf zmc7.0.0-EA-linux_x64.tar.gz
    ```

    <span data-ttu-id="cc411-118">**Windows:**</span><span class="sxs-lookup"><span data-stu-id="cc411-118">**Windows:**</span></span>

    ```cli
    unzip -zxvf zmc7.0.0-EA-win_x64.zip 
    ```

    <span data-ttu-id="cc411-119">**MacOS:**</span><span class="sxs-lookup"><span data-stu-id="cc411-119">**MacOS:**</span></span>

    ```cli
    tar -xzvf zmc7.0.0-EA-macosx_x64.tar.gz
    ```

4.  <span data-ttu-id="cc411-120">Запустите приложение Java с использованием одного из совместимых пакетов JDK.</span><span class="sxs-lookup"><span data-stu-id="cc411-120">Start your Java application using one of the compatible JDKs.</span></span> <span data-ttu-id="cc411-121">Например:</span><span class="sxs-lookup"><span data-stu-id="cc411-121">E.g.:</span></span>

    ```cli
    $JAVA_HOME/bin/java -jar MyApplication.jar
    ```

5.  <span data-ttu-id="cc411-122">Запустите Zulu Mission Control.</span><span class="sxs-lookup"><span data-stu-id="cc411-122">Start Zulu Mission Control</span></span>

    <span data-ttu-id="cc411-123">**Linux:**</span><span class="sxs-lookup"><span data-stu-id="cc411-123">**Linux:**</span></span>

    ```cli
    zmc7.0.0-EA-linux_x64/zmc
    ```

    <span data-ttu-id="cc411-124">**Windows:**</span><span class="sxs-lookup"><span data-stu-id="cc411-124">**Windows:**</span></span>

    ```cli
    zmc7.0.0-EA-win_x64\zmc.exe 
    ```

    <span data-ttu-id="cc411-125">**MacOS:**</span><span class="sxs-lookup"><span data-stu-id="cc411-125">**MacOS:**</span></span>

    ```cli
    zmc7.0.0-EA-macosx_x64/Zulu\ Mission\ Control.app/Contents/MacOS/zmc
    ```

6.  <span data-ttu-id="cc411-126">Измените установку JVM для Mission Control (необязательно).</span><span class="sxs-lookup"><span data-stu-id="cc411-126">Switch the JVM installation for Mission Control (Optional)</span></span>

    <span data-ttu-id="cc411-127">В Windows *zmc.exe* будет использовать установку JVM по умолчанию, настроенную в реестре.</span><span class="sxs-lookup"><span data-stu-id="cc411-127">On Windows, *zmc.exe* will use the default JVM installation configured in the registry.</span></span> <span data-ttu-id="cc411-128">Zulu Mission Control необходимо запустить из полного JDK, чтобы иметь возможность автоматически обнаруживать локальные экземпляры JVM.</span><span class="sxs-lookup"><span data-stu-id="cc411-128">Zulu Mission Control must be launched from a full JDK to be able to detect local JVM instances automatically.</span></span> <span data-ttu-id="cc411-129">Если это среда JRE, вы увидите следующее предупреждение:</span><span class="sxs-lookup"><span data-stu-id="cc411-129">If this is a JRE, you will see the warning below:</span></span>

    > [!div class="mx-imgBorder"]
    <span data-ttu-id="cc411-130">![Предупреждение, если установка JDK является только JRE](../media/jdk/azul-jfr-1.png)</span><span class="sxs-lookup"><span data-stu-id="cc411-130">![Warning if JDK install is JRE-only](../media/jdk/azul-jfr-1.png)</span></span>

    <span data-ttu-id="cc411-131">Чтобы изменить JVM, используемую сборкой Mission Control, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="cc411-131">To change the JVM used by Mission Control, follow these steps:</span></span> 
    1.  <span data-ttu-id="cc411-132">Откройте файл конфигурации *zmc.ini*, расположенный в том же каталоге, что и *zmc.exe*.</span><span class="sxs-lookup"><span data-stu-id="cc411-132">Open *zmc.ini* configuration file, located in the same directory as the *zmc.exe*</span></span>
    2.  <span data-ttu-id="cc411-133">Добавьте две строки перед строкой `-vmargs`:</span><span class="sxs-lookup"><span data-stu-id="cc411-133">Before the line `-vmargs`, add two lines:</span></span>
        * <span data-ttu-id="cc411-134">В первой строке напишите `–vm`.</span><span class="sxs-lookup"><span data-stu-id="cc411-134">On the first line, write `–vm`</span></span>
        * <span data-ttu-id="cc411-135">Во второй строке напишите путь к установке JDK.</span><span class="sxs-lookup"><span data-stu-id="cc411-135">On the second line, write the path to your JDK installation.</span></span> <span data-ttu-id="cc411-136">(Например, `C:\Program Files\Java\jdk1.8.0_212\bin\javaw.exe`).</span><span class="sxs-lookup"><span data-stu-id="cc411-136">(For example, `C:\Program Files\Java\jdk1.8.0_212\bin\javaw.exe`).</span></span>

7.  <span data-ttu-id="cc411-137">Найдите JVM, на которой запущено приложение.</span><span class="sxs-lookup"><span data-stu-id="cc411-137">Locate the JVM running your application</span></span>
    1.  <span data-ttu-id="cc411-138">В верхней левой панели окна Zulu Mission Control щелкните вкладку **JVM Browser** (Браузер JVM).</span><span class="sxs-lookup"><span data-stu-id="cc411-138">In the upper left pane of the Zulu Mission Control window click on the tab labelled **JVM Browser**.</span></span>
    2.  <span data-ttu-id="cc411-139">Выберите и разверните элемент списка в левом верхнем углу для экземпляра JVM, на котором запущено приложение.</span><span class="sxs-lookup"><span data-stu-id="cc411-139">Select and expand the list item in the upper left for your the JVM instance running your application.</span></span>

    > [!div class="mx-imgBorder"]
    <span data-ttu-id="cc411-140">![Развертывание элемента списка в левом верхнем углу для экземпляра JVM](../media/jdk/azul-jfr-2.png)</span><span class="sxs-lookup"><span data-stu-id="cc411-140">![Expand the list item in the upper-left for your JVM instance](../media/jdk/azul-jfr-2.png)</span></span>


8.  <span data-ttu-id="cc411-141">При необходимости начните запись с помощью инструмента Flight Recorder.</span><span class="sxs-lookup"><span data-stu-id="cc411-141">Start a Flight Recording, if necessary</span></span>
    1.  <span data-ttu-id="cc411-142">Если в Flight Recorder отображается No Recordings (Нет записей), начните запись. Для этого щелкните строку Flight Recorder правой кнопкой мыши на вкладке JVM Browser (Браузер JVM) и выберите **Start Flight Recording...** (Начать запись во время выполнения...).</span><span class="sxs-lookup"><span data-stu-id="cc411-142">If the Flight Recorder displays "No Recordings", start one by right-clicking on the Flight Recorder line in the JVM Browser tab and selecting **Start Flight Recording...**</span></span>
    2.  <span data-ttu-id="cc411-143">Выберите запись с фиксированной продолжительностью или непрерывную запись, а также конфигурацию профилирования (точную) или непрерывную конфигурацию (меньшие общие расходы), а затем нажмите кнопку **Finish** (Готово).</span><span class="sxs-lookup"><span data-stu-id="cc411-143">Select either a fixed duration recording or a continuous recording, and either a Profiling configuration (fine-grained) or a Continuous configuration (lower overhead), then click **Finish**.</span></span>

    > [!div class="mx-imgBorder"]
    <span data-ttu-id="cc411-144">![Начало записи во время выполнения приложения](../media/jdk/azul-jfr-3.png)</span><span class="sxs-lookup"><span data-stu-id="cc411-144">![Start a Flight Recording](../media/jdk/azul-jfr-3.png)</span></span>

9.  <span data-ttu-id="cc411-145">Создайте дамп записи, осуществляемой во время выполнения приложения.</span><span class="sxs-lookup"><span data-stu-id="cc411-145">Dump the Flight Recording</span></span>
    1.  <span data-ttu-id="cc411-146">Строка записи, осуществляемой во время выполнения приложения, должна отобразиться под строкой Flight Recorder на вкладке JVM Browser (Браузер JVM).</span><span class="sxs-lookup"><span data-stu-id="cc411-146">A Flight Recording should appear below the Flight Recorder line in the JVM Browser.</span></span> <span data-ttu-id="cc411-147">Щелкните правой кнопкой мыши строку с записью, осуществляемой во время выполнения приложения, и выберите **Dump whole recording** (Создать дамп всей записи).</span><span class="sxs-lookup"><span data-stu-id="cc411-147">Right-click on the line representing the Flight Recording and select **Dump whole recording**.</span></span>
    2.  <span data-ttu-id="cc411-148">Отобразится новая вкладка в большой области справа от окна Zulu Mission Control.</span><span class="sxs-lookup"><span data-stu-id="cc411-148">A new tab will appear in the large pane on the right side of the Zulu Mission Control window.</span></span> <span data-ttu-id="cc411-149">Эта область представляет запись, осуществляемую во время выполнения приложения, дамп которой создан из JVM, на которой запущено приложение.</span><span class="sxs-lookup"><span data-stu-id="cc411-149">This pane represents the Flight Recording just dumped from the JVM running your application.</span></span>

10. <span data-ttu-id="cc411-150">Проверьте запись, осуществляемую во время выполнения приложения, используя Zulu Mission Control.</span><span class="sxs-lookup"><span data-stu-id="cc411-150">Examine the Flight Recording using Zulu Mission Control</span></span>
    1.  <span data-ttu-id="cc411-151">Если активация еще не выполнена, выберите вкладку **Outline** (Структура) в левой области окна Zulu Mission Control.</span><span class="sxs-lookup"><span data-stu-id="cc411-151">If not already activated, select the tab labelled **Outline** in the left pane of the Zulu Mission Control Window.</span></span> <span data-ttu-id="cc411-152">Эта вкладка содержит различные представления данных, собранных в рамках записи, осуществляемой во время выполнения приложения.</span><span class="sxs-lookup"><span data-stu-id="cc411-152">This tab contains different views of the data collected in the Flight Recording.</span></span>
 
    > [!div class="mx-imgBorder"]
    <span data-ttu-id="cc411-153">![Просмотр записи во время выполнения программы](../media/jdk/azul-jfr-4.png)</span><span class="sxs-lookup"><span data-stu-id="cc411-153">![Review the Fliight Recording](../media/jdk/azul-jfr-4.png)</span></span>

## <a name="resources"></a><span data-ttu-id="cc411-154">Ресурсы</span><span class="sxs-lookup"><span data-stu-id="cc411-154">Resources</span></span>

<span data-ttu-id="cc411-155">Кроме того, мы приготовили [демонстрационное видео](https://www.azul.com/presentation/azul-webinar-open-source-flight-recorder-and-mission-control-managing-and-measuring-openjdk-8-performance/), комментируемое техническим директором Azul Systems Саймоном Риттером (Simon Ritter).</span><span class="sxs-lookup"><span data-stu-id="cc411-155">We have also prepared a [demonstration video](https://www.azul.com/presentation/azul-webinar-open-source-flight-recorder-and-mission-control-managing-and-measuring-openjdk-8-performance/) narrated by Azul Systems Deputy CTO Simon Ritter.</span></span> <span data-ttu-id="cc411-156">В этом видео описывается настройка и установка Flight Recorder и Zulu Mission Control.</span><span class="sxs-lookup"><span data-stu-id="cc411-156">The video walks you through the configuration and setup of both Flight Recorder and Zulu Mission Control.</span></span> <span data-ttu-id="cc411-157">Обсуждение Flight Recorder начинается на отметке времени 31:30.</span><span class="sxs-lookup"><span data-stu-id="cc411-157">The Flight Recorder discussion starts at 31:30.</span></span>

