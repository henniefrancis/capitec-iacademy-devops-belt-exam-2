FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 81

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY [".\Basic3TierAPI\Basic3TierAPI.csproj", "Basic3TierAPI/"]
RUN dotnet restore ".\Basic3TierAPI\Basic3TierAPI.csproj"
COPY . .
WORKDIR "/src/Basic3TierAPI"
RUN dotnet build ".\Basic3TierAPI\Basic3TierAPI.csproj" -c Release -o /app/build

FROM build as publish
RUN dotnet publish ".\Basic3TierAPI\Basic3TierAPI.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base as final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT [ "dotnet", "Basic3TierAPI.dll" ]