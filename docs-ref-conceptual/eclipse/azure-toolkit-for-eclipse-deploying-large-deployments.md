---
title: "Развертывание крупных систем"
description: "Узнайте о развертывании крупных систем с помощью набора средств Azure для Eclipse."
services: 
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
ms.assetid: 5e18bace-5df0-4af8-ad86-6151ea8bd823
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 09/11/2017
ms.author: robmcm
ms.openlocfilehash: 0e367e74d038043f1626dbf19aab87db6451bc02
ms.sourcegitcommit: 256044d7cbce16dcb8dc4e195d0f63c10cb44d4e
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/13/2017
---
# <a name="deploying-large-deployments"></a>Развертывание крупных систем

В случае если развертывание слишком велико для размещения в корневом каталоге приложения, вы можете использовать локальный ресурс хранилища в качестве корневой папки для своего JDK и сервера приложений.

## <a name="to-use-a-local-storage-resource-as-the-deployment-root-folder-for-large-deployments"></a>Использование локального ресурса хранилища в качестве корневой папки развертывания для крупных развертываний

1. Создайте новый локальный ресурс хранилища. Имя ресурса значения не имеет. Ресурсы хранилища определяются на уровне роли. Быстрее всего получить доступ к диалоговому окну настройки локального хранилища, из которого вы можете создать новый локальный ресурс хранилища, можно, сделав следующее: щелкните правой кнопкой мыши роль в представлении **Обозреватель проектов** (разверните узел проекта Azure, если вы не видите роль), выберите **Azure** и **Локальное хранилище**. В диалоговом окне **Локальное хранилище** нажмите кнопку **Добавить**, чтобы создать локальный ресурс хранилища.

1. Установите желаемый размер не менее 2048 МБ (меньшее значение может привести к тем же проблемам с размером файлов, что и в корневом каталоге приложения).

1. Установите флажок **Clean the contents when the role instance is recycled** (Очищать содержимое при перезапуске экземпляра роли). Это поможет предотвратить конфликты логики запуска развертывания с имеющимися файлами в ресурсе при перезапуске экземпляра роли.

1. Для значения **Environment variable storing the resource's directory path after deployment** (Переменная среды, хранящая путь к каталогу ресурса после развертывания) задайте строку **DEPLOYROOT**. Диалоговое окно локального ресурса хранилища будет выглядеть следующим образом.

   ![][ic667943]

Кроме того, если вы используете **DEPLOYROOT** в качестве *имени* локального ресурса и не изменяете автоматически созданное имя переменной среды (в данном случае это **DEPLOYROOT_PATH**), этот вариант также подойдет для вашего приложения.

Дополнительные сведения о создании локального ресурса хранилища вы можете найти в статье [Свойства локального хранилища][Local storage properties].

## <a name="next-steps"></a>Дальнейшие действия

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing the Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546
[Local storage properties]: http://go.microsoft.com/fwlink/?LinkID=699525#local_storage_properties

<!-- IMG List -->

[ic667943]: media/azure-toolkit-for-eclipse-deploying-large-deployments/ic667943.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/dn268601.aspx -->
