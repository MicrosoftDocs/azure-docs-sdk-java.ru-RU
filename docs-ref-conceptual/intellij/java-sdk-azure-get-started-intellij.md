---
title: Начало работы с Azure для Java с помощью Intellij
description: Базовое использование библиотек Azure для Java с вашей подпиской Azure.
keywords: Azure, Java, SDK, API, authenticate, get-started
services: ''
documentationcenter: java
author: roygara
manager: timlt
editor: ''
ms.assetid: ''
ms.author: v-rogara
ms.date: 02/01/2018
ms.devlang: java
ms.prod: azure
ms.service: multiple
ms.topic: get-started-article
ms.technology: azure
ms.openlocfilehash: 5c122b09d9d431ddcec667e61230eb53968c52e7
ms.sourcegitcommit: 720c2eaf66532d277015610ec375c71e934d9ee6
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/09/2018
ms.locfileid: "29065501"
---
# <a name="get-started-with-the-azure-libraries-using-intellij"></a>Начало работы с библиотеками Azure с помощью Intellij

В этом руководстве описано, как настроить среду разработки и использовать библиотеки Azure для Java. Вы создадите субъект-службу для аутентификации в Azure и выполните пример кода, который создает и использует ресурсы Azure в вашей подписке. Использование Intellij является необязательным при разработке приложений Java в Azure. Подходит любая среда IDE с интегрированным компонентом Maven. Кроме того, можно выполнять код из командной строки с помощью Maven, если вы предпочитаете не использовать IDE.

## <a name="prerequisites"></a>предварительным требованиям

