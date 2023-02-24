#FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
#FROM mcr.microsoft.com/dotnet/aspnet:5.0-buster-slim AS base
FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
ARG ENV_VAR
ENV ASPNETCORE_ENVIRONMENT=$ENV_VAR
WORKDIR /app
EXPOSE 80
EXPOSE 443


#FROM mcr.microsoft.com/dotnet/sdk:5.0-buster-slim AS build
FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY aspnetapp.sln ./
COPY . .
RUN dotnet restore "aspnetapp.sln"

WORKDIR "/src/."
RUN dotnet build "aspnetapp.sln" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "aspnetapp.sln" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "aspnetapp.dll"]