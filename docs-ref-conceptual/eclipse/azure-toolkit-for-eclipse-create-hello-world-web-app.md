---
title: Создание веб-приложения Hello World для Azure в Eclipse
description: В этом учебнике показано, как с помощью набора средств Azure для Eclipse создать веб-приложение Hello World для Azure.
services: app-service
documentationcenter: java
author: selvasingh
manager: routlaw
editor: ''
ms.assetid: 20d41e88-9eab-462e-8ee3-89da71e7a33f
ms.author: robmcm;asirveda
ms.date: 02/01/2018
ms.devlang: java
ms.service: app-service
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: web
ms.openlocfilehash: 5e025c90c2619ec72ffddf5815fd49c3ac59c00f
ms.sourcegitcommit: 798f4d4199d3be9fc5c9f8bf7a754d7393de31ae
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/08/2018
ms.locfileid: "33883651"
---
# <a name="create-a-hello-world-web-app-for-azure-using-eclipse"></a>Создание веб-приложения Hello World для Azure в Eclipse

В этом руководстве показано, как создать базовое приложение Hello World для Azure и развернуть его как веб-приложение с помощью [набора средств Azure для Eclipse].

> [!NOTE]
>
> Дополнительные сведения о версии, в которой используются [средства Azure для IntelliJ], см. в статье [Создание веб-приложения Azure (цен. категория "Базовый") с помощью IntelliJ][intellij-hello-world].
>

> [!IMPORTANT]
> 
> Набор средств Azure для Eclipse обновлен в августе 2017 года. В него добавлен другой рабочий процесс. В этой статье описывается, как создать веб-приложение Hello World с помощью набора средств Azure для Eclipse версии 3.0.7 (или более поздней). Если вы используете набор средств версии 3.0.6 (или более ранней), необходимо выполнить действия, описанные в руководстве по [созданию веб-приложения Hello World для Azure в Eclipse с помощью набора средств предыдущих версий][Legacy Version].
> 

После завершения этого учебника приложение при просмотре в веб-браузере будет выглядеть следующим образом:

![Предварительный просмотр приложения Hello World][browse-web-app]

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="create-a-new-web-app-project"></a>Создание проекта веб-приложения

1. Запустите Eclipse и войдите в учетную запись Azure, следуя инструкциям из статьи [Инструкции по входу для набора средств Azure для Eclipse][eclipse-sign-in-instructions].

1. Выберите **File** (Файл), **New** (Создать), а затем — **Dynamic Web Project** (Динамический веб-проект). (Если элемента **Динамический веб-проект** нет в списке доступных проектов после выбора пунктов **Файл** и **Создать**, сделайте следующее: последовательно щелкните **Файл**, **Создать**, **Проект...**, разверните узел **Интернет**, щелкните **Dynamic Web Project** (Динамический веб-проект) и нажмите кнопку **Далее**.)

   ![Создание динамического веб-проекта][file-new-dynamic-web-project]

2. Для целей данного учебника присвойте проекту имя **MyWebApp**. Экран будет выглядеть следующим образом:
   
   ![Свойства нового динамического веб-проекта][dynamic-web-project-properties]

3. Нажмите кнопку **Готово**

4. В представлении обозревателя проектов в Eclipse разверните узел **MyWebApp**. Щелкните правой кнопкой мыши **WebContent**, выберите **Создать**, затем щелкните **JSP File** (JSP-файл).

   ![Создание файла JSP][create-new-jsp-file]

5. В диалоговом окне **New JSP File** (Новый JSP-файл) укажите имя файла **index.jsp**, оставьте родительскую папку **MyWebApp/WebContent** без изменений, а затем нажмите кнопку **Далее**.

   ![Диалоговое окно New JSP File (Создание JSP-файла)][new-jsp-file-dialog]

6. Для нашего примера в диалоговом окне **Select JSP Template** (Выбор шаблона JSP) щелкните **New JSP File (html)** (Создать JSP-файл (html)) и нажмите кнопку **Готово**.

   ![Выбор шаблона JSP][select-jsp-template]

