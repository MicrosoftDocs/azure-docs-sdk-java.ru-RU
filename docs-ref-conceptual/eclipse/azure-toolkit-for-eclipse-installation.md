---
title: "Установка набора средств Azure для Eclipse"
description: "Узнайте, как установить набор средств Azure для Eclipse."
services: 
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
ms.assetid: 9e93ff6a-f42b-4d99-b55b-624136b4a730
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 09/11/2017
ms.author: robmcm
ms.openlocfilehash: 59a8bfb6ab4db8ea8c6c9025ca3ced8a13192628
ms.sourcegitcommit: 256044d7cbce16dcb8dc4e195d0f63c10cb44d4e
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/13/2017
---
# <a name="installing-the-azure-toolkit-for-eclipse"></a>Установка набора средств Azure для Eclipse

В набор средств Azure для Eclipse входят шаблоны и функциональные возможности для простого создания, разработки, тестирования и развертывания приложений Azure с помощью среды разработки Eclipse. Набор средств Azure для Eclipse является проектом с открытым кодом. Исходный код доступен по лицензии MIT по адресу: <https://github.com/microsoft/azure-tools-for-java>.

Ниже приведен процесс установки набора средств Azure для Eclipse.

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="to-install-the-azure-toolkit-for-eclipse"></a>Установка набора средств Azure для Eclipse

1. Запустите Eclipse.

1. Щелкните меню **Help** (Справка) и выберите пункт **Install New Software** (Установить новое программное обеспечение), как показано на следующем рисунке.
   
   ![Установка набора средств Azure для Eclipse][01]

1. В диалоговом окне **Available Software** (Доступное программное обеспечение) в текстовом поле **Work with** (Работа с) введите `http://dl.microsoft.com/eclipse/` и нажмите клавишу **ВВОД**.

1. В области **Name** (Имя) установите флажок **Azure Toolkit for Eclipse** (Набор средств Azure для Eclipse) и снимите флажок **Contact all update sites during install to find required software** (Проверить все сайты обновления во время установки для поиска требуемого ПО). Экран должен выглядеть следующим образом:
   
   ![Установка набора средств Azure для Eclipse][02]

1. Если вы развернете узел **Набор средств Azure для Eclipse**, вы увидите следующие элементы:
   
   * **Application Insights Plugin for Java**(Подключаемый модуль Application Insights для Java) — этот компонент позволяет использовать службы регистрации и анализа телеметрии Azure для приложений и экземпляров серверов.
   * **Фильтр служб контроля доcтупа Azure**— этот компонент обеспечивает поддержку проверки подлинности пользователей приложения с помощью Azure ACS, используя сценарии единого входа и перемещая логику удостоверений из приложения.
   * **Общий подключаемый модуль Azure**— этот компонент предоставляет функциональные возможности, необходимые другим компонентам набора средств.
   * **Обозреватель Azure для Eclipse**— этот компонент предоставляет функциональные возможности, необходимые другим компонентам набора средств.
   * **Подключаемый модуль Azure для Eclipse с Java**— этот компонент обеспечивает поддержку проектов, помогающих собирать, тестировать и развертывать приложения Java для облака Microsoft Azure в Eclipse и с помощью командной строки.
   * **Подключаемый модуль веб- приложений Azure с Java**— этот компонент обеспечивает поддержку развертывания веб-приложений Java в контейнерах веб-приложений Microsoft Azure.
   * **Драйвер Microsoft JDBC 4.2 для SQL Server**— этот компонент предоставляет API JDBC для SQL Server и Базу данных SQL Microsoft Azure для платформы Java Enterprise Edition 8.
   * **Package for Apache Qpid Client Libraries for JMS**(Пакет для клиентских библиотек Apache Qpid для JMS) — этот компонент предоставляет клиентские компоненты JMS из проекта Apache Qpid, чтобы ваше приложение могло использовать обмен сообщениями на основе протокола AMQP в Azure.
   * **Пакет для библиотек Microsoft Azure для Java** — этот компонент предоставляет API для доступа к службам Microsoft Azure, таким как хранилище, служебная шина, среда выполнения службы и т. д.

1. Щелкните **Далее**. (Если при установке набора средств возникают необычные задержки, убедитесь, что снят флажок **Contact all update sites during install to find required software** [Проверить все сайты обновления во время установки для поиска требуемого ПО].)

1. В диалоговом окне **Install Details** (Сведения об установке) нажмите кнопку **Далее**.
   
   ![Просмотр сведений об установке][03]

1. В диалоговом окне **Review Licenses** (Просмотр лицензий) ознакомьтесь с условиями лицензионного соглашения. Если вы принимаете условия лицензионных соглашений, установите переключатель **I accept the terms of the license agreements** (Я принимаю условия лицензионных соглашений), а затем нажмите кнопку **Готово**. (В следующих действиях предполагается, что вы принимаете условия лицензионных соглашений. Если вы не принимаете эти условия, завершите процесс установки.)
   
   ![Review Licenses][04]
   
   Eclipse скачает и установит необходимые пакеты.
   
   ![Ход установки][05]

1. Если отображается запрос на перезапуск Eclipse для завершения установки, нажмите кнопку **Yes**(Да).
   
   ![Запрос перезапуска][06]

## <a name="next-steps"></a>Дальнейшие действия

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

<!-- URL List -->

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690946.aspx -->

<!-- IMG List -->

[01]: media/azure-toolkit-for-eclipse-installation/eclipse-installation-01.png
[02]: media/azure-toolkit-for-eclipse-installation/eclipse-installation-02.png
[03]: media/azure-toolkit-for-eclipse-installation/eclipse-installation-03.png
[04]: media/azure-toolkit-for-eclipse-installation/eclipse-installation-04.png
[05]: media/azure-toolkit-for-eclipse-installation/eclipse-installation-05.png
[06]: media/azure-toolkit-for-eclipse-installation/eclipse-installation-06.png
