# 1. Definición del problema

- Actualmente, muchos concesionarios gestionan clientes, inventario, ventas y créditos mediante hojas de cálculo o herramientas independientes. Esta fragmentación provoca problemas recurrentes como duplicidad de datos, errores de registro, falta de trazabilidad y lentitud en los procesos administrativos, además de dificultar el control del inventario y la generación de reportes.
- La falta de un sistema centralizado también dificulta el seguimiento de clientes, la gestión de usuarios y el control de los permisos de acceso, afectando la eficiencia operativa e incrementando la probabilidad de errores humanos.
- En consecuencia, se requiere desarrollar un sistema de gestión que centralice la información y permita optimizar los procesos principales del concesionario de forma segura, organizada y escalable.

# 2. Objetivos generales

- Diseñar e implementar un sistema de software para concesionarios de vehículos enfocado en la centralización de procesos clave —clientes, inventario, ventas y permisos de usuario— para mejorar la trazabilidad de la información, reducir incidencias administrativas y optimizar la operativa comercial.

# 3. Objetivos específicos

- Analizar los procesos operativos y requerimientos del concesionario para definir las reglas de negocio y el alcance del sistema de gestión.

- Diseñar la arquitectura de software y el modelo de datos aplicando el paradigma de Programación Orientada a Objetos para garantizar la escalabilidad y mantenibilidad de la aplicación.

- Implementar una API REST utilizando Spring Boot para la gestión estructurada de clientes, inventario, ventas y roles de usuario.

- Desarrollar el módulo de seguridad, autenticación y autorización utilizando Spring Security y JSON Web Tokens (JWT) para asegurar el acceso controlado a los recursos.

- Realizar las pruebas funcionales e integración y validación del sistema para verificar el correcto funcionamiento de las operaciones comerciales y el manejo seguro de la información.

- Documentar la arquitectura, la base de datos y la API REST (mediante OpenAPI/Swagger) para facilitar el mantenimiento, uso y futuras expansiones del sistema.

# 4. Alcance

## Alcance Incluido (Dentro del Proyecto)
- Gestión de Entidades Clave (CRUD): Gestión de vehículos, clientes, usuarios, ventas y roles del sistema mediante operaciones de creación, consulta, actualización y eliminación (CRUD), según corresponda a cada entidad.

- Control de Acceso y Seguridad: Módulo de autenticación y autorización mediante tokenización (JWT), con asignación de roles y permisos diferenciados para limitar la operatividad según el perfil del usuario.

- Control de Inventario: Permitirá registrar y actualizar el estado operativo de cada vehículo (disponible, reservado, vendido o en mantenimiento), garantizando el control del inventario.

- Generación de Reportes Básicos: Módulo de consultas consolidando métricas clave como volumen de ventas, rotación de inventario y consultas y reportes básicos relacionados con ventas, inventario y clientes del concesionario.

- Documentación Técnica: Especificación de la arquitectura del backend, diagramas del modelo de datos y documentación interactiva de la API REST.

## Alcance no Incluido (Fuera del Proyecto)

- Procesamiento de Pagos e Integración Bancaria: No se contempla el procesamiento de transacciones financieras en línea, pasarelas de pago ni sincronización directa con entidades bancarias.

- Facturación Electrónica: La emisión de comprobantes fiscales electrónicos no formará parte de esta etapa del desarrollo.

- Plataformas Móviles: El proyecto contempla únicamente el desarrollo del backend mediante una API REST, excluyendo aplicaciones móviles y clientes web completos.

- Sistemas de Comunicación e Integración: No se implementará mensajería o chat en tiempo real, ni integraciones con software o servicios externos (CRMs, ERPs de terceros).

- Módulos de Inteligencia Artificial: Se excluyen algoritmos de analítica predictiva, recomendadores o cualquier componente basado en aprendizaje automático.

### Supuestos

Para el desarrollo del sistema se asume que:

- El concesionario cuenta con acceso a Internet.
- Los usuarios poseen conocimientos básicos sobre el uso de sistemas de información.
- Los vehículos registrados pertenecen únicamente al concesionario.
- Toda la información registrada será suministrada por usuarios autorizados.

### Limitaciones

- El sistema no contempla el almacenamiento de imágenes en esta primera versión.
- No se integrará con servicios gubernamentales para consultar antecedentes del vehículo.
- No se implementará facturación electrónica.
- No existirá sincronización con inventarios externos.

# 5. Identificación de los Stakeholders

Los stakeholders representan las personas, grupos o entidades que tienen interés en el desarrollo y funcionamiento del sistema, ya sea porque lo utilizan directamente o porque se benefician de la información que este proporciona.

| Stakeholder | Descripción | Interés |
|-------------|-------------|---------|
| Dueño del concesionario | Responsable del negocio. | Supervisar la operación y acceder a reportes para la toma de decisiones. |
| Gerente | Administra el funcionamiento general del concesionario. | Controlar ventas, inventario y desempeño del personal. |
| Administrador | Responsable de administrar la configuración del sistema y los usuarios. | Administrar usuarios, vehículos y permisos. |
| Vendedor | Responsable de la atención al cliente y las ventas. | Registrar clientes, consultar inventario y realizar ventas. |
| Cliente | Persona interesada en adquirir un vehículo. | CRecibir una atención eficiente y acceder a información confiable sobre los vehículos disponibles. |
| Área contable | Responsable de la gestión financiera. | Consultar información de ventas y facturación. |

#  6. Actores del Sistema

| Actor |	Responsabilidades |
| Administrador |	Gestionar el sistema, usuarios, roles, vehículos, ventas e inventario. |
| Vendedor |	Registrar clientes, consultar vehículos, gestionar ventas y actualizar el estado del inventario. |