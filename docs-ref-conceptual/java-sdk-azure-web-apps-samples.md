---
title: Библиотеки управления Azure для примеров веб-приложений Java
description: Получите пример кода для создания и обновления веб-приложений Azure, размещенных в службе приложений, используя библиотеки управления Azure для Java.
keywords: Azure, Java, SDK, API, Maven, Gradle, web apps, app service
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 04/16/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: multiple
ms.assetid: 43633e5c-9fb1-4807-ba63-e24c126754e2
ms.openlocfilehash: be4031059587ceb88f6824356f677c37a198de80
ms.sourcegitcommit: 115f4c8ad07a11f17d79e9d945d63917836b11c8
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "61592589"
---
# <a name="azure-management-libraries-for-java-samples-for-web-apps"></a>Библиотеки управления Azure для примеров веб-приложений Java

| **Создание приложения** ||
|---|---|
| [Создание веб-приложения и развертывание из FTP или GitHub][1] | Развертывание веб-приложений из локального репозитория Git или клиента FTP и непрерывная интеграция с репозиторием GitHub. |
| [Создание веб-приложения и управление слотами развертывания][2] | Создание веб-приложения и его развертывание в промежуточных слотах с последующим переключением между промежуточным и рабочим слотами. |
| **Настройка приложения** ||
| [Создание веб-приложения и настройка личного домена][3] | Создание веб-приложения с личным доменом и самозаверяющим SSL-сертификатом. |
| **Масштабирование приложений** ||
| [Масштабирование веб-приложения с высоким уровнем доступности в нескольких регионах][4] | Масштабирование веб-приложений в трех разных географических регионах и предоставление к ним доступа через одну конечную точку с помощью диспетчера трафика Azure. | 
| **Подключение приложения к ресурсам** ||
| [Подключение веб-приложения к учетной записи хранения][5] | Создание учетной записи хранения Azure и добавление строки подключения учетной записи хранения к параметрам приложения. |
| [Подключение веб-приложения к базе данных SQL][6] | Создание веб-приложения Azure и базы данных SQL, а также добавление строки подключения базы данных SQL к параметрам приложения. |

[1]: java-sdk-configure-webapp-sources.md
[2]: https://azure.microsoft.com/resources/samples/app-service-java-manage-staging-and-production-slots-for-web-apps/
[3]: https://azure.microsoft.com/resources/samples/app-service-java-manage-web-apps-with-custom-domains/
[4]: https://azure.microsoft.com/resources/samples/app-service-java-scale-web-apps-on-linux/
[5]: https://azure.microsoft.com/resources/samples/app-service-java-manage-storage-connections-for-web-apps/
[6]: https://azure.microsoft.com/resources/samples/app-service-java-manage-data-connections-for-web-apps/