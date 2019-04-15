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
ms.date: 12/19/2018
ms.devlang: java
ms.service: event-hubs
ms.tgt_pltfrm: na
ms.topic: article
ms.workload: na
ms.openlocfilehash: f2cf66a4e0ac113406781b4859869ff4edab527e
ms.sourcegitcommit: f0f140b0862ca5338b1b7e5c33cec3e58a70b8fd
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/03/2019
ms.locfileid: "53991539"
---
# <a name="how-to-use-the-spring-boot-starter-for-apache-kafka-with-azure-event-hubs"></a><span data-ttu-id="84651-103">Использование начального приложения Spring Boot для Apache Kafka в Центрах событий Azure</span><span class="sxs-lookup"><span data-stu-id="84651-103">How to use the Spring Boot Starter for Apache Kafka with Azure Event Hubs</span></span>

## <a name="overview"></a><span data-ttu-id="84651-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="84651-104">Overview</span></span>

<span data-ttu-id="84651-105">В статье показано, как настроить приложение Spring Cloud Stream Binder на основе Java, созданное с помощью Spring Boot Initializr для использования [Apache Kafka] в Центрах событий Azure.</span><span class="sxs-lookup"><span data-stu-id="84651-105">This article demonstrates how to configure a Java-based Spring Cloud Stream Binder created with the Spring Boot Initializer to use [Apache Kafka] with Azure Event Hubs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="84651-106">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="84651-106">Prerequisites</span></span>

<span data-ttu-id="84651-107">Чтобы выполнить действия, описанные в этой статье, необходимо иметь следующие компоненты:</span><span class="sxs-lookup"><span data-stu-id="84651-107">The following prerequisites are required in order to follow the steps in this article:</span></span>

