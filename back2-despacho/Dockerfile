FROM maven:3.9.6-eclipse-temurin-17 AS build

WORKDIR /app

COPY . .

RUN mvn clean package -DskipTests


FROM eclipse-temurin:17-jdk

WORKDIR /app

# Crear usuario no root
RUN addgroup --system spring && adduser --system spring --ingroup spring

COPY --from=build /app/target/*.jar app.jar

# Cambiar permisos
RUN chown spring:spring app.jar

USER spring

EXPOSE 8080

ENTRYPOINT ["java", "-jar", "app.jar"]