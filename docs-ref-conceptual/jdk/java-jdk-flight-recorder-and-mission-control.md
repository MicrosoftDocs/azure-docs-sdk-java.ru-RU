---
title: Инструмент Java Flight Recorder и сборка Mission Control
description: Руководство по использованию инструмента Java Flight Recorder и сборки Mission Control для сбора и просмотра данных приложения.
author: bmitchell287
manager: douge
ms.author: brendm
ms.date: 4/9/2019
ms.devlang: java
ms.topic: conceptual
ms.openlocfilehash: 64f64f2e5891fccf9d62510f39bd99d73457d590
ms.sourcegitcommit: f8faa4a14c714e148c513fd46f119524f3897abf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/03/2019
ms.locfileid: "67533625"
---
# <a name="use-java-flight-recorder-and-mission-control"></a><span data-ttu-id="19fcd-103">Использование Java Flight Recorder и Mission Control</span><span class="sxs-lookup"><span data-stu-id="19fcd-103">Use Java Flight Recorder and Mission Control</span></span>

<span data-ttu-id="19fcd-104">Zulu Mission Control — это полностью проверенная сборка JDK Mission Control, представленная с открытым кодом компанией Oracle в 2018 году. Управление сборкой осуществляется как управление проектом на базе OpenJDK.</span><span class="sxs-lookup"><span data-stu-id="19fcd-104">Zulu Mission Control is a fully-tested build of JDK Mission Control, which was open-sourced by Oracle in 2018 and is managed as a project under the OpenJDK umbrella.</span></span> <span data-ttu-id="19fcd-105">Java Flight Recorder (JFR) и Mission Control вместе предоставляют интерактивные возможности управления и мониторинга с минимальными затратами для рабочих нагрузок Java.</span><span class="sxs-lookup"><span data-stu-id="19fcd-105">Coupled with Java Flight Recorder (JFR), Mission Control delivers low-overhead, interactive monitoring and management capabilities for Java workloads.</span></span>

<span data-ttu-id="19fcd-106">Пакет Zulu Mission Control совместим со следующими пакетами Java Development Kit (JDK) и средами выполнения Java (JRE):</span><span class="sxs-lookup"><span data-stu-id="19fcd-106">Zulu Mission Control is compatible with the following Java Development Kits (JDKs) and Java Runtime Environments (JREs):</span></span>

* <span data-ttu-id="19fcd-107">Zulu 12.1 и более поздние версии;</span><span class="sxs-lookup"><span data-stu-id="19fcd-107">Zulu 12.1 and later</span></span>
* <span data-ttu-id="19fcd-108">Zulu 11.0 и более поздние версии;</span><span class="sxs-lookup"><span data-stu-id="19fcd-108">Zulu 11.0 and later</span></span>
* <span data-ttu-id="19fcd-109">Zulu 8u202 (8.36) и более поздние версии;</span><span class="sxs-lookup"><span data-stu-id="19fcd-109">Zulu 8u202 (8.36) and later</span></span>
* <span data-ttu-id="19fcd-110">Oracle OpenJDK 11 и 15 и более поздние версии</span><span class="sxs-lookup"><span data-stu-id="19fcd-110">Oracle OpenJDK 11 and 15 and later</span></span>
* <span data-ttu-id="19fcd-111">Oracle Java 11.0 и более поздние версии;</span><span class="sxs-lookup"><span data-stu-id="19fcd-111">Oracle Java 11.0 and later</span></span>
* <span data-ttu-id="19fcd-112">Oracle Java 8.0 и более поздние версии.</span><span class="sxs-lookup"><span data-stu-id="19fcd-112">Oracle Java 8.0 and later</span></span>

## <a name="install-zulu-mission-control-and-connect-to-a-jvm"></a><span data-ttu-id="19fcd-113">Установите Zulu Mission Control и подключитесь к виртуальной машине Java</span><span class="sxs-lookup"><span data-stu-id="19fcd-113">Install Zulu Mission Control and connect to a JVM</span></span>

<span data-ttu-id="19fcd-114">Чтобы установить Zulu Mission Control, подключиться к виртуальной машине Java (JVM) и получать представление обо всех аспектах запущенного приложения в режиме реального времени, выполните следующее.</span><span class="sxs-lookup"><span data-stu-id="19fcd-114">To install Zulu Mission Control, connect to a Java Virtual Machine (JVM), and gain real-time visibility into all aspects of a running application, do the following:</span></span>

