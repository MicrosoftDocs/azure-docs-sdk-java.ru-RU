---
title: "Публикация контейнера Docker с помощью набора средств Azure для Eclipse"
description: "Вы можете узнать, как опубликовать веб-приложение в Microsoft Azure в виде контейнера Docker с помощью набора средств Azure для Eclipse."
services: 
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
ms.assetid: 
ms.author: robmcm
ms.date: 02/01/2018
ms.devlang: Java
ms.service: multiple
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: na
ms.openlocfilehash: aec3682cc14204ca2b395d4b851db7bb68cb8728
ms.sourcegitcommit: 151aaa6ccc64d94ed67f03e846bab953bde15b4a
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/03/2018
---
# <a name="publish-a-web-app-as-a-docker-container-by-using-the-azure-toolkit-for-eclipse"></a><span data-ttu-id="3c4c6-103">Публикация веб-приложения в виде контейнера Docker с помощью набора средств Azure для Eclipse</span><span class="sxs-lookup"><span data-stu-id="3c4c6-103">Publish a web app as a Docker container by using the Azure Toolkit for Eclipse</span></span>

<span data-ttu-id="3c4c6-104">Контейнеры Docker широко используются при развертывании веб-приложений.</span><span class="sxs-lookup"><span data-stu-id="3c4c6-104">Docker containers are a widely used method for deploying web applications.</span></span> <span data-ttu-id="3c4c6-105">При этом разработчики могут объединить все зависимости и файлы проекта в одном пакете, а затем развернуть его на сервере.</span><span class="sxs-lookup"><span data-stu-id="3c4c6-105">By using Docker containers, developers can consolidate all their project files and dependencies into a single package for deployment to a server.</span></span> <span data-ttu-id="3c4c6-106">Набор средств Azure для Eclipse упрощает этот процесс для разработчиков на языке Java, предоставляя функции *публикации в виде контейнера Docker* при развертывании в Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="3c4c6-106">The Azure Toolkit for Eclipse simplifies this process for Java developers by adding *Publish as Docker Container* features for deployment to Microsoft Azure.</span></span> <span data-ttu-id="3c4c6-107">В этой статье описаны действия, необходимые для публикации приложений в Azure в качестве контейнеров Docker.</span><span class="sxs-lookup"><span data-stu-id="3c4c6-107">This article walks you through the steps required to publish your applications to Azure as Docker containers.</span></span>

> [!NOTE]
> <span data-ttu-id="3c4c6-108">Дополнительные сведения о Docker см. на [веб-сайте Docker].</span><span class="sxs-lookup"><span data-stu-id="3c4c6-108">More information about Docker is available on the [Docker website].</span></span>
>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="publish-your-web-app-to-azure-by-using-a-docker-container"></a><span data-ttu-id="3c4c6-109">Публикация веб-приложения в Azure с помощью контейнера Docker</span><span class="sxs-lookup"><span data-stu-id="3c4c6-109">Publish your web app to Azure by using a Docker container</span></span>

1. <span data-ttu-id="3c4c6-110">Откройте проект веб-приложения в Eclipse.</span><span class="sxs-lookup"><span data-stu-id="3c4c6-110">Open your web app project in Eclipse.</span></span>

