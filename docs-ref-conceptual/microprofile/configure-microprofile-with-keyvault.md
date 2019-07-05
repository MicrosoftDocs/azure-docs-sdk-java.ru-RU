---
title: Настройка MicroProfile с помощью Azure Key Vault
description: Узнайте, как добавлять секреты в веб-службу MicroProfile с помощью Azure Key Vault
services: key-vault
documentationcenter: java
author: jonathangiles
manager: routlaw
editor: jonathangiles
ms.assetid: ''
ms.author: jogiles
ms.date: 09/07/2018
ms.devlang: java
ms.service: key-vault
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: web
ms.openlocfilehash: c405711813176823f2ddee6b4002f75c2b25fdb5
ms.sourcegitcommit: f8faa4a14c714e148c513fd46f119524f3897abf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/03/2019
ms.locfileid: "67533615"
---
# <a name="configure-microprofile-by-using-azure-key-vault"></a><span data-ttu-id="aee2c-103">Настройка MicroProfile с помощью Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="aee2c-103">Configure MicroProfile by using Azure Key Vault</span></span>

<span data-ttu-id="aee2c-104">В этой статье показано, как настроить приложение [MicroProfile](http://microprofile.io) на получение секретов из [хранилища ключей Azure](https://azure.microsoft.com/services/key-vault/).</span><span class="sxs-lookup"><span data-stu-id="aee2c-104">This article demonstrates how to configure a [MicroProfile](http://microprofile.io) application to retrieve secrets from an [Azure key vault](https://azure.microsoft.com/services/key-vault/).</span></span> <span data-ttu-id="aee2c-105">В этом процессе [API-интерфейсы конфигурации MicroProfile](https://microprofile.io/project/eclipse/microprofile-config) используется для создания прямого подключения к хранилищу ключей Azure.</span><span class="sxs-lookup"><span data-stu-id="aee2c-105">In this process, you use the [MicroProfile Config APIs](https://microprofile.io/project/eclipse/microprofile-config) to create a direct connection to an Azure key vault.</span></span> <span data-ttu-id="aee2c-106">API-интерфейсы MicroProfile Config предоставляют разработчикам стандартные средства для добавления данных конфигурации в микрослужбы и получения этих данных.</span><span class="sxs-lookup"><span data-stu-id="aee2c-106">As a developer, by using the MicroProfile Config APIs, you benefit from a standard API for retrieving and injecting configuration data into their microservices.</span></span>

<span data-ttu-id="aee2c-107">Прежде чем начать, посмотрите, какое сочетание Azure Key Vault и API конфигурации MicroProfile позволяет написать нужный код.</span><span class="sxs-lookup"><span data-stu-id="aee2c-107">Before you start, take a quick look at what a combination of Azure Key Vault and the MicroProfile Config API enables you to write in your code.</span></span> <span data-ttu-id="aee2c-108">Следующий фрагмент кода из поля в классе, который объявлен в `@Inject` и `@ConfigProperty`.</span><span class="sxs-lookup"><span data-stu-id="aee2c-108">The following code snippet is of a field in a class that's annotated with `@Inject` and `@ConfigProperty`.</span></span> <span data-ttu-id="aee2c-109">Параметр *name*, указанный в объявлении, — это имя свойства, которое нужно найти в хранилище ключей, а *defaultValue* — значение по умолчанию, которое будет использовано, если ключ не будет найден.</span><span class="sxs-lookup"><span data-stu-id="aee2c-109">The *name* that's specified in the annotation is the name of the property to look up in your key vault, and the *defaultValue* is what will be set if the key is not discovered.</span></span> <span data-ttu-id="aee2c-110">Результатом является то, что значение, которое хранится в хранилище ключей, или значение по умолчанию, автоматически добавляется в поле во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="aee2c-110">The result is that the value that's stored in the key vault, or the default value, is injected automatically into the field at runtime.</span></span> <span data-ttu-id="aee2c-111">Это действие может существенно упростить жизнь, так как вам больше не нужно передавать значения в конструкторы и методы заданий.</span><span class="sxs-lookup"><span data-stu-id="aee2c-111">This action can simplify your life, because you no longer need to pass values around in constructors and setter methods.</span></span> <span data-ttu-id="aee2c-112">Вместо этого эту задачу берет на себя MicroProfile.</span><span class="sxs-lookup"><span data-stu-id="aee2c-112">Instead, MicroProfile handles this task.</span></span>

```java
@Inject
@ConfigProperty(name = "key-name", defaultValue = "Unknown")
String keyValue;
```

<span data-ttu-id="aee2c-113">Чтобы запросить секреты, при необходимости можно также обращаться к конфигурации MicroProfile напрямую.</span><span class="sxs-lookup"><span data-stu-id="aee2c-113">To request secrets, as necessary, you can also access the MicroProfile config directly.</span></span> <span data-ttu-id="aee2c-114">Например:</span><span class="sxs-lookup"><span data-stu-id="aee2c-114">For example:</span></span>

```java
public class DemoClass {
    @Inject
    Config config;

    public void method() {
        System.out.println("Hello: " + config.getValue("key-name", String.class));
    }
}
```

<span data-ttu-id="aee2c-115">В этом примере кода используется [Payara Micro](https://www.payara.fish/payara_micro) и [MicroProfile](https://microprofile.io/) для создания файла требования Tiny Java веб-приложения (WAR), который можно запустить локально на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="aee2c-115">This sample code uses [Payara Micro](https://www.payara.fish/payara_micro) and [MicroProfile](https://microprofile.io/) to create a tiny Java web application requirement (WAR) file that you can run locally on your machine.</span></span> <span data-ttu-id="aee2c-116">Упаковка кода в контейнер Docker и его отправка в Azure выходит за рамки нашего примера, но в конце этой статьи приведены ссылки на другие полезные руководства, в которых вы найдете нужную информацию.</span><span class="sxs-lookup"><span data-stu-id="aee2c-116">It doesn't demonstrate how to Dockerize or push the code to Azure, but the section at the end of this article has links to other useful tutorials that explain this.</span></span>

<span data-ttu-id="aee2c-117">В примере используется открытая и бесплатная библиотека, которая создает источник конфигурации (с помощью API конфигурации MicroProfile) в хранилище ключей.</span><span class="sxs-lookup"><span data-stu-id="aee2c-117">The sample uses a free and open source library that creates a config source (using the MicroProfile Config API) in your key vault.</span></span> <span data-ttu-id="aee2c-118">Подробные сведения об этой библиотеке и ее код можно найти на [странице проекта на сайте GitHub](https://github.com/Azure/azure-microprofile/tree/master/microprofile-config-keyvault).</span><span class="sxs-lookup"><span data-stu-id="aee2c-118">To learn more about this library and review the code, see the [project GitHub page](https://github.com/Azure/azure-microprofile/tree/master/microprofile-config-keyvault).</span></span> <span data-ttu-id="aee2c-119">При использовании этой библиотеки код в этом руководстве может упростить работу с конфигурацией библиотеки и дальнейшее внедрение ключей в код.</span><span class="sxs-lookup"><span data-stu-id="aee2c-119">If you use the library, the code in this tutorial can simply focus on the configuration of the library and then inject keys into your code.</span></span> <span data-ttu-id="aee2c-120">Благодаря этому нет необходимости писать код специально для Azure.</span><span class="sxs-lookup"><span data-stu-id="aee2c-120">You don't need to write any Azure-specific code.</span></span>

<span data-ttu-id="aee2c-121">Для выполнения этого кода на локальном компьютере начните с создания ресурса хранилища ключей, а затем следуйте инструкциям в следующих разделах.</span><span class="sxs-lookup"><span data-stu-id="aee2c-121">To run this code on your local machine, starting with creating a key vault resource, follow the instructions in the next sections.</span></span>

## <a name="create-a-key-vault-resource"></a><span data-ttu-id="aee2c-122">Создание ресурса хранилища ключей</span><span class="sxs-lookup"><span data-stu-id="aee2c-122">Create a key vault resource</span></span>

<span data-ttu-id="aee2c-123">В этом разделе для создания ресурса хранилища ключей и его заполнения одним секретом используется Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="aee2c-123">In this section, you use the Azure CLI to create a key vault resource and populate it with one secret.</span></span>

1. <span data-ttu-id="aee2c-124">Создайте субъект-службу Azure.</span><span class="sxs-lookup"><span data-stu-id="aee2c-124">Create an Azure service principal.</span></span> <span data-ttu-id="aee2c-125">На этом шаге вы получите идентификатор клиента и ключ, который необходим, чтобы получить доступ к хранилищу ключей:</span><span class="sxs-lookup"><span data-stu-id="aee2c-125">This step gives you the client ID and key that you need to access your key vault:</span></span>

    ```bash
    az login
    az account set --subscription <subscription_id>

    az ad sp create-for-rbac --name <service_principal_name>
    ```

    <span data-ttu-id="aee2c-126">Используйте, например, команду *microprofile-keyvault-service-principal*, чтобы заменить *\<имя_субъекта-службы>* , созданной ранее.</span><span class="sxs-lookup"><span data-stu-id="aee2c-126">Let's use *microprofile-keyvault-service-principal* to replace *\<service_principal_name>* in the preceding step.</span></span> <span data-ttu-id="aee2c-127">Ответ Azure будет примерно таким:</span><span class="sxs-lookup"><span data-stu-id="aee2c-127">The response from Azure would be similar to the following:</span></span>

    ```json
    {
      "appId": "5292398e-XXXX-40ce-XXXX-d49fXXXX9e79",
      "displayName": "microprofile-keyvault-service-principal",
      "name": "http://microprofile-keyvault-service-principal",
      "password": "9b217777-XXXX-4954-XXXX-deafXXXX790a",
      "tenant": "72f988bf-XXXX-41af-XXXX-2d7cd011db47"
    }
    ```

    <span data-ttu-id="aee2c-128">Обратите отдельное внимание на значения *appId* и *password*.</span><span class="sxs-lookup"><span data-stu-id="aee2c-128">Of particular note here are the *appId* and *password* values.</span></span> <span data-ttu-id="aee2c-129">Позднее в этой статье они будут использоваться в качестве *идентификатора клиента* и *ключа*.</span><span class="sxs-lookup"><span data-stu-id="aee2c-129">You'll use them later in this article as *client ID* and *key*.</span></span>

1. <span data-ttu-id="aee2c-130">Теперь, когда вы создали субъект-службу, можно создать группу ресурсов (необязательно).</span><span class="sxs-lookup"><span data-stu-id="aee2c-130">(Optional) Now that you've created a service principal, you can create a resource group.</span></span> <span data-ttu-id="aee2c-131">Если у вас уже есть группа ресурсов, которую вы хотите использовать, этот шаг можно пропустить.</span><span class="sxs-lookup"><span data-stu-id="aee2c-131">If you already have a resource group that you want to use, you can skip this step.</span></span> <span data-ttu-id="aee2c-132">Чтобы получить список расположений групп ресурсов, можно выполнить команду `az account list-locations`. Затем вы можете использовать значение *name* из этого списка, чтобы указать, где нужно создать группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="aee2c-132">To get a list of resource group locations, you can call `az account list-locations` and use the *name* value from that list to specify where the resource group should be created.</span></span>

    ```bash
    # In this tutorial, "westus" is the resource group location
    # and "jg-test" is the resource group name.
    az group create -l <resource_group_location> -n <resource_group_name>
    ```

1. <span data-ttu-id="aee2c-133">Создание ресурса хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="aee2c-133">Create a key vault resource.</span></span> <span data-ttu-id="aee2c-134">Вам понадобится вернуться к хранилищу ключей позднее, поэтому не забудьте выбрать для него запоминающееся имя.</span><span class="sxs-lookup"><span data-stu-id="aee2c-134">You'll use your key vault name to refer to the key vault later, so be sure to choose a memorable name.</span></span>

    ```bash
    az keyvault create --name <your_keyvault_name>            \
                      --resource-group <your_resource_group> \
                      --location <location>                  \
                      --enabled-for-deployment true          \
                      --enabled-for-disk-encryption true     \
                      --enabled-for-template-deployment true \
                      --sku standard
    ```

1. <span data-ttu-id="aee2c-135">Предоставьте созданному ранее субъекту-службе соответствующие разрешения, чтобы он мог получить доступ к секретам Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="aee2c-135">Grant the appropriate permissions to the service principal that you created earlier, so that it can access the key vault secrets.</span></span> <span data-ttu-id="aee2c-136">В следующем примере кода используется значение *appId* из шага 1, на котором вы создали субъект-службу.</span><span class="sxs-lookup"><span data-stu-id="aee2c-136">The appId value in the following code is the *appId* value from step 1, where you created the service principal.</span></span> <span data-ttu-id="aee2c-137">То есть параметр *appId* на шаге 1 имел значение *5292398e-XXXX-40ce-XXXX-d49fXXXX9e79*, но вам следует использовать значение из собственных выходных данных командной строки.</span><span class="sxs-lookup"><span data-stu-id="aee2c-137">That is, the *appId* in step 1 was *5292398e-XXXX-40ce-XXXX-d49fXXXX9e79*, but you should use the value from your own terminal output.</span></span>

    ```bash
    az keyvault set-policy --name <your_keyvault_name>   \
                          --secret-permission get list  \
                          --spn <your_sp_appId_created_in_step1>
    ```

1. <span data-ttu-id="aee2c-138">Теперь вы можете передать секрет в хранилище ключей.</span><span class="sxs-lookup"><span data-stu-id="aee2c-138">Now you can push a secret into your key vault.</span></span> <span data-ttu-id="aee2c-139">Используйте имя *demo-key* и задайте для ключа значение *demo-value*:</span><span class="sxs-lookup"><span data-stu-id="aee2c-139">Use the key name *demo-key*, and set the value of the key to *demo-value*:</span></span>

    ```bash
    az keyvault secret set --name demo-key      \
                           --value demo-value   \
                           --vault-name <your_keyvault_name>  
    ```

<span data-ttu-id="aee2c-140">Вот и все!</span><span class="sxs-lookup"><span data-stu-id="aee2c-140">That's it!</span></span> <span data-ttu-id="aee2c-141">Теперь у вас есть хранилище ключей в Azure, содержащее один секрет.</span><span class="sxs-lookup"><span data-stu-id="aee2c-141">You now have a key vault running in Azure with a single secret.</span></span> <span data-ttu-id="aee2c-142">Далее можно клонировать этот репозиторий и настроить его для использования этого ресурса в вашем приложении.</span><span class="sxs-lookup"><span data-stu-id="aee2c-142">You can now clone this repo and configure it to use this resource in your app.</span></span>

## <a name="get-up-and-running-locally"></a><span data-ttu-id="aee2c-143">Настройка и запуск на локальном компьютере</span><span class="sxs-lookup"><span data-stu-id="aee2c-143">Get up and running locally</span></span>

<span data-ttu-id="aee2c-144">В этом примере используется приложение, доступное на веб-сайте GitHub, поэтому вы можете просто клонировать это приложения и затем пошагово изучать код.</span><span class="sxs-lookup"><span data-stu-id="aee2c-144">This example is based on a sample application that's available on GitHub, so you'll clone that application and then step through the code.</span></span> 

1. <span data-ttu-id="aee2c-145">Чтобы клонировать код на свой компьютер, введите следующие команды:</span><span class="sxs-lookup"><span data-stu-id="aee2c-145">Clone the code onto your machine by entering the following commands:</span></span>

    `git clone https://github.com/Azure-Samples/microprofile-configsource-keyvault.git`

    `cd microprofile-configsource-keyvault`

1. <span data-ttu-id="aee2c-146">Перейдите к файлу *src/main/resources/META-INF/microprofile-config.properties*, а затем измените свойства в файле *microprofile-config.properties*, используя значения, полученные ранее.</span><span class="sxs-lookup"><span data-stu-id="aee2c-146">Go to *src/main/resources/META-INF/microprofile-config.properties*, and then change the properties in the *microprofile-config.properties* file by using the values from the previous steps.</span></span>

1. <span data-ttu-id="aee2c-147">Попробуйте запустить сервер при помощи команды `mvn clean package payara-micro:start`.</span><span class="sxs-lookup"><span data-stu-id="aee2c-147">Try running the server by using `mvn clean package payara-micro:start`.</span></span>

1. <span data-ttu-id="aee2c-148">Попробуйте открыть адрес [http://localhost:8080/keyvault-configsource/api/config](http://localhost:8080/keyvault-configsource/api/config) в веб-браузере.</span><span class="sxs-lookup"><span data-stu-id="aee2c-148">Try accessing [http://localhost:8080/keyvault-configsource/api/config](http://localhost:8080/keyvault-configsource/api/config) in your web browser.</span></span> <span data-ttu-id="aee2c-149">Вы должны увидеть простой ответ, который продемонстрирует значения, считываемые из хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="aee2c-149">You should see a simple response that demonstrates values that are being read from your key vault.</span></span>

## <a name="summary"></a><span data-ttu-id="aee2c-150">Сводка</span><span class="sxs-lookup"><span data-stu-id="aee2c-150">Summary</span></span>

<span data-ttu-id="aee2c-151">В этом примере приложения используется сочетание API MicroProfile Config, Azure Key Vault и бесплатной библиотеки [microprofile-config-keyvault](https://github.com/Azure/azure-microprofile/tree/master/microprofile-config-keyvault) с открытым кодом для простого добавления данных конфигурации и секретов в ваши веб-службы MicroProfile.</span><span class="sxs-lookup"><span data-stu-id="aee2c-151">This sample application combines the MicroProfile Config API, Azure Key Vault, and the free and open source [microprofile-config-keyvault](https://github.com/Azure/azure-microprofile/tree/master/microprofile-config-keyvault) library to enable easy injection of configuration data and secrets into your MicroProfile web services.</span></span>
