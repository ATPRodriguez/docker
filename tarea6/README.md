<div align="center">

# **Tarea 6 | Docker**
## **Conectar una Base de Datos NoSQL con un Cliente de Base de Datos.**
  <img src="../img/docker-logo.png" alt="logo-docker.png"/>

</div>

<div align="justify">

## Indice
- [Paso 1](#1)

___

### Volúmenes en Docker 
En Docker, un volumen es un mecanismo para almacenar y compartir datos entre contenedores o entre el host y los contenedores. Los volúmenes son administrados por Docker y permiten persistir datos incluso si el contenedor es eliminado. Esto es útil para mantener datos importantes, como bases de datos, configuraciones o cualquier otro archivo que necesite persistencia.

### Redes disponibles
Lista el conjunto de redes disponibles en este momento.

```bash
docker network ls
```

**Salida:**   
<img src="../img/tarea6/Redes.png" alt="Redes.png"/>

### Paso 1 - Crear una red personalizada <a name="1"></a>
Ejecuta el siguiente comando para crear una red llamada ```mongodb-network```:

```bash
docker network create mongodb-network
```

Ejecuta ```docker network ls```, y muestra las redes disponibles en docker.

**Salida:**   
<img src="../img/tarea6/Paso1.png" alt="Paso1.png"/>

### Paso 2 - Crear un Volumen para MongoDB <a name="2"></a>
Ejecuta el siguiente comando para crear un volumen llamado mongodb-data:

```bash
docker volume create mongodb-data
```

Ejecuta ```docker volume ls```, y muestra el resultado:


**Salida:**   
<img src="../img/tarea6/Paso2.png" alt="Paso2.png"/>

### Paso 3 - Levantar el Contenedor MongoDB <a name="3"></a>
Usa el siguiente comando para ejecutar MongoDB con el volumen y la red configurados:

```bash
docker run -d --name mongodb-container \
  --network mongodb-network \
  -e MONGO_INITDB_ROOT_USERNAME=admin \
  -e MONGO_INITDB_ROOT_PASSWORD=admin123 \
  -v mongodb-data:/data/db \
  -p 27017:27017 \
  mongo:latest
```

**Salida:**   
<img src="../img/tarea6/Paso3.png" alt="Paso3.png"/>

### Paso 4 - Levantar el Contenedor Mongo Express <a name="4"></a>
Mongo Express es un cliente web para gestionar MongoDB. Usa este comando para levantar el contenedor:

```bash
docker run -d --name mongo-express-container \
  --network mongodb-network \
  -e ME_CONFIG_MONGODB_ADMINUSERNAME=admin \
  -e ME_CONFIG_MONGODB_ADMINPASSWORD=admin123 \
  -e ME_CONFIG_MONGODB_SERVER=mongodb-container \
  -p 8081:8081 \
  mongo-express:latest
```

**Salida:**   
<img src="../img/tarea6/Paso4.png" alt="Paso4.png"/>

### Paso 5 - Verificar los Contenedores Activos <a name="5"></a>
Lista los contenedores activos para asegurarte de que están funcionando correctamente:

```bash
docker ps
```

**Salida:**   
<img src="../img/tarea6/Paso5.png" alt="Paso5.png"/>

### Paso 6 - Verifica los logs de Mongo Express <a name="6"></a>
Verifica los logs de Mongo Express:

```bash
docker logs mongo-express-container
```

Acceder al Cliente Mongo Express Abre tu navegador y visita ```localhost:8081```

**Salida:**   
<img src="../img/tarea6/Paso6-1.png" alt="Paso6-1.png"/>   

<img src="../img/tarea6/Paso6-2.png" alt="Paso6-2.png"/>

### Paso 7 - Prueba la persistencia de BBDD <a name="7"></a>
Accede a MongoDB desde el Cliente Crea una nueva base de datos llamada testdb.




</div>