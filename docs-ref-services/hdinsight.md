---
title: Пакет SDK Azure HDInsight для Java
description: Справочник по пакету SDK HDInsight для Java
keywords: Azure, Java, SDK, API, HDInsight
author: tylerfox
ms.author: tyfox
manager: arindamc
ms.date: 9/20/2018
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: hdinsight
ms.openlocfilehash: 4723613924d1a0c0b75cc8e4de28e3f59612ab19
ms.sourcegitcommit: 7c6a15f574fb85ee22f6ccdb7864627b73a6c1f7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/27/2018
ms.locfileid: "47398186"
---
# <a name="hdinsight-java-management-sdk-preview"></a><span data-ttu-id="83e25-104">Предварительная версия пакета SDK HDInsight для Java</span><span class="sxs-lookup"><span data-stu-id="83e25-104">HDInsight Java Management SDK Preview</span></span>

## <a name="overview"></a><span data-ttu-id="83e25-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="83e25-105">Overview</span></span>

<span data-ttu-id="83e25-106">Пакет SDK HDInsight для Java предоставляет классы и методы для управления кластерами HDInsight.</span><span class="sxs-lookup"><span data-stu-id="83e25-106">The HDInsight Java SDK provides classes and methods that allow you to manage your HDInsight clusters.</span></span> <span data-ttu-id="83e25-107">Пакет также поддерживает операции создания, удаления, обновления, получения списков, масштабирования, выполнения скриптов, мониторинга, получения свойства кластеров HDInsight и др.</span><span class="sxs-lookup"><span data-stu-id="83e25-107">It includes operations to create, delete, update, list, scale, execute script actions, monitor, get properties of HDInsight clusters, and more.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="83e25-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="83e25-108">Prerequisites</span></span>

