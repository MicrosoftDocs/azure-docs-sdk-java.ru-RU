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
ms.openlocfilehash: 3db8bf06892ca6c53cf93ee4ce151549044806d1
ms.sourcegitcommit: 613c1ffd2e0279fc7a96fca98aa1809563f52ee1
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/18/2017
---
# <a name="publish-a-web-app-as-a-docker-container-by-using-the-azure-toolkit-for-intellij"></a><span data-ttu-id="470de-103">Публикация веб-приложение в виде контейнера Docker с помощью набора средств Azure для IntelliJ</span><span class="sxs-lookup"><span data-stu-id="470de-103">Publish a web app as a Docker container by using the Azure Toolkit for IntelliJ</span></span>

<span data-ttu-id="470de-104">Контейнеры Docker широко используются при развертывании веб-приложений.</span><span class="sxs-lookup"><span data-stu-id="470de-104">Docker containers are a widely used method for deploying web applications.</span></span> <span data-ttu-id="470de-105">При этом разработчики могут объединить все зависимости и файлы проекта в одном пакете, а затем развернуть его на сервере.</span><span class="sxs-lookup"><span data-stu-id="470de-105">By using Docker containers, developers can consolidate all their project files and dependencies into a single package for deployment to a server.</span></span> <span data-ttu-id="470de-106">Набор средств Azure для IntelliJ упрощает этот процесс для разработчиков на языке Java, предоставляя функции *публикации в виде контейнера Docker* при развертывании в Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="470de-106">The Azure Toolkit for IntelliJ simplifies this process for Java developers by adding *Publish as Docker Container* features for deployment to Microsoft Azure.</span></span> <span data-ttu-id="470de-107">В этой статье описаны действия, необходимые для публикации приложений в Azure в качестве контейнеров Docker.</span><span class="sxs-lookup"><span data-stu-id="470de-107">This article walks you through the steps required to publish your applications to Azure as Docker containers.</span></span>

> [!NOTE]
>
> <span data-ttu-id="470de-108">Дополнительные сведения о Docker см. на [веб-сайте Docker].</span><span class="sxs-lookup"><span data-stu-id="470de-108">More information about Docker is available on the [Docker website].</span></span>
>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="publish-your-web-app-to-azure-by-using-a-docker-container"></a><span data-ttu-id="470de-109">Публикация веб-приложения в Azure с помощью контейнера Docker</span><span class="sxs-lookup"><span data-stu-id="470de-109">Publish your web app to Azure by using a Docker container</span></span>

