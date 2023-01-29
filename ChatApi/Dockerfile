FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build

WORKDIR /src
COPY . .
RUN dotnet restore "ChatApi/ChatApi.csproj"

COPY . .
WORKDIR "/src/ChatApi"
RUN dotnet build "ChatApi.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "ChatApi.csproj" -c Release -o /app/publish

FROM mcr.microsoft.com/dotnet/aspnet:6.0
WORKDIR /app
COPY --from=publish /app/publish .

ENV ASPNETCORE_URLS http://*:10560
EXPOSE 10560

ENTRYPOINT ["dotnet", "ChatApi.dll"]