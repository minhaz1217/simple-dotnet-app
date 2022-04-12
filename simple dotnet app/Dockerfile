#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY . .
RUN dotnet restore "simple dotnet app.csproj"
RUN dotnet build "simple dotnet app.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "simple dotnet app.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "simple dotnet app.dll"]

# Build using 
# docker build -t i_simple_dotnet .

# Run using
# docker run --name simple_dotnet -p3001:80 -p3002:443 -dit i_simple_dotnet