- Учетная запись Azure. Если у вас ее нет, [получите бесплатную пробную версию](https://azure.microsoft.com/free/).
- [Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/quickstart) или [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2).
- Последняя стабильная версия [Intellij](https://www.jetbrains.com/idea/).

## <a name="set-up-authentication"></a>Настройка проверки подлинности

Чтобы выполнить пример кода из этого руководства, предоставьте приложению Java в вашей подписке Azure разрешения на чтение и создание. Создайте субъект-службу и настройте приложение для выполнения со связанными учетными данными. Субъект-служба помогает создать неинтерактивную учетную запись, связанную с вашим идентификатором. Этой учетной записи предоставляются только разрешения, необходимые для запуска приложения.

[Создайте субъект-службу](/cli/azure/create-an-azure-service-principal-azure-cli), чтобы предоставить коду разрешение на создание и обновление ресурсов в вашей подписке без непосредственного использования учетных данных. Запишите выходные данные. Вместо `MY_SECURE_PASSWORD` в аргументе пароля нужно указать [безопасный пароль](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-policy). Пароль должен содержать 8–16 символов и соответствовать хотя бы трем из четырех следующих критериев:

* наличие строчных букв;
* наличие прописных букв;
* наличие цифр;
* наличие одного из следующих символов: @ # $ % ^ & * - _ ! + = [ ] { } | \ : ‘ , . ? / ` ~ “ ( ) ;


```azurecli-interactive
az ad sp create-for-rbac --name AzureJavaTest --password "MY_SECURE_PASSWORD"
```

Вы получите ответ в следующем формате:

```json
{
  "appId": "a487e0c1-82af-47d9-9a0b-af184eb87646d",
  "displayName": "AzureJavaTest",
  "name": "http://AzureJavaTest",
  "password": password,
  "tenant": "tttttttt-tttt-tttt-tttt-tttttttttttt"
}
```

Затем скопируйте следующий код в текстовый файл в системе:

```text
# sample management library properties file
subscription=ssssssss-ssss-ssss-ssss-ssssssssssss
client=cccccccc-cccc-cccc-cccc-cccccccccccc
key=kkkkkkkkkkkkkkkk
tenant=tttttttt-tttt-tttt-tttt-tttttttttttt
managementURI=https\://management.core.windows.net/
baseURL=https\://management.azure.com/
authURL=https\://login.windows.net/
graphURL=https\://graph.windows.net/
```

Замените первые четыре значения следующим кодом:

- subscription — используйте значение *id* из `az account show` в Azure CLI 2.0.
- client — используйте значение *appId* из выходных данных субъекта-службы.
- key — используйте значение *password* из выходных данных субъекта-службы.
- tenant — используйте значение *tenant* из выходных данных субъекта-службы.

Сохраните этот файл в безопасном расположении в вашей системе, доступном для кода. Вы можете использовать этот файл для будущего кода, поэтому рекомендуется сохранить его где-либо за пределами используемого в этой статье приложения. 

Задайте переменную среды `AZURE_AUTH_LOCATION` и укажите полный путь к файлу аутентификации в оболочке.  

```bash
export AZURE_AUTH_LOCATION=/Users/raisa/azureauth.properties
```

Если вы работаете в среде Windows, добавьте переменную в свойства системы. Откройте окно PowerShell с правами администратора. Замените вторую переменную путем к файлу и введите следующую команду:

```powershell
setx AZURE_AUTH_LOCATION "C:\<fullpath>\azureauth.properties" /m
```

## <a name="create-a-new-maven-project"></a>Создание нового проекта Maven

> [!NOTE]
> В этом руководстве пример кода создается и запускается с помощью средства сборки Maven. Но с библиотеками Azure для Java можно использовать и другие инструменты, например Gradle. 

Откройте Intellij, выберите "File" > "New" > "Project..." (Файл > Создать > Проект...). Перейдите к следующему экрану.

Введите com.fabrikam для groupID и произвольное значение для artifactID.

Перейдите к последнему экрану и завершите создание проекта.

Откройте файл pom.xml. Добавьте следующий код:

```XML
<dependencies>
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure</artifactId>
    <version>1.3.0</version>
</dependency>
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-storage</artifactId>
    <version>5.0.0</version>
</dependency>
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>6.2.1.jre8</version>
</dependency>
</dependencies>
```

Сохраните файл pom.xml.
   
## <a name="install-the-azure-toolkit-for-intellij"></a>Установка набора средств Azure для IntelliJ

[Набор средств Azure](azure-toolkit-for-intellij-installation.md) требуется, если вы развертываете веб-приложения и API-интерфейсы программными средствами. Сейчас этот набор не используется для разработки других типов. Ниже приведены общие сведения о действиях по установке. См. дополнительные сведения об [установке набора средств Azure для IntelliJ](azure-toolkit-for-intellij-installation.md).

В меню **Файл** выберите **Параметры**. 

Выберите **Обзор репозиториев...** найдите "Azure" и установите **набор средств Azure для Intellij**.

Перезапустите Intellij.

## <a name="create-a-linux-virtual-machine"></a>Создание виртуальной машины Linux

Создайте файл с именем `AzureApp.java` в каталоге проекта `src/main/java` и вставьте следующий блок кода. Обновите переменные `userName` и `sshKey`, указав реальные значения для своего компьютера. Код создает виртуальную машину Linux с именем `testLinuxVM` в группе ресурсов `sampleResourceGroup`, которая выполняется в регионе Azure "Восточная часть США".

Чтобы создать `sshkey`, откройте Cloud Shell и введите `ssh-keygen -t rsa -b 2048`. Введите имя файла, извлеките из файла с расширением .public ключ, который используется в следующем коде, а затем скопируйте и вставьте его в переменную `sshKey`.

```java

import com.microsoft.azure.management.Azure;
import com.microsoft.azure.management.compute.VirtualMachine;
import com.microsoft.azure.management.compute.KnownLinuxVirtualMachineImage;
import com.microsoft.azure.management.compute.VirtualMachineSizeTypes;
import com.microsoft.azure.management.appservice.PricingTier;
import com.microsoft.azure.management.appservice.WebApp;
import com.microsoft.azure.management.storage.StorageAccount;
import com.microsoft.azure.management.storage.SkuName;
import com.microsoft.azure.management.storage.StorageAccountKey;
import com.microsoft.azure.management.sql.SqlDatabase;
import com.microsoft.azure.management.sql.SqlServer;
import com.microsoft.azure.management.resources.fluentcore.arm.Region;
import com.microsoft.azure.management.resources.fluentcore.utils.SdkContext;

import com.microsoft.rest.LogLevel;

import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.blob.*;

import java.io.File;
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.Statement;
import java.util.List;

public class AzureApp {

    public static void main(String[] args) {

        final String userName = "YOUR_VM_USERNAME";
        final String sshKey = "YOUR_PUBLIC_SSH_KEY";

        try {

            // use the properties file with the service principal information to authenticate
            // change the name of the environment variable if you used a different name in the previous step
            final File credFile = new File(System.getenv("AZURE_AUTH_LOCATION"));    
            Azure azure = Azure.configure()
                    .withLogLevel(LogLevel.BASIC)
                    .authenticate(credFile)
                    .withDefaultSubscription();
           
            // create a Ubuntu virtual machine in a new resource group 
            VirtualMachine linuxVM = azure.virtualMachines().define("testLinuxVM")
                    .withRegion(Region.US_EAST)
                    .withNewResourceGroup("sampleVmResourceGroup")
                    .withNewPrimaryNetwork("10.0.0.0/24")
                    .withPrimaryPrivateIPAddressDynamic()
                    .withoutPrimaryPublicIPAddress()
                    .withPopularLinuxImage(KnownLinuxVirtualMachineImage.UBUNTU_SERVER_16_04_LTS)
                    .withRootUsername(userName)
                    .withSsh(sshKey)
                    .withUnmanagedDisks()
                    .withSize(VirtualMachineSizeTypes.STANDARD_D3_V2)
                    .create();   

        } catch (Exception e) {
            System.out.println(e.getMessage());
            e.printStackTrace();
        }
    }
}
```


В консоли отображаются некоторые запросы и ответы REST по мере того, как пакет SDK выполняет базовые вызовы Azure REST API, чтобы настроить виртуальную машину и ее ресурсы. Когда программа завершит работу, проверьте виртуальную машину в подписке с помощью Azure CLI 2.0:

```azurecli-interactive
az vm list --resource-group sampleVmResourceGroup
```

Проверив, что код работает, используйте CLI, чтобы удалить виртуальную машину и ее ресурсы.

```azurecli-interactive
az group delete --name sampleVmResourceGroup
```

## <a name="deploy-a-web-app-from-a-github-repo"></a>Развертывание веб-приложения из репозитория GitHub

Перед выполнением кода замените основной метод в `AzureApp.java` одним из указанных ниже, задав для переменной `appName` уникальное значение. Этот код развертывает веб-приложение из ветви `master` в общедоступном репозитории GitHub в новое [веб-приложение службы приложений Azure](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) ценовой категории "Бесплатный".

```java
    public static void main(String[] args) {
        try {

            final File credFile = new File(System.getenv("AZURE_AUTH_LOCATION"));
            final String appName = "YOUR_APP_NAME";

            Azure azure = Azure.configure()
                    .withLogLevel(LogLevel.BASIC)
                    .authenticate(credFile)
                    .withDefaultSubscription();

            WebApp app = azure.webApps().define(appName)
                    .withRegion(Region.US_WEST2)
                    .withNewResourceGroup("sampleWebResourceGroup")
                    .withNewWindowsPlan(PricingTier.FREE_F1)
                    .defineSourceControl()
                    .withPublicGitRepository(
                            "https://github.com/Azure-Samples/app-service-web-java-get-started")
                    .withBranch("master")
                    .attach()
                    .create();

        } catch (Exception e) {
            System.out.println(e.getMessage());
            e.printStackTrace();
        }
    }
```

Перед использованием Maven выполните следующий код:

Откройте браузер и укажите приложение в CLI:

```azurecli-interactive
az appservice web browse --resource-group sampleWebResourceGroup --name YOUR_APP_NAME
```
Проверив развертывание, удалите веб-приложение и план из подписки.

```azurecli-interactive
az group delete --name sampleWebResourceGroup
```

## <a name="connect-to-an-azure-sql-database"></a>Подключение к базе данных SQL Azure

Замените текущий основной метод в `AzureApp.java` кодом ниже, задав реальное значение для переменной `dbPassword`.
Этот код создает новую базу данных SQL с правилом брандмауэра, разрешающим удаленный доступ, и подключается к ней с помощью драйвера JBDC базы данных SQL. 

```java

    public static void main(String args[])
    {
        // create the db using the management libraries
        try {
            final File credFile = new File(System.getenv("AZURE_AUTH_LOCATION"));
            Azure azure = Azure.configure()
                    .withLogLevel(LogLevel.BASIC)
                    .authenticate(credFile)
                    .withDefaultSubscription();

            final String adminUser = SdkContext.randomResourceName("db",8);
            final String sqlServerName = SdkContext.randomResourceName("sql",10);
            final String sqlDbName = SdkContext.randomResourceName("dbname",8);
            final String dbPassword = "YOUR_PASSWORD_HERE";


            SqlServer sampleSQLServer = azure.sqlServers().define(sqlServerName)
                            .withRegion(Region.US_EAST)
                            .withNewResourceGroup("sampleSqlResourceGroup")
                            .withAdministratorLogin(adminUser)
                            .withAdministratorPassword(dbPassword)
                            .withNewFirewallRule("0.0.0.0","255.255.255.255")
                            .create();

            SqlDatabase sampleSQLDb = sampleSQLServer.databases().define(sqlDbName).create();

            // assemble the connection string to the database
            final String domain = sampleSQLServer.fullyQualifiedDomainName();
            String url = "jdbc:sqlserver://"+ domain + ":1433;" +
                    "database=" + sqlDbName +";" +
                    "user=" + adminUser+ "@" + sqlServerName + ";" +
                    "password=" + dbPassword + ";" +
                    "encrypt=true;trustServerCertificate=false;hostNameInCertificate=*.database.windows.net;loginTimeout=30;";

            // connect to the database, create a table and insert a entry into it
            Connection conn = DriverManager.getConnection(url);

            String createTable = "CREATE TABLE CLOUD ( name varchar(255), code int);";
            String insertValues = "INSERT INTO CLOUD (name, code ) VALUES ('Azure', 1);";
            String selectValues = "SELECT * FROM CLOUD";
            Statement createStatement = conn.createStatement();
            createStatement.execute(createTable);
            Statement insertStatement = conn.createStatement();
            insertStatement.execute(insertValues);
            Statement selectStatement = conn.createStatement();
            ResultSet rst = selectStatement.executeQuery(selectValues);

            while (rst.next()) {
                System.out.println(rst.getString(1) + " "
                        + rst.getString(2));
            }


        } catch (Exception e) {
            System.out.println(e.getMessage());
            System.out.println(e.getStackTrace().toString());
        }
    }
```
Запустите пример из командной строки:

```
mvn clean compile exec:java
```

Затем удалите ресурсы с помощью CLI:

```azurecli-interactive
az group delete --name sampleSqlResourceGroup
```

## <a name="write-a-blob-into-a-new-storage-account"></a>Запись большого двоичного объекта в новую учетную запись хранения

Замените текущий основной метод в `AzureApp.java` следующим кодом. Этот код создает [учетную запись хранения Azure](https://docs.microsoft.com/azure/storage/storage-introduction), а затем использует библиотеки хранилища Azure для Java, чтобы создать текстовый файл в облаке.

```java
public static void main(String[] args) {

    try {

        // use the properties file with the service principal information to authenticate
        // change the name of the environment variable if you used a different name in the previous step
        final File credFile = new File(System.getenv("AZURE_AUTH_LOCATION"));
        Azure azure = Azure.configure()
                .withLogLevel(LogLevel.BASIC)
                .authenticate(credFile)
                .withDefaultSubscription();

        // create a new storage account
        String storageAccountName = SdkContext.randomResourceName("st",8);
        StorageAccount storage = azure.storageAccounts().define(storageAccountName)
                    .withRegion(Region.US_WEST2)
                    .withNewResourceGroup("sampleStorageResourceGroup")
                    .create();

        // create a storage container to hold the file
        List<StorageAccountKey> keys = storage.getKeys();
        final String storageConnection = "DefaultEndpointsProtocol=https;"
                + "AccountName=" + storage.name()
                + ";AccountKey=" + keys.get(0).value()
                + ";EndpointSuffix=core.windows.net";

        CloudStorageAccount account = CloudStorageAccount.parse(storageConnection);
        CloudBlobClient serviceClient = account.createCloudBlobClient();

        // Container name must be lower case.
        CloudBlobContainer container = serviceClient.getContainerReference("helloazure");
        container.createIfNotExists();

        // Make the container public
        BlobContainerPermissions containerPermissions = new BlobContainerPermissions();
        containerPermissions.setPublicAccess(BlobContainerPublicAccessType.CONTAINER);
        container.uploadPermissions(containerPermissions);

        // write a blob to the container
        CloudBlockBlob blob = container.getBlockBlobReference("helloazure.txt");
        blob.uploadText("hello Azure");

    } catch (Exception e) {
        System.out.println(e.getMessage());
        e.printStackTrace();
    }
    }
}
```

Запустите пример из командной строки:

Перейти к файлу `helloazure.txt` в вашей учетной записи хранения можно с помощью портала Azure или [обозревателя хранилищ Azure](https://docs.microsoft.com/azure/vs-azure-tools-storage-explorer-blobs).

Удалите учетную запись хранилища с помощью CLI:

```azurecli-interactive
az group delete --name sampleStorageResourceGroup
```

## <a name="explore-more-samples"></a>Другие примеры

Дополнительные сведения о том, как использовать библиотеки управления Azure для Java, чтобы управлять ресурсами и автоматизировать задачи, см. в наших примерах кода для [виртуальных машин](../java-sdk-azure-virtual-machine-samples.md), [веб-приложений](../java-sdk-azure-web-apps-samples.md) и [базы данных SQL](../java-sdk-azure-sql-database-samples.md).

## <a name="reference-and-release-notes"></a>Ссылки и заметки о выпуске

[Ссылки](http://docs.microsoft.com/java/api) доступны для всех пакетов.

## <a name="get-help-and-give-feedback"></a>Справка и отзывы

Задавайте вопросы сообществу на сайте [Stack Overflow](http://stackoverflow.com/questions/tagged/azure+java). Сообщайте об ошибках и нерешенных проблемах с библиотеками Azure для Java на странице [проектов GitHub](https://github.com/Azure/azure-sdk-for-java).
