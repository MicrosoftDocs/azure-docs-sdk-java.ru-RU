---
title: "Средства для разработчиков Java в Azure | Документация Майкрософт"
description: "Средства интеграции IDE, эмуляторы, обозреватели ресурсов и интерфейсы командной строки для разработчиков Java, работающих со службами Azure."
author: rloutlaw
manager: douge
ms.assetid: b55923b7-d60a-460d-b77c-af5fac67f1cc
ms.devlang: java
ms.topic: article
ms.service: Azure
ms.technology: Azure
ms.date: 4/10/2017
ms.author: routlaw;asirveda
ms.openlocfilehash: 01fe31f2c59810f972875331d49ce5130755c8f2
ms.sourcegitcommit: 1500f341a96d9da461c288abf4baf79f494ae662
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/28/2017
---
# <a name="azure-tools-for-java-developers"></a><span data-ttu-id="23fed-103">Средства Azure для разработчиков Java</span><span class="sxs-lookup"><span data-stu-id="23fed-103">Azure tools for Java developers</span></span>

## <a name="client-and-management-libraries"></a><span data-ttu-id="23fed-104">Клиентские библиотеки и библиотеки управления</span><span class="sxs-lookup"><span data-stu-id="23fed-104">Client and management libraries</span></span>

<span data-ttu-id="23fed-105">Подключайтесь к службам и управляйте ресурсами Azure из своих приложений с помощью библиотек Azure для Java.</span><span class="sxs-lookup"><span data-stu-id="23fed-105">Connect to services and manage Azure resources from your applications with the Azure libraries for Java.</span></span> <span data-ttu-id="23fed-106">Импортируйте библиотеки управления в проекты Maven, добавляя следующую зависимость в файл проекта *pom.xml*.</span><span class="sxs-lookup"><span data-stu-id="23fed-106">Import the management libraries into your Maven projects by adding this dependency to your project *pom.xml*.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure</artifactId>
    <version>1.1.2</version>
</dependency>
```

<span data-ttu-id="23fed-107">Просмотрите [полный список библиотек](java-sdk-azure-install.md) и [начните работу](java-sdk-azure-get-started.md) с библиотеками Azure для Java.</span><span class="sxs-lookup"><span data-stu-id="23fed-107">View the [complete list of libraries](java-sdk-azure-install.md) and [get started](java-sdk-azure-get-started.md) with the Azure libraries for Java.</span></span>

## <a name="eclipse-and-intellij-plugins"></a><span data-ttu-id="23fed-108">Подключаемые модули Eclipse и IntelliJ</span><span class="sxs-lookup"><span data-stu-id="23fed-108">Eclipse and IntelliJ plugins</span></span>

<span data-ttu-id="23fed-109">Управляйте ресурсами Azure и развертывайте приложения из среды IDE с помощью наборов средств Azure для [Eclipse](https://docs.microsoft.com/azure/azure-toolkit-for-eclipse) и [IntelliJ](https://docs.microsoft.com/azure/azure-toolkit-for-intellij).</span><span class="sxs-lookup"><span data-stu-id="23fed-109">Manage Azure resources and deploy apps from your IDE with The Azure toolkits for [Eclipse](https://docs.microsoft.com/azure/azure-toolkit-for-eclipse) and [IntelliJ](https://docs.microsoft.com/azure/azure-toolkit-for-intellij).</span></span>   

![Набор средств IntelliJ с Azure Explorer](media/intelliJ-azure-explorer.png)

[<span data-ttu-id="23fed-111">Начало работы с набором средств Azure для Eclipse](https://docs.microsoft.com/azure/app-service-web/app-service-web-eclipse-create-hello-world-web-app) | [Начало работы с набором средств Azure для IntelliJ</span><span class="sxs-lookup"><span data-stu-id="23fed-111">Get started with Azure Toolkit for Eclipse](https://docs.microsoft.com/azure/app-service-web/app-service-web-eclipse-create-hello-world-web-app) | [Get started with Azure Toolkit for IntelliJ</span></span>](https://docs.microsoft.com/azure/app-service-web/app-service-web-intellij-create-hello-world-web-app) 

## <a name="azure-cli-20"></a><span data-ttu-id="23fed-112">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="23fed-112">Azure CLI 2.0</span></span>

<span data-ttu-id="23fed-113">Azure CLI 2.0 позволяет управлять ресурсами Azure с помощью командной строки.</span><span class="sxs-lookup"><span data-stu-id="23fed-113">The Azure 2.0 CLI provides a command-line experience to manage Azure resources.</span></span> <span data-ttu-id="23fed-114">Его можно использовать в браузере с [Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/overview) или [установить](https://docs.microsoft.com/cli/azure/install-azure-cli) в macOS, Linux или Windows и запускать из командной строки.</span><span class="sxs-lookup"><span data-stu-id="23fed-114">You can use it in your browser with [Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/overview), or you can [install](https://docs.microsoft.com/cli/azure/install-azure-cli) it on macOS, Linux, and Windows and run it from the command line.</span></span>

<span data-ttu-id="23fed-115">[Начало работы с Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli)</span><span class="sxs-lookup"><span data-stu-id="23fed-115">[Get started with Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli).</span></span>

## <a name="azure-storage-explorer"></a><span data-ttu-id="23fed-116">обозреватель хранилищ Azure</span><span class="sxs-lookup"><span data-stu-id="23fed-116">Azure Storage Explorer</span></span> 

<span data-ttu-id="23fed-117">Управляйте учетными записями хранения Azure, контейнерами, большими двоичными объектами и файлами с настольного компьютера.</span><span class="sxs-lookup"><span data-stu-id="23fed-117">Manage Azure storage accounts, containers, and blobs/files from your desktop.</span></span> <span data-ttu-id="23fed-118">Сейчас обозреватель хранилища Azure доступен в предварительной версии и работает в Windows, macOS и Linux.</span><span class="sxs-lookup"><span data-stu-id="23fed-118">Azure Storage Explorer is currently in Preview and works on Windows, macOS, and Linux.</span></span>

[<span data-ttu-id="23fed-119">Приступая к работе с обозревателем службы хранилища (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="23fed-119">Get started with Azure Storage Explorer</span></span>](https://docs.microsoft.com/azure/vs-azure-tools-storage-manage-with-storage-explorer)