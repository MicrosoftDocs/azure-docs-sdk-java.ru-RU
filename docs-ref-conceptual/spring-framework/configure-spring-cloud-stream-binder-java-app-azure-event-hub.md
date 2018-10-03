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
ms.date: 09/10/2018
ms.devlang: java
ms.service: event-hubs
ms.tgt_pltfrm: na
ms.topic: article
ms.workload: na
ms.openlocfilehash: 3f7eeffe8bd36196f9b79edd60830b5d202ea285
ms.sourcegitcommit: fd67d4088be2cad01c642b9ecf3f9475d9cb4f3c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/21/2018
ms.locfileid: "46506581"
---
# <a name="how-to-create-a-spring-cloud-stream-binder-application-with-azure-event-hubs"></a><span data-ttu-id="6e3a3-103">Создание приложения Spring Cloud Stream Binder с помощью Центров событий Azure</span><span class="sxs-lookup"><span data-stu-id="6e3a3-103">How to create a Spring Cloud Stream Binder application with Azure Event Hubs</span></span>

## <a name="overview"></a><span data-ttu-id="6e3a3-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="6e3a3-104">Overview</span></span>

<span data-ttu-id="6e3a3-105">В статье показано, как настроить приложение Spring Cloud Stream Binder на основе Java, созданное с помощью Spring Boot Initializr и Центров событий Azure.</span><span class="sxs-lookup"><span data-stu-id="6e3a3-105">This article demonstrates how to configure a Java-based Spring Cloud Stream Binder application created with the Spring Boot Initializer with Azure Event Hubs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6e3a3-106">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="6e3a3-106">Prerequisites</span></span>

<span data-ttu-id="6e3a3-107">Чтобы выполнить действия, описанные в этой статье, необходимо иметь следующие компоненты:</span><span class="sxs-lookup"><span data-stu-id="6e3a3-107">The following prerequisites are required in order to follow the steps in this article:</span></span>

