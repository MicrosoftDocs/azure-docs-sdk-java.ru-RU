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
# <a name="configure-microprofile-by-using-azure-key-vault"></a>Настройка MicroProfile с помощью Azure Key Vault

В этой статье показано, как настроить приложение [MicroProfile](http://microprofile.io) на получение секретов из [хранилища ключей Azure](https://azure.microsoft.com/services/key-vault/). В этом процессе [API-интерфейсы конфигурации MicroProfile](https://microprofile.io/project/eclipse/microprofile-config) используется для создания прямого подключения к хранилищу ключей Azure. API-интерфейсы MicroProfile Config предоставляют разработчикам стандартные средства для добавления данных конфигурации в микрослужбы и получения этих данных.

Прежде чем начать, посмотрите, какое сочетание Azure Key Vault и API конфигурации MicroProfile позволяет написать нужный код. Следующий фрагмент кода из поля в классе, который объявлен в `@Inject` и `@ConfigProperty`. Параметр *name*, указанный в объявлении, — это имя свойства, которое нужно найти в хранилище ключей, а *defaultValue* — значение по умолчанию, которое будет использовано, если ключ не будет найден. Результатом является то, что значение, которое хранится в хранилище ключей, или значение по умолчанию, автоматически добавляется в поле во время выполнения. Это действие может существенно упростить жизнь, так как вам больше не нужно передавать значения в конструкторы и методы заданий. Вместо этого эту задачу берет на себя MicroProfile.

```java
@Inject
@ConfigProperty(name = "key-name", defaultValue = "Unknown")
String keyValue;
```

Чтобы запросить секреты, при необходимости можно также обращаться к конфигурации MicroProfile напрямую. Например:

```java
public class DemoClass {
    @Inject
    Config config;

    public void method() {
        System.out.println("Hello: " + config.getValue("key-name", String.class));
    }
}
```

В этом примере кода используется [Payara Micro](https://www.payara.fish/payara_micro) и [MicroProfile](https://microprofile.io/) для создания файла требования Tiny Java веб-приложения (WAR), который можно запустить локально на вашем компьютере. Упаковка кода в контейнер Docker и его отправка в Azure выходит за рамки нашего примера, но в конце этой статьи приведены ссылки на другие полезные руководства, в которых вы найдете нужную информацию.

В примере используется открытая и бесплатная библиотека, которая создает источник конфигурации (с помощью API конфигурации MicroProfile) в хранилище ключей. Подробные сведения об этой библиотеке и ее код можно найти на [странице проекта на сайте GitHub](https://github.com/Azure/azure-microprofile/tree/master/microprofile-config-keyvault). При использовании этой библиотеки код в этом руководстве может упростить работу с конфигурацией библиотеки и дальнейшее внедрение ключей в код. Благодаря этому нет необходимости писать код специально для Azure.

Для выполнения этого кода на локальном компьютере начните с создания ресурса хранилища ключей, а затем следуйте инструкциям в следующих разделах.

## <a name="create-a-key-vault-resource"></a>Создание ресурса хранилища ключей

В этом разделе для создания ресурса хранилища ключей и его заполнения одним секретом используется Azure CLI.

1. Создайте субъект-службу Azure. На этом шаге вы получите идентификатор клиента и ключ, который необходим, чтобы получить доступ к хранилищу ключей:

    ```bash
    az login
    az account set --subscription <subscription_id>

    az ad sp create-for-rbac --name <service_principal_name>
    ```

    Используйте, например, команду *microprofile-keyvault-service-principal*, чтобы заменить *\<имя_субъекта-службы>* , созданной ранее. Ответ Azure будет примерно таким:

    ```json
    {
      "appId": "5292398e-XXXX-40ce-XXXX-d49fXXXX9e79",
      "displayName": "microprofile-keyvault-service-principal",
      "name": "http://microprofile-keyvault-service-principal",
      "password": "9b217777-XXXX-4954-XXXX-deafXXXX790a",
      "tenant": "72f988bf-XXXX-41af-XXXX-2d7cd011db47"
    }
    ```

    Обратите отдельное внимание на значения *appId* и *password*. Позднее в этой статье они будут использоваться в качестве *идентификатора клиента* и *ключа*.

1. Теперь, когда вы создали субъект-службу, можно создать группу ресурсов (необязательно). Если у вас уже есть группа ресурсов, которую вы хотите использовать, этот шаг можно пропустить. Чтобы получить список расположений групп ресурсов, можно выполнить команду `az account list-locations`. Затем вы можете использовать значение *name* из этого списка, чтобы указать, где нужно создать группу ресурсов.

    ```bash
    # In this tutorial, "westus" is the resource group location
    # and "jg-test" is the resource group name.
    az group create -l <resource_group_location> -n <resource_group_name>
    ```

1. Создание ресурса хранилища ключей. Вам понадобится вернуться к хранилищу ключей позднее, поэтому не забудьте выбрать для него запоминающееся имя.

    ```bash
    az keyvault create --name <your_keyvault_name>            \
                      --resource-group <your_resource_group> \
                      --location <location>                  \
                      --enabled-for-deployment true          \
                      --enabled-for-disk-encryption true     \
                      --enabled-for-template-deployment true \
                      --sku standard
    ```

1. Предоставьте созданному ранее субъекту-службе соответствующие разрешения, чтобы он мог получить доступ к секретам Azure Key Vault. В следующем примере кода используется значение *appId* из шага 1, на котором вы создали субъект-службу. То есть параметр *appId* на шаге 1 имел значение *5292398e-XXXX-40ce-XXXX-d49fXXXX9e79*, но вам следует использовать значение из собственных выходных данных командной строки.

    ```bash
    az keyvault set-policy --name <your_keyvault_name>   \
                          --secret-permission get list  \
                          --spn <your_sp_appId_created_in_step1>
    ```

1. Теперь вы можете передать секрет в хранилище ключей. Используйте имя *demo-key* и задайте для ключа значение *demo-value*:

    ```bash
    az keyvault secret set --name demo-key      \
                           --value demo-value   \
                           --vault-name <your_keyvault_name>  
    ```

Вот и все! Теперь у вас есть хранилище ключей в Azure, содержащее один секрет. Далее можно клонировать этот репозиторий и настроить его для использования этого ресурса в вашем приложении.

## <a name="get-up-and-running-locally"></a>Настройка и запуск на локальном компьютере

В этом примере используется приложение, доступное на веб-сайте GitHub, поэтому вы можете просто клонировать это приложения и затем пошагово изучать код. 

1. Чтобы клонировать код на свой компьютер, введите следующие команды:

    `git clone https://github.com/Azure-Samples/microprofile-configsource-keyvault.git`

    `cd microprofile-configsource-keyvault`

1. Перейдите к файлу *src/main/resources/META-INF/microprofile-config.properties*, а затем измените свойства в файле *microprofile-config.properties*, используя значения, полученные ранее.

1. Попробуйте запустить сервер при помощи команды `mvn clean package payara-micro:start`.

1. Попробуйте открыть адрес [http://localhost:8080/keyvault-configsource/api/config](http://localhost:8080/keyvault-configsource/api/config) в веб-браузере. Вы должны увидеть простой ответ, который продемонстрирует значения, считываемые из хранилища ключей.

## <a name="summary"></a>Сводка

В этом примере приложения используется сочетание API MicroProfile Config, Azure Key Vault и бесплатной библиотеки [microprofile-config-keyvault](https://github.com/Azure/azure-microprofile/tree/master/microprofile-config-keyvault) с открытым кодом для простого добавления данных конфигурации и секретов в ваши веб-службы MicroProfile.
