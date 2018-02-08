---
title: "Начальные приложения Spring Boot для Azure"
description: "В этой статье описаны разные начальные приложения Spring Boot Starter, доступные для Azure."
services: 
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
ms.assetid: 
ms.author: robmcm
ms.date: 02/01/2018
ms.devlang: java
ms.service: multiple
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: na
ms.openlocfilehash: 678d4b279cecb83c95b3bf0f6bcdf1581924aa62
ms.sourcegitcommit: 151aaa6ccc64d94ed67f03e846bab953bde15b4a
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/03/2018
---
# <a name="spring-boot-starters-for-azure"></a><span data-ttu-id="e9cde-103">Spring Boot Starter для Azure</span><span class="sxs-lookup"><span data-stu-id="e9cde-103">Spring Boot Starters for Azure</span></span>

<span data-ttu-id="e9cde-104">В этой статье описаны разные начальные приложения Spring Boot Starter для [Spring Initializr], которые предоставляют разработчикам Java функции интеграции для работы с Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="e9cde-104">This article describes the various Spring Boot Starters for the [Spring Initializr] that provide Java developers with integration features for working with Microsoft Azure.</span></span>

![Spring Boot Starter для Azure][spring-boot-starters]

<span data-ttu-id="e9cde-106">Сейчас для Azure доступны следующие начальные приложения Spring Boot:</span><span class="sxs-lookup"><span data-stu-id="e9cde-106">The following Spring Boot Starters are currently available for Azure:</span></span>

