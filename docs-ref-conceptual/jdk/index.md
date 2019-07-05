---
title: Пакеты JDK и долгосрочная поддержка разработки в Azure
description: Эта статья содержит ссылки для загрузки и заявление о поддержке Azure для разработки и запуска приложений Java.
author: bmitchell287
manager: douge
ms.devlang: java
ms.topic: conceptual
ms.date: 04/09/2019
ms.author: brendm
ms.openlocfilehash: 1bb93f775686b5b0f127c586dda802f4eb5f775d
ms.sourcegitcommit: f8faa4a14c714e148c513fd46f119524f3897abf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/03/2019
ms.locfileid: "67533639"
---
# <a name="java-long-term-support-for-azure-and-azure-stack"></a><span data-ttu-id="deb42-103">Долгосрочная поддержка Java для Azure и Azure Stack</span><span class="sxs-lookup"><span data-stu-id="deb42-103">Java long-term support for Azure and Azure Stack</span></span>

<span data-ttu-id="deb42-104">В Microsoft Azure и Azure Stack разработчики Java могут собирать и запускать производственные приложения на Java с помощью коллекции сборок [Azul Zulu Enterprise for Azure](https://www.azul.com/downloads/azure-only/zulu/), не неся при этом дополнительных затрат на поддержку.</span><span class="sxs-lookup"><span data-stu-id="deb42-104">As a Java developer on Microsoft Azure and Azure Stack, you can build and run production Java applications by using [Azul Zulu Enterprise for Azure](https://www.azul.com/downloads/azure-only/zulu/) without incurring additional support costs.</span></span> <span data-ttu-id="deb42-105">В Azure можно задействовать любые среды выполнения Java, но при использовании Zulu вы получаете бесплатное обслуживание и обработку запросов службой поддержки Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="deb42-105">You can use any Java runtime you want on Azure, but when you use Zulu, you get free maintenance updates and you can resolve support issues with Microsoft.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="deb42-106">Скачать и установить Java</span><span class="sxs-lookup"><span data-stu-id="deb42-106">Download and install Java</span></span>](java-jdk-install.md)

## <a name="long-term-support"></a><span data-ttu-id="deb42-107">Долгосрочная поддержка</span><span class="sxs-lookup"><span data-stu-id="deb42-107">Long-term support</span></span>

* [<span data-ttu-id="deb42-108">Java 11</span><span class="sxs-lookup"><span data-stu-id="deb42-108">Java 11</span></span>](https://www.azul.com/downloads/azure-only/zulu/#java11)
* <span data-ttu-id="deb42-109">[Java 8](https://www.azul.com/downloads/azure-only/zulu/#java8);</span><span class="sxs-lookup"><span data-stu-id="deb42-109">[Java 8](https://www.azul.com/downloads/azure-only/zulu/#java8)</span></span>
* [<span data-ttu-id="deb42-110">Java 7</span><span class="sxs-lookup"><span data-stu-id="deb42-110">Java 7</span></span>](https://www.azul.com/downloads/azure-only/zulu/#java7)

## <a name="technical-preview"></a><span data-ttu-id="deb42-111">Техническая предварительная версия</span><span class="sxs-lookup"><span data-stu-id="deb42-111">Technical preview</span></span>

* [<span data-ttu-id="deb42-112">Java 12</span><span class="sxs-lookup"><span data-stu-id="deb42-112">Java 12</span></span>](https://www.azul.com/downloads/azure-only/zulu/#java12)

## <a name="what-is-the-zulu-openjdk-for-azure"></a><span data-ttu-id="deb42-113">Что такое Zulu OpenJDK для Azure?</span><span class="sxs-lookup"><span data-stu-id="deb42-113">What is the Zulu OpenJDK for Azure?</span></span>

<span data-ttu-id="deb42-114">Сборка OpenJDK типа Azul Zulu Enterprise — это бесплатный мультиплатформенный, готовый дистрибутив OpenJDK для Azure и Azure Stack, который поддерживается корпорацией Майкрософт и Azul Systems.</span><span class="sxs-lookup"><span data-stu-id="deb42-114">Azul Zulu Enterprise builds of OpenJDK are a no-cost, multi-platform, production-ready distribution of the OpenJDK for Azure and Azure Stack that's backed by Microsoft and Azul Systems.</span></span> <span data-ttu-id="deb42-115">Эти дистрибутивы:</span><span class="sxs-lookup"><span data-stu-id="deb42-115">These distributions are:</span></span>

* <span data-ttu-id="deb42-116">Являются сборками OpenJDK с полностью открытым кодом, которые упакованы в виде комплектов Java Development Kit (JDK), сред выполнения Java (JRE) и автономных сред JRE.</span><span class="sxs-lookup"><span data-stu-id="deb42-116">100 percent open-source builds of OpenJDK that are packaged as Java Development Kits (JDKs), Java Runtime Environments (JREs), and Headless JREs.</span></span> <span data-ttu-id="deb42-117">Эти двоичные файлы являются полностью совместимыми коммерческими сборками Java Standard Edition (SE), которые можно использовать с приложениями или компонентами Java в Azure и Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="deb42-117">These binaries are fully compatible and compliant commercial builds of Java Standard Edition (SE) that can be used with Java applications or components on Azure and Azure Stack.</span></span>
* <span data-ttu-id="deb42-118">Предоставляются с долгосрочной поддержкой (LTS), предусматривающей исправление ошибок, улучшение производительности и исправления системы безопасности.</span><span class="sxs-lookup"><span data-stu-id="deb42-118">Provided with long-term support (LTS), which includes bug fixes, performance enhancements, and security patches.</span></span>
* <span data-ttu-id="deb42-119">Доступны для разработки и запуска приложений Java на Windows, Linux и macOS.</span><span class="sxs-lookup"><span data-stu-id="deb42-119">Available for developing and running Java applications on Windows, Linux, and macOS.</span></span>
* <span data-ttu-id="deb42-120">Доступны как образы контейнеров в Docker Hub, а также как виртуальные машины (Windows и Linux) в Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="deb42-120">Available as container images on Docker Hub and as virtual machines (Windows and Linux) in the Azure Marketplace.</span></span>
* <span data-ttu-id="deb42-121">Используются Azure для работы со многими службами Azure, такими как:</span><span class="sxs-lookup"><span data-stu-id="deb42-121">Used by Azure to power many Azure services, such as:</span></span>
  * <span data-ttu-id="deb42-122">Служба приложений Azure (Windows)</span><span class="sxs-lookup"><span data-stu-id="deb42-122">Azure App Service (Windows)</span></span>
  * <span data-ttu-id="deb42-123">Служба приложений Azure, (Linux)</span><span class="sxs-lookup"><span data-stu-id="deb42-123">Azure App Service (Linux)</span></span>
  * <span data-ttu-id="deb42-124">Функции Azure</span><span class="sxs-lookup"><span data-stu-id="deb42-124">Azure Functions</span></span>
  * <span data-ttu-id="deb42-125">Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="deb42-125">Azure Service Fabric</span></span>
  * <span data-ttu-id="deb42-126">Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="deb42-126">Azure HDInsight</span></span>
  * <span data-ttu-id="deb42-127">Поиск Azure</span><span class="sxs-lookup"><span data-stu-id="deb42-127">Azure Search</span></span>
  * <span data-ttu-id="deb42-128">Azure DevOps</span><span class="sxs-lookup"><span data-stu-id="deb42-128">Azure DevOps</span></span>
  * <span data-ttu-id="deb42-129">Azure Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="deb42-129">Azure Cloud Shell</span></span>  

## <a name="supported-java-versions-and-update-schedule"></a><span data-ttu-id="deb42-130">Поддерживаемые версии Java и график поддержки</span><span class="sxs-lookup"><span data-stu-id="deb42-130">Supported Java versions and update schedule</span></span>

<span data-ttu-id="deb42-131">Azul Systems предоставляет коллекцию полностью поддерживаемых [сборок OpenJDK под названием Zulu Enterprise для Azure](https://www.azul.com/downloads/azure-only/zulu/) для всех версий Java с долгосрочной поддержкой, начиная с Java SE 7, 8 и 11.</span><span class="sxs-lookup"><span data-stu-id="deb42-131">Azul Systems provides fully supported [Zulu Enterprise builds of OpenJDK for Azure](https://www.azul.com/downloads/azure-only/zulu/) for all LTS versions of Java, starting with Java SE 7, 8, and 11.</span></span> <span data-ttu-id="deb42-132">Дополнительные сведения см. в [пресс-релизе Azul](https://www.azul.com/press_release/free-java-production-support-for-microsoft-azure-azure-stack).</span><span class="sxs-lookup"><span data-stu-id="deb42-132">For more information, see the [Azul press release](https://www.azul.com/press_release/free-java-production-support-for-microsoft-azure-azure-stack).</span></span>

|<span data-ttu-id="deb42-133">Долгосрочная поддержка Java SE</span><span class="sxs-lookup"><span data-stu-id="deb42-133">Java SE LTS</span></span>  |<span data-ttu-id="deb42-134">Поддержка до</span><span class="sxs-lookup"><span data-stu-id="deb42-134">Support until</span></span>  |
|---------|----------|
|<span data-ttu-id="deb42-135">[![Java 7](../media/jdk/java-7.png)](https://www.azul.com/downloads/azure-only/zulu/#java7)</span><span class="sxs-lookup"><span data-stu-id="deb42-135">[![Java 7](../media/jdk/java-7.png)](https://www.azul.com/downloads/azure-only/zulu/#java7)</span></span> |<span data-ttu-id="deb42-136">Июль 2023 г.</span><span class="sxs-lookup"><span data-stu-id="deb42-136">July 2023</span></span> |
|<span data-ttu-id="deb42-137">[![Java 8](../media/jdk/java-8.png)](https://www.azul.com/downloads/azure-only/zulu/#java8)</span><span class="sxs-lookup"><span data-stu-id="deb42-137">[![Java 8](../media/jdk/java-8.png)](https://www.azul.com/downloads/azure-only/zulu/#java8)</span></span> |<span data-ttu-id="deb42-138">Март 2025 г.</span><span class="sxs-lookup"><span data-stu-id="deb42-138">March 2025</span></span>|
|<span data-ttu-id="deb42-139">[![Java 11](../media/jdk/java-11.png)](https://www.azul.com/downloads/azure-only/zulu/#java11)</span><span class="sxs-lookup"><span data-stu-id="deb42-139">[![Java 11](../media/jdk/java-11.png)](https://www.azul.com/downloads/azure-only/zulu/#java11)</span></span> |<span data-ttu-id="deb42-140">Сентябрь 2026 г.</span><span class="sxs-lookup"><span data-stu-id="deb42-140">September 2026</span></span>|
|<span data-ttu-id="deb42-141">[![Java 12](../media/jdk/java-12.png)]()</span><span class="sxs-lookup"><span data-stu-id="deb42-141">[![Java 12](../media/jdk/java-12.png)]()</span></span> |<span data-ttu-id="deb42-142">**Предварительный просмотр**</span><span class="sxs-lookup"><span data-stu-id="deb42-142">**Preview**</span></span>|

<span data-ttu-id="deb42-143">Для этих выпусков JDK выходят ежеквартальные обновления для системы безопасности и исправления ошибок, а также критические внеплановые обновления и исправления при необходимости.</span><span class="sxs-lookup"><span data-stu-id="deb42-143">These JDK releases have quarterly security updates, bug fixes, and critical out-of-band updates and patches as needed.</span></span> <span data-ttu-id="deb42-144">Эта поддержка предусматривает обратные порты обновлений безопасности и исправления ошибок для Java 7 и 8, имена которых присутствуют в более новых версиях Java, например Java 11.</span><span class="sxs-lookup"><span data-stu-id="deb42-144">This support includes back ports of security updates and bug fixes to Java 7 and 8 that are reported in newer versions of Java, such as Java 11.</span></span> <span data-ttu-id="deb42-145">Эта поддержка гарантирует непрерывную стабильность и безопасность более старых версий Java.</span><span class="sxs-lookup"><span data-stu-id="deb42-145">The support ensures the continued stability and security of older versions of Java.</span></span> <span data-ttu-id="deb42-146">Пользователи Azure могут получить эти обновления для системы безопасности и исправления ошибок платформы, не неся при этом незапланированных расходов на подписку на Java SE.</span><span class="sxs-lookup"><span data-stu-id="deb42-146">Azure customers can get these security updates and platform bug fixes without incurring any unplanned Java SE subscription fees.</span></span>

<span data-ttu-id="deb42-147">Выпуски от Azul Systems учитывают [график выхода новых версий Java SE](https://www.azul.com/products/azul_support_roadmap/).</span><span class="sxs-lookup"><span data-stu-id="deb42-147">Azul Systems maintains a [Java SE roadmap](https://www.azul.com/products/azul_support_roadmap/) for these releases.</span></span>

## <a name="benefits-for-developers"></a><span data-ttu-id="deb42-148">Преимущества для разработчиков</span><span class="sxs-lookup"><span data-stu-id="deb42-148">Benefits for developers</span></span>

<span data-ttu-id="deb42-149">Выпуски Azul Zulu JDK:</span><span class="sxs-lookup"><span data-stu-id="deb42-149">The Azul Zulu JDK releases are:</span></span>

* <span data-ttu-id="deb42-150">Поддерживаются корпорацией Майкрософт и Azul Systems.</span><span class="sxs-lookup"><span data-stu-id="deb42-150">Backed and supported by both Microsoft and Azul Systems.</span></span>

   * <span data-ttu-id="deb42-151">Двоичные файлы Zulu готовы к выпуску и поддерживаются корпорацией Майкрософт и Azul Systems.</span><span class="sxs-lookup"><span data-stu-id="deb42-151">Zulu binaries are production ready and backed by Microsoft and Azul Systems.</span></span>
   * <span data-ttu-id="deb42-152">Zulu поставляется с бесплатной долгосрочной поддержкой для Java 7, 8 и 11 (поддержка LTS будет оказываться и для Java 17).</span><span class="sxs-lookup"><span data-stu-id="deb42-152">Zulu comes with zero-cost LTS for Java 7, 8, and 11 (LTS will be provided for Java 17, as well).</span></span> <span data-ttu-id="deb42-153">Вы можете обновлять версии Java, только если это необходимо.</span><span class="sxs-lookup"><span data-stu-id="deb42-153">You can upgrade Java versions only when you need to.</span></span>
   * <span data-ttu-id="deb42-154">Java 7 поддерживается до июля 2023 г.</span><span class="sxs-lookup"><span data-stu-id="deb42-154">Java 7 is supported until July 2023.</span></span> <span data-ttu-id="deb42-155">Java 8 и 11 поддерживаются до 2024 года и дольше.</span><span class="sxs-lookup"><span data-stu-id="deb42-155">Java 8 and 11 are supported beyond 2024.</span></span>
   * <span data-ttu-id="deb42-156">Корпорация Майкрософт стремится запустить Zulu внутри на компьютерах, которые поддерживают многие службы Azure.</span><span class="sxs-lookup"><span data-stu-id="deb42-156">Microsoft is committed to running Zulu internally on machines that power many Azure services.</span></span>

* <span data-ttu-id="deb42-157">Готов к выпуску.</span><span class="sxs-lookup"><span data-stu-id="deb42-157">Production-ready.</span></span>

   * <span data-ttu-id="deb42-158">С полностью открытым кодом для сборок OpenJDK.</span><span class="sxs-lookup"><span data-stu-id="deb42-158">100 percent open-source for its builds of OpenJDK.</span></span>
   * <span data-ttu-id="deb42-159">Упрощенные замены для многих дистрибутивов Java SE.</span><span class="sxs-lookup"><span data-stu-id="deb42-159">Drop-in replacements for many Java SE distributions.</span></span>
   * <span data-ttu-id="deb42-160">JDK, JRE и автономная JRE.</span><span class="sxs-lookup"><span data-stu-id="deb42-160">JDK, JRE, and JRE-headless.</span></span>
   * <span data-ttu-id="deb42-161">Java 7, 8 и 11.</span><span class="sxs-lookup"><span data-stu-id="deb42-161">Java 7, 8, and 11.</span></span>
   * <span data-ttu-id="deb42-162">Проверены на соответствие спецификациям Java SE с использованием комплекта технологической совместимости (TCK) сообщества OpenJDK.</span><span class="sxs-lookup"><span data-stu-id="deb42-162">Verified compliant with the Java SE specifications that use the OpenJDK Community Technology Compatibility Kit (TCK).</span></span>
   * <span data-ttu-id="deb42-163">Разработчики продолжат получать производственные обновления для Java SE, в том числе исправления ошибок, улучшения производительности и исправления системы безопасности для Java SE 7, 8 и 11.</span><span class="sxs-lookup"><span data-stu-id="deb42-163">As a developer, you continue to receive production updates for Java SE, including bug fixes, performance enhancements, and security patches for Java SE 7, 8, and 11.</span></span>

* <span data-ttu-id="deb42-164">Поддерживаются для нескольких платформ.</span><span class="sxs-lookup"><span data-stu-id="deb42-164">Supported for multi-platform.</span></span> <span data-ttu-id="deb42-165">Zulu поддерживает двоичные файлы для нескольких платформ и версий, в том числе:</span><span class="sxs-lookup"><span data-stu-id="deb42-165">Zulu supports binaries for multiple platforms and versions, including:</span></span>

   * <span data-ttu-id="deb42-166">Клиент Windows</span><span class="sxs-lookup"><span data-stu-id="deb42-166">Windows client</span></span>
     * <span data-ttu-id="deb42-167">10</span><span class="sxs-lookup"><span data-stu-id="deb42-167">10</span></span>
     * <span data-ttu-id="deb42-168">8.1</span><span class="sxs-lookup"><span data-stu-id="deb42-168">8.1</span></span>
     * <span data-ttu-id="deb42-169">8, 7</span><span class="sxs-lookup"><span data-stu-id="deb42-169">8, 7</span></span>
   * <span data-ttu-id="deb42-170">Windows Server</span><span class="sxs-lookup"><span data-stu-id="deb42-170">Windows Server</span></span>
     * <span data-ttu-id="deb42-171">2016 R2</span><span class="sxs-lookup"><span data-stu-id="deb42-171">2016 R2</span></span>
     * <span data-ttu-id="deb42-172">2016</span><span class="sxs-lookup"><span data-stu-id="deb42-172">2016</span></span>
     * <span data-ttu-id="deb42-173">2012 R2</span><span class="sxs-lookup"><span data-stu-id="deb42-173">2012 R2</span></span>
     * <span data-ttu-id="deb42-174">2012</span><span class="sxs-lookup"><span data-stu-id="deb42-174">2012</span></span>
     * <span data-ttu-id="deb42-175">2008 R2</span><span class="sxs-lookup"><span data-stu-id="deb42-175">2008 R2</span></span>
   * <span data-ttu-id="deb42-176">Linux, включая</span><span class="sxs-lookup"><span data-stu-id="deb42-176">Linux, including</span></span>
     * <span data-ttu-id="deb42-177">RHEL</span><span class="sxs-lookup"><span data-stu-id="deb42-177">RHEL</span></span>
     * <span data-ttu-id="deb42-178">CentOS</span><span class="sxs-lookup"><span data-stu-id="deb42-178">CentOS</span></span>
     * <span data-ttu-id="deb42-179">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="deb42-179">Ubuntu</span></span>
     * <span data-ttu-id="deb42-180">SLES</span><span class="sxs-lookup"><span data-stu-id="deb42-180">SLES</span></span>
     * <span data-ttu-id="deb42-181">Debian</span><span class="sxs-lookup"><span data-stu-id="deb42-181">Debian</span></span>
     * <span data-ttu-id="deb42-182">Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="deb42-182">Oracle Linux</span></span>
   * <span data-ttu-id="deb42-183">macOS X</span><span class="sxs-lookup"><span data-stu-id="deb42-183">macOS X</span></span>
   * <span data-ttu-id="deb42-184">Предоставляются в нескольких видах упаковки:</span><span class="sxs-lookup"><span data-stu-id="deb42-184">Delivery in multiple package types:</span></span>
     * <span data-ttu-id="deb42-185">MSI, ZIP, TAR, DEB, RPM и DMG.</span><span class="sxs-lookup"><span data-stu-id="deb42-185">MSI, ZIP, TAR, DEB, RPM, and DMG</span></span>

    <span data-ttu-id="deb42-186">В Docker доступны сертифицированные образы контейнеров Docker для Zulu JDK, JRE и автономной среды JRE для нескольких базовых образов ОС.</span><span class="sxs-lookup"><span data-stu-id="deb42-186">Certified Docker container images for Zulu JDK, JRE, and JRE-headless on multiple base OS images are available at Docker.</span></span>

    <span data-ttu-id="deb42-187">Концентратор:</span><span class="sxs-lookup"><span data-stu-id="deb42-187">Hub:</span></span>

    * <span data-ttu-id="deb42-188">[JDK](https://hub.docker.com/_/microsoft-java-jdk).</span><span class="sxs-lookup"><span data-stu-id="deb42-188">[JDK](https://hub.docker.com/_/microsoft-java-jdk)</span></span>
    * [<span data-ttu-id="deb42-189">JRE</span><span class="sxs-lookup"><span data-stu-id="deb42-189">JRE</span></span>](https://hub.docker.com/_/microsoft-java-jre)
    * <span data-ttu-id="deb42-190">[Автономная среда JRE](https://hub.docker.com/_/microsoft-java-jre-headless).</span><span class="sxs-lookup"><span data-stu-id="deb42-190">[JRE-headless](https://hub.docker.com/_/microsoft-java-jre-headless)</span></span>

* <span data-ttu-id="deb42-191">Бесплатное использование.</span><span class="sxs-lookup"><span data-stu-id="deb42-191">No cost.</span></span>

   * <span data-ttu-id="deb42-192">Корпорация Майкрософт предоставляет все необходимое для создания и масштабирования приложений Java в Azure бесплатно.</span><span class="sxs-lookup"><span data-stu-id="deb42-192">Microsoft provides everything you need to build and scale Java apps on Azure, at no cost to you.</span></span> <span data-ttu-id="deb42-193">Через Zulu вы будете получать бесплатные обновления системы безопасности и исправления ошибок платформы для приложений Java без какой-либо платы.</span><span class="sxs-lookup"><span data-stu-id="deb42-193">Through Zulu you'll receive free security updates and platform bug fixes for Java apps without any fees.</span></span>
   * <span data-ttu-id="deb42-194">[Java Flight Recorder и Mission Control](java-jdk-flight-recorder-and-mission-control.md) доступны в Zulu Java 8, 11 и 12 (предварительная версия).</span><span class="sxs-lookup"><span data-stu-id="deb42-194">[Java Flight Recorder and Mission Control](java-jdk-flight-recorder-and-mission-control.md) are available in Zulu Java 8, 11, and 12 (Preview).</span></span>

* <span data-ttu-id="deb42-195">Доступна в виде технической предварительной версии без поддержки LTS.</span><span class="sxs-lookup"><span data-stu-id="deb42-195">Available as tech preview of non-LTS versions.</span></span>

   * <span data-ttu-id="deb42-196">Благодаря технической предварительной версии можно протестировать новые возможности сразу после их внедрения в текущих версиях, и которые со временем перейдут в Java 17 LTS.</span><span class="sxs-lookup"><span data-stu-id="deb42-196">With tech previews, you can progressively test new features as they're delivered, in short-term versions that will eventually graduate to Java 17 LTS.</span></span>

* <span data-ttu-id="deb42-197">Изменения в OpenJDK отправляются в вышестоящий репозитарий.</span><span class="sxs-lookup"><span data-stu-id="deb42-197">Changes to OpenJDK are sent upstream.</span></span>

   * <span data-ttu-id="deb42-198">Разработчики Azul Systems отправляют изменения Zulu в OpenJDK, что делает вышестоящий репозиторий целостным и инклюзивным.</span><span class="sxs-lookup"><span data-stu-id="deb42-198">Azul Systems committers push Zulu changes to OpenJDK, which makes the upstream repo comprehensive and inclusive.</span></span>

<span data-ttu-id="deb42-199">Как обычно, Java-разработчики могут перенести в Azure собственные среды выполнения Java, в том числе Oracle JDK и Red Hat JDK.</span><span class="sxs-lookup"><span data-stu-id="deb42-199">As always, as a Java developer, you can bring to Azure your own Java runtimes, including the Oracle JDK and the Red Hat JDK.</span></span> <span data-ttu-id="deb42-200">Можно также использовать безопасную инфраструктуру и многофункциональные службы.</span><span class="sxs-lookup"><span data-stu-id="deb42-200">You can also use the secure infrastructure and feature-rich services.</span></span> <span data-ttu-id="deb42-201">Выпуск Oracle Java SE для рабочей среды позволяет выполнять рабочие нагрузки Java на виртуальных машинах Azure (Windows или Linux).</span><span class="sxs-lookup"><span data-stu-id="deb42-201">The production edition of Oracle Java SE is available to you for running Java workloads in Windows or Linux virtual machines on Azure.</span></span>

## <a name="use-java-jdks-for-local-development"></a><span data-ttu-id="deb42-202">Использование пакетов Java JDK для локальной разработки</span><span class="sxs-lookup"><span data-stu-id="deb42-202">Use Java JDKs for local development</span></span> 

<span data-ttu-id="deb42-203">[Пакеты Java JDK для Azure и Azure Stack можно скачать](https://www.azul.com/downloads/azure-only/zulu/) для использования в локальных средах разработки.</span><span class="sxs-lookup"><span data-stu-id="deb42-203">You can [download Java JDKs for Azure and Azure Stack](https://www.azul.com/downloads/azure-only/zulu/) for use in your local development environments.</span></span> <span data-ttu-id="deb42-204">Файлы для скачивания доступны для Windows, Linux и macOS.</span><span class="sxs-lookup"><span data-stu-id="deb42-204">Downloads are available for Windows, Linux, and macOS.</span></span> <span data-ttu-id="deb42-205">При работе на платформе Linux, можно также получить пакеты с помощью диспетчеров пакетов [yum](https://www.azul.com/downloads/azure-only/zulu/#yum-repo) и [apt](https://www.azul.com/downloads/azure-only/zulu/#apt-repo).</span><span class="sxs-lookup"><span data-stu-id="deb42-205">If you're working on Linux, you can also get packages through the [yum](https://www.azul.com/downloads/azure-only/zulu/#yum-repo) and [apt](https://www.azul.com/downloads/azure-only/zulu/#apt-repo) package managers.</span></span>

<span data-ttu-id="deb42-206">Дополнительные рекомендации см. в статье [Use Docker with a JDK for Azure](java-jdk-docker-images.md) (Использование Docker с JDK для Azure).</span><span class="sxs-lookup"><span data-stu-id="deb42-206">For additional guidance, see [Docker images for Azure](java-jdk-docker-images.md).</span></span>
