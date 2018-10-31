---
title: Средства для разработчиков Java в Azure | Документация Майкрософт
description: Средства интеграции IDE, эмуляторы, обозреватели ресурсов и интерфейсы командной строки для разработчиков Java, работающих со службами Azure.
author: rloutlaw
manager: douge
ms.assetid: b55923b7-d60a-460d-b77c-af5fac67f1cc
ms.devlang: java
ms.topic: article
ms.service: Azure
ms.technology: Azure
ms.date: 4/10/2017
ms.author: routlaw;asirveda
ms.openlocfilehash: dac0a1c576974a141950919292129890f4e15be4
ms.sourcegitcommit: 19876d17fed0afd9af0cb8e161f5a463696e74cf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/22/2018
ms.locfileid: "49634457"
---
# <a name="azure-tools-for-java-developers"></a><span data-ttu-id="e6313-103">Средства Azure для разработчиков Java</span><span class="sxs-lookup"><span data-stu-id="e6313-103">Azure tools for Java developers</span></span>

## <a name="supported-jdk-runtimes"></a><span data-ttu-id="e6313-104">Поддерживаемые среды выполнения JDK</span><span class="sxs-lookup"><span data-stu-id="e6313-104">Supported JDK runtimes</span></span>

<span data-ttu-id="e6313-105">В Azure и Azure Stack разработчики Java могут собирать и запускать производственные приложения на Java 7, 8 и 11 с помощью [сборок OpenJDK под названием Zulu Enterprise от Azul Systems](https://www.azul.com/downloads/azure-only/zulu/), не неся при этом дополнительных затрат на поддержку.</span><span class="sxs-lookup"><span data-stu-id="e6313-105">Java developers on Azure and Azure Stack can build and run production Java 7,8, and 11 applications using [Azul Systems Zulu Enterprise builds of OpenJDK](https://www.azul.com/downloads/azure-only/zulu/) without incurring additional support costs.</span></span> <span data-ttu-id="e6313-106">Если сейчас вы используете другие пакеты JDK в своих приложениях на Java, рассмотрите возможность перехода на Zulu в Azure, чтобы получить бесплатную поддержку и обслуживание.</span><span class="sxs-lookup"><span data-stu-id="e6313-106">If you’re currently running Java apps with other JDKs, consider migrating to Zulu on Azure for free support and maintenance.</span></span> 

<span data-ttu-id="e6313-107">См. [дополнительные сведения](java-supported-jdk-runtime.md) о поддержке сред выполнения Java в Azure.</span><span class="sxs-lookup"><span data-stu-id="e6313-107">[Learn more](java-supported-jdk-runtime.md) about Azure supported Java runtimes.</span></span>

## <a name="eclipse-and-intellij-plugins"></a><span data-ttu-id="e6313-108">Подключаемые модули Eclipse и IntelliJ</span><span class="sxs-lookup"><span data-stu-id="e6313-108">Eclipse and IntelliJ plugins</span></span>

<span data-ttu-id="e6313-109">Управляйте ресурсами Azure и развертывайте приложения из среды IDE с помощью наборов средств Azure для [Eclipse](eclipse/azure-toolkit-for-eclipse.md) и [IntelliJ](intellij/azure-toolkit-for-intellij.md).</span><span class="sxs-lookup"><span data-stu-id="e6313-109">Manage Azure resources and deploy apps from your IDE with The Azure toolkits for [Eclipse](eclipse/azure-toolkit-for-eclipse.md) and [IntelliJ](intellij/azure-toolkit-for-intellij.md).</span></span>   

![Набор средств IntelliJ с Azure Explorer](media/intelliJ-azure-explorer.png)

<span data-ttu-id="e6313-111">[Начало работы с набором средств Azure для Eclipse](https://docs.microsoft.com/azure/app-service-web/app-service-web-eclipse-create-hello-world-web-app) | [Начало работы с набором средств Azure для IntelliJ](https://docs.microsoft.com/azure/app-service-web/app-service-web-intellij-create-hello-world-web-app)</span><span class="sxs-lookup"><span data-stu-id="e6313-111">[Get started with Azure Toolkit for Eclipse](https://docs.microsoft.com/azure/app-service-web/app-service-web-eclipse-create-hello-world-web-app) | [Get started with Azure Toolkit for IntelliJ](https://docs.microsoft.com/azure/app-service-web/app-service-web-intellij-create-hello-world-web-app)</span></span> 

## <a name="visual-studio-code"></a><span data-ttu-id="e6313-112">Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="e6313-112">Visual Studio Code</span></span>

<span data-ttu-id="e6313-113">[VS Code](https://code.visualstudio.com/) — это легковесный, но в то же время мощный редактор кода, доступный для MacOS, Windows и Linux.</span><span class="sxs-lookup"><span data-stu-id="e6313-113">[VS Code](https://code.visualstudio.com/) is a lightweight but powerful code editor available for MacOS, Windows, and Linux.</span></span> <span data-ttu-id="e6313-114">VS Code поддерживает простой и современный рабочий процесс разработки с помощью Java, предлагая ряд расширений, которые облегчают навигацию и работу с проектом, а также позволяют выполнять запуск, отладку и форматирование кода.</span><span class="sxs-lookup"><span data-stu-id="e6313-114">VS Code supports a simple, modern Java development workflow through a set of extensions that provide project support, code completion, debugging, linting, and navigation.</span></span>

<span data-ttu-id="e6313-115">[Начало работы с VS Code и Java](https://code.visualstudio.com/docs/java)
[пакет расширений Java для VS Code](https://code.visualstudio.com/docs/java/extensions)</span><span class="sxs-lookup"><span data-stu-id="e6313-115">[Get Started with VS Code and Java](https://code.visualstudio.com/docs/java)
[Java extension pack for VS Code](https://code.visualstudio.com/docs/java/extensions)</span></span>  

## <a name="azure-cli-20"></a><span data-ttu-id="e6313-116">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="e6313-116">Azure CLI 2.0</span></span>

<span data-ttu-id="e6313-117">Azure CLI 2.0 позволяет управлять ресурсами Azure с помощью командной строки.</span><span class="sxs-lookup"><span data-stu-id="e6313-117">The Azure 2.0 CLI provides a command-line experience to manage Azure resources.</span></span> <span data-ttu-id="e6313-118">Его можно использовать в браузере с [Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/overview) или [установить](https://docs.microsoft.com/cli/azure/install-azure-cli) в macOS, Linux или Windows и запускать из командной строки.</span><span class="sxs-lookup"><span data-stu-id="e6313-118">You can use it in your browser with [Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/overview), or you can [install](https://docs.microsoft.com/cli/azure/install-azure-cli) it on macOS, Linux, and Windows and run it from the command line.</span></span>

<span data-ttu-id="e6313-119">[Начало работы с Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli)</span><span class="sxs-lookup"><span data-stu-id="e6313-119">[Get started with Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli).</span></span>

## <a name="azure-storage-explorer"></a><span data-ttu-id="e6313-120">обозреватель хранилищ Azure</span><span class="sxs-lookup"><span data-stu-id="e6313-120">Azure Storage Explorer</span></span> 

<span data-ttu-id="e6313-121">Управляйте учетными записями хранения Azure, контейнерами, большими двоичными объектами и файлами с настольного компьютера.</span><span class="sxs-lookup"><span data-stu-id="e6313-121">Manage Azure storage accounts, containers, and blobs/files from your desktop.</span></span> <span data-ttu-id="e6313-122">Сейчас обозреватель хранилища Azure доступен в предварительной версии и работает в Windows, macOS и Linux.</span><span class="sxs-lookup"><span data-stu-id="e6313-122">Azure Storage Explorer is currently in Preview and works on Windows, macOS, and Linux.</span></span>

[<span data-ttu-id="e6313-123">Приступая к работе с обозревателем службы хранилища (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="e6313-123">Get started with Azure Storage Explorer</span></span>](https://docs.microsoft.com/azure/vs-azure-tools-storage-manage-with-storage-explorer)
