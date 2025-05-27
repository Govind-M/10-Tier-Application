FROM mcr.microsoft.com/dotnet/sdk:8.0 AS builder

WORKDIR /usr/src/app

COPY cartservice.csproj ./
RUN dotnet restore cartservice.csproj -r linux-musl-x64

COPY . .
RUN dotnet publish cartservice.csproj -r linux-musl-x64 \
    -p:PublishSingleFile=true \
    --self-contained true \
    -p:PublishTrimmed=True \
    -p:TrimMode=Full \
    -c release \
    -o /cartservice \
    --no-restore
   

FROM mcr.microsoft.com/dotnet/runtime-deps:8.0-alpine3.20

WORKDIR /usr/src/app

COPY --from=builder /cartservice ./

EXPOSE 7070
ENV DOTNET_EnableDiagnostics=0 \
    ASPNETCORE_HTTP_PORTS=7070

ENTRYPOINT [ "./cartservice" ]
