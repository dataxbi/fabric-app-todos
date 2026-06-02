# Especificaciones de MyFirstApp Todos

## Objetivo

MyFirstApp Todos es una aplicación de ejemplo construida con Rayfin/Fabric para demostrar un flujo completo de lista de tareas con autenticación, persistencia de datos y despliegue en Fabric.

La aplicación debe servir como referencia sencilla para entender:

- Cómo arrancar una app React + Vite con Rayfin.
- Cómo autenticar usuarios con Fabric.
- Cómo definir un modelo de datos Rayfin.
- Cómo consultar y modificar datos desde el cliente tipado.
- Cómo desplegar backend, esquema de datos y hosting estático con `rayfin up`.

## Funcionalidad

La pantalla principal debe permitir al usuario autenticado:

- Ver sus tareas ordenadas por fecha de creación, de más reciente a más antigua.
- Crear una tarea introduciendo un título no vacío.
- Marcar una tarea como completada.
- Volver a marcar una tarea completada como pendiente.
- Eliminar una tarea.
- Ver un estado vacío cuando todavía no tiene tareas.
- Cerrar sesión.

Las tareas se separan visualmente en dos grupos:

- `To Do`: tareas pendientes.
- `Completed`: tareas completadas.

## Modelo de Datos

La entidad principal es `Todo`, definida en `rayfin/data/Todo.ts`.

Campos:

- `id`: identificador UUID de la tarea.
- `title`: texto obligatorio entre 1 y 100 caracteres.
- `isCompleted`: booleano que indica si la tarea está completada.
- `createdAt`: fecha de creación.
- `user_id`: identificador del usuario propietario.

La entidad debe tener permisos explícitos con `@role('authenticated', '*')` y una política de seguridad por fila que limite el acceso a las tareas del usuario actual:

```ts
policy: (claims, item) => claims.sub.eq(item.user_id)
```

En MSSQL, los campos de texto deben declarar longitud máxima. Por eso `user_id` usa `@text({ max: 255 })`.

## Autenticación y Datos

La aplicación usa Rayfin Client para todas las operaciones de datos.

No se deben hacer llamadas GraphQL manuales ni `fetch()` directo para operaciones CRUD de tareas. Las operaciones deben pasar por `client.data.Todo`.

En local, si el backend configurado apunta a `localhost`, la app puede usar el fallback en memoria incluido en `src/services/todos.ts` para que la experiencia de desarrollo sea funcional sin base de datos remota.

En Fabric, la app debe usar:

- Fabric authentication.
- Rayfin Data.
- Static Hosting.

## Interfaz

La UI debe mantenerse sobria y orientada a una herramienta de productividad:

- Sin landing page ni contenido de marketing.
- Primera pantalla útil: login o lista de tareas.
- Controles claros para añadir, completar y borrar tareas.
- Estado de carga durante la comprobación de autenticación.
- Estado vacío cuando no hay tareas.
- Texto de marca principal: `MyFirstApp Todos`.

## Scripts y Despliegue

Comandos principales:

- `npm run dev`: aplica configuración Rayfin sin desplegar hosting estático y arranca Vite.
- `npm test`: ejecuta pruebas con Vitest.
- `npm run lint`: ejecuta ESLint.
- `npm run build`: compila TypeScript y genera build de Vite.
- `npx @microsoft/rayfin-cli up`: despliega la app completa en Fabric.
- `npx @microsoft/rayfin-cli up status`: comprueba estado del despliegue.

La URL publicada no se versiona porque pertenece al entorno privado de Fabric.

## Criterios de Aceptación

Antes de considerar un cambio listo:

- `npm test` debe pasar.
- `npm run lint` debe pasar sin errores.
- `npm run build` debe pasar.
- La app local debe responder en `http://localhost:5173/` cuando `npm run dev` esté activo.
- Tras despliegue, la URL de Static Hosting debe responder `200`.
- La app desplegada debe conservar el título HTML `MyFirstApp Todos`.
