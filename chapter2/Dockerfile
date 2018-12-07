FROM microsoft/dotnet:2.1-runtime AS base
WORKDIR /app

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["WebApplication.csproj", "./"]
RUN dotnet restore "./WebApplication.csproj"
COPY . .
WORKDIR "/src/."
RUN dotnet build "WebApplication.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "WebApplication.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "WebApplication.dll"]
