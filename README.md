# Proyecto MS Restaurante

Este repositorio contiene el host de los microservicios del ejercicio de Alegra.

## Descripción General

El proyecto cuenta con 5 submódulos o microservicios:

- **ms-order-service:** Se encarga de recibir pedidos del gerente y crearlos.
- **ms-kitchen:** Selecciona una receta para preparar.
- **ms-warehouse:** Administra el inventario de ingredientes.
- **ms-market:** Simula una API externa para la compra de ingredientes.

La comunicación entre estos servicios se realiza a través de RabbitMQ.

## Arquitectura

La solución se basa en una arquitectura de microservicios donde:

- **Comunicación asíncrona:** Se utiliza RabbitMQ para el envío y recepción de mensajes entre los servicios.
- **Persistencia NoSQL:** MongoDB se utiliza para almacenar pedidos, recetas, inventario y el historial de compras.
- **Contenerización:** Cada servicio se ejecuta en su propio contenedor Docker y se orquesta mediante Docker Compose.

Diagrama simplificado de la arquitectura:

![image](docs/image.png)

Capturas del resultado

![image](docs/code.png)


## Instrucciones de Uso

Clonar los repositorios 

``git clone --recurse-submodules https://github.com/tu-usuario/orchestrator.git``


# Correr contenedores

``docker-compose up --build``

## Despliegue en AWS

El proyecto ha sido desplegado en Amazon Web Services utilizando la siguiente configuración:

- **Elastic Load Balancer (ELB):** Distribuye el tráfico entre las instancias EC2, proporcionando alta disponibilidad y balanceo de carga para la aplicación.

- **Amazon Route 53:** Gestiona el DNS para enrutar el tráfico al balanceador de carga, permitiendo el acceso a través de un nombre de dominio fácil de recordar.

- **Dominio:** La aplicación Backend está disponible en [sandboxtesting.info](https://sandboxtesting.info)

- **Dominio:** La aplicación Frontend está disponible en https://magenta-bonbon-40d248.netlify.app/

- **Instancias EC2:** Ejecutan los contenedores Docker con los microservicios en un entorno de Amazon Linux 2.

- **VPC y Grupos de Seguridad:** Configurados para garantizar la seguridad y el acceso adecuado a los servicios.

### Comandos útiles para gestionar el despliegue

Para detener y limpiar completamente todos los recursos de Docker:

```bash
docker-compose down -v && docker volume rm $(docker volume ls -q) 2>/dev/null || true && docker system prune -a --force
```

Para reconstruir e iniciar los servicios:

```bash
docker-compose up --build -d
```
