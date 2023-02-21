FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["Witness.Host/Witness.Host.csproj", "Witness.Host/"]
RUN dotnet restore "Witness.Host/Witness.Host.csproj"
COPY . .
WORKDIR "/src/Witness.Host"
RUN dotnet build "Witness.Host.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Witness.Host.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Witness.Host.dll"]
