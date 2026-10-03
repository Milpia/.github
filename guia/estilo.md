# Guía de estilo de la documentación Milpia

Esta guía la comparten todos los repositorios de Milpia. Su objetivo es uno:
que **cualquier persona que llegue nueva entienda un proyecto y lo use por sí
misma**, y que pasar de un repositorio a otro se sienta familiar.

> **Regla de oro:** escribe para quien llega mañana, no para quien ya lo sabe.

---

## 1. Qué documentos tiene cada repositorio

| Archivo | Para quién | Qué responde |
|---|---|---|
| `README.md` | Todo el que abre el repo | Qué es, por qué existe, cómo empezar en 5 minutos y dónde seguir |
| `docs/README.md` | Quien va a trabajar con él | La puerta de entrada: caminos según lo que vienes a hacer |
| `docs/<tema>.md` | Quien ya sabe qué busca | **Un archivo por pregunta** («quién entra a qué», «cómo se despliega») |
| `AGENTS.md` | Personas y asistentes de IA | Reglas de trabajo: qué nunca hacer, flujo de git, secretos |
| `specs/` | Quien cambia el sistema | El porqué de cada decisión, antes del código |

Plantillas listas para copiar: [`plantillas/README.md`](../plantillas/README.md) y
[`plantillas/docs-README.md`](../plantillas/docs-README.md).

## 2. El README: una portada, no un manual

El README tiene que poder leerse en **dos minutos**. Todo lo que no cabe ahí
vive en `docs/` y se enlaza.

Orden fijo, de lo general a lo concreto:

1. **Cabecera centrada:** nombre, una frase de valor (qué consigue alguien con
   esto, no qué tecnología usa) y los badges de estado **reales** (CI, deploy,
   vigilancia). Nada de badges decorativos.
2. **En 30 segundos:** tres viñetas: qué es, dónde corre y cómo se cambia.
3. **Cómo encaja:** un diagrama Mermaid **simple**, de 8 a 12 cajas. El
   diagrama completo, si existe, va plegado en `<details>`.
4. **Empieza aquí:** una tabla con 2 o 3 caminos según el rol («soy nuevo»,
   «opero producción», «cambio el sistema»).
5. **Stack:** compacto, agrupado por capa, una línea por pieza. El detalle, en
   `docs/`.
6. **Cómo se trabaja:** el ciclo spec → plan → tareas → PR → despliegue, en una
   línea o un diagrama pequeño.
7. **Documentación y reglas:** enlaces a `docs/README.md`, `AGENTS.md` y la
   constitución, si la hay.

## 3. Cómo se escribe una receta

Cada procedimiento (conectarse, desplegar, rotar un secreto) sigue el mismo
molde, para que funcione como inducción:

- **Para qué sirve**, en una frase, antes del primer comando.
- **Requisitos** explícitos: qué instalar y qué cuenta o grupo hace falta.
- **Pasos numerados, un comando por paso**, cada uno con su **salida esperada**.
- **Errores frecuentes** en una tabla: el mensaje literal, qué pasa y qué hacer.
- **Cómo se deshace**, si el procedimiento cambia algo.

Y estas reglas:

- **Nunca** pongas secretos en un comando que quede en el historial. Usa
  `read -rs` y archivos con permisos `600`.
- **Nunca** guardes una opción entera en una variable para expandirla después
  (`$R`): zsh no la separa. Escribe la opción y guarda solo el valor
  (`--resolve $RS`).
- **Nunca** metas `$( … )` en comandos que alguien correrá como
  `ssh host "…"`: se evalúan en su máquina, no en el servidor.

## 4. Lenguaje

- **En español, claro y directo.** Frases cortas, voz activa y sujeto explícito
  («Traefik enruta la petición», no «la petición es enrutada»).
- **Cada sigla se explica la primera vez**: «SSO (inicio de sesión único)».
- **Las cosas se llaman como en el código.** Si el contenedor es
  `milpia-dokploy`, no escribas «el panel de despliegue» en un comando.
- **Presente para lo que existe y futuro solo para lo planeado**, y lo planeado
  se marca como tal.
- **Sin «simplemente», «obviamente» ni «solo hay que»**: no aportan nada y hacen
  sentir torpe a quien no lo ve claro.
- **Commits y títulos de PR en inglés** (Conventional Commits). Descripciones y
  documentación en español.

## 5. Estilo visual

Profesional, con carácter y fácil de mantener.

- **Iconos:** uno por título de sección del README, como mucho, y siempre del
  mismo juego:

  | Sección | Icono |
  |---|---|
  | En 30 segundos | ✨ |
  | Cómo encaja | 🗺️ |
  | Empieza aquí | 🧭 |
  | Stack | 🧱 |
  | Seguridad | 🛡️ |
  | Cómo se trabaja | 🔁 |
  | Documentación | 📚 |
  | Contribuir | 🤝 |

  Nunca dentro del texto ni en las tablas.
- **Badges:** solo de estado real, del propio GitHub Actions
  (`…/actions/workflows/<archivo>.yml/badge.svg`), que funcionan también en
  repos privados para quien tiene acceso.
- **Diagramas:** Mermaid en el propio Markdown, para que se vean en GitHub y se
  revisen en el PR. Uno simple a la vista y el detallado plegado.
- **Detalle plegable:** `<details><summary>…</summary>` para tablas largas o
  diagramas completos. La portada queda limpia y la información no se pierde.
- **Tablas** para comparar o mapear; **viñetas** para listas; **párrafos
  cortos** para explicar el porqué.

## 6. Referencias estables

Las secciones numeradas (`§4.5`, `§7.8`) que citan specs y PRs **no se
renumeran**: se añade al final o se marca como retirada. Romper un ancla rompe
la historia.

## 7. Antes de dar un documento por terminado

- [ ] Una persona nueva puede seguirlo sin preguntar.
- [ ] Cada comando tiene su salida esperada.
- [ ] No hay secretos ni datos internos sensibles (en los repos públicos, ni IPs
      ni nombres de hosts internos).
- [ ] Los enlaces y las anclas funcionan.
- [ ] Lo que describe está vigente; lo planeado está marcado como planeado.
