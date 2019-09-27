FROM mcr.microsoft.com/dotnet/core/aspnet:3.0-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:3.0-buster AS build
WORKDIR /src
COPY ["TestCI.Web.csproj", "TestCI.Web/"]
RUN dotnet restore "TestCI.Web/TestCI.Web.csproj"
COPY . .
WORKDIR "/src/TestCI.Web"
RUN dotnet build "TestCI.Web.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "TestCI.Web.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "TestCI.Web.dll"]