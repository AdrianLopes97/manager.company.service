#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["manager.company.service.webapi/manager.company.service.webapi.csproj", "manager.company.service.webapi/"]
RUN dotnet restore "manager.company.service.webapi/manager.company.service.webapi.csproj"
COPY . .
WORKDIR "/src/manager.company.service.webapi"
RUN dotnet build "manager.company.service.webapi.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "manager.company.service.webapi.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "manager.company.service.webapi.dll"]