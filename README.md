# MyMusic - Identity

This is a basic CRUD (Create, Read, Update, Delete) application that shows how you would implement and use **Identity** in a multi layer application.

**It uses the [MyMusic](https://github.com/alopes2/Medium-MyMusic) project as base.**

# Update from 3.0 to 3.1

To upgrade the [MyMusic](https://github.com/alopes2/Medium-MyMusic) project is simple, we just need to updated the `TargetFramework` to `netcoreapp.3.1` in the `MyMusic.Api.csproj` file, like this:

```
<TargetFramework>netcoreapp3.1</TargetFramework>
```

And update `Entity Framework` version in the Data project in the `MyMusic.Data.csproj`. You can run the following commands to update to version **3.1.2**:

```
dotnet add ./MyMusic.Data/MyMusic.Data.csproj package Microsoft.EntityFrameworkCore -v 3.1.2
dotnet add ./MyMusic.Data/MyMusic.Data.csproj package Microsoft.EntityFrameworkCore.Design -v 3.1.2
dotnet add ./MyMusic.Data/MyMusic.Data.csproj package Microsoft.EntityFrameworkCore.SqlServer -v 3.1.2
```

## Swagger

I also upgraded Swashbuckle's version to their final stable release 5.0.0.

To upgrade you need to update to their latest package with:

```
dotnet add ./MyMusic.Api/MyMusic.Api.csproj package Swashbuckle.AspNetCore -v 5.0.0
```

Also, if you have an API that uses Newtonsoft for serializing JSON, you need to add an extra package and an extra service configuration to your `Startup.cs` because since .NET Core 3.0, Microsoft introduced their own serializer, `System.Text.Json` (STJ), so Swashbuckle will assume you are using it as default. But don't worry, you just need to run the following line of code to add the out-of-the-box package: 

*Note that this is only needed if you need Newtonsoft in your application!*

```
dotnet add ./MyMusic.Api/MyMusic.Api.csproj package Swashbuckle.AspNetCore.Newtonsoft -v 5.0.0
```

And add the following service configuration in the `ConfigureServices` method just after `services.AddSwaggerGen` configuration:

```
services.AddSwaggerGenNewtonsoftSupport();
```

For more information and configuration, you can check the project's github .