1.  <span data-ttu-id="19fcd-115">[Установите экземпляры JDK и JRE, совместимые с Zulu Mission Control](java-jdk-install.md).</span><span class="sxs-lookup"><span data-stu-id="19fcd-115">[Install a Zulu Mission Control-compatible JDK and JRE](java-jdk-install.md).</span></span>

1.  <span data-ttu-id="19fcd-116">[Скачайте Zulu Mission Control](https://www.azul.com/products/zulu-mission-control/), выберите необходимую версию для системы, сохраните ее в локальном расположении и перейдите к этому каталогу.</span><span class="sxs-lookup"><span data-stu-id="19fcd-116">[Download Zulu Mission Control](https://www.azul.com/products/zulu-mission-control/), choose the appropriate version for your system, save it locally, and change to that directory.</span></span>

1.  <span data-ttu-id="19fcd-117">Разверните скачанный файл.</span><span class="sxs-lookup"><span data-stu-id="19fcd-117">Expand the downloaded file.</span></span>

    <span data-ttu-id="19fcd-118">**Linux:**</span><span class="sxs-lookup"><span data-stu-id="19fcd-118">**Linux:**</span></span>

    ```cli
    tar -xzvf zmc7.0.0-EA-linux_x64.tar.gz
    ```

    <span data-ttu-id="19fcd-119">**Windows:**</span><span class="sxs-lookup"><span data-stu-id="19fcd-119">**Windows:**</span></span>

    ```cli
    unzip -zxvf zmc7.0.0-EA-win_x64.zip 
    ```

    <span data-ttu-id="19fcd-120">**macOS:**</span><span class="sxs-lookup"><span data-stu-id="19fcd-120">**macOS:**</span></span>

    ```cli
    tar -xzvf zmc7.0.0-EA-macosx_x64.tar.gz
    ```

1.  <span data-ttu-id="19fcd-121">Запустите приложение Java с использованием одного из совместимых пакетов JDK.</span><span class="sxs-lookup"><span data-stu-id="19fcd-121">Start your Java application by using one of the compatible JDKs.</span></span> <span data-ttu-id="19fcd-122">Например:</span><span class="sxs-lookup"><span data-stu-id="19fcd-122">For example:</span></span>

    ```cli
    $JAVA_HOME/bin/java -jar MyApplication.jar
    ```

1.  <span data-ttu-id="19fcd-123">Запустите Zulu Mission Control.</span><span class="sxs-lookup"><span data-stu-id="19fcd-123">Start Zulu Mission Control.</span></span>

    <span data-ttu-id="19fcd-124">**Linux:**</span><span class="sxs-lookup"><span data-stu-id="19fcd-124">**Linux:**</span></span>

    ```cli
    zmc7.0.0-EA-linux_x64/zmc
    ```

    <span data-ttu-id="19fcd-125">**Windows:**</span><span class="sxs-lookup"><span data-stu-id="19fcd-125">**Windows:**</span></span>

    ```cli
    zmc7.0.0-EA-win_x64\zmc.exe 
    ```

    <span data-ttu-id="19fcd-126">**macOS:**</span><span class="sxs-lookup"><span data-stu-id="19fcd-126">**macOS:**</span></span>

    ```cli
    zmc7.0.0-EA-macosx_x64/Zulu\ Mission\ Control.app/Contents/MacOS/zmc
    ```

1.  <span data-ttu-id="19fcd-127">Измените установку JVM для Mission Control (необязательно).</span><span class="sxs-lookup"><span data-stu-id="19fcd-127">(Optional) Switch the JVM installation for Mission Control.</span></span>

    <span data-ttu-id="19fcd-128">На устройствах Windows *zmc.exe* использует установку виртуальной машины Java по умолчанию, заданную в реестре.</span><span class="sxs-lookup"><span data-stu-id="19fcd-128">On Windows devices, *zmc.exe* uses the default JVM installation that's configured in the registry.</span></span> <span data-ttu-id="19fcd-129">Zulu Mission Control необходимо запустить из полного JDK, чтобы иметь возможность автоматически обнаруживать локальные экземпляры JVM.</span><span class="sxs-lookup"><span data-stu-id="19fcd-129">Zulu Mission Control must be launched from a full JDK to be able to detect local JVM instances automatically.</span></span> <span data-ttu-id="19fcd-130">Если устанавливается JRE, виртуальная машина Java не будет обнаружена и на экране отобразится следующее предупреждение:</span><span class="sxs-lookup"><span data-stu-id="19fcd-130">If the installation is a JRE, no JVM will be detected, and you will receive the following warning:</span></span>

    > [!div class="mx-imgBorder"]
    <span data-ttu-id="19fcd-131">![Предупреждение для установки JDK только для JRE](../media/jdk/azul-jfr-1.png)</span><span class="sxs-lookup"><span data-stu-id="19fcd-131">![Warning if JDK installation is JRE-only](../media/jdk/azul-jfr-1.png)</span></span>

    <span data-ttu-id="19fcd-132">Чтобы изменить виртуальную машину Java, которая используется Mission Control, сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="19fcd-132">To change the JVM that's used by Mission Control, do the following:</span></span> 

    <span data-ttu-id="19fcd-133">a.</span><span class="sxs-lookup"><span data-stu-id="19fcd-133">a.</span></span> <span data-ttu-id="19fcd-134">Откройте файл конфигурации *zmc.ini*, который находится в той же папке, что и файл *zmc.exe*.</span><span class="sxs-lookup"><span data-stu-id="19fcd-134">Open the *zmc.ini* configuration file, which is in the same directory as the *zmc.exe* file.</span></span>

    <span data-ttu-id="19fcd-135">b.</span><span class="sxs-lookup"><span data-stu-id="19fcd-135">b.</span></span> <span data-ttu-id="19fcd-136">Добавьте две строки перед строкой `-vmargs`:</span><span class="sxs-lookup"><span data-stu-id="19fcd-136">Before the line `-vmargs`, add two lines:</span></span>  

       * <span data-ttu-id="19fcd-137">В первой строке введите `–vm`.</span><span class="sxs-lookup"><span data-stu-id="19fcd-137">On the first line, enter `–vm`.</span></span>  
       * <span data-ttu-id="19fcd-138">Во второй строке введите путь установки JDK (например, `C:\Program Files\Java\jdk1.8.0_212\bin\javaw.exe`).</span><span class="sxs-lookup"><span data-stu-id="19fcd-138">On the second line, enter the path to your JDK installation (for example, `C:\Program Files\Java\jdk1.8.0_212\bin\javaw.exe`).</span></span>

1.  <span data-ttu-id="19fcd-139">Найдите виртуальную машину Java, в которой выполняется приложение, сделав следующее.</span><span class="sxs-lookup"><span data-stu-id="19fcd-139">Locate the JVM that's running your application by doing the following:</span></span>

    <span data-ttu-id="19fcd-140">a.</span><span class="sxs-lookup"><span data-stu-id="19fcd-140">a.</span></span> <span data-ttu-id="19fcd-141">В левой части окна Zulu Mission Control выберите вкладку **JVM Browser** (Браузер виртуальной машины Java).</span><span class="sxs-lookup"><span data-stu-id="19fcd-141">In the left pane of the Zulu Mission Control window, select the **JVM Browser** tab.</span></span>

    <span data-ttu-id="19fcd-142">b.</span><span class="sxs-lookup"><span data-stu-id="19fcd-142">b.</span></span> <span data-ttu-id="19fcd-143">В списке выберите и разверните экземпляр виртуальной машины Java, в котором выполняется приложение.</span><span class="sxs-lookup"><span data-stu-id="19fcd-143">In the list, select and expand the JVM instance that's running your application.</span></span>

    ![Экземпляр виртуальной машины Java в раскрытом списке](../media/jdk/azul-jfr-2.png)


1.  <span data-ttu-id="19fcd-145">При необходимости начните запись с помощью инструмента Flight Recorder.</span><span class="sxs-lookup"><span data-stu-id="19fcd-145">Start a flight recording, if necessary.</span></span>

    <span data-ttu-id="19fcd-146">a.</span><span class="sxs-lookup"><span data-stu-id="19fcd-146">a.</span></span> <span data-ttu-id="19fcd-147">В области слева в разделе **Flight Recorder**, если отображается сообщение *No Recordings* (Нет записей), запустите операцию записи, щелкнув правой кнопкой мыши **Flight Recorder** и выбрав команду **Start Flight Recording** (Начать запись).</span><span class="sxs-lookup"><span data-stu-id="19fcd-147">In the left pane, under **Flight Recorder**, if a *No Recordings* message is displayed, start a recording by right-clicking **Flight Recorder** and then selecting **Start Flight Recording**.</span></span>

    <span data-ttu-id="19fcd-148">b.</span><span class="sxs-lookup"><span data-stu-id="19fcd-148">b.</span></span> <span data-ttu-id="19fcd-149">Выберите **Time fixed recording** (Запись с фиксированной продолжительностью) или **Continuous recording** (Непрерывная запись), а также (точную) конфигурацию **Profiling** (Профилирование) или конфигурацию (с меньшими общими расходами) **Continuous** (Непрерывная), а затем нажмите кнопку **Finish** (Готово).</span><span class="sxs-lookup"><span data-stu-id="19fcd-149">Select either **Time fixed recording** or **Continuous recording**, and either a **Profiling** configuration (fine-grained) or a **Continuous** configuration (lower overhead), and then select **Finish**.</span></span>

    ![Начало записи во время выполнения приложения](../media/jdk/azul-jfr-3.png)

    <span data-ttu-id="19fcd-151">Строка записи, осуществляемой во время выполнения приложения, должна отобразиться под строкой **Flight Recorder** на вкладке JVM Browser (Браузер JVM).</span><span class="sxs-lookup"><span data-stu-id="19fcd-151">A flight recording should appear below the **Flight Recorder** line in the JVM browser.</span></span>

1. <span data-ttu-id="19fcd-152">Создайте дамп записи, осуществляемой во время выполнения приложения.</span><span class="sxs-lookup"><span data-stu-id="19fcd-152">Dump the flight recording.</span></span> <span data-ttu-id="19fcd-153">Для этого щелкните правой кнопкой мыши строку, которая представляет во время выполнения приложения, а затем выберите команду **Dump whole recording** (Дамп всей записи).</span><span class="sxs-lookup"><span data-stu-id="19fcd-153">To do so, right-click the line that represents the flight recording, and then select **Dump whole recording**.</span></span>

    <span data-ttu-id="19fcd-154">Отобразится новая вкладка в большой области справа от окна Zulu Mission Control.</span><span class="sxs-lookup"><span data-stu-id="19fcd-154">A new tab appears in the large pane on the right side of the Zulu Mission Control window.</span></span> <span data-ttu-id="19fcd-155">Эта область представляет запись во время выполнения приложения, дамп которой создан из JVM, в которой запущено приложение.</span><span class="sxs-lookup"><span data-stu-id="19fcd-155">This pane represents the flight recording that was just dumped from the JVM that's running your application.</span></span>

1. <span data-ttu-id="19fcd-156">Проверьте запись, осуществляемую во время выполнения приложения, используя Zulu Mission Control.</span><span class="sxs-lookup"><span data-stu-id="19fcd-156">Examine the flight recording by using Zulu Mission Control.</span></span> <span data-ttu-id="19fcd-157">Чтобы сделать это, выберите вкладку **Outline** (Структура) в левой части окна Zulu Mission Control.</span><span class="sxs-lookup"><span data-stu-id="19fcd-157">To do so, select the **Outline** tab in the left pane of the Zulu Mission Control window.</span></span> <span data-ttu-id="19fcd-158">На этой вкладке отображаются различные представления данных, которые собираются в процессе записи.</span><span class="sxs-lookup"><span data-stu-id="19fcd-158">This tab displays various views of the data that's collected in the flight recording.</span></span>
 
    ![Просмотр записи, сделанной во время выполнения приложения](../media/jdk/azul-jfr-4.png)

## <a name="resources"></a><span data-ttu-id="19fcd-160">Ресурсы</span><span class="sxs-lookup"><span data-stu-id="19fcd-160">Resources</span></span>

<span data-ttu-id="19fcd-161">Дополнительные сведения см. на веб-сайте Azul Systems и вебинаре Azul: [ Open Source Flight Recorder and Mission Control - Managing and Measuring OpenJDK 8 Performance](https://www.azul.com/presentation/azul-webinar-open-source-flight-recorder-and-mission-control-managing-and-measuring-openjdk-8-performance/) (Инструменты с открытым исходным кодом Flight Recorder и Mission Control — управление OpenJDK 8 и оценка его производительности).</span><span class="sxs-lookup"><span data-stu-id="19fcd-161">To learn more, go to the Azul Systems site and view [Azul Webinar: Open Source Flight Recorder and Mission Control - Managing and Measuring OpenJDK 8 Performance](https://www.azul.com/presentation/azul-webinar-open-source-flight-recorder-and-mission-control-managing-and-measuring-openjdk-8-performance/).</span></span> <span data-ttu-id="19fcd-162">Это видео озвучено заместителем руководителя технологического отдела компании Azul Systems Саймоном Риттером (Simon Ritter).</span><span class="sxs-lookup"><span data-stu-id="19fcd-162">The video is narrated by Azul Systems Deputy CTO Simon Ritter.</span></span> <span data-ttu-id="19fcd-163">Обсуждение Flight Recorder начинается на отметке времени 31:30.</span><span class="sxs-lookup"><span data-stu-id="19fcd-163">The Flight Recorder discussion starts at 31:30.</span></span>

