---
title: "Развертывание веб-приложения Hello World, выполняющегося в контейнере Linux, в облаке с помощью набора средств Azure для IntelliJ"
description: "Запуск веб-приложения Hello World в контейнере Linux и его развертывание в облаке с помощью набора средств Azure для IntelliJ."
services: app-service\web
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 11/01/2017
ms.author: robmcm
ms.openlocfilehash: fdf41d6e8b23a6b7d6217ec626480e6c72e13969
ms.sourcegitcommit: 9c354a65b0f8ad49a528f40ddee647b091f7d246
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/04/2018
---
# <a name="deploy-a-hello-world-web-app-to-a-linux-container-in-the-cloud-using-the-azure-toolkit-for-intellij"></a>Развертывание веб-приложения Hello World в контейнере Linux в облаке с помощью набора средств Azure для IntelliJ

Контейнеры [Docker] широко используются при развертывании веб-приложений. При этом разработчики могут объединить все зависимости и файлы проекта в одном пакете, а затем развернуть его на сервере. Набор средств Azure для IntelliJ упрощает этот процесс для разработчиков на языке Java, предоставляя функции для развертывания контейнеров в Microsoft Azure.

В этой статье показаны действия, необходимые для создания базового веб-приложения Hello World и его публикации в контейнере Linux в Azure с помощью набора средств Azure для IntelliJ.

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]
* Клиент [Docker].

> [!NOTE]
>
> Для работы с этим руководством необходимо настроить [Docker], чтобы он имел возможность предоставить управляющую программу на порте 2375 без протокола TLS. Этот параметр можно настроить при установке Docker или с помощью меню параметров Docker.
>
> ![Меню параметров Docker][docker-settings-menu]
>

## <a name="create-a-new-web-app-project"></a>Создание проекта веб-приложения

1. Запустите IntelliJ и войдите в свою учетную запись Azure, следуя инструкциям из статьи "Инструкции по входу для набора средств Azure для IntelliJ".

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

## <a name="create-an-azure-container-registry-to-use-as-a-private-docker-registry"></a>Создание реестра контейнеров Azure для использования в качестве частного реестра Docker

Ниже рассмотрена процедура использования портала Azure для создания реестра контейнеров Azure.

> [!NOTE]
>
> Если вы хотите использовать Azure CLI, а не портал Azure, выполните процедуру, описанную в статье [Создание частного реестра контейнеров Docker с помощью Azure CLI 2.0][Create Docker Registry using Azure CLI].
>

1. Перейдите на [портал Azure] и выполните вход.

   После входа в свою учетную запись на портале Azure можно выполнить процедуру, описанную в статье [Создание частного реестра контейнеров Docker с помощью портала Azure], которую здесь полезно представить еще раз.

1. Щелкните значок меню **+ Создать**, нажмите кнопку **Контейнеры**, а затем нажмите кнопку **Реестр контейнеров Azure**.
   
   ![Создание нового реестра контейнеров Azure][AR01]

1. При появлении страницы сведений о шаблоне реестра контейнеров Azure нажмите кнопку **Создать**. 

   ![Создание нового реестра контейнеров Azure][AR02]

1. При появлении страницы **Создать реестр контейнеров** введите данные в поля **Имя реестра** и **Группа ресурсов**, выберите **Включить** для параметра **Пользователь-администратор** и нажмите кнопку **Создать**.

   ![Настройка параметров реестра контейнеров Azure][AR03]

1. После создания реестра контейнеров перейдите в реестр контейнеров на портале Azure и нажмите кнопку **Ключи доступа**. Запишите имя пользователя и пароль для последующих шагов.

   ![Ключи доступа к реестру контейнеров Azure][AR04]

## <a name="deploy-your-web-app-in-a-docker-container"></a>Развертывание веб-приложения в контейнере Docker

1. Щелкните правой кнопкой мыши проект в обозревателе проектов, выберите **Azure**, а затем — **Add Docker Support** (Добавление поддержки Docker).

   Файл Docker будет автоматически создан с конфигурацией по умолчанию.

   ![Добавление поддержки Docker][add-docker-support]

