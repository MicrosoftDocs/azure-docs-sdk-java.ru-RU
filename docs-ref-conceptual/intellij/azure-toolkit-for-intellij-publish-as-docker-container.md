---
title: Публикация контейнера Docker с помощью набора средств Azure для IntelliJ
description: Вы можете узнать, как опубликовать веб-приложение в Microsoft Azure в виде контейнера Docker с помощью набора средств Azure для IntelliJ.
services: ''
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 02/01/2018
ms.devlang: Java
ms.service: multiple
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: na
ms.openlocfilehash: 64cefc1ace5d0377dea25fdbdc83d8dada31ddf7
ms.sourcegitcommit: ed130145f9e5c2d803791d96bb118023175e644a
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/28/2018
---
# <a name="publish-a-web-app-as-a-docker-container-by-using-the-azure-toolkit-for-intellij"></a><span data-ttu-id="03e31-103">Публикация веб-приложение в виде контейнера Docker с помощью набора средств Azure для IntelliJ</span><span class="sxs-lookup"><span data-stu-id="03e31-103">Publish a web app as a Docker container by using the Azure Toolkit for IntelliJ</span></span>

<span data-ttu-id="03e31-104">Контейнеры Docker широко используются при развертывании веб-приложений.</span><span class="sxs-lookup"><span data-stu-id="03e31-104">Docker containers are a widely used method for deploying web applications.</span></span> <span data-ttu-id="03e31-105">При этом разработчики могут объединить все зависимости и файлы проекта в одном пакете, а затем развернуть его на сервере.</span><span class="sxs-lookup"><span data-stu-id="03e31-105">By using Docker containers, developers can consolidate all their project files and dependencies into a single package for deployment to a server.</span></span> <span data-ttu-id="03e31-106">Набор средств Azure для IntelliJ упрощает этот процесс для разработчиков на языке Java, предоставляя функции *публикации в виде контейнера Docker* при развертывании в Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="03e31-106">The Azure Toolkit for IntelliJ simplifies this process for Java developers by adding *Publish as Docker Container* features for deployment to Microsoft Azure.</span></span> <span data-ttu-id="03e31-107">В этой статье описаны действия, необходимые для публикации приложений в Azure в качестве контейнеров Docker.</span><span class="sxs-lookup"><span data-stu-id="03e31-107">This article walks you through the steps required to publish your applications to Azure as Docker containers.</span></span>

> [!NOTE]
>
> <span data-ttu-id="03e31-108">Дополнительные сведения о Docker см. на [веб-сайте Docker].</span><span class="sxs-lookup"><span data-stu-id="03e31-108">More information about Docker is available on the [Docker website].</span></span>
>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="publish-your-web-app-to-azure-by-using-a-docker-container"></a><span data-ttu-id="03e31-109">Публикация веб-приложения в Azure с помощью контейнера Docker</span><span class="sxs-lookup"><span data-stu-id="03e31-109">Publish your web app to Azure by using a Docker container</span></span>

