#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["DeliveryKing.AuthAPI/DeliveryKing.AuthAPI.csproj", "DeliveryKing.AuthAPI/"]
RUN dotnet restore "DeliveryKing.AuthAPI/DeliveryKing.AuthAPI.csproj"
COPY . .
WORKDIR "/src/DeliveryKing.AuthAPI"
RUN dotnet build "DeliveryKing.AuthAPI.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "DeliveryKing.AuthAPI.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "DeliveryKing.AuthAPI.dll"]