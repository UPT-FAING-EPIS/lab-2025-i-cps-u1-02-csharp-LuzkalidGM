FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /app

# Copy project files and restore dependencies individually
COPY Bank.WebApi/*.csproj ./Bank.WebApi/
COPY Bank.Domain/*.csproj ./Bank.Domain/
RUN dotnet restore ./Bank.WebApi/Bank.WebApi.csproj
RUN dotnet restore ./Bank.Domain/Bank.Domain.csproj

# Copy everything and build app
COPY Bank.WebApi/. ./Bank.WebApi/
COPY Bank.Domain/. ./Bank.Domain/
WORKDIR /app
RUN dotnet publish ./Bank.WebApi/Bank.WebApi.csproj -c Release -o out

# Build runtime image
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS runtime
WORKDIR /app
COPY --from=build /app/out ./
ENTRYPOINT ["dotnet", "Bank.WebApi.dll"]