---
title: Начальные приложения Spring Boot для Azure
description: В этой статье описаны разные начальные приложения Spring Boot Starter, доступные для Azure.
services: ''
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 12/19/2018
ms.devlang: java
ms.service: multiple
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: na
ms.openlocfilehash: 69c0381313994796af31d5301ceadb9f6f40dcb5
ms.sourcegitcommit: f0f140b0862ca5338b1b7e5c33cec3e58a70b8fd
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/03/2019
ms.locfileid: "53991558"
---
# <a name="spring-boot-starters-for-azure"></a><span data-ttu-id="d7b7f-103">Spring Boot Starter для Azure</span><span class="sxs-lookup"><span data-stu-id="d7b7f-103">Spring Boot Starters for Azure</span></span>

<span data-ttu-id="d7b7f-104">В этой статье описаны разные начальные приложения Spring Boot Starter для [Spring Initializr], которые предоставляют разработчикам Java функции интеграции для работы с Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="d7b7f-104">This article describes the various Spring Boot Starters for the [Spring Initializr] that provide Java developers with integration features for working with Microsoft Azure.</span></span>

![Spring Boot Starter для Azure][spring-boot-starters]

<span data-ttu-id="d7b7f-106">Сейчас для Azure доступны следующие начальные приложения Spring Boot:</span><span class="sxs-lookup"><span data-stu-id="d7b7f-106">The following Spring Boot Starters are currently available for Azure:</span></span>

