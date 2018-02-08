---
title: "Начало работы с Azure для Java с помощью Intellij"
description: "Базовое использование библиотек Azure для Java с вашей подпиской Azure."
keywords: Azure, Java, SDK, API, authenticate, get-started
services: 
documentationcenter: java
author: roygara
manager: timlt
editor: 
ms.assetid: 
ms.author: v-rogara
ms.date: 02/01/2018
ms.devlang: java
ms.prod: azure
ms.service: multiple
ms.topic: get-started-article
ms.technology: azure
ms.openlocfilehash: 0a059366f7cdc139dcb5a8e7e9ca78254384d19e
ms.sourcegitcommit: 151aaa6ccc64d94ed67f03e846bab953bde15b4a
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/03/2018
---
# <a name="get-started-with-the-azure-libraries-using-intellij"></a><span data-ttu-id="c74b2-104">Начало работы с библиотеками Azure с помощью Intellij</span><span class="sxs-lookup"><span data-stu-id="c74b2-104">Get started with the Azure libraries using Intellij</span></span>

<span data-ttu-id="c74b2-105">В этом руководстве описано, как настроить среду разработки и использовать библиотеки Azure для Java.</span><span class="sxs-lookup"><span data-stu-id="c74b2-105">This guide walks you through setting up a development environment and using the Azure libraries for Java.</span></span> <span data-ttu-id="c74b2-106">Вы создадите субъект-службу для аутентификации в Azure и выполните пример кода, который создает и использует ресурсы Azure в вашей подписке.</span><span class="sxs-lookup"><span data-stu-id="c74b2-106">You'll create a service principal to authenticate with Azure and run some sample code that creates and uses Azure resources in your subscription.</span></span> <span data-ttu-id="c74b2-107">Использование Intellij является необязательным при разработке приложений Java в Azure.</span><span class="sxs-lookup"><span data-stu-id="c74b2-107">Using Intellij is optional for Java development with Azure.</span></span> <span data-ttu-id="c74b2-108">Подходит любая среда IDE с интегрированным компонентом Maven.</span><span class="sxs-lookup"><span data-stu-id="c74b2-108">Any IDE that has Maven integration works.</span></span> <span data-ttu-id="c74b2-109">Кроме того, можно выполнять код из командной строки с помощью Maven, если вы предпочитаете не использовать IDE.</span><span class="sxs-lookup"><span data-stu-id="c74b2-109">Alternatively, you can run your code from the commandline using Maven if you prefer not to use any IDE.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c74b2-110">предварительным требованиям</span><span class="sxs-lookup"><span data-stu-id="c74b2-110">Prerequisites</span></span>

