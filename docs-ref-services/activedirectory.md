---
title: "Библиотеки Azure Active Directory для Java"
description: "Справочная документация по клиентской библиотеке Java и библиотекам управления Azure Active Directory"
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
ms.openlocfilehash: 081b8455a6cd8f26ce714328d10ce25ea6a07e3b
ms.sourcegitcommit: 4b63ecd2c92a9115dfae018618e4e4046b061b3e
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/14/2017
---
# <a name="azure-active-directory-libraries-for-java"></a><span data-ttu-id="0ae88-104">Библиотеки Azure Active Directory для Java</span><span class="sxs-lookup"><span data-stu-id="0ae88-104">Azure Active Directory libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="0ae88-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="0ae88-105">Overview</span></span>

<span data-ttu-id="0ae88-106">Для входа пользователей в приложения и управления доступом к приложениям и API-интерфейсам можно использовать [Azure Active Directory](/azure/active-directory/active-directory-whatis).</span><span class="sxs-lookup"><span data-stu-id="0ae88-106">Sign-on users and control access to applications and APIs with [Azure Active Directory](/azure/active-directory/active-directory-whatis).</span></span>

<span data-ttu-id="0ae88-107">Чтобы приступить к работе с Azure AD, ознакомьтесь со статьей [Вход в веб-приложение Java и выход из него с помощью Azure AD](/azure/active-directory/develop/active-directory-devquickstarts-webapp-java).</span><span class="sxs-lookup"><span data-stu-id="0ae88-107">To get started with Azure AD, see [Java web app sign-in and sign-out with Azure AD](/azure/active-directory/develop/active-directory-devquickstarts-webapp-java).</span></span>

## <a name="client-library"></a><span data-ttu-id="0ae88-108">Клиентская библиотека</span><span class="sxs-lookup"><span data-stu-id="0ae88-108">Client library</span></span>

