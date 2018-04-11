---
title: Проверка подлинности с использованием библиотек управления Azure для Java
description: Проверка подлинности с помощью субъекта-службы в библиотеках управления Azure для Java
keywords: Azure, Java, SDK, API, Maven, Gradle, authentication, active directory, service principal
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 04/16/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: multiple
ms.assetid: 10f457e3-578b-4655-8cd1-51339226ee7d
ms.openlocfilehash: 3808c6d56b04f28c84a89a25219e4ec523f87964
ms.sourcegitcommit: 61030d025614b084e897809e603b2ec79900ec8d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/03/2018
---
# <a name="authenticate-with-the-azure-libraries-for-java"></a><span data-ttu-id="b548d-104">Проверка подлинности с использованием библиотек Azure для Java</span><span class="sxs-lookup"><span data-stu-id="b548d-104">Authenticate with the Azure libraries for Java</span></span> 

## <a name="connect-to-services-with-connection-strings"></a><span data-ttu-id="b548d-105">Подключение к службам с помощью строк подключения</span><span class="sxs-lookup"><span data-stu-id="b548d-105">Connect to services with connection strings</span></span>

<span data-ttu-id="b548d-106">Большинство библиотек служб Azure используют строку подключения или ключ безопасности для проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="b548d-106">Most Azure service libraries use a connection string or secure key for authentication.</span></span> <span data-ttu-id="b548d-107">Например, база данных SQL содержит имя пользователя и пароль в строке подключения JDBC:</span><span class="sxs-lookup"><span data-stu-id="b548d-107">For example, SQL Database includes username and password information in the JDBC connection string:</span></span>

```java
String url = "jdbc:sqlserver://myazuredb.database.windows.net:1433;" + 
        "database=testjavadb;" + 
        "user=myazdbuser;" +
        "password=myazdbpass;" +
        "encrypt=true;hostNameInCertificate=*.database.windows.net;loginTimeout=30;";
        Connection conn = DriverManager.getConnection(url);
```

<span data-ttu-id="b548d-108">Служба хранилища Azure использует ключ к хранилищу данных для проверки подлинности приложения:</span><span class="sxs-lookup"><span data-stu-id="b548d-108">Azure Storage uses a storage key to authorize the application:</span></span>

```java
final String storageConnection = "DefaultEndpointsProtocol=https;"
        + "AccountName=" + storageName 
        + ";AccountKey=" + storageKey
        + ";EndpointSuffix=core.windows.net";
```

