---
title: Использование образов Docker с JDK для разработки приложений Java в Azure
description: ''
author: bmitchell287
manager: douge
ms.author: brendm
ms.date: 4/9/2019
ms.devlang: java
ms.topic: conceptual
ms.openlocfilehash: ee8df2a08b23d090965cb42e2c15b934d4785e7c
ms.sourcegitcommit: 03379369346974c6e80f86e7129b885112b5c1a9
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/29/2019
ms.locfileid: "64910231"
---
# <a name="use-docker-with-a-jdk-for-azure"></a><span data-ttu-id="31177-102">Использование Docker с JDK для среды Azure</span><span class="sxs-lookup"><span data-stu-id="31177-102">Use Docker with a JDK for Azure</span></span> 

<span data-ttu-id="31177-103">Готовые образы Docker для Java 7, 8 и 11 доступны через [Docker Hub](https://hub.docker.com/_/microsoft-java-se).</span><span class="sxs-lookup"><span data-stu-id="31177-103">Pre-built Docker images for Java 7, 8, and 11 are available through [Docker Hub](https://hub.docker.com/_/microsoft-java-se).</span></span>

<span data-ttu-id="31177-104">В Docker Hub доступны сертифицированные образы контейнеров Docker для Zulu JDK, JRE и автономной среды JRE на основе нескольких базовых образов ОС.</span><span class="sxs-lookup"><span data-stu-id="31177-104">Certified Docker container images for Zulu JDK, JRE, and JRE-headless on multiple base OS images are available at Docker Hub:</span></span>

* <span data-ttu-id="31177-105">[JDK](https://hub.docker.com/_/microsoft-java-jdk).</span><span class="sxs-lookup"><span data-stu-id="31177-105">[JDK](https://hub.docker.com/_/microsoft-java-jdk)</span></span>
* [<span data-ttu-id="31177-106">JRE</span><span class="sxs-lookup"><span data-stu-id="31177-106">JRE</span></span>](https://hub.docker.com/_/microsoft-java-jre)
* <span data-ttu-id="31177-107">[Автономная среда JRE](https://hub.docker.com/_/microsoft-java-jre-headless).</span><span class="sxs-lookup"><span data-stu-id="31177-107">[JRE-headless](https://hub.docker.com/_/microsoft-java-jre-headless)</span></span>

## <a name="running-a-docker-image"></a><span data-ttu-id="31177-108">Запуск образа Docker</span><span class="sxs-lookup"><span data-stu-id="31177-108">Running a Docker image</span></span>

<span data-ttu-id="31177-109">Образы Docker можно запускать с помощью синтаксиса `$ docker run mcr.microsoft.com/java/jdk:tag java`, как показано в примере ниже.</span><span class="sxs-lookup"><span data-stu-id="31177-109">Docker images can be run using the syntax `$ docker run mcr.microsoft.com/java/jdk:tag java` as shown in the following example.</span></span>

```cli
docker run mcr.microsoft.com/java/jdk:8u212-zulu-alpine java -version 
```

## <a name="creating-a-docker-image"></a><span data-ttu-id="31177-110">Создание образа Docker</span><span class="sxs-lookup"><span data-stu-id="31177-110">Creating a Docker image</span></span>

<span data-ttu-id="31177-111">Вы можете создать образ на основе официальных образов Майкрософт в Docker Hub, как показано в примерах ниже.</span><span class="sxs-lookup"><span data-stu-id="31177-111">You can create an image using Microsoft's official Docker Hub images as shown in the following examples.</span></span>

### <a name="create-a-docker-file"></a><span data-ttu-id="31177-112">Создание файла Docker</span><span class="sxs-lookup"><span data-stu-id="31177-112">Create a Docker file</span></span>

```cli
FROM mcr.microsoft.com/java/jdk:8u212-zulu-alpine 
  
RUN echo $' \
  
public class HelloWorld { \
   public static void main(String[] args) { \
      // Prints "Hello, World" in the terminal window. \
      System.out.println("Hello, World - From Microsoft Azure !!!"); \
   } \
}' > HelloWorld.java
  
RUN javac HelloWorld.java
  
CMD ["java", "HelloWorld"]
```

### <a name="build-a-docker-image"></a><span data-ttu-id="31177-113">Создание образа Docker</span><span class="sxs-lookup"><span data-stu-id="31177-113">Build a Docker image</span></span>

```cli
docker build -t hello-world
```

### <a name="run-the-new-image"></a><span data-ttu-id="31177-114">Запуск нового образа</span><span class="sxs-lookup"><span data-stu-id="31177-114">Run the new image</span></span>

```cli
docker run hello-world
```

<span data-ttu-id="31177-115">Вы увидите такой результат:</span><span class="sxs-lookup"><span data-stu-id="31177-115">You will see the following output:</span></span>

```output
Hello World - From Microsoft Azure !!!
```
