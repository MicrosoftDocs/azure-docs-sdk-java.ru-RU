---
title: "Библиотеки пакетной службы Azure для Java"
description: "Справочная документация по библиотекам пакетной службы для Java"
keywords: Azure, Java, SDK, API, Batch, processing, scheduling, long-running
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 06/21/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: batch
ms.openlocfilehash: 2c9fab2834ea6d9c906d9483aed839a0411aaa40
ms.sourcegitcommit: 634ab7578c73a219f8f3a2a6d43999d9d372cb43
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/09/2017
---
# <a name="azure-batch-libraries-for-java"></a>Библиотеки пакетной службы Azure для Java

## <a name="overview"></a>Обзор

Обеспечьте эффективную работу приложений для крупномасштабных параллельных и высокопроизводительных вычислений в облаке с помощью [пакетной службы Azure](/azure/batch/batch-technical-overview).   

Чтобы приступить к работе с пакетной службой Azure, ознакомьтесь со статьей [Создание учетной записи пакетной службы на портале Azure](/azure/batch/batch-account-create-portal).

## <a name="client-library"></a>Клиентская библиотека

Клиентские библиотеки пакетной службы Azure позволяют настроить вычислительные узлы и пулы, определить и настроить выполняемые задачи в заданиях, а также настроить диспетчер заданий, чтобы отслеживать выполнение заданий и управлять им. Дополнительные сведения об использовании этих объектов для запуска решений для крупномасштабных параллельных вычислений см. [здесь](/azure/batch/batch-api-basics).

[Добавьте зависимость](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) в файл Maven `pom.xml`, чтобы использовать клиентскую библиотеку в проекте.

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-batch</artifactId>
    <version>2.0.0</version>
</dependency>
```   

### <a name="example"></a>Пример

Настройте пул вычислительных узлов Linux в учетной записи пакетной службы.

```java
// create the batch client for an account using its URI and keys
BatchClient client = BatchClient.open(new BatchSharedKeyCredentials("https://fabrikambatch.eastus.batch.azure.com", "fabrikambatch", batchKey));

// configure a pool of VMs to use 
VirtualMachineConfiguration configuration = new VirtualMachineConfiguration();
configuration.withNodeAgentSKUId("batch.node.ubuntu 16.04");
client.poolOperations().createPool(poolId, poolVMSize, configuration, poolVMCount);
```

> [!div class="nextstepaction"]
> [Обзор клиентских API-интерфейсов](/java/api/overview/azure/batch/clientlibrary)


## <a name="management-api"></a>API управления

Используйте библиотеки управления пакетной службы Azure, чтобы создавать и удалять учетные записи пакетной службы, считывать и повторно создавать ключи учетной записи пакетной службы и управлять хранилищем учетных записей пакетной службы.

[Добавьте зависимость](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) в файл Maven `pom.xml`, чтобы использовать API управления в проекте.

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-batch</artifactId>
    <version>1.3.0</version>
</dependency>
```

### <a name="example"></a>Пример

Создайте учетную запись пакетной службы Azure и настройте новое приложение и учетную запись хранения Azure для него.

```java
BatchAccount batchAccount = azure.batchAccounts().define("newBatchAcct")
    .withRegion(Region.US_EAST)
    .withNewResourceGroup("myResourceGroup")
    .defineNewApplication("batchAppName")
        .defineNewApplicationPackage(applicationPackageName)
        .withAllowUpdates(true)
        .withDisplayName(applicationDisplayName)
        .attach()
    .withNewStorageAccount("batchStorageAcct")
    .create();
```

> [!div class="nextstepaction"]
> [Обзор API-интерфейсов управления](/java/api/overview/azure/batch/managementapi)


## <a name="samples"></a>Примеры

[Управление учетными записями пакетной службы][1]   

Ознакомьтесь с другими [примерами кода Java для пакетной службы Azure](https://azure.microsoft.com/resources/samples/?platform=java&term=batch), которые можно использовать в приложениях.

[1]: https://github.com/Azure-Samples/batch-java-manage-batch-accounts