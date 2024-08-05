FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src
COPY ["Atlantis.Soccer/Atlantis.Soccer.csproj", "Atlantis.Soccer/"]
RUN dotnet restore "Atlantis.Soccer/Atlantis.Soccer.csproj"
COPY . .
WORKDIR "/src/Atlantis.Soccer"
RUN dotnet build "Atlantis.Soccer.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Atlantis.Soccer.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Atlantis.Soccer.dll"]
