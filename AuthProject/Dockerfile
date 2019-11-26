FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["AuthProject/AuthProject.csproj", "AuthProject/"]
RUN dotnet restore "AuthProject/AuthProject.csproj"
COPY . .
WORKDIR "/src/AuthProject"
RUN dotnet build "AuthProject.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "AuthProject.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "AuthProject.dll"]