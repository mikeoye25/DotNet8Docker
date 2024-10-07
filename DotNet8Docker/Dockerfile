#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /DotNet8Docker
COPY ["DotNet8Docker/DotNet8Docker.csproj", "DotNet8Docker/"]
RUN dotnet restore "DotNet8Docker/DotNet8Docker.csproj"
COPY . .
WORKDIR "/DotNet8Docker/DotNet8Docker"
RUN dotnet build "DotNet8Docker.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "DotNet8Docker.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "DotNet8Docker.dll"]