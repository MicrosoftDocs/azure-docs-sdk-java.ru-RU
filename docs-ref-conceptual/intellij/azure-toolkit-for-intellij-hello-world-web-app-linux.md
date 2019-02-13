---
title: Развертывание веб-приложения Hello World, выполняющегося в контейнере Linux, в облаке с помощью набора средств Azure для IntelliJ
description: Запуск веб-приложения Hello World в контейнере Linux и его развертывание в облаке с помощью набора средств Azure для IntelliJ.
services: app-service\web
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 12/20/2018
ms.devlang: Java
ms.service: multiple
ms.tgt_pltfrm: multiple
ms.topic: article
ms.openlocfilehash: fdff8dc2bd7a29473314d5c0bc99b7bcda369156
ms.sourcegitcommit: 54e7f077d694a5b1dd7fa6c8870b7d476af9829c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/02/2019
ms.locfileid: "55648728"
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

1. Запустите IntelliJ и войдите в свою учетную запись Azure, следуя инструкциям по [входу для набора средств Azure для IntelliJ](https://docs.microsoft.com/java/azure/intellij/azure-toolkit-for-intellij-sign-in-instructions).

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

1. Щелкните значок меню **+ Создать ресурс**, а затем последовательно выберите **Контейнеры** и **Реестр контейнеров**.
   
   ![Создание нового реестра контейнеров Azure][create-container-registry-01]

1. При появлении страницы **Создать реестр контейнеров** введите данные в поля **Имя реестра** и **Группа ресурсов**, выберите **Включить** для параметра **Пользователь-администратор** и нажмите кнопку **Создать**.

   ![Настройка параметров реестра контейнеров Azure][create-container-registry-02]

## <a name="deploy-your-web-app-in-a-docker-container"></a>Развертывание веб-приложения в контейнере Docker

1. Щелкните правой кнопкой мыши проект в обозревателе проектов, выберите **Azure**, а затем — **Add Docker Support** (Добавление поддержки Docker).

   Файл Docker будет автоматически создан с конфигурацией по умолчанию.

   ![Добавление поддержки Docker][add-docker-support]

1. Добавив поддержку Docker, щелкните проект правой кнопкой мыши в обозревателе проектов, выберите **Azure**, а затем — **Run on Web App for Containers** (Выполнить в веб-приложении для контейнеров).

   ![Выполнение в веб-приложении для контейнеров][run-on-web-app-for-containers]

1. Когда отобразится диалоговое окно **Run on Web App for Containers** (Выполнение в веб-приложении для контейнеров), введите необходимые сведения:

   * **Имя.** Понятное имя, отображаемое в наборе средств Azure. 

   * **Container Registry** (Реестр контейнеров). Выберите в раскрывающемся меню реестр контейнеров, который вы создали в предыдущем разделе этой статьи. Поля **Server URL** (URL-адрес сервера), **Username** (Имя пользователя) и **Password** (Пароль) будут заполнены автоматически.

   * **Image and tag** (Образ и тег). Имя образа контейнера. Обычно используется следующий синтаксис: *registry*.azurecr.io/*appname*:latest, где: 
      * *registry* — это реестр контейнеров из предыдущего раздела этой статьи; 
      * *appname* — это имя веб-приложения. 

   * **Use Existing Web App** (Использовать существующее веб-приложение) или **Create New Web App** (Создать веб-приложение). Указывает, будете ли вы развертывать контейнер в существующем веб-приложении или создадите новое. С помощью указанного вами **имени приложения** будет создан URL-адрес для вашего веб-приложения, например: *wingtiptoys.azurewebsites.net*.

   * **Группа ресурсов**. Указывает, создадите ли вы группу ресурсов или будете использовать существующую. 

   * **App Service Plan** (План службы приложений). Указывает, создадите ли вы план службы приложений или будете использовать существующий. 

   ![Выполнение в веб-приложении для контейнеров][run-on-web-app-linux]

1. Настроив перечисленные выше параметры, нажмите кнопку **Run** (Выполнить). После успешного развертывания веб-приложения его состояние будет отображаться в окне **Run** (Выполнение).

   ![Веб-приложение успешно развернуто][successfully-deployed]

1. После публикации веб-приложения вы можете перейти к указанному для него ранее URL-адресу, например *wingtiptoys.azurewebsites.net*.

   ![Переход к веб-приложению][browsing-to-web-app]

## <a name="optional-modify-your-web-app-publish-settings"></a>Необязательно: Изменение параметров для публикации веб-приложения

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

[add-docker-support]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/add-docker-support.png
[browsing-to-web-app]:  media/azure-toolkit-for-intellij-hello-world-web-app-linux/browsing-to-web-app.png
[create-container-registry-01]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/create-container-registry-01.png
[create-container-registry-02]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/create-container-registry-02.png
[docker-settings-menu]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/docker-settings-menu.png
[edit-configuration-dialog]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/edit-configuration-dialog.png
[edit-configuration-menu]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/edit-configuration-menu.png
[file-new-project]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/file-new-project.png
[groupid-and-artifactid]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/groupid-and-artifactid.png
[maven-archetype-webapp]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/maven-archetype-webapp.png
[maven-options]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/maven-options.png
[project-name]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/project-name.png
[run-on-web-app-for-containers]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/run-on-web-app-for-containers.png
[run-on-web-app-linux]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/run-on-web-app-linux.png
[successfully-deployed]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/successfully-deployed.png