1. <span data-ttu-id="3c4c6-111">Чтобы запустить мастер **публикации в виде контейнера Docker**, выполните одно из следующих действий:</span><span class="sxs-lookup"><span data-stu-id="3c4c6-111">To start the **Publish as Docker Container** wizard, do either of the following:</span></span>

   * <span data-ttu-id="3c4c6-112">В представлении **Навигатор** щелкните правой кнопкой мыши проект, щелкните **Azure**, а затем выберите **Publish as Docker Container** (Опубликовать как контейнер Docker).</span><span class="sxs-lookup"><span data-stu-id="3c4c6-112">In the **Navigator** view, right-click your project, click **Azure**, and then click **Publish as Docker Container**.</span></span>

      ![Представление навигатора, команда публикации в виде контейнера Docker][PUB01]

   * <span data-ttu-id="3c4c6-114">На панели инструментов Eclipse нажмите кнопку **Опубликовать**, а затем выберите **Publish as Docker Container** (Опубликовать как контейнер Docker).</span><span class="sxs-lookup"><span data-stu-id="3c4c6-114">On the Eclipse toolbar, click the **Publish** button, and then click **Publish as Docker Container**.</span></span>

      ![Панель инструментов Eclipse, команда публикации в виде контейнера Docker][PUB02]
      
   <span data-ttu-id="3c4c6-116">После этого откроется мастер **развертывания контейнера Docker в Azure**.</span><span class="sxs-lookup"><span data-stu-id="3c4c6-116">The **Deploy Docker Container on Azure** wizard opens.</span></span>

   ![Мастер развертывания контейнера Docker в Azure][PUB03]

1. <span data-ttu-id="3c4c6-118">В окне **ввода имени образа, выбора пути артефакта и проверки используемого узла Docker** сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="3c4c6-118">In the **Type an image name, select the artifact's path and check a Docker host to be used** window, do the following:</span></span>

   <span data-ttu-id="3c4c6-119">a.</span><span class="sxs-lookup"><span data-stu-id="3c4c6-119">a.</span></span> <span data-ttu-id="3c4c6-120">В текстовом поле **Docker image name** (Имя образа Docker) введите уникальное имя узла Docker.</span><span class="sxs-lookup"><span data-stu-id="3c4c6-120">In the **Docker image name** box, enter a unique name for your Docker host.</span></span> <span data-ttu-id="3c4c6-121">(Мастер создаст это имя автоматически, но его можно изменить.)</span><span class="sxs-lookup"><span data-stu-id="3c4c6-121">(The wizard automatically creates a name, but you can modify it.)</span></span>

   <span data-ttu-id="3c4c6-122">Б.</span><span class="sxs-lookup"><span data-stu-id="3c4c6-122">b.</span></span> <span data-ttu-id="3c4c6-123">В области **Узлы** отображаются все созданные вами узлы Docker.</span><span class="sxs-lookup"><span data-stu-id="3c4c6-123">The **Hosts** area displays any Docker hosts that you have already created.</span></span> <span data-ttu-id="3c4c6-124">Выполните одно из приведенных ниже действий.</span><span class="sxs-lookup"><span data-stu-id="3c4c6-124">Do either of the following:</span></span>

   * <span data-ttu-id="3c4c6-125">Если вы уже создали узел Docker, вы можете развернуть веб-приложение в нем.</span><span class="sxs-lookup"><span data-stu-id="3c4c6-125">If you have an existing Docker host, you can deploy your web app to it.</span></span>
   * <span data-ttu-id="3c4c6-126">Чтобы создать узел Docker, нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="3c4c6-126">To create a new Docker host, click **Add**.</span></span>  
      
      <span data-ttu-id="3c4c6-127">После этого откроется диалоговое окно **Create Docker Host** (Создание узла Docker).</span><span class="sxs-lookup"><span data-stu-id="3c4c6-127">The **Create Docker Host** dialog box opens.</span></span>

   ![Мастер развертывания контейнера Docker в Azure][PUB04a]

