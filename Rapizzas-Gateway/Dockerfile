# ==========================================
# Etapa 1: Construcción (Build)
# ==========================================
FROM eclipse-temurin:26-jdk AS build
WORKDIR /app

# Copiamos el wrapper de Maven y archivos necesarios
COPY mvnw .
COPY .mvn .mvn
COPY pom.xml .

# Damos permisos de ejecución al wrapper
RUN chmod +x ./mvnw

# Copiamos el código fuente
COPY src src

# Construimos el proyecto ignorando tests
RUN ./mvnw clean package -DskipTests

# ==========================================
# Etapa 2: Ejecución (Run)
# ==========================================
FROM eclipse-temurin:26-jdk
WORKDIR /app

# Copiamos únicamente el JAR generado
COPY --from=build /app/target/*.jar app.jar

# Exponemos el puerto de tu Config Server
EXPOSE 2111

# Comando para iniciar la aplicación
ENTRYPOINT ["java", "-jar", "app.jar"]