> [!NOTE]
> * <span data-ttu-id="03e31-110">Чтобы опубликовать веб-приложение, необходимо создать готовый к развертыванию артефакт.</span><span class="sxs-lookup"><span data-stu-id="03e31-110">To publish your web app, you must create a deployment-ready artifact.</span></span> <span data-ttu-id="03e31-111">Дополнительные сведения о создании артефактов см. в [этом разделе](#artifacts).</span><span class="sxs-lookup"><span data-stu-id="03e31-111">To learn more, see the [Additional information about creating artifacts](#artifacts) section.</span></span>
>
> * <span data-ttu-id="03e31-112">После выполнения развертывания с помощью мастера хотя бы один раз большинство указанных параметров будет использоваться по умолчанию при повторном запуске этого мастера.</span><span class="sxs-lookup"><span data-stu-id="03e31-112">After you have completed the deployment wizard at least once, most of your settings are used as defaults when you run the wizard again.</span></span>
>

1. <span data-ttu-id="03e31-113">Откройте проект веб-приложения в IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="03e31-113">Open your web app project in IntelliJ.</span></span>

2. <span data-ttu-id="03e31-114">Чтобы запустить мастер **публикации в виде контейнера Docker**, выполните одно из следующих действий:</span><span class="sxs-lookup"><span data-stu-id="03e31-114">To start the **Publish as Docker Container** wizard, do either of the following:</span></span>

   * <span data-ttu-id="03e31-115">Щелкните правой кнопкой мыши проект в окне средства **Проект**, щелкните **Azure**, а затем выберите **Publish as Docker Container** (Опубликовать как контейнер Docker):</span><span class="sxs-lookup"><span data-stu-id="03e31-115">In the **Project** tool window, right-click your project, click **Azure**, and then click **Publish as Docker Container**:</span></span>

      ![Команда публикации в виде контейнера Docker][PUB01]

   * <span data-ttu-id="03e31-117">На панели инструментов IntelliJ нажмите кнопку **Publish Group** (Опубликовать группу), а затем выберите **Publish as Docker Container** (Опубликовать как контейнер Docker):</span><span class="sxs-lookup"><span data-stu-id="03e31-117">On the IntelliJ toolbar, click the **Publish Group** button, and then click **Publish as Docker Container**:</span></span>

      <span data-ttu-id="03e31-118">![Команда публикации в виде контейнера Docker][PUB02]</span><span class="sxs-lookup"><span data-stu-id="03e31-118">![The Publish as Docker Container command][PUB02]</span></span>  
    <span data-ttu-id="03e31-119">После этого откроется мастер **развертывания контейнера Docker в Azure**.</span><span class="sxs-lookup"><span data-stu-id="03e31-119">The **Deploy Docker Container on Azure** wizard opens.</span></span>

   ![Мастер развертывания контейнера Docker в Azure][PUB03]

3. <span data-ttu-id="03e31-121">В окне **ввода имени образа, выбора пути артефакта и проверки используемого узла Docker** сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="03e31-121">In the **Type an image name, select the artifact's path and check a Docker host to be used** window, do the following:</span></span> 

   <span data-ttu-id="03e31-122">a.</span><span class="sxs-lookup"><span data-stu-id="03e31-122">a.</span></span> <span data-ttu-id="03e31-123">В текстовом поле **Docker image name** (Имя образа Docker) введите уникальное имя узла Docker.</span><span class="sxs-lookup"><span data-stu-id="03e31-123">In the **Docker image name** box, enter a unique name for your Docker host.</span></span> <span data-ttu-id="03e31-124">(Мастер создаст это имя автоматически, но его можно изменить.)</span><span class="sxs-lookup"><span data-stu-id="03e31-124">(The wizard automatically creates a name, but you can modify it.)</span></span> 

   <span data-ttu-id="03e31-125">Б.</span><span class="sxs-lookup"><span data-stu-id="03e31-125">b.</span></span> <span data-ttu-id="03e31-126">В области **Узлы** отображаются все созданные вами узлы Docker.</span><span class="sxs-lookup"><span data-stu-id="03e31-126">The **Hosts** area displays any Docker hosts that you have already created.</span></span> <span data-ttu-id="03e31-127">Выполните одно из приведенных ниже действий.</span><span class="sxs-lookup"><span data-stu-id="03e31-127">Do either of the following:</span></span> 
      * <span data-ttu-id="03e31-128">Если вы уже создали узел Docker, вы можете развернуть веб-приложение в нем.</span><span class="sxs-lookup"><span data-stu-id="03e31-128">If you have an existing Docker host, you can deploy your web app to it.</span></span>
      * <span data-ttu-id="03e31-129">Чтобы создать узел Docker, щелкните зеленый знак "плюс" (**+**).</span><span class="sxs-lookup"><span data-stu-id="03e31-129">To create a Docker host, click the green plus sign (**+**).</span></span>  
       <span data-ttu-id="03e31-130">После этого откроется диалоговое окно **Create Docker Host** (Создание узла Docker).</span><span class="sxs-lookup"><span data-stu-id="03e31-130">The **Create Docker Host** dialog box opens.</span></span> 

      ![Мастер развертывания контейнера Docker в Azure][PUB04a]

4. <span data-ttu-id="03e31-132">В окне **настройки новой виртуальной машины** укажите приведенные ниже параметры узла Docker.</span><span class="sxs-lookup"><span data-stu-id="03e31-132">In the **Configure the new virtual machine** window, provide the following information about your Docker host.</span></span> <span data-ttu-id="03e31-133">(Мастер создаст большинство параметров автоматически, но их можно изменить.)</span><span class="sxs-lookup"><span data-stu-id="03e31-133">(The wizard automatically generates most of the information for you, but you can modify any of them.)</span></span> 

   <span data-ttu-id="03e31-134">a.</span><span class="sxs-lookup"><span data-stu-id="03e31-134">a.</span></span> <span data-ttu-id="03e31-135">В текстовом поле **Имя** введите уникальное имя узла Docker.</span><span class="sxs-lookup"><span data-stu-id="03e31-135">In the **Name** box, enter a unique name for the Docker host.</span></span> <span data-ttu-id="03e31-136">(Это не указанное выше имя образа Docker.)</span><span class="sxs-lookup"><span data-stu-id="03e31-136">(It is not the same as the Docker image name that you specified earlier.)</span></span> 
    
   <span data-ttu-id="03e31-137">Б.</span><span class="sxs-lookup"><span data-stu-id="03e31-137">b.</span></span> <span data-ttu-id="03e31-138">В текстовом поле **Подписка** укажите, какая подписка Azure будет использоваться для узла.</span><span class="sxs-lookup"><span data-stu-id="03e31-138">In the **Subscription** box, enter the Azure subscription that you use for your host.</span></span> 
      
   <span data-ttu-id="03e31-139">c.</span><span class="sxs-lookup"><span data-stu-id="03e31-139">c.</span></span> <span data-ttu-id="03e31-140">В текстовом поле **Регион** укажите географический регион, где размещен узел.</span><span class="sxs-lookup"><span data-stu-id="03e31-140">In the **Region** box, enter the geographical region where your host is located.</span></span>
      
   <span data-ttu-id="03e31-141">d.</span><span class="sxs-lookup"><span data-stu-id="03e31-141">d.</span></span> <span data-ttu-id="03e31-142">На вкладке **OS and Size** (ОС и размер) сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="03e31-142">On the **OS and Size** tab, do the following:</span></span>      
      * <span data-ttu-id="03e31-143">**Host OS** (ОС узла). Укажите операционную систему виртуальной машины, которая содержит узел.</span><span class="sxs-lookup"><span data-stu-id="03e31-143">**Host OS**: Enter the operating system for the virtual machine that contains your host.</span></span> 
      * <span data-ttu-id="03e31-144">**Size** (Размер). Укажите размер виртуальной машины узла.</span><span class="sxs-lookup"><span data-stu-id="03e31-144">**Size**: Enter the virtual-machine size for your host.</span></span>   
       
   <span data-ttu-id="03e31-145">д.</span><span class="sxs-lookup"><span data-stu-id="03e31-145">e.</span></span> <span data-ttu-id="03e31-146">На вкладке **Группа ресурсов** выберите один из следующих вариантов:</span><span class="sxs-lookup"><span data-stu-id="03e31-146">On the **Resource Group** tab, select either of the following:</span></span>      
      * <span data-ttu-id="03e31-147">**Новая группа ресурсов.** Создайте группу ресурсов для узла.</span><span class="sxs-lookup"><span data-stu-id="03e31-147">**New resource group**: Create a resource group for your host.</span></span>
      * <span data-ttu-id="03e31-148">**Существующая группа ресурсов.** Укажите имеющуюся группу ресурсов из учетной записи Azure.</span><span class="sxs-lookup"><span data-stu-id="03e31-148">**Existing resource group**: Specify an existing resource group from your Azure account.</span></span> 
       
   <span data-ttu-id="03e31-149">f.</span><span class="sxs-lookup"><span data-stu-id="03e31-149">f.</span></span> <span data-ttu-id="03e31-150">На вкладке **Сеть** выберите один из следующих вариантов:</span><span class="sxs-lookup"><span data-stu-id="03e31-150">On the **Network** tab, select either of the following:</span></span>      
      * <span data-ttu-id="03e31-151">**New virtual network** (Новая виртуальная сеть). Создайте виртуальную сеть для узла.</span><span class="sxs-lookup"><span data-stu-id="03e31-151">**New virtual network**: Create a virtual network for your host.</span></span>
      * <span data-ttu-id="03e31-152">**Existing virtual network** (Имеющаяся виртуальная сеть). Укажите имеющуюся виртуальную сеть из учетной записи Azure.</span><span class="sxs-lookup"><span data-stu-id="03e31-152">**Existing virtual network**: Specify an existing virtual network from your Azure account.</span></span> 
       
   <span data-ttu-id="03e31-153">ж.</span><span class="sxs-lookup"><span data-stu-id="03e31-153">g.</span></span> <span data-ttu-id="03e31-154">На вкладке **Хранилище** выберите один из следующих вариантов:</span><span class="sxs-lookup"><span data-stu-id="03e31-154">On the **Storage** tab, select either of the following:</span></span>      
      * <span data-ttu-id="03e31-155">**Создать учетную запись хранения.** Создайте учетную запись хранения для узла.</span><span class="sxs-lookup"><span data-stu-id="03e31-155">**New storage account**: Create a storage account for your host.</span></span>
      * <span data-ttu-id="03e31-156">**Existing storage account** (Имеющаяся учетная запись хранения). Укажите имеющуюся учетную запись хранения из учетной записи Azure.</span><span class="sxs-lookup"><span data-stu-id="03e31-156">**Existing storage account**: Specify an existing storage account from your Azure account.</span></span>
       
5. <span data-ttu-id="03e31-157">Нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="03e31-157">Click **Next**.</span></span>  
     <span data-ttu-id="03e31-158">После этого откроется окно **Configure log in credentials and port settings** (Настройка учетных данных для входа в систему и параметров порта).</span><span class="sxs-lookup"><span data-stu-id="03e31-158">The **Configure log in credentials and port settings** window opens.</span></span>

      ![Окно настройки учетных данных для входа в систему и параметров порта][PUB05]

6. <span data-ttu-id="03e31-160">Выберите один из следующих вариантов:</span><span class="sxs-lookup"><span data-stu-id="03e31-160">Select one of the following options:</span></span>

      * <span data-ttu-id="03e31-161">**Import credentials from Azure Key Vault** (Импортировать учетные данные из Azure Key Vault). Укажите сохраненный ранее набор учетных данных, хранящихся в подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="03e31-161">**Import credentials from Azure Key Vault**: Specify a previously saved set of credentials that are stored in your Azure subscription.</span></span>

          > [!NOTE]
          > <span data-ttu-id="03e31-162">Хранилище Azure Key Vault, созданное с помощью определенной учетной записи или определенного субъекта-службы, не становится автоматически доступным для другой учетной записи или субъекта-службы, которые относятся к той же подписке.</span><span class="sxs-lookup"><span data-stu-id="03e31-162">An Azure key vault that's created with a specific account or service principal is not automatically accessible by another account or service principal that shares the subscription.</span></span> <span data-ttu-id="03e31-163">Чтобы разрешить другой учетной записи или субъекту-службе использовать Key Vault, нужно добавить их на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="03e31-163">To allow another account or service principal to use the key vault, you must use the Azure portal to add the account or service principal.</span></span>

      * <span data-ttu-id="03e31-164">**New log in credentials** (Новые учетные данные для входа). Создайте набор учетных данных для входа в систему.</span><span class="sxs-lookup"><span data-stu-id="03e31-164">**New log in credentials**: Create a new set of login credentials.</span></span> <span data-ttu-id="03e31-165">Если вы выбрали этот параметр, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="03e31-165">If you select this option, do the following:</span></span>

    <span data-ttu-id="03e31-166">a.</span><span class="sxs-lookup"><span data-stu-id="03e31-166">a.</span></span> <span data-ttu-id="03e31-167">На вкладке **VM Credentials** (Учетные данные виртуальной машины) укажите следующие учетные данные для входа на виртуальную машину узла Docker:</span><span class="sxs-lookup"><span data-stu-id="03e31-167">On the **VM Credentials** tab, provide the following information for the virtual-machine login credentials of your Docker host:</span></span>

    * <span data-ttu-id="03e31-168">**Username** (Имя пользователя). Укажите имя пользователя для входа на виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="03e31-168">**Username**: Enter the username for your virtual-machine login credentials.</span></span>

    * <span data-ttu-id="03e31-169">**Password** (Пароль) и **Confirm** (Подтверждение). Укажите пароль для входа на виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="03e31-169">**Password** and **Confirm**: Enter the password for your virtual-machine login credentials.</span></span>

    * <span data-ttu-id="03e31-170">**SSH.** Укажите параметры Secure Shell (SSH) узла Docker.</span><span class="sxs-lookup"><span data-stu-id="03e31-170">**SSH**: Enter the Secure Shell (SSH) settings for your Docker host.</span></span> <span data-ttu-id="03e31-171">Вы можете выбрать один из следующих вариантов:</span><span class="sxs-lookup"><span data-stu-id="03e31-171">You can select one of the following options:</span></span>

        * <span data-ttu-id="03e31-172">**None** (Нет). Указывает, что виртуальная машина не разрешает SSH-подключения.</span><span class="sxs-lookup"><span data-stu-id="03e31-172">**None**: Specifies that your virtual machine does not allow SSH connections.</span></span>

        * <span data-ttu-id="03e31-173">**Auto-generate** (Автоматическое создание). Автоматически создает необходимые параметры для SSH-подключения.</span><span class="sxs-lookup"><span data-stu-id="03e31-173">**Auto-generate**: Automatically creates the requisite settings for connecting via SSH.</span></span>

        * <span data-ttu-id="03e31-174">**Import from directory** (Импорт из каталога). Позволяет указать каталог, содержащий набор ранее сохраненных параметров SSH.</span><span class="sxs-lookup"><span data-stu-id="03e31-174">**Import from directory**: Allows you to specify a directory that contains a set of previously saved SSH settings.</span></span> <span data-ttu-id="03e31-175">В частности, каталог должен содержать два следующих файла:</span><span class="sxs-lookup"><span data-stu-id="03e31-175">The directory must contain the following two files:</span></span>

            * <span data-ttu-id="03e31-176">*id_rsa*. Этот файл содержит идентификационные данные RSA для пользователя.</span><span class="sxs-lookup"><span data-stu-id="03e31-176">*id_rsa*: Contains the RSA identification for a user.</span></span>

            * <span data-ttu-id="03e31-177">*id_rsa.pub*. Этот файл содержит открытый ключ RSA, который используемый для проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="03e31-177">*id_rsa.pub*: Contains the RSA public key that is used for authentication.</span></span>

    <span data-ttu-id="03e31-178">Б.</span><span class="sxs-lookup"><span data-stu-id="03e31-178">b.</span></span> <span data-ttu-id="03e31-179">На вкладке **Docker Daemon Access** (Доступ к управляющей программе Docker) укажите следующие сведения:</span><span class="sxs-lookup"><span data-stu-id="03e31-179">On the **Docker Daemon Access** tab, provide the following information:</span></span>

    ![Окно Create Docker Host (Создание узла Docker)][PUB06]
    
    * <span data-ttu-id="03e31-181">**Docker Daemon port** (Порт управляющей программы Docker). Укажите уникальный TCP-порт для узла Docker.</span><span class="sxs-lookup"><span data-stu-id="03e31-181">**Docker Daemon port**: Enter the unique TCP port for your Docker host.</span></span>
    
    * <span data-ttu-id="03e31-182">**Безопасность TLS**. Введите параметры безопасности транспортного уровня для узла Docker.</span><span class="sxs-lookup"><span data-stu-id="03e31-182">**TLS Security**: Enter the Transport Layer Security settings for your Docker host.</span></span> <span data-ttu-id="03e31-183">Вы можете выбрать один из следующих параметров:</span><span class="sxs-lookup"><span data-stu-id="03e31-183">You can choose from the following options:</span></span>
    
        * <span data-ttu-id="03e31-184">**None** (Нет). Указывает, что виртуальная машина не разрешает TLS-подключения.</span><span class="sxs-lookup"><span data-stu-id="03e31-184">**None**: Specifies that your virtual machine does not allow TLS connections.</span></span>
        
        * <span data-ttu-id="03e31-185">**Auto-generate** (Автоматическое создание). Автоматически создает необходимые параметры для TLS-подключения.</span><span class="sxs-lookup"><span data-stu-id="03e31-185">**Auto-generate**: Automatically creates the requisite settings for connecting via TLS.</span></span>
        
        * <span data-ttu-id="03e31-186">**Import from directory** (Импорт из каталога). Позволяет указать каталог, содержащий набор ранее сохраненных параметров TLS.</span><span class="sxs-lookup"><span data-stu-id="03e31-186">**Import from directory**: Specifies a directory that contains a set of previously saved TLS settings.</span></span> <span data-ttu-id="03e31-187">В частности, каталог должен содержать шесть следующих файлов:</span><span class="sxs-lookup"><span data-stu-id="03e31-187">The directory must contain the following six files:</span></span>
        
            * <span data-ttu-id="03e31-188">*ca.pem* и *ca-key.pem*. Эти файлы содержат сертификат и открытый ключ для центра сертификации TLS.</span><span class="sxs-lookup"><span data-stu-id="03e31-188">*ca.pem* and *ca-key.pem*: Contain the certificate and public key for the TLS Certificate Authority.</span></span>
            
            * <span data-ttu-id="03e31-189">*cert.pem* и *key.pem*. Эти файлы содержат сертификат клиента и открытый ключ, которые будут использоваться для проверки подлинности TLS.</span><span class="sxs-lookup"><span data-stu-id="03e31-189">*cert.pem* and *key.pem*: Contain client certificate and public key which will be used for TLS authentication.</span></span>
            
            * <span data-ttu-id="03e31-190">*server.pem* и *server-key.pem*. Эти файлы содержат сертификат клиента и открытый ключ, которые будут использоваться для проверки подлинности TLS.</span><span class="sxs-lookup"><span data-stu-id="03e31-190">*server.pem* and *server-key.pem*: Contain the client certificate and public key that is used for TLS authentication.</span></span>

7. <span data-ttu-id="03e31-191">Указав необходимые сведения, нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="03e31-191">After you have entered the required information, click **Finish**.</span></span>  
    <span data-ttu-id="03e31-192">После этого снова отобразится мастер **развертывания контейнера Docker в Azure**.</span><span class="sxs-lookup"><span data-stu-id="03e31-192">The **Deploy Docker Container on Azure** wizard reappears.</span></span>

   ![Мастер развертывания контейнера Docker в Azure][PUB07]

8. <span data-ttu-id="03e31-194">Нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="03e31-194">Click **Next**.</span></span>  
    <span data-ttu-id="03e31-195">Откроется окно **Configure the Docker container to be created** (Настройка создаваемого контейнера Docker).</span><span class="sxs-lookup"><span data-stu-id="03e31-195">The **Configure the Docker container to be created** window opens.</span></span>

   ![Окно настройки создаваемого контейнера Docker][PUB08]

9. <span data-ttu-id="03e31-197">В окне **Configure the Docker container to be created** (Настройка создаваемого контейнера Docker) укажите следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="03e31-197">In the **Configure the Docker container to be created** window, provide the following information:</span></span> 

   <span data-ttu-id="03e31-198">a.</span><span class="sxs-lookup"><span data-stu-id="03e31-198">a.</span></span> <span data-ttu-id="03e31-199">В текстовом поле **Docker container name** (Имя контейнера Docker) введите уникальное имя контейнера Docker.</span><span class="sxs-lookup"><span data-stu-id="03e31-199">In the **Docker container name** box, enter a unique name for your Docker container.</span></span>

   <span data-ttu-id="03e31-200">Б.</span><span class="sxs-lookup"><span data-stu-id="03e31-200">b.</span></span> <span data-ttu-id="03e31-201">Выберите один из следующих образов Docker:</span><span class="sxs-lookup"><span data-stu-id="03e31-201">Choose one of the following Docker images:</span></span> 

      * <span data-ttu-id="03e31-202">**Predefined Docker image** (Предопределенный образ Docker). Укажите имеющийся образ Docker из Azure.</span><span class="sxs-lookup"><span data-stu-id="03e31-202">**Predefined Docker image**: Specify a pre-existing Docker image from Azure.</span></span> 

        > [!NOTE]
        > <span data-ttu-id="03e31-203">Список образов Docker в этом поле состоит из нескольких образов, в которые набор средств Azure устанавливает исправление таким образом, чтобы артефакт развертывался автоматически.</span><span class="sxs-lookup"><span data-stu-id="03e31-203">The list of Docker images in this box consists of several images that the Azure Toolkit has been configured to patch so that your artifact is deployed automatically.</span></span> 

      * <span data-ttu-id="03e31-204">**Custom Dockerfile** (Пользовательский Dockerfile). Укажите сохраненный ранее Dockerfile на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="03e31-204">**Custom Dockerfile**: Specify a previously saved Dockerfile from your local computer.</span></span>

        > [!NOTE]
        > <span data-ttu-id="03e31-205">Это расширенная функция для разработчиков, желающих развернуть собственный Dockerfile.</span><span class="sxs-lookup"><span data-stu-id="03e31-205">This is a more advanced feature for developers who want to deploy their own Dockerfile.</span></span> <span data-ttu-id="03e31-206">Однако за правильность сборки Dockerfile отвечают сами разработчики, использующие эту возможность.</span><span class="sxs-lookup"><span data-stu-id="03e31-206">However, it is up to developers who use this option to ensure that their Dockerfile is built correctly.</span></span> <span data-ttu-id="03e31-207">Набор средств Azure не проверяет содержимое пользовательского Dockerfile, поэтому при наличии проблем с этим файлом развертывание может завершиться ошибкой.</span><span class="sxs-lookup"><span data-stu-id="03e31-207">Because the Azure Toolkit does not validate the content in a custom Dockerfile, the deployment might fail if the Dockerfile has issues.</span></span> <span data-ttu-id="03e31-208">Кроме того, набор средств Azure ожидает, что пользовательский Dockerfile содержит артефакт веб-приложения, и попытается установить HTTP-подключение.</span><span class="sxs-lookup"><span data-stu-id="03e31-208">In addition, because the Azure Toolkit expects the custom Dockerfile to contain a web app artifact, it attempts to open an HTTP connection.</span></span> <span data-ttu-id="03e31-209">Если разработчики публикуют артефакт другого типа, то после развертывания могут возникнуть некритичные ошибки.</span><span class="sxs-lookup"><span data-stu-id="03e31-209">If developers publish a different type of artifact, they might receive innocuous errors after deployment.</span></span>

   <span data-ttu-id="03e31-210">c.</span><span class="sxs-lookup"><span data-stu-id="03e31-210">c.</span></span> <span data-ttu-id="03e31-211">В текстовом поле **Port settings** (Параметры порта) укажите уникальную привязку TCP-порта для контейнера Docker.</span><span class="sxs-lookup"><span data-stu-id="03e31-211">In the **Port settings** box, enter the unique TCP port binding for your Docker container.</span></span> 

10. <span data-ttu-id="03e31-212">Выполнив все предыдущие действия, нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="03e31-212">After you have completed the preceding steps, click **Finish**.</span></span> 

<span data-ttu-id="03e31-213">Набор средств Azure начинает развертывание веб-приложения в контейнере Docker Azure.</span><span class="sxs-lookup"><span data-stu-id="03e31-213">The Azure Toolkit begins deploying your web app to Azure in a Docker container.</span></span> <span data-ttu-id="03e31-214">Если вы не настроили развертывание IntelliJ в фоновом режиме, появится индикатор выполнения **развертывания в Azure**.</span><span class="sxs-lookup"><span data-stu-id="03e31-214">Unless you have configured IntelliJ to be deployed in the background, a **Deploying to Azure** progress bar appears.</span></span> 

![Индикатор выполнения развертывания][PUB09]

<a name="artifacts"></a>
## <a name="additional-information-about-creating-artifacts"></a><span data-ttu-id="03e31-216">Дополнительные сведения о создании артефактов</span><span class="sxs-lookup"><span data-stu-id="03e31-216">Additional information about creating artifacts</span></span>

<span data-ttu-id="03e31-217">Чтобы создать готовый к развертыванию артефакт, выполните следующее:</span><span class="sxs-lookup"><span data-stu-id="03e31-217">To create a deployment-ready artifact, do the following:</span></span>

1. <span data-ttu-id="03e31-218">Откройте проект веб-приложения в IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="03e31-218">Open your web app project in IntelliJ.</span></span>

2. <span data-ttu-id="03e31-219">В меню **File** (Файл) выберите **Project Structure** (Структура проекта).</span><span class="sxs-lookup"><span data-stu-id="03e31-219">Click **File**, and then click **Project Structure**.</span></span>

   ![Команда Project Structure (Структура проекта)][ART01]

3. <span data-ttu-id="03e31-221">Чтобы добавить артефакт, щелкните зеленый знак "плюс" (**+**), а затем выберите **Web Application: Artifact** (Веб-приложение: артефакт).</span><span class="sxs-lookup"><span data-stu-id="03e31-221">To add an artifact, click the green plus sign (**+**), and then click **Web Application: Archive**.</span></span>

   ![Команда Web Application: Artifact (Веб-приложение: артефакт)][ART02]

4. <span data-ttu-id="03e31-223">В текстовом поле **Имя** укажите имя артефакта ( без расширения *WAR*) и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="03e31-223">In the **Name** box, enter a name for your artifact (do not include the *.war* extension), and then click **OK**.</span></span>

   ![Поле "Имя" артефакта][ART03]

<span data-ttu-id="03e31-225">Дополнительные сведения о создании артефактов в IntelliJ см. в статье [Configuring Artifacts] (Настройка артефактов) на веб-сайте JetBrains.</span><span class="sxs-lookup"><span data-stu-id="03e31-225">For more information about creating artifacts in IntelliJ, see [Configuring artifacts] on the JetBrains website.</span></span>

## <a name="next-steps"></a><span data-ttu-id="03e31-226">Дополнительная информация</span><span class="sxs-lookup"><span data-stu-id="03e31-226">Next steps</span></span>

<span data-ttu-id="03e31-227">Дополнительные материалы по Docker доступны на официальном [веб-сайте Docker].</span><span class="sxs-lookup"><span data-stu-id="03e31-227">For additional resources for Docker, see the official [Docker website].</span></span>

[!INCLUDE [azure-toolkit-for-intellij-additional-resources](../includes/azure-toolkit-for-intellij-additional-resources.md)]

<!-- URL List -->

[веб-сайте Docker]: https://www.docker.com/
[Configuring Artifacts]: https://www.jetbrains.com/help/idea/2016.1/configuring-artifacts.html (Настройка артефактов)

<!-- IMG List -->

[PUB01]: media/azure-toolkit-for-intellij-publish-as-docker-container/PUB01.png
[PUB02]: media/azure-toolkit-for-intellij-publish-as-docker-container/PUB02.png
[PUB03]: media/azure-toolkit-for-intellij-publish-as-docker-container/PUB03.png
[PUB04a]: media/azure-toolkit-for-intellij-publish-as-docker-container/PUB04a.png
[PUB04b]: media/azure-toolkit-for-intellij-publish-as-docker-container/PUB04b.png
[PUB04c]: media/azure-toolkit-for-intellij-publish-as-docker-container/PUB04c.png
[PUB04d]: media/azure-toolkit-for-intellij-publish-as-docker-container/PUB04d.png
[PUB05]: media/azure-toolkit-for-intellij-publish-as-docker-container/PUB05.png
[PUB06]: media/azure-toolkit-for-intellij-publish-as-docker-container/PUB06.png
[PUB07]: media/azure-toolkit-for-intellij-publish-as-docker-container/PUB07.png
[PUB08]: media/azure-toolkit-for-intellij-publish-as-docker-container/PUB08.png
[PUB09]: media/azure-toolkit-for-intellij-publish-as-docker-container/PUB09.png

[ART01]: media/azure-toolkit-for-intellij-publish-as-docker-container/ART01.png
[ART02]: media/azure-toolkit-for-intellij-publish-as-docker-container/ART02.png
[ART03]: media/azure-toolkit-for-intellij-publish-as-docker-container/ART03.png
