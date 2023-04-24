# Kubernetes
#### Gómez Aldrete Luis Ignacio
#### 216588253
#
### ¿Qué es Kubernetes?

Kubernetes (también conocido como "K8s") es una plataforma de código abierto para la orquestación y gestión de contenedores, diseñada para automatizar la implementación, el escalado y la gestión de aplicaciones en contenedores.

Kubernetes permite a los usuarios gestionar múltiples contenedores que contienen aplicaciones y servicios, en una infraestructura distribuida y escalable, facilitando la automatización de tareas como el despliegue, la escalabilidad, la recuperación ante fallos y la gestión de recursos.

Kubernetes proporciona un conjunto de abstracciones que permiten a los desarrolladores y administradores de sistemas definir cómo se deben implementar y ejecutar las aplicaciones, sin preocuparse por los detalles de la infraestructura subyacente. Al utilizar Kubernetes, los equipos pueden implementar y administrar aplicaciones de forma más eficiente y con mayor fiabilidad, lo que puede reducir los costos operativos y mejorar la experiencia de los usuarios finales.

### ¿Qué es Ingress?

En Kubernetes, un Ingress es un objeto que proporciona una capa de abstracción para exponer servicios HTTP y HTTPS dentro del clúster a través de una ruta de URL externa. Básicamente, el Ingress actúa como un enrutador de tráfico HTTP/HTTPS hacia los servicios que se encuentran dentro del clúster.

El Ingress se define como un recurso Kubernetes y se utiliza para definir las reglas de enrutamiento del tráfico externo al interior del clúster, especificando la ruta de URL y el servicio al que se dirige el tráfico. Permite que los servicios dentro del clúster sean accesibles desde fuera de él, proporcionando una forma de exponer servicios en una única dirección IP pública y en un puerto específico.

El Ingress también es capaz de realizar balanceo de carga, lo que significa que puede distribuir el tráfico de manera equitativa entre los diferentes pods de un servicio. Además, también puede realizar la terminación SSL, lo que permite la gestión del cifrado y la autenticación de los certificados SSL.

### ¿Qué es un LoadBalancer?

Un Load Balancer o balanceador de carga es un dispositivo o software que distribuye el tráfico de red de entrada entre múltiples servidores o nodos para mejorar la disponibilidad, escalabilidad y fiabilidad de las aplicaciones y servicios en línea.

En el contexto de Kubernetes, un Load Balancer es un recurso que se puede utilizar para exponer un servicio a través de una dirección IP externa y un puerto fijo. El balanceador de carga es capaz de distribuir el tráfico entrante de manera uniforme entre los pods que implementan el servicio, mejorando la disponibilidad y el rendimiento del servicio.

Kubernetes proporciona diferentes opciones para implementar un balanceador de carga, como un balanceador de carga de nube proporcionado por el proveedor de la nube, un balanceador de carga de tipo NodePort que utiliza puertos de nodo y una dirección IP de nodo para exponer un servicio a través de un puerto fijo, o un balanceador de carga de tipo LoadBalancer que utiliza un balanceador de carga externo.

# Ejemplo de Kubernetes

Para realizar una práctica con Kubernetes, tuve que instalar los componentes necesarios para usar la herramienta. A pesar de que Kubernetes se basa en la nube, existe una manera de realizar clusters locales con [*minikube*](https://minikube.sigs.k8s.io/docs/start/). Además, se necesita de la herramienta de [*kubectl*](https://kubernetes.io/docs/tasks/tools/install-kubectl-windows/) para usar los comandos de Kubernetes con *minikube*.

![image](https://user-images.githubusercontent.com/80866790/233870031-6d43ea8d-bd3d-42cc-9c4c-795ec1d63c1a.png)

Una vez descargados e instalados ambos componentes, tienen que ser agregados al *Path* de Windows para ser utilizados.

![image](https://user-images.githubusercontent.com/80866790/233870421-c366eeef-9e3d-4105-a670-6ff5019ef291.png)

Para empezar a usar Kubernetes con *minikube* se ejecuta el comando

```cmd 
minikube start
```

Entonces *minikube* empezará su proceso de configuración, creando el contenedor en *Docker* para alojar Kubernetes.

![image](https://user-images.githubusercontent.com/80866790/233876412-54ac0a33-140e-45dd-9301-65067467e2d0.png)

También es posible obtener una interfaz gráfica de Kubernetes usando el comando 

```cmd
minikube dashboard
```

![image](https://user-images.githubusercontent.com/80866790/233876880-6bc67d51-6ae8-489e-a500-ab1bd00c7666.png)

Una vez empezado el servicio de *minkube* se necesita un proyecto contenido en *Docker* para usar Kubernetes. 

Se realiza un pequeñisímo proyecto de 'Hola Mundo!' para probar la tecnología de Node.js

``` js
const express = require('express')
const os = require('os')

const app = express()
app.get('/', (req, res) => {
    res.send(`Hello from ${os.hostname()}!`)
})

const port = 3000
app.listen(port, () => console.log(`listening on port ${port}`))
```

**Nota: La configuracion de WSL (Windows Subsystem for Linux), NVM, NPM y Docker ya estaba lista.**

Ya con el proyecto, simplemente se tiene que crear el pod de Kubernetes con el comando: 

``` cmd
kubectl create deployment --image nachogmz/node-hello-app node-app
```

Además se pueden configurar las replicas del pod para tener como respaldo.

![image](https://user-images.githubusercontent.com/80866790/233889112-3b8e4cc5-dcd0-41bf-be36-a2157327c968.png)

![image](https://user-images.githubusercontent.com/80866790/233889149-30e049c0-82c7-460f-ba86-d59ded9634bc.png)

Aquí se puede visualizar que el despliegue de *node-app* cuenta con 3 replicas del pod.
