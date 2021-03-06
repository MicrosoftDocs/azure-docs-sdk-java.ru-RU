---
title: ''
description: В этом руководстве показано, как с помощью набора средств Azure для Eclipse версии 3.0.6 (или более ранней) создать веб-приложение Hello World для Azure.
services: app-service
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 11/13/2018
ms.devlang: java
ms.service: app-service
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: web
ms.openlocfilehash: b05dcd52f36524ab17652f83c6ced4006f874365
ms.sourcegitcommit: 8d0c59ae7c91adbb9be3c3e6d4a3429ffe51519d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/27/2018
ms.locfileid: "52338718"
---
# <a name="create-a-hello-world-web-app-for-azure-using-the-legacy-toolkit-for-eclipse"></a>Создание веб-приложения Hello World для Azure с помощью набора средств для Eclipse предыдущих версий

В этом руководстве показано, как создать базовое приложение Hello World для Azure и развернуть его как веб-приложение с помощью [Набор средств Azure для Eclipse] версии 3.0.6 (или более ранней).

> [!NOTE]
>
> Дополнительные сведения о версии, в которой используются [Набор средств Azure для IntelliJ], см. в статье [Создание веб-приложения Azure (цен. категория "Базовый") с помощью IntelliJ][intellij-hello-world].
>

> [!IMPORTANT]
> 
> Набор средств Azure для Eclipse обновлен в августе 2017 года. В него добавлен другой рабочий процесс. В этой статье описывается, как создать веб-приложение Hello World с помощью набора средств Azure для Eclipse версии 3.0.6 (или более ранней). Если вы используете набор средств версии 3.0.7 (или более поздней), необходимо выполнить действия, описанные в руководстве по [созданию веб-приложения Hello World для Azure в Eclipse][Updated Version].
>

После завершения этого учебника приложение при просмотре в веб-браузере будет выглядеть следующим образом:

![Предварительный просмотр приложения Hello World][01]

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="create-a-new-web-app-project"></a>Создание проекта веб-приложения

1. Запустите Eclipse и войдите в свою учетную запись Azure, следуя инструкциям из статьи [Инструкции по входу для набора средств Azure для Eclipse][eclipse-sign-in-instructions].

1. Выберите **File** (Файл), **New** (Создать), а затем — **Dynamic Web Project** (Динамический веб-проект). (Если элемента **Динамический веб-проект** нет в списке доступных проектов после выбора пунктов **Файл** и **Создать**, сделайте следующее: последовательно щелкните **Файл**, **Создать**, **Проект...**, разверните узел **Интернет**, щелкните **Dynamic Web Project** (Динамический веб-проект) и нажмите кнопку **Далее**.)

2. Для целей данного учебника присвойте проекту имя **MyWebApp**. Экран будет выглядеть следующим образом:
   
   ![Создание динамического веб-проекта][02]

3. Нажмите кнопку **Готово**

4. В представлении **обозревателя проектов** в Eclipse разверните узел **MyWebApp**. Щелкните правой кнопкой мыши **WebContent**, выберите **Создать**, затем щелкните **JSP File** (JSP-файл).

5. В диалоговом окне **New JSP File** (Новый JSP-файл) укажите имя файла **index.jsp**, оставьте родительскую папку **MyWebApp/WebContent** без изменений, а затем нажмите кнопку **Далее**.

6. Для нашего примера в диалоговом окне **Select JSP Template** (Выбор шаблона JSP) щелкните **New JSP File (html)** (Создать JSP-файл (html)) и нажмите кнопку **Готово**.

7. При открытии в Eclipse файла index.jsp добавьте код для динамического отображения фразы **Hello World!** в существующий элемент `<body>`. Обновленное содержимое элемента `<body>` должно выглядеть так:
   
   ```jsp
   <body><b><% out.println("Hello World!"); %></b></body>
   ```

8. Сохраните index.jsp.

## <a name="deploy-your-web-app-to-azure"></a>Развертывание веб-приложения в Azure

