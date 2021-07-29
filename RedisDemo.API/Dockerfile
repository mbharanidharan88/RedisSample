#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["RedisDemo.API/RedisDemo.API.csproj", "RedisDemo.API/"]
RUN dotnet restore "RedisDemo.API/RedisDemo.API.csproj"
COPY . .
WORKDIR "/src/RedisDemo.API"
RUN dotnet build "RedisDemo.API.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "RedisDemo.API.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "RedisDemo.API.dll"]
