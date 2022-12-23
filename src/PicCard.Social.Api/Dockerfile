FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["src/PicCard.Social.Api/PicCard.Social.Api.csproj", "src/PicCard.Social.Api/"]
RUN dotnet restore "src/PicCard.Social.Api/PicCard.Social.Api.csproj"
COPY . .
WORKDIR "/src/src/PicCard.Social.Api"
RUN dotnet build "PicCard.Social.Api.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "PicCard.Social.Api.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "PicCard.Social.Api.dll"]