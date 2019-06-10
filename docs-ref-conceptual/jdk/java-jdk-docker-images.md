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
# <a name="use-docker-with-a-jdk-for-azure"></a>Использование Docker с JDK для среды Azure 

Готовые образы Docker для Java 7, 8 и 11 доступны через [Docker Hub](https://hub.docker.com/_/microsoft-java-se).

В Docker Hub доступны сертифицированные образы контейнеров Docker для Zulu JDK, JRE и автономной среды JRE на основе нескольких базовых образов ОС.

* [JDK](https://hub.docker.com/_/microsoft-java-jdk).
* [JRE](https://hub.docker.com/_/microsoft-java-jre)
* [Автономная среда JRE](https://hub.docker.com/_/microsoft-java-jre-headless).

## <a name="running-a-docker-image"></a>Запуск образа Docker

Образы Docker можно запускать с помощью синтаксиса `$ docker run mcr.microsoft.com/java/jdk:tag java`, как показано в примере ниже.

```cli
docker run mcr.microsoft.com/java/jdk:8u212-zulu-alpine java -version 
```

## <a name="creating-a-docker-image"></a>Создание образа Docker

Вы можете создать образ на основе официальных образов Майкрософт в Docker Hub, как показано в примерах ниже.

### <a name="create-a-docker-file"></a>Создание файла Docker

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

### <a name="build-a-docker-image"></a>Создание образа Docker

```cli
docker build -t hello-world
```

### <a name="run-the-new-image"></a>Запуск нового образа

```cli
docker run hello-world
```

Вы увидите такой результат:

```output
Hello World - From Microsoft Azure !!!
```
