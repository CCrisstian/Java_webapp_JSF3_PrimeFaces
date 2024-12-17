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
