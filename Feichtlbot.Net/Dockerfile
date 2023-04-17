FROM mcr.microsoft.com/dotnet/runtime:7.0 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["Feichtlbot.Net/Feichtlbot.Net.csproj", "Feichtlbot.Net/"]
RUN dotnet restore "Feichtlbot.Net/Feichtlbot.Net.csproj"
COPY . .
WORKDIR "/src/Feichtlbot.Net"
RUN dotnet build "Feichtlbot.Net.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Feichtlbot.Net.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Feichtlbot.Net.dll"]
