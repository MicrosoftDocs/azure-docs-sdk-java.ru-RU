---
title: "Публикация контейнера Docker с помощью набора средств Azure для IntelliJ"
description: "Вы можете узнать, как опубликовать веб-приложение в Microsoft Azure в виде контейнера Docker с помощью набора средств Azure для IntelliJ."
services: 
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 11/01/2017
ms.author: robmcm
ms.openlocfilehash: ed63d73e8a0c89af14613b1b1a880f1d40495b8d
ms.sourcegitcommit: 558d875e9a255deb5b83b3f1646bd1dd9eee0a0d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/01/2018
---
# <a name="publish-a-web-app-as-a-docker-container-by-using-the-azure-toolkit-for-intellij"></a><span data-ttu-id="96ed8-103">Публикация веб-приложение в виде контейнера Docker с помощью набора средств Azure для IntelliJ</span><span class="sxs-lookup"><span data-stu-id="96ed8-103">Publish a web app as a Docker container by using the Azure Toolkit for IntelliJ</span></span>

<span data-ttu-id="96ed8-104">Контейнеры Docker широко используются при развертывании веб-приложений.</span><span class="sxs-lookup"><span data-stu-id="96ed8-104">Docker containers are a widely used method for deploying web applications.</span></span> <span data-ttu-id="96ed8-105">При этом разработчики могут объединить все зависимости и файлы проекта в одном пакете, а затем развернуть его на сервере.</span><span class="sxs-lookup"><span data-stu-id="96ed8-105">By using Docker containers, developers can consolidate all their project files and dependencies into a single package for deployment to a server.</span></span> <span data-ttu-id="96ed8-106">Набор средств Azure для IntelliJ упрощает этот процесс для разработчиков на языке Java, предоставляя функции *публикации в виде контейнера Docker* при развертывании в Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="96ed8-106">The Azure Toolkit for IntelliJ simplifies this process for Java developers by adding *Publish as Docker Container* features for deployment to Microsoft Azure.</span></span> <span data-ttu-id="96ed8-107">В этой статье описаны действия, необходимые для публикации приложений в Azure в качестве контейнеров Docker.</span><span class="sxs-lookup"><span data-stu-id="96ed8-107">This article walks you through the steps required to publish your applications to Azure as Docker containers.</span></span>

> [!NOTE]
>
> <span data-ttu-id="96ed8-108">Дополнительные сведения о Docker см. на [веб-сайте Docker].</span><span class="sxs-lookup"><span data-stu-id="96ed8-108">More information about Docker is available on the [Docker website].</span></span>
>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="publish-your-web-app-to-azure-by-using-a-docker-container"></a><span data-ttu-id="96ed8-109">Публикация веб-приложения в Azure с помощью контейнера Docker</span><span class="sxs-lookup"><span data-stu-id="96ed8-109">Publish your web app to Azure by using a Docker container</span></span>

