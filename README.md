# Proyecto de la asignatura de Aplicaciones distribuidas
## Descripción del proyecto
El proyecto consiste en diseñar, implementar y cotizar una solución de balanceo de carga y
failover
El proyecto consiste en simular alguna aplicación web brindada, por ejemplo, una aplicación que
hayan realizado en alguna materia previa, un WordPress, un servicio ftp, correo, etc. Esta
aplicación debe estar replicada en varios nodos del clúster brindando un acceso optimo a cada
usuario que se conecte, esto lo puede utilizar con jmeter simulando n conexiones activas,
simultaneas y soportadas.
Posteriormente se simulará una falla en alguno de los servidores/nodos para lo cual el orquestador
debe levantar un nuevo servidor, manual o automáticamente.


## Arquitectura 
Para el desarrollo de la arquitectura vamos a utilizar [Draw.io](https://app.diagrams.net/) te ayuda a crear un diagrama de
flujo o cualquier diagrama con muchas formas para visualizar correctamente la infraestructura.

<img src="https://i.ibb.co/kxCP68F/Arquitectura-drawio-3.png" alt="drawing" width="800"/>

## Herramientas utilizadas
-  [Draw.io](https://app.diagrams.net/) : Para el diseño de la arquitectura.
-  [Minikube](https://minikube.sigs.k8s.io/docs/start/) : Crear un cluster local.
-  [Docker](https://www.docker.com/) : Para la implementacion de [Minikube](https://minikube.sigs.k8s.io/docs/start/) .
-  [Google Cloud](https://console.cloud.google.com/gcr/images/google-samples/GLOBAL/hello-app) : Para obtener una imagen de prueba.
-  [Jmeter](https://jmeter.apache.org//) : Utilizado como una herramienta de prueba de carga para analizar y medir el rendimiento.

## Codigo de implementacion

1. Iniciamos minikube para nuestro cluster(   Tendremos un nodo master y tres nodos de worker
)
```bash
minikube start --nodes 4 # Iniciar un nuevo clúster con un número dado de nodos
```
2. Revisamos los nodos con el comando y rol que tiene donde tendremos un nodo control-plane
```bash
kubectl get nodes
```
3. Revisamos el estado de cada uno 
```bash
minikube status 
```
4. Vamos aplicar nuestro archivo deployed (*Un controlador de Deployment proporciona actualizaciones declarativas para los Pods y los ReplicaSets*). Recuerda crear un archivo copiar el codigo y terminar con yaml. Ejemplo: deployment-svc-loadBalancer.yaml
```bash
apiVersion: apps/v1
kind: Deployment
metadata:
  name: appsdistribuidas #nombre de nuestro deployment
spec:
  replicas: 3 # numero de pods replicas que deseamos que se creen 
  selector:
    matchLabels:
      role: hello
  template:
    metadata:
      labels:
        role: hello # etiqueta que identificara y comunicara a los pods con el label de servicio
    spec:
      containers:
      - name: hello # nombre que asiganmos al contenedor
        image: gcr.io/google-samples/hello-app:1.0 # asignamos imagen
        ports:
        - containerPort: 8080 #asignamos un puerto

---
# creacion de un servicio para interactuar con los pods 
apiVersion: v1
kind: Service
metadata:
  name: appsdistribuidas #nombre del servicio
spec:
  type: LoadBalancer #tipo de servicio 
  ports:
  - port: 8080 # asignamos el puerto 8080 del contenedor 
    targetPort: 8080
  selector:
    role: hello # nombre que interactua con el pod debe ser igual label y redirigira el trafico a todos los pods con esa etiqueta

```
5. Al archivo deployment vamos a aplicarlo 
```bash
kubectl apply -f deployment-svc-loadBalancer.yaml
```
6. Para ver los servicios y los pods generados aplicamos el comando.
```bash
kubectl get all
```
7. Para poder ver las *IPS* de los pods asociados al servicio 
```bash
kubectl describe svc appsdistribuidas
```
8. Para ver las *IPS* de cada pod usamos el comando 
```bash
kubectl get pods -o wide
```
9. En una ventana extra vamos a aplicar el comando que nos recomeinda minikube para load balancer, esto nos asignara un ip publica
```bash
minikube tunnel
```
10. Para ver la *IP* publica usamos el comando 
```bash
kubectl get svc
```
12. Para probar el balanceador de carga usaremos la ip publica con el puerto asignado, donde el Hostname cambiara de acuerdo al pod que ingrese 
```bash
curl 127.0.0.1:8080
```

## Pruebas con Jmeter
Con la ayuda de la herramienta Jmeter vamos a poner a prueba nuestro balanceador de carga.
- Creacion de un `Thread Group`
<img src="https://i.ibb.co/x7pMPgQ/jmeter1.png" alt="drawing" width="700"/>

- Implementacion de las propiedas para evaluar como usuarios, el tiempo de demora y el bucle
<img src="https://i.ibb.co/cvK03vw/jmeter2.png" alt="drawing" width="700"/>

- Llamada request `HTTP Request`
<img src="https://i.ibb.co/x2tCT52/jmeter3.png" alt="drawing" width="700"/>

- Asignacion de IP y puerto
<img src="https://i.ibb.co/GW9QKXW/jmeter4.png" alt="drawing" width="700"/>

- Agregar oyentes o `listener`
<img src="https://i.ibb.co/hs6pcCG/jmeter5.png" alt="drawing" width="700"/>

- Verificacion de errores
<img src="https://i.ibb.co/j3Y8RFM/jmeter6.png" alt="drawing" width="700"/>


