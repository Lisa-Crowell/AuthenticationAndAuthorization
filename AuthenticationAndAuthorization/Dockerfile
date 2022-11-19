FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["AuthenticationAndAuthorization/AuthenticationAndAuthorization.csproj", "AuthenticationAndAuthorization/"]
RUN dotnet restore "AuthenticationAndAuthorization/AuthenticationAndAuthorization.csproj"
COPY . .
WORKDIR "/src/AuthenticationAndAuthorization"
RUN dotnet build "AuthenticationAndAuthorization.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "AuthenticationAndAuthorization.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "AuthenticationAndAuthorization.dll"]
