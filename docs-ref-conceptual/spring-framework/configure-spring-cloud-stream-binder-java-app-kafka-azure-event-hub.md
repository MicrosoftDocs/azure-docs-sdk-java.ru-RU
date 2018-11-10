---
title: Использование начального приложения Spring Boot для Apache Kafka в Центрах событий Azure
description: Как настроить приложение, созданное с помощью Spring Boot Initializer, для использования Apache Kafka в Центрах событий Azure.
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
ms.openlocfilehash: ccef834d0ff1c40b061946f8ab1852584da80d7b
ms.sourcegitcommit: a168dc8c2396b6c4749abef03debb1f69298da38
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/01/2018
ms.locfileid: "50747005"
---
# <a name="how-to-use-the-spring-boot-starter-for-apache-kafka-with-azure-event-hubs"></a><span data-ttu-id="8af7d-103">Использование начального приложения Spring Boot для Apache Kafka в Центрах событий Azure</span><span class="sxs-lookup"><span data-stu-id="8af7d-103">How to use the Spring Boot Starter for Apache Kafka with Azure Event Hubs</span></span>

## <a name="overview"></a><span data-ttu-id="8af7d-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="8af7d-104">Overview</span></span>

<span data-ttu-id="8af7d-105">В статье показано, как настроить приложение Spring Cloud Stream Binder на основе Java, созданное с помощью Spring Boot Initializr для использования [Apache Kafka] в Центрах событий Azure.</span><span class="sxs-lookup"><span data-stu-id="8af7d-105">This article demonstrates how to configure a Java-based Spring Cloud Stream Binder created with the Spring Boot Initializer to use [Apache Kafka] with Azure Event Hubs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8af7d-106">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="8af7d-106">Prerequisites</span></span>

<span data-ttu-id="8af7d-107">Чтобы выполнить действия, описанные в этой статье, необходимо иметь следующие компоненты:</span><span class="sxs-lookup"><span data-stu-id="8af7d-107">The following prerequisites are required in order to follow the steps in this article:</span></span>

