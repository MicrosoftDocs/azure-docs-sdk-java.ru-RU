---
title: "Развертывание веб-приложения Java в Azure за пять минут с помощью Maven | Документация Майкрософт"
description: "Создание и развертывание приложения Java, созданного с помощью Maven, в Azure"
services: app-service\web
documentationcenter: 
author: rloutlaw
manager: douge
editor: 
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 03/17/2017
ms.author: routlaw
ms.openlocfilehash: 1adc0a104ba22bcd353664e68323165890e46c64
ms.sourcegitcommit: 30d502b3150fa14bcc1251f5f88c7c0dd83e531e
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/12/2017
---
# <a name="create-and-deploy-a-java-app-to-azure-with-maven"></a>Создание и развертывание приложения Java в Azure с помощью Maven

Это краткое руководство поможет вам создать и развернуть простое веб-приложение Java в [службе приложений Azure](/azure/app-service/app-service-value-prop-what-is) с использованием [Apache Maven](http://maven.apache.org) и интерфейса командной строки Azure за считаные минуты.

## <a name="before-you-begin"></a>Перед началом работы

Прежде чем начать, настройте следующие компоненты:

- [Git.](https://git-scm.com/)
- [Java 8](https://www.azul.com/downloads/zulu/);
- [Maven 3](http://maven.apache.org/download.cgi)
- [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2)

Если у вас еще нет подписки Azure, [создайте бесплатную учетную запись Azure](https://azure.microsoft.com/free/?WT.mc_id=A261C142F), прежде чем начинать работу.

## <a name="get-the-sample-code"></a>Получение кода примера

Клонируйте репозиторий с примером приложения на локальный компьютер. Пример представляет собой простое приложение JSP с дополнительной конфигурацией Maven в проекте `pom.xml` для локального тестирования приложения и развертывания примера в службе приложений Azure.

```
git clone https://github.com/Azure-Samples/app-service-maven
```

## <a name="run-the-app-locally"></a>Локальный запуск приложения

Откройте командную строку, с помощью Maven выполните сборку приложения и запустите его в локальном веб-контейнере [Tomcat](https://tomcat.apache.org). 

```
cd app-service-maven
mvn package
mvn tomcat7:run-war
```

Откройте веб-браузер и перейдите по адресу http://localhost:8080, чтобы просмотреть приложение:

  ![Выходные данные Hello World из примера приложения Java](media/maven-quickstart/java-app-hello-world-output.png)

## <a name="log-in-to-azure"></a>Вход в Azure

Войдите в интерфейс командной строки Azure с помощью команды `az login`. В этом руководстве интерфейс командной строки используется для запроса и создания ресурсов Azure, необходимых для размещения приложения.
   
```azurecli
az login
```

## <a name="create-a-resource-group"></a>Создание группы ресурсов   

Создайте группу ресурсов с помощью команды [az group create](/cli/azure/group#create). Группа ресурсов Azure является логическим контейнером, в котором происходит развертывание ресурсов Azure и управление ими.

```azurecli
az group create --location "East US" --name myResourceGroup
```

Чтобы увидеть другие доступные значения для `---location`, выполните команду [az appservice list-locations](/cli/azure/appservice#list-locations).

## <a name="create-an-app-service-plan"></a>Создание плана службы приложений

Создайте **бесплатный** [план службы приложений](/azure/app-service/azure-web-sites-web-hosting-plans-in-depth-overview), выполнив команду [az appservice plan create](/cli/azure/appservice/plan#create). Планы службы приложений распределяют ресурсы, которые совместно используются всеми веб-приложениями, работающими в плане.


```azurecli
az appservice plan create --name my-free-appservice-plan --resource-group myResourceGroup --sku FREE
```

Когда план службы приложений будет готов, в интерфейсе командной строки Azure отобразятся следующие сведения:

```json
{
    "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/serverfarms/my-free-appservice-plan",
    "location": "East US",
    "sku": {
    "capacity": 1,
    "family": "S",
    "name": "S1",
    "tier": "Standard"
    },
    "status": "Ready",
    "type": "Microsoft.Web/serverfarms"
}
```


## <a name="create-a-web-app"></a>Создание веб-приложения

Создайте веб-приложение, использующее ресурсы плана, с помощью команды интерфейса командной строки Azure [az webapp create](/cli/azure/appservice/web#create). В определении веб-приложения указано место для развертывания кода и URL-адрес для доступа к приложению после его запуска.

В приведенной ниже команде замените заполнитель <appname> уникальным именем приложения. В качестве узла по умолчанию для веб-приложения используется <appname>. Если <appname> не является уникальным, вы получите сообщение об ошибке "Веб-сайт с указанным именем уже существует".

```azurecli
az webapp create --name appname --resource-group myResourceGroup --plan my-free-appservice-plan
```

После создания веб-приложения в Azure CLI отобразятся примерно такие сведения:

```json
{
    "clientAffinityEnabled": true,
    "defaultHostName": "<appname>.azurewebsites.net",
    "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/sites/<appname>",
    "isDefaultContainer": null,
    "kind": "app",
    "location": "East US",
    "name": "<app_name>",
    "repositorySiteName": "<app_name>",
    "reserved": true,
    "resourceGroup": "myResourceGroup",
    "serverFarmId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/serverfarms/my-free-appservice-plan",
    "state": "Running",
    "type": "Microsoft.Web/sites",
}
```

## <a name="configure-java-and-tomcat"></a>Настройка Java и Tomcat

Выполните команду Azure CLI [az webapp config](/cli/azure/appservice/web#config), чтобы настроить веб-приложение для использования Java и Tomcat. Приведенный ниже пример кода настраивает в службе приложений Java 8 и [Apache Tomcat 8.5](http://tomcat.apache.org/) для запуска приложения.

```azurecli
az webapp config set \ 
--name appname \
--resource-group myResourceGroup \
--java-container TOMCAT \
--java-version 1.8.0_73  \
--java-container-version 8.5
```

## <a name="configure-maven"></a>Настройка Maven 

Пример файла Maven `pom.xml` включает конфигурацию, которая передает пример в Azure по протоколу FTP. Но для развертывания веб-приложения это файл необходимо настроить. Получите учетные данные службы приложений с помощью команды [az appservice web deployment list-publishing-profiles](/cli/azure/appservice/web/deployment#list-publishing-profiles):

```azurecli
az webapp deployment list-publishing-profiles  \
--name appname \ 
--resource-group myResourceGroup  \
--query "[?publishMethod=='FTP'].{URL:publishUrl, Username:userName,Password:userPWD}" 
```

```json
[
  {
    "Password": "aBcDeFgHiJkLmNoPqRsTuVwXyZ",
    "URL": "ftp://waws-prod-blu-045.ftp.azurewebsites.windows.net/site/wwwroot",
    "Username": "appname\\$appname"
  }
]
```

Замените заполнители в файле `az-settings.xml` паролем, именем пользователя и именем узла FTP из выходных данных. В имени пользователя используйте только один символ `\` вместо экранированного значения из выходных данных интерфейса командной строки.
   
```XML
...
    <server>
      <id>azure-hello-world</id>
      <username>appname\$appname</username>
      <password>aBcDeFgHiJkLmNoPqRsTuVwXyZ</password>
    </server>
...
   <configuration>
     <fromFile>${basedir}/target/AzureAppDemo-0.0.1-SNAPSHOT.war</fromFile>
     <url>ftp://waws-prod-blu-045.ftp.azurewebsites.windows.net/site/wwwroot</url>
     <toFile>webapps/ROOT.war</toFile>
     <serverId>azure-hello-world</serverId>
   </configuration>
...
```

## <a name="deploy-the-sample-application"></a>Развертывание примера приложения

Разверните пример в Azure с помощью параметра Maven `-s` для использования конфигурации в файле `az-settings.xml`.

```
mvn install -s az-settings.xml
```

## <a name="browse-to-web-app"></a>Перейдите к веб-приложению

Просмотрите пример, запущенный в Azure:

```azurecli
az webapp browse --name appname --resource-group myResourceGroup
```

## <a name="update-the-app"></a>Обновление приложения

В текстовом редакторе откройте файл `src/main/webapp/index.jsp` и замените существующий JSP-элемент приведенным ниже.

```html
<%--
  Copyright (c) Microsoft Corporation. All rights reserved.
  Licensed under the MIT License. See License.txt in the project root for
  license information.
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java"  import="java.util.Date" %>
<html>
<head>
  <title>Azure Samples Hello World</title>
</head>
<body>
  <H1>Hello Azure!</H1>
   Current time is: <%= new Date() %>
</body>
</html>
```

Разверните обновление с помощью Maven:

```
mvn clean package
mvn install -s az-settings.xml
```

Обновите страницу в браузере после повторного развертывания приложения, чтобы увидеть изменения.

## <a name="manage-your-new-azure-app"></a>Управление новым приложением Azure

Перейдите на портал Azure, чтобы просмотреть созданное приложение.

Для этого войдите на портал [https://portal.azure.com](https://portal.azure.com).

В меню слева выберите **Служба приложений**, а затем щелкните имя своего веб-приложения Azure.

 ![Выбор приложения из списка веб-приложений на портале](media/azure-app-service-portal.png)

Протестируйте компонент мониторинга, выполнив команду `curl` в приложении, чтобы отправить трафик.

```bash
curl http://<appname>.azurewebsites.net/?[1-30]
```

Через несколько минут в компоненте мониторинга отобразится действие запроса.

 ![Мониторинг на портале Azure](media/java-app-monitoring.png)

## <a name="clean-up-resources"></a>Очистка ресурсов

Чтобы удалить все ресурсы, созданные в этом руководстве, выполните следующую команду:

```azurecli
az group delete --name myResrouceGroup
```

## <a name="next-steps"></a>Дальнейшие действия

Просмотрите полный список [примеров кода Java для Azure](https://azure.microsoft.com/resources/samples/?term=java).