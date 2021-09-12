FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["Vitorm.Munin.Api/Vitorm.Munin.Api.csproj", "Vitorm.Munin.Api/"]
RUN dotnet restore "Vitorm.Munin.Api/Vitorm.Munin.Api.csproj"
COPY . .
WORKDIR "/src/Vitorm.Munin.Api"
RUN dotnet build "Vitorm.Munin.Api.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Vitorm.Munin.Api.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Vitorm.Munin.Api.dll"]
