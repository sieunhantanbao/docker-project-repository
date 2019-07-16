FROM mcr.microsoft.com/dotnet/core/sdk:3.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443
# Copy proj and restore
COPY MyApplication.Web/*.csproj ./
RUN dotnet restore
# Copy everything else and build
COPY . ./
RUN dotnet build "MyApplication.Web/MyApplication.Web.csproj" -c Release -o out
RUN dotnet publish "MyApplication.Web/MyApplication.Web.csproj" -c Release -o out
# Build runtime image
FROM mcr.microsoft.com/dotnet/core/aspnet:3.0
WORKDIR /app
COPY --from=base /app/out .
ENTRYPOINT ["dotnet", "MyApplication.Web.dll"]