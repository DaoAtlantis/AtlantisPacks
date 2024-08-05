FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src
COPY ["Atlantis.Poker/Atlantis.Poker.csproj", "Atlantis.Poker/"]
RUN dotnet restore "Atlantis.Poker/Atlantis.Poker.csproj"
COPY . .
WORKDIR "/src/Atlantis.Poker"
RUN dotnet build "Atlantis.Poker.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Atlantis.Poker.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Atlantis.Poker.dll"]
