#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["Web/WebStore.Web/WebStore.Web.csproj", "Web/WebStore.Web/"]
RUN dotnet restore "Web/WebStore.Web/WebStore.Web.csproj"
COPY . .
WORKDIR "/src/Web/WebStore.Web"
RUN dotnet build "WebStore.Web.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "WebStore.Web.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "WebStore.Web.dll"]