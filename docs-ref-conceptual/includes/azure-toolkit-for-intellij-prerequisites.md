## <a name="prerequisites"></a><span data-ttu-id="b792e-101">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="b792e-101">Prerequisites</span></span>
<span data-ttu-id="b792e-102">Для выполнения описанных в статье шагов необходимо установить набор средств Azure для IntelliJ. Для этого требуются следующие компоненты:</span><span class="sxs-lookup"><span data-stu-id="b792e-102">To complete the steps in his article, you will need to install the Azure Toolkit for IntelliJ, which requires the following software components:</span></span>

* <span data-ttu-id="b792e-103">Выпуск IntelliJ IDEA Ultimate Edition или Community Edition. Его можно скачать с [веб-сайта JetBrains](https://www.jetbrains.com/idea/download/).</span><span class="sxs-lookup"><span data-stu-id="b792e-103">IntelliJ IDEA Ultimate Edition or Community Edition, which can be downloaded from the [JetBrains website](https://www.jetbrains.com/idea/download/).</span></span>
* <span data-ttu-id="b792e-104">Поддерживаемая версия Java Development Kit (JDK).</span><span class="sxs-lookup"><span data-stu-id="b792e-104">A supported Java Development Kit (JDK).</span></span> <span data-ttu-id="b792e-105">Дополнительные сведения о версиях JDK, доступных для разработки в Azure, см. в статье <https://aka.ms/azure-jdks>.</span><span class="sxs-lookup"><span data-stu-id="b792e-105">For more information about the JDKs available for use when developing on Azure, see <https://aka.ms/azure-jdks>.</span></span>
* <span data-ttu-id="b792e-106">Операционная система.</span><span class="sxs-lookup"><span data-stu-id="b792e-106">An operating system.</span></span> <span data-ttu-id="b792e-107">Набор средств Azure для IntelliJ проверен в следующих операционных системах:</span><span class="sxs-lookup"><span data-stu-id="b792e-107">The Azure Toolkit for IntelliJ has been tested on the following operating systems:</span></span>
  
  * <span data-ttu-id="b792e-108">Windows 10, Windows 8.1, Windows 8 и Windows 7;</span><span class="sxs-lookup"><span data-stu-id="b792e-108">Windows 10, Windows 8.1, Windows 8, and Windows 7</span></span>
  * <span data-ttu-id="b792e-109">Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 и Windows Server 2008;</span><span class="sxs-lookup"><span data-stu-id="b792e-109">Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, and Windows Server 2008</span></span>
  * <span data-ttu-id="b792e-110">[Mac OS X](http://www.apple.com/osx) версии Yosemite и выше;</span><span class="sxs-lookup"><span data-stu-id="b792e-110">[Mac OS X](http://www.apple.com/osx) version "Yosemite" and later</span></span>
  * <span data-ttu-id="b792e-111">[Ubuntu Linux](http://www.ubuntu.com) версии 14, 15 и 16.</span><span class="sxs-lookup"><span data-stu-id="b792e-111">[Ubuntu Linux](http://www.ubuntu.com) version 14, 15, and 16</span></span>

> [!NOTE]
> 
> <span data-ttu-id="b792e-112">На сайте репозитория подключаемых модулей JetBrains на странице [Azure Toolkit for IntelliJ](https://plugins.jetbrains.com/plugin/8053) приведен список сборок, совместимых с набором средств.</span><span class="sxs-lookup"><span data-stu-id="b792e-112">The [Azure Toolkit for IntelliJ](https://plugins.jetbrains.com/plugin/8053) page at the JetBrains Plugin Repository lists the builds that are compatible with the toolkit.</span></span>
> 

<!--
> [!IMPORTANT]
> 
> If you are using the Azure Toolkit for IntelliJ on Windows, the toolkit requires installing the Azure SDK 2.9.6 or later in order to use the Azure emulator. You have two options for installing the Azure SDK:
> 
> * You can download and install the Azure SDK by using the [Web Platform Installer (WebPI)](http://go.microsoft.com/fwlink/?LinkID=252838).
> * If you do not have the Azure SDK installed when you create your first Azure deployment project, you will be prompted to automatically download install the requisite version of the Azure SDK.
> 
> Note that the Azure SDK is only required on Windows.
> 
-->