<span data-ttu-id="b548d-109">Строки подключения службы используются для проверки подлинности других служб Azure, таких как [Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/sql-api-java-application#UseService), [кэш Redis](https://docs.microsoft.com/azure/redis-cache/cache-java-get-started) и [служебная шина](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-java-how-to-use-queues).</span><span class="sxs-lookup"><span data-stu-id="b548d-109">Service connection strings are used to authenticate to other Azure services like [Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/sql-api-java-application#UseService), [Redis Cache](https://docs.microsoft.com/azure/redis-cache/cache-java-get-started), and [Service Bus](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-java-how-to-use-queues).</span></span> <span data-ttu-id="b548d-110">Строки подключения можно получить с помощью портала или интерфейса командной строки Azure.</span><span class="sxs-lookup"><span data-stu-id="b548d-110">You can get the connection strings using the Azure portal or the CLI.</span></span>  <span data-ttu-id="b548d-111">Также с помощью библиотек управления Azure для Java можно выполнять запросы к ресурсам для создания строк подключения в коде.</span><span class="sxs-lookup"><span data-stu-id="b548d-111">You can also use the Azure management libraries for Java to query resources to build connection strings in your code.</span></span> 

<span data-ttu-id="b548d-112">Например, этот код использует библиотеки управления для создания строки подключения к учетной записи хранения:</span><span class="sxs-lookup"><span data-stu-id="b548d-112">For example, this code uses the management libraries to create a storage account connection string:</span></span>

```java
// create a new storage account
StorageAccount storage = azure.storageAccounts().getByResourceGroup("myResourceGroup","myStorageAccount");

// create a storage container to hold the file
List<StorageAccountKey> keys = storage.getKeys();
final String storageConnection = "DefaultEndpointsProtocol=https;"
        + "AccountName=" + storage.name()
        + ";AccountKey=" + keys.get(0).value()
        + ";EndpointSuffix=core.windows.net";
```

<span data-ttu-id="b548d-113">Другие библиотеки требуют, чтобы приложение работало с [субъектом-службой](https://docs.microsoft.com/azure/active-directory/develop/active-directory-application-objects), который разрешает приложению работать с предоставленными учетными данными.</span><span class="sxs-lookup"><span data-stu-id="b548d-113">Other libraries require your application to run with a [service prinicpal](https://docs.microsoft.com/azure/active-directory/develop/active-directory-application-objects) authorizing the application to run with granted credentials.</span></span> <span data-ttu-id="b548d-114">Эта конфигурация похожа на действия проверки подлинности на основе объектов для библиотеки управления, перечисленные ниже.</span><span class="sxs-lookup"><span data-stu-id="b548d-114">This configuration is similar to the object-based authentication steps for the management library listed below.</span></span>

<a name="mgmt-auth"></a>

##  <a name="authenticate-with-the-azure-management-libraries-for-java"></a><span data-ttu-id="b548d-115">Проверка подлинности с использованием библиотек управления Azure для Java</span><span class="sxs-lookup"><span data-stu-id="b548d-115">Authenticate with the Azure management libraries for Java</span></span>

<span data-ttu-id="b548d-116">Проверку подлинности приложения с помощью библиотек управления Azure для Java для создания и управления ресурсами можно выполнить двумя способами.</span><span class="sxs-lookup"><span data-stu-id="b548d-116">Two options are available to authenticate your application with Azure when using the Java management libraries to create and manage resources.</span></span>

### <a name="authenticate-with-an-applicationtokencredentials-object"></a><span data-ttu-id="b548d-117">Проверка подлинности с помощью объекта ApplicationTokenCredentials</span><span class="sxs-lookup"><span data-stu-id="b548d-117">Authenticate with an ApplicationTokenCredentials object</span></span>

<span data-ttu-id="b548d-118">Создайте экземпляр `ApplicationTokenCredentials`, чтобы предоставить учетные данные субъекта-службы объекту верхнего уровня `Azure` из кода.</span><span class="sxs-lookup"><span data-stu-id="b548d-118">Create an instance of `ApplicationTokenCredentials` to supply the service principal credentials to the top-level `Azure` object from inside your code.</span></span>

```java
import com.microsoft.azure.credentials.ApplicationTokenCredentials;
import com.microsoft.azure.AzureEnvironment;

// ...

ApplicationTokenCredentials credentials = new ApplicationTokenCredentials(client, 
        tenant,
        key, 
        AzureEnvironment.AZURE);
        
Azure azure = Azure
        .configure()
        .withLogLevel(LogLevel.NONE)
        .authenticate(credentials)
        .withDefaultSubscription();
```

<span data-ttu-id="b548d-119">`client`, `tenant` и `key` — это те же значения субъекта-службы, которые использовались для [проверки подлинности на основе файлов](#mgmt-file).</span><span class="sxs-lookup"><span data-stu-id="b548d-119">The `client`, `tenant` and `key` are the same service principal values used with [file-based authentication](#mgmt-file).</span></span> <span data-ttu-id="b548d-120">Значение `AzureEnvironment.AZURE` создает учетные данные для проверки подлинности в общедоступном облаке Azure.</span><span class="sxs-lookup"><span data-stu-id="b548d-120">The `AzureEnvironment.AZURE` value creates credentials against the Azure public cloud.</span></span> <span data-ttu-id="b548d-121">Если необходимо получить доступ к другому облаку (например, `AzureEnvironment.AZURE_GERMANY`), измените это значение.</span><span class="sxs-lookup"><span data-stu-id="b548d-121">Change this to a different value if you need to access another cloud (for example, `AzureEnvironment.AZURE_GERMANY`).</span></span>  

 <span data-ttu-id="b548d-122">Значения субъекта-службы можно найти в переменных среды или в хранилище управления секретами, например [Key Vault](/azure/key-vault/key-vault-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b548d-122">Read the service principal values from environment variables or a secret management store like [Key Vault](/azure/key-vault/key-vault-whatis.md).</span></span> <span data-ttu-id="b548d-123">Не рекомендуется задавать эти значения как строки открытого текста в коде, чтобы предотвратить случайный доступ к учетным данным из журнала управления версиями.</span><span class="sxs-lookup"><span data-stu-id="b548d-123">Avoid setting these values as cleartext strings in your code to prevent accidentally exposing credentials in your version control history.</span></span>   

<a name="mgmt-file"></a>

### <a name="file-based-authentication-preview"></a><span data-ttu-id="b548d-124">Проверка подлинности на основе файлов (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="b548d-124">File based authentication (Preview)</span></span>

<span data-ttu-id="b548d-125">Самый простой способ реализовать проверку подлинности — создать файл свойств, который содержит учетные данные для [субъекта-службы Azure](https://docs.microsoft.com/azure/active-directory/develop/active-directory-application-objects) в следующем формате:</span><span class="sxs-lookup"><span data-stu-id="b548d-125">The simplest way to authenticate is to create a properties file that contains credentials for an [Azure service principal](https://docs.microsoft.com/azure/active-directory/develop/active-directory-application-objects) using the following format:</span></span>

```text
# sample management library properties file
subscription=########-####-####-####-############
client=########-####-####-####-############
key=XXXXXXXXXXXXXXXX
tenant=########-####-####-####-############
managementURI=https\://management.core.windows.net/
baseURL=https\://management.azure.com/
authURL=https\://login.windows.net/
graphURL=https\://graph.windows.net/
```

- <span data-ttu-id="b548d-126">subscription — используйте значение *id* из `az account show` в Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="b548d-126">subscription: use the *id* value from `az account show` in the Azure CLI 2.0.</span></span>
- <span data-ttu-id="b548d-127">client — используйте значение *appId* из выходных данных субъекта-службы, созданного для запуска приложения.</span><span class="sxs-lookup"><span data-stu-id="b548d-127">client: use the *appId* value from the output taken from a service principal created to run the application.</span></span> <span data-ttu-id="b548d-128">Если вы не создали субъект-службу для приложения, [создайте его с помощью Azure CLI 2.0](https://docs.microsoft.com/cli/azure/create-an-azure-service-principal-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="b548d-128">If you don't have a service principal for your app, [create one with the Azure CLI 2.0](https://docs.microsoft.com/cli/azure/create-an-azure-service-principal-azure-cli).</span></span>
- <span data-ttu-id="b548d-129">key — используйте значение *password* из выходных данных CLI при создании субъекта-службы.</span><span class="sxs-lookup"><span data-stu-id="b548d-129">key: use the *password* value from the service principal create CLI output</span></span> 
- <span data-ttu-id="b548d-130">tenant — используйте значение *tenant* из выходных данных CLI при создании субъекта-службы.</span><span class="sxs-lookup"><span data-stu-id="b548d-130">tenant: use the *tenant* value from the service principal create CLI output</span></span>

<span data-ttu-id="b548d-131">Сохраните этот файл в безопасном расположении в вашей системе, доступном для кода.</span><span class="sxs-lookup"><span data-stu-id="b548d-131">Save this file in a secure location on your system where your code can read it.</span></span> <span data-ttu-id="b548d-132">Задайте переменную среды и укажите полный путь к файлу в оболочке:</span><span class="sxs-lookup"><span data-stu-id="b548d-132">Set an environment variable with the full path to the file in your shell:</span></span>

```bash
export AZURE_AUTH_LOCATION=/Users/raisa/azureauth.properties
```

<span data-ttu-id="b548d-133">Создайте точку входа объекта `Azure`, чтобы приступить к работе с библиотеками.</span><span class="sxs-lookup"><span data-stu-id="b548d-133">Create the entry point `Azure` object to start working with the libraries.</span></span> <span data-ttu-id="b548d-134">Найдите расположение файла свойств с помощью переменной среды.</span><span class="sxs-lookup"><span data-stu-id="b548d-134">Read the location of the properties file through the environment variable.</span></span>

```java
// pull in the location of the authenticaiton properties file from the environment 
final File credFile = new File(System.getenv("AZURE_AUTH_LOCATION"));

Azure azure = Azure
        .configure()
        .withLogLevel(LogLevel.NONE)
        .authenticate(credFile)
        .withDefaultSubscription();
```



