#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["CustomersApp.UI/CustomersApp.UI.csproj", "CustomersApp.UI/"]
RUN dotnet restore "CustomersApp.UI/CustomersApp.UI.csproj"
COPY . .
WORKDIR "/src/CustomersApp.UI"
RUN dotnet build "CustomersApp.UI.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "CustomersApp.UI.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "CustomersApp.UI.dll"]