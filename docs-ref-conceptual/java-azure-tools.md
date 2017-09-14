---
title: "Средства для разработчиков Java в Azure | Документация Майкрософт"
description: "Средства интеграции IDE, эмуляторы, обозреватели ресурсов и интерфейсы командной строки для разработчиков Java, работающих со службами Azure."
author: rloutlaw
manager: douge
ms.assetid: b55923b7-d60a-460d-b77c-af5fac67f1cc
ms.devlang: java
ms.topic: article
ms.service: Azure
ms.technology: Azure
ms.date: 4/10/2017
ms.author: routlaw;asirveda
ms.openlocfilehash: ce0b003cc7c48c8690f4236547ddec36e6ea9d53
ms.sourcegitcommit: ae39830d5a54fedceac78d8df1718e77741e03fa
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/09/2017
---
# <a name="azure-tools-for-java-developers"></a>Средства Azure для разработчиков Java

## <a name="client-and-management-libraries"></a>Клиентские библиотеки и библиотеки управления

Подключайтесь к службам и управляйте ресурсами Azure из своих приложений с помощью библиотек Azure для Java. Импортируйте библиотеки управления в проекты Maven, добавляя следующую зависимость в файл проекта *pom.xml*.

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure</artifactId>
    <version>1.2.1</version>
</dependency>
```

Просмотрите [полный список библиотек](java-sdk-azure-install.md) и [начните работу](java-sdk-azure-get-started.md) с библиотеками Azure для Java.

## <a name="eclipse-and-intellij-plugins"></a>Подключаемые модули Eclipse и IntelliJ

Управляйте ресурсами Azure и развертывайте приложения из среды IDE с помощью наборов средств Azure для [Eclipse](eclipse/azure-toolkit-for-eclipse.md) и [IntelliJ](intellij/azure-toolkit-for-intellij.md).   

![Набор средств IntelliJ с Azure Explorer](media/intelliJ-azure-explorer.png)

[Начало работы с набором средств Azure для Eclipse](https://docs.microsoft.com/azure/app-service-web/app-service-web-eclipse-create-hello-world-web-app) | [Начало работы с набором средств Azure для IntelliJ](https://docs.microsoft.com/azure/app-service-web/app-service-web-intellij-create-hello-world-web-app) 

## <a name="azure-cli-20"></a>Azure CLI 2.0

Azure CLI 2.0 позволяет управлять ресурсами Azure с помощью командной строки. Его можно использовать в браузере с [Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/overview) или [установить](https://docs.microsoft.com/cli/azure/install-azure-cli) в macOS, Linux или Windows и запускать из командной строки.

[Начало работы с Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli)

## <a name="azure-storage-explorer"></a>обозреватель хранилищ Azure 

Управляйте учетными записями хранения Azure, контейнерами, большими двоичными объектами и файлами с настольного компьютера. Сейчас обозреватель хранилища Azure доступен в предварительной версии и работает в Windows, macOS и Linux.

[Приступая к работе с обозревателем службы хранилища (предварительная версия)](https://docs.microsoft.com/azure/vs-azure-tools-storage-manage-with-storage-explorer)