* <span data-ttu-id="e9cde-107">**[Служба поддержки Azure](#azure-support)**</span><span class="sxs-lookup"><span data-stu-id="e9cde-107">**[Azure Support](#azure-support)**</span></span>

   <span data-ttu-id="e9cde-108">Предоставляет поддержку автоматической настройки для служб Azure, включая служебную шину, службу хранилища, Active Directory и т. д.</span><span class="sxs-lookup"><span data-stu-id="e9cde-108">Provides auto-configuration support for Azure Services; e.g. Service Bus, Storage, Active Directory, etc.</span></span>

* <span data-ttu-id="e9cde-109">**[Azure Active Directory](#azure-active-directory)**</span><span class="sxs-lookup"><span data-stu-id="e9cde-109">**[Azure Active Directory](#azure-active-directory)**</span></span>

   <span data-ttu-id="e9cde-110">Предоставляет поддержку интеграции для Spring Security с Azure Active Directory для аутентификации.</span><span class="sxs-lookup"><span data-stu-id="e9cde-110">Provides integration support for Spring Security with Azure Active Directory for authentication.</span></span>

* <span data-ttu-id="e9cde-111">**[Azure Key Vault](#azure-key-vault)**</span><span class="sxs-lookup"><span data-stu-id="e9cde-111">**[Azure Key Vault](#azure-key-vault)**</span></span>

   <span data-ttu-id="e9cde-112">Начальное приложение Spring Boot поддерживает интеграцию с секретами Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="e9cde-112">Provides Spring value annotation support for integration with Azure Key Vault Secrets.</span></span>

* <span data-ttu-id="e9cde-113">**[Служба хранилища Azure](#azure-storage)**</span><span class="sxs-lookup"><span data-stu-id="e9cde-113">**[Azure Storage](#azure-storage)**</span></span>

   <span data-ttu-id="e9cde-114">Spring Boot поддерживает службы хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="e9cde-114">Provides Spring Boot support for Azure Storage services.</span></span>

<a name="azure-support"></a>
## <a name="azure-support"></a><span data-ttu-id="e9cde-115">Поддержка Azure</span><span class="sxs-lookup"><span data-stu-id="e9cde-115">Azure Support</span></span>

<span data-ttu-id="e9cde-116">Это начальное приложение Spring Boot поддерживает автоматическую настройку таких служб Azure, как служебная шина, служба хранилища, Active Directory, Cosmos DB, Key Vault, и т. д.</span><span class="sxs-lookup"><span data-stu-id="e9cde-116">This Spring Boot Starter provides auto-configuration support for Azure Services; for example: Service Bus, Storage, Active Directory, Cosmos DB, Key Vault, etc.</span></span>

<span data-ttu-id="e9cde-117">Примеры использования разных функций Azure с этим начальным приложением, см. по следующей ссылке:</span><span class="sxs-lookup"><span data-stu-id="e9cde-117">For examples of how to use the various Azure features that are provided by this starter, see the following:</span></span>

* <span data-ttu-id="e9cde-118"><https://github.com/Microsoft/azure-spring-boot/tree/master/azure-spring-boot-samples></span><span class="sxs-lookup"><span data-stu-id="e9cde-118"><https://github.com/Microsoft/azure-spring-boot/tree/master/azure-spring-boot-samples></span></span>

<span data-ttu-id="e9cde-119">Когда вы добавляете это начальное приложение в проект Spring Boot, в файл *pom.xml* вносятся следующие изменения:</span><span class="sxs-lookup"><span data-stu-id="e9cde-119">When you add this starter to a Spring Boot project, the following changes are made to the *pom.xml* file:</span></span>

* <span data-ttu-id="e9cde-120">В элемент `<properties>` добавляется следующее свойство:</span><span class="sxs-lookup"><span data-stu-id="e9cde-120">The following property is added to `<properties>` element:</span></span>

   ```xml
   <properties>
      <!-- Other properties will be listed here -->
      <azure.version>0.2.0</azure.version>
   </properties>
   ```

* <span data-ttu-id="e9cde-121">Стандартная зависимость `spring-boot-starter` заменяется следующим образом:</span><span class="sxs-lookup"><span data-stu-id="e9cde-121">The default `spring-boot-starter` dependency is replaced with the following:</span></span>

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-spring-boot</artifactId>
   </dependency>
   ```

* <span data-ttu-id="e9cde-122">В файл добавляется следующий раздел:</span><span class="sxs-lookup"><span data-stu-id="e9cde-122">The following section is added to the file:</span></span>

   ```xml
   <dependencyManagement>
      <dependencies>
         <dependency>
            <groupId>com.microsoft.azure</groupId>
            <artifactId>azure-spring-boot-bom</artifactId>
            <version>${azure.version}</version>
            <type>pom</type>
            <scope>import</scope>
         </dependency>
      </dependencies>
   </dependencyManagement>
   ```

<a name="azure-active-directory"></a>
## <a name="azure-active-directory"></a><span data-ttu-id="e9cde-123">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e9cde-123">Azure Active Directory</span></span>

<span data-ttu-id="e9cde-124">Это начальное приложение Spring Boot поддерживает автоматическую настройку Spring Security, обеспечивая интеграцию с Azure Active Directory для аутентификации.</span><span class="sxs-lookup"><span data-stu-id="e9cde-124">This Spring Boot Starter provides auto-configuration support for Spring Security in order to provide integration with Azure Active Directory for authentication.</span></span>

<span data-ttu-id="e9cde-125">Примеры использования функций Azure Active Directory с этим начальным приложением, см. по следующей ссылке:</span><span class="sxs-lookup"><span data-stu-id="e9cde-125">For examples of how to use the Azure Active Directory features that are provided by this starter, see the following:</span></span>

* <span data-ttu-id="e9cde-126"><https://github.com/Microsoft/azure-spring-boot/tree/master/azure-spring-boot-samples/azure-active-directory-spring-boot-sample></span><span class="sxs-lookup"><span data-stu-id="e9cde-126"><https://github.com/Microsoft/azure-spring-boot/tree/master/azure-spring-boot-samples/azure-active-directory-spring-boot-sample></span></span>

<span data-ttu-id="e9cde-127">Когда вы добавляете это начальное приложение в проект Spring Boot, в файл *pom.xml* вносятся следующие изменения:</span><span class="sxs-lookup"><span data-stu-id="e9cde-127">When you add this starter to a Spring Boot project, the following changes are made to the *pom.xml* file:</span></span>

* <span data-ttu-id="e9cde-128">В элемент `<properties>` добавляется следующее свойство:</span><span class="sxs-lookup"><span data-stu-id="e9cde-128">The following property is added to `<properties>` element:</span></span>

   ```xml
   <properties>
      <!-- Other properties will be listed here -->
      <azure.version>0.2.0</azure.version>
   </properties>
   ```

* <span data-ttu-id="e9cde-129">Стандартная зависимость `spring-boot-starter` заменяется следующим образом:</span><span class="sxs-lookup"><span data-stu-id="e9cde-129">The default `spring-boot-starter` dependency is replaced with the following:</span></span>

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-active-directory-spring-boot-starter</artifactId>
   </dependency>
   ```

* <span data-ttu-id="e9cde-130">В файл добавляется следующий раздел:</span><span class="sxs-lookup"><span data-stu-id="e9cde-130">The following section is added to the file:</span></span>

   ```xml
   <dependencyManagement>
      <dependencies>
         <dependency>
            <groupId>com.microsoft.azure</groupId>
            <artifactId>azure-spring-boot-bom</artifactId>
            <version>${azure.version}</version>
            <type>pom</type>
            <scope>import</scope>
         </dependency>
      </dependencies>
   </dependencyManagement>
   ```

<a name="azure-key-vault"></a>
## <a name="azure-key-vault"></a><span data-ttu-id="e9cde-131">Хранилище ключей Azure</span><span class="sxs-lookup"><span data-stu-id="e9cde-131">Azure Key Vault</span></span>

<span data-ttu-id="e9cde-132">Приложение Spring Boot Starter обеспечивает поддержку заметок со значениями Spring для интеграции с секретами Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="e9cde-132">This Spring Boot Starter provides Spring value annotation support for integration with Azure Key Vault Secrets.</span></span>

<span data-ttu-id="e9cde-133">Примеры использования функций Azure Key Vault, предоставляемых этим начальным приложением, см. по следующей ссылке:</span><span class="sxs-lookup"><span data-stu-id="e9cde-133">For examples of how to use the Azure Key Vault features that are provided by this starter, see the following:</span></span>

* <span data-ttu-id="e9cde-134"><https://github.com/Microsoft/azure-spring-boot/tree/master/azure-spring-boot-samples/azure-keyvault-secrets-spring-boot-sample></span><span class="sxs-lookup"><span data-stu-id="e9cde-134"><https://github.com/Microsoft/azure-spring-boot/tree/master/azure-spring-boot-samples/azure-keyvault-secrets-spring-boot-sample></span></span>

<span data-ttu-id="e9cde-135">Когда вы добавляете это начальное приложение в проект Spring Boot, в файл *pom.xml* вносятся следующие изменения:</span><span class="sxs-lookup"><span data-stu-id="e9cde-135">When you add this starter to a Spring Boot project, the following changes are made to the *pom.xml* file:</span></span>

* <span data-ttu-id="e9cde-136">В элемент `<properties>` добавляется следующее свойство:</span><span class="sxs-lookup"><span data-stu-id="e9cde-136">The following property is added to `<properties>` element:</span></span>

   ```xml
   <properties>
      <!-- Other properties will be listed here -->
      <azure.version>0.2.0</azure.version>
   </properties>
   ```

* <span data-ttu-id="e9cde-137">Стандартная зависимость `spring-boot-starter` заменяется следующим образом:</span><span class="sxs-lookup"><span data-stu-id="e9cde-137">The default `spring-boot-starter` dependency is replaced with the following:</span></span>

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-keyvault-secrets-spring-boot-starter</artifactId>
   </dependency>
   ```

* <span data-ttu-id="e9cde-138">В файл добавляется следующий раздел:</span><span class="sxs-lookup"><span data-stu-id="e9cde-138">The following section is added to the file:</span></span>

   ```xml
   <dependencyManagement>
      <dependencies>
         <dependency>
            <groupId>com.microsoft.azure</groupId>
            <artifactId>azure-spring-boot-bom</artifactId>
            <version>${azure.version}</version>
            <type>pom</type>
            <scope>import</scope>
         </dependency>
      </dependencies>
   </dependencyManagement>
   ```

<a name="azure-storage"></a>
## <a name="azure-storage"></a><span data-ttu-id="e9cde-139">Хранилище Azure</span><span class="sxs-lookup"><span data-stu-id="e9cde-139">Azure Storage</span></span>

<span data-ttu-id="e9cde-140">Начальное приложение Spring Boot Starter обеспечивает поддержку интеграции Spring Boot для служб хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="e9cde-140">This Spring Boot Starter provides Spring Boot integration support for Azure Storage services.</span></span>

<span data-ttu-id="e9cde-141">Примеры использования функций службы хранилища Azure, предоставляемых этим начальным приложением, см. по следующей ссылке:</span><span class="sxs-lookup"><span data-stu-id="e9cde-141">For examples of how to use the Azure Storage features that are provided by this starter, see the following:</span></span>

* [<span data-ttu-id="e9cde-142">Как использовать Spring Boot Starter со службой хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="e9cde-142">How to use the Spring Boot Starter for Azure Storage</span></span>](configure-spring-boot-starter-java-app-with-azure-storage.md)

* <span data-ttu-id="e9cde-143"><https://github.com/Microsoft/azure-spring-boot/tree/master/azure-spring-boot-samples/azure-storage-spring-boot-sample></span><span class="sxs-lookup"><span data-stu-id="e9cde-143"><https://github.com/Microsoft/azure-spring-boot/tree/master/azure-spring-boot-samples/azure-storage-spring-boot-sample></span></span>

<span data-ttu-id="e9cde-144">Когда вы добавляете это начальное приложение в проект Spring Boot, в файл *pom.xml* вносятся следующие изменения:</span><span class="sxs-lookup"><span data-stu-id="e9cde-144">When you add this starter to a Spring Boot project, the following changes are made to the *pom.xml* file:</span></span>

* <span data-ttu-id="e9cde-145">В элемент `<properties>` добавляется следующее свойство:</span><span class="sxs-lookup"><span data-stu-id="e9cde-145">The following property is added to `<properties>` element:</span></span>

   ```xml
   <properties>
      <!-- Other properties will be listed here -->
      <azure.version>0.2.0</azure.version>
   </properties>
   ```

* <span data-ttu-id="e9cde-146">Стандартная зависимость `spring-boot-starter` заменяется следующим образом:</span><span class="sxs-lookup"><span data-stu-id="e9cde-146">The default `spring-boot-starter` dependency is replaced with the following:</span></span>

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-storage-spring-boot-starter</artifactId>
   </dependency>
   ```

* <span data-ttu-id="e9cde-147">В файл добавляется следующий раздел:</span><span class="sxs-lookup"><span data-stu-id="e9cde-147">The following section is added to the file:</span></span>

   ```xml
   <dependencyManagement>
      <dependencies>
         <dependency>
            <groupId>com.microsoft.azure</groupId>
            <artifactId>azure-spring-boot-bom</artifactId>
            <version>${azure.version}</version>
            <type>pom</type>
            <scope>import</scope>
         </dependency>
      </dependencies>
   </dependencyManagement>
   ```

## <a name="next-steps"></a><span data-ttu-id="e9cde-148">Дополнительная информация</span><span class="sxs-lookup"><span data-stu-id="e9cde-148">Next steps</span></span>

<span data-ttu-id="e9cde-149">Дополнительные сведения об использовании [приложений Spring Boot] в Azure см. [здесь].</span><span class="sxs-lookup"><span data-stu-id="e9cde-149">For more information about using [Spring Boot] applications on Azure, see [Spring on Azure].</span></span>

<span data-ttu-id="e9cde-150">Дополнительные сведения об использовании Azure с Java см. в руководствах по [Azure для разработчиков Java] и [инструментах Java для Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="e9cde-150">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="e9cde-151">Справку по началу работы с собственными приложениями Spring Boot см. на странице **Spring Initializr** по адресу https://start.spring.io/.</span><span class="sxs-lookup"><span data-stu-id="e9cde-151">For help with getting started with your own Spring Boot applications, see the **Spring Initializr** at https://start.spring.io/.</span></span>

<!-- URL List -->

[Azure для разработчиков Java]: https://docs.microsoft.com/java/azure/
[инструментах Java для Visual Studio Team Services]: https://java.visualstudio.com/ (Инструменты Java для Visual Studio Team Services)
[приложений Spring Boot]: http://projects.spring.io/spring-boot/
[здесь]: https://docs.microsoft.com/java/azure/spring-framework/
[Spring Framework]: https://spring.io/
[Spring Initializr]: https://start.spring.io/

<!-- IMG List -->

[spring-boot-starters]: media/spring-boot-starters-for-azure/spring-boot-starters-cropped.png