* <span data-ttu-id="84651-108">Подписка Azure. Если у вас ее еще нет, вы можете активировать [Преимущества для подписчиков MSDN] или зарегистрироваться для получения [бесплатной учетной записи Azure].</span><span class="sxs-lookup"><span data-stu-id="84651-108">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="84651-109">Поддерживаемая версия Java Development Kit (JDK).</span><span class="sxs-lookup"><span data-stu-id="84651-109">A supported Java Development Kit (JDK).</span></span> <span data-ttu-id="84651-110">Дополнительные сведения о версиях JDK, доступных для разработки в Azure, см. в статье <https://aka.ms/azure-jdks>.</span><span class="sxs-lookup"><span data-stu-id="84651-110">For more information about the JDKs available for use when developing on Azure, see <https://aka.ms/azure-jdks>.</span></span>
* <span data-ttu-id="84651-111">[Apache Maven](http://maven.apache.org/) версии 3.0 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="84651-111">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>

> [!IMPORTANT]
>
> <span data-ttu-id="84651-112">Для выполнения операций, описанных в этой статье, требуется Spring Boot 2.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="84651-112">Spring Boot version 2.0 or greater is required to complete the steps in this article.</span></span>
>

## <a name="create-an-azure-event-hub-using-the-azure-portal"></a><span data-ttu-id="84651-113">Создание концентратора событий на портале Azure</span><span class="sxs-lookup"><span data-stu-id="84651-113">Create an Azure Event Hub using the Azure portal</span></span>

### <a name="create-an-azure-event-hub-namespace"></a><span data-ttu-id="84651-114">Создание пространства имен концентратора событий Azure</span><span class="sxs-lookup"><span data-stu-id="84651-114">Create an Azure Event Hub Namespace</span></span>

1. <span data-ttu-id="84651-115">Перейдите на портал Azure по адресу <https://portal.azure.com/> и выполните вход.</span><span class="sxs-lookup"><span data-stu-id="84651-115">Browse to the Azure portal at <https://portal.azure.com/> and sign in.</span></span>

1. <span data-ttu-id="84651-116">Выберите **+Создать ресурс**, **Интернет вещей** и **Центры событий**.</span><span class="sxs-lookup"><span data-stu-id="84651-116">Click **+Create a resource**, then **Internet of Things**, and then click **Event Hubs**.</span></span>

   ![Создание пространства имен концентратора событий Azure][IMG01]

1. <span data-ttu-id="84651-118">На странице **Создание пространства имен** введите такую информацию:</span><span class="sxs-lookup"><span data-stu-id="84651-118">On the **Create Namespace** page, enter the following information:</span></span>

   * <span data-ttu-id="84651-119">Уникальное **имя**, которое станет частью URI для пространства имен концентратора событий.</span><span class="sxs-lookup"><span data-stu-id="84651-119">Enter a unique **Name**, which will become part of the URI for your event hub namespace.</span></span> <span data-ttu-id="84651-120">Например, если вы зададите **wingtiptoys** в качестве **имени**, URI примет вид *wingtiptoys.servicebus.windows.net*.</span><span class="sxs-lookup"><span data-stu-id="84651-120">For example: if you entered **wingtiptoys** for the **Name**, the URI would be *wingtiptoys.servicebus.windows.net*.</span></span>
   * <span data-ttu-id="84651-121">Выберите **ценовую категорию** для пространства имен концентратора событий.</span><span class="sxs-lookup"><span data-stu-id="84651-121">Choose a **Pricing tier** for your event hub namespace.</span></span>
   * <span data-ttu-id="84651-122">Отметьте **Включить Kafka** для пространства имен.</span><span class="sxs-lookup"><span data-stu-id="84651-122">Specify **Enable Kafka** for your namespace.</span></span>
   * <span data-ttu-id="84651-123">Выберите **подписку** для пространства имен.</span><span class="sxs-lookup"><span data-stu-id="84651-123">Choose the **Subscription** you want to use for your namespace.</span></span>
   * <span data-ttu-id="84651-124">Укажите, следует ли создать новую **группу ресурсов** для пространства имен или использовать существующую.</span><span class="sxs-lookup"><span data-stu-id="84651-124">Specify whether to create a new **Resource group** for your namespace, or choose an existing resource group.</span></span>
   * <span data-ttu-id="84651-125">Укажите **расположение** для пространства имен Центров событий.</span><span class="sxs-lookup"><span data-stu-id="84651-125">Specify the **Location** for your event hub namespace.</span></span>

   ![Создание пространства имен для концентратора событий Azure][IMG02]

1. <span data-ttu-id="84651-127">Указав эти параметры, щелкните **Создать**, чтобы создать пространство имен.</span><span class="sxs-lookup"><span data-stu-id="84651-127">When you have specified the options listed above, click **Create** to create your namespace.</span></span>

### <a name="create-an-azure-event-hub-in-your-namespace"></a><span data-ttu-id="84651-128">Создание концентратора событий Azure в пространстве имен</span><span class="sxs-lookup"><span data-stu-id="84651-128">Create an Azure Event Hub in your namespace</span></span>

1. <span data-ttu-id="84651-129">Перейдите на портал Azure по адресу <https://portal.azure.com/>.</span><span class="sxs-lookup"><span data-stu-id="84651-129">Browse to the Azure portal at <https://portal.azure.com/>.</span></span>

1. <span data-ttu-id="84651-130">Щелкните **Все ресурсы** и выберите созданное пространство имен.</span><span class="sxs-lookup"><span data-stu-id="84651-130">Click **All resources**, and then click the namespace that you created.</span></span>

   ![Выбор пространства имен концентратора событий Azure][IMG03]

1. <span data-ttu-id="84651-132">Щелкните **Центры событий**, а затем **+Концентратор событий**.</span><span class="sxs-lookup"><span data-stu-id="84651-132">Click **Event Hubs**, and then click **+Event Hub**.</span></span>

   ![Добавление нового концентратора событий][IMG04]

1. <span data-ttu-id="84651-134">В области **Создание концентратора событий** введите уникальное **имя** для концентратора событий и щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="84651-134">On the **Create Event Hub** page, enter a unique **Name** for your Event Hub, and then click **Create**.</span></span>

   ![Создание концентратора событий Azure][IMG05]

1. <span data-ttu-id="84651-136">Созданный концентратор событий появится в списке на странице **Центры событий**.</span><span class="sxs-lookup"><span data-stu-id="84651-136">When your Event Hub has been created, it will be listed on the **Event Hubs** page.</span></span>

   ![Создание концентратора событий Azure][IMG06]

## <a name="create-a-simple-spring-boot-application-with-the-spring-initializr"></a><span data-ttu-id="84651-138">Создание простого приложения Spring Boot с помощью Spring Initializr</span><span class="sxs-lookup"><span data-stu-id="84651-138">Create a simple Spring Boot application with the Spring Initializr</span></span>

1. <span data-ttu-id="84651-139">Перейдите по адресу <https://start.spring.io/>.</span><span class="sxs-lookup"><span data-stu-id="84651-139">Browse to <https://start.spring.io/>.</span></span>

1. <span data-ttu-id="84651-140">Задайте такие параметры:</span><span class="sxs-lookup"><span data-stu-id="84651-140">Specify the following options:</span></span>

   * <span data-ttu-id="84651-141">Выберите в соответствующих полях **Maven Project** (Проект Maven) и **Java**.</span><span class="sxs-lookup"><span data-stu-id="84651-141">Generate a **Maven** project with **Java**.</span></span>
   * <span data-ttu-id="84651-142">Выберите версию **Spring Boot** не ниже версии 2.0.</span><span class="sxs-lookup"><span data-stu-id="84651-142">Specify a **Spring Boot** version that is equal to or greater than 2.0.</span></span>
   * <span data-ttu-id="84651-143">Заполните поля **Group** (Группа) и **Artifact** (Артефакт) для приложения.</span><span class="sxs-lookup"><span data-stu-id="84651-143">Specify the **Group** and **Artifact** names for your application.</span></span>
   * <span data-ttu-id="84651-144">Добавьте зависимость **Web** (Веб).</span><span class="sxs-lookup"><span data-stu-id="84651-144">Add the **Web** dependency.</span></span>

      ![Основные параметры Spring Initializr][SI01]

   > [!NOTE]
   >
   > <span data-ttu-id="84651-146">Spring Initializr использует имена **Group** (Группы) и **Artifact** (Артефакта) для создания имени пакета, как например *com.wingtiptoys.kafka*.</span><span class="sxs-lookup"><span data-stu-id="84651-146">The Spring Initializr uses the **Group** and **Artifact** names to create the package name; for example: *com.wingtiptoys.kafka*.</span></span>
   >

1. <span data-ttu-id="84651-147">Указав эти параметры, щелкните **Generate Project** (Создать проект).</span><span class="sxs-lookup"><span data-stu-id="84651-147">When you have specified the options listed above, click **Generate Project**.</span></span>

1. <span data-ttu-id="84651-148">При появлении запроса скачайте проект на локальный компьютер.</span><span class="sxs-lookup"><span data-stu-id="84651-148">When prompted, download the project to a path on your local computer.</span></span>

   ![Скачивание проекта Spring][SI02]

1. <span data-ttu-id="84651-150">После извлечения файлов в локальной системе простое приложение Spring Boot можно будет редактировать.</span><span class="sxs-lookup"><span data-stu-id="84651-150">After you have extracted the files on your local system, your simple Spring Boot application will be ready for editing.</span></span>

## <a name="configure-your-spring-boot-app-to-use-the-spring-cloud-kafka-stream-and-azure-event-hub-starters"></a><span data-ttu-id="84651-151">Настройка приложения Spring Boot для использования начальных приложений Spring Cloud Kafka Stream и концентратора событий Azure</span><span class="sxs-lookup"><span data-stu-id="84651-151">Configure your Spring Boot app to use the Spring Cloud Kafka Stream and Azure Event Hub starters</span></span>

1. <span data-ttu-id="84651-152">Найдите файл *pom.xml* в корневой папке приложения, например так:</span><span class="sxs-lookup"><span data-stu-id="84651-152">Locate the *pom.xml* file in the root directory of your app; for example:</span></span>

   `C:\SpringBoot\kafka\pom.xml`

   <span data-ttu-id="84651-153">-или-</span><span class="sxs-lookup"><span data-stu-id="84651-153">-or-</span></span>

   `/users/example/home/kafka/pom.xml`

1. <span data-ttu-id="84651-154">Откройте файл *pom.xml* в текстовом редакторе и добавьте начальное приложение Spring Cloud Kafka Stream и начальное приложение концентратора событий Azure в список `<dependencies>`:</span><span class="sxs-lookup"><span data-stu-id="84651-154">Open the *pom.xml* file in a text editor, and add the Spring Cloud Kafka Stream and Azure Event Hub starters to the list of `<dependencies>`:</span></span>

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

1. <span data-ttu-id="84651-156">Сохраните и закройте файл *pom.xml*.</span><span class="sxs-lookup"><span data-stu-id="84651-156">Save and close the *pom.xml* file.</span></span>

## <a name="create-an-azure-credential-file"></a><span data-ttu-id="84651-157">Создание файла учетных данных Azure</span><span class="sxs-lookup"><span data-stu-id="84651-157">Create an Azure Credential File</span></span>

1. <span data-ttu-id="84651-158">Откройте окно командной строки.</span><span class="sxs-lookup"><span data-stu-id="84651-158">Open a command prompt.</span></span>

1. <span data-ttu-id="84651-159">Перейдите к каталогу *resources* приложения Spring Boot, например так:</span><span class="sxs-lookup"><span data-stu-id="84651-159">Navigate to the *resources* directory of your Spring Boot app; for example:</span></span>

   ```shell
   cd C:\SpringBoot\eventhub\src\main\resources
   ```

   <span data-ttu-id="84651-160">-или-</span><span class="sxs-lookup"><span data-stu-id="84651-160">-or-</span></span>

   ```shell
   cd /users/example/home/eventhub/src/main/resources
   ```

1. <span data-ttu-id="84651-161">Вход в учетную запись Azure:</span><span class="sxs-lookup"><span data-stu-id="84651-161">Sign in to your Azure account:</span></span>

   ```azurecli
   az login
   ```

1. <span data-ttu-id="84651-162">Отобразите список подписок:</span><span class="sxs-lookup"><span data-stu-id="84651-162">List your subscriptions:</span></span>

   ```azurecli
   az account list
   ```
   <span data-ttu-id="84651-163">Azure отобразит список подписок, и вам нужно будет скопировать идентификатор GUID для подписки, которая будет использоваться, например:</span><span class="sxs-lookup"><span data-stu-id="84651-163">Azure will return a list of your subscriptions, and you will need to copy the GUID for the subscription that you want to use; for example:</span></span>

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
   
1. <span data-ttu-id="84651-164">Укажите GUID подписки, которую вы собираетесь использовать в Azure, например:</span><span class="sxs-lookup"><span data-stu-id="84651-164">Specify the GUID for the subscription you want to use with Azure; for example:</span></span>

   ```azurecli
   az account set -s 11111111-1111-1111-1111-111111111111
   ```

1. <span data-ttu-id="84651-165">Создайте файл учетных данных Azure:</span><span class="sxs-lookup"><span data-stu-id="84651-165">Create your Azure Credential file:</span></span>

   ```azurecli
   az ad sp create-for-rbac --sdk-auth > my.azureauth
   ```

   <span data-ttu-id="84651-166">Эта команда создаст файл *my.azureauth* в каталоге *resources* приблизительно с таким содержимым:</span><span class="sxs-lookup"><span data-stu-id="84651-166">This command will create a *my.azureauth* file in your *resources* directory with contents that resemble the following example:</span></span>

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

## <a name="configure-your-spring-boot-app-to-use-your-azure-event-hub"></a><span data-ttu-id="84651-167">Настройка приложения Spring Boot для использования концентратора событий Azure</span><span class="sxs-lookup"><span data-stu-id="84651-167">Configure your Spring Boot app to use your Azure Event Hub</span></span>

1. <span data-ttu-id="84651-168">Найдите файл *application.properties* в каталоге *resources* приложения, например так:</span><span class="sxs-lookup"><span data-stu-id="84651-168">Locate the *application.properties* in the *resources* directory of your app; for example:</span></span>

   `C:\SpringBoot\eventhub\src\main\resources\application.properties`

   <span data-ttu-id="84651-169">-или-</span><span class="sxs-lookup"><span data-stu-id="84651-169">-or-</span></span>

   `/users/example/home/eventhub/src/main/resources/application.properties`

2. <span data-ttu-id="84651-170">Откройте файл *application.properties* в текстовом редакторе, добавьте следующие строки и замените примеры значений соответствующими параметрами концентратора событий:</span><span class="sxs-lookup"><span data-stu-id="84651-170">Open the *application.properties* file in a text editor, add the following lines, and then replace the sample values with the appropriate properties for your event hub:</span></span>

   ```yaml
   spring.cloud.azure.credential-file-path=my.azureauth
   spring.cloud.azure.resource-group=wingtiptoysresources
   spring.cloud.azure.region=West US
   spring.cloud.azure.eventhub.namespace=wingtiptoysnamespace

   spring.cloud.stream.bindings.input.destination=wingtiptoyshub
   spring.cloud.stream.bindings.input.group=$Default
   spring.cloud.stream.bindings.output.destination=wingtiptoyshub
   ```
   <span data-ttu-id="84651-171">Описание</span><span class="sxs-lookup"><span data-stu-id="84651-171">Where:</span></span>

   |                       <span data-ttu-id="84651-172">Поле</span><span class="sxs-lookup"><span data-stu-id="84651-172">Field</span></span>                       |                                                                                   <span data-ttu-id="84651-173">ОПИСАНИЕ</span><span class="sxs-lookup"><span data-stu-id="84651-173">Description</span></span>                                                                                    |
   |---------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
   |     `spring.cloud.azure.credential-file-path`     |                                                    <span data-ttu-id="84651-174">Определяет файл учетных данных Azure, который был создан ранее в этом примере.</span><span class="sxs-lookup"><span data-stu-id="84651-174">Specifies Azure credential file that you created earlier in this tutorial.</span></span>                                                    |
   |        `spring.cloud.azure.resource-group`        |                                                      <span data-ttu-id="84651-175">Определяет группу ресурсов Azure, которая содержит концентратор событий Azure.</span><span class="sxs-lookup"><span data-stu-id="84651-175">Specifies the Azure Resource Group that contains your Azure Event Hub.</span></span>                                                      |
   |            `spring.cloud.azure.region`            |                                           <span data-ttu-id="84651-176">Определяет географический регион, указанный при создании концентратора событий Azure.</span><span class="sxs-lookup"><span data-stu-id="84651-176">Specifies the geographical region that you specified when you created your Azure Event Hub.</span></span>                                            |
   |      `spring.cloud.azure.eventhub.namespace`      |                                          <span data-ttu-id="84651-177">Определяет уникальное имя, заданное при создании пространства имен концентратора событий Azure.</span><span class="sxs-lookup"><span data-stu-id="84651-177">Specifies the unique name that you specified when you created your Azure Event Hub Namespace.</span></span>                                           |
   | `spring.cloud.stream.bindings.input.destination`  |                            <span data-ttu-id="84651-178">Определяет назначение входящих данных концентратора событий Azure, которым в этом примере является сам концентратор, созданный ранее.</span><span class="sxs-lookup"><span data-stu-id="84651-178">Specifies the input destination Azure Event Hub, which for this tutorial is the  hub you created earlier in this tutorial.</span></span>                            |
   |    `spring.cloud.stream.bindings.input.group `    | <span data-ttu-id="84651-179">Определяет группу потребителей концентратора событий Azure, для которой можно установить значение $Default, чтобы использовать базовую группу потребителей, созданную вместе с концентратором событий Azure.</span><span class="sxs-lookup"><span data-stu-id="84651-179">Specifies a Consumer Group from Azure Event Hub, which can be set to '$Default' in order to use the basic consumer group that was created when you created your Azure Event Hub.</span></span> |
   | `spring.cloud.stream.bindings.output.destination` |                               <span data-ttu-id="84651-180">Определяет назначение исходящих данных для концентратора событий Azure, которое в этом примере совпадает с назначением входящих данных.</span><span class="sxs-lookup"><span data-stu-id="84651-180">Specifies the output destination Azure Event Hub, which for this tutorial will be the same as the input destination.</span></span>                               |


3. <span data-ttu-id="84651-181">Сохраните и закройте файл *application.properties*.</span><span class="sxs-lookup"><span data-stu-id="84651-181">Save and close the *application.properties* file.</span></span>

## <a name="add-sample-code-to-implement-basic-event-hub-functionality"></a><span data-ttu-id="84651-182">Добавление примера кода для реализации базовых функций концентратора событий</span><span class="sxs-lookup"><span data-stu-id="84651-182">Add sample code to implement basic event hub functionality</span></span>

<span data-ttu-id="84651-183">В этом разделе вы создадите классы Java, требуемые для отправки событий в концентратор событий.</span><span class="sxs-lookup"><span data-stu-id="84651-183">In this section, you create the necessary Java classes for sending events to your event hub.</span></span>

### <a name="modify-the-main-application-class"></a><span data-ttu-id="84651-184">Изменение класса основного приложения</span><span class="sxs-lookup"><span data-stu-id="84651-184">Modify the main application class</span></span>

1. <span data-ttu-id="84651-185">Найдите файл основного приложения Java в каталоге пакета приложения, например:</span><span class="sxs-lookup"><span data-stu-id="84651-185">Locate the main application Java file in the package directory of your app; for example:</span></span>

   `C:\SpringBoot\kafka\src\main\java\com\wingtiptoys\kafka\KafkaApplication.java`

   <span data-ttu-id="84651-186">-или-</span><span class="sxs-lookup"><span data-stu-id="84651-186">-or-</span></span>

   `/users/example/home/kafka/src/main/java/com/wingtiptoys/kafka/KafkaApplication.java`

1. <span data-ttu-id="84651-187">Откройте файл основного приложения Java в текстовом редакторе и добавьте в него следующие строки:</span><span class="sxs-lookup"><span data-stu-id="84651-187">Open the main application Java file in a text editor, and add the following lines to the file:</span></span>

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

1. <span data-ttu-id="84651-188">Сохраните и закройте файл основного приложения Java.</span><span class="sxs-lookup"><span data-stu-id="84651-188">Save and close the main application Java file.</span></span>


### <a name="create-a-new-class-for-the-source-connector"></a><span data-ttu-id="84651-189">Создание класса для соединителя источника</span><span class="sxs-lookup"><span data-stu-id="84651-189">Create a new class for the source connector</span></span>

1. <span data-ttu-id="84651-190">В каталоге пакета вашего приложения создайте файл Java с именем *KafkaSource.java*, а затем откройте этот файл в текстовом редакторе и добавьте следующие строки:</span><span class="sxs-lookup"><span data-stu-id="84651-190">Create a new Java file named *KafkaSource.java* in the package directory of your app, then open the file in a text editor and add the following lines:</span></span>

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

1. <span data-ttu-id="84651-191">Сохраните и закройте файл *KafkaSource.java*.</span><span class="sxs-lookup"><span data-stu-id="84651-191">Save and close the *KafkaSource.java* file.</span></span>

### <a name="create-a-new-class-for-the-sink-connector"></a><span data-ttu-id="84651-192">Создание класса для соединителя приемника</span><span class="sxs-lookup"><span data-stu-id="84651-192">Create a new class for the sink connector</span></span>

1. <span data-ttu-id="84651-193">В каталоге пакета вашего приложения создайте файл Java с именем *KafkaSink.java*, а затем откройте этот файл в текстовом редакторе и добавьте следующие строки:</span><span class="sxs-lookup"><span data-stu-id="84651-193">Create a new Java file named *KafkaSink.java* in the package directory of your app, then open the file in a text editor and add the following lines:</span></span>

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

1. <span data-ttu-id="84651-194">Сохраните и закройте файл *KafkaSink.java*.</span><span class="sxs-lookup"><span data-stu-id="84651-194">Save and close the *KafkaSink.java* file.</span></span>

## <a name="build-and-test-your-application"></a><span data-ttu-id="84651-195">Сборка и тестирование приложения</span><span class="sxs-lookup"><span data-stu-id="84651-195">Build and test your application</span></span>

1. <span data-ttu-id="84651-196">Откройте командную строку и перейдите из каталога в папку с файлом *pom.xml*, например:</span><span class="sxs-lookup"><span data-stu-id="84651-196">Open a command prompt and change directory to the folder where your *pom.xml* file is located; for example:</span></span>

   `cd C:\SpringBoot\kafka`

   <span data-ttu-id="84651-197">-или-</span><span class="sxs-lookup"><span data-stu-id="84651-197">-or-</span></span>

   `cd /users/example/home/kafka`

1. <span data-ttu-id="84651-198">Создайте приложение Spring Boot с помощью Maven и запустите его, например, следующим образом:</span><span class="sxs-lookup"><span data-stu-id="84651-198">Build your Spring Boot application with Maven and run it; for example:</span></span>

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

1. <span data-ttu-id="84651-199">После запуска приложения можно использовать средство *curl*, чтобы протестировать приложение, например:</span><span class="sxs-lookup"><span data-stu-id="84651-199">Once your application is running, you can use *curl* to test your application; for example:</span></span>

   ```shell
   curl -X POST -H "Content-Type: text/plain" -d "hello" http://localhost:8080/messages
   ```
   <span data-ttu-id="84651-200">В журналах приложения должна появиться запись "hello".</span><span class="sxs-lookup"><span data-stu-id="84651-200">You should see "hello" posted to your application's logs.</span></span> <span data-ttu-id="84651-201">Например: </span><span class="sxs-lookup"><span data-stu-id="84651-201">For example:</span></span>

   ```shell
   [http-nio-8080-exec-2] INFO org.apache.kafka.common.utils.AppInfoParser - Kafka version : 1.0.2
   [http-nio-8080-exec-2] INFO org.apache.kafka.common.utils.AppInfoParser - Kafka commitId : 2a121f7b1d402825
   [wingtiptoyshub.container-0-C-1] INFO com.wingtiptoys.kafka.KafkaSink - New message received: hello
   ```


> [!NOTE]
> 
> <span data-ttu-id="84651-202">Для тестирования можно изменить файл *KafkaSource.java*, добавив в него простую HTML-форму, как в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="84651-202">For testing purposes, you could modify your *KafkaSource.java* so that it contains a simple HTML form like the following example:</span></span>
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
> <span data-ttu-id="84651-203">Это позволит использовать веб-браузер для тестирования приложения:</span><span class="sxs-lookup"><span data-stu-id="84651-203">This will allow you to use a web browser to test your application:</span></span>
> 
> ![Тестирование приложения с помощью веб-браузера][TB01]
> 
> <span data-ttu-id="84651-205">После отправки данных формы в приложении отобразятся результаты:</span><span class="sxs-lookup"><span data-stu-id="84651-205">When you submit the form, your application will display the results:</span></span>
> 
> ![Ответ приложения в веб-браузере][TB02]
> 

## <a name="next-steps"></a><span data-ttu-id="84651-207">Дополнительная информация</span><span class="sxs-lookup"><span data-stu-id="84651-207">Next steps</span></span>

<span data-ttu-id="84651-208">Дополнительные сведения о Spring и Azure см. в центре документации об использовании Spring в Azure.</span><span class="sxs-lookup"><span data-stu-id="84651-208">To learn more about Spring and Azure, continue to the Spring on Azure documentation center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="84651-209">Spring в Azure</span><span class="sxs-lookup"><span data-stu-id="84651-209">Spring on Azure</span></span>](/java/azure/spring-framework)

