FROM mcr.microsoft.com/dotnet/aspnet:8.0-preview AS base
USER app
WORKDIR /app
EXPOSE 8080
EXPOSE 8081

FROM mcr.microsoft.com/dotnet/sdk:8.0-preview AS build
WORKDIR /src
COPY ["Sample.Dotnet8.csproj", "."]
RUN dotnet restore "./Sample.Dotnet8.csproj"
COPY . .
WORKDIR "/src/."
RUN dotnet build "Sample.Dotnet8.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Sample.Dotnet8.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Sample.Dotnet8.dll"]