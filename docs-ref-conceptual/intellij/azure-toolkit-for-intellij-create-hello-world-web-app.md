---
title: "Создание веб-приложения Hello World для Azure с помощью Eclipse"
description: "В этом учебнике показано, как с помощью набора средств Azure для IntelliJ создать веб-приложение Hello World для Azure."
services: app-service
documentationcenter: java
author: selvasingh
manager: routlaw
editor: 
ms.assetid: 75ce7b36-e3ae-491d-8305-4b42ce37db4e
ms.author: robmcm;asirveda
ms.date: 02/01/2018
ms.devlang: java
ms.service: app-service
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: web
ms.openlocfilehash: cc68e16a6940a1f0f2b08f0b63c90c58ec6dbc4e
ms.sourcegitcommit: 151aaa6ccc64d94ed67f03e846bab953bde15b4a
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/03/2018
---
# <a name="create-a-hello-world-web-app-for-azure-using-intellij"></a>Создание веб-приложения Hello World для Azure с помощью Eclipse

В этом руководстве показано, как создать базовое приложение Hello World для Azure и развернуть его как веб-приложение с помощью [набора средств Azure для IntelliJ].

> [!NOTE]
>
> Дополнительные сведения о версии, в которой используются [средства Azure для Eclipse], см. в статье [Создание веб-приложения Azure (цен. категория "Базовый") с помощью Eclipse][eclipse-hello-world].
>

> [!IMPORTANT]
> 
> Набор средств Azure для IntelliJ обновлен в августе 2017 года. В него добавлен другой рабочий процесс. В этой статье описывается, как создать веб-приложение Hello World с помощью набора средств Azure для IntelliJ версии 3.0.7 (или более поздней). Если вы используете набор средств версии 3.0.6 (или более ранней), необходимо выполнить действия, описанные в руководстве по [созданию веб-приложения Hello World для Azure в IntelliJ с помощью набора средств предыдущих версий][Legacy Version].
> 

После завершения этого учебника приложение при просмотре в веб-браузере будет выглядеть следующим образом:

![Предварительный просмотр приложения Hello World][browse-web-app]

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="create-a-new-web-app-project"></a>Создание проекта веб-приложения

1. Запустите IntelliJ и войдите в свою учетную запись Azure, следуя инструкциям из статьи [Инструкции по входу для набора средств Azure для IntelliJ][intelliJ-sign-in-instructions].

1. Щелкните меню **File** (Файл), выберите команду **New** (Создать), а затем — **Project** (Проект).
   
   ![Создание проекта][file-new-project]

1. В диалоговом окне **New Project** (Новый проект) выберите **Maven**, а затем **maven-archetype-webapp** и щелкните **Next** (Далее).
   
   ![Выбор веб-приложения архетипа Maven][maven-archetype-webapp]
   
1. Укажите значение **GroupId** (Идентификатор группы) и **ArtifactId** (Идентификатор артефакта) для веб-приложения и щелкните **Next** (Далее).
   
   ![Указание идентификатора группы и артефакта][groupid-and-artifactid]

1. Настройте любые параметры Maven или примите значения по умолчанию и щелкните **Next** (Далее).
   
   ![Указание параметров Maven][maven-options]

1. Укажите имя и расположение проекта, а затем щелкните **Finish** (Готово).
   
   ![Указание имени проекта][project-name]

1. В представлении обозревателя проектов IntelliJ разверните **src**, а затем **main**, **webapp** и дважды щелкните **index.jsp**.
   
   ![Открытие страницы индексов][open-index-page]

1. При открытии в IntelliJ файла index.jsp добавьте код для динамического отображения фразы **Hello World!** в существующий элемент `<body>`. Обновленное содержимое элемента `<body>` должно выглядеть так:
   
   ```java
   <body><b><% out.println("Hello World!"); %></b></body>
   ``` 

   ![Изменение страницы индексов][edit-index-page]

