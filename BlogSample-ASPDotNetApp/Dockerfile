#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["BlogSample-ASPDotNetApp/BlogSample-ASPDotNetApp.csproj", "BlogSample-ASPDotNetApp/"]
RUN dotnet restore "BlogSample-ASPDotNetApp/BlogSample-ASPDotNetApp.csproj"
COPY . .
WORKDIR "/src/BlogSample-ASPDotNetApp"
RUN dotnet build "BlogSample-ASPDotNetApp.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "BlogSample-ASPDotNetApp.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "BlogSample-ASPDotNetApp.dll"]