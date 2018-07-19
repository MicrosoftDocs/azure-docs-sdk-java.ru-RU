---
title: Библиотеки Azure Active Directory для Java
description: Справочная документация по клиентской библиотеке Java и библиотекам управления Azure Active Directory
keywords: Azure, Java, SDK, API, SQL, authentication, AAD, Active Directory, Graph, OAuth 2.0
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 07/11/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: active-directory
ms.openlocfilehash: 4a610e2f0d9fb2e219c42155e2b0cb76fc78b09a
ms.sourcegitcommit: 5bfb3af5778167500a061157cbd0ad1cede8f90e
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/04/2018
ms.locfileid: "37799702"
---
# <a name="azure-active-directory-libraries-for-java"></a>Библиотеки Azure Active Directory для Java

## <a name="overview"></a>Обзор

Для входа пользователей в приложения и управления доступом к приложениям и API-интерфейсам можно использовать [Azure Active Directory](/azure/active-directory/active-directory-whatis).

Чтобы приступить к работе с Azure AD, ознакомьтесь со статьей [Вход в веб-приложение Java и выход из него с помощью Azure AD](/azure/active-directory/develop/active-directory-devquickstarts-webapp-java).

## <a name="client-library"></a>Клиентская библиотека

Настройте проверку подлинности с помощью OAuth2, OpenID Connect или Active Directory Graph и единый вход через [SAML 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-protocol-reference) с помощью библиотеки [Azure Active Directory Authentication Library (ADAL) для Java](https://github.com/AzureAD/azure-activedirectory-library-for-java).

[Добавьте зависимость](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) в файл Maven `pom.xml`, чтобы использовать клиентскую библиотеку в проекте.

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>adal4j</artifactId>
    <version>1.2.0</version>
</dependency>
```   

### <a name="example"></a>Пример

Получите маркер JSON Web Token (JWT) для пользователя в клиенте Active Directory с помощью [API Graph](https://docs.microsoft.com/azure/active-directory/develop/active-directory-graph-api) Azure Active Directory. Затем вы можете использовать этот маркер для проверки подлинности пользователя с помощью приложения или API.

```java
ExecutorService service = Executors.newFixedThreadPool(1);
AuthenticationContext context = new AuthenticationContext(AUTHORITY, false, service);
Future<AuthenticationResult> future = context.acquireToken(
    "https://graph.windows.net", YOUR_TENANT_ID, username, password,
    null);
AuthenticationResult result = future.get();
System.out.println("Access Token - " + result.getAccessToken());
System.out.println("Refresh Token - " + result.getRefreshToken());
System.out.println("ID Token - " + result.getIdToken());
```

## <a name="management-api"></a>API управления

Настройте [управление доступом на основе ролей](/azure/active-directory/role-based-access-control-what-is) и назначьте этим ролям удостоверения (например, удостоверения пользователей и [субъектов-служб](https://docs.microsoft.com/azure/active-directory/develop/active-directory-application-objects)) с помощью API управления. 

[Добавьте зависимость](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) в файл Maven `pom.xml`, чтобы использовать API управления в проекте.

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-graph-rbac</artifactId>
    <version>1.3.0</version>
</dependency>
```

### <a name="example"></a>Пример 

Создайте субъект-службу и назначьте ему роль участника.

```java
ServicePrincipal sp = Azure.servicePrincipals().define(spName)
    .withNewApplication("http://" + spName)
    .create();
RoleAssignment roleAssignment2 = authenticated.roleAssignments()
    .define("contribRoleAssignment")
    .forServicePrincipal(sp)
    .withBuiltInRole(BuiltInRole.CONTRIBUTOR)
    .withSubscriptionScope("862f67bc-d3ae-4243-bec7-3da6dca77717")
    .create();
```

> [!div class="nextstepaction"]
> [Обзор API-интерфейсов управления](/java/api/activedirectory/management)


## <a name="samples"></a>Примеры

[Manage groups, users, and roles](https://github.com/Azure-Samples/aad-java-manage-users-groups-and-roles)   (Управление группами, пользователями и ролями)  
[Sign-in and sign-out users in a Java web app](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect)   (Вход пользователей в веб-приложение Java и выход из него)  
[Access an API with Azure AD using a command line app](https://github.com/Azure-Samples/active-directory-java-native-headless)  (Использование приложения командной строки для доступа к API с помощью Azure AD)  
[Call the Active AD Graph API from your Java web app](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect) (Вызов API Graph Active AD из веб-приложения Java)  

Ознакомьтесь с другими [примерами кода Java для Azure AD](https://azure.microsoft.com/en-us/resources/samples/?term=active+directory&platform=java), которые можно использовать в приложениях.
