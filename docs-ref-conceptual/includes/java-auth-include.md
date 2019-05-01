---
ms.openlocfilehash: 0a9b06932baa51c3cf003a4485a3a25261ffe91d
ms.sourcegitcommit: 115f4c8ad07a11f17d79e9d945d63917836b11c8
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "61592514"
---
Создайте [файл аутентификации](../java-sdk-azure-authenticate.md#mgmt-file), экспортируйте переменную среды `AZURE_AUTH_LOCATION` в командной строке и укажите полный путь к файлу.

```bash
export AZURE_AUTH_LOCATION=/Users/raisa/azure.auth
```

Файл аутентификации позволяет настроить объект `Azure` точки входа, используемый библиотеками управления для определения, создания и настройки ресурсов Azure.

```java
// pull in the location of the security file from the environment 
final File credFile = new File(System.getenv("AZURE_AUTH_LOCATION"));

Azure azure = Azure
        .configure()
        .withLogLevel(LogLevel.NONE)
        .authenticate(credFile)
        .withDefaultSubscription();
```

См. [дополнительные сведения](../java-sdk-azure-authenticate.md#mgmt-auth) о способах аутентификации при использовании библиотек управления Azure для Java.