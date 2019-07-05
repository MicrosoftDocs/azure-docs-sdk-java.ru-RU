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
# <a name="use-java-flight-recorder-and-mission-control"></a>Использование Java Flight Recorder и Mission Control

Zulu Mission Control — это полностью проверенная сборка JDK Mission Control, представленная с открытым кодом компанией Oracle в 2018 году. Управление сборкой осуществляется как управление проектом на базе OpenJDK. Java Flight Recorder (JFR) и Mission Control вместе предоставляют интерактивные возможности управления и мониторинга с минимальными затратами для рабочих нагрузок Java.

Пакет Zulu Mission Control совместим со следующими пакетами Java Development Kit (JDK) и средами выполнения Java (JRE):

* Zulu 12.1 и более поздние версии;
* Zulu 11.0 и более поздние версии;
* Zulu 8u202 (8.36) и более поздние версии;
* Oracle OpenJDK 11 и 15 и более поздние версии
* Oracle Java 11.0 и более поздние версии;
* Oracle Java 8.0 и более поздние версии.

## <a name="install-zulu-mission-control-and-connect-to-a-jvm"></a>Установите Zulu Mission Control и подключитесь к виртуальной машине Java

Чтобы установить Zulu Mission Control, подключиться к виртуальной машине Java (JVM) и получать представление обо всех аспектах запущенного приложения в режиме реального времени, выполните следующее.

1.  [Установите экземпляры JDK и JRE, совместимые с Zulu Mission Control](java-jdk-install.md).

1.  [Скачайте Zulu Mission Control](https://www.azul.com/products/zulu-mission-control/), выберите необходимую версию для системы, сохраните ее в локальном расположении и перейдите к этому каталогу.

1.  Разверните скачанный файл.

    **Linux:**

    ```cli
    tar -xzvf zmc7.0.0-EA-linux_x64.tar.gz
    ```

    **Windows:**

    ```cli
    unzip -zxvf zmc7.0.0-EA-win_x64.zip 
    ```

    **macOS:**

    ```cli
    tar -xzvf zmc7.0.0-EA-macosx_x64.tar.gz
    ```

1.  Запустите приложение Java с использованием одного из совместимых пакетов JDK. Например:

    ```cli
    $JAVA_HOME/bin/java -jar MyApplication.jar
    ```

1.  Запустите Zulu Mission Control.

    **Linux:**

    ```cli
    zmc7.0.0-EA-linux_x64/zmc
    ```

    **Windows:**

    ```cli
    zmc7.0.0-EA-win_x64\zmc.exe 
    ```

    **macOS:**

    ```cli
    zmc7.0.0-EA-macosx_x64/Zulu\ Mission\ Control.app/Contents/MacOS/zmc
    ```

1.  Измените установку JVM для Mission Control (необязательно).

    На устройствах Windows *zmc.exe* использует установку виртуальной машины Java по умолчанию, заданную в реестре. Zulu Mission Control необходимо запустить из полного JDK, чтобы иметь возможность автоматически обнаруживать локальные экземпляры JVM. Если устанавливается JRE, виртуальная машина Java не будет обнаружена и на экране отобразится следующее предупреждение:

    > [!div class="mx-imgBorder"]
    ![Предупреждение для установки JDK только для JRE](../media/jdk/azul-jfr-1.png)

    Чтобы изменить виртуальную машину Java, которая используется Mission Control, сделайте следующее. 

    a. Откройте файл конфигурации *zmc.ini*, который находится в той же папке, что и файл *zmc.exe*.

    b. Добавьте две строки перед строкой `-vmargs`:  

       * В первой строке введите `–vm`.  
       * Во второй строке введите путь установки JDK (например, `C:\Program Files\Java\jdk1.8.0_212\bin\javaw.exe`).

1.  Найдите виртуальную машину Java, в которой выполняется приложение, сделав следующее.

    a. В левой части окна Zulu Mission Control выберите вкладку **JVM Browser** (Браузер виртуальной машины Java).

    b. В списке выберите и разверните экземпляр виртуальной машины Java, в котором выполняется приложение.

    ![Экземпляр виртуальной машины Java в раскрытом списке](../media/jdk/azul-jfr-2.png)


1.  При необходимости начните запись с помощью инструмента Flight Recorder.

    a. В области слева в разделе **Flight Recorder**, если отображается сообщение *No Recordings* (Нет записей), запустите операцию записи, щелкнув правой кнопкой мыши **Flight Recorder** и выбрав команду **Start Flight Recording** (Начать запись).

    b. Выберите **Time fixed recording** (Запись с фиксированной продолжительностью) или **Continuous recording** (Непрерывная запись), а также (точную) конфигурацию **Profiling** (Профилирование) или конфигурацию (с меньшими общими расходами) **Continuous** (Непрерывная), а затем нажмите кнопку **Finish** (Готово).

    ![Начало записи во время выполнения приложения](../media/jdk/azul-jfr-3.png)

    Строка записи, осуществляемой во время выполнения приложения, должна отобразиться под строкой **Flight Recorder** на вкладке JVM Browser (Браузер JVM).

1. Создайте дамп записи, осуществляемой во время выполнения приложения. Для этого щелкните правой кнопкой мыши строку, которая представляет во время выполнения приложения, а затем выберите команду **Dump whole recording** (Дамп всей записи).

    Отобразится новая вкладка в большой области справа от окна Zulu Mission Control. Эта область представляет запись во время выполнения приложения, дамп которой создан из JVM, в которой запущено приложение.

1. Проверьте запись, осуществляемую во время выполнения приложения, используя Zulu Mission Control. Чтобы сделать это, выберите вкладку **Outline** (Структура) в левой части окна Zulu Mission Control. На этой вкладке отображаются различные представления данных, которые собираются в процессе записи.
 
    ![Просмотр записи, сделанной во время выполнения приложения](../media/jdk/azul-jfr-4.png)

## <a name="resources"></a>Ресурсы

Дополнительные сведения см. на веб-сайте Azul Systems и вебинаре Azul: [ Open Source Flight Recorder and Mission Control - Managing and Measuring OpenJDK 8 Performance](https://www.azul.com/presentation/azul-webinar-open-source-flight-recorder-and-mission-control-managing-and-measuring-openjdk-8-performance/) (Инструменты с открытым исходным кодом Flight Recorder и Mission Control — управление OpenJDK 8 и оценка его производительности). Это видео озвучено заместителем руководителя технологического отдела компании Azul Systems Саймоном Риттером (Simon Ritter). Обсуждение Flight Recorder начинается на отметке времени 31:30.