1. Сохраните index.jsp.

## <a name="deploy-your-web-app-to-azure"></a>Развертывание веб-приложения в Azure

1. В представлении обозревателя проектов IntelliJ щелкните правой кнопкой мыши проект, выберите **Azure**, а затем — **Run on Web App** (Выполнить в веб-приложении).
   
   ![Пункт меню Run on web app (Выполнить в веб-приложении)][run-on-web-app-menu]

1. В диалоговом окне Run on Web App (Выполнение в веб-приложении) можно выбрать один из таких вариантов:

   * Выберите имеющееся веб-приложение (если оно есть) и нажмите кнопку **Run** (Выполнить).

      ![Диалоговое окно Run on Web App (Выполнение в веб-приложении)][run-on-web-app-dialog]

   * Щелкните **Create New Web App** (Создать веб-приложение). Если вы решите создать веб-приложение, укажите требуемую информацию для веб-приложения и нажмите кнопку **Run** (Выполнить).

      ![Создание веб-приложения][create-new-web-app-dialog]

1. Набор средств отобразит сообщение о состоянии при успешном развертывании веб-приложения, где будет содержаться URL-адрес развернутого веб-приложения.

   ![Развертывание завершено успешно][successfully-deployed]

1. Перейти к своему веб-приложению можно с помощью ссылки, предоставленной в сообщении о состоянии.

   ![Просмотр веб-приложения][browse-web-app]

1. После публикации веб-приложения параметры будут сохранены в качестве параметров по умолчанию. Приложение можно запустить в Azure, щелкнув значок зеленой стрелки на панели инструментов. Вы можете изменить параметры, щелкнув раскрывающееся меню для веб-приложения, а затем — **Edit Configurations** (Изменить конфигурации).

   ![Пункт меню Edit configuration (Изменить конфигурацию)][edit-configuration-menu]

1. При отображении диалогового окна **Run/Debug Configurations** (Конфигурации выполнения и отладки) можно изменить любые параметры по умолчанию, а затем нажать кнопку **ОК**.

   ![Диалоговое окно Edit configuration (Изменение конфигурации)][edit-configuration-dialog]

## <a name="next-steps"></a>Дополнительная информация

[!INCLUDE [azure-toolkit-for-intellij-additional-resources](../includes/azure-toolkit-for-intellij-additional-resources.md)]

Дополнительные сведения о создании веб-приложений Azure см. в разделе [Обзор веб-приложений].

<!-- URL List -->

[набора средств Azure для IntelliJ]: azure-toolkit-for-intellij.md
[средства Azure для Eclipse]: ../eclipse/azure-toolkit-for-eclipse.md
[eclipse-hello-world]: ../eclipse/azure-toolkit-for-eclipse-create-hello-world-web-app.md
[Обзор веб-приложений]: /azure/app-service/app-service-web-overview
[Apache Tomcat]: http://tomcat.apache.org/
[Jetty]: http://www.eclipse.org/jetty/
[Legacy Version]: azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version.md
[intelliJ-sign-in-instructions]: azure-toolkit-for-intellij-sign-in-instructions.md

<!-- IMG List -->

[file-new-project]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/file-new-project.png
[maven-archetype-webapp]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/maven-archetype-webapp.png
[groupid-and-artifactid]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/groupid-and-artifactid.png
[maven-options]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/maven-options.png
[project-name]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/project-name.png
[open-index-page]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/open-index-page.png
[edit-index-page]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/edit-index-page.png
[run-on-web-app-menu]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/run-on-web-app-menu.png
[run-on-web-app-dialog]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/run-on-web-app-dialog.png
[create-new-web-app-dialog]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/create-new-web-app-dialog.png
[successfully-deployed]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/successfully-deployed.png
[browse-web-app]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/browse-web-app.png
[edit-configuration-menu]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/edit-configuration-menu.png
[edit-configuration-dialog]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/edit-configuration-dialog.png
