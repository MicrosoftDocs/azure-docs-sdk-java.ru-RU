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
ms.openlocfilehash: 05fb81466202547cb1bad34caae0f94f16a9d21b
ms.sourcegitcommit: b64017f119177f97da7a5930489874e67b09c0fc
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/09/2018
ms.locfileid: "48893655"
---
# <a name="publish-a-web-app-as-a-docker-container-by-using-the-azure-toolkit-for-intellij"></a>Публикация веб-приложение в виде контейнера Docker с помощью набора средств Azure для IntelliJ

Контейнеры Docker широко используются при развертывании веб-приложений. При этом разработчики могут объединить все зависимости и файлы проекта в одном пакете, а затем развернуть его на сервере. Набор средств Azure для IntelliJ упрощает этот процесс для разработчиков на языке Java, предоставляя функции *публикации в виде контейнера Docker* при развертывании в Microsoft Azure. В этой статье описаны действия, необходимые для публикации приложений в Azure в качестве контейнеров Docker.

> [!NOTE]
>
> Дополнительные сведения о Docker см. на [веб-сайте Docker].
>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="publish-your-web-app-to-azure-by-using-a-docker-container"></a>Публикация веб-приложения в Azure с помощью контейнера Docker

> [!NOTE]
> * Чтобы опубликовать веб-приложение, необходимо создать готовый к развертыванию артефакт. Дополнительные сведения о создании артефактов см. в [этом разделе](#artifacts).
>
> * После выполнения развертывания с помощью мастера хотя бы один раз большинство указанных параметров будет использоваться по умолчанию при повторном запуске этого мастера.
>

1. Откройте проект веб-приложения в IntelliJ.

2. Чтобы запустить мастер **публикации в виде контейнера Docker**, выполните одно из следующих действий:

   * Щелкните правой кнопкой мыши проект в окне средства **Проект**, щелкните **Azure**, а затем выберите **Publish as Docker Container** (Опубликовать как контейнер Docker):

      ![Команда публикации в виде контейнера Docker][PUB01]

   * На панели инструментов IntelliJ нажмите кнопку **Publish Group** (Опубликовать группу), а затем выберите **Publish as Docker Container** (Опубликовать как контейнер Docker):

      ![Команда публикации в виде контейнера Docker][PUB02]  
    После этого откроется мастер **развертывания контейнера Docker в Azure**.

   ![Мастер развертывания контейнера Docker в Azure][PUB03]

3. В окне **ввода имени образа, выбора пути артефакта и проверки используемого узла Docker** сделайте следующее: 

   a. В текстовом поле **Docker image name** (Имя образа Docker) введите уникальное имя узла Docker. (Мастер создаст это имя автоматически, но его можно изменить.) 

   b. В области **Узлы** отображаются все созданные вами узлы Docker. Выполните одно из приведенных ниже действий. 
   * Если вы уже создали узел Docker, вы можете развернуть веб-приложение в нем.
   * Чтобы создать узел Docker, щелкните зеленый знак "плюс" (**+**).  
     После этого откроется диалоговое окно **Create Docker Host** (Создание узла Docker). 

     ![Мастер развертывания контейнера Docker в Azure][PUB04a]

4. В окне **настройки новой виртуальной машины** укажите приведенные ниже параметры узла Docker. (Мастер создаст большинство параметров автоматически, но их можно изменить.) 

   a. В текстовом поле **Имя** введите уникальное имя узла Docker. (Это не указанное выше имя образа Docker.) 
    
   b. В текстовом поле **Подписка** укажите, какая подписка Azure будет использоваться для узла. 
      
   c. В текстовом поле **Регион** укажите географический регион, где размещен узел.
      
   d. На вкладке **OS and Size** (ОС и размер) сделайте следующее:      
      * **Host OS** (ОС узла). Укажите операционную систему виртуальной машины, которая содержит узел. 
      * **Size** (Размер). Укажите размер виртуальной машины узла.   
       
   д. На вкладке **Группа ресурсов** выберите один из следующих вариантов:      
      * **Новая группа ресурсов.** Создайте группу ресурсов для узла.
      * **Существующая группа ресурсов.** Укажите имеющуюся группу ресурсов из учетной записи Azure. 
       
   Е. На вкладке **Сеть** выберите один из следующих вариантов:      
      * **New virtual network** (Новая виртуальная сеть). Создайте виртуальную сеть для узла.
      * **Existing virtual network** (Имеющаяся виртуальная сеть). Укажите имеющуюся виртуальную сеть из учетной записи Azure. 
       
   ж. На вкладке **Хранилище** выберите один из следующих вариантов:      
      * **Создать учетную запись хранения.** Создайте учетную запись хранения для узла.
      * **Existing storage account** (Имеющаяся учетная запись хранения). Укажите имеющуюся учетную запись хранения из учетной записи Azure.
       
5. Щелкните **Далее**.  
     После этого откроется окно **Configure log in credentials and port settings** (Настройка учетных данных для входа в систему и параметров порта).

      ![Окно настройки учетных данных для входа в систему и параметров порта][PUB05]

6. Выберите один из следующих вариантов:

   * **Import credentials from Azure Key Vault** (Импортировать учетные данные из Azure Key Vault). Укажите сохраненный ранее набор учетных данных, хранящихся в подписке Azure.

       > [!NOTE]
       > Хранилище Azure Key Vault, созданное с помощью определенной учетной записи или определенного субъекта-службы, не становится автоматически доступным для другой учетной записи или субъекта-службы, которые относятся к той же подписке. Чтобы разрешить другой учетной записи или субъекту-службе использовать Key Vault, нужно добавить их на портале Azure.

   * **New log in credentials** (Новые учетные данные для входа). Создайте набор учетных данных для входа в систему. Если вы выбрали этот параметр, сделайте следующее:

     a. На вкладке **VM Credentials** (Учетные данные виртуальной машины) укажите следующие учетные данные для входа на виртуальную машину узла Docker:

     * **Username** (Имя пользователя). Укажите имя пользователя для входа на виртуальную машину.

     * **Password** (Пароль) и **Confirm** (Подтверждение). Укажите пароль для входа на виртуальную машину.

     * **SSH.** Укажите параметры Secure Shell (SSH) узла Docker. Вы можете выбрать один из следующих вариантов:

     * **None** (Нет). Указывает, что виртуальная машина не разрешает SSH-подключения.

     * **Auto-generate** (Автоматическое создание). Автоматически создает необходимые параметры для SSH-подключения.

     * **Import from directory** (Импорт из каталога). Позволяет указать каталог, содержащий набор ранее сохраненных параметров SSH. В частности, каталог должен содержать два следующих файла:

         * *id_rsa*. Этот файл содержит идентификационные данные RSA для пользователя.

         * *id_rsa.pub*. Этот файл содержит открытый ключ RSA, который используемый для проверки подлинности.

     b. На вкладке **Docker Daemon Access** (Доступ к управляющей программе Docker) укажите следующие сведения:

     ![Окно Create Docker Host (Создание узла Docker)][PUB06]
    
     * **Docker Daemon port** (Порт управляющей программы Docker). Укажите уникальный TCP-порт для узла Docker.
    
     * **Безопасность TLS**. Введите параметры безопасности транспортного уровня для узла Docker. Вы можете выбрать один из следующих параметров:
    
     * **None** (Нет). Указывает, что виртуальная машина не разрешает TLS-подключения.
        
     * **Auto-generate** (Автоматическое создание). Автоматически создает необходимые параметры для TLS-подключения.
        
     * **Import from directory** (Импорт из каталога). Позволяет указать каталог, содержащий набор ранее сохраненных параметров TLS. В частности, каталог должен содержать шесть следующих файлов:
        
         * *ca.pem* и *ca-key.pem*. Эти файлы содержат сертификат и открытый ключ для центра сертификации TLS.
            
         * *cert.pem* и *key.pem*. Эти файлы содержат сертификат клиента и открытый ключ, которые будут использоваться для проверки подлинности TLS.
            
         * *server.pem* и *server-key.pem*. Эти файлы содержат сертификат клиента и открытый ключ, которые будут использоваться для проверки подлинности TLS.

7. Указав необходимые сведения, нажмите кнопку **Готово**.  
    После этого снова отобразится мастер **развертывания контейнера Docker в Azure**.

   ![Мастер развертывания контейнера Docker в Azure][PUB07]

8. Щелкните **Далее**.  
    Откроется окно **Configure the Docker container to be created** (Настройка создаваемого контейнера Docker).

   ![Окно настройки создаваемого контейнера Docker][PUB08]

9. В окне **Configure the Docker container to be created** (Настройка создаваемого контейнера Docker) укажите следующие параметры: 

   a. В текстовом поле **Docker container name** (Имя контейнера Docker) введите уникальное имя контейнера Docker.

   b. Выберите один из следующих образов Docker: 

      * **Predefined Docker image** (Предопределенный образ Docker). Укажите имеющийся образ Docker из Azure. 

        > [!NOTE]
        > Список образов Docker в этом поле состоит из нескольких образов, в которые набор средств Azure устанавливает исправление таким образом, чтобы артефакт развертывался автоматически. 

      * **Custom Dockerfile** (Пользовательский Dockerfile). Укажите сохраненный ранее Dockerfile на локальном компьютере.

        > [!NOTE]
        > Это расширенная функция для разработчиков, желающих развернуть собственный Dockerfile. Однако за правильность сборки Dockerfile отвечают сами разработчики, использующие эту возможность. Набор средств Azure не проверяет содержимое пользовательского Dockerfile, поэтому при наличии проблем с этим файлом развертывание может завершиться ошибкой. Кроме того, набор средств Azure ожидает, что пользовательский Dockerfile содержит артефакт веб-приложения, и попытается установить HTTP-подключение. Если разработчики публикуют артефакт другого типа, то после развертывания могут возникнуть некритичные ошибки.

   c. В текстовом поле **Port settings** (Параметры порта) укажите уникальную привязку TCP-порта для контейнера Docker. 

10. Выполнив все предыдущие действия, нажмите кнопку **Готово**. 

Набор средств Azure начинает развертывание веб-приложения в контейнере Docker Azure. Если вы не настроили развертывание IntelliJ в фоновом режиме, появится индикатор выполнения **развертывания в Azure**. 

![Индикатор выполнения развертывания][PUB09]

<a name="artifacts"></a>
## <a name="additional-information-about-creating-artifacts"></a>Дополнительные сведения о создании артефактов

Чтобы создать готовый к развертыванию артефакт, выполните следующее:

1. Откройте проект веб-приложения в IntelliJ.

2. В меню **File** (Файл) выберите **Project Structure** (Структура проекта).

   ![Команда Project Structure (Структура проекта)][ART01]

3. Чтобы добавить артефакт, щелкните зеленый знак "плюс" (**+**), а затем выберите **Web Application: Artifact** (Веб-приложение: артефакт).

   ![Команда Web Application: Artifact (Веб-приложение: артефакт)][ART02]

4. В текстовом поле **Имя** укажите имя артефакта ( без расширения *WAR*) и нажмите кнопку **ОК**.

   ![Поле "Имя" артефакта][ART03]

Дополнительные сведения о создании артефактов в IntelliJ см. в статье [Configuring Artifacts] (Настройка артефактов) на веб-сайте JetBrains.

## <a name="next-steps"></a>Дополнительная информация

Дополнительные материалы по Docker доступны на официальном [веб-сайте Docker].

[!INCLUDE [azure-toolkit-for-intellij-additional-resources](../includes/azure-toolkit-for-intellij-additional-resources.md)]

<!-- URL List -->

[веб-сайте Docker]: https://www.docker.com/
[Configuring artifacts]: https://www.jetbrains.com/help/idea/2016.1/configuring-artifacts.html (Настройка артефактов)

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
