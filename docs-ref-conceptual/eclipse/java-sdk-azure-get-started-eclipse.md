---
title: "Начало работы с Azure для Java с помощью Eclipse"
description: "Базовое использование библиотек Azure для Java с вашей подпиской Azure."
keywords: Azure, Java, SDK, API, authenticate, get-started
author: roygara
ms.author: v-rogara
manager: timlt
ms.date: 10/30/2017
ms.topic: get-started-article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: multiple
ms.openlocfilehash: 1c1ef7b8646824c5c8bfcbbf5e0507c95ac1ee79
ms.sourcegitcommit: fcf1189ede712ae30f8c7626bde50c9b8bb561bc
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/01/2017
---
# <a name="get-started-with-the-azure-libraries-using-eclipse"></a><span data-ttu-id="9dc60-104">Начало работы с библиотеками Azure с помощью Eclipse</span><span class="sxs-lookup"><span data-stu-id="9dc60-104">Get started with the Azure libraries using Eclipse</span></span>

<span data-ttu-id="9dc60-105">В этом руководстве описано, как настроить среду разработки и использовать библиотеки Azure для Java.</span><span class="sxs-lookup"><span data-stu-id="9dc60-105">This guide walks you through setting up a development environment and using the Azure libraries for Java.</span></span> <span data-ttu-id="9dc60-106">Вы создадите субъект-службу для аутентификации в Azure и выполните пример кода, который создает и использует ресурсы Azure в вашей подписке.</span><span class="sxs-lookup"><span data-stu-id="9dc60-106">You'll create a service principal to authenticate with Azure and run some sample code that creates and uses Azure resources in your subscription.</span></span> <span data-ttu-id="9dc60-107">Использование Eclipse является необязательным при разработке приложений Java в Azure.</span><span class="sxs-lookup"><span data-stu-id="9dc60-107">Using Eclipse is optional for Java development with Azure.</span></span> <span data-ttu-id="9dc60-108">Подходит любая среда IDE с интегрированным компонентом Maven.</span><span class="sxs-lookup"><span data-stu-id="9dc60-108">Any IDE that has Maven integration works.</span></span> <span data-ttu-id="9dc60-109">Кроме того, можно выполнять код из командной строки с помощью Maven, если вы предпочитаете не использовать IDE.</span><span class="sxs-lookup"><span data-stu-id="9dc60-109">Alternatively, you can run your code from the commandline using Maven if you prefer not to use any IDE.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9dc60-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="9dc60-110">Prerequisites</span></span>