Существует несколько способов, с помощью которых можно развернуть веб-приложение Java в Azure. В этом учебнике описывается один из самых простых: ваше приложение будет развернуто в контейнер веб-приложения Azure — для этого не нужно выбирать особый тип проекта и не требуются дополнительные инструменты. JDK и программное обеспечение веб-контейнера будут предоставлены Azure, поэтому нет необходимости загружать их самостоятельно. Все, что вам нужно — ваше веб-приложение Java. В результате процесс публикации приложения занимает несколько секунд, а не минут.

1. В обозревателе проектов Eclipse щелкните правой кнопкой мыши **MyWebApp**.

2. В контекстном меню выберите **Azure**, затем щелкните **Опубликовать как веб-приложение Azure**.
   
   ![Опубликовать как веб-приложение Azure][03]
   
   Кроме того, выбирая проект веб-приложения в обозревателе проектов, вы можете нажать на панели инструментов кнопку с раскрывающимся списком **Опубликовать** и выбрать в списке **Publish as Azure Web App** (Опубликовать как веб-приложение Azure).
   
   ![Опубликовать как веб-приложение Azure][14]

3. Если вы еще не вошли в систему Azure из Eclipse, появится запрос на вход в учетную запись Azure:
   
   ![Диалоговое окно входа в Azure][04]
   
   При наличии нескольких учетных записей Azure некоторые запросы во время входа в систему могут отображаться несколько раз, даже если они выглядят одинаковыми. Если это происходит, выполните вход.

4. После успешного входа в учетную запись Azure в диалоговом окне **Управление подписками** отобразится список подписок, связанных с вашими учетными данными. Если список содержит несколько подписок и вы будете работать только с некоторыми из них, снимите флажки с подписок, которые не будете использовать. После выбора подписок щелкните **Закрыть**.
   
   ![Диалоговое окно управления подписками][05]

5. При открытии диалогового окна **Deploy to Azure Web App Container** (Развертывание в контейнер веб-приложения Azure) в нем будут показаны все контейнеры веб-приложений, созданные ранее. Если вы не создали ни одного контейнера, список будет пустым.
   
   ![Диалоговое окно развертывания в контейнер веб-приложения Azure][06]