> [!NOTE]
> * <span data-ttu-id="470de-110">Чтобы опубликовать веб-приложение, необходимо создать готовый к развертыванию артефакт.</span><span class="sxs-lookup"><span data-stu-id="470de-110">To publish your web app, you must create a deployment-ready artifact.</span></span> <span data-ttu-id="470de-111">Дополнительные сведения о создании артефактов см. в [этом разделе](#artifacts).</span><span class="sxs-lookup"><span data-stu-id="470de-111">To learn more, see the [Additional information about creating artifacts](#artifacts) section.</span></span>
>
> * <span data-ttu-id="470de-112">После выполнения развертывания с помощью мастера хотя бы один раз большинство указанных параметров будет использоваться по умолчанию при повторном запуске этого мастера.</span><span class="sxs-lookup"><span data-stu-id="470de-112">After you have completed the deployment wizard at least once, most of your settings are used as defaults when you run the wizard again.</span></span>
>

1. <span data-ttu-id="470de-113">Откройте проект веб-приложения в IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="470de-113">Open your web app project in IntelliJ.</span></span>

2. <span data-ttu-id="470de-114">Чтобы запустить мастер **публикации в виде контейнера Docker**, выполните одно из следующих действий:</span><span class="sxs-lookup"><span data-stu-id="470de-114">To start the **Publish as Docker Container** wizard, do either of the following:</span></span>

   * <span data-ttu-id="470de-115">Щелкните правой кнопкой мыши проект в окне средства **Проект**, щелкните **Azure**, а затем выберите **Publish as Docker Container** (Опубликовать как контейнер Docker):</span><span class="sxs-lookup"><span data-stu-id="470de-115">In the **Project** tool window, right-click your project, click **Azure**, and then click **Publish as Docker Container**:</span></span>

      ![Команда публикации в виде контейнера Docker][PUB01]

   * <span data-ttu-id="470de-117">На панели инструментов IntelliJ нажмите кнопку **Publish Group** (Опубликовать группу), а затем выберите **Publish as Docker Container** (Опубликовать как контейнер Docker):</span><span class="sxs-lookup"><span data-stu-id="470de-117">On the IntelliJ toolbar, click the **Publish Group** button, and then click **Publish as Docker Container**:</span></span>

      <span data-ttu-id="470de-118">![Команда публикации в виде контейнера Docker][PUB02]</span><span class="sxs-lookup"><span data-stu-id="470de-118">![The Publish as Docker Container command][PUB02]</span></span>  
    <span data-ttu-id="470de-119">После этого откроется мастер **развертывания контейнера Docker в Azure**.</span><span class="sxs-lookup"><span data-stu-id="470de-119">The **Deploy Docker Container on Azure** wizard opens.</span></span>

   ![Мастер развертывания контейнера Docker в Azure][PUB03]

3. <span data-ttu-id="470de-121">В окне **ввода имени образа, выбора пути артефакта и проверки используемого узла Docker** сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="470de-121">In the **Type an image name, select the artifact's path and check a Docker host to be used** window, do the following:</span></span> 

   <span data-ttu-id="470de-122">а.</span><span class="sxs-lookup"><span data-stu-id="470de-122">a.</span></span> <span data-ttu-id="470de-123">В текстовом поле **Docker image name** (Имя образа Docker) введите уникальное имя узла Docker.</span><span class="sxs-lookup"><span data-stu-id="470de-123">In the **Docker image name** box, enter a unique name for your Docker host.</span></span> <span data-ttu-id="470de-124">(Мастер создаст это имя автоматически, но его можно изменить.)</span><span class="sxs-lookup"><span data-stu-id="470de-124">(The wizard automatically creates a name, but you can modify it.)</span></span> 

   <span data-ttu-id="470de-125">b.</span><span class="sxs-lookup"><span data-stu-id="470de-125">b.</span></span> <span data-ttu-id="470de-126">В области **Узлы** отображаются все созданные вами узлы Docker.</span><span class="sxs-lookup"><span data-stu-id="470de-126">The **Hosts** area displays any Docker hosts that you have already created.</span></span> <span data-ttu-id="470de-127">Выполните одно из приведенных ниже действий.</span><span class="sxs-lookup"><span data-stu-id="470de-127">Do either of the following:</span></span> 
      * <span data-ttu-id="470de-128">Если вы уже создали узел Docker, вы можете развернуть веб-приложение в нем.</span><span class="sxs-lookup"><span data-stu-id="470de-128">If you have an existing Docker host, you can deploy your web app to it.</span></span>
      * <span data-ttu-id="470de-129">Чтобы создать узел Docker, щелкните зеленый знак "плюс" (**+**).</span><span class="sxs-lookup"><span data-stu-id="470de-129">To create a Docker host, click the green plus sign (**+**).</span></span>  
       <span data-ttu-id="470de-130">После этого откроется диалоговое окно **Create Docker Host** (Создание узла Docker).</span><span class="sxs-lookup"><span data-stu-id="470de-130">The **Create Docker Host** dialog box opens.</span></span> 

      ![Мастер развертывания контейнера Docker в Azure][PUB04a]

4. <span data-ttu-id="470de-132">В окне **настройки новой виртуальной машины** укажите приведенные ниже параметры узла Docker.</span><span class="sxs-lookup"><span data-stu-id="470de-132">In the **Configure the new virtual machine** window, provide the following information about your Docker host.</span></span> <span data-ttu-id="470de-133">(Мастер создаст большинство параметров автоматически, но их можно изменить.)</span><span class="sxs-lookup"><span data-stu-id="470de-133">(The wizard automatically generates most of the information for you, but you can modify any of them.)</span></span> 

   <span data-ttu-id="470de-134">а.</span><span class="sxs-lookup"><span data-stu-id="470de-134">a.</span></span> <span data-ttu-id="470de-135">В текстовом поле **Имя** введите уникальное имя узла Docker.</span><span class="sxs-lookup"><span data-stu-id="470de-135">In the **Name** box, enter a unique name for the Docker host.</span></span> <span data-ttu-id="470de-136">(Это не указанное выше имя образа Docker.)</span><span class="sxs-lookup"><span data-stu-id="470de-136">(It is not the same as the Docker image name that you specified earlier.)</span></span> 
    
   <span data-ttu-id="470de-137">b.</span><span class="sxs-lookup"><span data-stu-id="470de-137">b.</span></span> <span data-ttu-id="470de-138">В текстовом поле **Подписка** укажите, какая подписка Azure будет использоваться для узла.</span><span class="sxs-lookup"><span data-stu-id="470de-138">In the **Subscription** box, enter the Azure subscription that you use for your host.</span></span> 
      
   <span data-ttu-id="470de-139">c.</span><span class="sxs-lookup"><span data-stu-id="470de-139">c.</span></span> <span data-ttu-id="470de-140">В текстовом поле **Регион** укажите географический регион, где размещен узел.</span><span class="sxs-lookup"><span data-stu-id="470de-140">In the **Region** box, enter the geographical region where your host is located.</span></span>
      
   <span data-ttu-id="470de-141">г)</span><span class="sxs-lookup"><span data-stu-id="470de-141">d.</span></span> <span data-ttu-id="470de-142">На вкладке **OS and Size** (ОС и размер) сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="470de-142">On the **OS and Size** tab, do the following:</span></span>      
      * <span data-ttu-id="470de-143">**Host OS** (ОС узла). Укажите операционную систему виртуальной машины, которая содержит узел.</span><span class="sxs-lookup"><span data-stu-id="470de-143">**Host OS**: Enter the operating system for the virtual machine that contains your host.</span></span> 
      * <span data-ttu-id="470de-144">**Size** (Размер). Укажите размер виртуальной машины узла.</span><span class="sxs-lookup"><span data-stu-id="470de-144">**Size**: Enter the virtual-machine size for your host.</span></span>   
       
   <span data-ttu-id="470de-145">д.</span><span class="sxs-lookup"><span data-stu-id="470de-145">e.</span></span> <span data-ttu-id="470de-146">На вкладке **Группа ресурсов** выберите один из следующих вариантов:</span><span class="sxs-lookup"><span data-stu-id="470de-146">On the **Resource Group** tab, select either of the following:</span></span>      
      * <span data-ttu-id="470de-147">**Новая группа ресурсов.** Создайте группу ресурсов для узла.</span><span class="sxs-lookup"><span data-stu-id="470de-147">**New resource group**: Create a resource group for your host.</span></span>
      * <span data-ttu-id="470de-148">**Существующая группа ресурсов.** Укажите имеющуюся группу ресурсов из учетной записи Azure.</span><span class="sxs-lookup"><span data-stu-id="470de-148">**Existing resource group**: Specify an existing resource group from your Azure account.</span></span> 
       
   <span data-ttu-id="470de-149">f.</span><span class="sxs-lookup"><span data-stu-id="470de-149">f.</span></span> <span data-ttu-id="470de-150">На вкладке **Сеть** выберите один из следующих вариантов:</span><span class="sxs-lookup"><span data-stu-id="470de-150">On the **Network** tab, select either of the following:</span></span>      
      * <span data-ttu-id="470de-151">**New virtual network** (Новая виртуальная сеть). Создайте виртуальную сеть для узла.</span><span class="sxs-lookup"><span data-stu-id="470de-151">**New virtual network**: Create a virtual network for your host.</span></span>
      * <span data-ttu-id="470de-152">**Existing virtual network** (Имеющаяся виртуальная сеть). Укажите имеющуюся виртуальную сеть из учетной записи Azure.</span><span class="sxs-lookup"><span data-stu-id="470de-152">**Existing virtual network**: Specify an existing virtual network from your Azure account.</span></span> 
       
   <span data-ttu-id="470de-153">ж.</span><span class="sxs-lookup"><span data-stu-id="470de-153">g.</span></span> <span data-ttu-id="470de-154">На вкладке **Хранилище** выберите один из следующих вариантов:</span><span class="sxs-lookup"><span data-stu-id="470de-154">On the **Storage** tab, select either of the following:</span></span>      
      * <span data-ttu-id="470de-155">**Создать учетную запись хранения.** Создайте учетную запись хранения для узла.</span><span class="sxs-lookup"><span data-stu-id="470de-155">**New storage account**: Create a storage account for your host.</span></span>
      * <span data-ttu-id="470de-156">**Existing storage account** (Имеющаяся учетная запись хранения). Укажите имеющуюся учетную запись хранения из учетной записи Azure.</span><span class="sxs-lookup"><span data-stu-id="470de-156">**Existing storage account**: Specify an existing storage account from your Azure account.</span></span>
       
