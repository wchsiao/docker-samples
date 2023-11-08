FROM mcr.microsoft.com/dotnet/framework/sdk:4.8.1 AS build
WORKDIR /app

# copy csproj and restore as distinct layers
COPY *.sln .
COPY Sample_ASPNET_MVC/*.csproj ./Sample_ASPNET_MVC/
COPY Sample_ASPNET_MVC/*.config ./Sample_ASPNET_MVC/
RUN nuget restore

# copy everything else and build app
COPY Sample_ASPNET_MVC/. ./Sample_ASPNET_MVC/
WORKDIR /app/Sample_ASPNET_MVC
RUN msbuild /p:Configuration=Release -r:False


FROM mcr.microsoft.com/dotnet/framework/aspnet:4.8.1 AS runtime
WORKDIR /inetpub/wwwroot
COPY --from=build /app/Sample_ASPNET_MVC/. ./