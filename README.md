# Docker proxy

El siguiente repo utiliza Docker y Nginx para configurar un proxy que distribuye las solicitudes entre dos servidores web. 
Cada servidor web sirve una página estática simple que identifica a cada servidor y Nginx actúa como un proxy reverso.

## Descripción de Archivos

- **server1/Dockerfile**: Dockerfile para construir el primer servidor web.
- **server1/example.html**: Archivo HTML que se sirve desde `server1`.
- **server1/nginx.conf**: Archivo de configuración de Nginx para configurar que se utilice el puerto 8555.
- **server2/Dockerfile**: Dockerfile para construir el segundo servidor web.
- **server2/example2.html**: Archivo HTML que se sirve desde `server2`.
- **server2/nginx.conf**: Archivo de configuración de Nginx para configurar que se utilice el puerto 8555.
- **docker-compose.yml**: Define los servicios (servidores y proxy) y sus configuraciones.
- **nginx.conf**: Archivo de configuración de Nginx para manejar el balanceo de carga.

## Instrucciones de Uso

1. **Clonar el repositorio**:
   ```bash
   git clone https://github.com/jlborrego/docker-proxy.git
   cd docker-proxy

2. **Construir y ejecutar los contenedores**:

   ```bash
    docker-compose up 

3. **Probar petición a proxy**

    Se puede realizar tanto via navegador introduciendo http://localhost:80 , como via comando con curl:

   ```bash
    curl http://localhost:80
    ```
  De esta forma se alterna el mensaje de "Hola, soy el servidor 1" o "Hola, soy el servidor 2".


## Alternativa para no publicar puerto 80 en host

Con el fin de no utilizar nuestro puerto 80 de host con el del proxy, se podría directamente lanzar peticiones a la ip del contenedor. 
Para averiguar la IP:
   ```bash
    docker inspect -f '{{range.NetworkSettings.Networks}}{{.IPAddress}}{{end}}' proxy
   ```

Seguidamente se podría probar también con su IP:
   ```bash
    curl http://<IP>