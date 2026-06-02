# MyFirstApp Todos

Aplicacion minima de ejemplo construida con **Microsoft Fabric Apps** y **Rayfin**.

Este repositorio es una prueba inicial para validar el flujo completo de una app sencilla:

- scaffold de proyecto con Rayfin;
- autenticacion integrada con Fabric;
- modelo de datos declarativo;
- CRUD basico de tareas;
- despliegue en Fabric con hosting estatico.

La aplicacion implementa una lista de tareas muy simple. Un usuario autenticado puede crear tareas, marcarlas como completadas, volver a dejarlas pendientes y eliminarlas.

## Contexto

Este proyecto nace como una prueba tecnica alrededor de las novedades de **Microsoft Build 2026**, especialmente el enfoque de crear y publicar aplicaciones de forma rapida sobre Microsoft Fabric.

La idea no es construir una aplicacion de produccion completa, sino una base minima para entender como encajan las piezas:

- React + Vite para el frontend.
- Rayfin Client para acceso tipado a datos.
- Rayfin Data para definir la entidad `Todo`.
- Fabric Authentication para iniciar sesion.
- Static Hosting de Fabric para publicar la app.

## Creacion

La app fue creada de forma asistida con **Codex**, usando **GPT-5**, a partir del scaffold oficial de Rayfin:

```bash
npm create @microsoft/rayfin@latest -- "MyFirstApp" --project-name "MyFirstApp" --workspace "Fabric_App" --template todoapp --overwrite
```

Despues se ajusto la marca visual a `MyFirstApp Todos`, se documento la especificacion funcional en espanol y se desplego en Fabric.

## Documentacion del proyecto

- [Especificaciones funcionales](docs/especificaciones.md)
- [Instrucciones para agentes](AGENTS.md)

## Documentacion externa

- [Microsoft Fabric documentation](https://learn.microsoft.com/en-us/fabric/)
- [Microsoft Fabric fundamentals](https://learn.microsoft.com/en-us/fabric/fundamentals/)
- [Microsoft Fabric REST API documentation](https://learn.microsoft.com/en-us/rest/api/fabric/articles/)
- [Microsoft Build 2026](https://build.microsoft.com/)
- [Build session: Build and ship production-ready apps fast with Microsoft Fabric](https://build.microsoft.com/sessions/DEM313)
- [Rayfin CLI package](https://www.npmjs.com/package/@microsoft/rayfin-cli)
- [Rayfin project generator](https://www.npmjs.com/package/@microsoft/create-rayfin)

## Desarrollo local

Instalar dependencias:

```bash
npm install
```

Arrancar entorno local:

```bash
npm run dev
```

La app queda disponible en:

```text
http://localhost:5173/
```

## Comandos utiles

```bash
npm test
npm run lint
npm run build
npx @microsoft/rayfin-cli up
npx @microsoft/rayfin-cli up status
```

## Estructura principal

```text
rayfin/
  rayfin.yml
  data/
    Todo.ts
    schema.ts

src/
  App.tsx
  components/
  hooks/
  pages/
  services/
```

## Estado

Prueba inicial completada:

- app creada;
- autenticacion y datos habilitados;
- entidad `Todo` desplegada;
- hosting estatico publicado;
- documentacion inicial incluida;
- repositorio Git inicializado.