6. Если вы не создавали контейнер веб-приложения Azure или хотите опубликовать приложение в новый контейнер, выполните следующие действия. В противном случае выберите существующий контейнер веб-приложения и перейдите к шагу 7 ниже.
   
   a. Нажмите кнопку **Создать**
      
      ![Диалоговое окно развертывания в контейнер веб-приложения Azure][15]

   b. Откроется диалоговое окно **New Web App Container** (Новый контейнер веб-приложения):
      
      ![Диалоговое окно нового контейнера веб-приложения][07a]

   c. Укажите **метку DNS** для контейнера веб-приложения. Она образует метку листа DNS для URL-адреса узла веб-приложения в Azure. (Примечание. Имя должно быть доступным и соответствовать требованиям к именованию веб-приложений Azure.)

   d. В раскрывающемся меню **Веб-контейнер** выберите для своего приложения соответствующее программное обеспечение.
      
      На данный момент можно выбрать Tomcat 8, Tomcat 7 или Jetty 9. Последний дистрибутив выбранного ПО будет предоставлен Azure. Он будет работать с последним дистрибутивом JDK, также предоставленным Azure.

   д. В раскрывающемся меню **Подписка** выберите подписку, которую вы хотите использовать для этого развертывания.

   Е. В раскрывающемся меню **Группа ресурсов** выберите группу ресурсов, с которой вы хотите связать свое веб-приложение. (Группы ресурсов Azure позволяют сгруппировать связанные ресурсы, чтобы, например, удалить их одновременно.)
      
      Можно выбрать существующую группу ресурсов (если она есть) и перейти к шагу g ниже, или создать новую, сделав следующее:
      
   * Нажмите кнопку **Создать**
   * Откроется диалоговое окно **Новая группа ресурсов** :
        
       ![Диалоговое окно новой группы ресурсов][08]
   * В текстовое поле **Имя** введите имя новой группы ресурсов.
   * В раскрывающемся меню **Регион** выберите расположение центра обработки данных Azure для группы ресурсов.
   * Необязательно. По умолчанию Azure автоматически развернет последний дистрибутив Java 8 в ваш контейнер веб-приложения в качестве виртуальной машины Java. Тем не менее, если это нужно веб-приложению, то можно указать другую версию и дистрибутив виртуальной машины Java. Чтобы указать пакет JDK для веб-приложения, щелкните **JDK** и выберите один из следующих параметров.
     * **Deploy the default JDK offered by Azure Web Apps service** (Развернуть пакет JDK по умолчанию, предлагаемый службой веб-приложений Azure). Этот параметр позволит развернуть последний дистрибутив Java.
     * **Deploy a 3rd party JDK available on Azure** (Развернуть сторонний пакет JDK, доступный в Azure). Этот параметр позволяет выбрать из списка пакетов JDK, предоставляемых Microsoft Azure.
     * **Deploy my own JDK from this download location** (Развернуть собственный пакет JDK из этого расположения для скачивания). Этот параметр позволяет указать собственный дистрибутив JDK, который должен быть упакован в ZIP-файл и передан либо в общедоступное расположение для скачивания, либо в учетную запись хранения Azure, к которой у вас есть доступ.
          
       ![Диалоговое окно нового контейнера веб-приложения][07b]

   ж. Последовательно выберите **ОК**.

   h. В раскрывающемся меню **План службы приложений** перечислены планы службы приложений, связанные с выбранной группой ресурсов. (В планах службы приложений указываются такие сведения, как расположение веб-приложения, ценовая категория и размер вычислительной операции. Один план службы приложений можно использовать для нескольких веб-приложений, поэтому он поддерживается отдельно от развертывания конкретного веб-приложения.)
      
       You can select an existing App Service Plan (if you have any) and skip to step h below, or use the following these steps to create a new App Service Plan:
      
      * Нажмите кнопку **Создать**
      * Откроется диалоговое окно **Новый план службы приложений** :
        
          ![Диалоговое окно нового плана службы приложений][09]
      * В текстовое поле **Имя** введите имя нового плана службы приложений.
      * В раскрывающемся меню **Расположение** выберите расположение центра обработки данных Azure для плана.
      * В раскрывающемся меню **Ценовая категория** выберите соответствующую ценовую категорию для плана. Для тестирования можно выбрать категорию **Бесплатный**.
      * В раскрывающемся меню **Размер экземпляра** выберите для плана соответствующий размер экземпляра. Для тестирования можно выбрать **Маленький**.

   i. После завершения всех описанных выше действий диалоговое окно "Новый контейнер веб-приложения" должно выглядеть примерно так, как показано ниже:
      
      ![Диалоговое окно нового контейнера веб-приложения][10]

   j. Нажмите кнопку **ОК** , чтобы создать контейнер веб-приложения.
       
      Подождите несколько секунд. Когда список контейнеров веб-приложений обновится, созданный контейнер веб-приложения должен быть выбран в списке.

7. Теперь все готово для начального развертывания вашего веб-приложения в Azure:
   
   ![Диалоговое окно развертывания в контейнер веб-приложения Azure][11]
   
   Нажмите кнопку **ОК** , чтобы развернуть приложение Java в выбранный контейнер веб-приложения.
   
   По умолчанию приложение будет развернуто в подкаталог сервера приложений. Чтобы развернуть приложение в качестве корневого приложения, установите флажок **Deploy to root** (Развернуть в корень) перед нажатием кнопки **ОК**.

8. После этого вы должны увидеть представление **Журнал действий Azure** , в котором будет отображаться состояние развертывания веб-приложения.
   
   ![Журнал действий Azure][12]
   
   Процесс развертывания веб-приложения в Azure занимает всего несколько секунд. Когда процесс будет завершен, вы увидите ссылку **Опубликовано** in the **Состояние** . Если щелкнуть по ней, откроется домашняя страница развернутого веб-приложения.

## <a name="updating-your-web-app"></a>Обновление веб-приложения

Обновить существующее и запущенное веб-приложение Azure быстро и просто. Сделать это можно двумя способами:

