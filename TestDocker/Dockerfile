FROM mcr.microsoft.com/dotnet/core/aspnet:3.0-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:3.0-buster AS build
WORKDIR /src
COPY ["TestDocker/TestDocker.csproj", "TestDocker/"]
RUN dotnet restore "TestDocker/TestDocker.csproj"
COPY . .
WORKDIR "/src/TestDocker"
RUN dotnet build "TestDocker.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "TestDocker.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "TestDocker.dll"]