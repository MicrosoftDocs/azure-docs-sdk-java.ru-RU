---
title: "Как использовать Spring Boot Starter со службой хранилища Azure"
description: "Сведения о настройке приложения Spring Initializr с помощью начального приложения службы хранилища Azure."
services: storage
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: article
ms.date: 12/01/2017
ms.author: yungez;robmcm
ms.openlocfilehash: 0979c810711a01464c0b2c6e12a582a3f5eefef1
ms.sourcegitcommit: fc48e038721e6910cb8b1f8951df765d517e504d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/06/2017
---
# <a name="how-to-use-the-spring-boot-starter-for-azure-storage"></a><span data-ttu-id="d08b2-103">Как использовать Spring Boot Starter со службой хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="d08b2-103">How to use the Spring Boot Starter for Azure Storage</span></span>

## <a name="overview"></a><span data-ttu-id="d08b2-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="d08b2-104">Overview</span></span>

<span data-ttu-id="d08b2-105">В этой статье описано, как создать с помощью **Spring Initializr** приложения для получения доступа к хранилищу Azure.</span><span class="sxs-lookup"><span data-stu-id="d08b2-105">This article walks you through creating a custom application using the **Spring Initializr**, and then using that application to access Azure storage.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d08b2-106">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="d08b2-106">Prerequisites</span></span>

<span data-ttu-id="d08b2-107">Чтобы выполнить действия, описанные в этой статье, необходимо иметь следующие компоненты:</span><span class="sxs-lookup"><span data-stu-id="d08b2-107">The following prerequisites are required in order to follow the steps in this article:</span></span>

