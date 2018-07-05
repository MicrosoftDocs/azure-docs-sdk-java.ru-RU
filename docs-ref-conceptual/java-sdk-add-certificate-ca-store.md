---
title: Добавление корневого сертификата для Azure в хранилище ЦС Java
description: Узнайте, как добавить корневой сертификат центра сертификации (ЦС) в хранилище сертификатов ЦС Java (cacerts) для использования в Microsoft Azure.
services: ''
documentationcenter: java
author: rmcmurray
manager: mbaldwin
ms.assetid: d3699b0a-835c-43fb-844d-9c25344e5cda
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 05/23/2018
ms.author: robmcm
ms.openlocfilehash: 29b2b598968c9a3a896fffee3ce56f9b0cb4b1ee
ms.sourcegitcommit: 5282a51bf31771671df01af5814df1d2b8e4620c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/28/2018
ms.locfileid: "37090737"
---
# <a name="adding-a-root-certificate-to-the-java-ca-certificates-store"></a><span data-ttu-id="0ea48-103">Добавление корневого сертификата в хранилище сертификатов ЦС Java</span><span class="sxs-lookup"><span data-stu-id="0ea48-103">Adding a root certificate to the Java CA certificates store</span></span>

<span data-ttu-id="0ea48-104">Приложения, использующие службы Azure (например, Служебную шину Azure), должны доверять корневому сертификату Baltimore CyberTrust.</span><span class="sxs-lookup"><span data-stu-id="0ea48-104">Applications that use Azure services (such as Azure Service Bus) need to trust the Baltimore CyberTrust root certificate.</span></span> <span data-ttu-id="0ea48-105">Этот сертификат уже может быть установлен в вашей системе. Если это не так, из этого руководства вы узнаете, как с помощью средства Oracle **keytool** добавить необходимый корневой сертификат центра сертификации (ЦС) в хранилище сертификатов ЦС Java (cacerts). Добавленный сертификат будет использоваться для служб Azure.</span><span class="sxs-lookup"><span data-stu-id="0ea48-105">This certificate may already be installed on your system, but if it is not, the steps in this tutorial will show you how to use Oracle's **keytool** to add the required certificate authority (CA) root certificate to the Java CA certificate (cacerts) store that you will use for Azure services.</span></span>

<span data-ttu-id="0ea48-106">Служебная программа keytool от Oracle — это _средство управления ключами и сертификатами_, позволяющее разработчикам управлять списком доверенных сертификатов, которые можно использовать в Java.</span><span class="sxs-lookup"><span data-stu-id="0ea48-106">Oracle's keytool utility is a _Key and Certificate Management Tool_, which allows developers to manage the list of trusted certificates for use with Java.</span></span> <span data-ttu-id="0ea48-107">Чтобы добавить сертификат ЦС перед сжатием JDK и добавлением его в папку **approot** проекта Azure, можно использовать keytool (инструмент для работы с ключами) или выполнить задачу запуска Azure, где keytool используется для добавления сертификата.</span><span class="sxs-lookup"><span data-stu-id="0ea48-107">You can use keytool to add the CA certificate before zipping your JDK and adding it to your Azure project's **approot** folder, or you could run an Azure start-up task that uses keytool to add the certificate.</span></span>

<span data-ttu-id="0ea48-108">15 апреля 2013 года в системе Azure начался переход с корневого сертификата GTE CyberTrust Global на Baltimore CyberTrust.</span><span class="sxs-lookup"><span data-stu-id="0ea48-108">Beginning April 15, 2013, Azure began migrating from the GTE CyberTrust Global root certificate to the Baltimore CyberTrust root certificate.</span></span> <span data-ttu-id="0ea48-109">Далее в этой статье рассказывается, как с помощью средства keytool добавить корневой сертификат Baltimore CyberTrust в хранилище сертификатов ЦС Java (cacerts).</span><span class="sxs-lookup"><span data-stu-id="0ea48-109">The following steps show you how to use keytool to add the Baltimore CyberTrust root certificate to your Java CA certificate (cacerts) store.</span></span>

