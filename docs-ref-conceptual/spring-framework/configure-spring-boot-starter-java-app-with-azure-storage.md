---
title: Как использовать Spring Boot Starter со службой хранилища Azure
description: Сведения о настройке приложения Spring Initializr с помощью начального приложения службы хранилища Azure.
services: storage
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 09/10/2018
ms.devlang: java
ms.service: storage
ms.tgt_pltfrm: na
ms.topic: article
ms.workload: storage
ms.openlocfilehash: 4838b6dbd354ad941df12933dddfa7f3e7eef905
ms.sourcegitcommit: 4d52e47073fb0b3ac40a2689daea186bad5b1ef5
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/23/2018
ms.locfileid: "49799970"
---
# <a name="how-to-use-the-spring-boot-starter-for-azure-storage"></a><span data-ttu-id="a4632-103">Как использовать Spring Boot Starter со службой хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="a4632-103">How to use the Spring Boot Starter for Azure Storage</span></span>

## <a name="overview"></a><span data-ttu-id="a4632-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="a4632-104">Overview</span></span>

<span data-ttu-id="a4632-105">В статье описано, как создать пользовательское приложение с помощью **Spring Initializr** и добавить к нему начальное приложение службы хранилища Azure, а затем отправить большой двоичный объект в учетную запись хранения Azure с помощью этого приложения.</span><span class="sxs-lookup"><span data-stu-id="a4632-105">This article walks you through creating a custom application using the **Spring Initializr**, then adding the Azure storage starter to your application, and then using your application to upload a blob to your Azure storage account.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a4632-106">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="a4632-106">Prerequisites</span></span>

<span data-ttu-id="a4632-107">Чтобы выполнить действия, описанные в этой статье, необходимо иметь следующие компоненты:</span><span class="sxs-lookup"><span data-stu-id="a4632-107">The following prerequisites are required in order to follow the steps in this article:</span></span>