1. <span data-ttu-id="3c4c6-129">В окне **Настройка новой виртуальной машины** укажите приведенные ниже параметры для узла Docker.</span><span class="sxs-lookup"><span data-stu-id="3c4c6-129">In the **Configure the new virtual machine** window, specify the following options for your Docker host.</span></span> <span data-ttu-id="3c4c6-130">(Мастер создаст большинство параметров автоматически, но их можно изменить.)</span><span class="sxs-lookup"><span data-stu-id="3c4c6-130">(The wizard automatically generates most of the options for you, but you can modify any of them.)</span></span>

   <span data-ttu-id="3c4c6-131">a.</span><span class="sxs-lookup"><span data-stu-id="3c4c6-131">a.</span></span> <span data-ttu-id="3c4c6-132">**Имя**. Введите уникальное имя узла Docker.</span><span class="sxs-lookup"><span data-stu-id="3c4c6-132">**Name**: Enter a unique name for the Docker host.</span></span> <span data-ttu-id="3c4c6-133">(Это не указанное выше имя образа Docker.)</span><span class="sxs-lookup"><span data-stu-id="3c4c6-133">(It is not the same as the Docker image name that you specified earlier.)</span></span>

   <span data-ttu-id="3c4c6-134">Б.</span><span class="sxs-lookup"><span data-stu-id="3c4c6-134">b.</span></span> <span data-ttu-id="3c4c6-135">**Подписка**. Укажите, какая подписка Azure будет использоваться для узла.</span><span class="sxs-lookup"><span data-stu-id="3c4c6-135">**Subscription**: Enter the Azure subscription that you use for your host.</span></span>

   <span data-ttu-id="3c4c6-136">c.</span><span class="sxs-lookup"><span data-stu-id="3c4c6-136">c.</span></span> <span data-ttu-id="3c4c6-137">**Регион**. Укажите географический регион, где размещен узел.</span><span class="sxs-lookup"><span data-stu-id="3c4c6-137">**Region**: Enter the geographical region where your host is located.</span></span>

   <span data-ttu-id="3c4c6-138">d.</span><span class="sxs-lookup"><span data-stu-id="3c4c6-138">d.</span></span> <span data-ttu-id="3c4c6-139">На вкладке **Host OS and Size** (ОС и размер узла):</span><span class="sxs-lookup"><span data-stu-id="3c4c6-139">On the **Host OS and Size** tab:</span></span> 
   * <span data-ttu-id="3c4c6-140">**Host OS** (ОС узла). Укажите операционную систему виртуальной машины, которая содержит узел.</span><span class="sxs-lookup"><span data-stu-id="3c4c6-140">**Host OS**: Enter the operating system for the virtual machine that contains your host.</span></span>
   * <span data-ttu-id="3c4c6-141">**Size** (Размер). Укажите размер виртуальной машины узла.</span><span class="sxs-lookup"><span data-stu-id="3c4c6-141">**Size**: Enter the virtual-machine size for your host.</span></span>

   <span data-ttu-id="3c4c6-142">д.</span><span class="sxs-lookup"><span data-stu-id="3c4c6-142">e.</span></span> <span data-ttu-id="3c4c6-143">На вкладке **Resource Group** (Группа ресурсов):</span><span class="sxs-lookup"><span data-stu-id="3c4c6-143">On the **Resource Group** tab:</span></span> 
   * <span data-ttu-id="3c4c6-144">**Новая группа ресурсов**. Создайте группу ресурсов для узла.</span><span class="sxs-lookup"><span data-stu-id="3c4c6-144">**New resource group**: Create a new resource group for your host.</span></span>
   * <span data-ttu-id="3c4c6-145">**Существующая группа ресурсов**. Укажите имеющуюся группу ресурсов из учетной записи Azure.</span><span class="sxs-lookup"><span data-stu-id="3c4c6-145">**Existing resource group**: Enter an existing resource group from your Azure account.</span></span>

   <span data-ttu-id="3c4c6-146">f.</span><span class="sxs-lookup"><span data-stu-id="3c4c6-146">f.</span></span> <span data-ttu-id="3c4c6-147">На вкладке **Network** (Сеть):</span><span class="sxs-lookup"><span data-stu-id="3c4c6-147">On the **Network** tab:</span></span> 
   * <span data-ttu-id="3c4c6-148">**New virtual network** (Новая виртуальная сеть). Создайте виртуальную сеть для узла.</span><span class="sxs-lookup"><span data-stu-id="3c4c6-148">**New virtual network**: Create a new virtual network for your host.</span></span>
   * <span data-ttu-id="3c4c6-149">**Existing virtual network** (Имеющаяся виртуальная сеть). Укажите имеющуюся виртуальную сеть из учетной записи Azure.</span><span class="sxs-lookup"><span data-stu-id="3c4c6-149">**Existing virtual network**: Enter an existing virtual network from your Azure account.</span></span>

   <span data-ttu-id="3c4c6-150">ж.</span><span class="sxs-lookup"><span data-stu-id="3c4c6-150">g.</span></span> <span data-ttu-id="3c4c6-151">На вкладке **Storage** (Хранилище):</span><span class="sxs-lookup"><span data-stu-id="3c4c6-151">On the **Storage** tab:</span></span> 
   * <span data-ttu-id="3c4c6-152">**Создать учетную запись хранения**. Создайте учетную запись хранения для узла.</span><span class="sxs-lookup"><span data-stu-id="3c4c6-152">**New storage account**: Create a new storage account for your host.</span></span>
   * <span data-ttu-id="3c4c6-153">**Existing storage account** (Имеющаяся учетная запись хранения). Укажите имеющуюся учетную запись хранения из учетной записи Azure.</span><span class="sxs-lookup"><span data-stu-id="3c4c6-153">**Existing storage account**: Enter an existing storage account from your Azure account.</span></span>