> [!NOTE]
> 
> <span data-ttu-id="0ea48-110">Инструкции в этой статье можно использовать для настройки в пакете SDK для Java доверия к корневым сертификатам из других доверенных центров сертификации.</span><span class="sxs-lookup"><span data-stu-id="0ea48-110">You can use the steps in this article to configure your Java SDK to trust the root certificates from other trusted certificate authorities.</span></span> <span data-ttu-id="0ea48-111">Например, можно выбрать корневой сертификат из списка [корневых сертификатах GeoTrust](http://www.geotrust.com/resources/root-certificates/).</span><span class="sxs-lookup"><span data-stu-id="0ea48-111">For example, you might choose a root certificate from the list of certificates at [GeoTrust Root Certificates](http://www.geotrust.com/resources/root-certificates/).</span></span>
> 

## <a name="determining-which-root-certificates-are-installed"></a><span data-ttu-id="0ea48-112">Определение установленных сертификатов</span><span class="sxs-lookup"><span data-stu-id="0ea48-112">Determining which root certificates are installed</span></span>

<span data-ttu-id="0ea48-113">Сертификат Baltimore, возможно, уже установлен в вашем хранилище cacerts, поэтому сначала нужно определить, установлен ли он. Для этого сделайте вот что:</span><span class="sxs-lookup"><span data-stu-id="0ea48-113">The Baltimore certificate might already be installed in your cacerts store, so you need to use the following steps to determine if it has already been installed.</span></span>

1. <span data-ttu-id="0ea48-114">В командной строке администратора перейдите в папку JDK **jdk\jre\lib\security** и выполните приведенную ниже команду, которая возвращает список сертификатов, установленных на компьютере.</span><span class="sxs-lookup"><span data-stu-id="0ea48-114">At an administrator command prompt, navigate to your JDK's **jdk\jre\lib\security** folder, and then run the following command to list the certificates that are installed on your system:</span></span>

   ```shell
   keytool -list -keystore cacerts
   ```

1. <span data-ttu-id="0ea48-115">Если появится запрос ввести пароль хранилища, по умолчанию используется пароль **changeit**.</span><span class="sxs-lookup"><span data-stu-id="0ea48-115">If you are prompted for the store password, the default password is **changeit**.</span></span>

   > [!NOTE]
   > 
   > <span data-ttu-id="0ea48-116">Сведения о том, как изменить пароль, см. в документации по keytool: <http://docs.oracle.com/javase/7/docs/technotes/tools/windows/keytool.html>.</span><span class="sxs-lookup"><span data-stu-id="0ea48-116">If you want to change the store password, see the keytool documentation at <http://docs.oracle.com/javase/7/docs/technotes/tools/windows/keytool.html>.</span></span>
   > 

1. <span data-ttu-id="0ea48-117">Если в списке нет сертификата с отпечатком `d4:de:20:d0:5e:66:fc:53:fe:1a:50:88:2c:78:db:28:52:ca:e4:74`, скачайте и установите его, как описано ниже.</span><span class="sxs-lookup"><span data-stu-id="0ea48-117">If you do not see the certificate with the thumbprint of `d4:de:20:d0:5e:66:fc:53:fe:1a:50:88:2c:78:db:28:52:ca:e4:74`, use the steps in the following section to download and install the certificate.</span></span>

## <a name="to-add-a-root-certificate-to-the-cacerts-store"></a><span data-ttu-id="0ea48-118">Добавление корневого сертификата в хранилище cacerts</span><span class="sxs-lookup"><span data-stu-id="0ea48-118">To add a root certificate to the cacerts store</span></span>

1. <span data-ttu-id="0ea48-119">Скачайте корневой сертификат Baltimore CyberTrust по ссылке <https://cacert.omniroot.com/bc2025.crt> и сохраните его в папке **jdk\jre\lib\security** как файл с расширением **.cer**.</span><span class="sxs-lookup"><span data-stu-id="0ea48-119">Download the Baltimore CyberTrust root certificate from <https://cacert.omniroot.com/bc2025.crt>, and save to a local file with extension **.cer** in your **jdk\jre\lib\security** folder.</span></span> <span data-ttu-id="0ea48-120">Предположим, что вы скачали корневой сертификат Baltimore CyberTrust как файл **bc2025.cer**.</span><span class="sxs-lookup"><span data-stu-id="0ea48-120">For this example, assume that you downloaded the Baltimore CyberTrust root certificate file as **bc2025.cer**.</span></span>

   > [!NOTE]
   > 
   > <span data-ttu-id="0ea48-121">Корневой сертификат Baltimore CyberTrust имеет серийный номер `02:00:00:b9` и отпечаток SHA1 `d4:de:20:d0:5e:66:fc:53:fe:1a:50:88:2c:78:db:28:52:ca:e4:74`.</span><span class="sxs-lookup"><span data-stu-id="0ea48-121">The Baltimore CyberTrust root certificate has a serial number of `02:00:00:b9`, and a SHA1 thumbprint of `d4:de:20:d0:5e:66:fc:53:fe:1a:50:88:2c:78:db:28:52:ca:e4:74`.</span></span>
   > 

2. <span data-ttu-id="0ea48-122">Импортируйте сертификат в хранилище cacerts с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="0ea48-122">Import the certificate to the cacerts store by using the following command:</span></span>

   ```shell
   keytool -keystore cacerts -importcert -alias bc2025ca -file bc2025.cer
   ```
   <span data-ttu-id="0ea48-123">Описание</span><span class="sxs-lookup"><span data-stu-id="0ea48-123">Where:</span></span>

   |  <span data-ttu-id="0ea48-124">Параметр</span><span class="sxs-lookup"><span data-stu-id="0ea48-124">Parameter</span></span>   |                              <span data-ttu-id="0ea48-125">Описание</span><span class="sxs-lookup"><span data-stu-id="0ea48-125">Description</span></span>                               |
   |--------------|------------------------------------------------------------------------|
   |  `keystore`  |                    <span data-ttu-id="0ea48-126">Указывает хранилище сертификатов.</span><span class="sxs-lookup"><span data-stu-id="0ea48-126">Specifies the certificate store.</span></span>                    |
   | `importcert` |            <span data-ttu-id="0ea48-127">Указывает, что сертификат импортируется.</span><span class="sxs-lookup"><span data-stu-id="0ea48-127">Specifies that you are importing a certificate.</span></span>             |
   |   `alias`    |                <span data-ttu-id="0ea48-128">Указывает псевдоним для сертификата.</span><span class="sxs-lookup"><span data-stu-id="0ea48-128">Specifies an alias for the certificate.</span></span>                 |
   |    `file`    | <span data-ttu-id="0ea48-129">Указывает имя файла для импортируемого корневого сертификата.</span><span class="sxs-lookup"><span data-stu-id="0ea48-129">Specifies the filename of the root certificate that you are importing.</span></span> |


3. <span data-ttu-id="0ea48-130">Если появится запрос подтвердить доверие к сертификату, проверьте отпечаток. Если отпечаток — `d4:de:20:d0:5e:66:fc:53:fe:1a:50:88:2c:78:db:28:52:ca:e4:74`, введите **y** для подтверждения.</span><span class="sxs-lookup"><span data-stu-id="0ea48-130">If you are prompted to trust the certificate, verify the thumbprint as `d4:de:20:d0:5e:66:fc:53:fe:1a:50:88:2c:78:db:28:52:ca:e4:74`, and type **y** if the thumbprint is correct.</span></span>

4. <span data-ttu-id="0ea48-131">Выполните следующую команду, чтобы убедиться, что сертификат СЦ был успешно импортирован:</span><span class="sxs-lookup"><span data-stu-id="0ea48-131">Run the following command to ensure the CA certificate has been successfully imported:</span></span>

   ```shell
   keytool -list -keystore cacerts
   ```

<span data-ttu-id="0ea48-132">Добавив в JDK корневой сертификат, заархивируйте содержимое JDK и добавьте его в папку **approot** своего проекта в Azure.</span><span class="sxs-lookup"><span data-stu-id="0ea48-132">After you have successfully added the root certificate to your JDK, you can zip the contents of JDK and add it to your Azure project's **approot** folder.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0ea48-133">Дополнительная информация</span><span class="sxs-lookup"><span data-stu-id="0ea48-133">Next steps</span></span>

<span data-ttu-id="0ea48-134">Дополнительные сведения о служебной программе keytool см. по ссылке <http://docs.oracle.com/javase/7/docs/technotes/tools/windows/keytool.html>.</span><span class="sxs-lookup"><span data-stu-id="0ea48-134">For more information about the keytool utility, see <http://docs.oracle.com/javase/7/docs/technotes/tools/windows/keytool.html>.</span></span>

<span data-ttu-id="0ea48-135">Дополнительные сведения об используемых в Azure корневых сертификатах см. в записи блога [Azure Root Certificate Migration](http://blogs.msdn.com/b/windowsazure/archive/2013/03/15/windows-azure-root-certificate-migration.aspx) (Перенос корневых сертификатов Azure).</span><span class="sxs-lookup"><span data-stu-id="0ea48-135">For more information about the root certificates used by Azure, see [Azure Root Certificate Migration](http://blogs.msdn.com/b/windowsazure/archive/2013/03/15/windows-azure-root-certificate-migration.aspx).</span></span>

<span data-ttu-id="0ea48-136">Дополнительные сведения о Java см. в разделе [Azure for Java developers](/java/azure) (Azure для разработчиков Java).</span><span class="sxs-lookup"><span data-stu-id="0ea48-136">For more information about Java, see [Azure for Java developers](/java/azure).</span></span>
