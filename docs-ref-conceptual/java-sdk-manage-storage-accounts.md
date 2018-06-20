---
title: Управление учетными записями хранения Azure с помощью Java | Документация Майкрософт
description: Пример кода для управления учетными записями хранения Azure с помощью пакета Azure SDK для Java
author: rloutlaw
manager: douge
ms.assetid: 49be8b66-3b56-4c10-8f14-9d326d815cb4
ms.devlang: java
ms.topic: article
ms.service: Azure
ms.technology: Azure
ms.date: 3/30/2017
ms.author: routlaw;asirveda
ms.openlocfilehash: 5945164b2b04e1fa9169590a71f6c5f9f45842d6
ms.sourcegitcommit: 1500f341a96d9da461c288abf4baf79f494ae662
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/28/2017
ms.locfileid: "21931060"
---
# <a name="manage-azure-storage-accounts-from-your-java-applications"></a><span data-ttu-id="87906-103">Управление учетными записями хранения Azure из приложений Java</span><span class="sxs-lookup"><span data-stu-id="87906-103">Manage Azure storage accounts from your Java applications</span></span>

<span data-ttu-id="87906-104">[В этом примере кода](https://github.com/Azure-Samples/storage-java-manage-storage-accounts) создается учетная запись [хранения Azure](https://docs.microsoft.com/azure/storage/storage-introduction) и используются ключи доступа учетной записи с помощью [библиотек управления Java](https://github.com/Azure/azure-sdk-for-java).</span><span class="sxs-lookup"><span data-stu-id="87906-104">[This sample](https://github.com/Azure-Samples/storage-java-manage-storage-accounts) creates an [Azure Storage](https://docs.microsoft.com/azure/storage/storage-introduction) account and works with the account access keys using the [Java management libraries](https://github.com/Azure/azure-sdk-for-java).</span></span> 

## <a name="run-the-sample"></a><span data-ttu-id="87906-105">Запуск примера</span><span class="sxs-lookup"><span data-stu-id="87906-105">Run the sample</span></span>

<span data-ttu-id="87906-106">Создайте [файл проверки подлинности](https://github.com/Azure/azure-sdk-for-java/blob/master/AUTH.md), задайте переменную среды `AZURE_AUTH_LOCATION` и укажите полный путь к файлу на компьютере.</span><span class="sxs-lookup"><span data-stu-id="87906-106">Create an [authentication file](https://github.com/Azure/azure-sdk-for-java/blob/master/AUTH.md) and set an environment variable `AZURE_AUTH_LOCATION` with the full path to the file on your computer.</span></span> <span data-ttu-id="87906-107">Далее выполните:</span><span class="sxs-lookup"><span data-stu-id="87906-107">Then run:</span></span>

```
git clone https://github.com/Azure-Samples/storage-java-manage-storage-accounts.git
cd storage-java-manage-storage-accounts
mvn clean compile exec:java
```

<span data-ttu-id="87906-108">Просмотрите [полный пример кода на GitHub](https://github.com/Azure-Samples/storage-java-manage-storage-accounts).</span><span class="sxs-lookup"><span data-stu-id="87906-108">View the [complete code sample on GitHub](https://github.com/Azure-Samples/storage-java-manage-storage-accounts).</span></span>

## <a name="authenticate-with-azure"></a><span data-ttu-id="87906-109">Проверка подлинности с помощью Azure</span><span class="sxs-lookup"><span data-stu-id="87906-109">Authenticate with Azure</span></span>

[!INCLUDE [auth-include](includes/java-auth-include.md)] 

## <a name="create-a-storage-account"></a><span data-ttu-id="87906-110">Создайте учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="87906-110">Create a storage account</span></span>

```java
// create a new storage account
StorageAccount storageAccount = azure.storageAccounts().define(storageAccountName)
                    .withRegion(Region.US_EAST)
                    .withNewResourceGroup(rgName)
                    .create();
```

<span data-ttu-id="87906-111">Указанное имя хранилища должно быть уникальным в Azure и содержать только строчные буквы и цифры.</span><span class="sxs-lookup"><span data-stu-id="87906-111">The storage name provided must be unique across all names in Azure and contain only lowercase letters and numbers.</span></span> <span data-ttu-id="87906-112">Для этой учетной записи по умолчанию используется профиль производительности и репликации [Standard_GRS](https://docs.microsoft.com/azure/storage/storage-redundancy#geo-redundant-storage).</span><span class="sxs-lookup"><span data-stu-id="87906-112">The default performance and replication profile used for this account is [Standard_GRS](https://docs.microsoft.com/azure/storage/storage-redundancy#geo-redundant-storage).</span></span>

## <a name="list-keys-in-a-storage-account"></a><span data-ttu-id="87906-113">Получение списка ключей в учетной записи хранения</span><span class="sxs-lookup"><span data-stu-id="87906-113">List keys in a storage account</span></span>
```java
// list the name and value for each access key in the storage account
List<StorageAccountKey> storageAccountKeys = storageAccount.getKeys();
for(StorageAccountKey key : storageAccountKeys)    {
    System.out.println("Key name: " + key.keyName() + " with value "+ key.value());
}
```

<span data-ttu-id="87906-114">Для каждой учетной записи хранения Azure предоставляется два ключа, что позволяет повторно создать один ключ, а для доступа к хранилищу использовать другой.</span><span class="sxs-lookup"><span data-stu-id="87906-114">Two keys are provided in each Azure storage account so that you can regenerate one key while still allowing access to storage using the other key.</span></span>

## <a name="regenerate-a-key-in-a-storage-account"></a><span data-ttu-id="87906-115">Повторное создание ключа в учетной записи хранения</span><span class="sxs-lookup"><span data-stu-id="87906-115">Regenerate a key in a storage account</span></span>

```java
// regenerate the first key in a storage account and return an updated list of keys 
List<StorageAccountKey> updatedStorageAccountKeys =
    storageAccount.regenerateKey(storageAccountKeys.get(0).keyName());
```

<span data-ttu-id="87906-116">После повторного создания ключа вам потребуется обновить ключ во всех ресурсах и приложениях Azure.</span><span class="sxs-lookup"><span data-stu-id="87906-116">You must update all Azure resources and applications with the new key after generating a new one.</span></span>

## <a name="list-all-storage-accounts-in-a-resource-group"></a><span data-ttu-id="87906-117">Получение списка всех учетных записей хранения в группе ресурсов</span><span class="sxs-lookup"><span data-stu-id="87906-117">List all storage accounts in a resource group</span></span>
```java
// get a list of accounts in a resource group , log info about each one
List<StorageAccount> accounts = azure.storageAccounts().listByResourceGroup(rgName);
for (StorageAccount sa : accounts) {
    System.out.println("Storage Account " + sa.name() + " created @ " + sa.creationTime());
}
```

<span data-ttu-id="87906-118">На странице [com.microsoft.azure.management.storage.StorageAccount](https://docs.microsoft.com/java/api/com.microsoft.azure.management.storage._storage_account) доступен набор полезных методов для проверки настроек учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="87906-118">[com.microsoft.azure.management.storage.StorageAccount](https://docs.microsoft.com/java/api/com.microsoft.azure.management.storage._storage_account) provides a set of useful methods to inspect the configuration of a storage account.</span></span>

## <a name="delete-a-storage-account"></a><span data-ttu-id="87906-119">Удаление учетной записи хранения</span><span class="sxs-lookup"><span data-stu-id="87906-119">Delete a storage account</span></span>
```java
// delete by ID when you already have a storage account object
azure.storageAccounts().deleteById(storageAccount.id());

// delete by resource group and account name if you don't have an account object
azure.storageAccounts().deleteByResourceGroup(rgName,accountName);
```

> [!NOTE]
> <span data-ttu-id="87906-120">Учетные записи хранения с используемыми образами дисков, которые подключены к виртуальным машинам, или дисками, которые используются другими артефактами, невозможно удалить с помощью этих методов.</span><span class="sxs-lookup"><span data-stu-id="87906-120">Storage accounts with in-use disk images connected to virtual machines or disks in use by other artifacts may not remove with these methods.</span></span> <span data-ttu-id="87906-121">Отключите хранилище от этих ресурсов, чтобы удалить учетную запись.</span><span class="sxs-lookup"><span data-stu-id="87906-121">Detach the storage from these resources before removing the account.</span></span>

## <a name="sample-explanation"></a><span data-ttu-id="87906-122">Описание примера</span><span class="sxs-lookup"><span data-stu-id="87906-122">Sample explanation</span></span>

<span data-ttu-id="87906-123">[Пример кода на GitHub](https://github.com/Azure-Samples/storage-java-manage-storage-accounts) позволяет:</span><span class="sxs-lookup"><span data-stu-id="87906-123">[The sample code on GitHub](https://github.com/Azure-Samples/storage-java-manage-storage-accounts):</span></span>

- <span data-ttu-id="87906-124">создать учетную запись хранения;</span><span class="sxs-lookup"><span data-stu-id="87906-124">creates a storage account</span></span>
- <span data-ttu-id="87906-125">считывать и повторно создавать ключи доступа;</span><span class="sxs-lookup"><span data-stu-id="87906-125">reads and regenerates access keys</span></span>
- <span data-ttu-id="87906-126">выводить список всех учетных записей хранения в группе ресурсов;</span><span class="sxs-lookup"><span data-stu-id="87906-126">lists all storage accounts in a resource group</span></span>
- <span data-ttu-id="87906-127">удалить учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="87906-127">deletes the storage account</span></span> 

| <span data-ttu-id="87906-128">Класс, используемый в примере</span><span class="sxs-lookup"><span data-stu-id="87906-128">Class used in sample</span></span> | <span data-ttu-id="87906-129">Примечания</span><span class="sxs-lookup"><span data-stu-id="87906-129">Notes</span></span>
|-------|-------|
| [<span data-ttu-id="87906-130">StorageAccount</span><span class="sxs-lookup"><span data-stu-id="87906-130">StorageAccount</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.storage._storage_account)  | <span data-ttu-id="87906-131">Представляет учетную запись хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="87906-131">Representation of an Azure storage account.</span></span> <span data-ttu-id="87906-132">Чтобы получить сведения об учетной записи хранения, используйте методы в классе.</span><span class="sxs-lookup"><span data-stu-id="87906-132">Use the methods in the class to get information about the storage account.</span></span>
| [<span data-ttu-id="87906-133">StorageAccountKey</span><span class="sxs-lookup"><span data-stu-id="87906-133">StorageAccountKey</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.storage._storage_account_key) | <span data-ttu-id="87906-134">`StorageAccount.getKeys()` возвращает ключи учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="87906-134">`StorageAccount.getKeys()` returns the storage account keys.</span></span> <span data-ttu-id="87906-135">Используйте методы `regenerateKey` в `StorageAccount`, чтобы обновить ключи.</span><span class="sxs-lookup"><span data-stu-id="87906-135">Use the `regenerateKey` methods in `StorageAccount` to update the keys.</span></span>

## <a name="next-steps"></a><span data-ttu-id="87906-136">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="87906-136">Next steps</span></span>

[!INCLUDE [next-steps](includes/java-next-steps.md)]