* <span data-ttu-id="a4632-108">Подписка Azure. Если у вас ее еще нет, вы можете активировать [Преимущества для подписчиков MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) или зарегистрироваться для получения [бесплатной учетной записи Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a4632-108">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free Azure account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="a4632-109">[Интерфейс командной строки Azure (CLI)](http://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a4632-109">The [Azure Command-Line Interface (CLI)](http://docs.microsoft.com/cli/azure/overview).</span></span>
* <span data-ttu-id="a4632-110">Актуальный [пакет разработчиков Java (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/) версии 1.7 и выше.</span><span class="sxs-lookup"><span data-stu-id="a4632-110">An up-to-date [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), version 1.7 or later.</span></span>
* <span data-ttu-id="a4632-111">[Apache Maven](http://maven.apache.org/) версии 3.0 и выше.</span><span class="sxs-lookup"><span data-stu-id="a4632-111">Apache's [Maven](http://maven.apache.org/), version 3.0 or later.</span></span>

> [!IMPORTANT]
>
> <span data-ttu-id="a4632-112">Для выполнения операций, описанных в этой статье, требуется Spring Boot 2.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="a4632-112">Spring Boot version 2.0 or greater is required to complete the steps in this article.</span></span>
>

## <a name="create-an-azure-storage-account-and-blob-container-for-your-application"></a><span data-ttu-id="a4632-113">Создание учетной записи хранения Azure и контейнера BLOB-объектов для приложения</span><span class="sxs-lookup"><span data-stu-id="a4632-113">Create an Azure Storage Account and blob container for your application</span></span>

1. <span data-ttu-id="a4632-114">Перейдите на портал Azure по адресу <https://portal.azure.com/> и выполните вход.</span><span class="sxs-lookup"><span data-stu-id="a4632-114">Browse to the Azure portal at <https://portal.azure.com/> and sign in.</span></span>

1. <span data-ttu-id="a4632-115">Щелкните **+Создать ресурс**, **Служба хранилища**, **Учетная запись хранения**.</span><span class="sxs-lookup"><span data-stu-id="a4632-115">Click **+Create a resource**, then **Storage**, and then click **Storage Account**.</span></span>

   ![Создание учетной записи хранения Azure][IMG01]

1. <span data-ttu-id="a4632-117">На странице **Создание пространства имен** введите такую информацию:</span><span class="sxs-lookup"><span data-stu-id="a4632-117">On the **Create Namespace** page, enter the following information:</span></span>

   * <span data-ttu-id="a4632-118">Уникальное **имя**, которое станет частью URI для учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="a4632-118">Enter a unique **Name**, which will become part of the URI for your storage account.</span></span> <span data-ttu-id="a4632-119">Например, если вы зададите **wingtiptoysstorage** в качестве **имени**, URI примет вид *wingtiptoysstorage.core.windows.net*.</span><span class="sxs-lookup"><span data-stu-id="a4632-119">For example: if you entered **wingtiptoysstorage** for the **Name**, the URI would be *wingtiptoysstorage.core.windows.net*.</span></span>
   * <span data-ttu-id="a4632-120">Выберите **Хранилище BLOB-объектов** в поле **Тип учетной записи**.</span><span class="sxs-lookup"><span data-stu-id="a4632-120">Choose **Blob storage** for the **Account kind**.</span></span>
   * <span data-ttu-id="a4632-121">Укажите **расположение** для учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="a4632-121">Specify the **Location** for your storage account.</span></span>
   * <span data-ttu-id="a4632-122">Выберите **подписку**, которую нужно использовать для учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="a4632-122">Choose the **Subscription** you want to use for your storage account.</span></span>
   * <span data-ttu-id="a4632-123">Укажите, следует ли создать новую **группу ресурсов** для учетной записи хранения или использовать существующую.</span><span class="sxs-lookup"><span data-stu-id="a4632-123">Specify whether to create a new **Resource group** for your storage account, or choose an existing resource group.</span></span>

   ![Создание учетной записи хранения Azure][IMG02]

1. <span data-ttu-id="a4632-125">Указав эти параметры, щелкните **Создать**, чтобы создать учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="a4632-125">When you have specified the options listed above, click **Create** to create your storage account.</span></span>

1. <span data-ttu-id="a4632-126">После создания учетной записи хранения на портале Azure щелкните **Большие двоичные объекты** и **+Контейнер**.</span><span class="sxs-lookup"><span data-stu-id="a4632-126">When the Azure portal has created your storage account, click **Blobs**, then click **+Container**.</span></span>

   ![Создание контейнера больших двоичных объектов][IMG03]

1. <span data-ttu-id="a4632-128">Введите **имя** для контейнера BLOB-объектов и щелкните **ОК**.</span><span class="sxs-lookup"><span data-stu-id="a4632-128">Enter a **Name** for your blob container, and then click **OK**.</span></span>

   ![Настройка параметров контейнера BLOB-объектов][IMG04]

1. <span data-ttu-id="a4632-130">Созданный контейнер BLOB-объектов отобразится в соответствующем списке на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="a4632-130">The Azure portal will list your blob container after is has been created.</span></span>

   ![Список контейнеров BLOB-объектов][IMG05]

## <a name="create-a-simple-spring-boot-application-with-the-spring-initializr"></a><span data-ttu-id="a4632-132">Создание простого приложения Spring Boot с помощью Spring Initializr</span><span class="sxs-lookup"><span data-stu-id="a4632-132">Create a simple Spring Boot application with the Spring Initializr</span></span>

1. <span data-ttu-id="a4632-133">Перейдите по адресу <https://start.spring.io/>.</span><span class="sxs-lookup"><span data-stu-id="a4632-133">Browse to <https://start.spring.io/>.</span></span>

1. <span data-ttu-id="a4632-134">Задайте такие параметры:</span><span class="sxs-lookup"><span data-stu-id="a4632-134">Specify the following options:</span></span>

   * <span data-ttu-id="a4632-135">Выберите в соответствующих полях **Maven Project** (Проект Maven) и **Java**.</span><span class="sxs-lookup"><span data-stu-id="a4632-135">Generate a **Maven** project with **Java**.</span></span>
   * <span data-ttu-id="a4632-136">Выберите версию **Spring Boot** не ниже версии 2.0.</span><span class="sxs-lookup"><span data-stu-id="a4632-136">Specify a **Spring Boot** version that is equal to or greater than 2.0.</span></span>
   * <span data-ttu-id="a4632-137">Заполните поля **Group** (Группа) и **Artifact** (Артефакт) для приложения.</span><span class="sxs-lookup"><span data-stu-id="a4632-137">Specify the **Group** and **Artifact** names for your application.</span></span>
   * <span data-ttu-id="a4632-138">Добавьте зависимость **Web** (Веб).</span><span class="sxs-lookup"><span data-stu-id="a4632-138">Add the **Web** dependency.</span></span>

      ![Основные параметры Spring Initializr][SI01]

   > [!NOTE]
   >
   > <span data-ttu-id="a4632-140">Spring Initializr использует имена **Group** (Группы) и **Artifact** (Артефакта) для создания имени пакета, как например *com.wingtiptoys.storage*.</span><span class="sxs-lookup"><span data-stu-id="a4632-140">The Spring Initializr uses the **Group** and **Artifact** names to create the package name; for example: *com.wingtiptoys.storage*.</span></span>
   >

1. <span data-ttu-id="a4632-141">Указав эти параметры, щелкните **Generate Project** (Создать проект).</span><span class="sxs-lookup"><span data-stu-id="a4632-141">When you have specified the options listed above, click **Generate Project**.</span></span>

1. <span data-ttu-id="a4632-142">При появлении запроса скачайте проект на локальный компьютер.</span><span class="sxs-lookup"><span data-stu-id="a4632-142">When prompted, download the project to a path on your local computer.</span></span>

   ![Скачивание проекта Spring][SI02]

1. <span data-ttu-id="a4632-144">После извлечения файлов в локальной системе простое приложение Spring Boot можно будет редактировать.</span><span class="sxs-lookup"><span data-stu-id="a4632-144">After you have extracted the files on your local system, your simple Spring Boot application will be ready for editing.</span></span>

## <a name="configure-your-spring-boot-app-to-use-the-azure-storage-starter"></a><span data-ttu-id="a4632-145">Настройка приложения Spring Boot для использования начального приложения службы хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="a4632-145">Configure your Spring Boot app to use the Azure Storage starter</span></span>

1. <span data-ttu-id="a4632-146">Найдите файл *pom.xml* в корневой папке приложения, например так:</span><span class="sxs-lookup"><span data-stu-id="a4632-146">Locate the *pom.xml* file in the root directory of your app; for example:</span></span>

   `C:\SpringBoot\storage\pom.xml`

   <span data-ttu-id="a4632-147">-или-</span><span class="sxs-lookup"><span data-stu-id="a4632-147">-or-</span></span>

   `/users/example/home/storage/pom.xml`

1. <span data-ttu-id="a4632-148">Откройте файл *pom.xml* в текстовом редакторе и добавьте начальное приложение Spring Cloud для службы хранилища Azure в список `<dependencies>`:</span><span class="sxs-lookup"><span data-stu-id="a4632-148">Open the *pom.xml* file in a text editor, and add the Spring Cloud Azure Storage starter to the list of `<dependencies>`:</span></span>

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>spring-azure-starter-storage</artifactId>
      <version>1.0.0.M2</version>
   </dependency>
   ```

   ![Редактирование файла pom.xml][SI03]

1. <span data-ttu-id="a4632-150">Сохраните и закройте файл *pom.xml*.</span><span class="sxs-lookup"><span data-stu-id="a4632-150">Save and close the *pom.xml* file.</span></span>

## <a name="create-an-azure-credential-file"></a><span data-ttu-id="a4632-151">Создание файла учетных данных Azure</span><span class="sxs-lookup"><span data-stu-id="a4632-151">Create an Azure Credential File</span></span>

1. <span data-ttu-id="a4632-152">Откройте окно командной строки.</span><span class="sxs-lookup"><span data-stu-id="a4632-152">Open a command prompt.</span></span>

1. <span data-ttu-id="a4632-153">Перейдите к каталогу *resources* приложения Spring Boot, например так:</span><span class="sxs-lookup"><span data-stu-id="a4632-153">Navigate to the *resources* directory of your Spring Boot app; for example:</span></span>

   ```shell
   cd C:\SpringBoot\storage\src\main\resources
   ```

   <span data-ttu-id="a4632-154">-или-</span><span class="sxs-lookup"><span data-stu-id="a4632-154">-or-</span></span>

   ```shell
   cd /users/example/home/storage/src/main/resources
   ```

1. <span data-ttu-id="a4632-155">Вход в учетную запись Azure:</span><span class="sxs-lookup"><span data-stu-id="a4632-155">Sign in to your Azure account:</span></span>

   ```azurecli
   az login
   ```

1. <span data-ttu-id="a4632-156">Отобразите список подписок:</span><span class="sxs-lookup"><span data-stu-id="a4632-156">List your subscriptions:</span></span>

   ```azurecli
   az account list
   ```
   <span data-ttu-id="a4632-157">Azure отобразит список подписок, и вам нужно будет скопировать идентификатор GUID для подписки, которая будет использоваться, например:</span><span class="sxs-lookup"><span data-stu-id="a4632-157">Azure will return a list of your subscriptions, and you will need to copy the GUID for the subscription that you want to use; for example:</span></span>

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

1. <span data-ttu-id="a4632-158">Создайте файл учетных данных Azure:</span><span class="sxs-lookup"><span data-stu-id="a4632-158">Create your Azure Credential file:</span></span>

   ```azurecli
   az ad sp create-for-rbac --sdk-auth > my.azureauth
   ```

   <span data-ttu-id="a4632-159">Эта команда создаст файл *my.azureauth* в каталоге *resources* приблизительно с таким содержимым:</span><span class="sxs-lookup"><span data-stu-id="a4632-159">This command will create a *my.azureauth* file in your *resources* directory with contents that resemble the following example:</span></span>

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

## <a name="configure-your-spring-boot-app-to-use-your-azure-storage-account"></a><span data-ttu-id="a4632-160">Настройка приложения Spring Boot для использования учетной записи хранения Azure</span><span class="sxs-lookup"><span data-stu-id="a4632-160">Configure your Spring Boot app to use your Azure Storage account</span></span>

1. <span data-ttu-id="a4632-161">Найдите файл *application.properties* в каталоге *resources* приложения, например так:</span><span class="sxs-lookup"><span data-stu-id="a4632-161">Locate the *application.properties* in the *resources* directory of your app; for example:</span></span>

   `C:\SpringBoot\storage\src\main\resources\application.properties`

   <span data-ttu-id="a4632-162">-или-</span><span class="sxs-lookup"><span data-stu-id="a4632-162">-or-</span></span>

   `/users/example/home/storage/src/main/resources/application.properties`

2. <span data-ttu-id="a4632-163">Откройте файл *application.properties* в текстовом редакторе, добавьте указанные ниже строки в файл и замените примеры значений соответствующими параметрами учетной записи хранения:</span><span class="sxs-lookup"><span data-stu-id="a4632-163">Open the *application.properties* file in a text editor, add the following lines, and then replace the sample values with the appropriate properties for your storage account:</span></span>

   ```yaml
   spring.cloud.azure.credential-file-path=my.azureauth
   spring.cloud.azure.resource-group=wingtiptoysresources
   spring.cloud.azure.region=West US
   spring.cloud.azure.storage.account=wingtiptoysstorage
   ```
   <span data-ttu-id="a4632-164">Описание</span><span class="sxs-lookup"><span data-stu-id="a4632-164">Where:</span></span>

   |                   <span data-ttu-id="a4632-165">Поле</span><span class="sxs-lookup"><span data-stu-id="a4632-165">Field</span></span>                   |                                            <span data-ttu-id="a4632-166">ОПИСАНИЕ</span><span class="sxs-lookup"><span data-stu-id="a4632-166">Description</span></span>                                            |
   |-------------------------------------------|---------------------------------------------------------------------------------------------------|
   | `spring.cloud.azure.credential-file-path` |            <span data-ttu-id="a4632-167">Определяет файл учетных данных Azure, который был создан ранее в этом примере.</span><span class="sxs-lookup"><span data-stu-id="a4632-167">Specifies Azure credential file that you created earlier in this tutorial.</span></span>             |
   |    `spring.cloud.azure.resource-group`    |           <span data-ttu-id="a4632-168">Определяет группу ресурсов Azure, которая содержит учетную запись хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="a4632-168">Specifies the Azure Resource Group that contains your Azure Storage account.</span></span>            |
   |        `spring.cloud.azure.region`        | <span data-ttu-id="a4632-169">Определяет географический регион, указанный при создании учетной записи хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="a4632-169">Specifies the geographical region that you specified when you created your Azure Storage account.</span></span> |
   |   `spring.cloud.azure.storage.account`    |            <span data-ttu-id="a4632-170">Определяет учетную запись хранения Azure, которая была создана ранее в этом примере.</span><span class="sxs-lookup"><span data-stu-id="a4632-170">Specifies Azure Storage account that you created earlier in this tutorial.</span></span>             |


3. <span data-ttu-id="a4632-171">Сохраните и закройте файл *application.properties*.</span><span class="sxs-lookup"><span data-stu-id="a4632-171">Save and close the *application.properties* file.</span></span>

## <a name="add-sample-code-to-implement-basic-azure-storage-functionality"></a><span data-ttu-id="a4632-172">Добавление примера кода для реализации базовых функций службы хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="a4632-172">Add sample code to implement basic Azure storage functionality</span></span>

<span data-ttu-id="a4632-173">В этом разделе вы создадите классы Java, требуемые для хранения большого двоичного объекта в учетной записи хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="a4632-173">In this section, you create the necessary Java classes for storing a blob in your Azure storage account.</span></span>

### <a name="modify-the-main-application-class"></a><span data-ttu-id="a4632-174">Изменение класса основного приложения</span><span class="sxs-lookup"><span data-stu-id="a4632-174">Modify the main application class</span></span>

1. <span data-ttu-id="a4632-175">Найдите файл основного приложения Java в каталоге пакета приложения, например:</span><span class="sxs-lookup"><span data-stu-id="a4632-175">Locate the main application Java file in the package directory of your app; for example:</span></span>

   `C:\SpringBoot\storage\src\main\java\com\wingtiptoys\storage\StorageApplication.java`

   <span data-ttu-id="a4632-176">-или-</span><span class="sxs-lookup"><span data-stu-id="a4632-176">-or-</span></span>

   `/users/example/home/storage/src/main/java/com/wingtiptoys/storage/StorageApplication.java`

1. <span data-ttu-id="a4632-177">Откройте файл основного приложения Java в текстовом редакторе и добавьте в него следующие строки:</span><span class="sxs-lookup"><span data-stu-id="a4632-177">Open the main application Java file in a text editor, and add the following lines to the file:</span></span>

   ```java
   package com.wingtiptoys.storage;

   import org.springframework.boot.SpringApplication;
   import org.springframework.boot.autoconfigure.SpringBootApplication;

   @SpringBootApplication
   public class StorageApplication {
      public static void main(String[] args) {
         SpringApplication.run(StorageApplication.class, args);
      }
   }
   ```

1. <span data-ttu-id="a4632-178">Сохраните и закройте файл основного приложения Java.</span><span class="sxs-lookup"><span data-stu-id="a4632-178">Save and close the main application Java file.</span></span>

### <a name="add-a-web-controller-class"></a><span data-ttu-id="a4632-179">Добавление класса веб-контроллера</span><span class="sxs-lookup"><span data-stu-id="a4632-179">Add a web controller class</span></span>

1. <span data-ttu-id="a4632-180">Создайте файл Java с именем *WebController.java* в каталоге пакета приложения, например так:</span><span class="sxs-lookup"><span data-stu-id="a4632-180">Create a new Java file named *WebController.java* in the package directory of your app; for example:</span></span>

   `C:\SpringBoot\storage\src\main\java\com\wingtiptoys\storage\WebController.java`

   <span data-ttu-id="a4632-181">-или-</span><span class="sxs-lookup"><span data-stu-id="a4632-181">-or-</span></span>

   `/users/example/home/storage/src/main/java/com/wingtiptoys/storage/WebController.java`

1. <span data-ttu-id="a4632-182">Откройте файл Java веб-контроллера в текстовом редакторе и добавьте следующие строки:</span><span class="sxs-lookup"><span data-stu-id="a4632-182">Open the web controller Java file in a text editor, and add the following lines to the file:</span></span>

   ```java
   package com.wingtiptoys.storage;

   import org.springframework.beans.factory.annotation.Value;
   import org.springframework.core.io.Resource;
   import org.springframework.core.io.WritableResource;
   import org.springframework.util.StreamUtils;
   import org.springframework.web.bind.annotation.GetMapping;
   import org.springframework.web.bind.annotation.PostMapping;
   import org.springframework.web.bind.annotation.RequestBody;
   import org.springframework.web.bind.annotation.RestController;

   import java.io.IOException;
   import java.io.OutputStream;
   import java.nio.charset.Charset;

   @RestController
   public class WebController {

      @Value("blob://test/myfile.txt")
      private Resource blobFile;

      @GetMapping(value = "/")
      public String readBlobFile() throws IOException {
         return StreamUtils.copyToString(
            this.blobFile.getInputStream(),
            Charset.defaultCharset()) + "\n";
      }

      @PostMapping(value = "/")
      public String writeBlobFile(@RequestBody String data) throws IOException {
         try (OutputStream os = ((WritableResource) this.blobFile).getOutputStream()) {
            os.write(data.getBytes());
         }
         return "File was updated.\n";
      }
   }
   ```

   <span data-ttu-id="a4632-183">Синтаксис `@Value("blob://[container]/[blob]")` определяет имена контейнера и большого двоичного объекта для хранения данных.</span><span class="sxs-lookup"><span data-stu-id="a4632-183">Where the `@Value("blob://[container]/[blob]")` syntax respectively defines the names of the container and blob where you want to store the data.</span></span>

1. <span data-ttu-id="a4632-184">Сохраните и закройте файл Java веб-контроллера.</span><span class="sxs-lookup"><span data-stu-id="a4632-184">Save and close the web controller Java file.</span></span>

1. <span data-ttu-id="a4632-185">Откройте командную строку и перейдите из каталога в папку с файлом *pom.xml*, например:</span><span class="sxs-lookup"><span data-stu-id="a4632-185">Open a command prompt and change directory to the folder where your *pom.xml* file is located; for example:</span></span>

   `cd C:\SpringBoot\storage`

   <span data-ttu-id="a4632-186">-или-</span><span class="sxs-lookup"><span data-stu-id="a4632-186">-or-</span></span>

   `cd /users/example/home/storage`

1. <span data-ttu-id="a4632-187">Создайте приложение Spring Boot с помощью Maven и запустите его, например, следующим образом:</span><span class="sxs-lookup"><span data-stu-id="a4632-187">Build your Spring Boot application with Maven and run it; for example:</span></span>

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

1. <span data-ttu-id="a4632-188">После запуска приложения можно использовать средство *curl*, чтобы протестировать приложение, например:</span><span class="sxs-lookup"><span data-stu-id="a4632-188">Once your application is running, you can use *curl* to test your application; for example:</span></span>

   <span data-ttu-id="a4632-189">a.</span><span class="sxs-lookup"><span data-stu-id="a4632-189">a.</span></span> <span data-ttu-id="a4632-190">Отправьте запрос POST, чтобы обновить содержимое файла:</span><span class="sxs-lookup"><span data-stu-id="a4632-190">Send a POST request to update a file's contents:</span></span>

      ```shell
      curl -X POST -H "Content-Type: text/plain" -d "Hello World" http://localhost:8080/
      ```

      <span data-ttu-id="a4632-191">Вы должны получить ответ, подтверждающий обновление файла.</span><span class="sxs-lookup"><span data-stu-id="a4632-191">You should see a response that the file was updated.</span></span>

   <span data-ttu-id="a4632-192">b.</span><span class="sxs-lookup"><span data-stu-id="a4632-192">b.</span></span> <span data-ttu-id="a4632-193">Отправьте запрос GET, чтобы проверить содержимое файла:</span><span class="sxs-lookup"><span data-stu-id="a4632-193">Send a GET request to verify the file's contents:</span></span>

      ```shell
      curl -X GET http://localhost:8080/
      ```

     <span data-ttu-id="a4632-194">Должен отобразиться отправленный вами текст "Hello World".</span><span class="sxs-lookup"><span data-stu-id="a4632-194">You should see the "Hello World" text that you posted.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a4632-195">Дополнительная информация</span><span class="sxs-lookup"><span data-stu-id="a4632-195">Next steps</span></span>

<span data-ttu-id="a4632-196">См. дополнительные сведения о других [начальных приложениях Spring Boot для Microsoft Azure](spring-boot-starters-for-azure.md).</span><span class="sxs-lookup"><span data-stu-id="a4632-196">For more information about the additional Spring Boot Starters that are available for Microsoft Azure, see [Spring Boot Starters for Azure](spring-boot-starters-for-azure.md).</span></span>

<span data-ttu-id="a4632-197">См. дополнительные сведения об интеграции функций Azure в приложения на основе Spring в руководстве по [Spring Framework в Azure](/java/azure/spring-framework/).</span><span class="sxs-lookup"><span data-stu-id="a4632-197">For additional information about integrating Azure functionality into your Spring-based applications, see [Spring Framework on Azure](/java/azure/spring-framework/).</span></span>

<span data-ttu-id="a4632-198">См. дополнительные сведения о других API-интерфейсах службы хранилища Azure, которые можно вызывать из приложений Spring Boot:</span><span class="sxs-lookup"><span data-stu-id="a4632-198">For detailed information about additional Azure storage APIs that you can call from your Spring Boot applications, see the following articles:</span></span>
* [<span data-ttu-id="a4632-199">Использование хранилища BLOB-объектов Azure из Java</span><span class="sxs-lookup"><span data-stu-id="a4632-199">How to use Azure Blob storage from Java</span></span>](/azure/storage/blobs/storage-java-how-to-use-blob-storage)
* [<span data-ttu-id="a4632-200">Использование хранилища очередей Azure из Java</span><span class="sxs-lookup"><span data-stu-id="a4632-200">How to use Azure Queue storage from Java</span></span>](/azure/storage/queues/storage-java-how-to-use-queue-storage)
* [<span data-ttu-id="a4632-201">Использование хранилища таблиц Azure из Java</span><span class="sxs-lookup"><span data-stu-id="a4632-201">How to use Azure Table storage from Java</span></span>](/azure/cosmos-db/table-storage-how-to-use-java)
* [<span data-ttu-id="a4632-202">Использование хранилища файлов Azure из Java</span><span class="sxs-lookup"><span data-stu-id="a4632-202">How to use Azure File storage from Java</span></span>](/azure/storage/files/storage-java-how-to-use-file-storage)

<!-- IMG List -->

[IMG01]: ./media/configure-spring-boot-starter-java-app-with-azure-storage/create-storage-account-01.png
[IMG02]: ./media/configure-spring-boot-starter-java-app-with-azure-storage/create-storage-account-02.png
[IMG03]: ./media/configure-spring-boot-starter-java-app-with-azure-storage/create-storage-account-03.png
[IMG04]: ./media/configure-spring-boot-starter-java-app-with-azure-storage/create-storage-account-04.png
[IMG05]: ./media/configure-spring-boot-starter-java-app-with-azure-storage/create-storage-account-05.png

[SI01]: ./media/configure-spring-boot-starter-java-app-with-azure-storage/create-project-01.png
[SI02]: ./media/configure-spring-boot-starter-java-app-with-azure-storage/create-project-02.png
[SI03]: ./media/configure-spring-boot-starter-java-app-with-azure-storage/create-project-03.png
