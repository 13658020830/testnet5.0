#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["TestNet5.0/TestNet5.0.csproj", "TestNet5.0/"]
RUN dotnet restore "TestNet5.0/TestNet5.0.csproj"
COPY . .
WORKDIR "/src/TestNet5.0"
RUN dotnet build "TestNet5.0.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "TestNet5.0.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "TestNet5.0.dll"]