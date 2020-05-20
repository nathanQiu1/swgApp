FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-buster-slim AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster AS build
WORKDIR /src
COPY ["SwgWebApp/SwgWebApp.csproj", "SwgWebApp/"]
RUN dotnet restore "SwgWebApp/SwgWebApp.csproj"
COPY . .
WORKDIR "/src/SwgWebApp"
RUN dotnet build "SwgWebApp.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "SwgWebApp.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "SwgWebApp.dll"]