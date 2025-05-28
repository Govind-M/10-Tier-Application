FROM mcr.microsoft.com/dotnet/sdk:9.0.101-noble AS builder

WORKDIR /usr/src/app

COPY cartservice.csproj ./
RUN dotnet restore cartservice.csproj -r linux-musl-x64

COPY . .
RUN dotnet publish cartservice.csproj -r linux-musl-x64 \
    -p:PublishSingleFile=true \
    --self-contained true \
    -p:PublishTrimmed=True \
    -c release \
    -o /cartservice && \
    chmod +x /cartservice/cartservice


FROM mcr.microsoft.com/dotnet/runtime-deps:9.0.1-noble-chiseled

WORKDIR /usr/src/app

COPY --from=builder /cartservice .

EXPOSE 7070
ENV DOTNET_EnableDiagnostics=0 \
    ASPNETCORE_HTTP_PORTS=7070

ENTRYPOINT [ "/usr/src/app/cartservice" ]