5. <span data-ttu-id="470de-157">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="470de-157">Click **Next**.</span></span>  
     <span data-ttu-id="470de-158">После этого откроется окно **Configure log in credentials and port settings** (Настройка учетных данных для входа в систему и параметров порта).</span><span class="sxs-lookup"><span data-stu-id="470de-158">The **Configure log in credentials and port settings** window opens.</span></span>

      ![Окно настройки учетных данных для входа в систему и параметров порта][PUB05]

6. <span data-ttu-id="470de-160">Выберите один из следующих вариантов:</span><span class="sxs-lookup"><span data-stu-id="470de-160">Select one of the following options:</span></span>

      * <span data-ttu-id="470de-161">**Import credentials from Azure Key Vault** (Импортировать учетные данные из Azure Key Vault). Укажите сохраненный ранее набор учетных данных, хранящихся в подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="470de-161">**Import credentials from Azure Key Vault**: Specify a previously saved set of credentials that are stored in your Azure subscription.</span></span>

          > [!NOTE]
          > <span data-ttu-id="470de-162">Хранилище Azure Key Vault, созданное с помощью определенной учетной записи или определенного субъекта-службы, не становится автоматически доступным для другой учетной записи или субъекта-службы, которые относятся к той же подписке.</span><span class="sxs-lookup"><span data-stu-id="470de-162">An Azure key vault that's created with a specific account or service principal is not automatically accessible by another account or service principal that shares the subscription.</span></span> <span data-ttu-id="470de-163">Чтобы разрешить другой учетной записи или субъекту-службе использовать Key Vault, нужно добавить их на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="470de-163">To allow another account or service principal to use the key vault, you must use the Azure portal to add the account or service principal.</span></span>

      * <span data-ttu-id="470de-164">**New log in credentials** (Новые учетные данные для входа). Создайте набор учетных данных для входа в систему.</span><span class="sxs-lookup"><span data-stu-id="470de-164">**New log in credentials**: Create a new set of login credentials.</span></span> <span data-ttu-id="470de-165">Если вы выбрали этот параметр, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="470de-165">If you select this option, do the following:</span></span>

        <span data-ttu-id="470de-166">а.</span><span class="sxs-lookup"><span data-stu-id="470de-166">a.</span></span> <span data-ttu-id="470de-167">На вкладке **Учетные данные для виртуальной машины** укажите следующие параметры учетных данных для входа на виртуальную машину узла Docker: * **Имя пользователя** . Укажите имя пользователя для входа на виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="470de-167">On the **VM Credentials** tab, provide the following information for the virtual-machine login credentials of your Docker host: * **Username**: Enter the username for your virtual-machine login credentials.</span></span>
             <span data-ttu-id="470de-168">* **Пароль** и **Подтверждение**. Укажите пароль для входа на виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="470de-168">* **Password** and **Confirm**: Enter the password for your virtual-machine login credentials.</span></span>
             <span data-ttu-id="470de-169">* **SSH**. Укажите параметры Secure Shell (SSH) узла Docker.</span><span class="sxs-lookup"><span data-stu-id="470de-169">* **SSH**: Enter the Secure Shell (SSH) settings for your Docker host.</span></span> <span data-ttu-id="470de-170">Выберите один из следующих параметров: * **Нет** . Указывает, что виртуальная машина не разрешает SSH-подключения.</span><span class="sxs-lookup"><span data-stu-id="470de-170">You can select one of the following options: * **None**: Specifies that your virtual machine does not allow SSH connections.</span></span>
                <span data-ttu-id="470de-171">* **Auto-generate** (Автоматическое создание). Автоматически создает необходимые параметры для SSH-подключения.</span><span class="sxs-lookup"><span data-stu-id="470de-171">* **Auto-generate**: Automatically creates the requisite settings for connecting via SSH.</span></span>
                <span data-ttu-id="470de-172">* **Import from directory** (Импорт из каталога). Позволяет указать каталог, содержащий набор ранее сохраненных параметров SSH.</span><span class="sxs-lookup"><span data-stu-id="470de-172">* **Import from directory**: Allows you to specify a directory that contains a set of previously saved SSH settings.</span></span> <span data-ttu-id="470de-173">В частности, каталог должен содержать два следующих файла:</span><span class="sxs-lookup"><span data-stu-id="470de-173">The directory must contain the following two files:</span></span>
                
                  * *id_rsa*: Contains the RSA identification for a user.
                  * *id_rsa.pub*: Contains the RSA public key that is used for authentication.
            
        <span data-ttu-id="470de-174">b.</span><span class="sxs-lookup"><span data-stu-id="470de-174">b.</span></span> <span data-ttu-id="470de-175">На вкладке **Docker Daemon Access** (Доступ к управляющей программе Docker) укажите следующие сведения:</span><span class="sxs-lookup"><span data-stu-id="470de-175">On the **Docker Daemon Access** tab, provide the following information:</span></span>

          ![Окно Create Docker Host (Создание узла Docker)][PUB06]
    
             * **Docker Daemon port**: Enter the unique TCP port for your Docker host.
             * **TLS Security**: Enter the Transport Layer Security settings for your Docker host. You can choose from the following options:
                * **None**: Specifies that your virtual machine does not allow TLS connections.
                * **Auto-generate**: Automatically creates the requisite settings for connecting via TLS.
                * **Import from directory**: Specifies a directory that contains a set of previously saved TLS settings. The directory must contain the following six files: 
                   * *ca.pem* and *ca-key.pem*: Contain the certificate and public key for the TLS Certificate Authority.
                   * *cert.pem* and *key.pem*: Contain client certificate and public key which will be used for TLS authentication.
                   * *server.pem* and *server-key.pem*: Contain the client certificate and public key that is used for TLS authentication.

