FROM microsoft/aspnetcore:2.0 AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/aspnetcore-build:2.0 AS build
#WORKDIR ../
#RUN dir
COPY ACIDemoApp.sln .
COPY ACIDemoApp/ACIDemoApp.csproj ACIDemoApp
RUN dotnet restore -nowarn:msb3202,nu1503
COPY . .
WORKDIR /ACIDemoApp
RUN dotnet build -c Release -o /app

FROM build AS publish
RUN dotnet publish -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "ACIDemoApp.dll"]