* <span data-ttu-id="83e25-109">Учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="83e25-109">An Azure account.</span></span> <span data-ttu-id="83e25-110">Если у вас ее нет, [получите бесплатную пробную версию](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="83e25-110">If you don't have one, [get a free trial](https://azure.microsoft.com/free/).</span></span>
* [<span data-ttu-id="83e25-111">Java JDK</span><span class="sxs-lookup"><span data-stu-id="83e25-111">Java JDK</span></span>](https://www.oracle.com/technetwork/java/javase/downloads/index.html)
* [<span data-ttu-id="83e25-112">Maven</span><span class="sxs-lookup"><span data-stu-id="83e25-112">Maven</span></span>](https://maven.apache.org/install.html)

## <a name="sdk-installation"></a><span data-ttu-id="83e25-113">Установка пакета SDK</span><span class="sxs-lookup"><span data-stu-id="83e25-113">SDK Installation</span></span>

<span data-ttu-id="83e25-114">Пакет SDK HDInsight для Java доступен в [репозитории Maven](https://mvnrepository.com/artifact/com.microsoft.azure.hdinsight.v2018_06_01_preview/azure-mgmt-hdinsight).</span><span class="sxs-lookup"><span data-stu-id="83e25-114">The HDInsight Java SDK is available through Maven [here](https://mvnrepository.com/artifact/com.microsoft.azure.hdinsight.v2018_06_01_preview/azure-mgmt-hdinsight).</span></span> <span data-ttu-id="83e25-115">Добавьте следующую зависимость в файл pom.xml:</span><span class="sxs-lookup"><span data-stu-id="83e25-115">Add the following dependency to your pom.xml:</span></span>

```
<dependency>
    <groupId>com.microsoft.azure.hdinsight.v2018_06_01_preview</groupId>
    <artifactId>azure-mgmt-hdinsight</artifactId>
    <version>1.0.0-beta-1</version>
</dependency>
```

<span data-ttu-id="83e25-116">Также необходимо добавить такие зависимости в файл pom.xml:</span><span class="sxs-lookup"><span data-stu-id="83e25-116">You will also need to add the following dependencies to your pom.xml:</span></span>

* [<span data-ttu-id="83e25-117">Azure Client Authentication Library:</span><span class="sxs-lookup"><span data-stu-id="83e25-117">Azure Client Authentication Library:</span></span>](https://mvnrepository.com/artifact/com.microsoft.azure/azure-client-authentication/1.6.2)
```
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-client-authentication</artifactId>
    <version>1.6.2</version>
    <scope>test</scope>
</dependency>
```

* [<span data-ttu-id="83e25-118">Azure Java Client Runtime For ARM:</span><span class="sxs-lookup"><span data-stu-id="83e25-118">Azure Java Client Runtime For ARM:</span></span>](https://mvnrepository.com/artifact/com.microsoft.azure/azure-arm-client-runtime/1.6.2)
```
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-arm-client-runtime</artifactId>
    <version>1.6.2</version>
</dependency>
```

## <a name="authentication"></a><span data-ttu-id="83e25-119">Authentication</span><span class="sxs-lookup"><span data-stu-id="83e25-119">Authentication</span></span>

<span data-ttu-id="83e25-120">Для использования пакета SDK нужно выполнить аутентификацию с помощью подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="83e25-120">The SDK first needs to be authenticated with your Azure subscription.</span></span>  <span data-ttu-id="83e25-121">Ниже описано, как создать субъект-службу и использовать его для аутентификации.</span><span class="sxs-lookup"><span data-stu-id="83e25-121">Follow the example below to create a service principal and use it to authenticate.</span></span> <span data-ttu-id="83e25-122">После этого вы получите экземпляр `HDInsightManagementClientImpl`, в котором доступны различные методы (описанные далее) для операций управления.</span><span class="sxs-lookup"><span data-stu-id="83e25-122">After this is done, you will have an instance of an `HDInsightManagementClientImpl`, which contains many methods (outlined in below sections) that can be used to perform management operations.</span></span>

> [!NOTE]
> <span data-ttu-id="83e25-123">Кроме описанного выше, есть и другие методы аутентификации, которые могут оказаться удобнее для вас.</span><span class="sxs-lookup"><span data-stu-id="83e25-123">There are other ways to authenticate besides the below example that could potentially be better suited for your needs.</span></span> <span data-ttu-id="83e25-124">Все методы аутентификации см. в руководстве по [аутентификации с использованием библиотек управления Azure для Java](https://docs.microsoft.com/en-us/java/azure/java-sdk-azure-authenticate?view=azure-java-stable).</span><span class="sxs-lookup"><span data-stu-id="83e25-124">All methods are outlined here: [Authenticate with the Azure management libraries for Java](https://docs.microsoft.com/en-us/java/azure/java-sdk-azure-authenticate?view=azure-java-stable)</span></span>

### <a name="authentication-example-using-a-service-principal"></a><span data-ttu-id="83e25-125">Пример аутентификации с помощью субъекта-службы</span><span class="sxs-lookup"><span data-stu-id="83e25-125">Authentication Example Using a Service Principal</span></span>

<span data-ttu-id="83e25-126">Сначала войдите в [Azure Cloud Shell](https://shell.azure.com/bash).</span><span class="sxs-lookup"><span data-stu-id="83e25-126">First, login to [Azure Cloud Shell](https://shell.azure.com/bash).</span></span> <span data-ttu-id="83e25-127">Убедитесь, что вы используете подписку, в которой будет создан субъект-служба.</span><span class="sxs-lookup"><span data-stu-id="83e25-127">Verify you are currently using the subscription in which you want the service principal created.</span></span> 

```azurecli-interactive
az account show
```

<span data-ttu-id="83e25-128">Сведения о подписке отображаются в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="83e25-128">Your subscription information is displayed as JSON.</span></span>

```json
{
  "environmentName": "AzureCloud",
  "id": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
  "isDefault": true,
  "name": "XXXXXXX",
  "state": "Enabled",
  "tenantId": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
  "user": {
    "cloudShellID": true,
    "name": "XXX@XXX.XXX",
    "type": "user"
  }
}
```

<span data-ttu-id="83e25-129">Если вы вошли не в ту подписку, выполните такую команду, чтобы выбрать правильную подписку:</span><span class="sxs-lookup"><span data-stu-id="83e25-129">If you're not logged into the correct subscription, select the correct one by running:</span></span> 
```azurecli-interactive
az account set -s <name or ID of subscription>
```

> [!IMPORTANT]
> <span data-ttu-id="83e25-130">Если вы еще не зарегистрировали поставщик ресурсов HDInsight с помощью другого метода (например, создав кластер HDInsight на портале Azure), вам необходимо это сделать, прежде чем выполнять аутентификацию.</span><span class="sxs-lookup"><span data-stu-id="83e25-130">If you have not already registered the HDInsight Resource Provider by another method (such as by creating an HDInsight Cluster through the Azure Portal), you need to do this once before you can authenticate.</span></span> <span data-ttu-id="83e25-131">Это можно сделать с помощью [Azure Cloud Shell](https://shell.azure.com/bash), выполнив такую команду:</span><span class="sxs-lookup"><span data-stu-id="83e25-131">This can be done from the [Azure Cloud Shell](https://shell.azure.com/bash) by running the following command:</span></span>
>```azurecli-interactive
>az provider register --namespace Microsoft.HDInsight
>```

<span data-ttu-id="83e25-132">Создайте субъект-службу, выбрав имя и выполнив такую команду:</span><span class="sxs-lookup"><span data-stu-id="83e25-132">Next, choose a name for your service principal and create it with the following command:</span></span>

```azurecli-interactive
az ad sp create-for-rbac --name <Service Principal Name> --sdk-auth
```

<span data-ttu-id="83e25-133">Сведения о субъекте-службе отображаются в виде JSON.</span><span class="sxs-lookup"><span data-stu-id="83e25-133">The service principal information is displayed as JSON.</span></span>

```json
{
  "clientId": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
  "clientSecret": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
  "subscriptionId": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
  "tenantId": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
  "activeDirectoryEndpointUrl": "https://login.microsoftonline.com",
  "resourceManagerEndpointUrl": "https://management.azure.com/",
  "activeDirectoryGraphResourceId": "https://graph.windows.net/",
  "sqlManagementEndpointUrl": "https://management.core.windows.net:8443/",
  "galleryEndpointUrl": "https://gallery.azure.com/",
  "managementEndpointUrl": "https://management.core.windows.net/"
}
```
<span data-ttu-id="83e25-134">Скопируйте фрагмент кода ниже и задайте в качестве значений `TENANT_ID`, `CLIENT_ID`, `CLIENT_SECRET` и `SUBSCRIPTION_ID` строки из JSON-файла, возвращенного после выполнения команды для создания субъекта-службы.</span><span class="sxs-lookup"><span data-stu-id="83e25-134">Copy the below snippet and fill in `TENANT_ID`, `CLIENT_ID`, `CLIENT_SECRET`, and `SUBSCRIPTION_ID` with the strings from the JSON that was returned after running the command to create the service principal.</span></span>

```java
import com.microsoft.azure.management.hdinsight.v2018_06_01_preview.*;
import com.microsoft.azure.management.hdinsight.v2018_06_01_preview.implementation.HDInsightManagementClientImpl;

public class Main {
    public static void main (String[] args) {

        // Tenant ID for your Azure Subscription
        String TENANT_ID = "";
        // Your Service Principal App Client ID
        String CLIENT_ID = "";
        // Your Service Principal Client Secret
        String CLIENT_SECRET = "";
        // Azure Subscription ID
        String SUBSCRIPTION_ID = "";

        ApplicationTokenCredentials credentials = new ApplicationTokenCredentials(
                CLIENT_ID,
                TENANT_ID,
                CLIENT_SECRET,
                AzureEnvironment.AZURE);

        HDInsightManagementClientImpl client = new HDInsightManagementClientImpl(credentials);
```


## <a name="cluster-management"></a><span data-ttu-id="83e25-135">Управление кластерами</span><span class="sxs-lookup"><span data-stu-id="83e25-135">Cluster Management</span></span>

> [!NOTE]
> <span data-ttu-id="83e25-136">В этом разделе предполагается, что вы уже выполнили аутентификацию, создали экземпляр `HDInsightManagementClientImpl` и сохранили его в переменной с именем `client`.</span><span class="sxs-lookup"><span data-stu-id="83e25-136">This section assumes you have already authenticated and constructed an `HDInsightManagementClientImpl` instance and store it in a variable called `client`.</span></span> <span data-ttu-id="83e25-137">Инструкции по выполнению аутентификации и получению `HDInsightManagementClientImpl` см. в предыдущем разделе.</span><span class="sxs-lookup"><span data-stu-id="83e25-137">Instructions for authenticating and obtaining an `HDInsightManagementClientImpl` can be found in the Authentication section above.</span></span>

### <a name="create-a-cluster"></a><span data-ttu-id="83e25-138">Создание кластера</span><span class="sxs-lookup"><span data-stu-id="83e25-138">Create a Cluster</span></span>

<span data-ttu-id="83e25-139">Кластер можно создать, вызвав `client.clusters().create()`.</span><span class="sxs-lookup"><span data-stu-id="83e25-139">A new cluster can be created by calling `client.clusters().create()`.</span></span>

#### <a name="example"></a><span data-ttu-id="83e25-140">Пример</span><span class="sxs-lookup"><span data-stu-id="83e25-140">Example</span></span>

<span data-ttu-id="83e25-141">В этом примере показано, как создать кластер Spark с двумя головными узлами и одним рабочим.</span><span class="sxs-lookup"><span data-stu-id="83e25-141">This example demonstrates how to create a Spark cluster with 2 head nodes and 1 worker node.</span></span>

> [!NOTE]
> <span data-ttu-id="83e25-142">Сначала необходимо создать группу ресурсов и учетную запись хранения, как описано далее.</span><span class="sxs-lookup"><span data-stu-id="83e25-142">You first need to create a Resource Group and Storage Account, as explained below.</span></span> <span data-ttu-id="83e25-143">Если они уже созданы, следующие шаги можно пропустить.</span><span class="sxs-lookup"><span data-stu-id="83e25-143">If you have already created these, you can skip these steps.</span></span>

##### <a name="creating-a-resource-group"></a><span data-ttu-id="83e25-144">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="83e25-144">Creating a Resource Group</span></span>

<span data-ttu-id="83e25-145">Группу ресурсов можно создать с помощью [Azure Cloud Shell](https://shell.azure.com/bash), выполнив такую команду:</span><span class="sxs-lookup"><span data-stu-id="83e25-145">You can create a resource group using the [Azure Cloud Shell](https://shell.azure.com/bash) by running</span></span>
```azurecli-interactive
az group create -l <Region Name (i.e. eastus)> --n <Resource Group Name>
```
##### <a name="creating-a-storage-account"></a><span data-ttu-id="83e25-146">Создание учетной записи хранения</span><span class="sxs-lookup"><span data-stu-id="83e25-146">Creating a Storage Account</span></span>

<span data-ttu-id="83e25-147">Учетную запись хранения можно создать с помощью [Azure Cloud Shell](https://shell.azure.com/bash), выполнив такую команду:</span><span class="sxs-lookup"><span data-stu-id="83e25-147">You can create a storage account using the [Azure Cloud Shell](https://shell.azure.com/bash) by running:</span></span>
```azurecli-interactive
az storage account create -n <Storage Account Name> -g <Existing Resource Group Name> -l <Region Name (i.e. eastus)> --sku <SKU i.e. Standard_LRS>
```
<span data-ttu-id="83e25-148">Теперь выполните такую команду, чтобы получить ключ для учетной записи хранения (он потребуется для создания кластера):</span><span class="sxs-lookup"><span data-stu-id="83e25-148">Now run the following command to get the key for your storage account (you will need this to create a cluster):</span></span>
```azurecli-interactive
az storage account keys list -n <Storage Account Name>
```
---
<span data-ttu-id="83e25-149">Ниже показан фрагмент кода Java, который создает кластер Spark с двумя головными узлами и одним рабочим.</span><span class="sxs-lookup"><span data-stu-id="83e25-149">The below Java snippet creates a Spark cluster with 2 head nodes and 1 worker node.</span></span> <span data-ttu-id="83e25-150">Задайте переменные, как описано в комментариях, и при необходимости измените другие параметры.</span><span class="sxs-lookup"><span data-stu-id="83e25-150">Fill in the blank variables as explained in the comments and feel free to change other parameters to suit your specific needs.</span></span>

```java
// The name for the cluster you are creating
String clusterName = "";
// The name of your existing Resource Group
String resourceGroupName = "";
// Choose a username
String username = "";
// Choose a password
String password = "";
// Replace <> with the name of your storage account
String storageAccount = "<>.blob.core.windows.net";
// Storage account key you obtained above
String storageAccountKey = "";
// Choose a region
String location = "";
String container = "default";

HashMap<String, HashMap<String, String>> configurations = new HashMap<String, HashMap<String, String>>();
        HashMap<String, String> gateway = new HashMap<String, String>();
        gateway.put("restAuthCredential.enabled_credential", "True");
        gateway.put("restAuthCredential.username", username);
        gateway.put("restAuthCredential.password", password);
        configurations.put("gateway", gateway);

        ClusterCreateParametersExtended parameters = new ClusterCreateParametersExtended()
            .withLocation(location)
            .withTags(Collections.EMPTY_MAP)
            .withProperties(
                new ClusterCreateProperties()
                    .withClusterVersion("3.6")
                    .withOsType(OSType.LINUX)
                    .withClusterDefinition(new ClusterDefinition()
                            .withKind("spark")
                            .withConfigurations(configurations)
                    )
                    .withTier(Tier.STANDARD)
                    .withComputeProfile(new ComputeProfile()
                        .withRoles(List.of(
                            new Role()
                                .withName("headnode")
                                .withTargetInstanceCount(2)
                                .withHardwareProfile(new HardwareProfile()
                                    .withVmSize("Large")
                                )
                                .withOsProfile(new OsProfile()
                                    .withLinuxOperatingSystemProfile(new LinuxOperatingSystemProfile()
                                            .withUsername(username)
                                            .withPassword(password)
                                    )
                                ),
                            new Role()
                                    .withName("workernode")
                                    .withTargetInstanceCount(1)
                                    .withHardwareProfile(new HardwareProfile()
                                        .withVmSize("Large")
                                    )
                                    .withOsProfile(new OsProfile()
                                        .withLinuxOperatingSystemProfile(new LinuxOperatingSystemProfile()
                                            .withUsername(username)
                                            .withPassword(password)
                                        )
                                    )
                        ))
                    )
                    .withStorageProfile(new StorageProfile()
                        .withStorageaccounts(List.of(
                                new StorageAccount()
                                    .withName(storageAccount)
                                    .withKey(storageAccountKey)
                                    .withContainer(container)
                                    .withIsDefault(true)
                        ))
                    )
            );
        client.clusters().create(resourceGroupName, clusterName, parameters);
```

### <a name="get-cluster-details"></a><span data-ttu-id="83e25-151">Получение сведений о кластере</span><span class="sxs-lookup"><span data-stu-id="83e25-151">Get Cluster Details</span></span>

<span data-ttu-id="83e25-152">Чтобы получить сведения о свойствах кластера, выполните такую команду:</span><span class="sxs-lookup"><span data-stu-id="83e25-152">To get properties for a given cluster:</span></span>

```java
client.clusters.getByResourceGroup("<Resource Group Name>", "<Cluster Name>");
```

#### <a name="example"></a><span data-ttu-id="83e25-153">Пример</span><span class="sxs-lookup"><span data-stu-id="83e25-153">Example</span></span>

<span data-ttu-id="83e25-154">Чтобы убедиться в том, что вы создали кластер, можно использовать `get`.</span><span class="sxs-lookup"><span data-stu-id="83e25-154">You can use `get` to confirm that you have successfully created your cluster.</span></span>

```java
ClusterInner cluster = client.clusters().getByResourceGroup("<Resource Group Name>", "<Cluster Name>");
System.out.println(cluster.name()); //Prints the name of the cluster
System.out.println(cluster.id()); //Prints the resource Id of the cluster
```

<span data-ttu-id="83e25-155">Выходные данные должны выглядеть так:</span><span class="sxs-lookup"><span data-stu-id="83e25-155">The output should look like:</span></span>

```
<Cluster Name>
/subscriptions/XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX/resourceGroups/<Resource Group Name>/providers/Microsoft.HDInsight/clusters/<Cluster Name>
```

### <a name="list-clusters"></a><span data-ttu-id="83e25-156">Получение списка кластеров</span><span class="sxs-lookup"><span data-stu-id="83e25-156">List Clusters</span></span>

#### <a name="list-clusters-under-the-subscription"></a><span data-ttu-id="83e25-157">Получение списка кластеров в пределах подписки</span><span class="sxs-lookup"><span data-stu-id="83e25-157">List Clusters Under The Subscription</span></span>

```java
client.clusters.list();
```
#### <a name="list-clusters-by-resource-group"></a><span data-ttu-id="83e25-158">Получение списка кластеров в пределах в группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="83e25-158">List Clusters By Resource Group</span></span>

```java
client.clusters.listByResourceGroup("<Resource Group Name>");
```
> [!NOTE]
> <span data-ttu-id="83e25-159">Вызов `List()` и `ListByResourceGroup()` возвращает объект `PagedList<ClusterInner>`.</span><span class="sxs-lookup"><span data-stu-id="83e25-159">Both `List()` and `ListByResourceGroup()` return a `PagedList<ClusterInner>` object.</span></span> <span data-ttu-id="83e25-160">Вызов `loadNext()` возвращает список кластеров на этой странице и перемещает объект `ClusterPaged` на следующую страницу.</span><span class="sxs-lookup"><span data-stu-id="83e25-160">Calling `loadNext()` returns a list of clusters on that page and advances the `ClusterPaged` object to the next page.</span></span> <span data-ttu-id="83e25-161">Действие можно повторять, пока `hasNextPage()` не примет значение `false`, указывающее на последнюю страницу.</span><span class="sxs-lookup"><span data-stu-id="83e25-161">This can be repeated until `hasNextPage()` return `false`, indicating that there are no more pages.</span></span>

#### <a name="example"></a><span data-ttu-id="83e25-162">Пример</span><span class="sxs-lookup"><span data-stu-id="83e25-162">Example</span></span>

<span data-ttu-id="83e25-163">В следующем примере выводятся свойства всех кластеров в пределах текущей подписки:</span><span class="sxs-lookup"><span data-stu-id="83e25-163">The following example prints the properties of all clusters for the current subscription:</span></span>

```java
PagedList<ClusterInner> clusterPages = client.clusters().list();
while (true) {
    for (ClusterInner cluster : clusterPages.currentPage().items()) {
        System.out.println(cluster.name());
    }
    if (clusterPages.hasNextPage()) {
        clusterPages.loadNextPage();
    } else {
        break;
    }
}
```

### <a name="delete-a-cluster"></a><span data-ttu-id="83e25-164">Удаление кластера</span><span class="sxs-lookup"><span data-stu-id="83e25-164">Delete a Cluster</span></span>

<span data-ttu-id="83e25-165">Чтобы удалить кластер, выполните такую команду:</span><span class="sxs-lookup"><span data-stu-id="83e25-165">To delete a cluster:</span></span>

```java
client.clusters.delete("<Resource Group Name>", "<Cluster Name>");
```

### <a name="update-cluster-tags"></a><span data-ttu-id="83e25-166">Обновление тегов кластера</span><span class="sxs-lookup"><span data-stu-id="83e25-166">Update Cluster Tags</span></span>

<span data-ttu-id="83e25-167">Вы можете обновить теги кластера так:</span><span class="sxs-lookup"><span data-stu-id="83e25-167">You can update the tags of a given cluster like so:</span></span>

```java
client.clusters.update("<Resource Group Name>", "<Cluster Name>", <Map<String,String> of Tags>);
```

### <a name="scale-cluster"></a><span data-ttu-id="83e25-168">Масштабирование кластера</span><span class="sxs-lookup"><span data-stu-id="83e25-168">Scale Cluster</span></span>

<span data-ttu-id="83e25-169">Вы можете масштабировать кластер, изменяя количество его рабочих узлов так:</span><span class="sxs-lookup"><span data-stu-id="83e25-169">You can scale a given cluster's number of worker nodes by specifying a new size like so:</span></span>

```java
client.clusters.resize("<Resource Group Name>", "<Cluster Name>", <Num of Worker Nodes (int)>)
```

## <a name="cluster-monitoring"></a><span data-ttu-id="83e25-170">Мониторинг кластера</span><span class="sxs-lookup"><span data-stu-id="83e25-170">Cluster Monitoring</span></span>

<span data-ttu-id="83e25-171">Пакет Azure Management SDK для HDInsight также позволяет управлять мониторингом кластеров с помощью Operations Management Suite (OMS).</span><span class="sxs-lookup"><span data-stu-id="83e25-171">The HDInsight Management SDK can also be used to manage monitoring on your clusters via the Operations Management Suite (OMS).</span></span>

### <a name="enable-oms-monitoring"></a><span data-ttu-id="83e25-172">Включение мониторинга OMS</span><span class="sxs-lookup"><span data-stu-id="83e25-172">Enable OMS Monitoring</span></span>

> [!NOTE]
> <span data-ttu-id="83e25-173">Чтобы включить мониторинг OMS, требуется рабочая область Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="83e25-173">To enable OMS Monitoring, you must have an existing Log Analytics workspace.</span></span> <span data-ttu-id="83e25-174">Если вы не создавали такую рабочую область, см. статью [Создание рабочей области Log Analytics на портале Azure](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-quick-create-workspace).</span><span class="sxs-lookup"><span data-stu-id="83e25-174">If you have not already created one, you can learn how to do that here: [Create a Log Analytics workspace in the Azure portal](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-quick-create-workspace).</span></span>

<span data-ttu-id="83e25-175">Чтобы включить мониторинг OMS в кластере, выполните такую команду:</span><span class="sxs-lookup"><span data-stu-id="83e25-175">To enable OMS Monitoring on your cluster:</span></span>

```java
client.extensions().enableMonitoring("<Resource Group Name", "<Cluster Name>", new ClusterMonitoringRequest().withWorkspaceId("<Workspace Id>"));
```

### <a name="view-status-of-oms-monitoring"></a><span data-ttu-id="83e25-176">Просмотр состояния мониторинга OMS</span><span class="sxs-lookup"><span data-stu-id="83e25-176">View Status Of OMS Monitoring</span></span>

<span data-ttu-id="83e25-177">Чтобы узнать состояние мониторинга OMS в кластере, выполните такую команду:</span><span class="sxs-lookup"><span data-stu-id="83e25-177">To get the status of OMS on your cluster:</span></span>

```java
client.extensions().getMonitoringStatus("<Resource Group Name", "Cluster Name");
```

### <a name="disable-oms-monitoring"></a><span data-ttu-id="83e25-178">Отключение мониторинга OMS</span><span class="sxs-lookup"><span data-stu-id="83e25-178">Disable OMS Monitoring</span></span>

<span data-ttu-id="83e25-179">Чтобы отключить мониторинг OMS в кластере, выполните такую команду:</span><span class="sxs-lookup"><span data-stu-id="83e25-179">To disable OMS on your cluster:</span></span>

```java
client.extensions().disableMonitoring("<Resource Group Name>", "<Cluster Name>");
```

## <a name="script-actions"></a><span data-ttu-id="83e25-180">Элемент "Действия скрипта"</span><span class="sxs-lookup"><span data-stu-id="83e25-180">Script Actions</span></span>

<span data-ttu-id="83e25-181">В кластерах HDInsight поддерживается метод конфигурации с использованием, действий скриптов, который вызывает пользовательские скрипты для настройки кластера.</span><span class="sxs-lookup"><span data-stu-id="83e25-181">HDInsight provides a configuration method called script actions that invokes custom scripts to customize the cluster.</span></span>
> [!NOTE]
> <span data-ttu-id="83e25-182">Дополнительные сведения о действиях скриптов см. в статье [Настройка кластеров HDInsight под управлением Linux с помощью действий сценариев](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux).</span><span class="sxs-lookup"><span data-stu-id="83e25-182">More information on how to use script actions can be found here: [Customize Linux-based HDInsight clusters using script actions](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux)</span></span>

### <a name="execute-script-actions"></a><span data-ttu-id="83e25-183">Выполнение действий скриптов</span><span class="sxs-lookup"><span data-stu-id="83e25-183">Execute Script Actions</span></span>

<span data-ttu-id="83e25-184">Вы можете выполнить действия скриптов в кластере так:</span><span class="sxs-lookup"><span data-stu-id="83e25-184">You can execute script actions on a given cluster like so:</span></span>

```java
RuntimeScriptAction scriptAction1 = new RuntimeScriptAction()
    .withName("<Script Name>")
    .withUri("<URL To Script>")
    .withRoles(<List<String> of roles>);
client.clusters().executeScriptActions(
    resourceGroupName, 
    clusterName, 
    new ExecuteScriptActionParameters().withPersistOnSuccess(false).withScriptActions(new LinkedList<>(Arrays.asList(scriptAction1)))); //add more RuntimeScriptActions to the list to execute multiple scripts
```

### <a name="delete-script-action"></a><span data-ttu-id="83e25-185">Удаление действий скриптов</span><span class="sxs-lookup"><span data-stu-id="83e25-185">Delete Script Action</span></span>

<span data-ttu-id="83e25-186">Чтобы удалить сохраненные действия скриптов в кластере, выполните такую команду:</span><span class="sxs-lookup"><span data-stu-id="83e25-186">To delete a specified persisted script action on a given cluster:</span></span>

```java
client.scriptActions().delete("<Resource Group Name>", "<Cluster Name>", "<Script Name>");
```

### <a name="list-persisted-script-actions"></a><span data-ttu-id="83e25-187">Получение списка сохраненных действий скриптов</span><span class="sxs-lookup"><span data-stu-id="83e25-187">List Persisted Script Actions</span></span>

> [!NOTE]
> <span data-ttu-id="83e25-188">Метод `listByCluster()` возвращает объект `PagedList<RuntimeScriptActionDetailInner>`.</span><span class="sxs-lookup"><span data-stu-id="83e25-188">Both `listByCluster()` returns a `PagedList<RuntimeScriptActionDetailInner>` object.</span></span> <span data-ttu-id="83e25-189">Вызов `currentPage().items()` возвращает список `RuntimeScriptActionDetailInner`, а `loadNextPage()` выполняет переход к следующей странице.</span><span class="sxs-lookup"><span data-stu-id="83e25-189">Calling `currentPage().items()` returns a list of `RuntimeScriptActionDetailInner`, and `loadNextPage()` advances to the next page.</span></span> <span data-ttu-id="83e25-190">Действие можно повторять, пока `hasNextPage()` не примет значение `false`, указывающее на последнюю страницу.</span><span class="sxs-lookup"><span data-stu-id="83e25-190">This can be repeated until `hasNextPage()` returns `false`, indicating that there are no more pages.</span></span>

<span data-ttu-id="83e25-191">Чтобы получить список всех сохраненных действий скриптов в кластере, выполните такую команду:</span><span class="sxs-lookup"><span data-stu-id="83e25-191">To list all persisted script actions for the specified cluster:</span></span>
```java
client.scriptActions().listByCluster("<Resource Group Name>", "<Cluster Name>");
```

#### <a name="example"></a><span data-ttu-id="83e25-192">Пример</span><span class="sxs-lookup"><span data-stu-id="83e25-192">Example</span></span>

```java
PagedList<RuntimeScriptActionDetailInner> scriptsPaged = client.scriptActions().listByCluster(resourceGroupName, clusterName);
while (true) {
    for (RuntimeScriptActionDetailInner script : scriptsPaged.currentPage().items()) {
        System.out.println(script.name()); //There are methods to get other properties of RuntimeScriptActionDetail besides name(), such as status(), operation(), startTime(), endTime(), etc. See reference documentation.
    }
    if (scriptsPaged.hasNextPage()) {
        scriptsPaged.loadNextPage();
    } else {
        break;
    }
}
```

### <a name="list-all-scripts-execution-history"></a><span data-ttu-id="83e25-193">Просмотр журнала выполнения всех скриптов</span><span class="sxs-lookup"><span data-stu-id="83e25-193">List All Scripts' Execution History</span></span>

<span data-ttu-id="83e25-194">Чтобы получить журнал выполнения всех скриптов в кластере, выполните такую команду:</span><span class="sxs-lookup"><span data-stu-id="83e25-194">To list all scripts' execution history for the specified cluster:</span></span>

```java
client.scriptExecutionHistorys().listByCluster("<Resource Group Name>", "<Cluster Name>");
```

#### <a name="example"></a><span data-ttu-id="83e25-195">Пример</span><span class="sxs-lookup"><span data-stu-id="83e25-195">Example</span></span>

<span data-ttu-id="83e25-196">В этом примере выводятся сведения обо всех выполнявшихся скриптах.</span><span class="sxs-lookup"><span data-stu-id="83e25-196">This example prints all the details for all past script executions.</span></span>

```java
PagedList<RuntimeScriptActionDetailInner> scriptExecutionsPaged = client.scriptExecutionHistorys().listByCluster(resourceGroupName, clusterName);
while (true) {
    for (RuntimeScriptActionDetailInner script : scriptExecutionsPaged.currentPage().items()) {
        System.out.println(script.name()); //There are methods to get other properties of RuntimeScriptActionDetail besides name(), such as status(), operation(), startTime(), endTime(), etc. See reference documentation.
    }
    if (scriptExecutionsPaged.hasNextPage()) {
        scriptExecutionsPaged.loadNextPage();
    } else {
        break;
    }
}
```