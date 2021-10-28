FROM mcr.microsoft.com/dotnet/core/aspnet:3.1 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/core/sdk:3.1 AS build
WORKDIR /src
COPY ["myappnet/myappnet.csproj", "myappnet/"]

RUN dotnet restore "myappnet/myappnet.csproj"
COPY . .
WORKDIR "/src/myappnet"
RUN dotnet build "myappnet.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "myappnet.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "myappnet.dll"]