7. <span data-ttu-id="470de-177">Указав необходимые сведения, нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="470de-177">After you have entered the required information, click **Finish**.</span></span>  
    <span data-ttu-id="470de-178">После этого снова отобразится мастер **развертывания контейнера Docker в Azure**.</span><span class="sxs-lookup"><span data-stu-id="470de-178">The **Deploy Docker Container on Azure** wizard reappears.</span></span>

   ![Мастер развертывания контейнера Docker в Azure][PUB07]

8. <span data-ttu-id="470de-180">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="470de-180">Click **Next**.</span></span>  
    <span data-ttu-id="470de-181">Откроется окно **Configure the Docker container to be created** (Настройка создаваемого контейнера Docker).</span><span class="sxs-lookup"><span data-stu-id="470de-181">The **Configure the Docker container to be created** window opens.</span></span>

   ![Окно настройки создаваемого контейнера Docker][PUB08]

9. <span data-ttu-id="470de-183">В окне **Configure the Docker container to be created** (Настройка создаваемого контейнера Docker) укажите следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="470de-183">In the **Configure the Docker container to be created** window, provide the following information:</span></span> 

   <span data-ttu-id="470de-184">а.</span><span class="sxs-lookup"><span data-stu-id="470de-184">a.</span></span> <span data-ttu-id="470de-185">В текстовом поле **Docker container name** (Имя контейнера Docker) введите уникальное имя контейнера Docker.</span><span class="sxs-lookup"><span data-stu-id="470de-185">In the **Docker container name** box, enter a unique name for your Docker container.</span></span>

   <span data-ttu-id="470de-186">b.</span><span class="sxs-lookup"><span data-stu-id="470de-186">b.</span></span> <span data-ttu-id="470de-187">Выберите один из следующих образов Docker:</span><span class="sxs-lookup"><span data-stu-id="470de-187">Choose one of the following Docker images:</span></span> 

      * <span data-ttu-id="470de-188">**Predefined Docker image** (Предопределенный образ Docker). Укажите имеющийся образ Docker из Azure.</span><span class="sxs-lookup"><span data-stu-id="470de-188">**Predefined Docker image**: Specify a pre-existing Docker image from Azure.</span></span> 

        > [!NOTE]
        > <span data-ttu-id="470de-189">Список образов Docker в этом поле состоит из нескольких образов, в которые набор средств Azure устанавливает исправление таким образом, чтобы артефакт развертывался автоматически.</span><span class="sxs-lookup"><span data-stu-id="470de-189">The list of Docker images in this box consists of several images that the Azure Toolkit has been configured to patch so that your artifact is deployed automatically.</span></span> 

      * <span data-ttu-id="470de-190">**Custom Dockerfile** (Пользовательский Dockerfile). Укажите сохраненный ранее Dockerfile на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="470de-190">**Custom Dockerfile**: Specify a previously saved Dockerfile from your local computer.</span></span>

        > [!NOTE]
        > <span data-ttu-id="470de-191">Это расширенная функция для разработчиков, желающих развернуть собственный Dockerfile.</span><span class="sxs-lookup"><span data-stu-id="470de-191">This is a more advanced feature for developers who want to deploy their own Dockerfile.</span></span> <span data-ttu-id="470de-192">Однако за правильность сборки Dockerfile отвечают сами разработчики, использующие эту возможность.</span><span class="sxs-lookup"><span data-stu-id="470de-192">However, it is up to developers who use this option to ensure that their Dockerfile is built correctly.</span></span> <span data-ttu-id="470de-193">Набор средств Azure не проверяет содержимое пользовательского Dockerfile, поэтому при наличии проблем с этим файлом развертывание может завершиться ошибкой.</span><span class="sxs-lookup"><span data-stu-id="470de-193">Because the Azure Toolkit does not validate the content in a custom Dockerfile, the deployment might fail if the Dockerfile has issues.</span></span> <span data-ttu-id="470de-194">Кроме того, набор средств Azure ожидает, что пользовательский Dockerfile содержит артефакт веб-приложения, и попытается установить HTTP-подключение.</span><span class="sxs-lookup"><span data-stu-id="470de-194">In addition, because the Azure Toolkit expects the custom Dockerfile to contain a web app artifact, it attempts to open an HTTP connection.</span></span> <span data-ttu-id="470de-195">Если разработчики публикуют артефакт другого типа, то после развертывания могут возникнуть некритичные ошибки.</span><span class="sxs-lookup"><span data-stu-id="470de-195">If developers publish a different type of artifact, they might receive innocuous errors after deployment.</span></span>

   <span data-ttu-id="470de-196">c.</span><span class="sxs-lookup"><span data-stu-id="470de-196">c.</span></span> <span data-ttu-id="470de-197">В текстовом поле **Port settings** (Параметры порта) укажите уникальную привязку TCP-порта для контейнера Docker.</span><span class="sxs-lookup"><span data-stu-id="470de-197">In the **Port settings** box, enter the unique TCP port binding for your Docker container.</span></span> 