- <span data-ttu-id="c74b2-111">Учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="c74b2-111">An Azure account.</span></span> <span data-ttu-id="c74b2-112">Если у вас ее нет, [получите бесплатную пробную версию](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="c74b2-112">If you don't have one, [get a free trial](https://azure.microsoft.com/free/)</span></span>
- <span data-ttu-id="c74b2-113">[Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/quickstart) или [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="c74b2-113">[Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/quickstart) or [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2).</span></span>
- <span data-ttu-id="c74b2-114">Последняя стабильная версия [Intellij](https://www.jetbrains.com/idea/).</span><span class="sxs-lookup"><span data-stu-id="c74b2-114">The latest stable version of [Intellij](https://www.jetbrains.com/idea/)</span></span>

## <a name="set-up-authentication"></a><span data-ttu-id="c74b2-115">Настройка проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="c74b2-115">Set up authentication</span></span>

<span data-ttu-id="c74b2-116">Чтобы выполнить пример кода из этого руководства, предоставьте приложению Java в вашей подписке Azure разрешения на чтение и создание.</span><span class="sxs-lookup"><span data-stu-id="c74b2-116">Your Java application needs read and create permissions in your Azure subscription to run the sample code in this tutorial.</span></span> <span data-ttu-id="c74b2-117">Создайте субъект-службу и настройте приложение для выполнения со связанными учетными данными.</span><span class="sxs-lookup"><span data-stu-id="c74b2-117">Create a service principal and configure your application to run with its credentials.</span></span> <span data-ttu-id="c74b2-118">Субъект-служба помогает создать неинтерактивную учетную запись, связанную с вашим идентификатором. Этой учетной записи предоставляются только разрешения, необходимые для запуска приложения.</span><span class="sxs-lookup"><span data-stu-id="c74b2-118">Service principals provide a way to create a non-interactive account associated with your identity to which you grant only the privileges your app needs to run.</span></span>

<span data-ttu-id="c74b2-119">[Создайте субъект-службу](/cli/azure/create-an-azure-service-principal-azure-cli), чтобы предоставить коду разрешение на создание и обновление ресурсов в вашей подписке без непосредственного использования учетных данных.</span><span class="sxs-lookup"><span data-stu-id="c74b2-119">[Create a service principal](/cli/azure/create-an-azure-service-principal-azure-cli) to grant your code permission to create and update resources in your subscription without using your account credentials directly.</span></span> <span data-ttu-id="c74b2-120">Запишите выходные данные.</span><span class="sxs-lookup"><span data-stu-id="c74b2-120">Make sure to capture the output.</span></span> <span data-ttu-id="c74b2-121">Вместо `MY_SECURE_PASSWORD` в аргументе пароля нужно указать [безопасный пароль](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-policy).</span><span class="sxs-lookup"><span data-stu-id="c74b2-121">Provide a [secure password](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-policy) in the password argument instead of `MY_SECURE_PASSWORD`.</span></span> <span data-ttu-id="c74b2-122">Пароль должен содержать 8–16 символов и соответствовать хотя бы трем из четырех следующих критериев:</span><span class="sxs-lookup"><span data-stu-id="c74b2-122">Your password must be 8 to 16 characters and match at least 3 out of the 4 following criteria:</span></span>

* <span data-ttu-id="c74b2-123">наличие строчных букв;</span><span class="sxs-lookup"><span data-stu-id="c74b2-123">Include lowercase characters</span></span>
* <span data-ttu-id="c74b2-124">наличие прописных букв;</span><span class="sxs-lookup"><span data-stu-id="c74b2-124">Include uppercase characters</span></span>
* <span data-ttu-id="c74b2-125">наличие цифр;</span><span class="sxs-lookup"><span data-stu-id="c74b2-125">Include numbers</span></span>
* <span data-ttu-id="c74b2-126">наличие одного из следующих символов: @ # $ % ^ & \* - _ !</span><span class="sxs-lookup"><span data-stu-id="c74b2-126">Include one of the following symbols: @ # $ % ^ & \* - _ !</span></span> <span data-ttu-id="c74b2-127">+ = [ ] { } | \ : ‘ , .</span><span class="sxs-lookup"><span data-stu-id="c74b2-127">+ = [ ] { } | \ : ‘ , .</span></span> <span data-ttu-id="c74b2-128">?</span><span class="sxs-lookup"><span data-stu-id="c74b2-128">?</span></span> <span data-ttu-id="c74b2-129">/ \` ~ “ ( ) ;</span><span class="sxs-lookup"><span data-stu-id="c74b2-129">/ \` ~ “ ( ) ;</span></span>


```azurecli-interactive
az ad sp create-for-rbac --name AzureJavaTest --password "MY_SECURE_PASSWORD"
```

<span data-ttu-id="c74b2-130">Вы получите ответ в следующем формате:</span><span class="sxs-lookup"><span data-stu-id="c74b2-130">Which gives you a reply in the following format:</span></span>

```json
{
  "appId": "a487e0c1-82af-47d9-9a0b-af184eb87646d",
  "displayName": "AzureJavaTest",
  "name": "http://AzureJavaTest",
  "password": password,
  "tenant": "tttttttt-tttt-tttt-tttt-tttttttttttt"
}
```

<span data-ttu-id="c74b2-131">Затем скопируйте следующий код в текстовый файл в системе:</span><span class="sxs-lookup"><span data-stu-id="c74b2-131">Next, copy the following into a text file on your system:</span></span>

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

<span data-ttu-id="c74b2-132">Замените первые четыре значения следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="c74b2-132">Replace the top four values with the following:</span></span>

- <span data-ttu-id="c74b2-133">subscription — используйте значение *id* из `az account show` в Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="c74b2-133">subscription: use the *id* value from `az account show` in the Azure CLI 2.0.</span></span>
- <span data-ttu-id="c74b2-134">client — используйте значение *appId* из выходных данных субъекта-службы.</span><span class="sxs-lookup"><span data-stu-id="c74b2-134">client: use the *appId* value from the output taken from a service principal output.</span></span>
- <span data-ttu-id="c74b2-135">key — используйте значение *password* из выходных данных субъекта-службы.</span><span class="sxs-lookup"><span data-stu-id="c74b2-135">key: use the *password* value from the service principal output.</span></span>
- <span data-ttu-id="c74b2-136">tenant — используйте значение *tenant* из выходных данных субъекта-службы.</span><span class="sxs-lookup"><span data-stu-id="c74b2-136">tenant: use the *tenant* value from the service principal output.</span></span>

<span data-ttu-id="c74b2-137">Сохраните этот файл в безопасном расположении в вашей системе, доступном для кода.</span><span class="sxs-lookup"><span data-stu-id="c74b2-137">Save this file in a secure location on your system where your code can read it.</span></span> <span data-ttu-id="c74b2-138">Вы можете использовать этот файл для будущего кода, поэтому рекомендуется сохранить его где-либо за пределами используемого в этой статье приложения.</span><span class="sxs-lookup"><span data-stu-id="c74b2-138">You may use this file for future code so it's recommended to store it somewhere external to the application in this article.</span></span> 

<span data-ttu-id="c74b2-139">Задайте переменную среды `AZURE_AUTH_LOCATION` и укажите полный путь к файлу аутентификации в оболочке.</span><span class="sxs-lookup"><span data-stu-id="c74b2-139">Set an environment variable `AZURE_AUTH_LOCATION` with the full path to the authentication file in your shell.</span></span>  

```bash
export AZURE_AUTH_LOCATION=/Users/raisa/azureauth.properties
```

<span data-ttu-id="c74b2-140">Если вы работаете в среде Windows, добавьте переменную в свойства системы.</span><span class="sxs-lookup"><span data-stu-id="c74b2-140">If you're working in a windows environment, add the variable to your system properties.</span></span> <span data-ttu-id="c74b2-141">В PowerShell замените вторую переменную путем к файлу и введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="c74b2-141">Open PowerShell and, after replacing the second variable with the path to your file, enter the following command:</span></span>

```powershell
[Environment]::SetEnvironmentVariable("AZURE_AUTH_LOCATION", "C:\<fullpath>\azureauth.properties", "Machine")
```

## <a name="create-a-new-maven-project"></a><span data-ttu-id="c74b2-142">Создание нового проекта Maven</span><span class="sxs-lookup"><span data-stu-id="c74b2-142">Create a new Maven project</span></span>

> [!NOTE]
> <span data-ttu-id="c74b2-143">В этом руководстве пример кода создается и запускается с помощью средства сборки Maven. Но с библиотеками Azure для Java можно использовать и другие инструменты, например Gradle.</span><span class="sxs-lookup"><span data-stu-id="c74b2-143">This guide uses Maven build tool to build and run the sample code, but other build tools such as Gradle also work with the Azure libraries for Java.</span></span> 

<span data-ttu-id="c74b2-144">Откройте Intellij, выберите "File" > "New" > "Project..." (Файл > Создать > Проект...). Перейдите к следующему экрану.</span><span class="sxs-lookup"><span data-stu-id="c74b2-144">Open Intellij, select File > New > Project... Then proceed to the next screen.</span></span>

<span data-ttu-id="c74b2-145">Введите com.fabrikam для groupID и произвольное значение для artifactID.</span><span class="sxs-lookup"><span data-stu-id="c74b2-145">Enter "com.fabrikam" for the groupID and enter an artifactID of your choice.</span></span>

<span data-ttu-id="c74b2-146">Перейдите к последнему экрану и завершите создание проекта.</span><span class="sxs-lookup"><span data-stu-id="c74b2-146">Proceed to the final screen and finish creating the project.</span></span>

<span data-ttu-id="c74b2-147">Откройте файл pom.xml.</span><span class="sxs-lookup"><span data-stu-id="c74b2-147">Now, open the pom.xml file.</span></span> <span data-ttu-id="c74b2-148">Добавьте следующий код:</span><span class="sxs-lookup"><span data-stu-id="c74b2-148">And add the following code:</span></span>

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

<span data-ttu-id="c74b2-149">Сохраните файл pom.xml.</span><span class="sxs-lookup"><span data-stu-id="c74b2-149">Save the pom.xml.</span></span>
   
## <a name="install-the-azure-toolkit-for-intellij"></a><span data-ttu-id="c74b2-150">Установка набора средств Azure для IntelliJ</span><span class="sxs-lookup"><span data-stu-id="c74b2-150">Install the azure toolkit for Intellij</span></span>

<span data-ttu-id="c74b2-151">[Набор средств Azure](azure-toolkit-for-intellij-installation.md) требуется, если вы развертываете веб-приложения и API-интерфейсы программными средствами. Сейчас этот набор не используется для разработки других типов.</span><span class="sxs-lookup"><span data-stu-id="c74b2-151">The [Azure toolkit](azure-toolkit-for-intellij-installation.md) is necessary if you're going to be deploying web apps or APIs programmatically but is not currently used for any other kinds of development.</span></span> <span data-ttu-id="c74b2-152">Ниже приведены общие сведения о действиях по установке.</span><span class="sxs-lookup"><span data-stu-id="c74b2-152">The following is a summary of the installation process.</span></span> <span data-ttu-id="c74b2-153">См. дополнительные сведения об [установке набора средств Azure для IntelliJ](azure-toolkit-for-intellij-installation.md).</span><span class="sxs-lookup"><span data-stu-id="c74b2-153">For detailed stpes, visit [Installing the Azure Toolkit for IntelliJ](azure-toolkit-for-intellij-installation.md).</span></span>

<span data-ttu-id="c74b2-154">В меню **Файл** выберите **Параметры**.</span><span class="sxs-lookup"><span data-stu-id="c74b2-154">Select the **File** menu and then select **Settings...**.</span></span> 

<span data-ttu-id="c74b2-155">Выберите **Обзор репозиториев...** найдите "Azure" и установите **набор средств Azure для Intellij**.</span><span class="sxs-lookup"><span data-stu-id="c74b2-155">Select **Browse repositories...** and then search "Azure" and install the **Azure toolkit for Intellij**.</span></span>

<span data-ttu-id="c74b2-156">Перезапустите Intellij.</span><span class="sxs-lookup"><span data-stu-id="c74b2-156">Restart Intellij.</span></span>

## <a name="create-a-linux-virtual-machine"></a><span data-ttu-id="c74b2-157">Создание виртуальной машины Linux</span><span class="sxs-lookup"><span data-stu-id="c74b2-157">Create a Linux virtual machine</span></span>

<span data-ttu-id="c74b2-158">Создайте файл с именем `AzureApp.java` в каталоге проекта `src/main/java` и вставьте следующий блок кода.</span><span class="sxs-lookup"><span data-stu-id="c74b2-158">Create a new file named `AzureApp.java` in the project's `src/main/java` directory and paste in the following block of code.</span></span> <span data-ttu-id="c74b2-159">Обновите переменные `userName` и `sshKey`, указав реальные значения для своего компьютера.</span><span class="sxs-lookup"><span data-stu-id="c74b2-159">Update the `userName` and `sshKey` variables with real values for your machine.</span></span> <span data-ttu-id="c74b2-160">Код создает виртуальную машину Linux с именем `testLinuxVM` в группе ресурсов `sampleResourceGroup`, которая выполняется в регионе Azure "Восточная часть США".</span><span class="sxs-lookup"><span data-stu-id="c74b2-160">The code creates a new Linux VM with name `testLinuxVM` in a resource group `sampleResourceGroup` running in the US East Azure region.</span></span>

<span data-ttu-id="c74b2-161">Чтобы создать `sshkey`, откройте Cloud Shell и введите `ssh-keygen -t rsa -b 2048`.</span><span class="sxs-lookup"><span data-stu-id="c74b2-161">In order to create an `sshkey`, open the azure cloud shell and enter `ssh-keygen -t rsa -b 2048`.</span></span> <span data-ttu-id="c74b2-162">Введите имя файла, извлеките из файла с расширением .public ключ, который используется в следующем коде, а затем скопируйте и вставьте его в переменную `sshKey`.</span><span class="sxs-lookup"><span data-stu-id="c74b2-162">Enter a name for your file and then access the .public file to get the key, which you use in the following code, copy and paste it all into your variable `sshKey`.</span></span>

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


<span data-ttu-id="c74b2-163">В консоли отображаются некоторые запросы и ответы REST по мере того, как пакет SDK выполняет базовые вызовы Azure REST API, чтобы настроить виртуальную машину и ее ресурсы.</span><span class="sxs-lookup"><span data-stu-id="c74b2-163">You'll see some REST requests and responses in the console as the SDK makes the underlying calls to the Azure REST API to configure the virtual machine and its resources.</span></span> <span data-ttu-id="c74b2-164">Когда программа завершит работу, проверьте виртуальную машину в подписке с помощью Azure CLI 2.0:</span><span class="sxs-lookup"><span data-stu-id="c74b2-164">When the program finishes, verify the virtual machine in your subscription with the Azure CLI 2.0:</span></span>

```azurecli-interactive
az vm list --resource-group sampleVmResourceGroup
```

<span data-ttu-id="c74b2-165">Проверив, что код работает, используйте CLI, чтобы удалить виртуальную машину и ее ресурсы.</span><span class="sxs-lookup"><span data-stu-id="c74b2-165">Once you've verified that the code worked, use the CLI to delete the VM and its resources.</span></span>

```azurecli-interactive
az group delete --name sampleVmResourceGroup
```

## <a name="deploy-a-web-app-from-a-github-repo"></a><span data-ttu-id="c74b2-166">Развертывание веб-приложения из репозитория GitHub</span><span class="sxs-lookup"><span data-stu-id="c74b2-166">Deploy a web app from a GitHub repo</span></span>

<span data-ttu-id="c74b2-167">Перед выполнением кода замените основной метод в `AzureApp.java` одним из указанных ниже, задав для переменной `appName` уникальное значение.</span><span class="sxs-lookup"><span data-stu-id="c74b2-167">Replace the main method in `AzureApp.java` with the one below, updating the `appName` variable to a unique value before running the code.</span></span> <span data-ttu-id="c74b2-168">Этот код развертывает веб-приложение из ветви `master` в общедоступном репозитории GitHub в новое [веб-приложение службы приложений Azure](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) ценовой категории "Бесплатный".</span><span class="sxs-lookup"><span data-stu-id="c74b2-168">This code deploys a web application from the `master` branch in a public GitHub repo into a new [Azure App Service Web App](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) running in the free pricing tier.</span></span>

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

<span data-ttu-id="c74b2-169">Перед использованием Maven выполните следующий код:</span><span class="sxs-lookup"><span data-stu-id="c74b2-169">Run the code as before using Maven:</span></span>

<span data-ttu-id="c74b2-170">Откройте браузер и укажите приложение в CLI:</span><span class="sxs-lookup"><span data-stu-id="c74b2-170">Open a browser pointed to the application using the CLI:</span></span>

```azurecli-interactive
az appservice web browse --resource-group sampleWebResourceGroup --name YOUR_APP_NAME
```
<span data-ttu-id="c74b2-171">Проверив развертывание, удалите веб-приложение и план из подписки.</span><span class="sxs-lookup"><span data-stu-id="c74b2-171">Remove the web app and plan from your subscription once you've verified the deployment.</span></span>

```azurecli-interactive
az group delete --name sampleWebResourceGroup
```

## <a name="connect-to-an-azure-sql-database"></a><span data-ttu-id="c74b2-172">Подключение к базе данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="c74b2-172">Connect to an Azure SQL database</span></span>

<span data-ttu-id="c74b2-173">Замените текущий основной метод в `AzureApp.java` кодом ниже, задав реальное значение для переменной `dbPassword`.</span><span class="sxs-lookup"><span data-stu-id="c74b2-173">Replace the current main method in `AzureApp.java` with the code below, setting a real value for the `dbPassword` variable.</span></span>
<span data-ttu-id="c74b2-174">Этот код создает новую базу данных SQL с правилом брандмауэра, разрешающим удаленный доступ, и подключается к ней с помощью драйвера JBDC базы данных SQL.</span><span class="sxs-lookup"><span data-stu-id="c74b2-174">This code creates a new SQL database with a firewall rule allowing remote access,  and then connects to it using the SQL Database JBDC driver.</span></span> 

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
<span data-ttu-id="c74b2-175">Запустите пример из командной строки:</span><span class="sxs-lookup"><span data-stu-id="c74b2-175">Run the sample from the command line:</span></span>

```
mvn clean compile exec:java
```

<span data-ttu-id="c74b2-176">Затем удалите ресурсы с помощью CLI:</span><span class="sxs-lookup"><span data-stu-id="c74b2-176">Then clean up the resources using the CLI:</span></span>

```azurecli-interactive
az group delete --name sampleSqlResourceGroup
```

## <a name="write-a-blob-into-a-new-storage-account"></a><span data-ttu-id="c74b2-177">Запись большого двоичного объекта в новую учетную запись хранения</span><span class="sxs-lookup"><span data-stu-id="c74b2-177">Write a blob into a new storage account</span></span>

<span data-ttu-id="c74b2-178">Замените текущий основной метод в `AzureApp.java` следующим кодом.</span><span class="sxs-lookup"><span data-stu-id="c74b2-178">Replace the current main method in `AzureApp.java` with the code below.</span></span> <span data-ttu-id="c74b2-179">Этот код создает [учетную запись хранения Azure](https://docs.microsoft.com/azure/storage/storage-introduction), а затем использует библиотеки хранилища Azure для Java, чтобы создать текстовый файл в облаке.</span><span class="sxs-lookup"><span data-stu-id="c74b2-179">This code creates an [Azure storage account](https://docs.microsoft.com/azure/storage/storage-introduction) and then uses the Azure Storage libraries for Java to create a new text file in the cloud.</span></span>

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

<span data-ttu-id="c74b2-180">Запустите пример из командной строки:</span><span class="sxs-lookup"><span data-stu-id="c74b2-180">Run the sample from the command line:</span></span>

<span data-ttu-id="c74b2-181">Перейти к файлу `helloazure.txt` в вашей учетной записи хранения можно с помощью портала Azure или [обозревателя хранилищ Azure](https://docs.microsoft.com/azure/vs-azure-tools-storage-explorer-blobs).</span><span class="sxs-lookup"><span data-stu-id="c74b2-181">You can browse for the `helloazure.txt` file in your storage account through the Azure portal or with [Azure Storage Explorer](https://docs.microsoft.com/azure/vs-azure-tools-storage-explorer-blobs).</span></span>

<span data-ttu-id="c74b2-182">Удалите учетную запись хранилища с помощью CLI:</span><span class="sxs-lookup"><span data-stu-id="c74b2-182">Clean up the storage account using the CLI:</span></span>

```azurecli-interactive
az group delete --name sampleStorageResourceGroup
```

## <a name="explore-more-samples"></a><span data-ttu-id="c74b2-183">Другие примеры</span><span class="sxs-lookup"><span data-stu-id="c74b2-183">Explore more samples</span></span>

<span data-ttu-id="c74b2-184">Дополнительные сведения о том, как использовать библиотеки управления Azure для Java, чтобы управлять ресурсами и автоматизировать задачи, см. в наших примерах кода для [виртуальных машин](../java-sdk-azure-virtual-machine-samples.md), [веб-приложений](../java-sdk-azure-web-apps-samples.md) и [базы данных SQL](../java-sdk-azure-sql-database-samples.md).</span><span class="sxs-lookup"><span data-stu-id="c74b2-184">To learn more about how to use the Azure management libraries for Java to manage resources and automate tasks, see our sample code for [virtual machines](../java-sdk-azure-virtual-machine-samples.md), [web apps](../java-sdk-azure-web-apps-samples.md) and [SQL database](../java-sdk-azure-sql-database-samples.md).</span></span>

## <a name="reference-and-release-notes"></a><span data-ttu-id="c74b2-185">Ссылки и заметки о выпуске</span><span class="sxs-lookup"><span data-stu-id="c74b2-185">Reference and release notes</span></span>

<span data-ttu-id="c74b2-186">[Ссылки](http://docs.microsoft.com/java/api) доступны для всех пакетов.</span><span class="sxs-lookup"><span data-stu-id="c74b2-186">A [reference](http://docs.microsoft.com/java/api) is available for all packages.</span></span>

## <a name="get-help-and-give-feedback"></a><span data-ttu-id="c74b2-187">Справка и отзывы</span><span class="sxs-lookup"><span data-stu-id="c74b2-187">Get help and give feedback</span></span>

<span data-ttu-id="c74b2-188">Задавайте вопросы сообществу на сайте [Stack Overflow](http://stackoverflow.com/questions/tagged/azure+java).</span><span class="sxs-lookup"><span data-stu-id="c74b2-188">Post questions to the community on [Stack Overflow](http://stackoverflow.com/questions/tagged/azure+java).</span></span> <span data-ttu-id="c74b2-189">Сообщайте об ошибках и нерешенных проблемах с библиотеками Azure для Java на странице [проектов GitHub](https://github.com/Azure/azure-sdk-for-java).</span><span class="sxs-lookup"><span data-stu-id="c74b2-189">Report bugs and open issues against the Azure libraries for Java on the [project GitHub](https://github.com/Azure/azure-sdk-for-java).</span></span>