7. При открытии в Eclipse файла index.jsp добавьте код для динамического отображения фразы **Hello World!** в существующий элемент `<body>`. Обновленное содержимое элемента `<body>` должно выглядеть так:
   
   ```jsp
   <body><b><% out.println("Hello World!"); %></b></body>
   ```

8. Сохраните index.jsp.

## <a name="deploy-your-web-app-to-azure"></a>Развертывание веб-приложения в Azure

1. В представлении обозревателя проектов Eclipse щелкните правой кнопкой мыши проект, выберите **Azure**, а затем — **Publish as Azure Web App** (Опубликовать как веб-приложение Azure).
   
   ![Опубликовать как веб-приложение Azure][publish-as-azure-web-app]

1. В диалоговом окне **Deploy Web App** (Развертывание веб-приложения) можно выбрать один из следующих вариантов:

   * Выберите существующее веб-приложение.

      ![Выбор службы приложения][select-app-service]

   * Щелкните **Create New Web App** (Создать веб-приложение).

      ![Создание службы приложений][create-app-service]

      В диалоговом окне **Create App Service** (Создание службы приложений) укажите требуемую информацию для веб-приложения и нажмите кнопку **Create** (Создать).

      ![Диалоговое окно "Создание службы приложений"][create-app-service-dialog]

1. Выберите веб-приложение и щелкните **Deploy** (Развернуть).

   ![Развертывание службы приложений][deploy-app-service]

1. Набор средств отобразит сообщение о состоянии (**Опубликовано**) на вкладке **Журнал действий Azure** при успешном развертывании веб-приложения, где будет содержаться гиперссылка с URL-адресом развернутого веб-приложения.

   ![Состояние публикации][publish-status]

1. Перейти к своему веб-приложению можно с помощью ссылки, предоставленной в сообщении о состоянии.

   ![Просмотр веб-приложения][browse-web-app]

1. Опубликовав веб-сайт в Azure, вы можете управлять им, щелкнув его правой кнопкой мыши и выбрав один из параметров контекстного меню. Например, вы можете **запустить**, **остановить** или **удалить** веб-приложение.

   ![Управление службой приложений][manage-app-service]

## <a name="next-steps"></a>Дополнительная информация

[!INCLUDE [azure-toolkit-for-eclipse-additional-resources](../includes/azure-toolkit-for-eclipse-additional-resources.md)]

Дополнительные сведения о создании веб-приложений Azure см. в разделе [Обзор веб-приложений].

<!-- URL List -->

[набора средств Azure для Eclipse]: azure-toolkit-for-eclipse.md
[средства Azure для IntelliJ]: ../intellij/azure-toolkit-for-intellij.md
[intellij-hello-world]: ../intellij/azure-toolkit-for-intellij-create-hello-world-web-app.md
[Обзор веб-приложений]: /azure/app-service/app-service-web-overview
[Apache Tomcat]: http://tomcat.apache.org/
[Jetty]: http://www.eclipse.org/jetty/
[Legacy Version]: azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version.md

<!-- IMG List -->

[browse-web-app]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/browse-web-app.png
[file-new-dynamic-web-project]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/file-new-dynamic-web-project.png
[dynamic-web-project-properties]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/dynamic-web-project-properties.png
[create-new-jsp-file]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/create-new-jsp-file.png
[new-jsp-file-dialog]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/new-jsp-file-dialog.png
[select-jsp-template]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/select-jsp-template.png
[publish-as-azure-web-app]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/publish-as-azure-web-app.png
[deploy-web-app-dialog]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/deploy-web-app-dialog.png
[select-app-service]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/select-app-service.png
[create-app-service-dialog]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/create-app-service-dialog.png
[publish-status]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/publish-status.png
[create-app-service]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/create-app-service.png
[deploy-app-service]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/deploy-app-service.png
[manage-app-service]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/manage-app-service.png