### <a name="additional-resources"></a><span data-ttu-id="84651-210">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="84651-210">Additional Resources</span></span>

<span data-ttu-id="84651-211">Дополнительные сведения о поддержке в Azure Apache Kafka и Stream Binder для концентратора событий см. в статьях:</span><span class="sxs-lookup"><span data-stu-id="84651-211">For more information about Azure support for Event Hub Stream Binder and Apache Kafka, see the following articles:</span></span>

* [<span data-ttu-id="84651-212">Что такое Центры событий Azure?</span><span class="sxs-lookup"><span data-stu-id="84651-212">What is Azure Event Hubs?</span></span>](/azure/event-hubs/event-hubs-about)

* [<span data-ttu-id="84651-213">Центры событий Azure для Apache Kafka</span><span class="sxs-lookup"><span data-stu-id="84651-213">Azure Event Hubs for Apache Kafka</span></span>](/azure/event-hubs/event-hubs-for-kafka-ecosystem-overview)

* [<span data-ttu-id="84651-214">Создание пространства имен службы "Центры событий" и концентратора событий с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="84651-214">Create an Event Hubs namespace and an event hub using the Azure portal</span></span>](/azure/event-hubs/event-hubs-create)

* [<span data-ttu-id="84651-215">Создание Центров событий с поддержкой Apache Kafka</span><span class="sxs-lookup"><span data-stu-id="84651-215">Create Apache Kafka enabled event hubs</span></span>](/azure/event-hubs/event-hubs-create-kafka-enabled)

