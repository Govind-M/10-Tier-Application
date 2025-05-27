FROM eclipse-temurin:21-jdk AS builder

WORKDIR /usr/src/app

COPY gradlew* settings.gradle* build.gradle ./
COPY ./gradle ./gradle

RUN chmod +x ./gradlew
RUN ./gradlew downloadrepos

COPY . .
RUN chmod +x ./gradlew
RUN ./gradlew installDist


FROM eclipse-temurin:21-jre

WORKDIR /usr/src/app


COPY --from=builder /usr/src/app ./

EXPOSE 9555
ENTRYPOINT [ "./build/install/hipstershop/bin/AdService" ]