10. <span data-ttu-id="470de-198">Выполнив все предыдущие действия, нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="470de-198">After you have completed the preceding steps, click **Finish**.</span></span> 

<span data-ttu-id="470de-199">Набор средств Azure начинает развертывание веб-приложения в контейнере Docker Azure.</span><span class="sxs-lookup"><span data-stu-id="470de-199">The Azure Toolkit begins deploying your web app to Azure in a Docker container.</span></span> <span data-ttu-id="470de-200">Если вы не настроили развертывание IntelliJ в фоновом режиме, появится индикатор выполнения **развертывания в Azure**.</span><span class="sxs-lookup"><span data-stu-id="470de-200">Unless you have configured IntelliJ to be deployed in the background, a **Deploying to Azure** progress bar appears.</span></span> 

![Индикатор выполнения развертывания][PUB09]

<a name="artifacts"></a>
## <a name="additional-information-about-creating-artifacts"></a><span data-ttu-id="470de-202">Дополнительные сведения о создании артефактов</span><span class="sxs-lookup"><span data-stu-id="470de-202">Additional information about creating artifacts</span></span>

<span data-ttu-id="470de-203">Чтобы создать готовый к развертыванию артефакт, выполните следующее:</span><span class="sxs-lookup"><span data-stu-id="470de-203">To create a deployment-ready artifact, do the following:</span></span>

