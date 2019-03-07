---
title: Как использовать Spring Boot Starter со службой хранилища Azure
description: Сведения о настройке приложения Spring Initializr с помощью начального приложения службы хранилища Azure.
services: storage
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 12/19/2018
ms.devlang: java
ms.service: storage
ms.tgt_pltfrm: na
ms.topic: article
ms.workload: storage
ms.openlocfilehash: a1f35df5939a51fa5ce50c29752226b6c7649a9d
ms.sourcegitcommit: 1c1412ad5d8960975c3fc7fd3d1948152ef651ef
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/05/2019
ms.locfileid: "57335387"
---
# <a name="how-to-use-the-spring-boot-starter-for-azure-storage"></a><span data-ttu-id="ecd67-103">Как использовать Spring Boot Starter со службой хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="ecd67-103">How to use the Spring Boot Starter for Azure Storage</span></span>

## <a name="overview"></a><span data-ttu-id="ecd67-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="ecd67-104">Overview</span></span>

<span data-ttu-id="ecd67-105">В статье описано, как создать пользовательское приложение с помощью **Spring Initializr** и добавить к нему начальное приложение службы хранилища Azure, а затем отправить большой двоичный объект в учетную запись хранения Azure с помощью этого приложения.</span><span class="sxs-lookup"><span data-stu-id="ecd67-105">This article walks you through creating a custom application using the **Spring Initializr**, then adding the Azure storage starter to your application, and then using your application to upload a blob to your Azure storage account.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ecd67-106">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="ecd67-106">Prerequisites</span></span>

<span data-ttu-id="ecd67-107">Чтобы выполнить действия, описанные в этой статье, необходимо иметь следующие компоненты:</span><span class="sxs-lookup"><span data-stu-id="ecd67-107">The following prerequisites are required in order to follow the steps in this article:</span></span>

