---
title: Создание приложения Spring Cloud Stream Binder с помощью Центров событий Azure
description: Настройка приложения Spring Cloud Stream Binder на основе Java, созданного с помощью Spring Boot Initializr и Центров событий Azure.
services: event-hubs
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 12/19/2018
ms.devlang: java
ms.service: event-hubs
ms.tgt_pltfrm: na
ms.topic: article
ms.workload: na
ms.openlocfilehash: 98b3dc1243bf293ede121eafd51b041649d165db
ms.sourcegitcommit: f0f140b0862ca5338b1b7e5c33cec3e58a70b8fd
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/03/2019
ms.locfileid: "53991428"
---
# <a name="how-to-create-a-spring-cloud-stream-binder-application-with-azure-event-hubs"></a><span data-ttu-id="c2dc2-103">Создание приложения Spring Cloud Stream Binder с помощью Центров событий Azure</span><span class="sxs-lookup"><span data-stu-id="c2dc2-103">How to create a Spring Cloud Stream Binder application with Azure Event Hubs</span></span>

## <a name="overview"></a><span data-ttu-id="c2dc2-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="c2dc2-104">Overview</span></span>

<span data-ttu-id="c2dc2-105">В статье показано, как настроить приложение Spring Cloud Stream Binder на основе Java, созданное с помощью Spring Boot Initializr и Центров событий Azure.</span><span class="sxs-lookup"><span data-stu-id="c2dc2-105">This article demonstrates how to configure a Java-based Spring Cloud Stream Binder application created with the Spring Boot Initializer with Azure Event Hubs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c2dc2-106">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="c2dc2-106">Prerequisites</span></span>

<span data-ttu-id="c2dc2-107">Чтобы выполнить действия, описанные в этой статье, необходимо иметь следующие компоненты:</span><span class="sxs-lookup"><span data-stu-id="c2dc2-107">The following prerequisites are required in order to follow the steps in this article:</span></span>

