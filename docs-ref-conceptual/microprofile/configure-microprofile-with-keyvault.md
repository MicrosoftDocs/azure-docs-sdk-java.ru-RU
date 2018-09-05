---
title: Настройка MicroProfile для использования с Azure Key Vault
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
ms.openlocfilehash: fa93788f9b600d963f35ea599a58d309d3a3ee52
ms.sourcegitcommit: 77dc6c03a2e6264df688d91a04fc6b40950779ef
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2018
ms.locfileid: "43240827"
---
# <a name="configure-microprofile-with-azure-key-vault"></a><span data-ttu-id="4d7b3-103">Настройка MicroProfile для использования с Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="4d7b3-103">Configure MicroProfile with Azure Key Vault</span></span>

<span data-ttu-id="4d7b3-104">В этом руководстве мы продемонстрируем, как настроить приложение [MicroProfile](http://microprofile.io), чтобы получать секреты из [Azure Key Vault](https://azure.microsoft.com/services/key-vault/) с использованием программных интерфейсов [API MicroProfile Config](https://microprofile.io/project/eclipse/microprofile-config) для создания прямого соединения с Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="4d7b3-104">This tutorial will demonstrate how to configure a [MicroProfile](http://microprofile.io) application to retrieve secrets from [Azure Key Vault](https://azure.microsoft.com/services/key-vault/) using the [MicroProfile Config APIs](https://microprofile.io/project/eclipse/microprofile-config) to create a direct connection to Azure Key Vault.</span></span> <span data-ttu-id="4d7b3-105">Программные интерфейсы API MicroProfile Config предоставляют разработчикам стандартные средства для добавления данных конфигурации в микрослужбы и получения этих данных.</span><span class="sxs-lookup"><span data-stu-id="4d7b3-105">By using the MicroProfile Config APIs, developers benefit from a standard API for retrieving and injecting configuration data into their microservices.</span></span>

<span data-ttu-id="4d7b3-106">Прежде чем начать, рассмотрим вкратце те возможности, которые предоставляет сочетание Azure Key Vault и API MicroProfile Config при написании кода.</span><span class="sxs-lookup"><span data-stu-id="4d7b3-106">Before we dive in, lets quickly take a look at what a combination of Azure Key Vault and the MicroProfile Config API enables us to write in our code.</span></span> <span data-ttu-id="4d7b3-107">Ниже приведен фрагмент кода, содержащего поле класса с аннотациями `@Inject` и `@ConfigProperty`.</span><span class="sxs-lookup"><span data-stu-id="4d7b3-107">Here's a code snippet of a field in a class that has been annotated with `@Inject` and `@ConfigProperty`.</span></span> <span data-ttu-id="4d7b3-108">Параметр `name`, указанный в аннотации, — это имя свойства, которое нужно найти в Azure Key Vault, а `defaultValue` — значение по умолчанию, которое будет использовано, если ключ не найден.</span><span class="sxs-lookup"><span data-stu-id="4d7b3-108">The `name` specified in the annotation is the name of the property to look up in Azure Key Vault, and the `defaultValue` is what will be set if the key is not discovered.</span></span> <span data-ttu-id="4d7b3-109">Теперь значение, хранящееся в Azure Key Vault, или значение по умолчанию будет автоматически добавлено в поле во время выполнения. Благодаря этому разработчикам больше не нужно передавать значения в конструкторах или методах задания, так как всю работу берет на себя MicroProfile.</span><span class="sxs-lookup"><span data-stu-id="4d7b3-109">The end result is that the value stored in Azure Key Vault, or the default value, will be injected automatically into the field at runtime, simplifying the life of developers as they no longer need to pass values around in constuctors and setter methods, instead leaving it to MicroProfile to handle.</span></span>

```java
@Inject
@ConfigProperty(name = "key-name", defaultValue = "Unknown")
String keyValue;
```

<span data-ttu-id="4d7b3-110">Также можно осуществлять доступ непосредственно к конфигурации MicroProfile, чтобы получать секреты по мере необходимости, например:</span><span class="sxs-lookup"><span data-stu-id="4d7b3-110">It is also possible to access the MicroProfile config directly, to request secrets as necessary, e.g.:</span></span>

```java
public class DemoClass {
    @Inject
    Config config;

    public void method() {
        System.out.println("Hello: " + config.getValue("key-name", String.class));
    }
}
```

<span data-ttu-id="4d7b3-111">В этом примере используется [Payara Micro](https://www.payara.fish/payara_micro) и [MicroProfile](https://microprofile.io/) для создания компактного файла Java WAR, который можно запускать локально на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="4d7b3-111">This sample makes use of [Payara Micro](https://www.payara.fish/payara_micro) and [MicroProfile](https://microprofile.io/) to create a tiny Java war file that can be run locally on your machine.</span></span> <span data-ttu-id="4d7b3-112">Упаковка кода в контейнер Docker и его отправка в Azure выходит за рамки нашего примера, но в конце этого руководства приведены ссылки на другие полезные руководства, в которых вы найдете нужную информацию.</span><span class="sxs-lookup"><span data-stu-id="4d7b3-112">It does not demonstrate how to dockerise or push the code to Azure, but the links section at the end of this tutorial has links to other useful tutorials that explain this.</span></span>

<span data-ttu-id="4d7b3-113">В этом примере используется бесплатная библиотека с открытым кодом, которая создает источник конфигурации (при помощи API MicroProfile Config) для Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="4d7b3-113">This sample makes use of a free and open source library that creats a config source (using the MicroProfile Config API) for Azure Key Vault.</span></span> <span data-ttu-id="4d7b3-114">Подробные сведения об этой библиотеке и ее код можно найти на [странице проекта на сайте GitHub](https://github.com/Azure/azure-microprofile/tree/master/microprofile-config-keyvault).</span><span class="sxs-lookup"><span data-stu-id="4d7b3-114">You can learn more about this library, and review the code, on the [project GitHub page](https://github.com/Azure/azure-microprofile/tree/master/microprofile-config-keyvault).</span></span> <span data-ttu-id="4d7b3-115">Благодаря использованию этой библиотеки в этом руководстве нам не нужно писать специальный код для Azure. Мы можем просто настроить библиотеку и добавить ключи в свой код.</span><span class="sxs-lookup"><span data-stu-id="4d7b3-115">By using this library, the code in this tutorial can simply focus on configuration of the library, followed by injecting keys into your code, and we don't need to write any Azure-specific code.</span></span>

<span data-ttu-id="4d7b3-116">Ниже описаны действия, необходимые для запуска этого кода на вашем локальном компьютере, начиная с создания ресурса Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="4d7b3-116">Here are the steps required to run this code on your local machine, starting with creating an Azure Key Vault resource.</span></span>

## <a name="creating-an-azure-key-vault-resource"></a><span data-ttu-id="4d7b3-117">Создание ресурса Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="4d7b3-117">Creating an Azure Key Vault resource</span></span>

<span data-ttu-id="4d7b3-118">При помощи Azure CLI мы создадим ресурс Azure Key Vault и добавим в него один секрет.</span><span class="sxs-lookup"><span data-stu-id="4d7b3-118">We will use the Azure CLI to create the Azure Key Vault resource and populate it with one secret.</span></span>

1. <span data-ttu-id="4d7b3-119">Сначала создадим субъект-службу Azure.</span><span class="sxs-lookup"><span data-stu-id="4d7b3-119">Firstly, lets create an Azure service principal.</span></span> <span data-ttu-id="4d7b3-120">Это позволит нам получить идентификатор клиента и ключ, необходимые для доступа к Azure Key Vault:</span><span class="sxs-lookup"><span data-stu-id="4d7b3-120">This will provide us with the client ID and key we need to access Key Vault:</span></span>

```bash
az login
az account set --subscription <subscription_id>

az ad sp create-for-rbac --name <service_principal_name>
```

<span data-ttu-id="4d7b3-121">Предположим, что на предыдущем этапе ми использовали в качестве имени субъекта-службы значение `microprofile-keyvault-service-principal`.</span><span class="sxs-lookup"><span data-stu-id="4d7b3-121">Lets say we use `microprofile-keyvault-service-principal` for the service principal name in the previous step.</span></span> <span data-ttu-id="4d7b3-122">Тогда ответ от Azure будет иметь следующий вид (значения немного отредактированы):</span><span class="sxs-lookup"><span data-stu-id="4d7b3-122">The response from Azure for doing this will be in the following, slightly censored, form:</span></span>

```json
{
  "appId": "5292398e-XXXX-40ce-XXXX-d49fXXXX9e79",
  "displayName": "microprofile-keyvault-service-principal",
  "name": "http://microprofile-keyvault-service-principal",
  "password": "9b217777-XXXX-4954-XXXX-deafXXXX790a",
  "tenant": "72f988bf-XXXX-41af-XXXX-2d7cd011db47"
}
```

<span data-ttu-id="4d7b3-123">Обратите внимание на значения `appID` и `password`. Они будут использованы позднее для параметров `client ID` и `key` соответственно.</span><span class="sxs-lookup"><span data-stu-id="4d7b3-123">Of particular note here is the `appID` and `password` values - these are what we will use later on as `client ID` and `key`, respectively.</span></span>

<span data-ttu-id="4d7b3-124">После создания субъекта-службы мы дополнительно можем создать группу ресурсов (можно пропустить этот шаг, если у вас уже есть группа ресурсов, которую вы планируете использовать).</span><span class="sxs-lookup"><span data-stu-id="4d7b3-124">Now that we have created a service principal, we can optionally create a resource group (if you already have one you want to use, you can skip this step).</span></span> <span data-ttu-id="4d7b3-125">Чтобы получить список расположений групп ресурсов, можно выполнить команду `az account list-locations`. Затем вы можете использовать значение `name` из этого списка, чтобы указать, где нужно создать группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="4d7b3-125">Note that to get a list of resource group locations, you can call `az account list-locations` and use the `name` value from that list to specify where the resource group should be created.</span></span>

```bash
# For this tutorial, the author chose to use `westus`
# and `jg-test` for the resource group name.
az group create -l <resource_group_location> -n <resource_group_name>
```

<span data-ttu-id="4d7b3-126">Теперь мы создадим ресурс Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="4d7b3-126">We now create an Azure Key Vault resource.</span></span> <span data-ttu-id="4d7b3-127">Обратите внимание, что имя хранилища ключей Azure Key Vault будет позднее использоваться для доступа к этому хранилищу. Поэтому выберите имя, которое легко запомнить.</span><span class="sxs-lookup"><span data-stu-id="4d7b3-127">Note that the Key Vault name is what you will use to reference the key vault later, so choose something memorable.</span></span>

```bash
az keyvault create --name <your_keyvault_name>            \
                   --resource-group <your_resource_group> \
                   --location <location>                  \
                   --enabled-for-deployment true          \
                   --enabled-for-disk-encryption true     \
                   --enabled-for-template-deployment true \
                   --sku standard
```

<span data-ttu-id="4d7b3-128">Нам также нужно предоставить созданному ранее субъекту-службе соответствующие разрешения, чтобы он мог осуществлять доступ к секретам Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="4d7b3-128">We also need to grant the appropriate permissions to the service principal we created earlier, so that it may access the Key Vault secrets.</span></span> <span data-ttu-id="4d7b3-129">Обратите внимание, что значение "appID" здесь — это значение `appId`, полученное при создании субъекта-службы ранее (т. е. `5292398e-XXXX-40ce-XXXX-d49fXXXX9e79`, но вам нужно использовать свое значение, полученное при выполнении соответствующей команды).</span><span class="sxs-lookup"><span data-stu-id="4d7b3-129">Note that the appID value is the `appId` value from above where we created the service principal (that is, `5292398e-XXXX-40ce-XXXX-d49fXXXX9e79` - but use the value from your terminal output).</span></span>

```bash
az keyvault set-policy --name <your_keyvault_name>   \
                       --secret-permission get list  \
                       --spn <your_sp_appId_created_in_step1>
```

<span data-ttu-id="4d7b3-130">На этом этапе мы можем отправить секрет в Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="4d7b3-130">We are now at the point where we can push a secret into Key Vault.</span></span> <span data-ttu-id="4d7b3-131">Используем имя ключа `demo-key` и его значение `demo-value`:</span><span class="sxs-lookup"><span data-stu-id="4d7b3-131">Lets use the key name `demo-key`, and set the value of the key to be `demo-value`:</span></span>

```bash
az keyvault secret set --name demo-key      \
                       --value demo-value   \
                       --vault-name <your_keyvault_name>  
```

<span data-ttu-id="4d7b3-132">Вот и все!</span><span class="sxs-lookup"><span data-stu-id="4d7b3-132">That's it!</span></span> <span data-ttu-id="4d7b3-133">Теперь у нас есть хранилище ключей Azure Key Vault с одним секретом.</span><span class="sxs-lookup"><span data-stu-id="4d7b3-133">We now have Key Vault running in Azure with a single secret.</span></span> <span data-ttu-id="4d7b3-134">Далее мы можем клонировать нужный репозиторий и настроить его для использования этого ресурса в нашем приложении.</span><span class="sxs-lookup"><span data-stu-id="4d7b3-134">We can now clone this repo and configure it to use this resource in our app.</span></span>

## <a name="getting-up-and-running-locally"></a><span data-ttu-id="4d7b3-135">Настройка и запуск на локальном компьютере</span><span class="sxs-lookup"><span data-stu-id="4d7b3-135">Getting up and running locally</span></span>

<span data-ttu-id="4d7b3-136">Наш пример построен на основе демонстрационного приложения, доступного на сайте GitHub, поэтому мы клонируем это приложение и пошагово выполним нужный код.</span><span class="sxs-lookup"><span data-stu-id="4d7b3-136">This example is based on a sample application available on GitHub, so we will clone that and then step through the code.</span></span> <span data-ttu-id="4d7b3-137">Чтобы клонировать код на свой компьютер, выполните следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="4d7b3-137">Follow the steps below to get the code cloned onto your machine:</span></span>

1. `git clone https://github.com/Azure-Samples/microprofile-configsource-keyvault.git`

1. `cd microprofile-configsource-keyvault`

1. <span data-ttu-id="4d7b3-138">Перейдите к расположению `src/main/resources/META-INF/microprofile-config.properties` и измените файл microprofile-config.properties, указав сведения, полученные ранее.</span><span class="sxs-lookup"><span data-stu-id="4d7b3-138">Navigate to `src/main/resources/META-INF/microprofile-config.properties` and change the properties in microprofile-config.properties file with details from above.</span></span>

1. <span data-ttu-id="4d7b3-139">Попробуйте запустить сервер при помощи команды `mvn clean package payara-micro:start`.</span><span class="sxs-lookup"><span data-stu-id="4d7b3-139">Try running the server using `mvn clean package payara-micro:start`</span></span>

1. <span data-ttu-id="4d7b3-140">Попытайтесь открыть адрес [http://localhost:8080/keyvault-configsource/api/config](http://localhost:8080/keyvault-configsource/api/config) в своем веб-браузере. Должен отобразиться простой ответ, содержащий значения, полученные из Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="4d7b3-140">Try accessing [http://localhost:8080/keyvault-configsource/api/config](http://localhost:8080/keyvault-configsource/api/config) in your web browser - you should see a simple response that demonstrates values being read from Azure Key Vault.</span></span>

## <a name="summary"></a><span data-ttu-id="4d7b3-141">Сводка</span><span class="sxs-lookup"><span data-stu-id="4d7b3-141">Summary</span></span>

<span data-ttu-id="4d7b3-142">В этом примере приложения используется сочетание API MicroProfile Config, Azure Key Vault и бесплатной библиотеки [microprofile-config-keyvault](https://github.com/Azure/azure-microprofile/tree/master/microprofile-config-keyvault) с открытым кодом для простого добавления данных конфигурации и секретов в веб-службы MicroProfile.</span><span class="sxs-lookup"><span data-stu-id="4d7b3-142">This sample application bakes together the MicroProfile Config API, Azure Key Vault, and the free and open source [microprofile-config-keyvault](https://github.com/Azure/azure-microprofile/tree/master/microprofile-config-keyvault) library to enable easy injection of configuration data and secrets into our MicroProfile web services.</span></span>
