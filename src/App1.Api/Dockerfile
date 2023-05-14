FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["src/App1.Api/App1.Api.csproj", "src/App1.Api/"]
RUN dotnet restore "src/App1.Api/App1.Api.csproj"
COPY . .
WORKDIR "/src/src/App1.Api"
RUN dotnet build "App1.Api.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "App1.Api.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "App1.Api.dll"]