1. <span data-ttu-id="3c4c6-154">Нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="3c4c6-154">Click **Next**.</span></span>

1. <span data-ttu-id="3c4c6-155">В окне **Configure log in credentials and port settings** (Настройка учетных данных для входа в систему и параметров порта) выберите один из следующих параметров.</span><span class="sxs-lookup"><span data-stu-id="3c4c6-155">In the **Configure log in credentials and port settings** window, select one of the following options:</span></span>

   * <span data-ttu-id="3c4c6-156">**Import credentials from Azure Key Vault** (Импортировать учетные данные из Azure Key Vault). Укажите сохраненный ранее набор учетных данных, хранящихся в подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="3c4c6-156">**Import credentials from Azure Key Vault**: Specifies a previously saved set of credentials that are stored in your Azure subscription.</span></span> 

   >[!NOTE]
   ><span data-ttu-id="3c4c6-157">Хранилище Azure Key Vault, созданное с помощью определенной учетной записи или определенного субъекта-службы, не становится автоматически доступным для другой учетной записи или субъекта-службы, которые относятся к той же подписке.</span><span class="sxs-lookup"><span data-stu-id="3c4c6-157">An Azure Key Vault that's created with a specific account or service principal is not automatically accessible by another account or service principal that shares the subscription.</span></span> <span data-ttu-id="3c4c6-158">Чтобы разрешить другой учетной записи или субъекту-службе использовать Key Vault, нужно добавить их на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="3c4c6-158">To allow another account or service principal to use the Key Vault, you must use the Azure portal to add the account or service principal.</span></span>
   >

   * <span data-ttu-id="3c4c6-159">**New log in credentials** (Новые учетные данные для входа). Создайте набор учетных данных для входа в систему.</span><span class="sxs-lookup"><span data-stu-id="3c4c6-159">**New log in credentials**: Creates a new set of login credentials.</span></span> <span data-ttu-id="3c4c6-160">Если вы выбрали этот параметр, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="3c4c6-160">If you select this option, do the following:</span></span> 
    
      * <span data-ttu-id="3c4c6-161">На вкладке **Учетные данные виртуальной машины** выберите один из следующих параметров для учетной записи входа на виртуальную машину узла Docker.</span><span class="sxs-lookup"><span data-stu-id="3c4c6-161">On the **VM Credentials** tab, choose one of the following options for the virtual-machine login credentials of your Docker host:</span></span> 

         * <span data-ttu-id="3c4c6-162">**Имя пользователя.** Укажите имя пользователя для входа на виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="3c4c6-162">**Username**: Enter the username for your virtual machine login credentials.</span></span> 
         * <span data-ttu-id="3c4c6-163">**Пароль** и **Подтверждение.** Укажите пароль для входа на виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="3c4c6-163">**Password** and **Confirm**: Enter the password for your virtual machine login credentials.</span></span> 
         * <span data-ttu-id="3c4c6-164">**SSH.** Укажите параметры Secure Shell (SSH) узла Docker.</span><span class="sxs-lookup"><span data-stu-id="3c4c6-164">**SSH**: Enter the Secure Shell (SSH) settings for your Docker host.</span></span> <span data-ttu-id="3c4c6-165">Вы можете выбрать один из следующих параметров:</span><span class="sxs-lookup"><span data-stu-id="3c4c6-165">You can choose from the following options:</span></span> 
            * <span data-ttu-id="3c4c6-166">**None** (Нет): указывает, что виртуальная машина не разрешает SSH-подключения.</span><span class="sxs-lookup"><span data-stu-id="3c4c6-166">**None**: Specifies that your virtual machine will not allow SSH connections.</span></span> 
            * <span data-ttu-id="3c4c6-167">**Auto-generate** (Автоматическое создание). Автоматически создает необходимые параметры для SSH-подключения.</span><span class="sxs-lookup"><span data-stu-id="3c4c6-167">**Auto-generate**: Automatically creates the requisite settings for connecting via SSH.</span></span> 
            * <span data-ttu-id="3c4c6-168">**Import from directory** (Импорт из каталога). Позволяет указать каталог, содержащий набор ранее сохраненных параметров SSH.</span><span class="sxs-lookup"><span data-stu-id="3c4c6-168">**Import from directory**: Specifies a directory that contains a set of previously saved SSH settings.</span></span> <span data-ttu-id="3c4c6-169">В частности, каталог должен содержать два следующих файла:</span><span class="sxs-lookup"><span data-stu-id="3c4c6-169">The directory must contain the following two files:</span></span> 
               * <span data-ttu-id="3c4c6-170">*id_rsa*. Этот файл содержит идентификационные данные RSA для пользователя.</span><span class="sxs-lookup"><span data-stu-id="3c4c6-170">*id_rsa*: Contains the RSA identification for a user.</span></span> 
               * <span data-ttu-id="3c4c6-171">*id_rsa.pub*. Этот файл содержит открытый ключ RSA, который используемый для проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="3c4c6-171">*id_rsa.pub*: Contains the RSA public key that is used for authentication.</span></span> 
        
         ![Создание узла Docker][PUB05]

      * <span data-ttu-id="3c4c6-173">На вкладке **Docker Daemon Access** (Доступ к управляющей программе Docker) укажите следующие параметры.</span><span class="sxs-lookup"><span data-stu-id="3c4c6-173">On the **Docker Daemon Credentials** tab, specify the following options:</span></span> 

         * <span data-ttu-id="3c4c6-174">**Docker Daemon port** (Порт управляющей программы Docker). Укажите уникальный TCP-порт для узла Docker.</span><span class="sxs-lookup"><span data-stu-id="3c4c6-174">**Docker Daemon port**: Enter the unique TCP port for your Docker host.</span></span> 
         * <span data-ttu-id="3c4c6-175">**Безопасность TLS**. Введите параметры безопасности транспортного уровня для узла Docker.</span><span class="sxs-lookup"><span data-stu-id="3c4c6-175">**TLS Security**: Enter the Transport Layer Security settings for your Docker host.</span></span> <span data-ttu-id="3c4c6-176">Вы можете выбрать один из следующих параметров:</span><span class="sxs-lookup"><span data-stu-id="3c4c6-176">You can choose from the following options:</span></span> 
            * <span data-ttu-id="3c4c6-177">**None** (Нет): указывает, что виртуальная машина не разрешает TLS-подключения.</span><span class="sxs-lookup"><span data-stu-id="3c4c6-177">**None**: Specifies that your virtual machine will not allow TLS connections.</span></span> 
            * <span data-ttu-id="3c4c6-178">**Auto-generate** (Автоматическое создание). Автоматически создает необходимые параметры для TLS-подключения.</span><span class="sxs-lookup"><span data-stu-id="3c4c6-178">**Auto-generate**: Automatically creates the requisite settings for connecting via TLS.</span></span> 
            * <span data-ttu-id="3c4c6-179">**Import from directory** (Импорт из каталога). Позволяет указать каталог, содержащий набор ранее сохраненных параметров TLS.</span><span class="sxs-lookup"><span data-stu-id="3c4c6-179">**Import from directory**: Specifies a directory that contains a set of previously saved TLS settings.</span></span> <span data-ttu-id="3c4c6-180">В частности, каталог должен содержать шесть следующих файлов:</span><span class="sxs-lookup"><span data-stu-id="3c4c6-180">More specifically, the directory must contain the following six files:</span></span> 
               * <span data-ttu-id="3c4c6-181">*ca.pem* и *ca-key.pem*. Эти файлы содержат сертификат и открытый ключ для центра сертификации TLS.</span><span class="sxs-lookup"><span data-stu-id="3c4c6-181">*ca.pem* and *ca-key.pem*: Contain the certificate and public key for the TLS Certificate Authority.</span></span> 
               * <span data-ttu-id="3c4c6-182">*cert.pem* и *key.pem*. Эти файлы содержат сертификат клиента и открытый ключ, которые будут использоваться для аутентификации TLS.</span><span class="sxs-lookup"><span data-stu-id="3c4c6-182">*cert.pem* and *key.pem*: Contain the client certificate and public key that is used for TLS authentication.</span></span> 
               * <span data-ttu-id="3c4c6-183">*server.pem* и *server-key.pem*. Эти файлы содержат сертификат сервера и открытый ключ для узла.</span><span class="sxs-lookup"><span data-stu-id="3c4c6-183">*server.pem* and *server-key.pem*: Contain the server certificate and public key for the host.</span></span> 

         ![Окно Create Docker Host (Создание узла Docker)][PUB06]

