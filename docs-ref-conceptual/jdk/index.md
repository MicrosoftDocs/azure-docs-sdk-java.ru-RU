---
title: Пакеты JDK и долгосрочная поддержка разработки в Azure
description: Файлы для скачивания и заявление о поддержке разработки и выполнения приложений на Java в Azure.
author: bmitchell287
manager: douge
ms.devlang: java
ms.topic: conceptual
ms.date: 04/09/2019
ms.author: brendm
ms.openlocfilehash: 340f6149ffe39ccbb2d7de534ed63b8784d1f63a
ms.sourcegitcommit: 394521c47ac9895d00d9f97535cc9d1e27d08fe9
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/28/2019
ms.locfileid: "66270885"
---
# <a name="java-long-term-support-for-azure-and-azure-stack"></a><span data-ttu-id="cb8b6-103">Долгосрочная поддержка Java для Azure и Azure Stack</span><span class="sxs-lookup"><span data-stu-id="cb8b6-103">Java Long-Term Support for Azure and Azure Stack</span></span>

<span data-ttu-id="cb8b6-104">В Azure и Azure Stack разработчики Java могут собирать и запускать производственные приложения на Java с помощью коллекции сборок [Azul Zulu Enterprise for Azure](https://www.azul.com/downloads/azure-only/zulu/), не неся при этом дополнительных затрат на поддержку.</span><span class="sxs-lookup"><span data-stu-id="cb8b6-104">Java developers on Azure and Azure Stack can build and run production Java applications using [Azul Zulu Enterprise for Azure](https://www.azul.com/downloads/azure-only/zulu/) without incurring additional support costs.</span></span> <span data-ttu-id="cb8b6-105">В Azure можно задействовать любые среды выполнения Java, но при использовании Zulu вы получаете бесплатное обслуживание и можете направлять запросы в службу поддержки Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="cb8b6-105">You can use any Java runtime you want on Azure, but when you use Zulu you get free maintenance updates and can create support issues with Microsoft.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="cb8b6-106">Скачать и установить Java</span><span class="sxs-lookup"><span data-stu-id="cb8b6-106">Download and install Java</span></span>](java-jdk-install.md)

## <a name="long-term-support-lts"></a><span data-ttu-id="cb8b6-107">Долгосрочная поддержка (LTS):</span><span class="sxs-lookup"><span data-stu-id="cb8b6-107">Long-term support (LTS)</span></span>

* [<span data-ttu-id="cb8b6-108">Java 11</span><span class="sxs-lookup"><span data-stu-id="cb8b6-108">Java 11</span></span>](https://www.azul.com/downloads/azure-only/zulu/#java11)
* <span data-ttu-id="cb8b6-109">[Java 8](https://www.azul.com/downloads/azure-only/zulu/#java8);</span><span class="sxs-lookup"><span data-stu-id="cb8b6-109">[Java 8](https://www.azul.com/downloads/azure-only/zulu/#java8)</span></span>
* [<span data-ttu-id="cb8b6-110">Java 7</span><span class="sxs-lookup"><span data-stu-id="cb8b6-110">Java 7</span></span>](https://www.azul.com/downloads/azure-only/zulu/#java7)

## <a name="technical-preview"></a><span data-ttu-id="cb8b6-111">Техническая предварительная версия</span><span class="sxs-lookup"><span data-stu-id="cb8b6-111">Technical preview</span></span>

* [<span data-ttu-id="cb8b6-112">Java 12</span><span class="sxs-lookup"><span data-stu-id="cb8b6-112">Java 12</span></span>](https://www.azul.com/downloads/azure-only/zulu/#java12)

## <a name="what-is-the-zulu-openjdk-for-azure"></a><span data-ttu-id="cb8b6-113">Что такое Zulu OpenJDK для Azure?</span><span class="sxs-lookup"><span data-stu-id="cb8b6-113">What is the Zulu OpenJDK for Azure?</span></span>

<span data-ttu-id="cb8b6-114">Сборка OpenJDK типа Azul Zulu Enterprise — это бесплатный мультиплатформенный, готовый дистрибутив OpenJDK для Azure и Azure Stack, который поддерживается корпорацией Майкрософт и Azul Systems.</span><span class="sxs-lookup"><span data-stu-id="cb8b6-114">Azul Zulu Enterprise builds of OpenJDK are a no-cost, multi-platform, production-ready distribution of the OpenJDK for Azure and Azure Stack backed by Microsoft and Azul Systems.</span></span> <span data-ttu-id="cb8b6-115">Эти дистрибутивы:</span><span class="sxs-lookup"><span data-stu-id="cb8b6-115">These distributions are:</span></span>

* <span data-ttu-id="cb8b6-116">Являются сборками OpenJDK с полностью открытым кодом, которые упакованы в виде комплектов Java Development Kit (JDK), сред выполнения Java (JRE) и автономных сред JRE.</span><span class="sxs-lookup"><span data-stu-id="cb8b6-116">100% open source builds of OpenJDK packaged as Java Development Kits (JDKs), Java Runtime Environments (JREs), and Headless JREs.</span></span> <span data-ttu-id="cb8b6-117">Эти двоичные файлы являются полностью совместимыми коммерческими сборками Java Standard Edition (SE), которые можно использовать с приложениями или компонентами Java в Azure и Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="cb8b6-117">These binaries are fully compatible and compliant commercial builds of Java Standard Edition (SE) that can be used with Java applications or components on Azure and Azure Stack.</span></span>
* <span data-ttu-id="cb8b6-118">Предоставляются с долгосрочной поддержкой, включающей исправления ошибок, улучшения производительности и исправления системы безопасности.</span><span class="sxs-lookup"><span data-stu-id="cb8b6-118">Provided with long-term support including bug fixes, performance enhancements, and security patches.</span></span>
* <span data-ttu-id="cb8b6-119">Доступны для разработки и запуска приложений Java на Windows, Linux и MacOS.</span><span class="sxs-lookup"><span data-stu-id="cb8b6-119">Available for developing and running Java applications on Windows, Linux, and MacOS.</span></span>
* <span data-ttu-id="cb8b6-120">Доступны как образы контейнеров в Docker Hub, а также как виртуальные машины (Windows и Linux) в Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="cb8b6-120">Available as container images on Docker Hub and as virtual machines (Windows and Linux) on Azure Marketplace.</span></span>
* <span data-ttu-id="cb8b6-121">Используются Microsoft Azure для работы со многими службами Azure, такими как:</span><span class="sxs-lookup"><span data-stu-id="cb8b6-121">Used by Microsoft Azure to power many Azure services, such as:</span></span>
  * <span data-ttu-id="cb8b6-122">Служба приложений (Windows);</span><span class="sxs-lookup"><span data-stu-id="cb8b6-122">App Service Windows</span></span>
  * <span data-ttu-id="cb8b6-123">Служба приложений для Linux;</span><span class="sxs-lookup"><span data-stu-id="cb8b6-123">App Service Linux</span></span>
  * <span data-ttu-id="cb8b6-124">Функции Azure</span><span class="sxs-lookup"><span data-stu-id="cb8b6-124">Functions</span></span>
  * <span data-ttu-id="cb8b6-125">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="cb8b6-125">Service Fabric</span></span>
  * <span data-ttu-id="cb8b6-126">HDInsight</span><span class="sxs-lookup"><span data-stu-id="cb8b6-126">HDInsight</span></span>
  * <span data-ttu-id="cb8b6-127">Поиск</span><span class="sxs-lookup"><span data-stu-id="cb8b6-127">Search</span></span>
  * <span data-ttu-id="cb8b6-128">Azure DevOps</span><span class="sxs-lookup"><span data-stu-id="cb8b6-128">Azure DevOps</span></span>
  * <span data-ttu-id="cb8b6-129">Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="cb8b6-129">Cloud Shell</span></span>  

## <a name="supported-java-versions-and-update-schedule"></a><span data-ttu-id="cb8b6-130">Поддерживаемые версии Java и график поддержки</span><span class="sxs-lookup"><span data-stu-id="cb8b6-130">Supported Java versions and update schedule</span></span>

<span data-ttu-id="cb8b6-131">Azul Systems предоставляет коллекцию полностью поддерживаемых [сборок OpenJDK под названием Zulu Enterprise для Microsoft Azure](https://www.azul.com/downloads/azure-only/zulu/) для всех версий Java с долгосрочной поддержкой, начиная с Java SE 7, 8 и 11.</span><span class="sxs-lookup"><span data-stu-id="cb8b6-131">Azul Systems provides fully-supported [Zulu Enterprise builds of OpenJDK for Microsoft Azure](https://www.azul.com/downloads/azure-only/zulu/) for all long-term support (LTS) versions of Java, starting with Java SE 7, 8, and 11.</span></span> <span data-ttu-id="cb8b6-132">Дополнительные сведения см. в [пресс-релизе Azul](https://www.azul.com/press_release/free-java-production-support-for-microsoft-azure-azure-stack).</span><span class="sxs-lookup"><span data-stu-id="cb8b6-132">More information can be found in the [Azul press release](https://www.azul.com/press_release/free-java-production-support-for-microsoft-azure-azure-stack).</span></span>

|<span data-ttu-id="cb8b6-133">Долгосрочная поддержка Java SE</span><span class="sxs-lookup"><span data-stu-id="cb8b6-133">Java SE LTS</span></span>  |<span data-ttu-id="cb8b6-134">Поддержка до</span><span class="sxs-lookup"><span data-stu-id="cb8b6-134">Support until</span></span>  |
|---------|----------|
|<span data-ttu-id="cb8b6-135">[![Java 7](../media/jdk/java-7.png)](https://www.azul.com/downloads/azure-only/zulu/#java7)</span><span class="sxs-lookup"><span data-stu-id="cb8b6-135">[![Java 7](../media/jdk/java-7.png)](https://www.azul.com/downloads/azure-only/zulu/#java7)</span></span> |<span data-ttu-id="cb8b6-136">Июль 2023 г.</span><span class="sxs-lookup"><span data-stu-id="cb8b6-136">July 2023</span></span> |
|<span data-ttu-id="cb8b6-137">[![Java 8](../media/jdk/java-8.png)](https://www.azul.com/downloads/azure-only/zulu/#java8)</span><span class="sxs-lookup"><span data-stu-id="cb8b6-137">[![Java 8](../media/jdk/java-8.png)](https://www.azul.com/downloads/azure-only/zulu/#java8)</span></span> |<span data-ttu-id="cb8b6-138">Март 2025 г.</span><span class="sxs-lookup"><span data-stu-id="cb8b6-138">March 2025</span></span>|
|<span data-ttu-id="cb8b6-139">[![Java 11](../media/jdk/java-11.png)](https://www.azul.com/downloads/azure-only/zulu/#java11)</span><span class="sxs-lookup"><span data-stu-id="cb8b6-139">[![Java 11](../media/jdk/java-11.png)](https://www.azul.com/downloads/azure-only/zulu/#java11)</span></span> |<span data-ttu-id="cb8b6-140">Сентябрь 2026 г.</span><span class="sxs-lookup"><span data-stu-id="cb8b6-140">Sept. 2026</span></span>|
|<span data-ttu-id="cb8b6-141">[![Java 12](../media/jdk/java-12.png)]()</span><span class="sxs-lookup"><span data-stu-id="cb8b6-141">[![Java 12](../media/jdk/java-12.png)]()</span></span> |<span data-ttu-id="cb8b6-142">**Предварительная версия**</span><span class="sxs-lookup"><span data-stu-id="cb8b6-142">**PREVIEW**</span></span>|

<span data-ttu-id="cb8b6-143">Для этих выпусков JDK выходят ежеквартальные обновления для системы безопасности и исправления ошибок, а также критические внеплановые обновления и исправления при необходимости.</span><span class="sxs-lookup"><span data-stu-id="cb8b6-143">These JDK releases have quarterly security updates, bug fixes, and critical out-of-band updates and patches as needed.</span></span>  <span data-ttu-id="cb8b6-144">Поддержка включает в себя обратное портирование обновлений для системы безопасности и исправлений ошибок для Java 7 и 8, обнаруженных в более новых версиях Java, например Java 11, что гарантирует стабильную работу и безопасность приложений на старых версиях Java.</span><span class="sxs-lookup"><span data-stu-id="cb8b6-144">This support includes back ports of security updates and bug fixes to Java 7 and 8 reported in newer versions of Java such as Java 11, which ensures the continued stability and security of older versions of Java.</span></span>  <span data-ttu-id="cb8b6-145">Пользователи Azure могут получить эти обновления для системы безопасности и исправления ошибок платформы, не неся при этом незапланированных расходов на подписку на Java SE.</span><span class="sxs-lookup"><span data-stu-id="cb8b6-145">Azure customers can get these security updates and platform bug fixes without incurring any unplanned Java SE subscription fees.</span></span>

<span data-ttu-id="cb8b6-146">Выпуски от Azul Systems учитывают [график выхода новых версий Java SE](https://www.azul.com/products/azul_support_roadmap/).</span><span class="sxs-lookup"><span data-stu-id="cb8b6-146">Azul Systems maintains a [Java SE roadmap](https://www.azul.com/products/azul_support_roadmap/) for these releases.</span></span>

## <a name="benefits-for-developers"></a><span data-ttu-id="cb8b6-147">Преимущества для разработчиков</span><span class="sxs-lookup"><span data-stu-id="cb8b6-147">Benefits for developers</span></span>

<span data-ttu-id="cb8b6-148">Выпуски Azul Zulu JDK:</span><span class="sxs-lookup"><span data-stu-id="cb8b6-148">The Azul Zulu JDK releases are:</span></span>

1. <span data-ttu-id="cb8b6-149">Поддерживаются корпорацией Майкрософт и Azul Systems.</span><span class="sxs-lookup"><span data-stu-id="cb8b6-149">Backed and supported by both Microsoft and Azul Systems</span></span>

   * <span data-ttu-id="cb8b6-150">Двоичные файлы Zulu готовы к выпуску и поддерживаются корпорацией Майкрософт и Azul Systems.</span><span class="sxs-lookup"><span data-stu-id="cb8b6-150">Zulu binaries are production-ready and backed by Microsoft and Azul Systems</span></span>
   * <span data-ttu-id="cb8b6-151">Zulu поставляется с бесплатной долгосрочной поддержкой (LTS) для Java 7, 8, и 11.</span><span class="sxs-lookup"><span data-stu-id="cb8b6-151">Zulu comes with zero-cost long-term support (LTS) for Java 7, 8, and 11.</span></span> <span data-ttu-id="cb8b6-152">(LTS будет также предоставляться для Java 17.)</span><span class="sxs-lookup"><span data-stu-id="cb8b6-152">(LTS will be provided for Java 17, as well).</span></span> <span data-ttu-id="cb8b6-153">Вы можете обновлять версии Java, только если это необходимо.</span><span class="sxs-lookup"><span data-stu-id="cb8b6-153">You can upgrade Java versions only when you need to.</span></span>
   * <span data-ttu-id="cb8b6-154">Java 7 поддерживается до июля 2023 г.</span><span class="sxs-lookup"><span data-stu-id="cb8b6-154">Java 7 supported until July 2023.</span></span> <span data-ttu-id="cb8b6-155">Java 8 и 11 поддерживаются до 2024 года и дольше.</span><span class="sxs-lookup"><span data-stu-id="cb8b6-155">Java 8 and 11 are supported beyond 2024.</span></span>
   * <span data-ttu-id="cb8b6-156">Корпорация Майкрософт стремится запустить Zulu внутри на компьютерах, которые поддерживают многие службы Azure.</span><span class="sxs-lookup"><span data-stu-id="cb8b6-156">Microsoft is committed to running Zulu internally on machines that power many Azure services.</span></span>

2. <span data-ttu-id="cb8b6-157">Готовы к выпуску.</span><span class="sxs-lookup"><span data-stu-id="cb8b6-157">Production-ready</span></span>

   * <span data-ttu-id="cb8b6-158">С полностью открытым кодом для сборок OpenJDK.</span><span class="sxs-lookup"><span data-stu-id="cb8b6-158">100% open-source for its builds of OpenJDK.</span></span>
   * <span data-ttu-id="cb8b6-159">Упрощенные замены для многих дистрибутивов Java SE.</span><span class="sxs-lookup"><span data-stu-id="cb8b6-159">Drop-in replacements for many Java SE distributions.</span></span>
   * <span data-ttu-id="cb8b6-160">JDK, JRE и автономная JRE.</span><span class="sxs-lookup"><span data-stu-id="cb8b6-160">JDK, JRE, and JRE-headless</span></span>
   * <span data-ttu-id="cb8b6-161">Java 7, 8 и 11.</span><span class="sxs-lookup"><span data-stu-id="cb8b6-161">Java 7, 8, and 11</span></span>
   * <span data-ttu-id="cb8b6-162">Проверены на соответствие спецификациям Java SE с использованием комплекта технологической совместимости (TCK) сообщества OpenJDK.</span><span class="sxs-lookup"><span data-stu-id="cb8b6-162">Verified compliant with the Java SE  specifications using the OpenJDK Community Technology Compatibility Kit (TCK).</span></span>
   * <span data-ttu-id="cb8b6-163">Разработчики продолжат получать производственные обновления для Java SE, включая исправления ошибок, улучшения производительности и исправления системы безопасности для Java SE 7, 8 и 11.</span><span class="sxs-lookup"><span data-stu-id="cb8b6-163">Developers will continue to receive production updates for Java SE, including bug fixes, performance enhancements, and security patches for Java SE 7, 8, and 11.</span></span>

3. <span data-ttu-id="cb8b6-164">Поддерживаются для нескольких платформ.</span><span class="sxs-lookup"><span data-stu-id="cb8b6-164">Supported for multi-platform.</span></span> <span data-ttu-id="cb8b6-165">Zulu поддерживает двоичные файлы для нескольких платформ и версий, в том числе:</span><span class="sxs-lookup"><span data-stu-id="cb8b6-165">Zulu supports binaries for multiple platforms and versions, including:</span></span>

   * <span data-ttu-id="cb8b6-166">Клиент Windows</span><span class="sxs-lookup"><span data-stu-id="cb8b6-166">Windows Client</span></span>
     * <span data-ttu-id="cb8b6-167">10</span><span class="sxs-lookup"><span data-stu-id="cb8b6-167">10</span></span>
     * <span data-ttu-id="cb8b6-168">8.1</span><span class="sxs-lookup"><span data-stu-id="cb8b6-168">8.1</span></span>
     * <span data-ttu-id="cb8b6-169">8, 7</span><span class="sxs-lookup"><span data-stu-id="cb8b6-169">8, 7</span></span>
   * <span data-ttu-id="cb8b6-170">Windows Server</span><span class="sxs-lookup"><span data-stu-id="cb8b6-170">Windows Server</span></span>
     * <span data-ttu-id="cb8b6-171">2016R2</span><span class="sxs-lookup"><span data-stu-id="cb8b6-171">2016R2</span></span>
     * <span data-ttu-id="cb8b6-172">2016</span><span class="sxs-lookup"><span data-stu-id="cb8b6-172">2016</span></span>
     * <span data-ttu-id="cb8b6-173">2012 R2</span><span class="sxs-lookup"><span data-stu-id="cb8b6-173">2012 R2</span></span>
     * <span data-ttu-id="cb8b6-174">2012</span><span class="sxs-lookup"><span data-stu-id="cb8b6-174">2012</span></span>
     * <span data-ttu-id="cb8b6-175">2008 R2</span><span class="sxs-lookup"><span data-stu-id="cb8b6-175">2008 R2</span></span>
   * <span data-ttu-id="cb8b6-176">Linux, включая</span><span class="sxs-lookup"><span data-stu-id="cb8b6-176">Linux, including</span></span>
     * <span data-ttu-id="cb8b6-177">RHEL</span><span class="sxs-lookup"><span data-stu-id="cb8b6-177">RHEL</span></span>
     * <span data-ttu-id="cb8b6-178">CentOS</span><span class="sxs-lookup"><span data-stu-id="cb8b6-178">CentOS</span></span>
     * <span data-ttu-id="cb8b6-179">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="cb8b6-179">Ubuntu</span></span>
     * <span data-ttu-id="cb8b6-180">SLES</span><span class="sxs-lookup"><span data-stu-id="cb8b6-180">SLES</span></span>
     * <span data-ttu-id="cb8b6-181">Debian</span><span class="sxs-lookup"><span data-stu-id="cb8b6-181">Debian</span></span>
     * <span data-ttu-id="cb8b6-182">Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="cb8b6-182">Oracle Linux</span></span>
   * <span data-ttu-id="cb8b6-183">Mac OS X</span><span class="sxs-lookup"><span data-stu-id="cb8b6-183">Mac OS X</span></span>
   * <span data-ttu-id="cb8b6-184">Предоставляются в нескольких типах упаковки:</span><span class="sxs-lookup"><span data-stu-id="cb8b6-184">delivered in multiple package types:</span></span>
     * <span data-ttu-id="cb8b6-185">MSI, ZIP, TAR, DEB, RPM и DMG.</span><span class="sxs-lookup"><span data-stu-id="cb8b6-185">MSI, ZIP, TAR, DEB, RPM, and DMG</span></span>

    <span data-ttu-id="cb8b6-186">В Docker доступны сертифицированные образы контейнеров Docker для Zulu JDK, JRE и автономной среды JRE для нескольких базовых образов ОС.</span><span class="sxs-lookup"><span data-stu-id="cb8b6-186">Certified Docker container images for Zulu JDK, JRE, and JRE-headless on multiple base OS images are available at Docker.</span></span>

    <span data-ttu-id="cb8b6-187">Концентратор:</span><span class="sxs-lookup"><span data-stu-id="cb8b6-187">Hub:</span></span>

    * <span data-ttu-id="cb8b6-188">[JDK](https://hub.docker.com/_/microsoft-java-jdk).</span><span class="sxs-lookup"><span data-stu-id="cb8b6-188">[JDK](https://hub.docker.com/_/microsoft-java-jdk)</span></span>
    * <span data-ttu-id="cb8b6-189">[JRE](https://hub.docker.com/_/microsoft-java-jre).</span><span class="sxs-lookup"><span data-stu-id="cb8b6-189">[JRE](https://hub.docker.com/_/microsoft-java-jre)</span></span>
    * <span data-ttu-id="cb8b6-190">[Автономная среда JRE](https://hub.docker.com/_/microsoft-java-jre-headless).</span><span class="sxs-lookup"><span data-stu-id="cb8b6-190">[JRE-headless](https://hub.docker.com/_/microsoft-java-jre-headless)</span></span>

4. <span data-ttu-id="cb8b6-191">Бесплатны.</span><span class="sxs-lookup"><span data-stu-id="cb8b6-191">No cost</span></span>

   * <span data-ttu-id="cb8b6-192">Корпорация Майкрософт предоставляет все необходимое для создания и масштабирования приложений Java в Azure бесплатно.</span><span class="sxs-lookup"><span data-stu-id="cb8b6-192">Microsoft provides everything you need to build and scale Java apps on Azure at no cost to you.</span></span> <span data-ttu-id="cb8b6-193">Через Zulu вы будете получать бесплатные обновления системы безопасности и исправления ошибок платформы для приложений Java без какой-либо платы.</span><span class="sxs-lookup"><span data-stu-id="cb8b6-193">Through Zulu you'll receive free security updates and platform bug fixes for Java apps without any fees.</span></span>
   * <span data-ttu-id="cb8b6-194">[Java Flight Recorder и Mission Control](java-jdk-flight-recorder-and-mission-control.md) доступны в Zulu Java 8, 11 и 12 (предварительная версия).</span><span class="sxs-lookup"><span data-stu-id="cb8b6-194">[Java Flight Recorder and Mission Control](java-jdk-flight-recorder-and-mission-control.md) are available in Zulu Java 8, 11, and 12 (Preview).</span></span>

5. <span data-ttu-id="cb8b6-195">Технические предварительные версии без LTS</span><span class="sxs-lookup"><span data-stu-id="cb8b6-195">Tech Preview of Non-LTS versions</span></span>

   * <span data-ttu-id="cb8b6-196">Технические предварительные версии позволяют постепенно протестировать новые функции, так как они предоставляются в краткосрочных версиях, которые в конечном итоге перейдут на долгосрочную поддержку Java 17.</span><span class="sxs-lookup"><span data-stu-id="cb8b6-196">Tech previews provide you with opportunities to progressively test new features as they are delivered in short-term versions that will eventually graduate to Java 17 LTS.</span></span>

6. <span data-ttu-id="cb8b6-197">Изменения в OpenJDK вносятся в вышестоящий источник.</span><span class="sxs-lookup"><span data-stu-id="cb8b6-197">Changes to OpenJDK are up-streamed</span></span>

   * <span data-ttu-id="cb8b6-198">Разработчики Azul Systems отправляют изменения Zulu в OpenJDK, что делает вышестоящий репозиторий целостным и инклюзивным.</span><span class="sxs-lookup"><span data-stu-id="cb8b6-198">Azul Systems committers push Zulu changes to OpenJDK which makes the upstream repo comprehensive and inclusive.</span></span>

<span data-ttu-id="cb8b6-199">Как всегда, разработчики Java могут перенести в Azure свои собственные среды выполнения Java, включая Oracle JDK и Red Hat JDK, и использовать защищенную инфраструктуру и многофункциональные службы.</span><span class="sxs-lookup"><span data-stu-id="cb8b6-199">As always, Java developers can bring their own Java run-times, including Oracle JDK and Red Hat JDK, to Azure and use  the secure infrastructure and feature-rich services.</span></span> <span data-ttu-id="cb8b6-200">Выпуск Oracle Java SE для рабочей среды также доступен для разработчиков Java, выполняющих рабочие нагрузки Java на виртуальных машинах Azure (Windows или Linux).</span><span class="sxs-lookup"><span data-stu-id="cb8b6-200">The production edition of Oracle Java SE is also available to Java developers for running Java workloads in Windows or Linux virtual machines on Azure.</span></span>

## <a name="use-for-local-development"></a><span data-ttu-id="cb8b6-201">Использование в локальной разработке</span><span class="sxs-lookup"><span data-stu-id="cb8b6-201">Use for local development</span></span> 

<span data-ttu-id="cb8b6-202">Пакеты Java JDK для Azure и Azure Stack доступны для [скачивания](https://www.azul.com/downloads/azure-only/zulu/) разработчикам для использования в локальных средах разработки.</span><span class="sxs-lookup"><span data-stu-id="cb8b6-202">Developers can [download](https://www.azul.com/downloads/azure-only/zulu/) Java JDKs for Azure and Azure Stack for use in local development environments.</span></span> <span data-ttu-id="cb8b6-203">Файлы для скачивания доступны для Windows, Linux и macOS.</span><span class="sxs-lookup"><span data-stu-id="cb8b6-203">Downloads are available for Windows, Linux, and macOS.</span></span> <span data-ttu-id="cb8b6-204">Разработчики, работающие на платформе Linux, могут также получить пакеты с помощью диспетчеров пакетов [yum](https://www.azul.com/downloads/azure-only/zulu/#yum-repo) и [apt](https://www.azul.com/downloads/azure-only/zulu/#apt-repo).</span><span class="sxs-lookup"><span data-stu-id="cb8b6-204">Developers working on Linux can also get packages through the [yum](https://www.azul.com/downloads/azure-only/zulu/#yum-repo) and [apt](https://www.azul.com/downloads/azure-only/zulu/#apt-repo) package managers.</span></span>

<span data-ttu-id="cb8b6-205">Дополнительные рекомендации см. в статье [Use Docker with a JDK for Azure](java-jdk-docker-images.md) (Использование Docker с JDK для Azure).</span><span class="sxs-lookup"><span data-stu-id="cb8b6-205">For additional guidance see [Docker images for Azure](java-jdk-docker-images.md).</span></span>