> [!NOTE]
> * <span data-ttu-id="96ed8-110">Чтобы опубликовать веб-приложение, необходимо создать готовый к развертыванию артефакт.</span><span class="sxs-lookup"><span data-stu-id="96ed8-110">To publish your web app, you must create a deployment-ready artifact.</span></span> <span data-ttu-id="96ed8-111">Дополнительные сведения о создании артефактов см. в [этом разделе](#artifacts).</span><span class="sxs-lookup"><span data-stu-id="96ed8-111">To learn more, see the [Additional information about creating artifacts](#artifacts) section.</span></span>
>
> * <span data-ttu-id="96ed8-112">После выполнения развертывания с помощью мастера хотя бы один раз большинство указанных параметров будет использоваться по умолчанию при повторном запуске этого мастера.</span><span class="sxs-lookup"><span data-stu-id="96ed8-112">After you have completed the deployment wizard at least once, most of your settings are used as defaults when you run the wizard again.</span></span>
>

1. <span data-ttu-id="96ed8-113">Откройте проект веб-приложения в IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="96ed8-113">Open your web app project in IntelliJ.</span></span>

2. <span data-ttu-id="96ed8-114">Чтобы запустить мастер **публикации в виде контейнера Docker**, выполните одно из следующих действий:</span><span class="sxs-lookup"><span data-stu-id="96ed8-114">To start the **Publish as Docker Container** wizard, do either of the following:</span></span>

   * <span data-ttu-id="96ed8-115">Щелкните правой кнопкой мыши проект в окне средства **Проект**, щелкните **Azure**, а затем выберите **Publish as Docker Container** (Опубликовать как контейнер Docker):</span><span class="sxs-lookup"><span data-stu-id="96ed8-115">In the **Project** tool window, right-click your project, click **Azure**, and then click **Publish as Docker Container**:</span></span>

      ![Команда публикации в виде контейнера Docker][PUB01]

   * <span data-ttu-id="96ed8-117">На панели инструментов IntelliJ нажмите кнопку **Publish Group** (Опубликовать группу), а затем выберите **Publish as Docker Container** (Опубликовать как контейнер Docker):</span><span class="sxs-lookup"><span data-stu-id="96ed8-117">On the IntelliJ toolbar, click the **Publish Group** button, and then click **Publish as Docker Container**:</span></span>

      <span data-ttu-id="96ed8-118">![Команда публикации в виде контейнера Docker][PUB02]</span><span class="sxs-lookup"><span data-stu-id="96ed8-118">![The Publish as Docker Container command][PUB02]</span></span>  
    <span data-ttu-id="96ed8-119">После этого откроется мастер **развертывания контейнера Docker в Azure**.</span><span class="sxs-lookup"><span data-stu-id="96ed8-119">The **Deploy Docker Container on Azure** wizard opens.</span></span>

   ![Мастер развертывания контейнера Docker в Azure][PUB03]

3. <span data-ttu-id="96ed8-121">В окне **ввода имени образа, выбора пути артефакта и проверки используемого узла Docker** сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="96ed8-121">In the **Type an image name, select the artifact's path and check a Docker host to be used** window, do the following:</span></span> 

   <span data-ttu-id="96ed8-122">a.</span><span class="sxs-lookup"><span data-stu-id="96ed8-122">a.</span></span> <span data-ttu-id="96ed8-123">В текстовом поле **Docker image name** (Имя образа Docker) введите уникальное имя узла Docker.</span><span class="sxs-lookup"><span data-stu-id="96ed8-123">In the **Docker image name** box, enter a unique name for your Docker host.</span></span> <span data-ttu-id="96ed8-124">(Мастер создаст это имя автоматически, но его можно изменить.)</span><span class="sxs-lookup"><span data-stu-id="96ed8-124">(The wizard automatically creates a name, but you can modify it.)</span></span> 

   <span data-ttu-id="96ed8-125">Б.</span><span class="sxs-lookup"><span data-stu-id="96ed8-125">b.</span></span> <span data-ttu-id="96ed8-126">В области **Узлы** отображаются все созданные вами узлы Docker.</span><span class="sxs-lookup"><span data-stu-id="96ed8-126">The **Hosts** area displays any Docker hosts that you have already created.</span></span> <span data-ttu-id="96ed8-127">Выполните одно из приведенных ниже действий.</span><span class="sxs-lookup"><span data-stu-id="96ed8-127">Do either of the following:</span></span> 
      * <span data-ttu-id="96ed8-128">Если вы уже создали узел Docker, вы можете развернуть веб-приложение в нем.</span><span class="sxs-lookup"><span data-stu-id="96ed8-128">If you have an existing Docker host, you can deploy your web app to it.</span></span>
      * <span data-ttu-id="96ed8-129">Чтобы создать узел Docker, щелкните зеленый знак "плюс" (**+**).</span><span class="sxs-lookup"><span data-stu-id="96ed8-129">To create a Docker host, click the green plus sign (**+**).</span></span>  
       <span data-ttu-id="96ed8-130">После этого откроется диалоговое окно **Create Docker Host** (Создание узла Docker).</span><span class="sxs-lookup"><span data-stu-id="96ed8-130">The **Create Docker Host** dialog box opens.</span></span> 

      ![Мастер развертывания контейнера Docker в Azure][PUB04a]

4. <span data-ttu-id="96ed8-132">В окне **настройки новой виртуальной машины** укажите приведенные ниже параметры узла Docker.</span><span class="sxs-lookup"><span data-stu-id="96ed8-132">In the **Configure the new virtual machine** window, provide the following information about your Docker host.</span></span> <span data-ttu-id="96ed8-133">(Мастер создаст большинство параметров автоматически, но их можно изменить.)</span><span class="sxs-lookup"><span data-stu-id="96ed8-133">(The wizard automatically generates most of the information for you, but you can modify any of them.)</span></span> 

   <span data-ttu-id="96ed8-134">a.</span><span class="sxs-lookup"><span data-stu-id="96ed8-134">a.</span></span> <span data-ttu-id="96ed8-135">В текстовом поле **Имя** введите уникальное имя узла Docker.</span><span class="sxs-lookup"><span data-stu-id="96ed8-135">In the **Name** box, enter a unique name for the Docker host.</span></span> <span data-ttu-id="96ed8-136">(Это не указанное выше имя образа Docker.)</span><span class="sxs-lookup"><span data-stu-id="96ed8-136">(It is not the same as the Docker image name that you specified earlier.)</span></span> 
    
   <span data-ttu-id="96ed8-137">Б.</span><span class="sxs-lookup"><span data-stu-id="96ed8-137">b.</span></span> <span data-ttu-id="96ed8-138">В текстовом поле **Подписка** укажите, какая подписка Azure будет использоваться для узла.</span><span class="sxs-lookup"><span data-stu-id="96ed8-138">In the **Subscription** box, enter the Azure subscription that you use for your host.</span></span> 
      
   <span data-ttu-id="96ed8-139">c.</span><span class="sxs-lookup"><span data-stu-id="96ed8-139">c.</span></span> <span data-ttu-id="96ed8-140">В текстовом поле **Регион** укажите географический регион, где размещен узел.</span><span class="sxs-lookup"><span data-stu-id="96ed8-140">In the **Region** box, enter the geographical region where your host is located.</span></span>
      
   <span data-ttu-id="96ed8-141">d.</span><span class="sxs-lookup"><span data-stu-id="96ed8-141">d.</span></span> <span data-ttu-id="96ed8-142">На вкладке **OS and Size** (ОС и размер) сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="96ed8-142">On the **OS and Size** tab, do the following:</span></span>      
      * <span data-ttu-id="96ed8-143">**Host OS** (ОС узла). Укажите операционную систему виртуальной машины, которая содержит узел.</span><span class="sxs-lookup"><span data-stu-id="96ed8-143">**Host OS**: Enter the operating system for the virtual machine that contains your host.</span></span> 
      * <span data-ttu-id="96ed8-144">**Size** (Размер). Укажите размер виртуальной машины узла.</span><span class="sxs-lookup"><span data-stu-id="96ed8-144">**Size**: Enter the virtual-machine size for your host.</span></span>   
       
   <span data-ttu-id="96ed8-145">д.</span><span class="sxs-lookup"><span data-stu-id="96ed8-145">e.</span></span> <span data-ttu-id="96ed8-146">На вкладке **Группа ресурсов** выберите один из следующих вариантов:</span><span class="sxs-lookup"><span data-stu-id="96ed8-146">On the **Resource Group** tab, select either of the following:</span></span>      
      * <span data-ttu-id="96ed8-147">**Новая группа ресурсов.** Создайте группу ресурсов для узла.</span><span class="sxs-lookup"><span data-stu-id="96ed8-147">**New resource group**: Create a resource group for your host.</span></span>
      * <span data-ttu-id="96ed8-148">**Существующая группа ресурсов.** Укажите имеющуюся группу ресурсов из учетной записи Azure.</span><span class="sxs-lookup"><span data-stu-id="96ed8-148">**Existing resource group**: Specify an existing resource group from your Azure account.</span></span> 
       
   <span data-ttu-id="96ed8-149">f.</span><span class="sxs-lookup"><span data-stu-id="96ed8-149">f.</span></span> <span data-ttu-id="96ed8-150">На вкладке **Сеть** выберите один из следующих вариантов:</span><span class="sxs-lookup"><span data-stu-id="96ed8-150">On the **Network** tab, select either of the following:</span></span>      
      * <span data-ttu-id="96ed8-151">**New virtual network** (Новая виртуальная сеть). Создайте виртуальную сеть для узла.</span><span class="sxs-lookup"><span data-stu-id="96ed8-151">**New virtual network**: Create a virtual network for your host.</span></span>
      * <span data-ttu-id="96ed8-152">**Existing virtual network** (Имеющаяся виртуальная сеть). Укажите имеющуюся виртуальную сеть из учетной записи Azure.</span><span class="sxs-lookup"><span data-stu-id="96ed8-152">**Existing virtual network**: Specify an existing virtual network from your Azure account.</span></span> 
       
   <span data-ttu-id="96ed8-153">ж.</span><span class="sxs-lookup"><span data-stu-id="96ed8-153">g.</span></span> <span data-ttu-id="96ed8-154">На вкладке **Хранилище** выберите один из следующих вариантов:</span><span class="sxs-lookup"><span data-stu-id="96ed8-154">On the **Storage** tab, select either of the following:</span></span>      
      * <span data-ttu-id="96ed8-155">**Создать учетную запись хранения.** Создайте учетную запись хранения для узла.</span><span class="sxs-lookup"><span data-stu-id="96ed8-155">**New storage account**: Create a storage account for your host.</span></span>
      * <span data-ttu-id="96ed8-156">**Existing storage account** (Имеющаяся учетная запись хранения). Укажите имеющуюся учетную запись хранения из учетной записи Azure.</span><span class="sxs-lookup"><span data-stu-id="96ed8-156">**Existing storage account**: Specify an existing storage account from your Azure account.</span></span>
       
5. <span data-ttu-id="96ed8-157">Нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="96ed8-157">Click **Next**.</span></span>  
     <span data-ttu-id="96ed8-158">После этого откроется окно **Configure log in credentials and port settings** (Настройка учетных данных для входа в систему и параметров порта).</span><span class="sxs-lookup"><span data-stu-id="96ed8-158">The **Configure log in credentials and port settings** window opens.</span></span>

      ![Окно настройки учетных данных для входа в систему и параметров порта][PUB05]

6. <span data-ttu-id="96ed8-160">Выберите один из следующих вариантов:</span><span class="sxs-lookup"><span data-stu-id="96ed8-160">Select one of the following options:</span></span>

      * <span data-ttu-id="96ed8-161">**Import credentials from Azure Key Vault** (Импортировать учетные данные из Azure Key Vault). Укажите сохраненный ранее набор учетных данных, хранящихся в подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="96ed8-161">**Import credentials from Azure Key Vault**: Specify a previously saved set of credentials that are stored in your Azure subscription.</span></span>

          > [!NOTE]
          > <span data-ttu-id="96ed8-162">Хранилище Azure Key Vault, созданное с помощью определенной учетной записи или определенного субъекта-службы, не становится автоматически доступным для другой учетной записи или субъекта-службы, которые относятся к той же подписке.</span><span class="sxs-lookup"><span data-stu-id="96ed8-162">An Azure key vault that's created with a specific account or service principal is not automatically accessible by another account or service principal that shares the subscription.</span></span> <span data-ttu-id="96ed8-163">Чтобы разрешить другой учетной записи или субъекту-службе использовать Key Vault, нужно добавить их на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="96ed8-163">To allow another account or service principal to use the key vault, you must use the Azure portal to add the account or service principal.</span></span>

      * <span data-ttu-id="96ed8-164">**New log in credentials** (Новые учетные данные для входа). Создайте набор учетных данных для входа в систему.</span><span class="sxs-lookup"><span data-stu-id="96ed8-164">**New log in credentials**: Create a new set of login credentials.</span></span> <span data-ttu-id="96ed8-165">Если вы выбрали этот параметр, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="96ed8-165">If you select this option, do the following:</span></span>

        <span data-ttu-id="96ed8-166">a.</span><span class="sxs-lookup"><span data-stu-id="96ed8-166">a.</span></span> <span data-ttu-id="96ed8-167">На вкладке **Учетные данные для виртуальной машины** укажите следующие параметры учетных данных для входа на виртуальную машину узла Docker: \* **Имя пользователя** . Укажите имя пользователя для входа на виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="96ed8-167">On the **VM Credentials** tab, provide the following information for the virtual-machine login credentials of your Docker host: \* **Username**: Enter the username for your virtual-machine login credentials.</span></span>
             <span data-ttu-id="96ed8-168">\* **Пароль** и **Подтверждение**. Укажите пароль для входа на виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="96ed8-168">\* **Password** and **Confirm**: Enter the password for your virtual-machine login credentials.</span></span>
             <span data-ttu-id="96ed8-169">\* **SSH**. Укажите параметры Secure Shell (SSH) узла Docker.</span><span class="sxs-lookup"><span data-stu-id="96ed8-169">\* **SSH**: Enter the Secure Shell (SSH) settings for your Docker host.</span></span> <span data-ttu-id="96ed8-170">Выберите один из следующих параметров: \* **Нет** . Указывает, что виртуальная машина не разрешает SSH-подключения.</span><span class="sxs-lookup"><span data-stu-id="96ed8-170">You can select one of the following options: \* **None**: Specifies that your virtual machine does not allow SSH connections.</span></span>
                <span data-ttu-id="96ed8-171">\* **Auto-generate** (Автоматическое создание). Автоматически создает необходимые параметры для SSH-подключения.</span><span class="sxs-lookup"><span data-stu-id="96ed8-171">\* **Auto-generate**: Automatically creates the requisite settings for connecting via SSH.</span></span>
                <span data-ttu-id="96ed8-172">\* **Import from directory** (Импорт из каталога). Позволяет указать каталог, содержащий набор ранее сохраненных параметров SSH.</span><span class="sxs-lookup"><span data-stu-id="96ed8-172">\* **Import from directory**: Allows you to specify a directory that contains a set of previously saved SSH settings.</span></span> <span data-ttu-id="96ed8-173">В частности, каталог должен содержать два следующих файла:</span><span class="sxs-lookup"><span data-stu-id="96ed8-173">The directory must contain the following two files:</span></span>
                
                  * *id_rsa*: Contains the RSA identification for a user.
                  * *id_rsa.pub*: Contains the RSA public key that is used for authentication.
            
        <span data-ttu-id="96ed8-174">Б.</span><span class="sxs-lookup"><span data-stu-id="96ed8-174">b.</span></span> <span data-ttu-id="96ed8-175">На вкладке **Docker Daemon Access** (Доступ к управляющей программе Docker) укажите следующие сведения:</span><span class="sxs-lookup"><span data-stu-id="96ed8-175">On the **Docker Daemon Access** tab, provide the following information:</span></span>

         ![Окно Create Docker Host (Создание узла Docker)][PUB06]
    
           * <span data-ttu-id="96ed8-177">**Docker Daemon port** (Порт управляющей программы Docker). Укажите уникальный TCP-порт для узла Docker.</span><span class="sxs-lookup"><span data-stu-id="96ed8-177">**Docker Daemon port**: Enter the unique TCP port for your Docker host.</span></span>
           * <span data-ttu-id="96ed8-178">**Безопасность TLS**. Введите параметры безопасности транспортного уровня для узла Docker.</span><span class="sxs-lookup"><span data-stu-id="96ed8-178">**TLS Security**: Enter the Transport Layer Security settings for your Docker host.</span></span> <span data-ttu-id="96ed8-179">Вы можете выбрать один из следующих параметров:</span><span class="sxs-lookup"><span data-stu-id="96ed8-179">You can choose from the following options:</span></span>
                * <span data-ttu-id="96ed8-180">**None** (Нет). Указывает, что виртуальная машина не разрешает TLS-подключения.</span><span class="sxs-lookup"><span data-stu-id="96ed8-180">**None**: Specifies that your virtual machine does not allow TLS connections.</span></span>
                * <span data-ttu-id="96ed8-181">**Auto-generate** (Автоматическое создание). Автоматически создает необходимые параметры для TLS-подключения.</span><span class="sxs-lookup"><span data-stu-id="96ed8-181">**Auto-generate**: Automatically creates the requisite settings for connecting via TLS.</span></span>
                * <span data-ttu-id="96ed8-182">**Import from directory** (Импорт из каталога). Позволяет указать каталог, содержащий набор ранее сохраненных параметров TLS.</span><span class="sxs-lookup"><span data-stu-id="96ed8-182">**Import from directory**: Specifies a directory that contains a set of previously saved TLS settings.</span></span> <span data-ttu-id="96ed8-183">В частности, каталог должен содержать шесть следующих файлов:</span><span class="sxs-lookup"><span data-stu-id="96ed8-183">The directory must contain the following six files:</span></span> 
                   * <span data-ttu-id="96ed8-184">*ca.pem* и *ca-key.pem*. Эти файлы содержат сертификат и открытый ключ для центра сертификации TLS.</span><span class="sxs-lookup"><span data-stu-id="96ed8-184">*ca.pem* and *ca-key.pem*: Contain the certificate and public key for the TLS Certificate Authority.</span></span>
                   * <span data-ttu-id="96ed8-185">*cert.pem* и *key.pem*. Эти файлы содержат сертификат клиента и открытый ключ, которые будут использоваться для проверки подлинности TLS.</span><span class="sxs-lookup"><span data-stu-id="96ed8-185">*cert.pem* and *key.pem*: Contain client certificate and public key which will be used for TLS authentication.</span></span>
                   * <span data-ttu-id="96ed8-186">*server.pem* и *server-key.pem*. Эти файлы содержат сертификат клиента и открытый ключ, которые будут использоваться для проверки подлинности TLS.</span><span class="sxs-lookup"><span data-stu-id="96ed8-186">*server.pem* and *server-key.pem*: Contain the client certificate and public key that is used for TLS authentication.</span></span>

7. <span data-ttu-id="96ed8-187">Указав необходимые сведения, нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="96ed8-187">After you have entered the required information, click **Finish**.</span></span>  
    <span data-ttu-id="96ed8-188">После этого снова отобразится мастер **развертывания контейнера Docker в Azure**.</span><span class="sxs-lookup"><span data-stu-id="96ed8-188">The **Deploy Docker Container on Azure** wizard reappears.</span></span>

   ![Мастер развертывания контейнера Docker в Azure][PUB07]

8. <span data-ttu-id="96ed8-190">Нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="96ed8-190">Click **Next**.</span></span>  
    <span data-ttu-id="96ed8-191">Откроется окно **Configure the Docker container to be created** (Настройка создаваемого контейнера Docker).</span><span class="sxs-lookup"><span data-stu-id="96ed8-191">The **Configure the Docker container to be created** window opens.</span></span>

   ![Окно настройки создаваемого контейнера Docker][PUB08]

9. <span data-ttu-id="96ed8-193">В окне **Configure the Docker container to be created** (Настройка создаваемого контейнера Docker) укажите следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="96ed8-193">In the **Configure the Docker container to be created** window, provide the following information:</span></span> 

   <span data-ttu-id="96ed8-194">a.</span><span class="sxs-lookup"><span data-stu-id="96ed8-194">a.</span></span> <span data-ttu-id="96ed8-195">В текстовом поле **Docker container name** (Имя контейнера Docker) введите уникальное имя контейнера Docker.</span><span class="sxs-lookup"><span data-stu-id="96ed8-195">In the **Docker container name** box, enter a unique name for your Docker container.</span></span>

   <span data-ttu-id="96ed8-196">Б.</span><span class="sxs-lookup"><span data-stu-id="96ed8-196">b.</span></span> <span data-ttu-id="96ed8-197">Выберите один из следующих образов Docker:</span><span class="sxs-lookup"><span data-stu-id="96ed8-197">Choose one of the following Docker images:</span></span> 

      * <span data-ttu-id="96ed8-198">**Predefined Docker image** (Предопределенный образ Docker). Укажите имеющийся образ Docker из Azure.</span><span class="sxs-lookup"><span data-stu-id="96ed8-198">**Predefined Docker image**: Specify a pre-existing Docker image from Azure.</span></span> 

        > [!NOTE]
        > <span data-ttu-id="96ed8-199">Список образов Docker в этом поле состоит из нескольких образов, в которые набор средств Azure устанавливает исправление таким образом, чтобы артефакт развертывался автоматически.</span><span class="sxs-lookup"><span data-stu-id="96ed8-199">The list of Docker images in this box consists of several images that the Azure Toolkit has been configured to patch so that your artifact is deployed automatically.</span></span> 

      * <span data-ttu-id="96ed8-200">**Custom Dockerfile** (Пользовательский Dockerfile). Укажите сохраненный ранее Dockerfile на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="96ed8-200">**Custom Dockerfile**: Specify a previously saved Dockerfile from your local computer.</span></span>

        > [!NOTE]
        > <span data-ttu-id="96ed8-201">Это расширенная функция для разработчиков, желающих развернуть собственный Dockerfile.</span><span class="sxs-lookup"><span data-stu-id="96ed8-201">This is a more advanced feature for developers who want to deploy their own Dockerfile.</span></span> <span data-ttu-id="96ed8-202">Однако за правильность сборки Dockerfile отвечают сами разработчики, использующие эту возможность.</span><span class="sxs-lookup"><span data-stu-id="96ed8-202">However, it is up to developers who use this option to ensure that their Dockerfile is built correctly.</span></span> <span data-ttu-id="96ed8-203">Набор средств Azure не проверяет содержимое пользовательского Dockerfile, поэтому при наличии проблем с этим файлом развертывание может завершиться ошибкой.</span><span class="sxs-lookup"><span data-stu-id="96ed8-203">Because the Azure Toolkit does not validate the content in a custom Dockerfile, the deployment might fail if the Dockerfile has issues.</span></span> <span data-ttu-id="96ed8-204">Кроме того, набор средств Azure ожидает, что пользовательский Dockerfile содержит артефакт веб-приложения, и попытается установить HTTP-подключение.</span><span class="sxs-lookup"><span data-stu-id="96ed8-204">In addition, because the Azure Toolkit expects the custom Dockerfile to contain a web app artifact, it attempts to open an HTTP connection.</span></span> <span data-ttu-id="96ed8-205">Если разработчики публикуют артефакт другого типа, то после развертывания могут возникнуть некритичные ошибки.</span><span class="sxs-lookup"><span data-stu-id="96ed8-205">If developers publish a different type of artifact, they might receive innocuous errors after deployment.</span></span>

   <span data-ttu-id="96ed8-206">c.</span><span class="sxs-lookup"><span data-stu-id="96ed8-206">c.</span></span> <span data-ttu-id="96ed8-207">В текстовом поле **Port settings** (Параметры порта) укажите уникальную привязку TCP-порта для контейнера Docker.</span><span class="sxs-lookup"><span data-stu-id="96ed8-207">In the **Port settings** box, enter the unique TCP port binding for your Docker container.</span></span> 

10. <span data-ttu-id="96ed8-208">Выполнив все предыдущие действия, нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="96ed8-208">After you have completed the preceding steps, click **Finish**.</span></span> 

<span data-ttu-id="96ed8-209">Набор средств Azure начинает развертывание веб-приложения в контейнере Docker Azure.</span><span class="sxs-lookup"><span data-stu-id="96ed8-209">The Azure Toolkit begins deploying your web app to Azure in a Docker container.</span></span> <span data-ttu-id="96ed8-210">Если вы не настроили развертывание IntelliJ в фоновом режиме, появится индикатор выполнения **развертывания в Azure**.</span><span class="sxs-lookup"><span data-stu-id="96ed8-210">Unless you have configured IntelliJ to be deployed in the background, a **Deploying to Azure** progress bar appears.</span></span> 

![Индикатор выполнения развертывания][PUB09]

<a name="artifacts"></a>
## <a name="additional-information-about-creating-artifacts"></a><span data-ttu-id="96ed8-212">Дополнительные сведения о создании артефактов</span><span class="sxs-lookup"><span data-stu-id="96ed8-212">Additional information about creating artifacts</span></span>

<span data-ttu-id="96ed8-213">Чтобы создать готовый к развертыванию артефакт, выполните следующее:</span><span class="sxs-lookup"><span data-stu-id="96ed8-213">To create a deployment-ready artifact, do the following:</span></span>

1. <span data-ttu-id="96ed8-214">Откройте проект веб-приложения в IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="96ed8-214">Open your web app project in IntelliJ.</span></span>

2. <span data-ttu-id="96ed8-215">В меню **File** (Файл) выберите **Project Structure** (Структура проекта).</span><span class="sxs-lookup"><span data-stu-id="96ed8-215">Click **File**, and then click **Project Structure**.</span></span>

   ![Команда Project Structure (Структура проекта)][ART01]

3. <span data-ttu-id="96ed8-217">Чтобы добавить артефакт, щелкните зеленый знак "плюс" (**+**), а затем выберите **Web Application: Artifact** (Веб-приложение: артефакт).</span><span class="sxs-lookup"><span data-stu-id="96ed8-217">To add an artifact, click the green plus sign (**+**), and then click **Web Application: Archive**.</span></span>

   ![Команда Web Application: Artifact (Веб-приложение: артефакт)][ART02]

4. <span data-ttu-id="96ed8-219">В текстовом поле **Имя** укажите имя артефакта ( без расширения *WAR*) и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="96ed8-219">In the **Name** box, enter a name for your artifact (do not include the *.war* extension), and then click **OK**.</span></span>

   ![Поле "Имя" артефакта][ART03]

<span data-ttu-id="96ed8-221">Дополнительные сведения о создании артефактов в IntelliJ см. в статье [Configuring Artifacts] (Настройка артефактов) на веб-сайте JetBrains.</span><span class="sxs-lookup"><span data-stu-id="96ed8-221">For more information about creating artifacts in IntelliJ, see [Configuring artifacts] on the JetBrains website.</span></span>

## <a name="next-steps"></a><span data-ttu-id="96ed8-222">Дополнительная информация</span><span class="sxs-lookup"><span data-stu-id="96ed8-222">Next steps</span></span>

<span data-ttu-id="96ed8-223">Дополнительные материалы по Docker доступны на официальном [веб-сайте Docker].</span><span class="sxs-lookup"><span data-stu-id="96ed8-223">For additional resources for Docker, see the official [Docker website].</span></span>

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