* <span data-ttu-id="ecd67-108">Подписка Azure. Если у вас ее еще нет, вы можете активировать [Преимущества для подписчиков MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) или зарегистрироваться для получения [бесплатной учетной записи Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ecd67-108">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free Azure account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="ecd67-109">[Интерфейс командной строки Azure (CLI)](http://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="ecd67-109">The [Azure Command-Line Interface (CLI)](http://docs.microsoft.com/cli/azure/overview).</span></span>
* <span data-ttu-id="ecd67-110">Поддерживаемая версия Java Development Kit (JDK).</span><span class="sxs-lookup"><span data-stu-id="ecd67-110">A supported Java Development Kit (JDK).</span></span> <span data-ttu-id="ecd67-111">Дополнительные сведения о версиях JDK, доступных для разработки в Azure, см. в статье <https://aka.ms/azure-jdks>.</span><span class="sxs-lookup"><span data-stu-id="ecd67-111">For more information about the JDKs available for use when developing on Azure, see <https://aka.ms/azure-jdks>.</span></span>
* <span data-ttu-id="ecd67-112">[Apache Maven](http://maven.apache.org/) версии 3.0 и выше.</span><span class="sxs-lookup"><span data-stu-id="ecd67-112">Apache's [Maven](http://maven.apache.org/), version 3.0 or later.</span></span>

> [!IMPORTANT]
>
> <span data-ttu-id="ecd67-113">Для выполнения операций, описанных в этой статье, требуется Spring Boot 2.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="ecd67-113">Spring Boot version 2.0 or greater is required to complete the steps in this article.</span></span>
>

## <a name="create-an-azure-storage-account-and-blob-container-for-your-application"></a><span data-ttu-id="ecd67-114">Создание учетной записи хранения Azure и контейнера BLOB-объектов для приложения</span><span class="sxs-lookup"><span data-stu-id="ecd67-114">Create an Azure Storage Account and blob container for your application</span></span>

1. <span data-ttu-id="ecd67-115">Перейдите на портал Azure по адресу <https://portal.azure.com/> и выполните вход.</span><span class="sxs-lookup"><span data-stu-id="ecd67-115">Browse to the Azure portal at <https://portal.azure.com/> and sign in.</span></span>

1. <span data-ttu-id="ecd67-116">Щелкните **+Создать ресурс**, **Служба хранилища**, **Учетная запись хранения**.</span><span class="sxs-lookup"><span data-stu-id="ecd67-116">Click **+Create a resource**, then **Storage**, and then click **Storage Account**.</span></span>

   ![Создание учетной записи хранения Azure][IMG01]

1. <span data-ttu-id="ecd67-118">На странице **Создание пространства имен** введите такую информацию:</span><span class="sxs-lookup"><span data-stu-id="ecd67-118">On the **Create Namespace** page, enter the following information:</span></span>

   * <span data-ttu-id="ecd67-119">Уникальное **имя**, которое станет частью URI для учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="ecd67-119">Enter a unique **Name**, which will become part of the URI for your storage account.</span></span> <span data-ttu-id="ecd67-120">Например, если вы зададите **wingtiptoysstorage** в качестве **имени**, URI примет вид *wingtiptoysstorage.core.windows.net*.</span><span class="sxs-lookup"><span data-stu-id="ecd67-120">For example: if you entered **wingtiptoysstorage** for the **Name**, the URI would be *wingtiptoysstorage.core.windows.net*.</span></span>
   * <span data-ttu-id="ecd67-121">Выберите **Хранилище BLOB-объектов** в поле **Тип учетной записи**.</span><span class="sxs-lookup"><span data-stu-id="ecd67-121">Choose **Blob storage** for the **Account kind**.</span></span>
   * <span data-ttu-id="ecd67-122">Укажите **расположение** для учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="ecd67-122">Specify the **Location** for your storage account.</span></span>
   * <span data-ttu-id="ecd67-123">Выберите **подписку**, которую нужно использовать для учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="ecd67-123">Choose the **Subscription** you want to use for your storage account.</span></span>
   * <span data-ttu-id="ecd67-124">Укажите, следует ли создать новую **группу ресурсов** для учетной записи хранения или использовать существующую.</span><span class="sxs-lookup"><span data-stu-id="ecd67-124">Specify whether to create a new **Resource group** for your storage account, or choose an existing resource group.</span></span>

   ![Создание учетной записи хранения Azure][IMG02]

1. <span data-ttu-id="ecd67-126">Указав эти параметры, щелкните **Создать**, чтобы создать учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="ecd67-126">When you have specified the options listed above, click **Create** to create your storage account.</span></span>

1. <span data-ttu-id="ecd67-127">После создания учетной записи хранения на портале Azure щелкните **Большие двоичные объекты** и **+Контейнер**.</span><span class="sxs-lookup"><span data-stu-id="ecd67-127">When the Azure portal has created your storage account, click **Blobs**, then click **+Container**.</span></span>

   ![Создание контейнера больших двоичных объектов][IMG03]

1. <span data-ttu-id="ecd67-129">Введите **имя** для контейнера BLOB-объектов и щелкните **ОК**.</span><span class="sxs-lookup"><span data-stu-id="ecd67-129">Enter a **Name** for your blob container, and then click **OK**.</span></span>

   ![Настройка параметров контейнера BLOB-объектов][IMG04]

1. <span data-ttu-id="ecd67-131">Созданный контейнер BLOB-объектов отобразится в соответствующем списке на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="ecd67-131">The Azure portal will list your blob container after is has been created.</span></span>

   ![Список контейнеров BLOB-объектов][IMG05]

## <a name="create-a-simple-spring-boot-application-with-the-spring-initializr"></a><span data-ttu-id="ecd67-133">Создание простого приложения Spring Boot с помощью Spring Initializr</span><span class="sxs-lookup"><span data-stu-id="ecd67-133">Create a simple Spring Boot application with the Spring Initializr</span></span>

1. <span data-ttu-id="ecd67-134">Перейдите по адресу <https://start.spring.io/>.</span><span class="sxs-lookup"><span data-stu-id="ecd67-134">Browse to <https://start.spring.io/>.</span></span>

1. <span data-ttu-id="ecd67-135">Задайте такие параметры:</span><span class="sxs-lookup"><span data-stu-id="ecd67-135">Specify the following options:</span></span>

   * <span data-ttu-id="ecd67-136">Выберите в соответствующих полях **Maven Project** (Проект Maven) и **Java**.</span><span class="sxs-lookup"><span data-stu-id="ecd67-136">Generate a **Maven** project with **Java**.</span></span>
   * <span data-ttu-id="ecd67-137">Выберите версию **Spring Boot** не ниже версии 2.0.</span><span class="sxs-lookup"><span data-stu-id="ecd67-137">Specify a **Spring Boot** version that is equal to or greater than 2.0.</span></span>
   * <span data-ttu-id="ecd67-138">Заполните поля **Group** (Группа) и **Artifact** (Артефакт) для приложения.</span><span class="sxs-lookup"><span data-stu-id="ecd67-138">Specify the **Group** and **Artifact** names for your application.</span></span>
   * <span data-ttu-id="ecd67-139">Добавьте зависимость **Web** (Веб).</span><span class="sxs-lookup"><span data-stu-id="ecd67-139">Add the **Web** dependency.</span></span>

      ![Основные параметры Spring Initializr][SI01]

   > [!NOTE]
   >
   > <span data-ttu-id="ecd67-141">Spring Initializr использует имена **Group** (Группы) и **Artifact** (Артефакта) для создания имени пакета, как например *com.wingtiptoys.storage*.</span><span class="sxs-lookup"><span data-stu-id="ecd67-141">The Spring Initializr uses the **Group** and **Artifact** names to create the package name; for example: *com.wingtiptoys.storage*.</span></span>
   >

1. <span data-ttu-id="ecd67-142">Указав эти параметры, щелкните **Generate Project** (Создать проект).</span><span class="sxs-lookup"><span data-stu-id="ecd67-142">When you have specified the options listed above, click **Generate Project**.</span></span>

1. <span data-ttu-id="ecd67-143">При появлении запроса скачайте проект на локальный компьютер.</span><span class="sxs-lookup"><span data-stu-id="ecd67-143">When prompted, download the project to a path on your local computer.</span></span>

   ![Скачивание проекта Spring][SI02]

1. <span data-ttu-id="ecd67-145">После извлечения файлов в локальной системе простое приложение Spring Boot можно будет редактировать.</span><span class="sxs-lookup"><span data-stu-id="ecd67-145">After you have extracted the files on your local system, your simple Spring Boot application will be ready for editing.</span></span>

## <a name="configure-your-spring-boot-app-to-use-the-azure-storage-starter"></a><span data-ttu-id="ecd67-146">Настройка приложения Spring Boot для использования начального приложения службы хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="ecd67-146">Configure your Spring Boot app to use the Azure Storage starter</span></span>

1. <span data-ttu-id="ecd67-147">Найдите файл *pom.xml* в корневой папке приложения, например так:</span><span class="sxs-lookup"><span data-stu-id="ecd67-147">Locate the *pom.xml* file in the root directory of your app; for example:</span></span>

   `C:\SpringBoot\storage\pom.xml`

   <span data-ttu-id="ecd67-148">-или-</span><span class="sxs-lookup"><span data-stu-id="ecd67-148">-or-</span></span>

   `/users/example/home/storage/pom.xml`

1. <span data-ttu-id="ecd67-149">Откройте файл *pom.xml* в текстовом редакторе и добавьте начальное приложение Spring Cloud для службы хранилища Azure в список `<dependencies>`:</span><span class="sxs-lookup"><span data-stu-id="ecd67-149">Open the *pom.xml* file in a text editor, and add the Spring Cloud Azure Storage starter to the list of `<dependencies>`:</span></span>

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>spring-azure-starter-storage</artifactId>
      <version>1.0.0.M2</version>
   </dependency>
   ```

   ![Редактирование файла pom.xml][SI03]

1. <span data-ttu-id="ecd67-151">Сохраните и закройте файл *pom.xml*.</span><span class="sxs-lookup"><span data-stu-id="ecd67-151">Save and close the *pom.xml* file.</span></span>

## <a name="create-an-azure-credential-file"></a><span data-ttu-id="ecd67-152">Создание файла учетных данных Azure</span><span class="sxs-lookup"><span data-stu-id="ecd67-152">Create an Azure Credential File</span></span>

1. <span data-ttu-id="ecd67-153">Откройте окно командной строки.</span><span class="sxs-lookup"><span data-stu-id="ecd67-153">Open a command prompt.</span></span>

1. <span data-ttu-id="ecd67-154">Перейдите к каталогу *resources* приложения Spring Boot, например так:</span><span class="sxs-lookup"><span data-stu-id="ecd67-154">Navigate to the *resources* directory of your Spring Boot app; for example:</span></span>

   ```shell
   cd C:\SpringBoot\storage\src\main\resources
   ```

   <span data-ttu-id="ecd67-155">-или-</span><span class="sxs-lookup"><span data-stu-id="ecd67-155">-or-</span></span>

   ```shell
   cd /users/example/home/storage/src/main/resources
   ```

1. <span data-ttu-id="ecd67-156">Вход в учетную запись Azure:</span><span class="sxs-lookup"><span data-stu-id="ecd67-156">Sign in to your Azure account:</span></span>

   ```azurecli
   az login
   ```

1. <span data-ttu-id="ecd67-157">Отобразите список подписок:</span><span class="sxs-lookup"><span data-stu-id="ecd67-157">List your subscriptions:</span></span>

   ```azurecli
   az account list
   ```
   <span data-ttu-id="ecd67-158">Azure отобразит список подписок, и вам нужно будет скопировать идентификатор GUID для подписки, которая будет использоваться, например:</span><span class="sxs-lookup"><span data-stu-id="ecd67-158">Azure will return a list of your subscriptions, and you will need to copy the GUID for the subscription that you want to use; for example:</span></span>

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

1. <span data-ttu-id="ecd67-159">Укажите GUID подписки, которую вы собираетесь использовать в Azure, например:</span><span class="sxs-lookup"><span data-stu-id="ecd67-159">Specify the GUID for the subscription you want to use with Azure; for example:</span></span>

   ```azurecli
   az account set -s 11111111-1111-1111-1111-111111111111
   ```

1. <span data-ttu-id="ecd67-160">Создайте файл учетных данных Azure:</span><span class="sxs-lookup"><span data-stu-id="ecd67-160">Create your Azure Credential file:</span></span>

   ```azurecli
   az ad sp create-for-rbac --sdk-auth > my.azureauth
   ```

   <span data-ttu-id="ecd67-161">Эта команда создаст файл *my.azureauth* в каталоге *resources* приблизительно с таким содержимым:</span><span class="sxs-lookup"><span data-stu-id="ecd67-161">This command will create a *my.azureauth* file in your *resources* directory with contents that resemble the following example:</span></span>

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

## <a name="configure-your-spring-boot-app-to-use-your-azure-storage-account"></a><span data-ttu-id="ecd67-162">Настройка приложения Spring Boot для использования учетной записи хранения Azure</span><span class="sxs-lookup"><span data-stu-id="ecd67-162">Configure your Spring Boot app to use your Azure Storage account</span></span>

1. <span data-ttu-id="ecd67-163">Найдите файл *application.properties* в каталоге *resources* приложения, например так:</span><span class="sxs-lookup"><span data-stu-id="ecd67-163">Locate the *application.properties* in the *resources* directory of your app; for example:</span></span>

   `C:\SpringBoot\storage\src\main\resources\application.properties`

   <span data-ttu-id="ecd67-164">-или-</span><span class="sxs-lookup"><span data-stu-id="ecd67-164">-or-</span></span>

   `/users/example/home/storage/src/main/resources/application.properties`

2. <span data-ttu-id="ecd67-165">Откройте файл *application.properties* в текстовом редакторе, добавьте указанные ниже строки в файл и замените примеры значений соответствующими параметрами учетной записи хранения:</span><span class="sxs-lookup"><span data-stu-id="ecd67-165">Open the *application.properties* file in a text editor, add the following lines, and then replace the sample values with the appropriate properties for your storage account:</span></span>

   ```yaml
   spring.cloud.azure.credential-file-path=my.azureauth
   spring.cloud.azure.resource-group=wingtiptoysresources
   spring.cloud.azure.region=West US
   spring.cloud.azure.storage.account=wingtiptoysstorage
   ```
   <span data-ttu-id="ecd67-166">Описание</span><span class="sxs-lookup"><span data-stu-id="ecd67-166">Where:</span></span>

   |                   <span data-ttu-id="ecd67-167">Поле</span><span class="sxs-lookup"><span data-stu-id="ecd67-167">Field</span></span>                   |                                            <span data-ttu-id="ecd67-168">ОПИСАНИЕ</span><span class="sxs-lookup"><span data-stu-id="ecd67-168">Description</span></span>                                            |
   |-------------------------------------------|---------------------------------------------------------------------------------------------------|
   | `spring.cloud.azure.credential-file-path` |            <span data-ttu-id="ecd67-169">Определяет файл учетных данных Azure, который был создан ранее в этом примере.</span><span class="sxs-lookup"><span data-stu-id="ecd67-169">Specifies Azure credential file that you created earlier in this tutorial.</span></span>             |
   |    `spring.cloud.azure.resource-group`    |           <span data-ttu-id="ecd67-170">Определяет группу ресурсов Azure, которая содержит учетную запись хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="ecd67-170">Specifies the Azure Resource Group that contains your Azure Storage account.</span></span>            |
   |        `spring.cloud.azure.region`        | <span data-ttu-id="ecd67-171">Определяет географический регион, указанный при создании учетной записи хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="ecd67-171">Specifies the geographical region that you specified when you created your Azure Storage account.</span></span> |
   |   `spring.cloud.azure.storage.account`    |            <span data-ttu-id="ecd67-172">Определяет учетную запись хранения Azure, которая была создана ранее в этом примере.</span><span class="sxs-lookup"><span data-stu-id="ecd67-172">Specifies Azure Storage account that you created earlier in this tutorial.</span></span>             |


3. <span data-ttu-id="ecd67-173">Сохраните и закройте файл *application.properties*.</span><span class="sxs-lookup"><span data-stu-id="ecd67-173">Save and close the *application.properties* file.</span></span>

## <a name="add-sample-code-to-implement-basic-azure-storage-functionality"></a><span data-ttu-id="ecd67-174">Добавление примера кода для реализации базовых функций службы хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="ecd67-174">Add sample code to implement basic Azure storage functionality</span></span>

<span data-ttu-id="ecd67-175">В этом разделе вы создадите классы Java, требуемые для хранения большого двоичного объекта в учетной записи хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="ecd67-175">In this section, you create the necessary Java classes for storing a blob in your Azure storage account.</span></span>

### <a name="modify-the-main-application-class"></a><span data-ttu-id="ecd67-176">Изменение класса основного приложения</span><span class="sxs-lookup"><span data-stu-id="ecd67-176">Modify the main application class</span></span>

1. <span data-ttu-id="ecd67-177">Найдите файл основного приложения Java в каталоге пакета приложения, например:</span><span class="sxs-lookup"><span data-stu-id="ecd67-177">Locate the main application Java file in the package directory of your app; for example:</span></span>

   `C:\SpringBoot\storage\src\main\java\com\wingtiptoys\storage\StorageApplication.java`

   <span data-ttu-id="ecd67-178">-или-</span><span class="sxs-lookup"><span data-stu-id="ecd67-178">-or-</span></span>

   `/users/example/home/storage/src/main/java/com/wingtiptoys/storage/StorageApplication.java`

1. <span data-ttu-id="ecd67-179">Откройте файл основного приложения Java в текстовом редакторе и добавьте в него следующие строки:</span><span class="sxs-lookup"><span data-stu-id="ecd67-179">Open the main application Java file in a text editor, and add the following lines to the file:</span></span>

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

1. <span data-ttu-id="ecd67-180">Сохраните и закройте файл основного приложения Java.</span><span class="sxs-lookup"><span data-stu-id="ecd67-180">Save and close the main application Java file.</span></span>

### <a name="add-a-web-controller-class"></a><span data-ttu-id="ecd67-181">Добавление класса веб-контроллера</span><span class="sxs-lookup"><span data-stu-id="ecd67-181">Add a web controller class</span></span>

1. <span data-ttu-id="ecd67-182">Создайте файл Java с именем *WebController.java* в каталоге пакета приложения, например так:</span><span class="sxs-lookup"><span data-stu-id="ecd67-182">Create a new Java file named *WebController.java* in the package directory of your app; for example:</span></span>

   `C:\SpringBoot\storage\src\main\java\com\wingtiptoys\storage\WebController.java`

   <span data-ttu-id="ecd67-183">-или-</span><span class="sxs-lookup"><span data-stu-id="ecd67-183">-or-</span></span>

   `/users/example/home/storage/src/main/java/com/wingtiptoys/storage/WebController.java`

1. <span data-ttu-id="ecd67-184">Откройте файл Java веб-контроллера в текстовом редакторе и добавьте следующие строки:</span><span class="sxs-lookup"><span data-stu-id="ecd67-184">Open the web controller Java file in a text editor, and add the following lines to the file:</span></span>

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

   <span data-ttu-id="ecd67-185">Синтаксис `@Value("blob://[container]/[blob]")` определяет имена контейнера и большого двоичного объекта для хранения данных.</span><span class="sxs-lookup"><span data-stu-id="ecd67-185">Where the `@Value("blob://[container]/[blob]")` syntax respectively defines the names of the container and blob where you want to store the data.</span></span>

1. <span data-ttu-id="ecd67-186">Сохраните и закройте файл Java веб-контроллера.</span><span class="sxs-lookup"><span data-stu-id="ecd67-186">Save and close the web controller Java file.</span></span>

1. <span data-ttu-id="ecd67-187">Откройте командную строку и перейдите из каталога в папку с файлом *pom.xml*, например:</span><span class="sxs-lookup"><span data-stu-id="ecd67-187">Open a command prompt and change directory to the folder where your *pom.xml* file is located; for example:</span></span>

   `cd C:\SpringBoot\storage`

   <span data-ttu-id="ecd67-188">-или-</span><span class="sxs-lookup"><span data-stu-id="ecd67-188">-or-</span></span>

   `cd /users/example/home/storage`

1. <span data-ttu-id="ecd67-189">Создайте приложение Spring Boot с помощью Maven и запустите его, например, следующим образом:</span><span class="sxs-lookup"><span data-stu-id="ecd67-189">Build your Spring Boot application with Maven and run it; for example:</span></span>

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

1. <span data-ttu-id="ecd67-190">После запуска приложения можно использовать средство *curl*, чтобы протестировать приложение, например:</span><span class="sxs-lookup"><span data-stu-id="ecd67-190">Once your application is running, you can use *curl* to test your application; for example:</span></span>

   <span data-ttu-id="ecd67-191">a.</span><span class="sxs-lookup"><span data-stu-id="ecd67-191">a.</span></span> <span data-ttu-id="ecd67-192">Отправьте запрос POST, чтобы обновить содержимое файла:</span><span class="sxs-lookup"><span data-stu-id="ecd67-192">Send a POST request to update a file's contents:</span></span>

      ```shell
      curl -X POST -H "Content-Type: text/plain" -d "Hello World" http://localhost:8080/
      ```

      <span data-ttu-id="ecd67-193">Вы должны получить ответ, подтверждающий обновление файла.</span><span class="sxs-lookup"><span data-stu-id="ecd67-193">You should see a response that the file was updated.</span></span>

   <span data-ttu-id="ecd67-194">b.</span><span class="sxs-lookup"><span data-stu-id="ecd67-194">b.</span></span> <span data-ttu-id="ecd67-195">Отправьте запрос GET, чтобы проверить содержимое файла:</span><span class="sxs-lookup"><span data-stu-id="ecd67-195">Send a GET request to verify the file's contents:</span></span>

      ```shell
      curl -X GET http://localhost:8080/
      ```

     <span data-ttu-id="ecd67-196">Должен отобразиться отправленный вами текст "Hello World".</span><span class="sxs-lookup"><span data-stu-id="ecd67-196">You should see the "Hello World" text that you posted.</span></span>

## <a name="summary"></a><span data-ttu-id="ecd67-197">Сводка</span><span class="sxs-lookup"><span data-stu-id="ecd67-197">Summary</span></span>

<span data-ttu-id="ecd67-198">В этом руководстве описано, как создать приложение Java с помощью **[Spring Initializr]** и добавить к нему начальное приложение службы хранилища Azure, а затем настроить приложение, чтобы отправить большой двоичный объект в учетную запись хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="ecd67-198">In this tutorial, you created a new Java application using the **[Spring Initializr]**, added the Azure storage starter to your application, and then configured your application to upload a blob to your Azure storage account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ecd67-199">Дополнительная информация</span><span class="sxs-lookup"><span data-stu-id="ecd67-199">Next steps</span></span>

<span data-ttu-id="ecd67-200">Дополнительные сведения о Spring и Azure см. в центре документации об использовании Spring в Azure.</span><span class="sxs-lookup"><span data-stu-id="ecd67-200">To learn more about Spring and Azure, continue to the Spring on Azure documentation center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ecd67-201">Spring в Azure</span><span class="sxs-lookup"><span data-stu-id="ecd67-201">Spring on Azure</span></span>](/java/azure/spring-framework)

### <a name="additional-resources"></a><span data-ttu-id="ecd67-202">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="ecd67-202">Additional Resources</span></span>

<span data-ttu-id="ecd67-203">См. дополнительные сведения о других [начальных приложениях Spring Boot для Microsoft Azure](spring-boot-starters-for-azure.md).</span><span class="sxs-lookup"><span data-stu-id="ecd67-203">For more information about the additional Spring Boot Starters that are available for Microsoft Azure, see [Spring Boot Starters for Azure](spring-boot-starters-for-azure.md).</span></span>

<span data-ttu-id="ecd67-204">См. дополнительные сведения о других API-интерфейсах службы хранилища Azure, которые можно вызывать из приложений Spring Boot:</span><span class="sxs-lookup"><span data-stu-id="ecd67-204">For detailed information about additional Azure storage APIs that you can call from your Spring Boot applications, see the following articles:</span></span>
* [<span data-ttu-id="ecd67-205">Использование хранилища BLOB-объектов Azure из Java</span><span class="sxs-lookup"><span data-stu-id="ecd67-205">How to use Azure Blob storage from Java</span></span>](/azure/storage/blobs/storage-java-how-to-use-blob-storage)
* [<span data-ttu-id="ecd67-206">Использование хранилища очередей Azure из Java</span><span class="sxs-lookup"><span data-stu-id="ecd67-206">How to use Azure Queue storage from Java</span></span>](/azure/storage/queues/storage-java-how-to-use-queue-storage)
* [<span data-ttu-id="ecd67-207">Использование хранилища таблиц Azure из Java</span><span class="sxs-lookup"><span data-stu-id="ecd67-207">How to use Azure Table storage from Java</span></span>](/azure/cosmos-db/table-storage-how-to-use-java)
* [<span data-ttu-id="ecd67-208">Использование хранилища файлов Azure из Java</span><span class="sxs-lookup"><span data-stu-id="ecd67-208">How to use Azure File storage from Java</span></span>](/azure/storage/files/storage-java-how-to-use-file-storage)

<!-- IMG List -->

[IMG01]: ./media/configure-spring-boot-starter-java-app-with-azure-storage/create-storage-account-01.png
[IMG02]: ./media/configure-spring-boot-starter-java-app-with-azure-storage/create-storage-account-02.png
[IMG03]: ./media/configure-spring-boot-starter-java-app-with-azure-storage/create-storage-account-03.png
[IMG04]: ./media/configure-spring-boot-starter-java-app-with-azure-storage/create-storage-account-04.png
[IMG05]: ./media/configure-spring-boot-starter-java-app-with-azure-storage/create-storage-account-05.png

[SI01]: ./media/configure-spring-boot-starter-java-app-with-azure-storage/create-project-01.png
[SI02]: ./media/configure-spring-boot-starter-java-app-with-azure-storage/create-project-02.png
[SI03]: ./media/configure-spring-boot-starter-java-app-with-azure-storage/create-project-03.png