<span data-ttu-id="0ae88-109">Настройте проверку подлинности с помощью OAuth2, OpenID Connect или Active Directory Graph и единый вход через [SAML 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-protocol-reference) с помощью библиотеки [Azure Active Directory Authentication Library (ADAL) для Java](https://github.com/AzureAD/azure-activedirectory-library-for-java).</span><span class="sxs-lookup"><span data-stu-id="0ae88-109">Configure OAuth2, OpenID Connect, or Active Directory Graph authentication and [SAML 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-protocol-reference) single-sign on with the [Azure Active Directory authentication library (ADAL) for Java](https://github.com/AzureAD/azure-activedirectory-library-for-java).</span></span>

<span data-ttu-id="0ae88-110">[Добавьте зависимость](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) в файл Maven `pom.xml`, чтобы использовать клиентскую библиотеку в проекте.</span><span class="sxs-lookup"><span data-stu-id="0ae88-110">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the client library in your project.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>adal4j</artifactId>
    <version>1.2.0</version>
</dependency>
```   

### <a name="example"></a><span data-ttu-id="0ae88-111">Пример</span><span class="sxs-lookup"><span data-stu-id="0ae88-111">Example</span></span>

<span data-ttu-id="0ae88-112">Получите маркер JSON Web Token (JWT) для пользователя в клиенте Active Directory с помощью [API Graph](https://docs.microsoft.com/azure/active-directory/develop/active-directory-graph-api) Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="0ae88-112">Retrieve a JSON Web Token (JWT) for a user in your an Active Directory tenant using Azure Active Directory's [Graph API](https://docs.microsoft.com/azure/active-directory/develop/active-directory-graph-api).</span></span> <span data-ttu-id="0ae88-113">Затем вы можете использовать этот маркер для проверки подлинности пользователя с помощью приложения или API.</span><span class="sxs-lookup"><span data-stu-id="0ae88-113">This token can then be used to authenticate the user with an application or API.</span></span>

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

## <a name="management-api"></a><span data-ttu-id="0ae88-114">API управления</span><span class="sxs-lookup"><span data-stu-id="0ae88-114">Management API</span></span>

<span data-ttu-id="0ae88-115">Настройте [управление доступом на основе ролей](/azure/active-directory/role-based-access-control-what-is) и назначьте этим ролям удостоверения (например, удостоверения пользователей и [субъектов-служб](https://docs.microsoft.com/azure/active-directory/develop/active-directory-application-objects)) с помощью API управления.</span><span class="sxs-lookup"><span data-stu-id="0ae88-115">Configure [role based access control](/azure/active-directory/role-based-access-control-what-is) and assign identities (such as users and [service principals](https://docs.microsoft.com/azure/active-directory/develop/active-directory-application-objects)) to those roles with the management API.</span></span> 

<span data-ttu-id="0ae88-116">[Добавьте зависимость](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) в файл Maven `pom.xml`, чтобы использовать API управления в проекте.</span><span class="sxs-lookup"><span data-stu-id="0ae88-116">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the management API in your project.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-graph-rbac</artifactId>
    <version>1.3.0</version>
</dependency>
```

### <a name="example"></a><span data-ttu-id="0ae88-117">Пример</span><span class="sxs-lookup"><span data-stu-id="0ae88-117">Example</span></span> 

<span data-ttu-id="0ae88-118">Создайте субъект-службу и назначьте ему роль участника.</span><span class="sxs-lookup"><span data-stu-id="0ae88-118">Create a new service principal and assign it the Contributor role.</span></span>

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
> [<span data-ttu-id="0ae88-119">Обзор API-интерфейсов управления</span><span class="sxs-lookup"><span data-stu-id="0ae88-119">Explore the Management APIs</span></span>](/java/api/overview/azure/activedirectory/managementapi)


## <a name="samples"></a><span data-ttu-id="0ae88-120">Примеры</span><span class="sxs-lookup"><span data-stu-id="0ae88-120">Samples</span></span>

<span data-ttu-id="0ae88-121">[Manage groups, users, and roles](https://github.com/Azure-Samples/aad-java-browse-graph-and-manage-roles)   (Управление группами, пользователями и ролями)</span><span class="sxs-lookup"><span data-stu-id="0ae88-121">[Manage groups, users, and roles](https://github.com/Azure-Samples/aad-java-browse-graph-and-manage-roles)  </span></span>  
<span data-ttu-id="0ae88-122">[Sign-in and sign-out users in a Java web app](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect)   (Вход пользователей в веб-приложение Java и выход из него)</span><span class="sxs-lookup"><span data-stu-id="0ae88-122">[Sign-in and sign-out users in a Java web app](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect)  </span></span>  
<span data-ttu-id="0ae88-123">[Access an API with Azure AD using a command line app](https://github.com/Azure-Samples/active-directory-java-native-headless)  (Использование приложения командной строки для доступа к API с помощью Azure AD)</span><span class="sxs-lookup"><span data-stu-id="0ae88-123">[Access an API with Azure AD using a command line app](https://github.com/Azure-Samples/active-directory-java-native-headless) </span></span>  
<span data-ttu-id="0ae88-124">[Call the Active AD Graph API from your Java web app](https://github.com/Azure-Samples/active-directory-java-graphapi-web/) (Вызов API Graph Active AD из веб-приложения Java)</span><span class="sxs-lookup"><span data-stu-id="0ae88-124">[Call the Active AD Graph API from your Java web app](https://github.com/Azure-Samples/active-directory-java-graphapi-web/)</span></span>  

<span data-ttu-id="0ae88-125">Ознакомьтесь с другими [примерами кода Java для Azure AD](https://azure.microsoft.com/en-us/resources/samples/?term=active+directory&platform=java), которые можно использовать в приложениях.</span><span class="sxs-lookup"><span data-stu-id="0ae88-125">Explore more [sample Java code for Azure AD](https://azure.microsoft.com/en-us/resources/samples/?term=active+directory&platform=java) you can use in your apps.</span></span>