* Можно обновить развертывание существующего веб-приложения Java.
* Можно опубликовать дополнительное приложение Java в тот же контейнер веб-приложения.

Процесс в каждом случае идентичен и занимает несколько секунд.

1. В обозревателе проектов Eclipse щелкните правой кнопкой мыши приложение Java, которое вы хотите обновить или добавить в существующий контейнер веб-приложения.

2. В контекстном меню выберите **Azure**, а затем щелкните **Опубликовать как веб-приложение Azure**.

3. Так как ранее вы уже вошли в систему, вы увидите список существующих контейнеров веб-приложений. Выберите контейнер, в котором вы хотите опубликовать или повторно опубликовать приложение Java, и нажмите кнопку **ОК**.

Через несколько секунд в представлении **Журнал действий Azure** состояние обновленного развертывания изменится на **Опубликовано**, и вы сможете проверить свое обновленное приложение в веб-браузере.

## <a name="starting-stopping-or-restarting-an-existing-web-app"></a>Запуск, остановка или перезапуск существующего веб-приложения

Запустить или остановить существующий контейнер веб-приложения Azure (включая все развернутые в нем приложения Java) можно в представлении **Обозреватель Azure** .

Если представление **Azure Explorer** еще не открыто, это можно сделать, щелкнув в Eclipse меню **Окно** и последовательно выбрав **Show View** (Показать представление), **Other** (Другие), **Azure**, **Azure Explorer**. Если ранее вы не вошли в систему, вам будет предложено это сделать.

Когда представление **Обозреватель Azure** откроется, выполните следующие действия для запуска или остановки веб-приложения. 

1. Разверните узел **Azure** .

2. Разверните узел **Web Apps** (Веб-приложения). 

3. Щелкните правой кнопкой мыши необходимое веб-приложение.

4. В открывшемся контекстном меню выберите **Запустить**, **Остановить** или **Перезапустить**. Обратите внимание, что доступные меню контекстно зависимы, поэтому можно только остановить веб-приложение или запустить веб-приложение, которое в данный момент не запущено.
   
   ![Остановка существующего веб-приложения][13]

## <a name="next-steps"></a>Дополнительная информация

[!INCLUDE [azure-toolkit-for-eclipse-additional-resources](../includes/azure-toolkit-for-eclipse-additional-resources.md)]

Дополнительные сведения о создании веб-приложений Azure см. в разделе [Обзор веб-приложений].

<!-- URL List -->

[Набор средств Azure для Eclipse]: azure-toolkit-for-eclipse.md
[Набор средств Azure для IntelliJ]: ../intellij/azure-toolkit-for-intellij.md
[intellij-hello-world]: ../intellij/azure-toolkit-for-intellij-create-hello-world-web-app.md
[Обзор веб-приложений]: /azure/app-service/app-service-web-overview
[Apache Tomcat]: http://tomcat.apache.org/
[Jetty]: http://www.eclipse.org/jetty/
[Updated Version]: azure-toolkit-for-eclipse-create-hello-world-web-app.md
[eclipse-sign-in-instructions]: azure-toolkit-for-eclipse-sign-in-instructions.md


<!-- IMG List -->

[01]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version/01-Web-Page.png
[02]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version/02-Dynamic-Web-Project.png
[03]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version/03-Context-Menu.png
[04]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version/04-Log-In-Dialog.png
[05]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version/05-Manage-Subscriptions-Dialog.png
[06]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version/06-Deploy-To-Azure-Web-Container.png
[07a]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version/07a-New-Web-App-Container-Dialog.png
[07b]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version/07b-New-Web-App-Container-Dialog.png
[08]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version/08-New-Resource-Group-Dialog.png
[09]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version/09-New-Service-Plan-Dialog.png
[10]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version/10-Completed-Web-App-Container-Dialog.png
[11]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version/11-Completed-Deploy-Dialog.png
[12]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version/12-Activity-Log-View.png
[13]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version/13-Azure-Explorer-Web-App.png
[14]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version/14-publishDropdownButton.png
[15]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version/15-New-Azure-Web-Container.png
