FROM microsoft/aspnetcore:2.0 AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/aspnetcore-build:2.0 AS build
WORKDIR /src
COPY IdentityServer/IdentityServer.csproj IdentityServer/
RUN dotnet restore IdentityServer/IdentityServer.csproj
COPY . .
WORKDIR /src/IdentityServer
RUN dotnet build IdentityServer.csproj -c Docker -o /app

FROM build AS publish
RUN dotnet publish IdentityServer.csproj -c Docker -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "IdentityServer.dll"]
