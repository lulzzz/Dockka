FROM microsoft/aspnetcore:2.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 9000

FROM microsoft/aspnetcore-build:2.0 AS build
WORKDIR /src
COPY *.sln ./
COPY src/Dockka.Api/Dockka.Api.csproj src/Dockka.Api/
COPY src/Dockka.Logging/Dockka.Logging.csproj src/Dockka.Logging/
COPY src/Dockka.Data/Dockka.Data.csproj src/Dockka.Data/
RUN dotnet restore
COPY . .
WORKDIR /src/src/Dockka.Api
RUN dotnet build -c Release -o /app

FROM build AS publish
RUN dotnet publish -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Dockka.Api.dll"]
