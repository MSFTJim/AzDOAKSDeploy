FROM mcr.microsoft.com/dotnet/core/aspnet:3.1 AS base
WORKDIR /app
EXPOSE 80
#EXPOSE 5001

FROM mcr.microsoft.com/dotnet/core/sdk:3.1 AS build
WORKDIR /src
COPY *.csproj ./
#COPY ["aksapp/aksapp.csproj", "aksapp/"]
RUN dotnet restore  
#RUN dotnet restore "aksapp/aksapp.csproj"
COPY . .
#WORKDIR "/src/aksapp"
RUN dotnet build  -c Release -o /app/build
#RUN dotnet build "aksapp.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish -c Release -o /app/publish
#RUN dotnet publish "aksapp.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "aksapp.dll"]
