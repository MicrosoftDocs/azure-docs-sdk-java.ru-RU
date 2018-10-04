---
title: Библиотеки Центра Интернета вещей для Java
description: Справочная документация по библиотекам Центра Интернета вещей для Java
keywords: Azure, Java, SDK, API, event, IoT, streams, devices, iot hub
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 07/20/2017
ms.topic: article
ms.technology: azure
ms.devlang: java
ms.service: iot-hub
ms.openlocfilehash: 497b2a72d851b8e43a48384c6f1a160e8a38cbe6
ms.sourcegitcommit: bb7286fad75a2bb43e6ce1a8f1b09e701147c9f9
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/02/2018
ms.locfileid: "48047151"
---
# <a name="azure-iot-libraries-for-java"></a>Библиотеки Интернета вещей Azure для Java

Подключайте, отслеживайте и администрируйте миллионы ресурсов Интернета вещей с помощью [Центра Интернета вещей](https://docs.microsoft.com/azure/iot-hub/iot-hub-what-is-iot-hub).

Чтобы приступить к работе с Центром Интернета вещей, см. инструкции по [подключению устройств к Центру Интернета вещей с помощью Java](/azure/iot-hub/iot-hub-java-java-getstarted).

## <a name="iot-service-library"></a>Библиотека службы Интернета вещей

Регистрируйте устройства и отправляйте сообщения из облака в зарегистрированные устройства с помощью библиотеки службы Интернета вещей.

[Добавьте зависимость](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) в файл Maven `pom.xml`, чтобы использовать клиентскую библиотеку в проекте.  

```XML
<dependency>
    <groupId>com.microsoft.azure.sdk.iot</groupId>
    <artifactId>iot-service-client</artifactId>
    <version>1.6.23</version>
</dependency>
```   

## <a name="iot-device-library"></a>Библиотека устройств Интернета вещей

Отправляйте сообщения в облако и получайте их на устройствах с помощью библиотеки устройств Интернета вещей.

[Добавьте зависимость](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) в файл Maven `pom.xml`, чтобы использовать клиентскую библиотеку в проекте.  

```XML
<dependency>
    <groupId>com.microsoft.azure.sdk.iot</groupId>
    <artifactId>iot-device-client</artifactId>
    <version>1.3.31</version>
</dependency>
```

> [!div class="nextstepaction"]
> [Обзор клиентских API-интерфейсов](/java/api/overview/azure/iot/client)   

## <a name="example"></a>Пример

Отправляйте сообщения из Центра Интернета вещей на устройства.

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


## <a name="samples"></a>Примеры

[Примеры устройств Интернета вещей](https://github.com/Azure/azure-iot-sdk-java/tree/master/device/iot-device-samples)     
[Примеры службы Интернета вещей](https://github.com/Azure/azure-iot-sdk-java/tree/master/service/iot-service-samples)

Ознакомьтесь с [примерами кода Java для Интернета вещей Azure](https://azure.microsoft.com/resources/samples/?platform=java&term=iot), которые можно использовать в своих приложениях.
