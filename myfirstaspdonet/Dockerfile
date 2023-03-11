#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.
#TTEst
FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
ENV ASPNETCORE_URLS http://+:8222
EXPOSE 8222

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["myfirstaspdonet/myfirstaspdonet.csproj", "myfirstaspdonet/"]
RUN dotnet restore "myfirstaspdonet/myfirstaspdonet.csproj"
COPY . .
WORKDIR "/src/myfirstaspdonet"
RUN dotnet build "myfirstaspdonet.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "myfirstaspdonet.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "myfirstaspdonet.dll"]
