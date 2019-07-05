FROM mcr.microsoft.com/dotnet/core/aspnet:2.1-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.1-stretch AS build
WORKDIR /src
COPY ["Client.ServiceApi/Client.ServiceApi.csproj", "Client.ServiceApi/"]
RUN dotnet restore "Client.ServiceApi/Client.ServiceApi.csproj"
COPY . .
WORKDIR "/src/Client.ServiceApi"
RUN dotnet build "Client.ServiceApi.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "Client.ServiceApi.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Client.ServiceApi.dll"]