* <span data-ttu-id="8af7d-108">Подписка Azure. Если у вас ее еще нет, вы можете активировать [Преимущества для подписчиков MSDN] или зарегистрироваться для получения [бесплатной учетной записи Azure].</span><span class="sxs-lookup"><span data-stu-id="8af7d-108">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="8af7d-109">[Пакет разработчиков Java (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/) версии 1.7 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="8af7d-109">A [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), version 1.7 or later.</span></span>
* <span data-ttu-id="8af7d-110">[Apache Maven](http://maven.apache.org/) версии 3.0 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="8af7d-110">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>

> [!IMPORTANT]
>
> <span data-ttu-id="8af7d-111">Для выполнения операций, описанных в этой статье, требуется Spring Boot 2.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="8af7d-111">Spring Boot version 2.0 or greater is required to complete the steps in this article.</span></span>
>

## <a name="create-an-azure-event-hub-using-the-azure-portal"></a><span data-ttu-id="8af7d-112">Создание концентратора событий на портале Azure</span><span class="sxs-lookup"><span data-stu-id="8af7d-112">Create an Azure Event Hub using the Azure portal</span></span>

### <a name="create-an-azure-event-hub-namespace"></a><span data-ttu-id="8af7d-113">Создание пространства имен концентратора событий Azure</span><span class="sxs-lookup"><span data-stu-id="8af7d-113">Create an Azure Event Hub Namespace</span></span>

1. <span data-ttu-id="8af7d-114">Перейдите на портал Azure по адресу <https://portal.azure.com/> и выполните вход.</span><span class="sxs-lookup"><span data-stu-id="8af7d-114">Browse to the Azure portal at <https://portal.azure.com/> and sign in.</span></span>

1. <span data-ttu-id="8af7d-115">Выберите **+Создать ресурс**, **Интернет вещей** и **Центры событий**.</span><span class="sxs-lookup"><span data-stu-id="8af7d-115">Click **+Create a resource**, then **Internet of Things**, and then click **Event Hubs**.</span></span>

   ![Создание пространства имен концентратора событий Azure][IMG01]

1. <span data-ttu-id="8af7d-117">На странице **Создание пространства имен** введите такую информацию:</span><span class="sxs-lookup"><span data-stu-id="8af7d-117">On the **Create Namespace** page, enter the following information:</span></span>

   * <span data-ttu-id="8af7d-118">Уникальное **имя**, которое станет частью URI для пространства имен концентратора событий.</span><span class="sxs-lookup"><span data-stu-id="8af7d-118">Enter a unique **Name**, which will become part of the URI for your event hub namespace.</span></span> <span data-ttu-id="8af7d-119">Например, если вы зададите **wingtiptoys** в качестве **имени**, URI примет вид *wingtiptoys.servicebus.windows.net*.</span><span class="sxs-lookup"><span data-stu-id="8af7d-119">For example: if you entered **wingtiptoys** for the **Name**, the URI would be *wingtiptoys.servicebus.windows.net*.</span></span>
   * <span data-ttu-id="8af7d-120">Выберите **ценовую категорию** для пространства имен концентратора событий.</span><span class="sxs-lookup"><span data-stu-id="8af7d-120">Choose a **Pricing tier** for your event hub namespace.</span></span>
   * <span data-ttu-id="8af7d-121">Отметьте **Включить Kafka** для пространства имен.</span><span class="sxs-lookup"><span data-stu-id="8af7d-121">Specify **Enable Kafka** for your namespace.</span></span>
   * <span data-ttu-id="8af7d-122">Выберите **подписку** для пространства имен.</span><span class="sxs-lookup"><span data-stu-id="8af7d-122">Choose the **Subscription** you want to use for your namespace.</span></span>
   * <span data-ttu-id="8af7d-123">Укажите, следует ли создать новую **группу ресурсов** для пространства имен или использовать существующую.</span><span class="sxs-lookup"><span data-stu-id="8af7d-123">Specify whether to create a new **Resource group** for your namespace, or choose an existing resource group.</span></span>
   * <span data-ttu-id="8af7d-124">Укажите **расположение** для пространства имен Центров событий.</span><span class="sxs-lookup"><span data-stu-id="8af7d-124">Specify the **Location** for your event hub namespace.</span></span>

   ![Создание пространства имен для концентратора событий Azure][IMG02]

1. <span data-ttu-id="8af7d-126">Указав эти параметры, щелкните **Создать**, чтобы создать пространство имен.</span><span class="sxs-lookup"><span data-stu-id="8af7d-126">When you have specified the options listed above, click **Create** to create your namespace.</span></span>

### <a name="create-an-azure-event-hub-in-your-namespace"></a><span data-ttu-id="8af7d-127">Создание концентратора событий Azure в пространстве имен</span><span class="sxs-lookup"><span data-stu-id="8af7d-127">Create an Azure Event Hub in your namespace</span></span>

1. <span data-ttu-id="8af7d-128">Перейдите на портал Azure по адресу <https://portal.azure.com/>.</span><span class="sxs-lookup"><span data-stu-id="8af7d-128">Browse to the Azure portal at <https://portal.azure.com/>.</span></span>

1. <span data-ttu-id="8af7d-129">Щелкните **Все ресурсы** и выберите созданное пространство имен.</span><span class="sxs-lookup"><span data-stu-id="8af7d-129">Click **All resources**, and then click the namespace that you created.</span></span>

   ![Выбор пространства имен концентратора событий Azure][IMG03]

1. <span data-ttu-id="8af7d-131">Щелкните **Центры событий**, а затем **+Концентратор событий**.</span><span class="sxs-lookup"><span data-stu-id="8af7d-131">Click **Event Hubs**, and then click **+Event Hub**.</span></span>

   ![Добавление нового концентратора событий][IMG04]

1. <span data-ttu-id="8af7d-133">В области **Создание концентратора событий** введите уникальное **имя** для концентратора событий и щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="8af7d-133">On the **Create Event Hub** page, enter a unique **Name** for your Event Hub, and then click **Create**.</span></span>

   ![Создание концентратора событий Azure][IMG05]

1. <span data-ttu-id="8af7d-135">Созданный концентратор событий появится в списке на странице **Центры событий**.</span><span class="sxs-lookup"><span data-stu-id="8af7d-135">When your Event Hub has been created, it will be listed on the **Event Hubs** page.</span></span>

   ![Создание концентратора событий Azure][IMG06]

## <a name="create-a-simple-spring-boot-application-with-the-spring-initializr"></a><span data-ttu-id="8af7d-137">Создание простого приложения Spring Boot с помощью Spring Initializr</span><span class="sxs-lookup"><span data-stu-id="8af7d-137">Create a simple Spring Boot application with the Spring Initializr</span></span>

1. <span data-ttu-id="8af7d-138">Перейдите по адресу <https://start.spring.io/>.</span><span class="sxs-lookup"><span data-stu-id="8af7d-138">Browse to <https://start.spring.io/>.</span></span>

1. <span data-ttu-id="8af7d-139">Задайте такие параметры:</span><span class="sxs-lookup"><span data-stu-id="8af7d-139">Specify the following options:</span></span>

   * <span data-ttu-id="8af7d-140">Выберите в соответствующих полях **Maven Project** (Проект Maven) и **Java**.</span><span class="sxs-lookup"><span data-stu-id="8af7d-140">Generate a **Maven** project with **Java**.</span></span>
   * <span data-ttu-id="8af7d-141">Выберите версию **Spring Boot** не ниже версии 2.0.</span><span class="sxs-lookup"><span data-stu-id="8af7d-141">Specify a **Spring Boot** version that is equal to or greater than 2.0.</span></span>
   * <span data-ttu-id="8af7d-142">Заполните поля **Group** (Группа) и **Artifact** (Артефакт) для приложения.</span><span class="sxs-lookup"><span data-stu-id="8af7d-142">Specify the **Group** and **Artifact** names for your application.</span></span>
   * <span data-ttu-id="8af7d-143">Добавьте зависимость **Web** (Веб).</span><span class="sxs-lookup"><span data-stu-id="8af7d-143">Add the **Web** dependency.</span></span>

      ![Основные параметры Spring Initializr][SI01]

   > [!NOTE]
   >
   > <span data-ttu-id="8af7d-145">Spring Initializr использует имена **Group** (Группы) и **Artifact** (Артефакта) для создания имени пакета, как например *com.wingtiptoys.kafka*.</span><span class="sxs-lookup"><span data-stu-id="8af7d-145">The Spring Initializr uses the **Group** and **Artifact** names to create the package name; for example: *com.wingtiptoys.kafka*.</span></span>
   >

1. <span data-ttu-id="8af7d-146">Указав эти параметры, щелкните **Generate Project** (Создать проект).</span><span class="sxs-lookup"><span data-stu-id="8af7d-146">When you have specified the options listed above, click **Generate Project**.</span></span>

1. <span data-ttu-id="8af7d-147">При появлении запроса скачайте проект на локальный компьютер.</span><span class="sxs-lookup"><span data-stu-id="8af7d-147">When prompted, download the project to a path on your local computer.</span></span>

   ![Скачивание проекта Spring][SI02]

1. <span data-ttu-id="8af7d-149">После извлечения файлов в локальной системе простое приложение Spring Boot можно будет редактировать.</span><span class="sxs-lookup"><span data-stu-id="8af7d-149">After you have extracted the files on your local system, your simple Spring Boot application will be ready for editing.</span></span>

## <a name="configure-your-spring-boot-app-to-use-the-spring-cloud-kafka-stream-and-azure-event-hub-starters"></a><span data-ttu-id="8af7d-150">Настройка приложения Spring Boot для использования начальных приложений Spring Cloud Kafka Stream и концентратора событий Azure</span><span class="sxs-lookup"><span data-stu-id="8af7d-150">Configure your Spring Boot app to use the Spring Cloud Kafka Stream and Azure Event Hub starters</span></span>

1. <span data-ttu-id="8af7d-151">Найдите файл *pom.xml* в корневой папке приложения, например так:</span><span class="sxs-lookup"><span data-stu-id="8af7d-151">Locate the *pom.xml* file in the root directory of your app; for example:</span></span>

   `C:\SpringBoot\kafka\pom.xml`

   <span data-ttu-id="8af7d-152">-или-</span><span class="sxs-lookup"><span data-stu-id="8af7d-152">-or-</span></span>

   `/users/example/home/kafka/pom.xml`

1. <span data-ttu-id="8af7d-153">Откройте файл *pom.xml* в текстовом редакторе и добавьте начальное приложение Spring Cloud Kafka Stream и начальное приложение концентратора событий Azure в список `<dependencies>`:</span><span class="sxs-lookup"><span data-stu-id="8af7d-153">Open the *pom.xml* file in a text editor, and add the Spring Cloud Kafka Stream and Azure Event Hub starters to the list of `<dependencies>`:</span></span>

   ```xml
   <dependency>
      <groupId>org.springframework.cloud</groupId>
      <artifactId>spring-cloud-starter-stream-kafka</artifactId>
      <version>2.0.1.RELEASE</version>
   </dependency>
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>spring-cloud-azure-starter-eventhub</artifactId>
      <version>1.0.0.M2</version>
   </dependency>
   ```

   ![Редактирование файла pom.xml][SI03]

1. <span data-ttu-id="8af7d-155">Сохраните и закройте файл *pom.xml*.</span><span class="sxs-lookup"><span data-stu-id="8af7d-155">Save and close the *pom.xml* file.</span></span>

## <a name="create-an-azure-credential-file"></a><span data-ttu-id="8af7d-156">Создание файла учетных данных Azure</span><span class="sxs-lookup"><span data-stu-id="8af7d-156">Create an Azure Credential File</span></span>

1. <span data-ttu-id="8af7d-157">Откройте окно командной строки.</span><span class="sxs-lookup"><span data-stu-id="8af7d-157">Open a command prompt.</span></span>

1. <span data-ttu-id="8af7d-158">Перейдите к каталогу *resources* приложения Spring Boot, например так:</span><span class="sxs-lookup"><span data-stu-id="8af7d-158">Navigate to the *resources* directory of your Spring Boot app; for example:</span></span>

   ```shell
   cd C:\SpringBoot\eventhub\src\main\resources
   ```

   <span data-ttu-id="8af7d-159">-или-</span><span class="sxs-lookup"><span data-stu-id="8af7d-159">-or-</span></span>

   ```shell
   cd /users/example/home/eventhub/src/main/resources
   ```

1. <span data-ttu-id="8af7d-160">Вход в учетную запись Azure:</span><span class="sxs-lookup"><span data-stu-id="8af7d-160">Sign in to your Azure account:</span></span>

   ```azurecli
   az login
   ```

1. <span data-ttu-id="8af7d-161">Отобразите список подписок:</span><span class="sxs-lookup"><span data-stu-id="8af7d-161">List your subscriptions:</span></span>

   ```azurecli
   az account list
   ```
   <span data-ttu-id="8af7d-162">Azure отобразит список подписок, и вам нужно будет скопировать идентификатор GUID для подписки, которая будет использоваться, например:</span><span class="sxs-lookup"><span data-stu-id="8af7d-162">Azure will return a list of your subscriptions, and you will need to copy the GUID for the subscription that you want to use; for example:</span></span>

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
   
1. <span data-ttu-id="8af7d-163">Укажите GUID подписки, которую вы собираетесь использовать в Azure, например:</span><span class="sxs-lookup"><span data-stu-id="8af7d-163">Specify the GUID for the subscription you want to use with Azure; for example:</span></span>

   ```azurecli
   az account set -s 11111111-1111-1111-1111-111111111111
   ```

1. <span data-ttu-id="8af7d-164">Создайте файл учетных данных Azure:</span><span class="sxs-lookup"><span data-stu-id="8af7d-164">Create your Azure Credential file:</span></span>

   ```azurecli
   az ad sp create-for-rbac --sdk-auth > my.azureauth
   ```

   <span data-ttu-id="8af7d-165">Эта команда создаст файл *my.azureauth* в каталоге *resources* приблизительно с таким содержимым:</span><span class="sxs-lookup"><span data-stu-id="8af7d-165">This command will create a *my.azureauth* file in your *resources* directory with contents that resemble the following example:</span></span>

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

## <a name="configure-your-spring-boot-app-to-use-your-azure-event-hub"></a><span data-ttu-id="8af7d-166">Настройка приложения Spring Boot для использования концентратора событий Azure</span><span class="sxs-lookup"><span data-stu-id="8af7d-166">Configure your Spring Boot app to use your Azure Event Hub</span></span>

1. <span data-ttu-id="8af7d-167">Найдите файл *application.properties* в каталоге *resources* приложения, например так:</span><span class="sxs-lookup"><span data-stu-id="8af7d-167">Locate the *application.properties* in the *resources* directory of your app; for example:</span></span>

   `C:\SpringBoot\eventhub\src\main\resources\application.properties`

   <span data-ttu-id="8af7d-168">-или-</span><span class="sxs-lookup"><span data-stu-id="8af7d-168">-or-</span></span>

   `/users/example/home/eventhub/src/main/resources/application.properties`

2. <span data-ttu-id="8af7d-169">Откройте файл *application.properties* в текстовом редакторе, добавьте следующие строки и замените примеры значений соответствующими параметрами концентратора событий:</span><span class="sxs-lookup"><span data-stu-id="8af7d-169">Open the *application.properties* file in a text editor, add the following lines, and then replace the sample values with the appropriate properties for your event hub:</span></span>

   ```yaml
   spring.cloud.azure.credential-file-path=my.azureauth
   spring.cloud.azure.resource-group=wingtiptoysresources
   spring.cloud.azure.region=West US
   spring.cloud.azure.eventhub.namespace=wingtiptoysnamespace

   spring.cloud.stream.bindings.input.destination=wingtiptoyshub
   spring.cloud.stream.bindings.input.group=$Default
   spring.cloud.stream.bindings.output.destination=wingtiptoyshub
   ```
   <span data-ttu-id="8af7d-170">Описание</span><span class="sxs-lookup"><span data-stu-id="8af7d-170">Where:</span></span>

   |                       <span data-ttu-id="8af7d-171">Поле</span><span class="sxs-lookup"><span data-stu-id="8af7d-171">Field</span></span>                       |                                                                                   <span data-ttu-id="8af7d-172">ОПИСАНИЕ</span><span class="sxs-lookup"><span data-stu-id="8af7d-172">Description</span></span>                                                                                    |
   |---------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
   |     `spring.cloud.azure.credential-file-path`     |                                                    <span data-ttu-id="8af7d-173">Определяет файл учетных данных Azure, который был создан ранее в этом примере.</span><span class="sxs-lookup"><span data-stu-id="8af7d-173">Specifies Azure credential file that you created earlier in this tutorial.</span></span>                                                    |
   |        `spring.cloud.azure.resource-group`        |                                                      <span data-ttu-id="8af7d-174">Определяет группу ресурсов Azure, которая содержит концентратор событий Azure.</span><span class="sxs-lookup"><span data-stu-id="8af7d-174">Specifies the Azure Resource Group that contains your Azure Event Hub.</span></span>                                                      |
   |            `spring.cloud.azure.region`            |                                           <span data-ttu-id="8af7d-175">Определяет географический регион, указанный при создании концентратора событий Azure.</span><span class="sxs-lookup"><span data-stu-id="8af7d-175">Specifies the geographical region that you specified when you created your Azure Event Hub.</span></span>                                            |
   |      `spring.cloud.azure.eventhub.namespace`      |                                          <span data-ttu-id="8af7d-176">Определяет уникальное имя, заданное при создании пространства имен концентратора событий Azure.</span><span class="sxs-lookup"><span data-stu-id="8af7d-176">Specifies the unique name that you specified when you created your Azure Event Hub Namespace.</span></span>                                           |
   | `spring.cloud.stream.bindings.input.destination`  |                            <span data-ttu-id="8af7d-177">Определяет назначение входящих данных концентратора событий Azure, которым в этом примере является сам концентратор, созданный ранее.</span><span class="sxs-lookup"><span data-stu-id="8af7d-177">Specifies the input destination Azure Event Hub, which for this tutorial is the  hub you created earlier in this tutorial.</span></span>                            |
   |    `spring.cloud.stream.bindings.input.group `    | <span data-ttu-id="8af7d-178">Определяет группу потребителей концентратора событий Azure, для которой можно установить значение $Default, чтобы использовать базовую группу потребителей, созданную вместе с концентратором событий Azure.</span><span class="sxs-lookup"><span data-stu-id="8af7d-178">Specifies a Consumer Group from Azure Event Hub, which can be set to '$Default' in order to use the basic consumer group that was created when you created your Azure Event Hub.</span></span> |
   | `spring.cloud.stream.bindings.output.destination` |                               <span data-ttu-id="8af7d-179">Определяет назначение исходящих данных для концентратора событий Azure, которое в этом примере совпадает с назначением входящих данных.</span><span class="sxs-lookup"><span data-stu-id="8af7d-179">Specifies the output destination Azure Event Hub, which for this tutorial will be the same as the input destination.</span></span>                               |


3. <span data-ttu-id="8af7d-180">Сохраните и закройте файл *application.properties*.</span><span class="sxs-lookup"><span data-stu-id="8af7d-180">Save and close the *application.properties* file.</span></span>

## <a name="add-sample-code-to-implement-basic-event-hub-functionality"></a><span data-ttu-id="8af7d-181">Добавление примера кода для реализации базовых функций концентратора событий</span><span class="sxs-lookup"><span data-stu-id="8af7d-181">Add sample code to implement basic event hub functionality</span></span>

<span data-ttu-id="8af7d-182">В этом разделе вы создадите классы Java, требуемые для отправки событий в концентратор событий.</span><span class="sxs-lookup"><span data-stu-id="8af7d-182">In this section, you create the necessary Java classes for sending events to your event hub.</span></span>

### <a name="modify-the-main-application-class"></a><span data-ttu-id="8af7d-183">Изменение класса основного приложения</span><span class="sxs-lookup"><span data-stu-id="8af7d-183">Modify the main application class</span></span>

1. <span data-ttu-id="8af7d-184">Найдите файл основного приложения Java в каталоге пакета приложения, например:</span><span class="sxs-lookup"><span data-stu-id="8af7d-184">Locate the main application Java file in the package directory of your app; for example:</span></span>

   `C:\SpringBoot\kafka\src\main\java\com\wingtiptoys\kafka\KafkaApplication.java`

   <span data-ttu-id="8af7d-185">-или-</span><span class="sxs-lookup"><span data-stu-id="8af7d-185">-or-</span></span>

   `/users/example/home/kafka/src/main/java/com/wingtiptoys/kafka/KafkaApplication.java`

1. <span data-ttu-id="8af7d-186">Откройте файл основного приложения Java в текстовом редакторе и добавьте в него следующие строки:</span><span class="sxs-lookup"><span data-stu-id="8af7d-186">Open the main application Java file in a text editor, and add the following lines to the file:</span></span>

   ```java
   package com.wingtiptoys.kafka;

   import org.springframework.boot.SpringApplication;
   import org.springframework.boot.autoconfigure.SpringBootApplication;

   @SpringBootApplication
   public class KafkaApplication {
      public static void main(String[] args) {
         SpringApplication.run(KafkaApplication.class, args);
      }
   }
   ```

1. <span data-ttu-id="8af7d-187">Сохраните и закройте файл основного приложения Java.</span><span class="sxs-lookup"><span data-stu-id="8af7d-187">Save and close the main application Java file.</span></span>


### <a name="create-a-new-class-for-the-source-connector"></a><span data-ttu-id="8af7d-188">Создание класса для соединителя источника</span><span class="sxs-lookup"><span data-stu-id="8af7d-188">Create a new class for the source connector</span></span>

1. <span data-ttu-id="8af7d-189">В каталоге пакета вашего приложения создайте файл Java с именем *KafkaSource.java*, а затем откройте этот файл в текстовом редакторе и добавьте следующие строки:</span><span class="sxs-lookup"><span data-stu-id="8af7d-189">Create a new Java file named *KafkaSource.java* in the package directory of your app, then open the file in a text editor and add the following lines:</span></span>

   ```java
   package com.wingtiptoys.kafka;

   import org.springframework.beans.factory.annotation.Autowired;
   import org.springframework.cloud.stream.annotation.EnableBinding;
   import org.springframework.cloud.stream.messaging.Source;
   import org.springframework.messaging.support.GenericMessage;
   import org.springframework.web.bind.annotation.PostMapping;
   import org.springframework.web.bind.annotation.RequestBody;
   import org.springframework.web.bind.annotation.RequestParam;
   import org.springframework.web.bind.annotation.RestController;

   @EnableBinding(Source.class)
   @RestController
   public class KafkaSource {
      @Autowired
      private Source source;

      @PostMapping("/messages")
      public String sendMessage(@RequestBody String message) {
         this.source.output().send(new GenericMessage<>(message));
         return message;
      }
   }
   ```

1. <span data-ttu-id="8af7d-190">Сохраните и закройте файл *KafkaSource.java*.</span><span class="sxs-lookup"><span data-stu-id="8af7d-190">Save and close the *KafkaSource.java* file.</span></span>

### <a name="create-a-new-class-for-the-sink-connector"></a><span data-ttu-id="8af7d-191">Создание класса для соединителя приемника</span><span class="sxs-lookup"><span data-stu-id="8af7d-191">Create a new class for the sink connector</span></span>

1. <span data-ttu-id="8af7d-192">В каталоге пакета вашего приложения создайте файл Java с именем *KafkaSink.java*, а затем откройте этот файл в текстовом редакторе и добавьте следующие строки:</span><span class="sxs-lookup"><span data-stu-id="8af7d-192">Create a new Java file named *KafkaSink.java* in the package directory of your app, then open the file in a text editor and add the following lines:</span></span>

   ```java
   package com.wingtiptoys.kafka;

   import org.slf4j.Logger;
   import org.slf4j.LoggerFactory;
   import org.springframework.cloud.stream.annotation.EnableBinding;
   import org.springframework.cloud.stream.annotation.StreamListener;
   import org.springframework.cloud.stream.messaging.Sink;

   @EnableBinding(Sink.class)
   public class KafkaSink {
      private static final Logger LOGGER = LoggerFactory.getLogger(KafkaSink.class);

      @StreamListener(Sink.INPUT)
      public void handleMessage(String message) {
         LOGGER.info("New message received: " + message);
      }
   }
   ```

1. <span data-ttu-id="8af7d-193">Сохраните и закройте файл *KafkaSink.java*.</span><span class="sxs-lookup"><span data-stu-id="8af7d-193">Save and close the *KafkaSink.java* file.</span></span>

## <a name="build-and-test-your-application"></a><span data-ttu-id="8af7d-194">Сборка и тестирование приложения</span><span class="sxs-lookup"><span data-stu-id="8af7d-194">Build and test your application</span></span>

1. <span data-ttu-id="8af7d-195">Откройте командную строку и перейдите из каталога в папку с файлом *pom.xml*, например:</span><span class="sxs-lookup"><span data-stu-id="8af7d-195">Open a command prompt and change directory to the folder where your *pom.xml* file is located; for example:</span></span>

   `cd C:\SpringBoot\kafka`

   <span data-ttu-id="8af7d-196">-или-</span><span class="sxs-lookup"><span data-stu-id="8af7d-196">-or-</span></span>

   `cd /users/example/home/kafka`

1. <span data-ttu-id="8af7d-197">Создайте приложение Spring Boot с помощью Maven и запустите его, например, следующим образом:</span><span class="sxs-lookup"><span data-stu-id="8af7d-197">Build your Spring Boot application with Maven and run it; for example:</span></span>

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

1. <span data-ttu-id="8af7d-198">После запуска приложения можно использовать средство *curl*, чтобы протестировать приложение, например:</span><span class="sxs-lookup"><span data-stu-id="8af7d-198">Once your application is running, you can use *curl* to test your application; for example:</span></span>

   ```shell
   curl -X POST -H "Content-Type: text/plain" -d "hello" http://localhost:8080/messages
   ```
   <span data-ttu-id="8af7d-199">В журнале приложения должна появиться запись "hello".</span><span class="sxs-lookup"><span data-stu-id="8af7d-199">You should see "hello" posted to your application's logs.</span></span> <span data-ttu-id="8af7d-200">Например: </span><span class="sxs-lookup"><span data-stu-id="8af7d-200">For example:</span></span>

   ```shell
   [http-nio-8080-exec-2] INFO org.apache.kafka.common.utils.AppInfoParser - Kafka version : 1.0.2
   [http-nio-8080-exec-2] INFO org.apache.kafka.common.utils.AppInfoParser - Kafka commitId : 2a121f7b1d402825
   [wingtiptoyshub.container-0-C-1] INFO com.wingtiptoys.kafka.KafkaSink - New message received: hello
   ```


> [!NOTE]
> 
> <span data-ttu-id="8af7d-201">Для тестирования можно изменить файл *KafkaSource.java*, добавив в него простую HTML-форму, как в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="8af7d-201">For testing purposes, you could modify your *KafkaSource.java* so that it contains a simple HTML form like the following example:</span></span>
> 
> ```java
> package com.wingtiptoys.kafka;
>    
> import org.springframework.beans.factory.annotation.Autowired;
> import org.springframework.cloud.stream.annotation.EnableBinding;
> import org.springframework.cloud.stream.messaging.Source;
> import org.springframework.messaging.support.GenericMessage;
> import org.springframework.web.bind.annotation.GetMapping;
> import org.springframework.web.bind.annotation.PostMapping;
> import org.springframework.web.bind.annotation.RequestBody;
> import org.springframework.web.bind.annotation.RequestParam;
> import org.springframework.web.bind.annotation.RestController;
> 
> @EnableBinding(Source.class)
> @RestController
> public class KafkaSource {
>   @Autowired
>   private Source source;
> 
>   @GetMapping("/")
>   public String sendForm() {
>     return "<html><body>" +
>       "<form action=\"/messages\" method=\"post\">" +
>       "<input type=\"text\" name=\"text\">" +
>       "<input type=\"submit\">" +
>       "</form></body><html>";
>     }
> 
>   @PostMapping("/messages")
>   public String sendMessage(@RequestBody String message) {
>     this.source.output().send(new GenericMessage<>(message));
>     return message;
>   }
> }
> ```
> 
> <span data-ttu-id="8af7d-202">Это позволит использовать веб-браузер для тестирования приложения:</span><span class="sxs-lookup"><span data-stu-id="8af7d-202">This will allow you to use a web browser to test your application:</span></span>
> 
> ![Тестирование приложения с помощью веб-браузера][TB01]
> 
> <span data-ttu-id="8af7d-204">После отправки данных формы в приложении отобразятся результаты:</span><span class="sxs-lookup"><span data-stu-id="8af7d-204">When you submit the form, your application will display the results:</span></span>
> 
> ![Ответ приложения в веб-браузере][TB02]
> 

## <a name="next-steps"></a><span data-ttu-id="8af7d-206">Дополнительная информация</span><span class="sxs-lookup"><span data-stu-id="8af7d-206">Next steps</span></span>

<span data-ttu-id="8af7d-207">Дополнительные сведения о поддержке в Azure Apache Kafka и Stream Binder для концентратора событий см. в статьях:</span><span class="sxs-lookup"><span data-stu-id="8af7d-207">For more information about Azure support for Event Hub Stream Binder and Apache Kafka, see the following articles:</span></span>

* [<span data-ttu-id="8af7d-208">Что такое Центры событий Azure?</span><span class="sxs-lookup"><span data-stu-id="8af7d-208">What is Azure Event Hubs?</span></span>](/azure/event-hubs/event-hubs-about)

* [<span data-ttu-id="8af7d-209">Центры событий Azure для Apache Kafka</span><span class="sxs-lookup"><span data-stu-id="8af7d-209">Azure Event Hubs for Apache Kafka</span></span>](/azure/event-hubs/event-hubs-for-kafka-ecosystem-overview)

* [<span data-ttu-id="8af7d-210">Создание пространства имен службы "Центры событий" и концентратора событий с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="8af7d-210">Create an Event Hubs namespace and an event hub using the Azure portal</span></span>](/azure/event-hubs/event-hubs-create)

* [<span data-ttu-id="8af7d-211">Создание Центров событий с поддержкой Apache Kafka</span><span class="sxs-lookup"><span data-stu-id="8af7d-211">Create Apache Kafka enabled event hubs</span></span>](/azure/event-hubs/event-hubs-create-kafka-enabled)

<span data-ttu-id="8af7d-212">См. дополнительные сведения об использовании Java в Azure и [инструментах Java для Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="8af7d-212">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="8af7d-213">**[Spring Framework]** — это решение с открытым кодом, которое помогает разработчикам Java создавать приложения корпоративного класса.</span><span class="sxs-lookup"><span data-stu-id="8af7d-213">The **[Spring Framework]** is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="8af7d-214">Одним из самых популярных проектов, созданных на этой платформе, является проект [Spring Boot]. Он упрощает подход к созданию автономных приложений Java.</span><span class="sxs-lookup"><span data-stu-id="8af7d-214">One of the more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating stand-alone Java applications.</span></span> <span data-ttu-id="8af7d-215">В помощь разработчикам, начинающим работать со Spring Boot, по адресу <https://github.com/spring-guides/> доступно несколько примеров пакетов этого приложения.</span><span class="sxs-lookup"><span data-stu-id="8af7d-215">To help developers get started with Spring Boot, several sample Spring Boot packages are available at <https://github.com/spring-guides/>.</span></span> <span data-ttu-id="8af7d-216">Помимо выбора из списка основных проектов Spring Boot, **[Spring Initializr]** помогает разработчикам создавать пользовательские приложения Spring Boot.</span><span class="sxs-lookup"><span data-stu-id="8af7d-216">In addition to choosing from the list of basic Spring Boot projects, the **[Spring Initializr]** helps developers get started with creating custom Spring Boot applications.</span></span>

<!-- URL List -->

[Apache Kafka]: http://kafka.apache.org
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

[IMG01]: ./media/configure-spring-cloud-stream-binder-java-app-kafka-azure-event-hub/create-kafka-event-hub-01.png
[IMG02]: ./media/configure-spring-cloud-stream-binder-java-app-kafka-azure-event-hub/create-kafka-event-hub-02.png
[IMG03]: ./media/configure-spring-cloud-stream-binder-java-app-kafka-azure-event-hub/create-kafka-event-hub-03.png
[IMG04]: ./media/configure-spring-cloud-stream-binder-java-app-kafka-azure-event-hub/create-kafka-event-hub-04.png
[IMG05]: ./media/configure-spring-cloud-stream-binder-java-app-kafka-azure-event-hub/create-kafka-event-hub-05.png
[IMG06]: ./media/configure-spring-cloud-stream-binder-java-app-kafka-azure-event-hub/create-kafka-event-hub-06.png
[IMG07]: ./media/configure-spring-cloud-stream-binder-java-app-kafka-azure-event-hub/create-kafka-event-hub-07.png
[IMG08]: ./media/configure-spring-cloud-stream-binder-java-app-kafka-azure-event-hub/create-kafka-event-hub-08.png

[SI01]: ./media/configure-spring-cloud-stream-binder-java-app-kafka-azure-event-hub/create-project-01.png
[SI02]: ./media/configure-spring-cloud-stream-binder-java-app-kafka-azure-event-hub/create-project-02.png
[SI03]: ./media/configure-spring-cloud-stream-binder-java-app-kafka-azure-event-hub/create-project-03.png

[TB01]: ./media/configure-spring-cloud-stream-binder-java-app-kafka-azure-event-hub/test-browser-01.png
[TB02]: ./media/configure-spring-cloud-stream-binder-java-app-kafka-azure-event-hub/test-browser-02.png