* <span data-ttu-id="d08b2-108">Подписка Azure; если у вас еще нет подписки Azure, вы можете активировать [преимущества для подписчиков MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) или зарегистрироваться для получения [бесплатной учетной записи Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d08b2-108">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free Azure account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="d08b2-109">[Интерфейс командной строки Azure (CLI)](http://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d08b2-109">The [Azure Command-Line Interface (CLI)](http://docs.microsoft.com/cli/azure/overview).</span></span>
* <span data-ttu-id="d08b2-110">Актуальный [пакет разработчиков Java (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/) версии 1.7 и выше.</span><span class="sxs-lookup"><span data-stu-id="d08b2-110">An up-to-date [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), version 1.7 or later.</span></span>
* <span data-ttu-id="d08b2-111">[Apache Maven](http://maven.apache.org/) версии 3.0 и выше.</span><span class="sxs-lookup"><span data-stu-id="d08b2-111">Apache's [Maven](http://maven.apache.org/), version 3.0 or later.</span></span>

## <a name="create-a-custom-application-using-the-spring-initializr"></a><span data-ttu-id="d08b2-112">Создание пользовательского приложения с помощью Spring Initializr</span><span class="sxs-lookup"><span data-stu-id="d08b2-112">Create a custom application using the Spring Initializr</span></span>

1. <span data-ttu-id="d08b2-113">Перейдите по адресу <https://start.spring.io/>.</span><span class="sxs-lookup"><span data-stu-id="d08b2-113">Browse to <https://start.spring.io/>.</span></span>

1. <span data-ttu-id="d08b2-114">Укажите, что необходимо создать проект **Maven** с помощью **Java**, введите имя **группы** и **артефакта** вашего приложения, а затем щелкните ссылку, чтобы **перейти к полной версии** Spring Initializr.</span><span class="sxs-lookup"><span data-stu-id="d08b2-114">Specify that you want to generate a **Maven** project with **Java**, enter the **Group** and **Aritifact** names for your application, and then click the link to **Switch to the full version** of the Spring Initializr.</span></span>

   ![Основные параметры Spring Initializr](media/configure-spring-boot-starter-java-app-with-azure-storage/spring-initializr-basic.png)

   > [!NOTE]
   >
   > <span data-ttu-id="d08b2-116">Spring Initializr будет использовать имена **группы** и **артефакта** для создания имени пакета, например *com.contoso.wingtiptoysdemo*.</span><span class="sxs-lookup"><span data-stu-id="d08b2-116">The Spring Initializr will use the **Group** and **Aritifact** names to create the package name; for example: *com.contoso.wingtiptoysdemo*.</span></span>
   >

1. <span data-ttu-id="d08b2-117">Прокрутите вниз до раздела **Azure** статьи и установите флажок рядом с пунктом **Azure Storage** (Служба хранилища Azure).</span><span class="sxs-lookup"><span data-stu-id="d08b2-117">Scroll down to the **Azure** section and check the box for **Azure Storage**.</span></span>

   ![Все параметры Spring Initializr](media/configure-spring-boot-starter-java-app-with-azure-storage/spring-initializr-advanced.png)

1. <span data-ttu-id="d08b2-119">Прокрутите страницу вниз и нажмите соответствующую кнопку, чтобы **создать проект**.</span><span class="sxs-lookup"><span data-stu-id="d08b2-119">Scroll to the bottom of the page and click the button to **Generate Project**.</span></span>

   ![Все параметры Spring Initializr](media/configure-spring-boot-starter-java-app-with-azure-storage/spring-initializr-generate.png)

1. <span data-ttu-id="d08b2-121">При появлении запроса скачайте проект на локальный компьютер.</span><span class="sxs-lookup"><span data-stu-id="d08b2-121">When prompted, download the project to a path on your local computer.</span></span>

   ![Скачивание пользовательского проекта Spring Boot](media/configure-spring-boot-starter-java-app-with-azure-storage/download-app.png)

## <a name="sign-into-azure-and-select-the-subscription-to-use"></a><span data-ttu-id="d08b2-123">Вход в Azure и выбор подписки для использования</span><span class="sxs-lookup"><span data-stu-id="d08b2-123">Sign into Azure and select the subscription to use</span></span>

1. <span data-ttu-id="d08b2-124">Откройте окно командной строки.</span><span class="sxs-lookup"><span data-stu-id="d08b2-124">Open a command prompt.</span></span>

1. <span data-ttu-id="d08b2-125">Войдите в учетную запись Azure с помощью интерфейса командной строки Azure.</span><span class="sxs-lookup"><span data-stu-id="d08b2-125">Sign into your Azure account by using the Azure CLI:</span></span>

   ```azurecli
   az login
   ```
   <span data-ttu-id="d08b2-126">Для завершения процесса входа следуйте инструкциям.</span><span class="sxs-lookup"><span data-stu-id="d08b2-126">Follow the instructions to complete the sign-in process.</span></span>

1. <span data-ttu-id="d08b2-127">Отобразите список подписок:</span><span class="sxs-lookup"><span data-stu-id="d08b2-127">List your subscriptions:</span></span>

   ```azurecli
   az account list
   ```
   <span data-ttu-id="d08b2-128">Azure отобразит список подписок, и вам нужно будет скопировать идентификатор GUID для подписки, которая будет использоваться, например:</span><span class="sxs-lookup"><span data-stu-id="d08b2-128">Azure will return a list of your subscriptions, and you will need to copy the GUID for the subscription that you want to use; for example:</span></span>

   ```json
   [
     {
       "cloudName": "AzureCloud",
       "id": "ssssssss-ssss-ssss-ssss-ssssssssssss",
       "isDefault": true,
       "name": "Converted Windows Azure MSDN - Visual Studio Ultimate",
       "state": "Enabled",
       "tenantId": "tttttttt-tttt-tttt-tttt-tttttttttttt",
       "user": {
         "name": "contoso@microsoft.com",
         "type": "user"
       }
     }
   ]

1. Specify the GUID for the account you want to use with Azure; for example:

   ```azurecli
   az account set -s ssssssss-ssss-ssss-ssss-ssssssssssss
   ```

## <a name="create-an-azure-storage-account"></a><span data-ttu-id="d08b2-129">Создание учетной записи хранения Azure</span><span class="sxs-lookup"><span data-stu-id="d08b2-129">Create an Azure Storage account</span></span>

1. <span data-ttu-id="d08b2-130">Создайте группу ресурсов Azure, используемых в этой статье, например:</span><span class="sxs-lookup"><span data-stu-id="d08b2-130">Create a resource group for the Azure resources you will use in this article; for example:</span></span>
   ```azurecli
   az group create --name wingtiptoysresources --location westus
   ```
   <span data-ttu-id="d08b2-131">Описание</span><span class="sxs-lookup"><span data-stu-id="d08b2-131">Where:</span></span>
   | <span data-ttu-id="d08b2-132">Параметр</span><span class="sxs-lookup"><span data-stu-id="d08b2-132">Parameter</span></span> | <span data-ttu-id="d08b2-133">Описание</span><span class="sxs-lookup"><span data-stu-id="d08b2-133">Description</span></span> |
   |---|---|
   | `name` | <span data-ttu-id="d08b2-134">Указывает уникальное имя для группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="d08b2-134">Specifies a unique name for your resource group.</span></span> |
   | `location` | <span data-ttu-id="d08b2-135">Указывает [регион Azure](https://azure.microsoft.com/regions/) для размещения группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="d08b2-135">Specifies the [Azure region](https://azure.microsoft.com/regions/) where your resource group will be hosted.</span></span> |

   <span data-ttu-id="d08b2-136">В Azure CLI отобразятся результаты созданной группы ресурсов, например:</span><span class="sxs-lookup"><span data-stu-id="d08b2-136">The Azure CLI will display the results of your resource group creation; for example:</span></span>  

   ```json
   {
     "id": "/subscriptions/ssssssss-ssss-ssss-ssss-ssssssssssss/resourceGroups/wingtiptoysresources",
     "location": "westus",
     "managedBy": null,
     "name": "wingtiptoysresources",
     "properties": {
       "provisioningState": "Succeeded"
     },
     "tags": null
   }
   ```

1. <span data-ttu-id="d08b2-137">Создайте учетную запись хранения Azure в группе ресурсов для приложения Spring Boot, например:</span><span class="sxs-lookup"><span data-stu-id="d08b2-137">Create an Azure storage account in the in the resource group for your Spring Boot app; for example:</span></span>
   ```azurecli
   az storage account create --name wingtiptoysstorage --resource-group wingtiptoysresources --location westus --sku Standard_LRS
   ```
   <span data-ttu-id="d08b2-138">Описание</span><span class="sxs-lookup"><span data-stu-id="d08b2-138">Where:</span></span>
   | <span data-ttu-id="d08b2-139">Параметр</span><span class="sxs-lookup"><span data-stu-id="d08b2-139">Parameter</span></span> | <span data-ttu-id="d08b2-140">Описание</span><span class="sxs-lookup"><span data-stu-id="d08b2-140">Description</span></span> |
   |---|---|
   | `name` | <span data-ttu-id="d08b2-141">Указывает уникальное имя для учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="d08b2-141">Specifies a unique name for your storage account.</span></span> |
   | `resource-group` | <span data-ttu-id="d08b2-142">Указывает имя созданной ранее группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="d08b2-142">Specifies the name of the resource group group you created in the previous step.</span></span> |
   | `location` | <span data-ttu-id="d08b2-143">Указывает [регион Azure](https://azure.microsoft.com/regions/) для размещения учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="d08b2-143">Specifies the [Azure region](https://azure.microsoft.com/regions/) where your storage account will be hosted.</span></span> |
   | `sku` | <span data-ttu-id="d08b2-144">Указывает одно из следующих значений: `Premium_LRS`, `Standard_GRS`, `Standard_LRS`, `Standard_RAGRS`, `Standard_ZRS`.</span><span class="sxs-lookup"><span data-stu-id="d08b2-144">Specifies one of the following: `Premium_LRS`, `Standard_GRS`, `Standard_LRS`, `Standard_RAGRS`, `Standard_ZRS`.</span></span> |

   <span data-ttu-id="d08b2-145">Azure вернет длинную строку JSON, которая содержит сведения о состоянии подготовки, например:</span><span class="sxs-lookup"><span data-stu-id="d08b2-145">Azure will return a long JSON string which contains the provisioning state; for example: |</span></span>
   
   ```json
   {
     "id": "/subscriptions/ssssssss-ssss-ssss-ssss-ssssssssssss/...",
     "identity": null,
     "kind": "Storage"
       ...
       ... (A long list of values will be displayed here.)
       ...
     "statusOfPrimary": "available",
     "statusOfSecondary": null,
     "tags": {},
     "type": "Microsoft.Storage/storageAccounts"
   }
   ```

1. <span data-ttu-id="d08b2-146">Извлеките строку подключения для учетной записи хранения, например:</span><span class="sxs-lookup"><span data-stu-id="d08b2-146">Retrieve the connection string for your storage account; for example:</span></span>
   ```azurecli
   az storage account show-connection-string --name wingtiptoysstorage --resource-group wingtiptoysresources
   ```
   <span data-ttu-id="d08b2-147">Описание</span><span class="sxs-lookup"><span data-stu-id="d08b2-147">Where:</span></span>
   | <span data-ttu-id="d08b2-148">Параметр</span><span class="sxs-lookup"><span data-stu-id="d08b2-148">Parameter</span></span> | <span data-ttu-id="d08b2-149">Описание</span><span class="sxs-lookup"><span data-stu-id="d08b2-149">Description</span></span> |
   | ---|---|
   | `name` | <span data-ttu-id="d08b2-150">Указывает уникальное имя созданной ранее учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="d08b2-150">Specifies a unique name of the storage account you created in previous steps.</span></span> |
   | `resource-group` | <span data-ttu-id="d08b2-151">Указывает имя созданной ранее группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="d08b2-151">Specifies the name of the resource group you created in previous steps.</span></span> |

   <span data-ttu-id="d08b2-152">Azure вернет строку JSON, которая содержит строку подключения для учетной записи хранения, например:</span><span class="sxs-lookup"><span data-stu-id="d08b2-152">Azure will return a JSON string which contains the connection string for your storage account; for example:</span></span>

   ```json
   {
     "connectionString": "DefaultEndpointsProtocol=https;EndpointSuffix=core.windows.net;AccountName=wingtiptoysstorage;AccountKey=AbCdEfGhIjKlMnOpQrStUvWxYz=="
   }
   ```

## <a name="configure-and-compile-your-spring-boot-application"></a><span data-ttu-id="d08b2-153">Настройка и компиляция приложения Spring Boot</span><span class="sxs-lookup"><span data-stu-id="d08b2-153">Configure and compile your Spring Boot application</span></span>

1. <span data-ttu-id="d08b2-154">Распакуйте скачанный архив с файлами проекта в каталог.</span><span class="sxs-lookup"><span data-stu-id="d08b2-154">Extract the files from the downloaded project archive into a directory.</span></span>

1. <span data-ttu-id="d08b2-155">В папке *src/main/resources* проекта откройте файл *application.properties* в текстовом редакторе.</span><span class="sxs-lookup"><span data-stu-id="d08b2-155">Navigate to the *src/main/resources* folder in your project and open the *application.properties* file in a text editor.</span></span>

1. <span data-ttu-id="d08b2-156">Добавьте ключ для учетной записи хранения, например:</span><span class="sxs-lookup"><span data-stu-id="d08b2-156">Add the key for your storage account; for example:</span></span>
   ```yaml
   azure.storage.connection-string=DefaultEndpointsProtocol=https;EndpointSuffix=core.windows.net;AccountName=wingtiptoysstorage;AccountKey=AbCdEfGhIjKlMnOpQrStUvWxYz==
   ```

1. <span data-ttu-id="d08b2-157">В папке */src/main/java/com/example/wingtiptoysdemo* проекта откройте файл *WingtiptoysdemoApplication.java* в текстовом редакторе.</span><span class="sxs-lookup"><span data-stu-id="d08b2-157">Navigate to the */src/main/java/com/example/wingtiptoysdemo* folder in your project and open the *WingtiptoysdemoApplication.java* file in a text editor.</span></span>

1. <span data-ttu-id="d08b2-158">Замените существующий код Java следующим примером, который содержит список больших двоичных объектов в контейнере:</span><span class="sxs-lookup"><span data-stu-id="d08b2-158">Replace the existing Java code with the following example that lists the blobs in a container:</span></span>

   ```java
   package com.example.wingtiptoysdemo;

   import com.microsoft.azure.storage.*;
   import com.microsoft.azure.storage.blob.*;
   import org.springframework.beans.factory.annotation.Autowired;
   import org.springframework.boot.CommandLineRunner;
   import org.springframework.boot.SpringApplication;
   import org.springframework.boot.autoconfigure.SpringBootApplication;

   import java.net.URISyntaxException;

   @SpringBootApplication
   public class WingtiptoysdemoApplication implements CommandLineRunner {

      @Autowired
      private CloudStorageAccount cloudStorageAccount;

      final String containerName = "mycontainer";

      public static void main(String[] args) {
         SpringApplication.run(WingtiptoysdemoApplication.class, args);
      }

      public void run(String... var1)
             throws URISyntaxException, StorageException {
          // Create a container (if it does not exist).
          createContainerIfNotExists(containerName);
          // Upload a blob to the container.
          uploadTextBlob(containerName);
      }

      private void createContainerIfNotExists(String containerName)
            throws URISyntaxException, StorageException {
         try
         {
            // Create a blob client.
            final CloudBlobClient blobClient = cloudStorageAccount.createCloudBlobClient();
            // Get a reference to a container. (Name must be lower case.)
            final CloudBlobContainer container = blobClient.getContainerReference(containerName);
            // Create the container if it does not exist.
            container.createIfNotExists();
         }
         catch (Exception e)
         {
            // Output the stack trace.
            e.printStackTrace();
         }
      }

      private void uploadTextBlob(String containerName)
            throws URISyntaxException, StorageException {
         try
         {
            // Create a blob client.
            final CloudBlobClient blobClient = cloudStorageAccount.createCloudBlobClient();
            // Get a reference to a container. (Name must be lower case.)
            final CloudBlobContainer container = blobClient.getContainerReference(containerName);
            // Get a blob reference for a text file.
            CloudBlockBlob blob = container.getBlockBlobReference("test.txt");
            // Upload some text into the blob.
            blob.uploadText("Hello World!");
         }
         catch (Exception e)
         {
            // Output the stack trace.
            e.printStackTrace();
         }
      }
   }
   ```
   > [!NOTE]
   >
   > <span data-ttu-id="d08b2-159">Этот пример автоматически передает параметры учетной записи хранения, определенные в файле *application.properties*.</span><span class="sxs-lookup"><span data-stu-id="d08b2-159">The above example autowires the storage account settings that you defined in the *application.properties* file.</span></span>
   >

1. <span data-ttu-id="d08b2-160">Скомпилируйте и запустите приложение:</span><span class="sxs-lookup"><span data-stu-id="d08b2-160">Compile and run the application:</span></span>
   ```shell
   mvn clean package spring-boot:run
   ```
   
   <span data-ttu-id="d08b2-161">Приложение создаст контейнер и отправит в контейнер текстовый файл как большой двоичный объект, который появится в списке в вашей учетной записи хранения на [портале Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d08b2-161">The application will create a container and upload a text file as a blob to the container, which will be listed under your storage account in the [Azure portal](https://portal.azure.com).</span></span>

   ![Список больших двоичных объектов на портале Azure](media/configure-spring-boot-starter-java-app-with-azure-storage/list-blobs-in-portal.png)

   > [!NOTE]
   > 
   > <span data-ttu-id="d08b2-163">При компиляции приложения может появиться следующее сообщение об ошибке:</span><span class="sxs-lookup"><span data-stu-id="d08b2-163">When you compile your application, you might see the following error message:</span></span>
   > 
   > `[INFO] ------------------------------------------------------------------------`<br/>
   > `[INFO] BUILD FAILURE`<br/>
   > `[INFO] ------------------------------------------------------------------------`<br/>
   > `[INFO] Total time: 2.616 s`<br/>
   > `[INFO] Finished at: 2017-11-11T13:14:15Z`<br/>
   > `[INFO] Final Memory: 26M/213M`<br/>
   > `[INFO] ------------------------------------------------------------------------`<br/>
   > `[ERROR] Failed to execute goal org.apache.maven.plugins:maven-surefire-plugin:2`<br/>
   > `.18.1:test (default-test) on project wingtiptoysdemo: Execution default-test of`<br/>
   > `goal org.apache.maven.plugins:maven-surefire-plugin:2.18.1:test failed: The for`<br/>
   > `ked VM terminated without properly saying goodbye. VM crash or System.exit called?`<br/>
   > `[ERROR] Command was /bin/sh -c cd /home/robert/SpringBoot/wingtiptoysdemo && /u`<br/>
   > `sr/lib/jvm/java-8-openjdk-amd64/jre/bin/java -jar /home/robert/SpringBoot/wingt`<br/>
   > `iptoysdemo/target/surefire/surefirebooter6371623993063346766.jar /home/robert/S`<br/>
   > `pringBoot/wingtiptoysdemo/target/surefire/surefire5107893623933537917tmp /home/`<br/>
   > `robert/SpringBoot/wingtiptoysdemo/target/surefire/surefire_01414159391084128068tmp`<br/>
   > `[ERROR] -> [Help 1]`<br/>
   > 
   > <span data-ttu-id="d08b2-164">В таком случае можно отключить тестирование Maven Surefire. Для этого добавьте следующую запись подключаемого модуля в файл *pom.xml*:</span><span class="sxs-lookup"><span data-stu-id="d08b2-164">If this happens, you might want to disable the Maven Surefire testing; to do so, add the following plugin entry in your *pom.xml* file:</span></span>
   > 
   > ```xml
   > <plugin>
   >   <groupId>org.apache.maven.plugins</groupId>
   >   <artifactId>maven-surefire-plugin</artifactId>
   >   <version>2.20.1</version>
   >   <configuration>
   >     <skipTests>true</skipTests>
   >   </configuration>
   > </plugin>
   > ```
   > 

## <a name="next-steps"></a><span data-ttu-id="d08b2-165">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d08b2-165">Next steps</span></span>

<span data-ttu-id="d08b2-166">См. дополнительные сведения о других [начальных приложениях Spring Boot для Microsoft Azure](spring-boot-starters-for-azure.md).</span><span class="sxs-lookup"><span data-stu-id="d08b2-166">For more information about the additional Spring Boot Starters that are available for Microsoft Azure, see [Spring Boot Starters for Azure](spring-boot-starters-for-azure.md).</span></span>

<span data-ttu-id="d08b2-167">См. дополнительные сведения об интеграции функций Azure в приложения на основе Spring в руководстве по [Spring Framework в Azure](/java/azure/spring-framework/).</span><span class="sxs-lookup"><span data-stu-id="d08b2-167">For additional information about integrating Azure functionality into your Spring-based applications, see [Spring Framework on Azure](/java/azure/spring-framework/).</span></span>

<span data-ttu-id="d08b2-168">См. дополнительные сведения о других API-интерфейсах службы хранилища Azure, которые можно вызывать из приложений Spring Boot:</span><span class="sxs-lookup"><span data-stu-id="d08b2-168">For detailed information about additional Azure storage APIs that you can call from your Spring Boot applications, see the following articles:</span></span>
* [<span data-ttu-id="d08b2-169">Использование хранилища BLOB-объектов Azure из Java</span><span class="sxs-lookup"><span data-stu-id="d08b2-169">How to use Azure Blob storage from Java</span></span>](/azure/storage/blobs/storage-java-how-to-use-blob-storage)
* [<span data-ttu-id="d08b2-170">Использование хранилища очередей Azure из Java</span><span class="sxs-lookup"><span data-stu-id="d08b2-170">How to use Azure Queue storage from Java</span></span>](/azure/storage/queues/storage-java-how-to-use-queue-storage)
* [<span data-ttu-id="d08b2-171">Использование хранилища таблиц Azure из Java</span><span class="sxs-lookup"><span data-stu-id="d08b2-171">How to use Azure Table storage from Java</span></span>](/azure/cosmos-db/table-storage-how-to-use-java)
* [<span data-ttu-id="d08b2-172">Использование хранилища файлов Azure из Java</span><span class="sxs-lookup"><span data-stu-id="d08b2-172">How to use Azure File storage from Java</span></span>](/azure/storage/files/storage-java-how-to-use-file-storage)
