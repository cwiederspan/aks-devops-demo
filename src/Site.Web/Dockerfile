FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["Site.Web/Site.Web.csproj", "Site.Web/"]
RUN dotnet restore "Site.Web/Site.Web.csproj"
COPY . .
WORKDIR "/src/Site.Web"
RUN dotnet build "Site.Web.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "Site.Web.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Site.Web.dll"]