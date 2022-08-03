#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:3.1 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:3.1 AS build
WORKDIR /src
COPY ["webapi1/webapi1.csproj", "webapi1/"]
RUN dotnet restore "webapi1/webapi1.csproj"
COPY . .
WORKDIR "/src/webapi1"
RUN dotnet build "webapi1.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "webapi1.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "webapi1.dll"]