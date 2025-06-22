FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /app

# Copy csproj and restore dependencies
COPY *.sln .
COPY Bank.WebApi/*.csproj ./Bank.WebApi/
COPY Bank.Domain/*.csproj ./Bank.Domain/
RUN dotnet restore

# Copy everything and build app
COPY Bank.WebApi/. ./Bank.WebApi/
COPY Bank.Domain/. ./Bank.Domain/
WORKDIR /app
RUN dotnet publish -c Release -o out

# Build runtime image
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS runtime
WORKDIR /app
COPY --from=build /app/out ./
ENTRYPOINT ["dotnet", "Bank.WebApi.dll"]