<span data-ttu-id="84651-216">Дополнительные сведения об использовании Java в Azure см. в статьях [Azure для разработчиков Java] и [Working with Azure DevOps and Java] (Работа с Azure DevOps и Java).</span><span class="sxs-lookup"><span data-stu-id="84651-216">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Working with Azure DevOps and Java].</span></span>

<span data-ttu-id="84651-217">**[Spring Framework]** — это решение с открытым кодом, которое помогает разработчикам Java создавать приложения корпоративного класса.</span><span class="sxs-lookup"><span data-stu-id="84651-217">The **[Spring Framework]** is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="84651-218">Одним из самых популярных проектов, созданных на этой платформе, является проект [Spring Boot]. Он упрощает подход к созданию автономных приложений Java.</span><span class="sxs-lookup"><span data-stu-id="84651-218">One of the more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating stand-alone Java applications.</span></span> <span data-ttu-id="84651-219">В помощь разработчикам, начинающим работать со Spring Boot, по адресу <https://github.com/spring-guides/> доступно несколько примеров пакетов этого приложения.</span><span class="sxs-lookup"><span data-stu-id="84651-219">To help developers get started with Spring Boot, several sample Spring Boot packages are available at <https://github.com/spring-guides/>.</span></span> <span data-ttu-id="84651-220">Помимо выбора из списка основных проектов Spring Boot, **[Spring Initializr]** помогает разработчикам создавать пользовательские приложения Spring Boot.</span><span class="sxs-lookup"><span data-stu-id="84651-220">In addition to choosing from the list of basic Spring Boot projects, the **[Spring Initializr]** helps developers get started with creating custom Spring Boot applications.</span></span>

<!-- URL List -->

[Apache Kafka]: http://kafka.apache.org
[бесплатной учетной записи Azure]: https://azure.microsoft.com/pricing/free-trial/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[Working with Azure DevOps and Java]: /azure/devops/ (Работа с Azure DevOps и Java)
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
