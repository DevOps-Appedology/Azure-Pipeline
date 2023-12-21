FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["WebApplication(DotNet)/WebApplication(DotNet).csproj", "WebApplication(DotNet)/"]
RUN dotnet restore "WebApplication(DotNet)/WebApplication(DotNet).csproj"
COPY . .
WORKDIR "/src/WebApplication1"
RUN dotnet build "WebApplication(DotNet).csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "WebApplication(DotNet).csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "WebApplication1.dll"]
