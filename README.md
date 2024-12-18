<h1 align="center">Jakarta Server Faces (JSF 3)</h1>
<p><b>Jakarta Server Faces</b> (<b>JSF 3</b>) es un framework de desarrollo web basado en <b>Java</b> diseñado para simplificar la creación de interfaces de usuario dinámicas en aplicaciones empresariales. Es parte de la especificación <b>Jakarta EE</b> y utiliza el patrón <b>Modelo-Vista-Controlador</b> (<b>MVC</b>) para separar la lógica empresarial de la presentación.</p>

![image](https://github.com/user-attachments/assets/571203bc-b6a4-44fc-a875-041d6080e30b)

<h3>Características de JSF 3:</h3>

- <b>Modelo vista controlador (MVC)</b>: Permite separar la lógica de la aplicación (modelo) de la presentación (vista) y el control de flujo de la aplicación (controlador), facilitando el desarrollo y mantenimiento.
- <b>Componentes para interfaces de usuario</b>: Ofrece una amplia gama de componentes reutilizables para crear interfaces de usuario ricas y dinámicas, como botones, tablas, formularios, etc.
- <b>Manejo de eventos</b>: Permite definir y gestionar eventos de usuario, como clics en botones, cambios en campos de texto, entre otros, para interactuar con la lógica del servidor.
- <b>Define reglas de navegación</b>: Proporciona una manera de definir y gestionar la navegación entre diferentes vistas y páginas dentro de la aplicación, facilitando el flujo de la aplicación.
- <b>Validación de campos de formulario</b>: Ofrece mecanismos integrados para validar datos de entrada en formularios, asegurando que la información enviada por el usuario cumpla con ciertos criterios antes de ser procesada.
- <b>Soporte de internacionalización y localización</b>: Permite crear aplicaciones que soporten múltiples idiomas y regiones, adaptando el contenido y formato de acuerdo a la localización del usuario.
- <b>Integración CDI y EJB</b>: Se integra con Contexts and Dependency Injection (CDI) y Enterprise JavaBeans (EJB) para gestionar la inyección de dependencias y proporcionar funcionalidades avanzadas de negocio y transacciones en la aplicación.

<h3>Ciclo de vida</h3>

![image](https://github.com/user-attachments/assets/7bea2367-45ba-4b5a-b91c-1b183b598776)

- <b>Restaura la vista</b>: Se reconstruye el árbol de componentes a partir del estado guardado.
- <b>Aplica valores del request</b>: Los valores enviados por el usuario se aplican a los componentes de la interfaz.
- <b>Procesa eventos</b>:
  - <b>Petición sin parámetros</b>: Se maneja la petición sin parámetros.
  - <b>Renderizar la respuesta</b>: Se prepara la respuesta para ser enviada al cliente.
- <b>Procesa las validaciones</b>: Se validan los datos de entrada según las reglas definidas.
- <b>Procesa eventos</b>:
  - <b>Error de conversión o validación</b>: Se manejan los errores y se prepara la respuesta para informarlos.
  - <b>Renderizar la respuesta</b>: Se genera la vista con los mensajes de error.
- <b>Actualiza valores del modelo</b>: Los valores validados se actualizan en el modelo de datos.
- <b>Procesa eventos</b>:
  - <b>Error de conversión</b>: Se maneja cualquier error de conversión de datos.
- <b>Invoca evento de aplicación</b>: Se invocan los métodos de negocio según las acciones del usuario.
- <b>Procesa eventos</b>: Otros eventos son gestionados a medida que ocurren.
- <b>Renderizar la respuesta</b>: Finalmente, se genera la vista y se envía como respuesta HTTP al cliente.

<h2 align="center">JSF maneja el ciclo de vida HTTP internamente</h2>
<p>JSF es un <b>framework basado en componentes</b> que implementa MVC (Modelo-Vista-Controlador) y encapsula los detalles de las solicitudes HTTP. Esto significa que <b>JSF se encarga del manejo de las peticiones HTTP</b>, de forma que no se necesita interactuar directamente con <b>HttpServletRequest</b>, <b>doGet</b> ni <b>doPost.</b></p>

<h2 align="center">Uso de beans y anotaciones CDI</h2>

La anotación `@Model` que se usa en el controlador `ProductoController` es una combinación de `@Named` y `@RequestScoped`, que es parte del estándar `CDI` (<b>Contexts and Dependency Injection</b>). Esto permite que <b>JSF</b> gestione el ciclo de vida de los objetos y los exponga en la vista como beans.

```java
@Model
public class ProductoController {

}
```

- `@Named`: Permite que el bean sea accesible desde las páginas JSF mediante E.L. (Expression Language), como `#{productoController}`.
- `@RequestScoped`: Define que el bean tendrá un ciclo de vida que dura una sola petición HTTP.

<h2 align="center">Acciones y binding a componentes UI</h2>

En la vista `index.xhtml`, se utilizan componentes como `<p:commandButton>` y `<p:ajax>` de <b>PrimeFaces</b>, que permiten invocar métodos directamente desde el controlador (`ProductoController`).

```xhtml
<p:commandButton value="Eliminar"
    action="#{productoController.eliminar(prod)}"
    update="tabla"/>
```

- `action`: Ejecuta el método `eliminar` en el bean `productoController`.
- `update`: Especifica qué parte de la vista se actualizará tras la ejecución del método.

<b>JSF</b> se encarga de generar las solicitudes HTTP necesarias bajo el capó y llamar a los métodos del controlador, sin que se tenga que escribir manualmente un `servlet` ni manejar `doGet` o `doPost`.

<h2 align="center">Vista declarativa con Facelets</h2>

Facelets (`*.xhtml`) es el motor de vistas de JSF y reemplaza la necesidad de escribir HTML y lógica de backend manualmente en un servlet. Cumple un papel crucial en el diseño de interfaces web dinámicas al permitir que el desarrollador defina la estructura y el comportamiento de la vista directamente en archivos `XHTML` mediante etiquetas declarativas.

```xhtml
            <h:form>
                <div class="p-field p-grid p-my-2">
                    <label for="textoBuscar" class="p-col-fixed" style="width:100px">Buscar</label>
                    <div class="p-col">
                        <p:inputText id="textoBuscar" value="#{productoController.textoBuscar}" placeholder="Buscar">
                            <p:ajax listener="#{productoController.buscar}" event="keyup" update="mostrar tabla"/>
                        </p:inputText>
                    </div>
                    <div class="p-col">
                        <h:outputText value="#{productoController.textoBuscar}" id="mostrar"/>
                    </div>
                </div>
            </h:form>
```

<h3>Relación con el Controlador ProductoController:</h3>

- Método `buscar()`:
  - Invocado por <b>AJAX</b> cada vez que el usuario escribe algo en el campo de texto.
  - Filtra la lista de productos según el valor de `textoBuscar` mediante el método `service.buscarPorNombre(this.textoBuscar)`.
- Propiedad `textoBuscar`:
  - Define la entrada del usuario vinculada al campo de texto de la vista.
  - Su valor se actualiza automáticamente gracias a la vinculación con `value="#{productoController.textoBuscar}"`.
- Lista de productos (`listado`):
  - Contiene los resultados filtrados de la búsqueda.
  - Se utiliza en otras partes de la vista (por ejemplo, en una tabla) para mostrar los productos que coinciden con el criterio de búsqueda.

<h3>Flujo general del comportamiento:</h3>

- El usuario escribe en el campo de texto.
- El evento `keyup` activa el componente <b>AJAX</b>, que envía el texto ingresado al servidor.
- El método `buscar()` en el controlador actualiza la lista de productos según el texto ingresado.
- Las partes de la vista especificadas (`mostrar` y `tabla`) se actualizan dinámicamente con los nuevos datos sin recargar la página completa.

<h3>Ventajas de usar Facelets:</h3>

- Separación de responsabilidades:
  - La vista (`XHTML`) se encarga de definir el diseño y la interacción, mientras que la lógica de negocio está en el controlador.
- Desarrollo rápido y modular:
  - El uso de componentes reutilizables reduce el tiempo de desarrollo y mejora la legibilidad del código.
- Interactividad mejorada:
  - <b>AJAX</b> permite crear experiencias de usuario más dinámicas y fluidas.

<h2 align="center">Eventos y AJAX en JSF</h2>

JSF ofrece soporte integrado para <b>eventos y AJAX</b> que facilitan el manejo de interacciones asincrónicas, como lo hace:

```xml
<p:ajax listener="#{productoController.buscar}" event="keyup" update="tabla"/>
```

- `listener`: Llama al método `buscar` del controlador.
- `update`: Actualiza dinámicamente partes de la página (sin recargar toda la vista).

El soporte de <b>AJAX</b> y eventos simplifica la interacción con el servidor y evita la necesidad de escribir lógica manual en un servlet.

<h2 align="center">Abstracción del HTTPServlet</h2>

El servlet todavía existe en JSF internamente, ya que <b>JSF utiliza un servlet especial llamado</b> `FacesServlet` para procesar todas las peticiones. Este servlet es configurado automáticamente en el archivo `web.xml` o mediante anotaciones.

```xml
    <servlet>
        <servlet-name>faces-servlet-name</servlet-name>
        <servlet-class>jakarta.faces.webapp.FacesServlet</servlet-class>
    </servlet>

    <servlet-mapping>
        <servlet-name>faces-servlet-name</servlet-name>
        <url-pattern>*.jsf</url-pattern>
    </servlet-mapping>
```

<h2 align="center">AJAX - Faces - PrimeFaces</h2>
<h3>AJAX (Asynchronous JavaScript and XML):</h3>

- Es una técnica que permite realizar solicitudes al servidor sin recargar toda la página web.
- Funciona de manera asíncrona, es decir, el navegador puede enviar datos al servidor y recibir respuestas sin interrumpir la experiencia del usuario.
- En <b>JSF</b> y <b>PrimeFaces</b>, <b>AJAX</b> se utiliza con componentes como `<p:ajax>` para actualizar partes específicas de la página de forma eficiente.

<h3>Faces (Jakarta Faces / JSF):</h3>

- Es un <b>framework</b> para aplicaciones <b>web en Java</b>, parte de la especificación de Jakarta EE (anteriormente Java EE).
- Permite desarrollar interfaces de usuario basadas en componentes reutilizables.
- Usa páginas <b>XHTML</b> para definir la interfaz de usuario y <b>beans</b> (como `ProductoController`) para manejar la lógica de la aplicación.
- Facilita la integración de la lógica del servidor con el frontend.

<h3>PrimeFaces:</h3>

- Es una <b>biblioteca de componentes</b> para <b>JSF</b>.
- Proporciona componentes avanzados y personalizables como <b>botones, tablas, formularios, diálogos</b> y soporte integrado para <b>AJAX</b>.
- Simplifica el desarrollo de interfaces modernas y ricas en funcionalidades, optimizando la interacción con el usuario.

<p><b>AJAX</b> facilita la comunicación asíncrona con el servidor, <b>JSF</b> gestiona la arquitectura y el flujo de la aplicación web, y <b>PrimeFaces</b> ofrece componentes visuales avanzados que mejoran la experiencia de desarrollo.</p>
