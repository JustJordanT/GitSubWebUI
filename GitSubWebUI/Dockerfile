﻿FROM mcr.microsoft.com/dotnet/core/aspnet:3.1 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:3.1 AS build
WORKDIR /src
COPY ["GitSubWebUI/GitSubWebUI.csproj", "GitSubWebUI/"]
RUN dotnet restore "GitSubWebUI/GitSubWebUI.csproj"
COPY . .
WORKDIR "/src/GitSubWebUI"
RUN dotnet build "GitSubWebUI.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "GitSubWebUI.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "GitSubWebUI.dll"]