* <span data-ttu-id="d7b7f-107">**[Служба поддержки Azure](#azure-support)**</span><span class="sxs-lookup"><span data-stu-id="d7b7f-107">**[Azure Support](#azure-support)**</span></span>

   <span data-ttu-id="d7b7f-108">Предоставляет поддержку автоматической настройки для служб Azure, включая служебную шину, службу хранилища, Active Directory и т. д.</span><span class="sxs-lookup"><span data-stu-id="d7b7f-108">Provides auto-configuration support for Azure Services; e.g. Service Bus, Storage, Active Directory, etc.</span></span>

* <span data-ttu-id="d7b7f-109">**[Azure Active Directory](#azure-active-directory)**</span><span class="sxs-lookup"><span data-stu-id="d7b7f-109">**[Azure Active Directory](#azure-active-directory)**</span></span>

   <span data-ttu-id="d7b7f-110">Предоставляет поддержку интеграции для Spring Security с Azure Active Directory для аутентификации.</span><span class="sxs-lookup"><span data-stu-id="d7b7f-110">Provides integration support for Spring Security with Azure Active Directory for authentication.</span></span>

* <span data-ttu-id="d7b7f-111">**[Azure Key Vault](#azure-key-vault)**</span><span class="sxs-lookup"><span data-stu-id="d7b7f-111">**[Azure Key Vault](#azure-key-vault)**</span></span>

   <span data-ttu-id="d7b7f-112">Начальное приложение Spring Boot поддерживает интеграцию с секретами Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="d7b7f-112">Provides Spring value annotation support for integration with Azure Key Vault Secrets.</span></span>

* <span data-ttu-id="d7b7f-113">**[Служба хранилища Azure](#azure-storage)**</span><span class="sxs-lookup"><span data-stu-id="d7b7f-113">**[Azure Storage](#azure-storage)**</span></span>

   <span data-ttu-id="d7b7f-114">Spring Boot поддерживает службы хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="d7b7f-114">Provides Spring Boot support for Azure Storage services.</span></span>

<a name="azure-support"></a>
## <a name="azure-support"></a><span data-ttu-id="d7b7f-115">Поддержка Azure</span><span class="sxs-lookup"><span data-stu-id="d7b7f-115">Azure Support</span></span>

<span data-ttu-id="d7b7f-116">Начальное приложение Spring Boot поддерживает автоматическую настройку служб Azure, таких как Служебная шина Azure, служба хранилища Azure, Active Directory, Cosmos DB, Key Vault и др.</span><span class="sxs-lookup"><span data-stu-id="d7b7f-116">This Spring Boot Starter provides auto-configuration support for Azure Services; for example: Service Bus, Storage, Active Directory, Cosmos DB, Key Vault, etc.</span></span>

<span data-ttu-id="d7b7f-117">Примеры использования разных функций Azure с этим начальным приложением, см. по следующей ссылке:</span><span class="sxs-lookup"><span data-stu-id="d7b7f-117">For examples of how to use the various Azure features that are provided by this starter, see the following:</span></span>

* <https://github.com/Microsoft/azure-spring-boot/tree/master/azure-spring-boot-samples>

<span data-ttu-id="d7b7f-118">Когда вы добавляете это начальное приложение в проект Spring Boot, в файл *pom.xml* вносятся следующие изменения:</span><span class="sxs-lookup"><span data-stu-id="d7b7f-118">When you add this starter to a Spring Boot project, the following changes are made to the *pom.xml* file:</span></span>

* <span data-ttu-id="d7b7f-119">В элемент `<properties>` добавляется следующее свойство:</span><span class="sxs-lookup"><span data-stu-id="d7b7f-119">The following property is added to `<properties>` element:</span></span>

   ```xml
   <properties>
      <!-- Other properties will be listed here -->
      <azure.version>0.2.0</azure.version>
   </properties>
   ```

* <span data-ttu-id="d7b7f-120">Стандартная зависимость `spring-boot-starter` заменяется следующим образом:</span><span class="sxs-lookup"><span data-stu-id="d7b7f-120">The default `spring-boot-starter` dependency is replaced with the following:</span></span>

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-spring-boot</artifactId>
   </dependency>
   ```

* <span data-ttu-id="d7b7f-121">В файл добавляется следующий раздел:</span><span class="sxs-lookup"><span data-stu-id="d7b7f-121">The following section is added to the file:</span></span>

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
## <a name="azure-active-directory"></a><span data-ttu-id="d7b7f-122">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d7b7f-122">Azure Active Directory</span></span>

<span data-ttu-id="d7b7f-123">Это начальное приложение Spring Boot поддерживает автоматическую настройку Spring Security, обеспечивая интеграцию с Azure Active Directory для аутентификации.</span><span class="sxs-lookup"><span data-stu-id="d7b7f-123">This Spring Boot Starter provides auto-configuration support for Spring Security in order to provide integration with Azure Active Directory for authentication.</span></span>

<span data-ttu-id="d7b7f-124">Примеры использования функций Azure Active Directory с этим начальным приложением, см. по следующей ссылке:</span><span class="sxs-lookup"><span data-stu-id="d7b7f-124">For examples of how to use the Azure Active Directory features that are provided by this starter, see the following:</span></span>

* <https://github.com/Microsoft/azure-spring-boot/tree/master/azure-spring-boot-samples/azure-active-directory-spring-boot-sample>

<span data-ttu-id="d7b7f-125">Когда вы добавляете это начальное приложение в проект Spring Boot, в файл *pom.xml* вносятся следующие изменения:</span><span class="sxs-lookup"><span data-stu-id="d7b7f-125">When you add this starter to a Spring Boot project, the following changes are made to the *pom.xml* file:</span></span>

* <span data-ttu-id="d7b7f-126">В элемент `<properties>` добавляется следующее свойство:</span><span class="sxs-lookup"><span data-stu-id="d7b7f-126">The following property is added to `<properties>` element:</span></span>

   ```xml
   <properties>
      <!-- Other properties will be listed here -->
      <azure.version>0.2.0</azure.version>
   </properties>
   ```

* <span data-ttu-id="d7b7f-127">Стандартная зависимость `spring-boot-starter` заменяется следующим образом:</span><span class="sxs-lookup"><span data-stu-id="d7b7f-127">The default `spring-boot-starter` dependency is replaced with the following:</span></span>

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-active-directory-spring-boot-starter</artifactId>
   </dependency>
   ```

* <span data-ttu-id="d7b7f-128">В файл добавляется следующий раздел:</span><span class="sxs-lookup"><span data-stu-id="d7b7f-128">The following section is added to the file:</span></span>

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
## <a name="azure-key-vault"></a><span data-ttu-id="d7b7f-129">Хранилище ключей Azure</span><span class="sxs-lookup"><span data-stu-id="d7b7f-129">Azure Key Vault</span></span>

<span data-ttu-id="d7b7f-130">Приложение Spring Boot Starter обеспечивает поддержку заметок со значениями Spring для интеграции с секретами Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="d7b7f-130">This Spring Boot Starter provides Spring value annotation support for integration with Azure Key Vault Secrets.</span></span>

<span data-ttu-id="d7b7f-131">Примеры использования функций Azure Key Vault, предоставляемых этим начальным приложением, см. по следующей ссылке:</span><span class="sxs-lookup"><span data-stu-id="d7b7f-131">For examples of how to use the Azure Key Vault features that are provided by this starter, see the following:</span></span>

* <https://github.com/Microsoft/azure-spring-boot/tree/master/azure-spring-boot-samples/azure-keyvault-secrets-spring-boot-sample>

<span data-ttu-id="d7b7f-132">Когда вы добавляете это начальное приложение в проект Spring Boot, в файл *pom.xml* вносятся следующие изменения:</span><span class="sxs-lookup"><span data-stu-id="d7b7f-132">When you add this starter to a Spring Boot project, the following changes are made to the *pom.xml* file:</span></span>

* <span data-ttu-id="d7b7f-133">В элемент `<properties>` добавляется следующее свойство:</span><span class="sxs-lookup"><span data-stu-id="d7b7f-133">The following property is added to `<properties>` element:</span></span>

   ```xml
   <properties>
      <!-- Other properties will be listed here -->
      <azure.version>0.2.0</azure.version>
   </properties>
   ```

* <span data-ttu-id="d7b7f-134">Стандартная зависимость `spring-boot-starter` заменяется следующим образом:</span><span class="sxs-lookup"><span data-stu-id="d7b7f-134">The default `spring-boot-starter` dependency is replaced with the following:</span></span>

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-keyvault-secrets-spring-boot-starter</artifactId>
   </dependency>
   ```

* <span data-ttu-id="d7b7f-135">В файл добавляется следующий раздел:</span><span class="sxs-lookup"><span data-stu-id="d7b7f-135">The following section is added to the file:</span></span>

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
## <a name="azure-storage"></a><span data-ttu-id="d7b7f-136">Хранилище Azure</span><span class="sxs-lookup"><span data-stu-id="d7b7f-136">Azure Storage</span></span>

<span data-ttu-id="d7b7f-137">Начальное приложение Spring Boot Starter обеспечивает поддержку интеграции Spring Boot для служб хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="d7b7f-137">This Spring Boot Starter provides Spring Boot integration support for Azure Storage services.</span></span>

<span data-ttu-id="d7b7f-138">Примеры использования функций службы хранилища Azure, предоставляемых этим начальным приложением, см. по следующей ссылке:</span><span class="sxs-lookup"><span data-stu-id="d7b7f-138">For examples of how to use the Azure Storage features that are provided by this starter, see the following:</span></span>

* [<span data-ttu-id="d7b7f-139">Как использовать Spring Boot Starter со службой хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="d7b7f-139">How to use the Spring Boot Starter for Azure Storage</span></span>](configure-spring-boot-starter-java-app-with-azure-storage.md)

* <https://github.com/Microsoft/azure-spring-boot/tree/master/azure-spring-boot-samples/azure-storage-spring-boot-sample>

<span data-ttu-id="d7b7f-140">Когда вы добавляете это начальное приложение в проект Spring Boot, в файл *pom.xml* вносятся следующие изменения:</span><span class="sxs-lookup"><span data-stu-id="d7b7f-140">When you add this starter to a Spring Boot project, the following changes are made to the *pom.xml* file:</span></span>

* <span data-ttu-id="d7b7f-141">В элемент `<properties>` добавляется следующее свойство:</span><span class="sxs-lookup"><span data-stu-id="d7b7f-141">The following property is added to `<properties>` element:</span></span>

   ```xml
   <properties>
      <!-- Other properties will be listed here -->
      <azure.version>0.2.0</azure.version>
   </properties>
   ```

* <span data-ttu-id="d7b7f-142">Стандартная зависимость `spring-boot-starter` заменяется следующим образом:</span><span class="sxs-lookup"><span data-stu-id="d7b7f-142">The default `spring-boot-starter` dependency is replaced with the following:</span></span>

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-storage-spring-boot-starter</artifactId>
   </dependency>
   ```

* <span data-ttu-id="d7b7f-143">В файл добавляется следующий раздел:</span><span class="sxs-lookup"><span data-stu-id="d7b7f-143">The following section is added to the file:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="d7b7f-144">Дополнительная информация</span><span class="sxs-lookup"><span data-stu-id="d7b7f-144">Next steps</span></span>

<span data-ttu-id="d7b7f-145">Дополнительные сведения о Spring и Azure см. в центре документации об использовании Spring в Azure.</span><span class="sxs-lookup"><span data-stu-id="d7b7f-145">To learn more about Spring and Azure, continue to the Spring on Azure documentation center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d7b7f-146">Spring в Azure</span><span class="sxs-lookup"><span data-stu-id="d7b7f-146">Spring on Azure</span></span>](/java/azure/spring-framework)

### <a name="additional-resources"></a><span data-ttu-id="d7b7f-147">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="d7b7f-147">Additional Resources</span></span>

<span data-ttu-id="d7b7f-148">Дополнительные сведения об использовании [Spring Boot] в Azure см. [Spring в Azure].</span><span class="sxs-lookup"><span data-stu-id="d7b7f-148">For more information about using [Spring Boot] applications on Azure, see [Spring on Azure].</span></span>

<span data-ttu-id="d7b7f-149">Дополнительные сведения об использовании Java в Azure см. в статьях [Azure для разработчиков Java] и [Working with Azure DevOps and Java] (Работа с Azure DevOps и Java).</span><span class="sxs-lookup"><span data-stu-id="d7b7f-149">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Working with Azure DevOps and Java].</span></span>

<span data-ttu-id="d7b7f-150">Справку по началу работы с собственными приложениями Spring Boot см. на странице **Spring Initializr**: https://start.spring.io/.</span><span class="sxs-lookup"><span data-stu-id="d7b7f-150">For help with getting started with your own Spring Boot applications, see the **Spring Initializr** at https://start.spring.io/.</span></span>

<!-- URL List -->

[Azure для разработчиков Java]: /java/azure/
[Azure for Java Developers]: /java/azure/
[Working with Azure DevOps and Java]: /azure/devops/ (Работа с Azure DevOps и Java)
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring в Azure]: /java/azure/spring-framework/
[Spring on Azure]: /java/azure/spring-framework/
[Spring Framework]: https://spring.io/
[Spring Initializr]: https://start.spring.io/

<!-- IMG List -->

[spring-boot-starters]: media/spring-boot-starters-for-azure/spring-boot-starters-cropped.png
