# Kafka

# Kafka & Zookeeper con Docker Compose

Este proyecto levanta un entorno local de **Apache Kafka** utilizando **Zookeeper**, ideal para entornos de desarrollo y pruebas rápidas.

---

## Requisitos

Asegúrate de tener instaladas las siguientes herramientas:

- [Docker](https://www.docker.com/)
- [Docker Compose](https://docs.docker.com/compose/)

Verifica la instalación ejecutando:

```bash
docker --version
docker compose version
```

---

## Contenido del `docker-compose.yml`

El archivo define dos servicios principales:

### Zookeeper
Encargado de coordinar los brokers de Kafka.  
Por defecto, se expone en el puerto **2181**.

### Kafka Broker
Servicio de Apache Kafka configurado para escuchar en **localhost:9092**.

---

## Levantar el entorno

Ubícate en la carpeta donde tengas el archivo `docker-compose.yml` y ejecuta:

```bash
docker compose up -d
```

Esto levantará los siguientes servicios:

| Servicio  | Puerto | Descripción |
|------------|---------|-------------|
| Zookeeper  | 2181    | Coordinador de brokers |
| Kafka      | 9092    | Broker principal |

---

## Detener el entorno

Para detener y eliminar los contenedores, ejecuta:

```bash
docker compose down
```

---

##  Verificar que Kafka está funcionando

### Entrar al contenedor de Kafka
```bash
docker exec -it kafka bash
```

### Crear un tópico de prueba
```bash
kafka-topics --create --topic test-topic --bootstrap-server localhost:9092 --partitions 1 --replication-factor 1
```

### Listar los tópicos existentes
```bash
kafka-topics --list --bootstrap-server localhost:9092
```

### Enviar mensajes al tópico
```bash
kafka-console-producer --topic test-topic --bootstrap-server localhost:9092
```
> Escribe mensajes y presiona **Enter** para enviarlos.

### Leer mensajes desde el tópico

En otra terminal:
```bash
docker exec -it kafka bash
kafka-console-consumer --topic test-topic --bootstrap-server localhost:9092 --from-beginning
```

---

##  Limpieza opcional

Para eliminar los volúmenes y datos almacenados:
```bash
docker compose down -v
```

---
