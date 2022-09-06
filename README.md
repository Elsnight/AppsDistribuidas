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


Un documento, en general, va a tener un título principal y luego una serie de
secciones, con una jerarquía inferior, que estructuran el texto en partes
relacionadas. Un `README`, por ejemplo, tendrá, tras una introducción,
instrucciones para instalar, para ejecutar y quizás una nota sobre la licencia
o sobre cómo colaborar con el mismo.

Si quieres poner cabeceras a tu texto, algo así como los títulos de cada
sección, solo tienes que escribir el carácter almohadilla y un espacio antes
de la frase a resaltar. Cuantas más almohadillas pongas, más abajo en la
jerarquía estará esa cabecera. Es decir, `# Este es el nombre de mi proyecto`
y `## Cómo instalar`. `### Instalar desde GitHub` y así.

Por ejemplo, si quieres tener tu texto en cursiva, solo necesitas abrir y
cerrar la oración con un asterisco, tal que `*este texto se muestra en
cursiva*`. También vale la barra baja "`_`" en lugar del asterisco. ¿Qué tengo
que hacer si quiero poner ese mismo texto en negrita? En lugar de utilizar un
asterisco, utiliza dos. También vale para el caso del carácter "barra baja".
Osea, `**este texto estaría en negrita**`. Y `**_este otro estaría en negrita y
cursiva_**`.

Markdown no interpretará, al menos por defecto, cuando quieras incluir
en tu texto un enlace a una página web. Para incluir uno, tienes que hacerlo
de la forma siguiente:`[Texto a mostrar](URL a la que ir)`. ¿Así de fácil? Así
de fácil.

Insertar imágenes es muy parecido a insertar enlaces: la estructura es
la misma, salvo que tenemos que poner un signo de admiración justo antes
del primer corchete. Osea, `![Texto a mostrar](URL a la imagen)`. En cuanto
al "texto a mostrar", es el texto que verás si la imagen no carga o, si por
ejemplo has exportado el documento a HTML, el texto que se muestra
al poner el cursor del ratón encima.

¿Qué hay en un texto más enriquecedor que hacer referencia a otros textos
o, incluso, a lo que simplemente alguien dijo en algún momento? Para insertar
una cita, solo necesitamos iniciar la cita con el carácter "mayor que". Imagina
que queremos citar a John Johnson, entonces: `> "Primero resuelve el problema.
Entonces, escribe el código"`. Este texto se interpretará como:

> "Primero resuelve el problema. Entonces, escribe el código"

Las listas tampoco podían faltar. Aquí tenemos dos opciones:
* Listas sin orden: para estas listas solamente necesitas poner cada elemento
de la lista en una nueva línea y preceder dicha línea por un asterisco y
un espacio. Un ejemplo de lista sería:
```bash
`* Resolver el problema`
`* Escribir el código`
`* Compartir la solución`
```

Aquí todavía continúa el texto.
  Esta es la primera línea del bloque de código.
     La segunda línea tiene aún más sangría.
  Esta es otra línea del bloque de código.
Aquí vuelve a empezar el texto

* Listas ordenadas: tienes que precederlas por un número seguido de un punto:
```bash
`1. Resolver el problema`
`2. Escribir el código`
`3. Compartir la solución`
```
Imagina que por alguna razón, no numeras bien la lista. ¡No pasa nada! El
intérprete se dará cuenta y mostrará correctamente la lista ordenada.

¿Y qué pasa si quiero hacer una lista dentro de un elemento de una lista?
Solamente tienes que añadir un nivel de indentación. Por ejemplo:

```bash
`* Resolver el problema`
` * Mirar posibles soluciones`
` * Establecer cual es la más adecuada`
`* Escribir el código`
` * Elegir un lenguaje`
` * Elegir los tipos de dato más adecuados`
`* Compartir la solución`
` * Publicarla en Github`
` * Escribir un artículo sobre ello`
```

Resultaría en:
* Resolver el problema
 * Mirar posibles soluciones
 * Establecer cual es la más adecuada
* Escribir el código
 * Elegir un lenguaje
 * Elegir los tipos de dato más adecuados
* Compartir la solución
 * Publicarla en Github
 * Escribir un artículo sobre ello

Con esta pincelada, tienes casi todo lo que hay que saber sobre Markdown.
Pero Markdown es una base que tiene diferentes *sabores*. Algunos, 
[como el de GitHub](https://guides.github.com/features/mastering-markdown/),
tienen algunas otras marcas que pueden ser muy útiles, como listas de
tareas, tablas o resaltadores de sintaxis. Incluso emojis.

## *En resumen*

Markdown es un buen lenguaje para enriquecer el texto plano. Con
unas pocas reglas de sintaxis puede hacer que tu texto incluya
negritas, cursivas o cabeceras entre otros. Además, es el lenguaje que
se usa en webs como las que se alojan en Github. Pero ese ya es otro capítulo.
