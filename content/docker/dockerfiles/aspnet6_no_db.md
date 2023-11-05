# Exemplo de *dockerfile* para uma aplicação ASP.NET Core 6, sem acesso a banco de dados

```docker
# <https://hub.docker.com/_/microsoft-dotnet>
FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /source

# copy csproj and restore as distinct layers
COPY *.sln .
COPY MelStore/*.csproj ./MelStore/
COPY MelStore.Core/*.csproj ./MelStore.Core/
COPY MelStore.Tests/*.csproj ./MelStore.Tests/
RUN dotnet restore

# copy everything else and build app
COPY MelStore/. ./MelStore/
COPY MelStore.Core/. ./MelStore.Core/
COPY MelStore.Tests/. ./MelStore.Tests/
WORKDIR /source/MelStore
RUN dotnet publish -c release -o /app

# final stage/image
FROM mcr.microsoft.com/dotnet/aspnet:6.0
WORKDIR /app
COPY --from=build /app ./
ENTRYPOINT ["dotnet", "MelStore.dll"]
```
