---
title: "Библиотеки Центра Интернета вещей для Java"
description: "Справочная документация по библиотекам Центра Интернета вещей для Java"
keywords: Azure, Java, SDK, API, event, IoT, streams, devices, iot hub
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 07/20/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: iot-hub
ms.openlocfilehash: c1af3dae0fe37eb4919db02da87beed193c547a7
ms.sourcegitcommit: acc83bb537d77568b2a5427479d6354d6ae30885
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/03/2017
---
# <a name="azure-iot-libraries-for-java"></a><span data-ttu-id="40d7c-104">Библиотеки Интернета вещей Azure для Java</span><span class="sxs-lookup"><span data-stu-id="40d7c-104">Azure IoT libraries for Java</span></span>

<span data-ttu-id="40d7c-105">Подключайте, отслеживайте и администрируйте миллионы ресурсов Интернета вещей с помощью [Центра Интернета вещей](https://docs.microsoft.com/azure/iot-hub/iot-hub-what-is-iot-hub).</span><span class="sxs-lookup"><span data-stu-id="40d7c-105">Connect, monitor, and control Internet of Things assets with [Azure IoT Hub](https://docs.microsoft.com/azure/iot-hub/iot-hub-what-is-iot-hub).</span></span>

<span data-ttu-id="40d7c-106">Чтобы приступить к работе с Центром Интернета вещей, см. инструкции по [подключению устройств к Центру Интернета вещей с помощью Java](/azure/iot-hub/iot-hub-java-java-getstarted).</span><span class="sxs-lookup"><span data-stu-id="40d7c-106">To get started with Azure IoT Hub, see [Connect your device to your IoT hub using Java](/azure/iot-hub/iot-hub-java-java-getstarted).</span></span>

## <a name="iot-service-library"></a><span data-ttu-id="40d7c-107">Библиотека службы Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="40d7c-107">IoT Service library</span></span>

<span data-ttu-id="40d7c-108">Регистрируйте устройства и отправляйте сообщения из облака в зарегистрированные устройства с помощью библиотеки службы Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="40d7c-108">Register devices and send messages from the cloud to registered devices using the IoT Service library.</span></span>

<span data-ttu-id="40d7c-109">[Добавьте зависимость](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) в файл Maven `pom.xml`, чтобы использовать клиентскую библиотеку в проекте.</span><span class="sxs-lookup"><span data-stu-id="40d7c-109">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the client library in your project.</span></span>  

```XML
<dependency>
    <groupId>com.microsoft.azure.sdk.iot</groupId>
    <artifactId>iot-service-client</artifactId>
    <version>1.6.23</version>
</dependency>
```   

## <a name="iot-device-library"></a><span data-ttu-id="40d7c-110">Библиотека устройств Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="40d7c-110">Iot Device library</span></span>

<span data-ttu-id="40d7c-111">Отправляйте сообщения в облако и получайте их на устройствах с помощью библиотеки устройств Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="40d7c-111">Send messages to the cloud and receive messages on devices using the IoT Device library.</span></span>

<span data-ttu-id="40d7c-112">[Добавьте зависимость](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) в файл Maven `pom.xml`, чтобы использовать клиентскую библиотеку в проекте.</span><span class="sxs-lookup"><span data-stu-id="40d7c-112">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the client library in your project.</span></span>  

```XML
<dependency>
    <groupId>com.microsoft.azure.sdk.iot</groupId>
    <artifactId>iot-device-client</artifactId>
    <version>1.3.31</version>
</dependency>
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="40d7c-113">Обзор клиентских API-интерфейсов</span><span class="sxs-lookup"><span data-stu-id="40d7c-113">Explore the Client APIs</span></span>](/java/api/overview/azure/iot/clientlibrary)   

## <a name="example"></a><span data-ttu-id="40d7c-114">Пример</span><span class="sxs-lookup"><span data-stu-id="40d7c-114">Example</span></span>

<span data-ttu-id="40d7c-115">Отправляйте сообщения из Центра Интернета вещей на устройства.</span><span class="sxs-lookup"><span data-stu-id="40d7c-115">Send a message from Azure IoT Hub to a device.</span></span>

```java
Message messageToSend = new Message(messageText);
messageToSend.setDeliveryAcknowledgement(DeliveryAcknowledgement.Full);
messageToSend.setMessageId(java.util.UUID.randomUUID().toString());

// set message properties
Map<String, String> propertiesToSend = new HashMap<String, String>();
propertiesToSend.put(messagePropertyKey,messagePropertyKey);
messageToSend.setProperties(propertiesToSend);

CompletableFuture<Void> future = serviceClient.sendAsync(deviceId, messageToSend);
try {
    future.get();
}
catch (ExecutionException e) {
    System.out.println("Exception : " + e.getMessage());
}
```


## <a name="samples"></a><span data-ttu-id="40d7c-116">Примеры</span><span class="sxs-lookup"><span data-stu-id="40d7c-116">Samples</span></span>

<span data-ttu-id="40d7c-117">[Примеры устройств Интернета вещей](https://github.com/Azure/azure-iot-sdk-java/tree/master/device/iot-device-samples)   </span><span class="sxs-lookup"><span data-stu-id="40d7c-117">[IoT Device samples](https://github.com/Azure/azure-iot-sdk-java/tree/master/device/iot-device-samples)   </span></span>  
[<span data-ttu-id="40d7c-118">Примеры службы Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="40d7c-118">IoT Service samples</span></span>](https://github.com/Azure/azure-iot-sdk-java/tree/master/service/iot-service-samples)

<span data-ttu-id="40d7c-119">Ознакомьтесь с [примерами кода Java для Интернета вещей Azure](https://azure.microsoft.com/resources/samples/?platform=java&term=iot), которые можно использовать в своих приложениях.</span><span class="sxs-lookup"><span data-stu-id="40d7c-119">Explore more [sample Java code for Azure IoT](https://azure.microsoft.com/resources/samples/?platform=java&term=iot) you can use in your apps.</span></span>
