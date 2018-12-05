---
title: Пакет SDK Azure HDInsight для Java
description: Справочник по пакету SDK Azure HDInsight для Java. Пакет SDK HDInsight для Java предоставляет классы и методы для управления кластерами HDInsight.
author: tylerfox
ms.author: tyfox
ms.reviewer: jasonh
ms.service: hdinsight
ms.topic: reference
ms.devlang: java
ms.date: 11/21/2018
ms.openlocfilehash: 96ecbedc90706775a80b97c42f0d55a46a45b8ac
ms.sourcegitcommit: 8d0c59ae7c91adbb9be3c3e6d4a3429ffe51519d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/27/2018
ms.locfileid: "52338688"
---
# <a name="hdinsight-java-management-sdk-preview"></a>Пакет SDK для управления HDInsight для Java (предварительная версия)

## <a name="overview"></a>Обзор

Пакет SDK HDInsight для Java предоставляет классы и методы для управления кластерами HDInsight. Пакет также поддерживает операции создания, удаления, обновления, получения списков, масштабирования, выполнения скриптов, мониторинга, получения свойства кластеров HDInsight и т. д.

## <a name="prerequisites"></a>Предварительные требования

* Учетная запись Azure. Если у вас ее нет, [получите бесплатную пробную версию](https://azure.microsoft.com/free/).
* Поддерживаемая версия Java Development Kit (JDK). Дополнительные сведения о версиях JDK, доступных для разработки в Azure, см. в статье <https://aka.ms/azure-jdks>.
* [Maven](https://maven.apache.org/install.html)

## <a name="sdk-installation"></a>Установка пакета SDK

Пакет SDK HDInsight для Java доступен в [репозитории Maven](https://mvnrepository.com/artifact/com.microsoft.azure.hdinsight.v2018_06_01_preview/azure-mgmt-hdinsight). Добавьте следующую зависимость в файл pom.xml:

```
<dependency>
    <groupId>com.microsoft.azure.hdinsight.v2018_06_01_preview</groupId>
    <artifactId>azure-mgmt-hdinsight</artifactId>
    <version>1.0.0-beta-1</version>
</dependency>
```

Также необходимо добавить такие зависимости в файл pom.xml:

* [Azure Client Authentication Library:](https://mvnrepository.com/artifact/com.microsoft.azure/azure-client-authentication/1.6.2)
  ```
  <dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-client-authentication</artifactId>
    <version>1.6.2</version>
    <scope>test</scope>
  </dependency>
  ```

* [Azure Java Client Runtime For ARM:](https://mvnrepository.com/artifact/com.microsoft.azure/azure-arm-client-runtime/1.6.2)
  ```
  <dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-arm-client-runtime</artifactId>
    <version>1.6.2</version>
  </dependency>
  ```

## <a name="authentication"></a>Authentication

Для использования пакета SDK нужно выполнить аутентификацию с помощью подписки Azure.  Ниже описано, как создать субъект-службу и использовать его для аутентификации. После этого вы получите экземпляр `HDInsightManagementClientImpl`, в котором доступны различные методы (описанные далее) для операций управления.

> [!NOTE]
> Кроме описанного выше, есть и другие методы аутентификации, которые могут оказаться удобнее для вас. Все методы аутентификации см. в руководстве по [аутентификации с использованием библиотек управления Azure для Java](https://docs.microsoft.com/en-us/java/azure/java-sdk-azure-authenticate?view=azure-java-stable).

### <a name="authentication-example-using-a-service-principal"></a>Пример аутентификации с помощью субъекта-службы

Сначала войдите в [Azure Cloud Shell](https://shell.azure.com/bash). Убедитесь, что вы используете подписку, в которой будет создан субъект-служба. 

```azurecli-interactive
az account show
```

Сведения о подписке отображаются в формате JSON.

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

Если вы вошли не в ту подписку, выполните такую команду, чтобы выбрать правильную подписку: 
```azurecli-interactive
az account set -s <name or ID of subscription>
```

> [!IMPORTANT]
> Если вы еще не зарегистрировали поставщик ресурсов HDInsight с помощью другого метода (например, создав кластер HDInsight на портале Azure), вам необходимо это сделать, прежде чем выполнять аутентификацию. Это можно сделать с помощью [Azure Cloud Shell](https://shell.azure.com/bash), выполнив такую команду:
>```azurecli-interactive
>az provider register --namespace Microsoft.HDInsight
>```

Создайте субъект-службу, выбрав имя и выполнив такую команду:

```azurecli-interactive
az ad sp create-for-rbac --name <Service Principal Name> --sdk-auth
```

Сведения о субъекте-службе отображаются в виде JSON.

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
Скопируйте фрагмент кода ниже и задайте в качестве значений `TENANT_ID`, `CLIENT_ID`, `CLIENT_SECRET` и `SUBSCRIPTION_ID` строки из JSON-файла, возвращенного после выполнения команды для создания субъекта-службы.

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


## <a name="cluster-management"></a>Управление кластерами

> [!NOTE]
> В этом разделе предполагается, что вы уже выполнили аутентификацию, создали экземпляр `HDInsightManagementClientImpl` и сохранили его в переменной с именем `client`. Инструкции по выполнению аутентификации и получению `HDInsightManagementClientImpl` см. в предыдущем разделе.

### <a name="create-a-cluster"></a>Создание кластера

Кластер можно создать, вызвав `client.clusters().create()`.

#### <a name="example"></a>Пример

В этом примере показано, как создать кластер Spark с двумя головными узлами и одним рабочим.

> [!NOTE]
> Сначала необходимо создать группу ресурсов и учетную запись хранения, как описано далее. Если они уже созданы, следующие шаги можно пропустить.

##### <a name="creating-a-resource-group"></a>Создание группы ресурсов

Группу ресурсов можно создать с помощью [Azure Cloud Shell](https://shell.azure.com/bash), выполнив такую команду:
```azurecli-interactive
az group create -l <Region Name (i.e. eastus)> --n <Resource Group Name>
```
##### <a name="creating-a-storage-account"></a>Создание учетной записи хранения

Учетную запись хранения можно создать с помощью [Azure Cloud Shell](https://shell.azure.com/bash), выполнив такую команду:
```azurecli-interactive
az storage account create -n <Storage Account Name> -g <Existing Resource Group Name> -l <Region Name (i.e. eastus)> --sku <SKU i.e. Standard_LRS>
```
Теперь выполните такую команду, чтобы получить ключ для учетной записи хранения (он потребуется для создания кластера):
```azurecli-interactive
az storage account keys list -n <Storage Account Name>
```
---
Ниже показан фрагмент кода Java, который создает кластер Spark с двумя головными узлами и одним рабочим. Задайте переменные, как описано в комментариях, и при необходимости измените другие параметры.

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

### <a name="get-cluster-details"></a>Получение сведений о кластере

Чтобы получить сведения о свойствах кластера, выполните такую команду:

```java
client.clusters.getByResourceGroup("<Resource Group Name>", "<Cluster Name>");
```

#### <a name="example"></a>Пример

Чтобы убедиться в том, что вы создали кластер, можно использовать `get`.

```java
ClusterInner cluster = client.clusters().getByResourceGroup("<Resource Group Name>", "<Cluster Name>");
System.out.println(cluster.name()); //Prints the name of the cluster
System.out.println(cluster.id()); //Prints the resource Id of the cluster
```

Выходные данные должны выглядеть так:

```
<Cluster Name>
/subscriptions/XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX/resourceGroups/<Resource Group Name>/providers/Microsoft.HDInsight/clusters/<Cluster Name>
```

### <a name="list-clusters"></a>Получение списка кластеров

#### <a name="list-clusters-under-the-subscription"></a>Получение списка кластеров в пределах подписки

```java
client.clusters.list();
```
#### <a name="list-clusters-by-resource-group"></a>Получение списка кластеров в пределах в группы ресурсов

```java
client.clusters.listByResourceGroup("<Resource Group Name>");
```
> [!NOTE]
> Вызов `List()` и `ListByResourceGroup()` возвращает объект `PagedList<ClusterInner>`. Вызов `loadNext()` возвращает список кластеров на этой странице и перемещает объект `ClusterPaged` на следующую страницу. Действие можно повторять, пока `hasNextPage()` не примет значение `false`, указывающее на последнюю страницу.

#### <a name="example"></a>Пример

В следующем примере выводятся свойства всех кластеров в пределах текущей подписки:

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

### <a name="delete-a-cluster"></a>Удаление кластера

Чтобы удалить кластер, выполните такую команду:

```java
client.clusters.delete("<Resource Group Name>", "<Cluster Name>");
```

### <a name="update-cluster-tags"></a>Обновление тегов кластера

Вы можете обновить теги кластера так:

```java
client.clusters.update("<Resource Group Name>", "<Cluster Name>", <Map<String,String> of Tags>);
```

### <a name="resize-cluster"></a>Изменение размера кластера

Вы можете изменить размер кластера, изменяя количество его рабочих узлов. Укажите новый размер, как показано ниже:

```java
client.clusters.resize("<Resource Group Name>", "<Cluster Name>", <Num of Worker Nodes (int)>)
```

## <a name="cluster-monitoring"></a>Мониторинг кластера

Пакет Azure Management SDK для HDInsight также позволяет управлять мониторингом кластеров с помощью Operations Management Suite (OMS).

### <a name="enable-oms-monitoring"></a>Включение мониторинга OMS

> [!NOTE]
> Чтобы включить мониторинг OMS, требуется рабочая область Log Analytics. Если вы не создавали такую рабочую область, см. статью [Создание рабочей области Log Analytics на портале Azure](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-quick-create-workspace).

Чтобы включить мониторинг OMS в кластере, выполните такую команду:

```java
client.extensions().enableMonitoring("<Resource Group Name", "<Cluster Name>", new ClusterMonitoringRequest().withWorkspaceId("<Workspace Id>"));
```

### <a name="view-status-of-oms-monitoring"></a>Просмотр состояния мониторинга OMS

Чтобы узнать состояние мониторинга OMS в кластере, выполните такую команду:

```java
client.extensions().getMonitoringStatus("<Resource Group Name", "Cluster Name");
```

### <a name="disable-oms-monitoring"></a>Отключение мониторинга OMS

Чтобы отключить мониторинг OMS в кластере, выполните такую команду:

```java
client.extensions().disableMonitoring("<Resource Group Name>", "<Cluster Name>");
```

## <a name="script-actions"></a>Элемент "Действия скрипта"

В кластерах HDInsight поддерживается метод конфигурации с использованием, действий скриптов, который вызывает пользовательские скрипты для настройки кластера.
> [!NOTE]
> Дополнительные сведения о действиях скриптов см. в статье [Настройка кластеров HDInsight под управлением Linux с помощью действий сценариев](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux).

### <a name="execute-script-actions"></a>Выполнение действий скриптов

Вы можете выполнить действия скриптов в кластере так:

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

### <a name="delete-script-action"></a>Удаление действий скриптов

Чтобы удалить сохраненные действия скриптов в кластере, выполните такую команду:

```java
client.scriptActions().delete("<Resource Group Name>", "<Cluster Name>", "<Script Name>");
```

### <a name="list-persisted-script-actions"></a>Получение списка сохраненных действий скриптов

> [!NOTE]
> Метод `listByCluster()` возвращает объект `PagedList<RuntimeScriptActionDetailInner>`. Вызов `currentPage().items()` возвращает список `RuntimeScriptActionDetailInner`, а `loadNextPage()` выполняет переход к следующей странице. Действие можно повторять, пока `hasNextPage()` не примет значение `false`, указывающее на последнюю страницу.

Чтобы получить список всех сохраненных действий скриптов в кластере, выполните такую команду:
```java
client.scriptActions().listByCluster("<Resource Group Name>", "<Cluster Name>");
```

#### <a name="example"></a>Пример

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

### <a name="list-all-scripts-execution-history"></a>Просмотр журнала выполнения всех скриптов

Чтобы получить журнал выполнения всех скриптов в кластере, выполните такую команду:

```java
client.scriptExecutionHistorys().listByCluster("<Resource Group Name>", "<Cluster Name>");
```

#### <a name="example"></a>Пример

В этом примере выводятся сведения обо всех выполнявшихся скриптах.

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
