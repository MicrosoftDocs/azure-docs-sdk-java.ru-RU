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
ms.openlocfilehash: 2f1e43f3835ffcdb138bf7e29a1656b7ee381281
ms.sourcegitcommit: 1500f341a96d9da461c288abf4baf79f494ae662
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/28/2017
ms.locfileid: "21930900"
---
# <a name="azure-management-libraries-for-java-samples-for-web-apps"></a><span data-ttu-id="b47c1-104">Библиотеки управления Azure для примеров веб-приложений Java</span><span class="sxs-lookup"><span data-stu-id="b47c1-104">Azure management libraries for Java samples for web apps</span></span>

| <span data-ttu-id="b47c1-105">**Создание приложения**</span><span class="sxs-lookup"><span data-stu-id="b47c1-105">**Create an app**</span></span> ||
|---|---|
| <span data-ttu-id="b47c1-106">[Создание веб-приложения и развертывание из FTP или GitHub][1]</span><span class="sxs-lookup"><span data-stu-id="b47c1-106">[Create a web app and deploy from FTP or GitHub][1]</span></span> | <span data-ttu-id="b47c1-107">Развертывание веб-приложений из локального репозитория Git или клиента FTP и непрерывная интеграция с репозиторием GitHub.</span><span class="sxs-lookup"><span data-stu-id="b47c1-107">Deploy web apps from local Git, FTP, and continuous integration from GitHub.</span></span> |
| <span data-ttu-id="b47c1-108">[Создание веб-приложения и управление слотами развертывания][2]</span><span class="sxs-lookup"><span data-stu-id="b47c1-108">[Create a web app and manage deployment slots][2]</span></span> | <span data-ttu-id="b47c1-109">Создание веб-приложения и его развертывание в промежуточных слотах с последующим переключением между промежуточным и рабочим слотами.</span><span class="sxs-lookup"><span data-stu-id="b47c1-109">Create a web app and deploy to staging slots, and then swap deployments between slots.</span></span> |
| <span data-ttu-id="b47c1-110">**Настройка приложения**</span><span class="sxs-lookup"><span data-stu-id="b47c1-110">**Configure app**</span></span> ||
| <span data-ttu-id="b47c1-111">[Создание веб-приложения и настройка личного домена][3]</span><span class="sxs-lookup"><span data-stu-id="b47c1-111">[Create a web app and configure a custom domain][3]</span></span> | <span data-ttu-id="b47c1-112">Создание веб-приложения с личным доменом и самозаверяющим SSL-сертификатом.</span><span class="sxs-lookup"><span data-stu-id="b47c1-112">Create a web app with a custom domain and self-signed SSL certificate.</span></span> |
| <span data-ttu-id="b47c1-113">**Масштабирование приложений**</span><span class="sxs-lookup"><span data-stu-id="b47c1-113">**Scale apps**</span></span> ||
| <span data-ttu-id="b47c1-114">[Масштабирование веб-приложения с высоким уровнем доступности в нескольких регионах][4]</span><span class="sxs-lookup"><span data-stu-id="b47c1-114">[Scale a web app with high availability across multiple regions][4]</span></span> | <span data-ttu-id="b47c1-115">Масштабирование веб-приложений в трех разных географических регионах и предоставление к ним доступа через одну конечную точку с помощью диспетчера трафика Azure.</span><span class="sxs-lookup"><span data-stu-id="b47c1-115">Scale a web app in three different geographical regions and make them available through a single endpoint using Azure Traffic Manager.</span></span> | 
| <span data-ttu-id="b47c1-116">**Подключение приложения к ресурсам**</span><span class="sxs-lookup"><span data-stu-id="b47c1-116">**Connect app to resources**</span></span> ||
| <span data-ttu-id="b47c1-117">[Подключение веб-приложения к учетной записи хранения][5]</span><span class="sxs-lookup"><span data-stu-id="b47c1-117">[Connect a web app to a storage account][5]</span></span> | <span data-ttu-id="b47c1-118">Создание учетной записи хранения Azure и добавление строки подключения учетной записи хранения к параметрам приложения.</span><span class="sxs-lookup"><span data-stu-id="b47c1-118">Create an Azure storage account and add the storage account connection string to the app settings.</span></span> |
| <span data-ttu-id="b47c1-119">[Подключение веб-приложения к базе данных SQL][6]</span><span class="sxs-lookup"><span data-stu-id="b47c1-119">[Connect a web app to a SQL database][6]</span></span> | <span data-ttu-id="b47c1-120">Создание веб-приложения Azure и базы данных SQL, а также добавление строки подключения базы данных SQL к параметрам приложения.</span><span class="sxs-lookup"><span data-stu-id="b47c1-120">Create a web app and SQL database, and then add the SQL database connection string to the app settings.</span></span> |

[1]: java-sdk-configure-webapp-sources.md
[2]: https://azure.microsoft.com/resources/samples/app-service-java-manage-staging-and-production-slots-for-web-apps/
[3]: https://azure.microsoft.com/resources/samples/app-service-java-manage-web-apps-with-custom-domains/
[4]: https://azure.microsoft.com/resources/samples/app-service-java-scale-web-apps-on-linux/
[5]: https://azure.microsoft.com/resources/samples/app-service-java-manage-storage-connections-for-web-apps/
[6]: https://azure.microsoft.com/resources/samples/app-service-java-manage-data-connections-for-web-apps/