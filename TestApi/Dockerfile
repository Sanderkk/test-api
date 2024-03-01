FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build-env

WORKDIR /app

COPY . .

# Build and publish App
WORKDIR /app/

RUN dotnet publish -c Release -o out

# Build runtime container
FROM mcr.microsoft.com/dotnet/aspnet:8.0

WORKDIR /app

COPY --from=build-env /app/out ./

RUN useradd -ms /bin/bash -u 999 nonrootuser
USER 999

ENV ASPNETCORE_URLS=http://*:8080
EXPOSE 8080

ENTRYPOINT ["dotnet", "TestApi.dll"]