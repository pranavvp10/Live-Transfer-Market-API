#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0-alpine-amd64 AS build
WORKDIR /src
COPY ["LiveTransferMarket.API/LiveTransferMarket.API.csproj", "LiveTransferMarket.API/"]
RUN dotnet restore "LiveTransferMarket.API/LiveTransferMarket.API.csproj"
COPY . .
WORKDIR "/src/LiveTransferMarket.API"
RUN dotnet build "LiveTransferMarket.API.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "LiveTransferMarket.API.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "LiveTransferMarket.API.dll"]
