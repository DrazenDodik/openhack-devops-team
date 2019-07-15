FROM microsoft/dotnet:2.1-sdk AS build-env
WORKDIR /app

# copy csproj and restore as distinct layers
COPY *.csproj ./
RUN dotnet restore

# copy everything else and build
COPY . ./
RUN dotnet publish -c Release -o out
COPY ./appsettings.*.json /app/out/
COPY ./appsettings.json /app/out/

# build runtime image
FROM microsoft/dotnet:2.1-aspnetcore-runtime
WORKDIR /app

ENV SQL_USER="openhack1c40sa" \
SQL_PASSWORD="uW6hh7Tq2pwd" \
SQL_SERVER="openhack1c40sql" \
SQL_DBNAME="mydrivingDB" \
WEB_PORT="80" \
WEB_SERVER_BASE_URI="http://0.0.0.0" \
DOCS_URI="http://localhost" \
DEBUG_LOGGING="false"

COPY --from=build-env /app/out .

ENTRYPOINT ["dotnet", "poi.dll"]

