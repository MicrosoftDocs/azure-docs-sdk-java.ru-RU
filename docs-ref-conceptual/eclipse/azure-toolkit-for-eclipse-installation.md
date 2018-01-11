---
title: "Установка набора средств Azure для Eclipse"
description: "Узнайте, как установить набор средств Azure для подключаемого модуля Eclipse, чтобы создавать и развертывать облачные приложения в Azure."
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
ms.date: 11/01/2017
ms.author: robmcm
ms.openlocfilehash: 54f636f1291832702bfed2b49888b531d358cb73
ms.sourcegitcommit: 9c354a65b0f8ad49a528f40ddee647b091f7d246
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/04/2018
---
# <a name="install-the-azure-toolkit-for-eclipse"></a>Установка набора средств Azure для Eclipse

В набор средств Azure для Eclipse входят шаблоны и функции для простого создания, разработки, тестирования и развертывания облачных приложений в Azure с помощью среды разработки Eclipse.

> [!NOTE] 
> 
> Набор средств Azure для Eclipse — это проект с открытым кодом, исходный код которого доступен по лицензии MIT на сайте проекта в GitHub по следующему URL-адресу: 
> 
> <https://github.com/microsoft/azure-tools-for-java> 
> 

Ниже приведен процесс установки набора средств Azure для Eclipse.

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="to-install-the-azure-toolkit-for-eclipse"></a>Установка набора средств Azure для Eclipse

1. Запустите Eclipse.

1. Щелкните меню **Help** (Справка) и выберите пункт **Install New Software** (Установить новое программное обеспечение), как показано на следующем рисунке.
   
   ![Установка набора средств Azure для Eclipse][01]

1. В диалоговом окне **Available Software** (Доступное программное обеспечение) в текстовом поле **Work with** (Работа с) введите `http://dl.microsoft.com/eclipse/` и нажмите клавишу **ВВОД**.

1. В области **Name** (Имя) установите флажок **Azure Toolkit for Eclipse** (Набор средств Azure для Eclipse) и снимите флажок **Contact all update sites during install to find required software** (Проверить все сайты обновления во время установки для поиска требуемого ПО). Экран должен выглядеть следующим образом:
   
   ![Установка набора средств Azure для Eclipse][02]

1. Если развернуть **набор средств Azure для Eclipse**, вы увидите список компонентов, которые будут установлены, например:

   | Функция | ОПИСАНИЕ | 
   |---|---| 
   | **Подключаемый модуль Application Insights для Java** | Этот компонент позволяет использовать службы регистрации и анализа телеметрии Azure для приложений и экземпляров серверов. | 
   | **Общий подключаемый модуль Azure** | Этот компонент предоставляет функциональные возможности, необходимые другим компонентам набора средств. | 
   | **Набор средств контейнеров Azure для Eclipse** | Этот компонент позволяет создавать и развертывать WAR-файлы как контейнеры Docker в виртуальной машине Docker. | 
   | **Контейнеры Azure для Eclipse** | Этот компонент позволяет развертывать WAR-файлы или артефакт JAR как контейнер Docker в виртуальной машине Azure. | 
   | **Azure Explorer для Eclipse** | Этот компонент предоставляет интерфейс в виде проводника для управления ресурсами Azure. | 
   | **Microsoft JDBC Driver 6.1 для SQL Server** | Этот компонент предоставляет API JDBC для SQL Server и Базу данных SQL Microsoft Azure для платформы Java Enterprise Edition 8. | 
   | **Пакет для библиотек Microsoft Azure для Java** | Этот компонент предоставляет API-интерфейсы для доступа к таким службам Microsoft Azure, как хранилище, служебная шина, среда выполнения службы и т. д. | 

1. Нажмите кнопку **Далее**. (Если при установке набора средств возникают необычные задержки, убедитесь, что снят флажок **Contact all update sites during install to find required software** [Проверить все сайты обновления во время установки для поиска требуемого ПО].)

1. В диалоговом окне **Install Details** (Сведения об установке) нажмите кнопку **Далее**.
   
   ![Просмотр сведений об установке][03]

1. В диалоговом окне **Review Licenses** (Просмотр лицензий) ознакомьтесь с условиями лицензионного соглашения. Если вы принимаете условия лицензионных соглашений, установите переключатель **I accept the terms of the license agreements** (Я принимаю условия лицензионных соглашений), а затем нажмите кнопку **Готово**. (В следующих действиях предполагается, что вы принимаете условия лицензионных соглашений. Если вы не принимаете эти условия, завершите процесс установки.)
   
   ![Review Licenses][04]
   
   Eclipse скачает и установит необходимые пакеты.
   
   ![Ход установки][05]

1. Если отображается запрос на перезапуск Eclipse для завершения установки, нажмите кнопку **Yes**(Да).
   
   ![Запрос перезапуска][06]

## <a name="next-steps"></a>Дополнительная информация

[!INCLUDE [azure-toolkit-for-eclipse-additional-resources](../includes/azure-toolkit-for-eclipse-additional-resources.md)]

<!-- URL List -->

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690946.aspx -->

<!-- IMG List -->

[01]: media/azure-toolkit-for-eclipse-installation/eclipse-installation-01.png
[02]: media/azure-toolkit-for-eclipse-installation/eclipse-installation-02.png
[03]: media/azure-toolkit-for-eclipse-installation/eclipse-installation-03.png
[04]: media/azure-toolkit-for-eclipse-installation/eclipse-installation-04.png
[05]: media/azure-toolkit-for-eclipse-installation/eclipse-installation-05.png
[06]: media/azure-toolkit-for-eclipse-installation/eclipse-installation-06.png