- <span data-ttu-id="9dc60-111">Учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="9dc60-111">An Azure account.</span></span> <span data-ttu-id="9dc60-112">Если у вас ее нет, [получите бесплатную пробную версию](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="9dc60-112">If you don't have one, [get a free trial](https://azure.microsoft.com/free/)</span></span>
- <span data-ttu-id="9dc60-113">[Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/quickstart) или [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="9dc60-113">[Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/quickstart) or [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2).</span></span>
- <span data-ttu-id="9dc60-114">Последняя стабильная версия [Eclipse](http://www.eclipse.org/downloads/).</span><span class="sxs-lookup"><span data-stu-id="9dc60-114">The latest stable version of [Eclipse](http://www.eclipse.org/downloads/)</span></span>

## <a name="set-up-authentication"></a><span data-ttu-id="9dc60-115">Настройка проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="9dc60-115">Set up authentication</span></span>

<span data-ttu-id="9dc60-116">Чтобы выполнить пример кода из этого руководства, предоставьте приложению Java в вашей подписке Azure разрешения на чтение и создание.</span><span class="sxs-lookup"><span data-stu-id="9dc60-116">Your Java application needs read and create permissions in your Azure subscription to run the sample code in this tutorial.</span></span> <span data-ttu-id="9dc60-117">Создайте субъект-службу и настройте приложение для выполнения со связанными учетными данными.</span><span class="sxs-lookup"><span data-stu-id="9dc60-117">Create a service principal and configure your application to run with its credentials.</span></span> <span data-ttu-id="9dc60-118">Субъект-служба помогает создать неинтерактивную учетную запись, связанную с вашим идентификатором. Этой учетной записи предоставляются только разрешения, необходимые для запуска приложения.</span><span class="sxs-lookup"><span data-stu-id="9dc60-118">Service principals provide a way to create a non-interactive account associated with your identity to which you grant only the privileges your app needs to run.</span></span>

<span data-ttu-id="9dc60-119">[Создайте субъект-службу](/cli/azure/create-an-azure-service-principal-azure-cli), чтобы предоставить коду разрешение на создание и обновление ресурсов в вашей подписке без непосредственного использования учетных данных.</span><span class="sxs-lookup"><span data-stu-id="9dc60-119">[Create a service principal](/cli/azure/create-an-azure-service-principal-azure-cli) to grant your code permission to create and update resources in your subscription without using your account credentials directly.</span></span> <span data-ttu-id="9dc60-120">Запишите выходные данные.</span><span class="sxs-lookup"><span data-stu-id="9dc60-120">Make sure to capture the output.</span></span> <span data-ttu-id="9dc60-121">Вместо `MY_SECURE_PASSWORD` в аргументе пароля нужно указать [безопасный пароль](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-policy).</span><span class="sxs-lookup"><span data-stu-id="9dc60-121">Provide a [secure password](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-policy) in the password argument instead of `MY_SECURE_PASSWORD`.</span></span> <span data-ttu-id="9dc60-122">Пароль должен содержать 8–16 символов и соответствовать хотя бы трем из четырех следующих критериев:</span><span class="sxs-lookup"><span data-stu-id="9dc60-122">Your password must be 8 to 16 characters and match at least 3 out of the 4 following criteria:</span></span>

* <span data-ttu-id="9dc60-123">наличие строчных букв;</span><span class="sxs-lookup"><span data-stu-id="9dc60-123">Include lowercase characters</span></span>
* <span data-ttu-id="9dc60-124">наличие прописных букв;</span><span class="sxs-lookup"><span data-stu-id="9dc60-124">Include uppercase characters</span></span>
* <span data-ttu-id="9dc60-125">наличие цифр;</span><span class="sxs-lookup"><span data-stu-id="9dc60-125">Include numbers</span></span>
* <span data-ttu-id="9dc60-126">наличие одного из следующих символов: @ # $ % ^ & * - _ !</span><span class="sxs-lookup"><span data-stu-id="9dc60-126">Include one of the following symbols: @ # $ % ^ & * - _ !</span></span> <span data-ttu-id="9dc60-127">+ = [ ] { } | \ : ‘ , .</span><span class="sxs-lookup"><span data-stu-id="9dc60-127">+ = [ ] { } | \ : ‘ , .</span></span> <span data-ttu-id="9dc60-128">?</span><span class="sxs-lookup"><span data-stu-id="9dc60-128">?</span></span> <span data-ttu-id="9dc60-129">/ \` ~ “ ( ) ;</span><span class="sxs-lookup"><span data-stu-id="9dc60-129">/ \` ~ “ ( ) ;</span></span>


```azurecli-interactive
az ad sp create-for-rbac --name AzureJavaTest --password "MY_SECURE_PASSWORD"
```

<span data-ttu-id="9dc60-130">Вы получите ответ в следующем формате:</span><span class="sxs-lookup"><span data-stu-id="9dc60-130">Which gives you a reply in the following format:</span></span>

```json
{
  "appId": "a487e0c1-82af-47d9-9a0b-af184eb87646d",
  "displayName": "AzureJavaTest",
  "name": "http://AzureJavaTest",
  "password": password,
  "tenant": "tttttttt-tttt-tttt-tttt-tttttttttttt"
}
```

<span data-ttu-id="9dc60-131">Затем скопируйте следующий код в текстовый файл в системе:</span><span class="sxs-lookup"><span data-stu-id="9dc60-131">Next, copy the following into a text file on your system:</span></span>

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

<span data-ttu-id="9dc60-132">Замените первые четыре значения следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="9dc60-132">Replace the top four values with the following:</span></span>

- <span data-ttu-id="9dc60-133">subscription — используйте значение *id* из `az account show` в Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="9dc60-133">subscription: use the *id* value from `az account show` in the Azure CLI 2.0.</span></span>
- <span data-ttu-id="9dc60-134">client — используйте значение *appId* из выходных данных субъекта-службы.</span><span class="sxs-lookup"><span data-stu-id="9dc60-134">client: use the *appId* value from the output taken from a service principal output.</span></span>
- <span data-ttu-id="9dc60-135">key — используйте значение *password* из выходных данных субъекта-службы.</span><span class="sxs-lookup"><span data-stu-id="9dc60-135">key: use the *password* value from the service principal output.</span></span>
- <span data-ttu-id="9dc60-136">tenant — используйте значение *tenant* из выходных данных субъекта-службы.</span><span class="sxs-lookup"><span data-stu-id="9dc60-136">tenant: use the *tenant* value from the service principal output.</span></span>

<span data-ttu-id="9dc60-137">Сохраните этот файл в безопасном расположении в вашей системе, доступном для кода.</span><span class="sxs-lookup"><span data-stu-id="9dc60-137">Save this file in a secure location on your system where your code can read it.</span></span> <span data-ttu-id="9dc60-138">Вы можете использовать этот файл для будущего кода, поэтому рекомендуется сохранить его где-либо за пределами используемого в этой статье приложения.</span><span class="sxs-lookup"><span data-stu-id="9dc60-138">You may use this file for future code so it's recommended to store it somewhere external to the application in this article.</span></span>

<span data-ttu-id="9dc60-139">Задайте переменную среды `AZURE_AUTH_LOCATION` и укажите полный путь к файлу аутентификации в оболочке.</span><span class="sxs-lookup"><span data-stu-id="9dc60-139">Set an environment variable `AZURE_AUTH_LOCATION` with the full path to the authentication file in your shell.</span></span>

```bash
export AZURE_AUTH_LOCATION=/Users/raisa/azureauth.properties
```

<span data-ttu-id="9dc60-140">Если вы работаете в среде Windows, добавьте переменную в свойства системы.</span><span class="sxs-lookup"><span data-stu-id="9dc60-140">If you're working in a windows environment, add the variable to your system properties.</span></span> <span data-ttu-id="9dc60-141">В PowerShell замените вторую переменную путем к файлу и введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="9dc60-141">Open PowerShell and, after replacing the second variable with the path to your file, enter the following command:</span></span>

```powershell
[Environment]::SetEnvironmentVariable("AZURE_AUTH_LOCATION", "C:\<fullpath>\azureauth.properties", "Machine")
```

## <a name="create-a-new-maven-project"></a><span data-ttu-id="9dc60-142">Создание нового проекта Maven</span><span class="sxs-lookup"><span data-stu-id="9dc60-142">Create a new Maven project</span></span>

> [!NOTE]
> <span data-ttu-id="9dc60-143">В этом руководстве пример кода создается и запускается с помощью средства сборки Maven. Но с библиотеками Azure для Java можно использовать и другие инструменты, например Gradle.</span><span class="sxs-lookup"><span data-stu-id="9dc60-143">This guide uses Maven build tool to build and run the sample code, but other build tools such as Gradle also work with the Azure libraries for Java.</span></span> 

<span data-ttu-id="9dc60-144">Откройте Eclipse и выберите **File** -> **New** (Файл > Создать).</span><span class="sxs-lookup"><span data-stu-id="9dc60-144">Open Eclipse, select **File** -> **New**.</span></span> <span data-ttu-id="9dc60-145">В новом окне откройте папку Maven и выберите проект Maven.</span><span class="sxs-lookup"><span data-stu-id="9dc60-145">In the new window that appears open the Maven folder then select Maven Project.</span></span> 

<span data-ttu-id="9dc60-146">Оставьте на следующем экране значения по умолчанию и щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="9dc60-146">Leave the selections on the next screen defaults, and select **Next**.</span></span> <span data-ttu-id="9dc60-147">Выполните эти же действия на этом экране в отношении архетипов.</span><span class="sxs-lookup"><span data-stu-id="9dc60-147">Do the same for this screen regarding archetypes.</span></span>

<span data-ttu-id="9dc60-148">Откроется экран с предложением указать groupID, ArtifactID и т. д. Введите com.fabrikam для groupID и AzureApp для artifactID.</span><span class="sxs-lookup"><span data-stu-id="9dc60-148">When you come to the screen asking for groupID, ArtifactID, etc. Enter "com.fabrikam" for the groupID and enter "AzureApp" for the artifactID.</span></span>

<span data-ttu-id="9dc60-149">Откройте файл pom.xml.</span><span class="sxs-lookup"><span data-stu-id="9dc60-149">Now, open the pom.xml file.</span></span> <span data-ttu-id="9dc60-150">В теге `dependencies` добавьте следующий код:</span><span class="sxs-lookup"><span data-stu-id="9dc60-150">Inside the `dependencies` tag add the following code:</span></span>

```XML
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
```

<span data-ttu-id="9dc60-151">Сохраните файл pom.xml.</span><span class="sxs-lookup"><span data-stu-id="9dc60-151">Now, save the pom.xml.</span></span> <span data-ttu-id="9dc60-152">После этого Eclipse скачает все указанные зависимости.</span><span class="sxs-lookup"><span data-stu-id="9dc60-152">This prompts Eclipse to download all the specified dependencies.</span></span> <span data-ttu-id="9dc60-153">Это может занять какое-то время.</span><span class="sxs-lookup"><span data-stu-id="9dc60-153">This may take a moment.</span></span>
   
## <a name="install-the-azure-toolkit-for-eclipse"></a><span data-ttu-id="9dc60-154">Установка набора средств Azure для Eclipse</span><span class="sxs-lookup"><span data-stu-id="9dc60-154">Install the azure toolkit for Eclipse</span></span>

<span data-ttu-id="9dc60-155">[Набор средств Azure](azure-toolkit-for-eclipse.md) требуется, если вы развертываете веб-приложения и API-интерфейсы программными средствами. Сейчас этот набор не используется для разработки других типов.</span><span class="sxs-lookup"><span data-stu-id="9dc60-155">The [Azure toolkit](azure-toolkit-for-eclipse.md) is necessary if you're going to be deploying web apps or APIs programmatically but is not currently used for any other kinds of development.</span></span> <span data-ttu-id="9dc60-156">Ниже приведены общие сведения о действиях по установке.</span><span class="sxs-lookup"><span data-stu-id="9dc60-156">The following is a summary of the installation process.</span></span> <span data-ttu-id="9dc60-157">См. дополнительные сведения об [установке набора средств Azure для Eclipse](azure-toolkit-for-eclipse.md).</span><span class="sxs-lookup"><span data-stu-id="9dc60-157">For detailed stpes, visit [Installing the Azure Toolkit for Eclipse](azure-toolkit-for-eclipse.md).</span></span>

<span data-ttu-id="9dc60-158">В меню **Help** (Справка) выберите пункт **Install New Software** (Установка нового программного обеспечения).</span><span class="sxs-lookup"><span data-stu-id="9dc60-158">Select the **Help** menu and then select **Install New software**.</span></span>

<span data-ttu-id="9dc60-159">В поле **Work with:** (Работа с:) введите `http://dl.microsoft.com/eclipse` и нажмите клавишу ВВОД.</span><span class="sxs-lookup"><span data-stu-id="9dc60-159">In the **Work with:** field enter `http://dl.microsoft.com/eclipse` and press enter.</span></span>

<span data-ttu-id="9dc60-160">Затем установите флажок рядом с пунктом **Azure toolkit for Java** (Набор средств Azure для Java) и снимите флажок рядом с пунктом **Contact all update sites during install to find required software** (Проверить все сайты обновления во время установки для поиска требуемого ПО).</span><span class="sxs-lookup"><span data-stu-id="9dc60-160">Then, select the checkbox next to **Azure toolkit for Java** and uncheck the checkbox for **Contact all update sites during install to find required software**.</span></span> <span data-ttu-id="9dc60-161">Затем нажмите кнопку "Далее".</span><span class="sxs-lookup"><span data-stu-id="9dc60-161">Then select next.</span></span>

## <a name="create-a-linux-virtual-machine"></a><span data-ttu-id="9dc60-162">Создание виртуальной машины Linux</span><span class="sxs-lookup"><span data-stu-id="9dc60-162">Create a Linux virtual machine</span></span>

<span data-ttu-id="9dc60-163">Создайте файл с именем `AzureApp.java` в каталоге проекта `src/main/java` и вставьте следующий блок кода.</span><span class="sxs-lookup"><span data-stu-id="9dc60-163">Create a new file named `AzureApp.java` in the project's `src/main/java` directory and paste in the following block of code.</span></span> <span data-ttu-id="9dc60-164">Обновите переменные `userName` и `sshKey`, указав реальные значения для своего компьютера.</span><span class="sxs-lookup"><span data-stu-id="9dc60-164">Update the `userName` and `sshKey` variables with real values for your machine.</span></span> <span data-ttu-id="9dc60-165">Код создает виртуальную машину Linux с именем `testLinuxVM` в группе ресурсов `sampleResourceGroup`, которая выполняется в регионе Azure "Восточная часть США".</span><span class="sxs-lookup"><span data-stu-id="9dc60-165">The code creates a new Linux VM with name `testLinuxVM` in a resource group `sampleResourceGroup` running in the US East Azure region.</span></span>

<span data-ttu-id="9dc60-166">Чтобы создать `sshkey`, откройте Cloud Shell и введите `ssh-keygen -t rsa -b 2048`.</span><span class="sxs-lookup"><span data-stu-id="9dc60-166">In order to create an `sshkey`, open the azure cloud shell and enter `ssh-keygen -t rsa -b 2048`.</span></span> <span data-ttu-id="9dc60-167">Введите имя файла, извлеките из файла с расширением .public ключ, который используется в следующем коде, а затем скопируйте и вставьте его в переменную `sshKey`.</span><span class="sxs-lookup"><span data-stu-id="9dc60-167">Name the file and then access the .public file to get the key, which you use in the following code, copy and paste it all into your variable `sshKey`.</span></span>

```java
package com.fabrikam.AzureApp;

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


<span data-ttu-id="9dc60-168">В консоли будут отображаться некоторые запросы и ответы REST по мере того, как пакет SDK выполняет базовые вызовы REST API Azure, чтобы настроить виртуальную машину и ее ресурсы.</span><span class="sxs-lookup"><span data-stu-id="9dc60-168">You see some REST requests and responses in the console as the SDK makes the underlying calls to the Azure REST API to configure the virtual machine and its resources.</span></span> <span data-ttu-id="9dc60-169">Когда программа завершит работу, проверьте виртуальную машину в подписке с помощью Azure CLI 2.0:</span><span class="sxs-lookup"><span data-stu-id="9dc60-169">When the program finishes, verify the virtual machine in your subscription with the Azure CLI 2.0:</span></span>

```azurecli-interactive
az vm list --resource-group sampleVmResourceGroup
```

<span data-ttu-id="9dc60-170">Проверив, что код работает, используйте CLI, чтобы удалить виртуальную машину и ее ресурсы.</span><span class="sxs-lookup"><span data-stu-id="9dc60-170">Once you've verified that the code worked, use the CLI to delete the VM and its resources.</span></span>

```azurecli-interactive
az group delete --name sampleVmResourceGroup
```

## <a name="deploy-a-web-app-from-a-github-repo"></a><span data-ttu-id="9dc60-171">Развертывание веб-приложения из репозитория GitHub</span><span class="sxs-lookup"><span data-stu-id="9dc60-171">Deploy a web app from a GitHub repo</span></span>

<span data-ttu-id="9dc60-172">Перед выполнением кода замените основной метод в `AzureApp.java` одним из указанных ниже, задав для переменной `appName` уникальное значение.</span><span class="sxs-lookup"><span data-stu-id="9dc60-172">Replace the main method in `AzureApp.java` with the one below, updating the `appName` variable to a unique value before running the code.</span></span> <span data-ttu-id="9dc60-173">Этот код развертывает веб-приложение из ветви `master` в общедоступном репозитории GitHub в новое [веб-приложение службы приложений Azure](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) ценовой категории "Бесплатный".</span><span class="sxs-lookup"><span data-stu-id="9dc60-173">This code deploys a web application from the `master` branch in a public GitHub repo into a new [Azure App Service Web App](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) running in the free pricing tier.</span></span>

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

<span data-ttu-id="9dc60-174">Перед использованием Maven выполните следующий код:</span><span class="sxs-lookup"><span data-stu-id="9dc60-174">Run the code as before using Maven:</span></span>

<span data-ttu-id="9dc60-175">Откройте браузер и укажите приложение в CLI:</span><span class="sxs-lookup"><span data-stu-id="9dc60-175">Open a browser pointed to the application using the CLI:</span></span>

```azurecli-interactive
az appservice web browse --resource-group sampleWebResourceGroup --name YOUR_APP_NAME
```
<span data-ttu-id="9dc60-176">Проверив развертывание, удалите веб-приложение и план из подписки.</span><span class="sxs-lookup"><span data-stu-id="9dc60-176">Remove the web app and plan from your subscription once you've verified the deployment.</span></span>

```azurecli-interactive
az group delete --name sampleWebResourceGroup
```

## <a name="connect-to-an-azure-sql-database"></a><span data-ttu-id="9dc60-177">Подключение к базе данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="9dc60-177">Connect to an Azure SQL database</span></span>

<span data-ttu-id="9dc60-178">Замените текущий основной метод в `AzureApp.java` кодом ниже, задав реальное значение для переменной `dbPassword`.</span><span class="sxs-lookup"><span data-stu-id="9dc60-178">Replace the current main method in `AzureApp.java` with the code below, setting a real value for the `dbPassword` variable.</span></span>
<span data-ttu-id="9dc60-179">Этот код создает новую базу данных SQL с правилом брандмауэра, разрешающим удаленный доступ, и подключается к ней с помощью драйвера JBDC базы данных SQL.</span><span class="sxs-lookup"><span data-stu-id="9dc60-179">This code creates a new SQL database with a firewall rule allowing remote access,  and then connects to it using the SQL Database JBDC driver.</span></span> 

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
<span data-ttu-id="9dc60-180">Запустите пример из командной строки:</span><span class="sxs-lookup"><span data-stu-id="9dc60-180">Run the sample from the command line:</span></span>

```
mvn clean compile exec:java
```

<span data-ttu-id="9dc60-181">Затем удалите ресурсы с помощью CLI:</span><span class="sxs-lookup"><span data-stu-id="9dc60-181">Then clean up the resources using the CLI:</span></span>

```azurecli-interactive
az group delete --name sampleSqlResourceGroup
```

## <a name="write-a-blob-into-a-new-storage-account"></a><span data-ttu-id="9dc60-182">Запись большого двоичного объекта в новую учетную запись хранения</span><span class="sxs-lookup"><span data-stu-id="9dc60-182">Write a blob into a new storage account</span></span>

<span data-ttu-id="9dc60-183">Замените текущий основной метод в `AzureApp.java` следующим кодом.</span><span class="sxs-lookup"><span data-stu-id="9dc60-183">Replace the current main method in `AzureApp.java` with the code below.</span></span> <span data-ttu-id="9dc60-184">Этот код создает [учетную запись хранения Azure](https://docs.microsoft.com/azure/storage/storage-introduction), а затем использует библиотеки хранилища Azure для Java, чтобы создать текстовый файл в облаке.</span><span class="sxs-lookup"><span data-stu-id="9dc60-184">This code creates an [Azure storage account](https://docs.microsoft.com/azure/storage/storage-introduction) and then uses the Azure Storage libraries for Java to create a new text file in the cloud.</span></span>

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

            // create a storage container to hold the files
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

<span data-ttu-id="9dc60-185">Запустите пример из командной строки:</span><span class="sxs-lookup"><span data-stu-id="9dc60-185">Run the sample from the command line:</span></span>

<span data-ttu-id="9dc60-186">Перейти к файлу `helloazure.txt` в вашей учетной записи хранения можно с помощью портала Azure или [обозревателя хранилищ Azure](https://docs.microsoft.com/azure/vs-azure-tools-storage-explorer-blobs).</span><span class="sxs-lookup"><span data-stu-id="9dc60-186">You can browse for the `helloazure.txt` file in your storage account through the Azure portal or with [Azure Storage Explorer](https://docs.microsoft.com/azure/vs-azure-tools-storage-explorer-blobs).</span></span>

<span data-ttu-id="9dc60-187">Удалите учетную запись хранилища с помощью CLI:</span><span class="sxs-lookup"><span data-stu-id="9dc60-187">Clean up the storage account using the CLI:</span></span>

```azurecli-interactive
az group delete --name sampleStorageResourceGroup
```

## <a name="explore-more-samples"></a><span data-ttu-id="9dc60-188">Другие примеры</span><span class="sxs-lookup"><span data-stu-id="9dc60-188">Explore more samples</span></span>

<span data-ttu-id="9dc60-189">Дополнительные сведения о том, как использовать библиотеки управления Azure для Java, чтобы управлять ресурсами и автоматизировать задачи, см. в наших примерах кода для [виртуальных машин](../java-sdk-azure-virtual-machine-samples.md), [веб-приложений](../java-sdk-azure-web-apps-samples.md) и [базы данных SQL](../java-sdk-azure-sql-database-samples.md).</span><span class="sxs-lookup"><span data-stu-id="9dc60-189">To learn more about how to use the Azure management libraries for Java to manage resources and automate tasks, see our sample code for [virtual machines](../java-sdk-azure-virtual-machine-samples.md), [web apps](../java-sdk-azure-web-apps-samples.md) and [SQL database](../java-sdk-azure-sql-database-samples.md).</span></span>

## <a name="reference-and-release-notes"></a><span data-ttu-id="9dc60-190">Ссылки и заметки о выпуске</span><span class="sxs-lookup"><span data-stu-id="9dc60-190">Reference and release notes</span></span>

<span data-ttu-id="9dc60-191">[Ссылки](http://docs.microsoft.com/java/api) доступны для всех пакетов.</span><span class="sxs-lookup"><span data-stu-id="9dc60-191">A [reference](http://docs.microsoft.com/java/api) is available for all packages.</span></span>

## <a name="get-help-and-give-feedback"></a><span data-ttu-id="9dc60-192">Справка и отзывы</span><span class="sxs-lookup"><span data-stu-id="9dc60-192">Get help and give feedback</span></span>

<span data-ttu-id="9dc60-193">Задавайте вопросы сообществу на сайте [Stack Overflow](http://stackoverflow.com/questions/tagged/azure+java).</span><span class="sxs-lookup"><span data-stu-id="9dc60-193">Post questions to the community on [Stack Overflow](http://stackoverflow.com/questions/tagged/azure+java).</span></span> <span data-ttu-id="9dc60-194">Сообщайте об ошибках и нерешенных проблемах с библиотеками Azure для Java на странице [проектов GitHub](https://github.com/Azure/azure-sdk-for-java).</span><span class="sxs-lookup"><span data-stu-id="9dc60-194">Report bugs and open issues against the Azure libraries for Java on the [project GitHub](https://github.com/Azure/azure-sdk-for-java).</span></span>
