<span data-ttu-id="0e63f-101">Создайте [файл аутентификации](../java-sdk-azure-authenticate.md#mgmt-file), экспортируйте переменную среды `AZURE_AUTH_LOCATION` в командной строке и укажите полный путь к файлу.</span><span class="sxs-lookup"><span data-stu-id="0e63f-101">Create an [authentication file](../java-sdk-azure-authenticate.md#mgmt-file) and export an environment variable `AZURE_AUTH_LOCATION` on the command line with the full path to the file.</span></span>

```bash
export AZURE_AUTH_LOCATION=/Users/raisa/azure.auth
```

<span data-ttu-id="0e63f-102">Файл аутентификации позволяет настроить объект `Azure` точки входа, используемый библиотеками управления для определения, создания и настройки ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="0e63f-102">The authentication file is used to configure the entry point `Azure` object used by the management libraries to define, create, and configure Azure resources.</span></span>

```java
// pull in the location of the security file from the environment 
final File credFile = new File(System.getenv("AZURE_AUTH_LOCATION"));

Azure azure = Azure
        .configure()
        .withLogLevel(LogLevel.NONE)
        .authenticate(credFile)
        .withDefaultSubscription();
```

<span data-ttu-id="0e63f-103">См. [дополнительные сведения](../java-sdk-azure-authenticate.md#mgmt-auth) о способах аутентификации при использовании библиотек управления Azure для Java.</span><span class="sxs-lookup"><span data-stu-id="0e63f-103">[Learn more](../java-sdk-azure-authenticate.md#mgmt-auth) about authentication options when using the Azure management libraries for Java.</span></span>