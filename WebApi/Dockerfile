# Build Stage
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src

# Projektdateien kopieren
COPY . .

# Restore
RUN dotnet restore

# Publish
RUN dotnet publish -c Release -o /app/publish

# Runtime Stage
FROM mcr.microsoft.com/dotnet/aspnet:8.0
WORKDIR /app

# Veröffentlichte Dateien kopieren
COPY --from=build /app/publish .

# Port freigeben
EXPOSE 5001

# Anwendung auf Port 5001 laufen lassen
ENV ASPNETCORE_URLS=http://localhost:5001

# Starten
ENTRYPOINT ["dotnet", "WebApi.dll"]