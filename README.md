# challenge-devsecops
# 1- Identificar la infraestructura necesaria para ingestar, almacenar y exponer datos

## a-. En que consiste la infraestructura
### Diferentes fuentes de datos -> Bus de eventos -> Proceso de transformación y carga -> base de datos -> API 

### La primera parte necesaria son las diferentes fuentes de datos (envían información relevante para data analytics), la cuál será la totalidad de nuestra fuente de informaciónd de entrada, las fuentes de datos las definirá el usuario de acuerdo a lo que requiera.

### La segunda parte será el bus de eventos google Pub/Sub. El bus de eventos es un servicio de mensajería escalable y asíncrono que separa los servicios que producen mensajes de los que los procesan. El bus de eventos permite que los servicios se comuniquen de forma asíncrona. Una forma de implementar el bus de eventos es el producto google Pub/Sub.

### La tercera parte son servicios que se suscribirán a esa fuente de información y que realizarán un primer filtro de información para seleccionar sólo lo que será necesario analizar según nuestro caso de negocio, estos servicios pueden ser microservicios que estén deployados en la nube y que estén constantemente consultando la actualización de información y la llegada de nuevos datos. En este caso el componente será una google cloud function que consume el servicio y lo envía a la base de datos. 

### La cuarta parte será la ingesta a nuestra base de datos que almacenará dicha información previamente filtrada y estructurada de tal forma que en el siguiente paso los consumidores de esta información  puedan analizar y extraer según sea necesario, esta ingesta puede ser realizada mediante una API que tenga acceso a la base de datos y que esté solamente expuesta para este servicio con la finalidad de guardar la información requerida. La base de datos será Big Query de google.

### La quinta parte serán las APIS que expondrán esta información con ciertos filtros para que estos datos sean analizados por el cliente final o sean analizados mediante un sistema de reportería, en este caso podría ser un sistema jasper report que se conecte a las apis para ordenar y mostrar la información de acuerdo a los parámetros que se establezcan. Este componente será google Apigee.

### La sexta parte y última serán los sistemas de reportería y herramientas que tenga el cliente para poder analizar la información disponibilizada para cada caso particular (Esto estaría fuera de la infraestructura de esta solución, pero para efectos de documentación y conocimiento debe estar indicada).