* <span data-ttu-id="6e3a3-108">Подписка Azure. Если у вас ее еще нет, вы можете активировать [Преимущества для подписчиков MSDN] или зарегистрироваться для получения [бесплатной учетной записи Azure].</span><span class="sxs-lookup"><span data-stu-id="6e3a3-108">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="6e3a3-109">[Пакет разработчиков Java (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/) версии 1.7 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="6e3a3-109">A [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), version 1.7 or later.</span></span>
* <span data-ttu-id="6e3a3-110">[Apache Maven](http://maven.apache.org/) версии 3.0 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="6e3a3-110">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>

> [!IMPORTANT]
>
> <span data-ttu-id="6e3a3-111">Для выполнения операций, описанных в этой статье, требуется Spring Boot 2.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="6e3a3-111">Spring Boot version 2.0 or greater is required to complete the steps in this article.</span></span>
>

## <a name="create-an-azure-event-hub-using-the-azure-portal"></a><span data-ttu-id="6e3a3-112">Создание концентратора событий на портале Azure</span><span class="sxs-lookup"><span data-stu-id="6e3a3-112">Create an Azure Event Hub using the Azure portal</span></span>

### <a name="create-an-azure-event-hub-namespace"></a><span data-ttu-id="6e3a3-113">Создание пространства имен концентратора событий Azure</span><span class="sxs-lookup"><span data-stu-id="6e3a3-113">Create an Azure Event Hub Namespace</span></span>

1. <span data-ttu-id="6e3a3-114">Перейдите на портал Azure по адресу <https://portal.azure.com/> и выполните вход.</span><span class="sxs-lookup"><span data-stu-id="6e3a3-114">Browse to the Azure portal at <https://portal.azure.com/> and sign in.</span></span>

1. <span data-ttu-id="6e3a3-115">Выберите **+Создать ресурс**, **Интернет вещей** и **Центры событий**.</span><span class="sxs-lookup"><span data-stu-id="6e3a3-115">Click **+Create a resource**, then **Internet of Things**, and then click **Event Hubs**.</span></span>

   ![Создание пространства имен концентратора событий Azure][IMG01]

1. <span data-ttu-id="6e3a3-117">На странице **Создание пространства имен** введите такую информацию:</span><span class="sxs-lookup"><span data-stu-id="6e3a3-117">On the **Create Namespace** page, enter the following information:</span></span>

   * <span data-ttu-id="6e3a3-118">Уникальное **имя**, которое станет частью URI для пространства имен концентратора событий.</span><span class="sxs-lookup"><span data-stu-id="6e3a3-118">Enter a unique **Name**, which will become part of the URI for your event hub namespace.</span></span> <span data-ttu-id="6e3a3-119">Например, если вы зададите **wingtiptoys** в качестве **имени**, URI примет вид *wingtiptoys.servicebus.windows.net*.</span><span class="sxs-lookup"><span data-stu-id="6e3a3-119">For example: if you entered **wingtiptoys** for the **Name**, the URI would be *wingtiptoys.servicebus.windows.net*.</span></span>
   * <span data-ttu-id="6e3a3-120">Выберите **ценовую категорию** для пространства имен концентратора событий.</span><span class="sxs-lookup"><span data-stu-id="6e3a3-120">Choose a **Pricing tier** for your event hub namespace.</span></span>
   * <span data-ttu-id="6e3a3-121">Выберите **подписку** для пространства имен.</span><span class="sxs-lookup"><span data-stu-id="6e3a3-121">Choose the **Subscription** you want to use for your namespace.</span></span>
   * <span data-ttu-id="6e3a3-122">Укажите, следует ли создать новую **группу ресурсов** для пространства имен или использовать существующую.</span><span class="sxs-lookup"><span data-stu-id="6e3a3-122">Specify whether to create a new **Resource group** for your namespace, or choose an existing resource group.</span></span>
   * <span data-ttu-id="6e3a3-123">Укажите **расположение** для пространства имен Центров событий.</span><span class="sxs-lookup"><span data-stu-id="6e3a3-123">Specify the **Location** for your event hub namespace.</span></span>
   
   ![Создание пространства имен для концентратора событий Azure][IMG02]

1. <span data-ttu-id="6e3a3-125">Указав эти параметры, щелкните **Создать**, чтобы создать пространство имен.</span><span class="sxs-lookup"><span data-stu-id="6e3a3-125">When you have specified the options listed above, click **Create** to create your namespace.</span></span>

### <a name="create-an-azure-event-hub-in-your-namespace"></a><span data-ttu-id="6e3a3-126">Создание концентратора событий Azure в пространстве имен</span><span class="sxs-lookup"><span data-stu-id="6e3a3-126">Create an Azure Event Hub in your namespace</span></span>

1. <span data-ttu-id="6e3a3-127">Перейдите на портал Azure по адресу <https://portal.azure.com/>.</span><span class="sxs-lookup"><span data-stu-id="6e3a3-127">Browse to the Azure portal at <https://portal.azure.com/>.</span></span>

1. <span data-ttu-id="6e3a3-128">Щелкните **Все ресурсы** и выберите созданное пространство имен.</span><span class="sxs-lookup"><span data-stu-id="6e3a3-128">Click **All resources**, and then click the namespace that you created.</span></span>

   ![Выбор пространства имен концентратора событий Azure][IMG03]

1. <span data-ttu-id="6e3a3-130">Щелкните **Центры событий**, а затем **+Концентратор событий**.</span><span class="sxs-lookup"><span data-stu-id="6e3a3-130">Click **Event Hubs**, and then click **+Event Hub**.</span></span>

   ![Добавление нового концентратора событий Azure][IMG04]

1. <span data-ttu-id="6e3a3-132">В области **Создание концентратора событий** введите уникальное **имя** для концентратора событий и щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="6e3a3-132">On the **Create Event Hub** page, enter a unique **Name** for your Event Hub, and then click **Create**.</span></span>

   ![Создание концентратора событий Azure][IMG05]

1. <span data-ttu-id="6e3a3-134">Созданный концентратор событий появится в списке на странице **Центры событий**.</span><span class="sxs-lookup"><span data-stu-id="6e3a3-134">When your Event Hub has been created, it will be listed on the **Event Hubs** page.</span></span>

   ![Создание концентратора событий Azure][IMG06]

### <a name="create-an-azure-storage-account-for-your-event-hub-checkpoints"></a><span data-ttu-id="6e3a3-136">Создание учетной записи хранения для контрольных точек концентратора событий</span><span class="sxs-lookup"><span data-stu-id="6e3a3-136">Create an Azure Storage Account for your Event Hub checkpoints</span></span>

1. <span data-ttu-id="6e3a3-137">Перейдите на портал Azure по адресу <https://portal.azure.com/>.</span><span class="sxs-lookup"><span data-stu-id="6e3a3-137">Browse to the Azure portal at <https://portal.azure.com/>.</span></span>

1. <span data-ttu-id="6e3a3-138">Щелкните **+Создать ресурс**, **Служба хранилища**, **Учетная запись хранения**.</span><span class="sxs-lookup"><span data-stu-id="6e3a3-138">Click **+Create a resource**, then **Storage**, and then click **Storage Account**.</span></span>

   ![Создание учетной записи хранения Azure][IMG07]

1. <span data-ttu-id="6e3a3-140">На странице **Создание пространства имен** введите такую информацию:</span><span class="sxs-lookup"><span data-stu-id="6e3a3-140">On the **Create Namespace** page, enter the following information:</span></span>

   * <span data-ttu-id="6e3a3-141">Уникальное **имя**, которое станет частью URI для учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="6e3a3-141">Enter a unique **Name**, which will become part of the URI for your storage account.</span></span> <span data-ttu-id="6e3a3-142">Например, если вы зададите **wingtiptoys** в качестве **имени**, URI примет вид *wingtiptoys.core.windows.net*.</span><span class="sxs-lookup"><span data-stu-id="6e3a3-142">For example: if you entered **wingtiptoys** for the **Name**, the URI would be *wingtiptoys.core.windows.net*.</span></span>
   * <span data-ttu-id="6e3a3-143">Выберите **Хранилище BLOB-объектов** в поле **Тип учетной записи**.</span><span class="sxs-lookup"><span data-stu-id="6e3a3-143">Choose **Blob storage** for the **Account kind**.</span></span>
   * <span data-ttu-id="6e3a3-144">Укажите **расположение** для учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="6e3a3-144">Specify the **Location** for your storage account.</span></span>
   * <span data-ttu-id="6e3a3-145">Выберите **подписку**, которую нужно использовать для учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="6e3a3-145">Choose the **Subscription** you want to use for your storage account.</span></span>
   * <span data-ttu-id="6e3a3-146">Укажите, следует ли создать новую **группу ресурсов** для учетной записи хранения или использовать существующую.</span><span class="sxs-lookup"><span data-stu-id="6e3a3-146">Specify whether to create a new **Resource group** for your storage account, or choose an existing resource group.</span></span>
   
   ![Создание учетной записи хранения][IMG08]

1. <span data-ttu-id="6e3a3-148">Указав эти параметры, щелкните **Создать**, чтобы создать учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="6e3a3-148">When you have specified the options listed above, click **Create** to create your storage account.</span></span>

## <a name="create-a-simple-spring-boot-application-with-the-spring-initializr"></a><span data-ttu-id="6e3a3-149">Создание простого приложения Spring Boot с помощью Spring Initializr</span><span class="sxs-lookup"><span data-stu-id="6e3a3-149">Create a simple Spring Boot application with the Spring Initializr</span></span>

1. <span data-ttu-id="6e3a3-150">Перейдите по адресу <https://start.spring.io/>.</span><span class="sxs-lookup"><span data-stu-id="6e3a3-150">Browse to <https://start.spring.io/>.</span></span>

1. <span data-ttu-id="6e3a3-151">Задайте такие параметры:</span><span class="sxs-lookup"><span data-stu-id="6e3a3-151">Specify the following options:</span></span>

   * <span data-ttu-id="6e3a3-152">Выберите в соответствующих полях **Maven Project** (Проект Maven) и **Java**.</span><span class="sxs-lookup"><span data-stu-id="6e3a3-152">Generate a **Maven** project with **Java**.</span></span>
   * <span data-ttu-id="6e3a3-153">Выберите версию **Spring Boot** не ниже версии 2.0.</span><span class="sxs-lookup"><span data-stu-id="6e3a3-153">Specify a **Spring Boot** version that is equal to or greater than 2.0.</span></span>
   * <span data-ttu-id="6e3a3-154">Заполните поля **Group** (Группа) и **Artifact** (Артефакт) для приложения.</span><span class="sxs-lookup"><span data-stu-id="6e3a3-154">Specify the **Group** and **Artifact** names for your application.</span></span>
   * <span data-ttu-id="6e3a3-155">Добавьте зависимость **Web** (Веб).</span><span class="sxs-lookup"><span data-stu-id="6e3a3-155">Add the **Web** dependency.</span></span>

      ![Основные параметры Spring Initializr][SI01]

   > [!NOTE]
   >
   > <span data-ttu-id="6e3a3-157">Spring Initializr использует имена в полях **Group** (Группа) и **Artifact** (Артефакт) для создания имени пакета, например *com.example.wintiptoys*.</span><span class="sxs-lookup"><span data-stu-id="6e3a3-157">The Spring Initializr uses the **Group** and **Artifact** names to create the package name; for example: *com.wingtiptoys.eventhub*.</span></span>
   >

1. <span data-ttu-id="6e3a3-158">Указав эти параметры, щелкните **Generate Project** (Создать проект).</span><span class="sxs-lookup"><span data-stu-id="6e3a3-158">When you have specified the options listed above, click **Generate Project**.</span></span>

1. <span data-ttu-id="6e3a3-159">При появлении запроса скачайте проект на локальный компьютер.</span><span class="sxs-lookup"><span data-stu-id="6e3a3-159">When prompted, download the project to a path on your local computer.</span></span>

   ![Скачивание проекта Spring][SI02]

1. <span data-ttu-id="6e3a3-161">После извлечения файлов в локальной системе простое приложение Spring Boot можно будет редактировать.</span><span class="sxs-lookup"><span data-stu-id="6e3a3-161">After you have extracted the files on your local system, your simple Spring Boot application will be ready for editing.</span></span>

## <a name="configure-your-spring-boot-app-to-use-the-azure-event-hub-starter"></a><span data-ttu-id="6e3a3-162">Настройка приложения Spring Boot для использования начального приложения концентратора событий Azure</span><span class="sxs-lookup"><span data-stu-id="6e3a3-162">Configure your Spring Boot app to use the Azure Event Hub starter</span></span>

1. <span data-ttu-id="6e3a3-163">Найдите файл *pom.xml* в корневой папке приложения, например так:</span><span class="sxs-lookup"><span data-stu-id="6e3a3-163">Locate the *pom.xml* file in the root directory of your app; for example:</span></span>

   `C:\SpringBoot\eventhub\pom.xml`

   <span data-ttu-id="6e3a3-164">-или-</span><span class="sxs-lookup"><span data-stu-id="6e3a3-164">-or-</span></span>

   `/users/example/home/eventhub/pom.xml`

1. <span data-ttu-id="6e3a3-165">Откройте файл *pom.xml* в текстовом редакторе и добавьте начальное приложение Spring Cloud Stream Binder для концентратора событий Azure в список `<dependencies>`:</span><span class="sxs-lookup"><span data-stu-id="6e3a3-165">Open the *pom.xml* file in a text editor, and add the Spring Cloud Azure Event Hub Stream Binder starter to the list of `<dependencies>`:</span></span>

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>spring-cloud-azure-eventhub-stream-binder</artifactId>
      <version>1.0.0.M2</version>
   </dependency>
   ```

   ![Редактирование файла pom.xml][SI03]

1. <span data-ttu-id="6e3a3-167">Сохраните и закройте файл *pom.xml*.</span><span class="sxs-lookup"><span data-stu-id="6e3a3-167">Save and close the *pom.xml* file.</span></span>

## <a name="create-an-azure-credential-file"></a><span data-ttu-id="6e3a3-168">Создание файла учетных данных Azure</span><span class="sxs-lookup"><span data-stu-id="6e3a3-168">Create an Azure Credential File</span></span>

1. <span data-ttu-id="6e3a3-169">Откройте окно командной строки.</span><span class="sxs-lookup"><span data-stu-id="6e3a3-169">Open a command prompt.</span></span>

1. <span data-ttu-id="6e3a3-170">Перейдите к каталогу *resources* приложения Spring Boot, например так:</span><span class="sxs-lookup"><span data-stu-id="6e3a3-170">Navigate to the *resources* directory of your Spring Boot app; for example:</span></span>

   ```shell
   cd C:\SpringBoot\eventhub\src\main\resources
   ```

   <span data-ttu-id="6e3a3-171">-или-</span><span class="sxs-lookup"><span data-stu-id="6e3a3-171">-or-</span></span>

   ```shell
   cd /users/example/home/eventhub/src/main/resources
   ```

1. <span data-ttu-id="6e3a3-172">Вход в учетную запись Azure:</span><span class="sxs-lookup"><span data-stu-id="6e3a3-172">Sign in to your Azure account:</span></span>

   ```azurecli
   az login
   ```

1. <span data-ttu-id="6e3a3-173">Отобразите список подписок:</span><span class="sxs-lookup"><span data-stu-id="6e3a3-173">List your subscriptions:</span></span>

   ```azurecli
   az account list
   ```
   <span data-ttu-id="6e3a3-174">Azure отобразит список подписок, и вам нужно будет скопировать идентификатор GUID для подписки, которая будет использоваться, например:</span><span class="sxs-lookup"><span data-stu-id="6e3a3-174">Azure will return a list of your subscriptions, and you will need to copy the GUID for the subscription that you want to use; for example:</span></span>

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

1. Specify the GUID for the subscription you want to use with Azure; for example:

   ```azurecli
   az account set -s 11111111-1111-1111-1111-111111111111
   ```

1. <span data-ttu-id="6e3a3-175">Создайте файл учетных данных Azure:</span><span class="sxs-lookup"><span data-stu-id="6e3a3-175">Create your Azure Credential file:</span></span>

   ```azurecli
   az ad sp create-for-rbac --sdk-auth > my.azureauth
   ```

   <span data-ttu-id="6e3a3-176">Эта команда создаст файл *my.azureauth* в каталоге *resources* приблизительно с таким содержимым:</span><span class="sxs-lookup"><span data-stu-id="6e3a3-176">This command will create a *my.azureauth* file in your *resources* directory with contents that resemble the following example:</span></span>

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

## <a name="configure-your-spring-boot-app-to-use-your-azure-event-hub"></a><span data-ttu-id="6e3a3-177">Настройка приложения Spring Boot для использования концентратора событий Azure</span><span class="sxs-lookup"><span data-stu-id="6e3a3-177">Configure your Spring Boot app to use your Azure Event Hub</span></span>

1. <span data-ttu-id="6e3a3-178">Найдите файл *application.properties* в каталоге *resources* приложения, например так:</span><span class="sxs-lookup"><span data-stu-id="6e3a3-178">Locate the *application.properties* in the *resources* directory of your app; for example:</span></span>

   `C:\SpringBoot\eventhub\src\main\resources\application.properties`

   <span data-ttu-id="6e3a3-179">-или-</span><span class="sxs-lookup"><span data-stu-id="6e3a3-179">-or-</span></span>

   `/users/example/home/eventhub/src/main/resources/application.properties`

1.  <span data-ttu-id="6e3a3-180">Откройте файл *application.properties* в текстовом редакторе, добавьте следующие строки и замените примеры значений соответствующими параметрами концентратора событий:</span><span class="sxs-lookup"><span data-stu-id="6e3a3-180">Open the *application.properties* file in a text editor, add the following lines, and then replace the sample values with the appropriate properties for your event hub:</span></span>

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
   <span data-ttu-id="6e3a3-181">Описание</span><span class="sxs-lookup"><span data-stu-id="6e3a3-181">Where:</span></span>
   | <span data-ttu-id="6e3a3-182">Поле</span><span class="sxs-lookup"><span data-stu-id="6e3a3-182">Field</span></span> | <span data-ttu-id="6e3a3-183">ОПИСАНИЕ</span><span class="sxs-lookup"><span data-stu-id="6e3a3-183">Description</span></span> |
   | ---|---|
   | `spring.cloud.azure.credential-file-path` | <span data-ttu-id="6e3a3-184">Определяет файл учетных данных Azure, который был создан ранее в этом примере.</span><span class="sxs-lookup"><span data-stu-id="6e3a3-184">Specifies Azure credential file that you created earlier in this tutorial.</span></span> |
   | `spring.cloud.azure.resource-group` | <span data-ttu-id="6e3a3-185">Определяет группу ресурсов Azure, которая содержит концентратор событий Azure.</span><span class="sxs-lookup"><span data-stu-id="6e3a3-185">Specifies the Azure Resource Group that contains your Azure Event Hub.</span></span> |
   | `spring.cloud.azure.region` | <span data-ttu-id="6e3a3-186">Определяет географический регион, указанный при создании концентратора событий Azure.</span><span class="sxs-lookup"><span data-stu-id="6e3a3-186">Specifies the geographical region that you specified when you created your Azure Event Hub.</span></span> |
   | `spring.cloud.azure.eventhub.namespace` | <span data-ttu-id="6e3a3-187">Определяет уникальное имя, заданное при создании пространства имен концентратора событий Azure.</span><span class="sxs-lookup"><span data-stu-id="6e3a3-187">Specifies the unique name that you specified when you created your Azure Event Hub Namespace.</span></span> |
   | `spring.cloud.azure.eventhub.checkpoint-storage-account` | <span data-ttu-id="6e3a3-188">Определяет учетную запись хранения Azure, которая была создана ранее в этом примере.</span><span class="sxs-lookup"><span data-stu-id="6e3a3-188">Specifies Azure Storage Account that you created earlier in this tutorial.</span></span>
   | `spring.cloud.stream.bindings.input.destination` | <span data-ttu-id="6e3a3-189">Определяет назначение входящих данных концентратора событий Azure, которым в этом примере является сам концентратор, созданный ранее.</span><span class="sxs-lookup"><span data-stu-id="6e3a3-189">Specifies the input destination Azure Event Hub, which for this tutorial is the  hub you created earlier in this tutorial.</span></span> |
   | `spring.cloud.stream.bindings.input.group `| <span data-ttu-id="6e3a3-190">Определяет группу потребителей концентратора событий Azure, для которой можно установить значение $Default, чтобы использовать базовую группу потребителей, созданную вместе с концентратором событий Azure.</span><span class="sxs-lookup"><span data-stu-id="6e3a3-190">Specifies a Consumer Group from Azure Event Hub, which can be set to '$Default' in order to use the basic consumer group that was created when you created your Azure Event Hub.</span></span> |
   | `spring.cloud.stream.bindings.output.destination` | <span data-ttu-id="6e3a3-191">Определяет назначение исходящих данных для концентратора событий Azure, которое в этом примере совпадает с назначением входящих данных.</span><span class="sxs-lookup"><span data-stu-id="6e3a3-191">Specifies the output destination Azure Event Hub, which for this tutorial will be the same as the input destination.</span></span> |

1. <span data-ttu-id="6e3a3-192">Сохраните и закройте файл *application.properties*.</span><span class="sxs-lookup"><span data-stu-id="6e3a3-192">Save and close the *application.properties* file.</span></span>

## <a name="add-sample-code-to-implement-basic-event-hub-functionality"></a><span data-ttu-id="6e3a3-193">Добавление примера кода для реализации базовых функций концентратора событий</span><span class="sxs-lookup"><span data-stu-id="6e3a3-193">Add sample code to implement basic event hub functionality</span></span>

<span data-ttu-id="6e3a3-194">В этом разделе вы создадите классы Java, требуемые для отправки событий в концентратор событий.</span><span class="sxs-lookup"><span data-stu-id="6e3a3-194">In this section, you create the necessary Java classes for sending events to your event hub.</span></span>

### <a name="modify-the-main-application-class"></a><span data-ttu-id="6e3a3-195">Изменение класса основного приложения</span><span class="sxs-lookup"><span data-stu-id="6e3a3-195">Modify the main application class</span></span>

1. <span data-ttu-id="6e3a3-196">Найдите файл основного приложения Java в каталоге пакета приложения, например:</span><span class="sxs-lookup"><span data-stu-id="6e3a3-196">Locate the main application Java file in the package directory of your app; for example:</span></span>

   `C:\SpringBoot\eventhub\src\main\java\com\wingtiptoys\eventhub\EventhubApplication.java`

   <span data-ttu-id="6e3a3-197">-или-</span><span class="sxs-lookup"><span data-stu-id="6e3a3-197">-or-</span></span>

   `/users/example/home/eventhub/src/main/java/com/wingtiptoys/eventhub/EventhubApplication.java`

1. <span data-ttu-id="6e3a3-198">Откройте файл основного приложения Java в текстовом редакторе и добавьте в него следующие строки:</span><span class="sxs-lookup"><span data-stu-id="6e3a3-198">Open the main application Java file in a text editor, and add the following lines to the file:</span></span>

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

1. <span data-ttu-id="6e3a3-199">Сохраните и закройте файл основного приложения Java.</span><span class="sxs-lookup"><span data-stu-id="6e3a3-199">Save and close the main application Java file.</span></span>

### <a name="create-a-new-class-for-the-source-connector"></a><span data-ttu-id="6e3a3-200">Создание класса для соединителя источника</span><span class="sxs-lookup"><span data-stu-id="6e3a3-200">Create a new class for the source connector</span></span>

1. <span data-ttu-id="6e3a3-201">В каталоге пакета приложения создайте файл Java с именем *EventhubSource.java*, а затем откройте этот файл в текстовом редакторе и добавьте следующие строки:</span><span class="sxs-lookup"><span data-stu-id="6e3a3-201">Create a new Java file named *EventhubSource.java* in the package directory of your app, then open the file in a text editor and add the following lines:</span></span>

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
1. <span data-ttu-id="6e3a3-202">Сохраните и закройте файл *EventhubSource.java*.</span><span class="sxs-lookup"><span data-stu-id="6e3a3-202">Save and close the *EventhubSource.java* file.</span></span>

### <a name="create-a-new-class-for-the-sink-connector"></a><span data-ttu-id="6e3a3-203">Создание класса для соединителя приемника</span><span class="sxs-lookup"><span data-stu-id="6e3a3-203">Create a new class for the sink connector</span></span>

1. <span data-ttu-id="6e3a3-204">В каталоге пакета приложения создайте файл Java с именем *EventhubSink.java*, а затем откройте этот файл в текстовом редакторе и добавьте следующие строки:</span><span class="sxs-lookup"><span data-stu-id="6e3a3-204">Create a new Java file named *EventhubSink.java* in the package directory of your app, then open the file in a text editor and add the following lines:</span></span>

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

1. <span data-ttu-id="6e3a3-205">Сохраните и закройте файл *EventhubSink.java*.</span><span class="sxs-lookup"><span data-stu-id="6e3a3-205">Save and close the *EventhubSink.java* file.</span></span>

## <a name="build-and-test-your-application"></a><span data-ttu-id="6e3a3-206">Сборка и тестирование приложения</span><span class="sxs-lookup"><span data-stu-id="6e3a3-206">Build and test your application</span></span>

1. <span data-ttu-id="6e3a3-207">Откройте командную строку и перейдите из каталога в папку с файлом *pom.xml*, например:</span><span class="sxs-lookup"><span data-stu-id="6e3a3-207">Open a command prompt and change directory to the folder where your *pom.xml* file is located; for example:</span></span>

   `cd C:\SpringBoot\eventhub`

   <span data-ttu-id="6e3a3-208">-или-</span><span class="sxs-lookup"><span data-stu-id="6e3a3-208">-or-</span></span>

   `cd /users/example/home/eventhub`

1. <span data-ttu-id="6e3a3-209">Создайте приложение Spring Boot с помощью Maven и запустите его, например, следующим образом:</span><span class="sxs-lookup"><span data-stu-id="6e3a3-209">Build your Spring Boot application with Maven and run it; for example:</span></span>

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

1. <span data-ttu-id="6e3a3-210">После запуска приложения можно использовать средство *curl*, чтобы протестировать приложение, например:</span><span class="sxs-lookup"><span data-stu-id="6e3a3-210">Once your application is running, you can use *curl* to test your application; for example:</span></span>

   ```shell
   curl -X POST -H "Content-Type: text/plain" -d "hello" http://localhost:8080/messages
   ```
   <span data-ttu-id="6e3a3-211">В журнале приложения должна появиться запись "hello".</span><span class="sxs-lookup"><span data-stu-id="6e3a3-211">You should see "hello" posted to your application's logs.</span></span> <span data-ttu-id="6e3a3-212">Например: </span><span class="sxs-lookup"><span data-stu-id="6e3a3-212">For example:</span></span>

   ```shell
   [Thread-13] INFO com.wingtiptoys.eventhub.EventhubSink - New message received: 'hello'
   [pool-10-thread-7] INFO com.wingtiptoys.eventhub.EventhubSink - Message 'hello' successfully checkpointed
   ```

## <a name="next-steps"></a><span data-ttu-id="6e3a3-213">Дополнительная информация</span><span class="sxs-lookup"><span data-stu-id="6e3a3-213">Next steps</span></span>

<span data-ttu-id="6e3a3-214">Дополнительные сведения о поддержке в Azure приложения Event Hub Stream Binder для концентратора событий см. в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="6e3a3-214">For more information about Azure support for Event Hub Stream Binder, see the following articles:</span></span>

* [<span data-ttu-id="6e3a3-215">Что такое Центры событий Azure?</span><span class="sxs-lookup"><span data-stu-id="6e3a3-215">What is Azure Event Hubs?</span></span>](/azure/event-hubs/event-hubs-about)

* [<span data-ttu-id="6e3a3-216">Создание пространства имен службы "Центры событий" и концентратора событий с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="6e3a3-216">Create an Event Hubs namespace and an event hub using the Azure portal</span></span>](/azure/event-hubs/event-hubs-create)

* <span data-ttu-id="6e3a3-217">[How to use the Spring Boot Starter for Apache Kafka with Azure Event Hubs](configure-spring-cloud-stream-binder-java-app-kafka-azure-event-hub.md) (Использование начального приложения Spring Boot для Apache Kafka в Центрах событий)</span><span class="sxs-lookup"><span data-stu-id="6e3a3-217">[How to use the Spring Boot Starter for Apache Kafka with Azure Event Hubs](configure-spring-cloud-stream-binder-java-app-kafka-azure-event-hub.md)</span></span>

<span data-ttu-id="6e3a3-218">См. дополнительные сведения об использовании Java в Azure и [инструментах Java для Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="6e3a3-218">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="6e3a3-219">**[Spring Framework]** — это решение с открытым кодом, которое помогает разработчикам Java создавать приложения корпоративного класса.</span><span class="sxs-lookup"><span data-stu-id="6e3a3-219">The **[Spring Framework]** is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="6e3a3-220">Одним из самых популярных проектов, созданных на этой платформе, является проект [Spring Boot]. Он упрощает подход к созданию автономных приложений Java.</span><span class="sxs-lookup"><span data-stu-id="6e3a3-220">One of the more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating stand-alone Java applications.</span></span> <span data-ttu-id="6e3a3-221">В помощь разработчикам, начинающим работать со Spring Boot, по адресу <https://github.com/spring-guides/> доступно несколько примеров пакетов этого приложения.</span><span class="sxs-lookup"><span data-stu-id="6e3a3-221">To help developers get started with Spring Boot, several sample Spring Boot packages are available at <https://github.com/spring-guides/>.</span></span> <span data-ttu-id="6e3a3-222">Помимо выбора из списка основных проектов Spring Boot, **[Spring Initializr]** помогает разработчикам создавать пользовательские приложения Spring Boot.</span><span class="sxs-lookup"><span data-stu-id="6e3a3-222">In addition to choosing from the list of basic Spring Boot projects, the **[Spring Initializr]** helps developers get started with creating custom Spring Boot applications.</span></span>

<!-- URL List -->

[бесплатной учетной записи Azure]: https://azure.microsoft.com/pricing/free-trial/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[инструментах Java для Visual Studio Team Services]: https://java.visualstudio.com/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
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
