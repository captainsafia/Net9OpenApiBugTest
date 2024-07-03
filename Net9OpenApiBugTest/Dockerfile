FROM mcr.microsoft.com/dotnet/nightly/aspnet:9.0-preview AS base
USER $APP_UID
WORKDIR /app
EXPOSE 8080
EXPOSE 8081

FROM mcr.microsoft.com/dotnet/nightly/sdk:9.0-preview AS build
ARG BUILD_CONFIGURATION=Release
WORKDIR /src
COPY ["Net9OpenApiBugTest/Net9OpenApiBugTest.csproj", "Net9OpenApiBugTest/"]
RUN dotnet restore -s https://pkgs.dev.azure.com/dnceng/public/_packaging/dotnet9/nuget/v3/index.json -s https://api.nuget.org/v3/index.json "Net9OpenApiBugTest/Net9OpenApiBugTest.csproj" 
COPY . .
WORKDIR "/src/Net9OpenApiBugTest"
RUN dotnet build "Net9OpenApiBugTest.csproj" -c $BUILD_CONFIGURATION -o /app/build

FROM build AS publish
ARG BUILD_CONFIGURATION=Release
RUN dotnet publish "Net9OpenApiBugTest.csproj" -c $BUILD_CONFIGURATION -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Net9OpenApiBugTest.dll"]