1. <span data-ttu-id="470de-204">Откройте проект веб-приложения в IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="470de-204">Open your web app project in IntelliJ.</span></span>

2. <span data-ttu-id="470de-205">В меню **File** (Файл) выберите **Project Structure** (Структура проекта).</span><span class="sxs-lookup"><span data-stu-id="470de-205">Click **File**, and then click **Project Structure**.</span></span>

   ![Команда Project Structure (Структура проекта)][ART01]

3. <span data-ttu-id="470de-207">Чтобы добавить артефакт, щелкните зеленый знак "плюс" (**+**), а затем выберите **Web Application: Artifact** (Веб-приложение: артефакт).</span><span class="sxs-lookup"><span data-stu-id="470de-207">To add an artifact, click the green plus sign (**+**), and then click **Web Application: Archive**.</span></span>

   ![Команда Web Application: Artifact (Веб-приложение: артефакт)][ART02]

4. <span data-ttu-id="470de-209">В текстовом поле **Имя** укажите имя артефакта ( без расширения *WAR*) и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="470de-209">In the **Name** box, enter a name for your artifact (do not include the *.war* extension), and then click **OK**.</span></span>

   ![Поле "Имя" артефакта][ART03]

<span data-ttu-id="470de-211">Дополнительные сведения о создании артефактов в IntelliJ см. в статье [Configuring Artifacts] (Настройка артефактов) на веб-сайте JetBrains.</span><span class="sxs-lookup"><span data-stu-id="470de-211">For more information about creating artifacts in IntelliJ, see [Configuring artifacts] on the JetBrains website.</span></span>

## <a name="next-steps"></a><span data-ttu-id="470de-212">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="470de-212">Next steps</span></span>

<span data-ttu-id="470de-213">Дополнительные материалы по Docker доступны на официальном [веб-сайте Docker].</span><span class="sxs-lookup"><span data-stu-id="470de-213">For additional resources for Docker, see the official [Docker website].</span></span>

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
