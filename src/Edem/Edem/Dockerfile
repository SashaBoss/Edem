#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster AS build
WORKDIR /src
COPY ["Edem/Edem.csproj", "Edem/"]
RUN dotnet restore "Edem/Edem.csproj"
COPY . .
WORKDIR "/src/Edem"
RUN dotnet build "Edem.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Edem.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Edem.dll"]