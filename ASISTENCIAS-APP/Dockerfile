# Runtime-only: usa los binarios ya publicados en ./app (no compila fuente)
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS runtime
WORKDIR /app
COPY app/ ./

ENV ASPNETCORE_ENVIRONMENT=Development
ENV ASPNETCORE_URLS=http://*:5003
EXPOSE 5003

ENTRYPOINT ["dotnet", "ControlAsistencias_API.dll"]
