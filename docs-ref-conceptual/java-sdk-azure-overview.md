---
title: Библиотеки Azure для Java
description: Обзор библиотек служб и библиотек управления Azure для Java
keywords: Azure, Java, SDK, API
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 04/16/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: multiple
ms.assetid: 9aaf22a2-382a-4b13-a8e3-0e467d607207
ms.openlocfilehash: 22a337e928085475e905a271f991147729d97671
ms.sourcegitcommit: 1500f341a96d9da461c288abf4baf79f494ae662
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/28/2017
ms.locfileid: "21930880"
---
# <a name="azure-libraries-for-java"></a>Библиотеки Azure для Java

Библиотеки Azure для Java позволяют подключаться к службам и управлять ресурсами Azure, используя код приложения. Эти библиотеки доступны в качестве [импортируемых файлов Maven](java-sdk-azure-install.md), которые можно использовать в проектах Java. 

## <a name="manage-azure-resources"></a>Управление ресурсами Azure

Создавайте ресурсы Azure и управляйте ими из приложений Java, используя [библиотеки управления Azure для Java](java-sdk-azure-get-started.md). Используйте эти библиотеки для создания собственных служб и средств автоматизации Azure. 

Например, для создания виртуальной машины Linux следует написать следующий код:

```java
VirtualMachine linuxVM = azure.virtualMachines().define("myAzureVM")
           .withRegion(region)
           .withExistingResourceGroup("sampleResourceGroup")
           .withNewPrimaryNetwork("10.0.0.0/28")
           .withPrimaryPrivateIpAddressDynamic()
           .withoutPrimaryPublicIpAddress()
           .withPopularLinuxImage(KnownLinuxVirtualMachineImage.UBUNTU_SERVER_16_04_LTS)
           .withRootUsername(userName)
           .withSsh(key)
           .withUnmanagedStorage()
           .withSize(VirtualMachineSizeTypes.STANDARD_D3_V2)
           .create();
 ```

Полный список библиотек и рекомендации по их импорту в проекты см. в [инструкциях по установке](java-sdk-azure-install.md). А сведения по настройке проверки подлинности и выполнению примера кода в подписке Azure см. в [статье по началу работы](java-sdk-azure-get-started.md). 

## <a name="connect-to-azure-services"></a>Подключение к службам Azure

Библиотеки Java можно использовать не только для создания ресурсов и управления ими в Azure, но и для подключения и использования этих ресурсов в приложениях. Например, для обновления табличной базы данных SQL или хранения файлов в службе хранилища Azure. Выберите библиотеку, необходимую для конкретной службы, в [полном списке библиотек](java-sdk-azure-install.md) и ознакомьтесь с руководствами и примерами кода, которые помогут вам использовать библиотеки в приложениях, в [центре разработчиков Java](https://azure.microsoft.com/develop/java/).

Например, чтобы вывести содержимое каждого большого двоичного объекта в контейнере хранилища Azure, используйте следующий код:

```java
// get the container from the blob client
CloudBlobContainer container = blobClient.getContainerReference("blobcontainer");

// For each item in the container
for (ListBlobItem blobItem : container.listBlobs()) {
    // If the item is a blob, not a virtual directory
    if (blobItem instanceof CloudBlockBlob) {
        // Download the text
        CloudBlockBlob retrievedBlob = (CloudBlockBlob) blobItem;
        System.out.println(retrievedBlob.downloadText());
    }
}
```

## <a name="sample-code-and-reference"></a>Примеры кода и справочные материалы

В примерах кода ниже представлены общие задачи автоматизации, выполняемые с помощью библиотек управления Azure для Java. Это готовый код, который вы можете использовать в своих приложениях.

- [Виртуальные машины](java-sdk-azure-virtual-machine-samples.md)
- [Веб-приложения](java-sdk-azure-web-apps-samples.md)
- [База данных SQL](java-sdk-azure-sql-database-samples.md)
   
[Справочник](https://docs.microsoft.com/java/api) доступен для всех пакетов в библиотеках служб и библиотеках управления. Сведения о новых функциях и критически важных изменениях, а также инструкции по переходу с предыдущих версий см. в [заметках о выпуске](java-sdk-azure-release-notes.md).