1. <span data-ttu-id="3c4c6-185">Указав предыдущие сведения, нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="3c4c6-185">After you have entered all of the preceding information, click **Finish**.</span></span>

1. <span data-ttu-id="3c4c6-186">В мастере **развертывания контейнера Docker в Azure** нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="3c4c6-186">In the **Deploy Docker Container on Azure** wizard, click **Next**.</span></span>

   ![Мастер развертывания контейнера Docker в Azure][PUB07]

1. <span data-ttu-id="3c4c6-188">В окне **Configure the Docker container to be created** (Настройка создаваемого контейнера Docker) выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="3c4c6-188">In the **Configure the Docker container to be created** window, do the following:</span></span>

   <span data-ttu-id="3c4c6-189">a.</span><span class="sxs-lookup"><span data-stu-id="3c4c6-189">a.</span></span> <span data-ttu-id="3c4c6-190">В текстовом поле **Docker container name** (Имя контейнера Docker) введите уникальное имя контейнера Docker.</span><span class="sxs-lookup"><span data-stu-id="3c4c6-190">In the **Docker container name** box, enter a unique name for your Docker container.</span></span>

   <span data-ttu-id="3c4c6-191">Б.</span><span class="sxs-lookup"><span data-stu-id="3c4c6-191">b.</span></span> <span data-ttu-id="3c4c6-192">Выберите один из следующих образов Docker:</span><span class="sxs-lookup"><span data-stu-id="3c4c6-192">Choose one of the following Docker images:</span></span> 

      * <span data-ttu-id="3c4c6-193">**Predefined Docker image** (Предопределенный образ Docker). Укажите имеющийся образ Docker из Azure.</span><span class="sxs-lookup"><span data-stu-id="3c4c6-193">**Predefined Docker image**: Specifies a pre-existing Docker image from Azure.</span></span> 

      >[!NOTE]
      ><span data-ttu-id="3c4c6-194">Список образов Docker в этом поле состоит из нескольких образов, в которые набор средств Azure устанавливает исправление таким образом, чтобы артефакт развертывался автоматически.</span><span class="sxs-lookup"><span data-stu-id="3c4c6-194">The list of Docker images in this box consists of several images that the Azure Toolkit has been configured to patch so that your artifact is deployed automatically.</span></span>
      >

      * <span data-ttu-id="3c4c6-195">**Custom Dockerfile** (Пользовательский Dockerfile). Укажите сохраненный ранее Dockerfile на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="3c4c6-195">**Custom Dockerfile**: Specifies a previously saved Dockerfile from your local computer.</span></span>

      >[!NOTE]
      ><span data-ttu-id="3c4c6-196">Это расширенная функция для разработчиков, желающих развернуть собственный Dockerfile.</span><span class="sxs-lookup"><span data-stu-id="3c4c6-196">This is a more advanced feature for developers who want to deploy their own Dockerfile.</span></span> <span data-ttu-id="3c4c6-197">Однако за правильность сборки Dockerfile отвечают сами разработчики, использующие эту возможность.</span><span class="sxs-lookup"><span data-stu-id="3c4c6-197">However, it is up to developers who use this option to ensure that their Dockerfile is built correctly.</span></span> <span data-ttu-id="3c4c6-198">Набор средств Azure не проверяет содержимое пользовательского Dockerfile, поэтому при наличии проблем в Dockerfile развертывание может завершиться ошибкой.</span><span class="sxs-lookup"><span data-stu-id="3c4c6-198">The Azure Toolkit does not validate the content in a custom Dockerfile, so the deployment might fail if the Dockerfile has issues.</span></span> <span data-ttu-id="3c4c6-199">Кроме того, набор средств Azure ожидает, что пользовательский Dockerfile содержит артефакт веб-приложения, и попытается установить HTTP-подключение.</span><span class="sxs-lookup"><span data-stu-id="3c4c6-199">In addition, the Azure Toolkit expects the custom Dockerfile to contain a web app artifact, and it will attempt to open an HTTP connection.</span></span> <span data-ttu-id="3c4c6-200">Если разработчики публикуют артефакт другого типа, то после развертывания могут возникнуть некритичные ошибки.</span><span class="sxs-lookup"><span data-stu-id="3c4c6-200">If developers publish a different type of artifact, they may receive innocuous errors after deployment.</span></span>
      >

   <span data-ttu-id="3c4c6-201">c.</span><span class="sxs-lookup"><span data-stu-id="3c4c6-201">c.</span></span> <span data-ttu-id="3c4c6-202">**Port settings** (Параметры порта). Укажите уникальную привязку TCP-порта для контейнера Docker.</span><span class="sxs-lookup"><span data-stu-id="3c4c6-202">**Port settings**: Enter the unique TCP port binding for your Docker container.</span></span>

      ![Окно настройки создаваемого контейнера Docker][PUB08]

