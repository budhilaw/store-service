FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["Store-Service/Store-Service.csproj", "Store-Service/"]
RUN dotnet restore "Store-Service/Store-Service.csproj"
COPY . .
WORKDIR "/src/Store-Service"
RUN dotnet build "Store-Service.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Store-Service.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Store-Service.dll"]
