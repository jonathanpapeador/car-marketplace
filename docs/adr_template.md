# ADR-001: Adopción de Stack Tecnológico Cliente-Servidor (React, Django, PostgreSQL)

<!--
Nombra el archivo con el número consecutivo y un slug corto, por ejemplo:
docs/adr/0001-usar-postgresql-como-base-de-datos-principal.md
Los ADR se numeran en orden y NUNCA se editan después de aceptados para
cambiar la decisión en sí (sí puedes corregir errores de redacción). Si la
decisión cambia, escribes un ADR nuevo y marcas este como reemplazado
(ver "Estado"). Así el repositorio queda como una bitácora histórica de
por qué el sistema es como es.
-->
 
Autores:
 - @jonathanpapeador
 - @cromerosi
 - @JulrR0d

Fecha: 2026-09-10
 
## Estado

<!--
Uno de: Propuesto | Aceptado | Rechazado | Reemplazado por ADR-000Y | Obsoleto
Un ADR "Propuesto" está en discusión. Una vez el equipo decide, pasa a
"Aceptado" (o "Rechazado" si se descarta la propuesta) y ya no se
modifica su contenido de fondo.
-->
 
Aceptado
 
## Contexto
 
<!--
¿Qué problema técnico, restricción o fuerza nos obliga a tomar esta
decisión ahora? Describe la situación de forma neutral y objetiva —
todavía no es el lugar para argumentar a favor de una opción.
Ejemplos de fuerzas en juego: requisitos no funcionales (rendimiento,
seguridad, escalabilidad), restricciones de equipo o de tiempo,
deuda técnica existente, compatibilidad con sistemas ya construidos.
-->
El proyecto requiere el desarrollo de una aplicación web que garantice una alta integridad de datos relacionales, seguridad robusta y una interfaz de usuario altamente interactiva. El equipo necesita equilibrar un tiempo de comercialización rápido (Time-to-Market) con la capacidad de escalar la aplicación a futuro. 

Se requiere una separación clara de responsabilidades que permita desarrollar la lógica de negocio independientemente de la interfaz gráfica, además de mitigar la carga operativa de administrar infraestructura de bases de datos.
 
## Decisión
 
<!--
Qué vamos a hacer, en una o dos frases claras y en tiempo presente
("Vamos a usar X para Y"). Esta es la sección más corta del documento:
un ADR no es un RFC, no necesita convencer a nadie aquí — la
justificación ya quedó en "Contexto" y las alternativas descartadas
van abajo.
-->

Vamos a adoptar una arquitectura cliente-servidor desacoplada utilizando el siguiente stack tecnológico:

1. **Frontend (SPA):** React con TypeScript, empaquetado con Vite, estilizado con Tailwind CSS y gestionado con Axios y React Router.
2. **Backend (API REST):** Python con Django y Django REST Framework (DRF), utilizando JWT para la autenticación sin estado (stateless).
3. **Base de Datos:** PostgreSQL como motor relacional, alojado de forma gestionada (Serverless) en Neon.
 
## Alternativas consideradas
 
<!--
Qué otras opciones se evaluaron y por qué se descartaron. No hace
falta un análisis exhaustivo, basta con dejar constancia de que se
consideraron y el motivo del descarte (costo, madurez, curva de
aprendizaje, no cumple un requisito, etc.).
-->

* **Frontend - Angular o Vue.js:** Se descartó Angular por su alta curva de aprendizaje y rigidez, y Vue por tener un ecosistema de librerías más reducido. React ofrece el equilibrio ideal con un ecosistema masivo.
* **Frontend - JavaScript vs TypeScript:** Se descartó JS puro porque la falta de tipado estático aumenta el riesgo de errores en tiempo de ejecución al integrar estructuras JSON complejas del backend.
* **Backend - FastAPI o Flask:** Se descartaron en favor de Django porque, aunque son más ligeros, carecen de las "baterías incluidas" (ORM robusto, panel de administración, sistema de autenticación integrado) que aceleran drásticamente el desarrollo inicial.
* **Backend - Node.js (Express):** Se descartó porque el ecosistema de Python ofrece una mejor base para futuras integraciones de análisis de datos o scripts analíticos.
* **Base de Datos - MongoDB (NoSQL):** Se descartó porque la naturaleza del dominio del proyecto exige relaciones estrictas y cumplimiento de normativas ACID, lo cual es la fortaleza de PostgreSQL.
* **Infraestructura - PostgreSQL autogestionado (EC2/VPS):** Se descartó por el alto costo operativo de mantenimiento, parches y backups, optando por el modelo DBaaS de Neon.
 
## Consecuencias
 
<!--
¿Qué se vuelve más fácil o más difícil después de esta decisión?
Incluye efectos positivos y negativos por igual — un ADR honesto
también documenta el costo que se está aceptando (deuda técnica
introducida, dependencia nueva, curva de aprendizaje del equipo).
-->
 
**Positivas:**
* **Escalabilidad independiente:** Al separar frontend y backend mediante una API REST y usar JWT, podemos escalar los servidores web o cambiar de cliente (ej. crear una app móvil) sin tocar la lógica de negocio.
* **Alta productividad:** El ORM de Django y las clases utilitarias de Tailwind reducen significativamente el tiempo de escritura de código repetitivo (boilerplate).
* **Robustez de datos y código:** TypeScript en el cliente y PostgreSQL en el servidor reducen familias enteras de errores de consistencia antes de llegar a producción.
* **Baja carga operativa:** Neon elimina la necesidad de contar con un DBA (Administrador de Base de Datos) a tiempo completo para tareas de mantenimiento rutinario.

**Negativas (Costos aceptados):**
* **Complejidad de integración:** Mantener dos repositorios o entornos (Frontend y Backend) exige gestionar configuraciones adicionales como políticas CORS y el manejo seguro de los tokens JWT en el cliente.
* **Renderizado Inicial:** Al ser una Single Page Application (React/Vite), la carga inicial en navegadores con conexiones muy lentas puede ser ligeramente superior a la de una aplicación renderizada 100% en el servidor (SSR).
 
<!-- ### Diferencia con un RFC (referencia rápida)
 
Elimina esta sección en el ADR final; queda aquí solo como recordatorio
para quien usa la plantilla.
- Un RFC se escribe ANTES de decidir, para abrir discusión y llegar a
  consenso; es un documento "vivo" mientras dura la deliberación.
- Un ADR registra una decisión YA tomada (o que se está formalizando);
  una vez aceptado, es casi inmutable — si cambia, se escribe un ADR
  nuevo que reemplaza al anterior, no se edita el viejo.
- El RFC suele ser más largo (motivación, métricas, riesgos, preguntas
  abiertas); el ADR es deliberadamente corto: Contexto, Decisión,
  Consecuencias.
- En equipos que usan ambos: el RFC es el proceso de deliberación,
  y al cerrarlo se destila un ADR corto como registro histórico de lo
  que finalmente se decidió.
-->