1. <span data-ttu-id="3c4c6-204">Выполнив все предыдущие действия, нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="3c4c6-204">After you have completed all of the preceding steps, click **Finish**.</span></span>

<span data-ttu-id="3c4c6-205">Набор средств Azure начинает развертывание веб-приложения в контейнере Docker Azure.</span><span class="sxs-lookup"><span data-stu-id="3c4c6-205">The Azure Toolkit begins deploying your web app to Azure in a Docker container.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="3c4c6-206">Дополнительная информация</span><span class="sxs-lookup"><span data-stu-id="3c4c6-206">Next steps</span></span>

<span data-ttu-id="3c4c6-207">Дополнительные материалы по Docker доступны на официальном [веб-сайте Docker].</span><span class="sxs-lookup"><span data-stu-id="3c4c6-207">For additional resources for Docker, see the official [Docker website].</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-additional-resources](../includes/azure-toolkit-for-eclipse-additional-resources.md)]

<!-- URL List -->

[веб-сайте Docker]: https://www.docker.com/

<!-- IMG List -->

[PUB01]: media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB01.png
[PUB02]: media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB02.png
[PUB03]: media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB03.png
[PUB04a]: media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB04a.png
[PUB04b]: media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB04b.png
[PUB04c]: media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB04c.png
[PUB04d]: media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB04d.png
[PUB05]: media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB05.png
[PUB06]: media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB06.png
[PUB07]: media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB07.png
[PUB08]: media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB08.png