1. Добавив поддержку Docker, щелкните правой кнопкой мыши проект в обозревателе проектов, выберите **Azure**, а затем — **Run on Web App (Linux)** (Выполнить веб-приложение (Linux)).

   ![Выполнение веб-приложения (Linux)][run-on-web-app-linux]

1. Когда отобразится диалоговое окно **Run on Web App (Linux)** (Выполнение веб-приложения (Linux)), введите необходимые сведения:

   * **Name** (Имя) — понятное имя, отображаемое в наборе средств Azure. 

   * **Server URL** (URL-адрес сервера) — URL-адрес реестра контейнеров из предыдущего раздела этой статьи. Обычно используется следующий синтаксис *registry*.azurecr.io. 

   * **Username** (Имя пользователя) и **Password** (Пароль) — ключи доступа для реестра контейнеров из предыдущего раздела этой статьи. 

   * **Image and tag** (Образ и тег) — название образа контейнера. Обычно используется следующий синтаксис: *registry*.azurecr.io/*appname*:latest, где: 
      * *registry* — это реестр контейнеров из предыдущего раздела этой статьи; 
      * *appname* — это имя веб-приложения. 

   * **Use Existing Web App** (Использовать имеющееся веб-приложение) или **Create New Web App** (Создать веб-приложение) — указывает, будете ли вы развертывать контейнер в имеющемся веб-приложении или создадите веб-приложение. 

   * **Resource Group** (Группа ресурсов) — указывает, создадите ли вы группу ресурсов или будете использовать имеющуюся. 

   * **App Service Plan** (План службы приложений) — указывает, создадите ли вы план службы приложений или будете использовать имеющийся. 

1. Настроив перечисленные выше параметры, нажмите кнопку **Run** (Выполнить).

   ![Создание веб-приложения][create-web-app]

1. После публикации веб-приложения параметры будут сохранены в качестве параметров по умолчанию. Приложение можно запустить в Azure, щелкнув значок зеленой стрелки на панели инструментов. Вы можете изменить параметры, щелкнув раскрывающееся меню для веб-приложения, а затем — **Edit Configurations** (Изменить конфигурации).

   ![Пункт меню Edit configuration (Изменить конфигурацию)][edit-configuration-menu]

1. При отображении диалогового окна **Run/Debug Configurations** (Конфигурации выполнения и отладки) можно изменить любые параметры по умолчанию, а затем нажать кнопку **ОК**.

   ![Диалоговое окно Edit configuration (Изменение конфигурации)][edit-configuration-dialog]

## <a name="next-steps"></a>Дополнительная информация

Дополнительные материалы по Docker доступны на официальном [веб-сайте Docker][Docker].

[!INCLUDE [azure-toolkit-for-intellij-additional-resources](../includes/azure-toolkit-for-intellij-additional-resources.md)]

<!-- URL List -->

[портал Azure]: https://portal.azure.com/
[Создание частного реестра контейнеров Docker с помощью портала Azure]: /azure/container-registry/container-registry-get-started-portal
[Azure for Java Developers]: https://docs.microsoft.com/java/azure/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Create Docker Registry using Azure CLI]: /azure/container-registry/container-registry-get-started-azure-cli

[Docker]: https://www.docker.com/
[Configuring artifacts]: https://www.jetbrains.com/help/idea/2016.1/configuring-artifacts.html

<!-- IMG List -->

[AR01]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/AR01.png
[AR02]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/AR02.png
[AR03]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/AR03.png
[AR04]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/AR04.png

[docker-settings-menu]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/docker-settings-menu.png
[file-new-project]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/file-new-project.png
[maven-archetype-webapp]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/maven-archetype-webapp.png
[groupid-and-artifactid]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/groupid-and-artifactid.png
[maven-options]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/maven-options.png
[project-name]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/project-name.png
[add-docker-support]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/add-docker-support.png
[run-on-web-app-linux]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/run-on-web-app-linux.png
[create-web-app]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/create-web-app.png
[edit-configuration-menu]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/edit-configuration-menu.png
[edit-configuration-dialog]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/edit-configuration-dialog.png
[successfully-deployed]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/successfully-deployed.png
