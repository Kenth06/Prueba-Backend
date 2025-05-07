# Prueba Técnica para Backend en Cloudflare Workers

## 1. Bienvenida

¡Bienvenido(a) a nuestra prueba técnica! Queremos evaluar tu capacidad de adaptarte a nuevas tecnologías y resolver problemas de forma práctica usando **Cloudflare Workers**. No buscamos un código perfecto, sino tu habilidad para investigar, aprender y proponer soluciones.

> **¿Por qué Cloudflare Workers?**  
> * **Latencia global**: Cloudflare Workers permite ejecutar código directamente en múltiples ubicaciones alrededor del mundo, lo que reduce significativamente la latencia para los usuarios, asegurando una experiencia más rápida y eficiente.  
> * **Bajo coste y sin gestión de infraestructura**: Cloudflare se encarga de la infraestructura, lo que ahorra tiempo y dinero. Solo pagas por lo que usas sin preocuparte por el mantenimiento o la escala.

Te invitamos a que completes este desafío en un plazo **aproximado de 3 días** (72 horas) desde que lo recibas. ¡Mucho éxito!

---

## 2. Requisitos

Asegúrate de contar con lo siguiente antes de comenzar:

1. **Cuenta gratuita en [Cloudflare](https://dash.cloudflare.com/sign-up)** y la CLI de **[Wrangler](https://developers.cloudflare.com/workers/wrangler/get-started/)** instalada.  
2. **[Node.js ≥ 18](https://nodejs.org/es/)** y un gestor de paquetes (npm, pnpm o yarn).  
3. Un editor de código, preferiblemente **[Visual Studio Code](https://code.visualstudio.com/)**.  
4. **[Git](https://git-scm.com/)** para crear tu repositorio y subir tus cambios. 
5. **Cuenta en [GitHub](https://github.com/)** donde crearás el repositorio y abrirás el Pull Request de entrega.  

---

## 3. Instrucciones de Flujo de Trabajo

1. Crea un **nuevo repositorio** en la plataforma GitHub. Puede ser público o privado; si es privado, asegúrate de invitarnos como revisores.  
2. Opcionalmente, crea una rama para tu solución (p. ej. `feature/tu-nombre`) o trabaja en la rama principal si lo prefieres.  
3. Implementa todas las tareas descritas más abajo dentro de tu repositorio.  
4. Cuando finalices (o se cumpla el plazo de 72 h), abre un **Pull Request** dentro de tu propio repositorio (por ejemplo, de `feature/tu-nombre` a `main`) donde incluyas:  
   * Tus observaciones sobre limitaciones o mejoras pendientes.  
   * La **URL en producción** de tu Cloudflare Worker (`wrangler deploy`).  
   * Cualquier instrucción extra para probar tu API.  
5. Comparte con nosotros el enlace a ese Pull Request para que podamos revisarlo.

---

## 4. Tareas

### Implementar un CRUD con Cloudflare Workers, Hono y Drizzle ORM sobre D1

1. **Configurar el proyecto**  
   * Utiliza **TypeScript** como lenguaje principal.  
   * Tipa de forma explícita los objetos (payloads) y las respuestas de tu API usando `interface` o `type` de TypeScript; evita el uso de `any`.  
   * Agrega la dependencia de **[Hono](https://hono.dev/docs/getting-started/cloudflare-workers)** para manejar el enrutado y la lógica de tu API.  
   * Configura **[Drizzle ORM](https://orm.drizzle.team/docs/connect-cloudflare-d1)** para interactuar con la base de datos D1.  

2. **Definir modelos y migraciones**  
     * Elige **un** modelo de datos de ejemplo (por ejemplo, `users`, `tasks`, `posts`, etc.)
   * Al elegir un de las opciónes de modelos de datos mencionados anteriormente, define con claridad las **tablas, columnas, relaciones y restricciones** que sean necesarias:  
     * El esquema debe ser **coherente** y estar **documentado** (comentarios en el código y/o en las migraciones).  
     * Debe cubrir todos los requisitos de las tareas restantes.  
   * Crea y versiona las migraciones usando **Drizzle ORM** o las **[migraciones oficiales de D1](https://developers.cloudflare.com/d1/reference/migrations/)**.  
     * Incluye al menos una migración de creación inicial y, si lo ves útil, migraciones posteriores de ejemplo (p. ej. añadir una columna o crear una relación). 

3. **Endpoints CRUD**  
   Implementa los endpoints básicos de un CRUD para tu modelo de datos elegido (usaremos en este caso `items` como ejemplo):  
   * **GET** `/items` (listar todos)  
   * **GET** `/items/:id` (obtener uno por ID)  
   * **POST** `/items` (crear uno nuevo)  
   * **PUT** `/items/:id` (actualizar)  
   * **DELETE** `/items/:id` (eliminar)  

4. **Seguridad: Middleware de API Key**  
   * Crea un middleware en Hono que verifique la cabecera `X-API-Key` (o la que prefieras).  
   * Almacena la clave en un binding o variable de entorno (`API_KEY`) configurado en `wrangler.toml o wrangler.jsonc`,  la forma recomendada es guardarla como un **secret** con [Wrangler](https://developers.cloudflare.com/workers/wrangler/commands/#secret-put) .  
   * Si la clave está ausente o no coincide, responde con **401 Unauthorized**.  
   * Aplica el middleware a todas las rutas del CRUD (o a un router padre) para proteger tu API.  
    * Cuando el equipo revisor lo solicite, proporciona la API Key **por un canal privado o en un comentario del Pull Request si el repositorio es privado** para que puedan probar los endpoints protegidos. 



5. **Despliegue**  
   * Realiza el despliegue con `wrangler deploy`.  
    * Asegúrate de que tu `wrangler.toml` o `wrangler.jsonc` incluya los bindings de D1.

6. **Entrega de la URL pública**  
   * Incluye la **URL pública** de tu Worker en la descripción del Pull Request (ver sección 6).  

> **Tip**: Añade validaciones, pruebas simples o comentarios en el código para demostrar la forma en que verificas tus endpoints y la seguridad del middleware.

---

## 5. Recursos Útiles

* **Cloudflare Workers**  
  [Documentación oficial](https://developers.cloudflare.com/workers/)  

* **Wrangler CLI**  
  [Guía de comandos: `wrangler dev`, `wrangler deploy`, `wrangler d1`, etc.](https://developers.cloudflare.com/workers/wrangler/)  

* **Hono**  
  [Uso con Cloudflare Workers]((https://hono.dev/docs/getting-started/cloudflare-workers))  

* **Drizzle ORM**  
  [Sitio oficial](https://orm.drizzle.team/)  
  [Guía y ejemplos](https://orm.drizzle.team/docs/column-types/sqlite)  
  [Conexión con D1 / Migraciones](https://orm.drizzle.team/docs/connect-cloudflare-d1)  

* **D1 Database**  
  [Información oficial](https://developers.cloudflare.com/d1/)  

* **Tutorial CRUD (Hono + Workers + D1)**  
  [A comments API with Cloudflare D1 + Hono](https://developers.cloudflare.com/d1/tutorials/build-a-comments-api/)  

* **Cloudflare Workers Secrets**  
  [Documentación oficia de Cloudflare Workers secretsl](https://developers.cloudflare.com/workers/configuration/secrets/)  

---

## 6. Presentación de la Prueba

1. Asegúrate de que todo tu código esté subido a tu repositorio.  
2. Crea el **Pull Request** indicado en la sección 3.  
3. En la descripción del Pull Request incluye:  
   * Cualquier limitación o mejora pendiente.  
   * La **URL en producción** de tu Worker (resultado de `wrangler deploy`).  

Una vez concluyas la prueba, crea el **Pull Request** dentro de los **3 días hábiles** y avísanos por el medio de contacto acordado para que podamos comenzar la revisión.

---

¡Gracias por participar en nuestro proceso de selección y mucho éxito!