* <span data-ttu-id="c2dc2-108">Подписка Azure. Если у вас ее еще нет, вы можете активировать [Преимущества для подписчиков MSDN] или зарегистрироваться для получения [бесплатной учетной записи Azure].</span><span class="sxs-lookup"><span data-stu-id="c2dc2-108">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="c2dc2-109">Поддерживаемая версия Java Development Kit (JDK).</span><span class="sxs-lookup"><span data-stu-id="c2dc2-109">A supported Java Development Kit (JDK).</span></span> <span data-ttu-id="c2dc2-110">Дополнительные сведения о версиях JDK, доступных для разработки в Azure, см. в статье <https://aka.ms/azure-jdks>.</span><span class="sxs-lookup"><span data-stu-id="c2dc2-110">For more information about the JDKs available for use when developing on Azure, see <https://aka.ms/azure-jdks>.</span></span>
* <span data-ttu-id="c2dc2-111">[Apache Maven](http://maven.apache.org/) версии 3.0 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="c2dc2-111">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>

> [!IMPORTANT]
>
> <span data-ttu-id="c2dc2-112">Для выполнения операций, описанных в этой статье, требуется Spring Boot 2.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="c2dc2-112">Spring Boot version 2.0 or greater is required to complete the steps in this article.</span></span>
>

## <a name="create-an-azure-event-hub-using-the-azure-portal"></a><span data-ttu-id="c2dc2-113">Создание концентратора событий на портале Azure</span><span class="sxs-lookup"><span data-stu-id="c2dc2-113">Create an Azure Event Hub using the Azure portal</span></span>

### <a name="create-an-azure-event-hub-namespace"></a><span data-ttu-id="c2dc2-114">Создание пространства имен концентратора событий Azure</span><span class="sxs-lookup"><span data-stu-id="c2dc2-114">Create an Azure Event Hub Namespace</span></span>

1. <span data-ttu-id="c2dc2-115">Перейдите на портал Azure по адресу <https://portal.azure.com/> и выполните вход.</span><span class="sxs-lookup"><span data-stu-id="c2dc2-115">Browse to the Azure portal at <https://portal.azure.com/> and sign in.</span></span>

1. <span data-ttu-id="c2dc2-116">Выберите **+Создать ресурс**, **Интернет вещей** и **Центры событий**.</span><span class="sxs-lookup"><span data-stu-id="c2dc2-116">Click **+Create a resource**, then **Internet of Things**, and then click **Event Hubs**.</span></span>

   ![Создание пространства имен концентратора событий Azure][IMG01]

1. <span data-ttu-id="c2dc2-118">На странице **Создание пространства имен** введите такую информацию:</span><span class="sxs-lookup"><span data-stu-id="c2dc2-118">On the **Create Namespace** page, enter the following information:</span></span>

   * <span data-ttu-id="c2dc2-119">Уникальное **имя**, которое станет частью URI для пространства имен концентратора событий.</span><span class="sxs-lookup"><span data-stu-id="c2dc2-119">Enter a unique **Name**, which will become part of the URI for your event hub namespace.</span></span> <span data-ttu-id="c2dc2-120">Например, если вы зададите **wingtiptoys** в качестве **имени**, URI примет вид *wingtiptoys.servicebus.windows.net*.</span><span class="sxs-lookup"><span data-stu-id="c2dc2-120">For example: if you entered **wingtiptoys** for the **Name**, the URI would be *wingtiptoys.servicebus.windows.net*.</span></span>
   * <span data-ttu-id="c2dc2-121">Выберите **ценовую категорию** для пространства имен концентратора событий.</span><span class="sxs-lookup"><span data-stu-id="c2dc2-121">Choose a **Pricing tier** for your event hub namespace.</span></span>
   * <span data-ttu-id="c2dc2-122">Выберите **подписку** для пространства имен.</span><span class="sxs-lookup"><span data-stu-id="c2dc2-122">Choose the **Subscription** you want to use for your namespace.</span></span>
   * <span data-ttu-id="c2dc2-123">Укажите, следует ли создать новую **группу ресурсов** для пространства имен или использовать существующую.</span><span class="sxs-lookup"><span data-stu-id="c2dc2-123">Specify whether to create a new **Resource group** for your namespace, or choose an existing resource group.</span></span>
   * <span data-ttu-id="c2dc2-124">Укажите **расположение** для пространства имен Центров событий.</span><span class="sxs-lookup"><span data-stu-id="c2dc2-124">Specify the **Location** for your event hub namespace.</span></span>

   ![Создание пространства имен для концентратора событий Azure][IMG02]

1. <span data-ttu-id="c2dc2-126">Указав эти параметры, щелкните **Создать**, чтобы создать пространство имен.</span><span class="sxs-lookup"><span data-stu-id="c2dc2-126">When you have specified the options listed above, click **Create** to create your namespace.</span></span>

### <a name="create-an-azure-event-hub-in-your-namespace"></a><span data-ttu-id="c2dc2-127">Создание концентратора событий Azure в пространстве имен</span><span class="sxs-lookup"><span data-stu-id="c2dc2-127">Create an Azure Event Hub in your namespace</span></span>

1. <span data-ttu-id="c2dc2-128">Перейдите на портал Azure по адресу <https://portal.azure.com/>.</span><span class="sxs-lookup"><span data-stu-id="c2dc2-128">Browse to the Azure portal at <https://portal.azure.com/>.</span></span>

1. <span data-ttu-id="c2dc2-129">Щелкните **Все ресурсы** и выберите созданное пространство имен.</span><span class="sxs-lookup"><span data-stu-id="c2dc2-129">Click **All resources**, and then click the namespace that you created.</span></span>

   ![Выбор пространства имен концентратора событий Azure][IMG03]

1. <span data-ttu-id="c2dc2-131">Щелкните **Центры событий**, а затем **+Концентратор событий**.</span><span class="sxs-lookup"><span data-stu-id="c2dc2-131">Click **Event Hubs**, and then click **+Event Hub**.</span></span>

   ![Добавление нового концентратора событий][IMG04]

1. <span data-ttu-id="c2dc2-133">В области **Создание концентратора событий** введите уникальное **имя** для концентратора событий и щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="c2dc2-133">On the **Create Event Hub** page, enter a unique **Name** for your Event Hub, and then click **Create**.</span></span>

   ![Создание концентратора событий Azure][IMG05]

1. <span data-ttu-id="c2dc2-135">Созданный концентратор событий появится в списке на странице **Центры событий**.</span><span class="sxs-lookup"><span data-stu-id="c2dc2-135">When your Event Hub has been created, it will be listed on the **Event Hubs** page.</span></span>

   ![Создание концентратора событий Azure][IMG06]

### <a name="create-an-azure-storage-account-for-your-event-hub-checkpoints"></a><span data-ttu-id="c2dc2-137">Создание учетной записи хранения для контрольных точек концентратора событий</span><span class="sxs-lookup"><span data-stu-id="c2dc2-137">Create an Azure Storage Account for your Event Hub checkpoints</span></span>

1. <span data-ttu-id="c2dc2-138">Перейдите на портал Azure по адресу <https://portal.azure.com/>.</span><span class="sxs-lookup"><span data-stu-id="c2dc2-138">Browse to the Azure portal at <https://portal.azure.com/>.</span></span>

1. <span data-ttu-id="c2dc2-139">Щелкните **+Создать ресурс**, **Служба хранилища**, **Учетная запись хранения**.</span><span class="sxs-lookup"><span data-stu-id="c2dc2-139">Click **+Create a resource**, then **Storage**, and then click **Storage Account**.</span></span>

   ![Создание учетной записи хранения Azure][IMG07]

1. <span data-ttu-id="c2dc2-141">На странице **Создание пространства имен** введите такую информацию:</span><span class="sxs-lookup"><span data-stu-id="c2dc2-141">On the **Create Namespace** page, enter the following information:</span></span>

   * <span data-ttu-id="c2dc2-142">Уникальное **имя**, которое станет частью URI для учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="c2dc2-142">Enter a unique **Name**, which will become part of the URI for your storage account.</span></span> <span data-ttu-id="c2dc2-143">Например, если вы зададите **wingtiptoys** в качестве **имени**, URI примет вид *wingtiptoys.core.windows.net*.</span><span class="sxs-lookup"><span data-stu-id="c2dc2-143">For example: if you entered **wingtiptoys** for the **Name**, the URI would be *wingtiptoys.core.windows.net*.</span></span>
   * <span data-ttu-id="c2dc2-144">Выберите **Хранилище BLOB-объектов** в поле **Тип учетной записи**.</span><span class="sxs-lookup"><span data-stu-id="c2dc2-144">Choose **Blob storage** for the **Account kind**.</span></span>
   * <span data-ttu-id="c2dc2-145">Укажите **расположение** для учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="c2dc2-145">Specify the **Location** for your storage account.</span></span>
   * <span data-ttu-id="c2dc2-146">Выберите **подписку**, которую нужно использовать для учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="c2dc2-146">Choose the **Subscription** you want to use for your storage account.</span></span>
   * <span data-ttu-id="c2dc2-147">Укажите, следует ли создать новую **группу ресурсов** для учетной записи хранения или использовать существующую.</span><span class="sxs-lookup"><span data-stu-id="c2dc2-147">Specify whether to create a new **Resource group** for your storage account, or choose an existing resource group.</span></span>

   ![Создание учетной записи хранения Azure][IMG08]

1. <span data-ttu-id="c2dc2-149">Указав эти параметры, щелкните **Создать**, чтобы создать учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="c2dc2-149">When you have specified the options listed above, click **Create** to create your storage account.</span></span>

## <a name="create-a-simple-spring-boot-application-with-the-spring-initializr"></a><span data-ttu-id="c2dc2-150">Создание простого приложения Spring Boot с помощью Spring Initializr</span><span class="sxs-lookup"><span data-stu-id="c2dc2-150">Create a simple Spring Boot application with the Spring Initializr</span></span>

1. <span data-ttu-id="c2dc2-151">Перейдите по адресу <https://start.spring.io/>.</span><span class="sxs-lookup"><span data-stu-id="c2dc2-151">Browse to <https://start.spring.io/>.</span></span>

1. <span data-ttu-id="c2dc2-152">Задайте такие параметры:</span><span class="sxs-lookup"><span data-stu-id="c2dc2-152">Specify the following options:</span></span>

   * <span data-ttu-id="c2dc2-153">Выберите в соответствующих полях **Maven Project** (Проект Maven) и **Java**.</span><span class="sxs-lookup"><span data-stu-id="c2dc2-153">Generate a **Maven** project with **Java**.</span></span>
   * <span data-ttu-id="c2dc2-154">Выберите версию **Spring Boot** не ниже версии 2.0.</span><span class="sxs-lookup"><span data-stu-id="c2dc2-154">Specify a **Spring Boot** version that is equal to or greater than 2.0.</span></span>
   * <span data-ttu-id="c2dc2-155">Заполните поля **Group** (Группа) и **Artifact** (Артефакт) для приложения.</span><span class="sxs-lookup"><span data-stu-id="c2dc2-155">Specify the **Group** and **Artifact** names for your application.</span></span>
   * <span data-ttu-id="c2dc2-156">Добавьте зависимость **Web** (Веб).</span><span class="sxs-lookup"><span data-stu-id="c2dc2-156">Add the **Web** dependency.</span></span>

      ![Основные параметры Spring Initializr][SI01]

   > [!NOTE]
   >
   > <span data-ttu-id="c2dc2-158">Spring Initializr использует имена в полях **Group** (Группа) и **Artifact** (Артефакт) для создания имени пакета, например *com.example.wintiptoys*.</span><span class="sxs-lookup"><span data-stu-id="c2dc2-158">The Spring Initializr uses the **Group** and **Artifact** names to create the package name; for example: *com.wingtiptoys.eventhub*.</span></span>
   >

1. <span data-ttu-id="c2dc2-159">Указав эти параметры, щелкните **Generate Project** (Создать проект).</span><span class="sxs-lookup"><span data-stu-id="c2dc2-159">When you have specified the options listed above, click **Generate Project**.</span></span>

1. <span data-ttu-id="c2dc2-160">При появлении запроса скачайте проект на локальный компьютер.</span><span class="sxs-lookup"><span data-stu-id="c2dc2-160">When prompted, download the project to a path on your local computer.</span></span>

   ![Скачивание проекта Spring][SI02]

1. <span data-ttu-id="c2dc2-162">После извлечения файлов в локальной системе простое приложение Spring Boot можно будет редактировать.</span><span class="sxs-lookup"><span data-stu-id="c2dc2-162">After you have extracted the files on your local system, your simple Spring Boot application will be ready for editing.</span></span>

## <a name="configure-your-spring-boot-app-to-use-the-azure-event-hub-starter"></a><span data-ttu-id="c2dc2-163">Настройка приложения Spring Boot для использования начального приложения концентратора событий Azure</span><span class="sxs-lookup"><span data-stu-id="c2dc2-163">Configure your Spring Boot app to use the Azure Event Hub starter</span></span>

1. <span data-ttu-id="c2dc2-164">Найдите файл *pom.xml* в корневой папке приложения, например так:</span><span class="sxs-lookup"><span data-stu-id="c2dc2-164">Locate the *pom.xml* file in the root directory of your app; for example:</span></span>

   `C:\SpringBoot\eventhub\pom.xml`

   <span data-ttu-id="c2dc2-165">-или-</span><span class="sxs-lookup"><span data-stu-id="c2dc2-165">-or-</span></span>

   `/users/example/home/eventhub/pom.xml`

1. <span data-ttu-id="c2dc2-166">Откройте файл *pom.xml* в текстовом редакторе и добавьте начальное приложение Spring Cloud Stream Binder для концентратора событий Azure в список `<dependencies>`:</span><span class="sxs-lookup"><span data-stu-id="c2dc2-166">Open the *pom.xml* file in a text editor, and add the Spring Cloud Azure Event Hub Stream Binder starter to the list of `<dependencies>`:</span></span>

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>spring-cloud-azure-eventhub-stream-binder</artifactId>
      <version>1.0.0.M2</version>
   </dependency>
   ```

   ![Редактирование файла pom.xml][SI03]

1. <span data-ttu-id="c2dc2-168">Сохраните и закройте файл *pom.xml*.</span><span class="sxs-lookup"><span data-stu-id="c2dc2-168">Save and close the *pom.xml* file.</span></span>

## <a name="create-an-azure-credential-file"></a><span data-ttu-id="c2dc2-169">Создание файла учетных данных Azure</span><span class="sxs-lookup"><span data-stu-id="c2dc2-169">Create an Azure Credential File</span></span>

1. <span data-ttu-id="c2dc2-170">Откройте окно командной строки.</span><span class="sxs-lookup"><span data-stu-id="c2dc2-170">Open a command prompt.</span></span>

1. <span data-ttu-id="c2dc2-171">Перейдите к каталогу *resources* приложения Spring Boot, например так:</span><span class="sxs-lookup"><span data-stu-id="c2dc2-171">Navigate to the *resources* directory of your Spring Boot app; for example:</span></span>

   ```shell
   cd C:\SpringBoot\eventhub\src\main\resources
   ```

   <span data-ttu-id="c2dc2-172">-или-</span><span class="sxs-lookup"><span data-stu-id="c2dc2-172">-or-</span></span>

   ```shell
   cd /users/example/home/eventhub/src/main/resources
   ```

1. <span data-ttu-id="c2dc2-173">Вход в учетную запись Azure:</span><span class="sxs-lookup"><span data-stu-id="c2dc2-173">Sign in to your Azure account:</span></span>

   ```azurecli
   az login
   ```

1. <span data-ttu-id="c2dc2-174">Отобразите список подписок:</span><span class="sxs-lookup"><span data-stu-id="c2dc2-174">List your subscriptions:</span></span>

   ```azurecli
   az account list
   ```
   <span data-ttu-id="c2dc2-175">Azure отобразит список подписок, и вам нужно будет скопировать идентификатор GUID для подписки, которая будет использоваться, например:</span><span class="sxs-lookup"><span data-stu-id="c2dc2-175">Azure will return a list of your subscriptions, and you will need to copy the GUID for the subscription that you want to use; for example:</span></span>

   ```json
   [
     {
       "cloudName": "AzureCloud",
       "id": "11111111-1111-1111-1111-111111111111",
       "isDefault": true,
       "name": "Converted Windows Azure MSDN - Visual Studio Ultimate",
       "state": "Enabled",
       "tenantId": "22222222-2222-2222-2222-222222222222",
       "user": {
         "name": "gena.soto@wingtiptoys.com",
         "type": "user"
       }
     }
   ]
   ```
1. <span data-ttu-id="c2dc2-176">Укажите GUID подписки, которую вы собираетесь использовать в Azure, например:</span><span class="sxs-lookup"><span data-stu-id="c2dc2-176">Specify the GUID for the subscription you want to use with Azure; for example:</span></span>

   ```azurecli
   az account set -s 11111111-1111-1111-1111-111111111111
   ```

1. <span data-ttu-id="c2dc2-177">Создайте файл учетных данных Azure:</span><span class="sxs-lookup"><span data-stu-id="c2dc2-177">Create your Azure Credential file:</span></span>

   ```azurecli
   az ad sp create-for-rbac --sdk-auth > my.azureauth
   ```

   <span data-ttu-id="c2dc2-178">Эта команда создаст файл *my.azureauth* в каталоге *resources* приблизительно с таким содержимым:</span><span class="sxs-lookup"><span data-stu-id="c2dc2-178">This command will create a *my.azureauth* file in your *resources* directory with contents that resemble the following example:</span></span>

   ```json
   {
     "clientId": "33333333-3333-3333-3333-333333333333",
     "clientSecret": "44444444-4444-4444-4444-444444444444",
     "subscriptionId": "11111111-1111-1111-1111-111111111111",
     "tenantId": "22222222-2222-2222-2222-222222222222",
     "activeDirectoryEndpointUrl": "https://login.microsoftonline.com",
     "resourceManagerEndpointUrl": "https://management.azure.com/",
     "activeDirectoryGraphResourceId": "https://graph.windows.net/",
     "sqlManagementEndpointUrl": "https://management.core.windows.net:8443/",
     "galleryEndpointUrl": "https://gallery.azure.com/",
     "managementEndpointUrl": "https://management.core.windows.net/"
   }
   ```

## <a name="configure-your-spring-boot-app-to-use-your-azure-event-hub"></a><span data-ttu-id="c2dc2-179">Настройка приложения Spring Boot для использования концентратора событий Azure</span><span class="sxs-lookup"><span data-stu-id="c2dc2-179">Configure your Spring Boot app to use your Azure Event Hub</span></span>

1. <span data-ttu-id="c2dc2-180">Найдите файл *application.properties* в каталоге *resources* приложения, например так:</span><span class="sxs-lookup"><span data-stu-id="c2dc2-180">Locate the *application.properties* in the *resources* directory of your app; for example:</span></span>

   `C:\SpringBoot\eventhub\src\main\resources\application.properties`

   <span data-ttu-id="c2dc2-181">-или-</span><span class="sxs-lookup"><span data-stu-id="c2dc2-181">-or-</span></span>

   `/users/example/home/eventhub/src/main/resources/application.properties`

2. <span data-ttu-id="c2dc2-182">Откройте файл *application.properties* в текстовом редакторе, добавьте следующие строки и замените примеры значений соответствующими параметрами концентратора событий:</span><span class="sxs-lookup"><span data-stu-id="c2dc2-182">Open the *application.properties* file in a text editor, add the following lines, and then replace the sample values with the appropriate properties for your event hub:</span></span>

   ```yaml
   spring.cloud.azure.credential-file-path=my.azureauth
   spring.cloud.azure.resource-group=wingtiptoysresources
   spring.cloud.azure.region=West US
   spring.cloud.azure.eventhub.namespace=wingtiptoysnamespace
   spring.cloud.azure.eventhub.checkpoint-storage-account=wingtiptoysstorage
   spring.cloud.stream.bindings.input.destination=wingtiptoyshub
   spring.cloud.stream.bindings.input.group=$Default
   spring.cloud.stream.bindings.output.destination=wingtiptoyshub
   spring.cloud.stream.eventhub.bindings.input.consumer.checkpoint-mode=MANUAL
   ```
   <span data-ttu-id="c2dc2-183">Описание</span><span class="sxs-lookup"><span data-stu-id="c2dc2-183">Where:</span></span>

   |                          <span data-ttu-id="c2dc2-184">Поле</span><span class="sxs-lookup"><span data-stu-id="c2dc2-184">Field</span></span>                           |                                                                                   <span data-ttu-id="c2dc2-185">ОПИСАНИЕ</span><span class="sxs-lookup"><span data-stu-id="c2dc2-185">Description</span></span>                                                                                    |
   |----------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
   |        `spring.cloud.azure.credential-file-path`         |                                                    <span data-ttu-id="c2dc2-186">Определяет файл учетных данных Azure, который был создан ранее в этом примере.</span><span class="sxs-lookup"><span data-stu-id="c2dc2-186">Specifies Azure credential file that you created earlier in this tutorial.</span></span>                                                    |
   |           `spring.cloud.azure.resource-group`            |                                                      <span data-ttu-id="c2dc2-187">Определяет группу ресурсов Azure, которая содержит концентратор событий Azure.</span><span class="sxs-lookup"><span data-stu-id="c2dc2-187">Specifies the Azure Resource Group that contains your Azure Event Hub.</span></span>                                                      |
   |               `spring.cloud.azure.region`                |                                           <span data-ttu-id="c2dc2-188">Определяет географический регион, указанный при создании концентратора событий Azure.</span><span class="sxs-lookup"><span data-stu-id="c2dc2-188">Specifies the geographical region that you specified when you created your Azure Event Hub.</span></span>                                            |
   |         `spring.cloud.azure.eventhub.namespace`          |                                          <span data-ttu-id="c2dc2-189">Определяет уникальное имя, заданное при создании пространства имен концентратора событий Azure.</span><span class="sxs-lookup"><span data-stu-id="c2dc2-189">Specifies the unique name that you specified when you created your Azure Event Hub Namespace.</span></span>                                           |
   | `spring.cloud.azure.eventhub.checkpoint-storage-account` |                                                    <span data-ttu-id="c2dc2-190">Определяет учетную запись хранения Azure, которая была создана ранее в этом примере.</span><span class="sxs-lookup"><span data-stu-id="c2dc2-190">Specifies Azure Storage Account that you created earlier in this tutorial.</span></span>                                                    |
   |     `spring.cloud.stream.bindings.input.destination`     |                            <span data-ttu-id="c2dc2-191">Определяет назначение входящих данных концентратора событий Azure, которым в этом примере является сам концентратор, созданный ранее.</span><span class="sxs-lookup"><span data-stu-id="c2dc2-191">Specifies the input destination Azure Event Hub, which for this tutorial is the  hub you created earlier in this tutorial.</span></span>                            |
   |       `spring.cloud.stream.bindings.input.group `        | <span data-ttu-id="c2dc2-192">Определяет группу потребителей концентратора событий Azure, для которой можно установить значение $Default, чтобы использовать базовую группу потребителей, созданную вместе с концентратором событий Azure.</span><span class="sxs-lookup"><span data-stu-id="c2dc2-192">Specifies a Consumer Group from Azure Event Hub, which can be set to '$Default' in order to use the basic consumer group that was created when you created your Azure Event Hub.</span></span> |
   |    `spring.cloud.stream.bindings.output.destination`     |                               <span data-ttu-id="c2dc2-193">Определяет назначение исходящих данных для концентратора событий Azure, которое в этом примере совпадает с назначением входящих данных.</span><span class="sxs-lookup"><span data-stu-id="c2dc2-193">Specifies the output destination Azure Event Hub, which for this tutorial will be the same as the input destination.</span></span>                               |


3. <span data-ttu-id="c2dc2-194">Сохраните и закройте файл *application.properties*.</span><span class="sxs-lookup"><span data-stu-id="c2dc2-194">Save and close the *application.properties* file.</span></span>

## <a name="add-sample-code-to-implement-basic-event-hub-functionality"></a><span data-ttu-id="c2dc2-195">Добавление примера кода для реализации базовых функций концентратора событий</span><span class="sxs-lookup"><span data-stu-id="c2dc2-195">Add sample code to implement basic event hub functionality</span></span>

<span data-ttu-id="c2dc2-196">В этом разделе вы создадите классы Java, требуемые для отправки событий в концентратор событий.</span><span class="sxs-lookup"><span data-stu-id="c2dc2-196">In this section, you create the necessary Java classes for sending events to your event hub.</span></span>

### <a name="modify-the-main-application-class"></a><span data-ttu-id="c2dc2-197">Изменение класса основного приложения</span><span class="sxs-lookup"><span data-stu-id="c2dc2-197">Modify the main application class</span></span>

1. <span data-ttu-id="c2dc2-198">Найдите файл основного приложения Java в каталоге пакета приложения, например:</span><span class="sxs-lookup"><span data-stu-id="c2dc2-198">Locate the main application Java file in the package directory of your app; for example:</span></span>

   `C:\SpringBoot\eventhub\src\main\java\com\wingtiptoys\eventhub\EventhubApplication.java`

   <span data-ttu-id="c2dc2-199">-или-</span><span class="sxs-lookup"><span data-stu-id="c2dc2-199">-or-</span></span>

   `/users/example/home/eventhub/src/main/java/com/wingtiptoys/eventhub/EventhubApplication.java`

1. <span data-ttu-id="c2dc2-200">Откройте файл основного приложения Java в текстовом редакторе и добавьте в него следующие строки:</span><span class="sxs-lookup"><span data-stu-id="c2dc2-200">Open the main application Java file in a text editor, and add the following lines to the file:</span></span>

   ```java
   package com.wingtiptoys.eventhub;

   import org.springframework.boot.SpringApplication;
   import org.springframework.boot.autoconfigure.SpringBootApplication;

   @SpringBootApplication
   public class EventhubApplication {
      public static void main(String[] args) {
         SpringApplication.run(EventhubApplication.class, args);
      }
   }
   ```

1. <span data-ttu-id="c2dc2-201">Сохраните и закройте файл основного приложения Java.</span><span class="sxs-lookup"><span data-stu-id="c2dc2-201">Save and close the main application Java file.</span></span>

### <a name="create-a-new-class-for-the-source-connector"></a><span data-ttu-id="c2dc2-202">Создание класса для соединителя источника</span><span class="sxs-lookup"><span data-stu-id="c2dc2-202">Create a new class for the source connector</span></span>

1. <span data-ttu-id="c2dc2-203">В каталоге пакета приложения создайте файл Java с именем *EventhubSource.java*, а затем откройте этот файл в текстовом редакторе и добавьте следующие строки:</span><span class="sxs-lookup"><span data-stu-id="c2dc2-203">Create a new Java file named *EventhubSource.java* in the package directory of your app, then open the file in a text editor and add the following lines:</span></span>

   ```java
   package com.wingtiptoys.eventhub;

   import org.springframework.beans.factory.annotation.Autowired;
   import org.springframework.cloud.stream.annotation.EnableBinding;
   import org.springframework.cloud.stream.messaging.Source;
   import org.springframework.messaging.support.GenericMessage;
   import org.springframework.web.bind.annotation.PostMapping;
   import org.springframework.web.bind.annotation.RequestBody;
   import org.springframework.web.bind.annotation.RestController;

   @EnableBinding(Source.class)
   @RestController
   public class EventhubSource {

      @Autowired
      private Source source;

      @PostMapping("/messages")
      public String postMessage(@RequestBody String message) {
         this.source.output().send(new GenericMessage<>(message));
         return message;
      }
   }
   ```
1. <span data-ttu-id="c2dc2-204">Сохраните и закройте файл *EventhubSource.java*.</span><span class="sxs-lookup"><span data-stu-id="c2dc2-204">Save and close the *EventhubSource.java* file.</span></span>

### <a name="create-a-new-class-for-the-sink-connector"></a><span data-ttu-id="c2dc2-205">Создание класса для соединителя приемника</span><span class="sxs-lookup"><span data-stu-id="c2dc2-205">Create a new class for the sink connector</span></span>

1. <span data-ttu-id="c2dc2-206">В каталоге пакета приложения создайте файл Java с именем *EventhubSink.java*, а затем откройте этот файл в текстовом редакторе и добавьте следующие строки:</span><span class="sxs-lookup"><span data-stu-id="c2dc2-206">Create a new Java file named *EventhubSink.java* in the package directory of your app, then open the file in a text editor and add the following lines:</span></span>

   ```java
   package com.wingtiptoys.eventhub;

   import com.microsoft.azure.spring.integration.core.AzureHeaders;
   import com.microsoft.azure.spring.integration.core.api.Checkpointer;
   import org.slf4j.Logger;
   import org.slf4j.LoggerFactory;
   import org.springframework.cloud.stream.annotation.EnableBinding;
   import org.springframework.cloud.stream.annotation.StreamListener;
   import org.springframework.cloud.stream.messaging.Sink;
   import org.springframework.messaging.handler.annotation.Header;

   @EnableBinding(Sink.class)
   public class EventhubSink {

      private static final Logger LOGGER = LoggerFactory.getLogger(EventhubSink.class);

      @StreamListener(Sink.INPUT)
      public void handleMessage(String message, @Header(AzureHeaders.CHECKPOINTER) Checkpointer checkpointer) {
         LOGGER.info("New message received: '{}'", message);
         checkpointer.success().handle((r, ex) -> {
            if (ex == null) {
               LOGGER.info("Message '{}' successfully checkpointed", message);
            }
            return null;
         });
      }
   }
   ```

1. <span data-ttu-id="c2dc2-207">Сохраните и закройте файл *EventhubSink.java*.</span><span class="sxs-lookup"><span data-stu-id="c2dc2-207">Save and close the *EventhubSink.java* file.</span></span>

## <a name="build-and-test-your-application"></a><span data-ttu-id="c2dc2-208">Сборка и тестирование приложения</span><span class="sxs-lookup"><span data-stu-id="c2dc2-208">Build and test your application</span></span>

1. <span data-ttu-id="c2dc2-209">Откройте командную строку и перейдите из каталога в папку с файлом *pom.xml*, например:</span><span class="sxs-lookup"><span data-stu-id="c2dc2-209">Open a command prompt and change directory to the folder where your *pom.xml* file is located; for example:</span></span>

   `cd C:\SpringBoot\eventhub`

   <span data-ttu-id="c2dc2-210">-или-</span><span class="sxs-lookup"><span data-stu-id="c2dc2-210">-or-</span></span>

   `cd /users/example/home/eventhub`

1. <span data-ttu-id="c2dc2-211">Создайте приложение Spring Boot с помощью Maven и запустите его, например, следующим образом:</span><span class="sxs-lookup"><span data-stu-id="c2dc2-211">Build your Spring Boot application with Maven and run it; for example:</span></span>

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

1. <span data-ttu-id="c2dc2-212">После запуска приложения можно использовать средство *curl*, чтобы протестировать приложение, например:</span><span class="sxs-lookup"><span data-stu-id="c2dc2-212">Once your application is running, you can use *curl* to test your application; for example:</span></span>

   ```shell
   curl -X POST -H "Content-Type: text/plain" -d "hello" http://localhost:8080/messages
   ```
   <span data-ttu-id="c2dc2-213">В журнале приложения должна появиться запись "hello".</span><span class="sxs-lookup"><span data-stu-id="c2dc2-213">You should see "hello" posted to your application's logs.</span></span> <span data-ttu-id="c2dc2-214">Например: </span><span class="sxs-lookup"><span data-stu-id="c2dc2-214">For example:</span></span>

   ```shell
   [Thread-13] INFO com.wingtiptoys.eventhub.EventhubSink - New message received: 'hello'
   [pool-10-thread-7] INFO com.wingtiptoys.eventhub.EventhubSink - Message 'hello' successfully checkpointed
   ```

## <a name="next-steps"></a><span data-ttu-id="c2dc2-215">Дополнительная информация</span><span class="sxs-lookup"><span data-stu-id="c2dc2-215">Next steps</span></span>

<span data-ttu-id="c2dc2-216">Дополнительные сведения о Spring и Azure см. в центре документации об использовании Spring в Azure.</span><span class="sxs-lookup"><span data-stu-id="c2dc2-216">To learn more about Spring and Azure, continue to the Spring on Azure documentation center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c2dc2-217">Spring в Azure</span><span class="sxs-lookup"><span data-stu-id="c2dc2-217">Spring on Azure</span></span>](/java/azure/spring-framework)

### <a name="additional-resources"></a><span data-ttu-id="c2dc2-218">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="c2dc2-218">Additional Resources</span></span>

<span data-ttu-id="c2dc2-219">Дополнительные сведения о поддержке в Azure приложения Event Hub Stream Binder для концентратора событий см. в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="c2dc2-219">For more information about Azure support for Event Hub Stream Binder, see the following articles:</span></span>

* [<span data-ttu-id="c2dc2-220">Что такое Центры событий Azure?</span><span class="sxs-lookup"><span data-stu-id="c2dc2-220">What is Azure Event Hubs?</span></span>](/azure/event-hubs/event-hubs-about)

* [<span data-ttu-id="c2dc2-221">Создание пространства имен службы "Центры событий" и концентратора событий с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="c2dc2-221">Create an Event Hubs namespace and an event hub using the Azure portal</span></span>](/azure/event-hubs/event-hubs-create)

* <span data-ttu-id="c2dc2-222">[How to use the Spring Boot Starter for Apache Kafka with Azure Event Hubs](configure-spring-cloud-stream-binder-java-app-kafka-azure-event-hub.md) (Использование начального приложения Spring Boot для Apache Kafka в Центрах событий)</span><span class="sxs-lookup"><span data-stu-id="c2dc2-222">[How to use the Spring Boot Starter for Apache Kafka with Azure Event Hubs](configure-spring-cloud-stream-binder-java-app-kafka-azure-event-hub.md)</span></span>

<span data-ttu-id="c2dc2-223">Дополнительные сведения об использовании Java в Azure см. в статьях [Azure для разработчиков Java] и [Working with Azure DevOps and Java] (Работа с Azure DevOps и Java).</span><span class="sxs-lookup"><span data-stu-id="c2dc2-223">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Working with Azure DevOps and Java].</span></span>

<span data-ttu-id="c2dc2-224">**[Spring Framework]** — это решение с открытым кодом, которое помогает разработчикам Java создавать приложения корпоративного класса.</span><span class="sxs-lookup"><span data-stu-id="c2dc2-224">The **[Spring Framework]** is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="c2dc2-225">Одним из самых популярных проектов, созданных на этой платформе, является проект [Spring Boot]. Он упрощает подход к созданию автономных приложений Java.</span><span class="sxs-lookup"><span data-stu-id="c2dc2-225">One of the more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating stand-alone Java applications.</span></span> <span data-ttu-id="c2dc2-226">В помощь разработчикам, начинающим работать со Spring Boot, по адресу <https://github.com/spring-guides/> доступно несколько примеров пакетов этого приложения.</span><span class="sxs-lookup"><span data-stu-id="c2dc2-226">To help developers get started with Spring Boot, several sample Spring Boot packages are available at <https://github.com/spring-guides/>.</span></span> <span data-ttu-id="c2dc2-227">Помимо выбора из списка основных проектов Spring Boot, **[Spring Initializr]** помогает разработчикам создавать пользовательские приложения Spring Boot.</span><span class="sxs-lookup"><span data-stu-id="c2dc2-227">In addition to choosing from the list of basic Spring Boot projects, the **[Spring Initializr]** helps developers get started with creating custom Spring Boot applications.</span></span>

<!-- URL List -->

[бесплатной учетной записи Azure]: https://azure.microsoft.com/pricing/free-trial/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[Working with Azure DevOps and Java]: /azure/devops/ (Работа с Azure DevOps и Java)
[Преимущества для подписчиков MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Initializr]: https://start.spring.io/
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[IMG01]: ./media/configure-spring-cloud-stream-binder-java-app-azure-event-hub/create-event-hub-01.png
[IMG02]: ./media/configure-spring-cloud-stream-binder-java-app-azure-event-hub/create-event-hub-02.png
[IMG03]: ./media/configure-spring-cloud-stream-binder-java-app-azure-event-hub/create-event-hub-03.png
[IMG04]: ./media/configure-spring-cloud-stream-binder-java-app-azure-event-hub/create-event-hub-04.png
[IMG05]: ./media/configure-spring-cloud-stream-binder-java-app-azure-event-hub/create-event-hub-05.png
[IMG06]: ./media/configure-spring-cloud-stream-binder-java-app-azure-event-hub/create-event-hub-06.png
[IMG07]: ./media/configure-spring-cloud-stream-binder-java-app-azure-event-hub/create-event-hub-07.png
[IMG08]: ./media/configure-spring-cloud-stream-binder-java-app-azure-event-hub/create-event-hub-08.png

[SI01]: ./media/configure-spring-cloud-stream-binder-java-app-azure-event-hub/create-project-01.png
[SI02]: ./media/configure-spring-cloud-stream-binder-java-app-azure-event-hub/create-project-02.png
[SI03]: ./media/configure-spring-cloud-stream-binder-java-app-azure-event-hub/create-project-03.png
