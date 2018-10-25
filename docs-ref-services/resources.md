---
title: Библиотеки Azure Resource Manager для Java
description: Справочная документация по библиотекам Azure Resource Manager для Java
keywords: Azure, Java, SDK, API, resource groups, arm, resource manager
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 06/21/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: data-lake-store
ms.openlocfilehash: 7316c05e39bc88c50670dcb0f6331ce8440fd711
ms.sourcegitcommit: 4d52e47073fb0b3ac40a2689daea186bad5b1ef5
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/23/2018
ms.locfileid: "49799810"
---
# <a name="azure-resource-manager-libraries-for-java"></a>Библиотеки Azure Resource Manager для Java

## <a name="overview"></a>Обзор

Развертывайте, отслеживайте и администрируйте ресурсы в группах с помощью [Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview).

## <a name="management-api"></a>API управления

Используйте API управления для создания групп ресурсов и развертывания ресурсов на основе шаблонов.

[Добавьте зависимость](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) в файл Maven `pom.xml`, чтобы использовать API управления в проекте.


```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-resources</artifactId>
    <version>1.3.0</version>
</dependency>
```

## <a name="example"></a>Пример

Создайте группу ресурсов в следующем регионе Azure: восточная часть США.

```java
ResourceGroup resourceGroup = azure.resourceGroups().define("myResourceGroup")
            .withRegion(Region.US_EAST)
            .create();
```

> [!div class="nextstepaction"]
> [Обзор API-интерфейсов управления](/java/api/overview/azure/resources/management)

## <a name="samples"></a>Примеры

[Управление группами ресурсов Azure с помощью Java][1] 
[Развертывание ресурсов с помощью шаблона ARM][2]

[1]: https://github.com/Azure-Samples/resources-java-manage-resource-group
[2]: https://github.com/Azure-Samples/resources-java-deploy-using-arm-template

См. [полный список](https://azure.microsoft.com/resources/samples/?platform=java&term=resource) примеров для Azure Resource Manager.
