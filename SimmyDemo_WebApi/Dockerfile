FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["SimmyDemo_WebApi/SimmyDemo_WebApi.csproj", "SimmyDemo_WebApi/"]
RUN dotnet restore "SimmyDemo_WebApi/SimmyDemo_WebApi.csproj"
COPY . .
WORKDIR "/src/SimmyDemo_WebApi"
RUN dotnet build "SimmyDemo_WebApi.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "SimmyDemo_WebApi.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "SimmyDemo_WebApi.dll"]