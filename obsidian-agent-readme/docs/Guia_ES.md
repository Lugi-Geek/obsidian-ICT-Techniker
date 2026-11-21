# Obsidian-Agent – Guía de uso

Obsidian-Agent es una interfaz web local para la **gestión de proyectos en Obsidian**. Proyectos, tareas, actas, decisiones, riesgos, reuniones periódicas y el equipo se guardan como archivos Markdown normales en su bóveda de Obsidian. Una pequeña base de datos solo sirve de índice y agenda diaria, y se reconstruye a partir de la bóveda en cualquier momento.

- Funciona solo en su ordenador: `http://127.0.0.1:5055`. No se envía ningún dato a Internet.
- Puede trabajar siempre directamente en Obsidian. El agente vuelve a leerlo todo en la siguiente sincronización.
- Interfaz, plantillas y nombres de carpeta en alemán, inglés, francés, italiano, español y rumano.

## 1. Instalación

### Windows

1. Haga doble clic en `Obsidian-Agent-Setup-2.0.0.exe`. No se necesitan derechos de administrador.
2. Si aparece «Windows protegió su PC», haga clic en **Más información → Ejecutar de todas formas**. El instalador no está firmado con un certificado de pago.
3. Elija el idioma y siga el instalador.
4. A continuación, el instalador configura automáticamente:
   - **Python**, si falta (mediante winget o, si no, directamente desde python.org),
   - su **bóveda** (diálogo de carpeta, quizá detrás de la ventana),
   - el **inicio automático** en segundo plano en cada inicio de sesión y la **sincronización diaria**,
   - accesos directos en el **menú Inicio** y en el **escritorio**.
5. El navegador se abre con el agente.

Carpeta del programa: `%LOCALAPPDATA%\Programs\Obsidian-Agent` · Ajustes y base de datos: `%LOCALAPPDATA%\Obsidian-Agent`

### macOS

1. Haga doble clic en `Obsidian-Agent-2.0.0.pkg`.
2. Si macOS indica que no se puede verificar el paquete, elija **Ajustes del Sistema → Privacidad y seguridad → Abrir igualmente** (versiones anteriores: clic derecho en el paquete → Abrir). El paquete no está firmado con un certificado de desarrollador de Apple.
3. Siga el instalador e introduzca la contraseña de administrador.
4. Tras la copia, el paquete configura automáticamente: Python (desde python.org, si falta), el idioma de su Mac, su bóveda (diálogo de carpeta), el inicio automático y la sincronización diaria.
5. Después abra el agente desde **Aplicaciones → Obsidian-Agent**.

Si la bóveda está en *Documentos*, en el *Escritorio* o en *iCloud Drive*, macOS puede bloquear la sincronización en segundo plano. El paquete lo detecta y muestra el archivo que debe añadir en **Ajustes del Sistema → Privacidad y seguridad → Acceso total al disco**.

Programa: `/Applications/Obsidian-Agent` · Ajustes y base de datos: `~/Library/Application Support/Obsidian-Agent` · Registro de instalación: `/tmp/obsidian-agent-install.log`

### Sin instalación (todos los sistemas)

Basta con Python 3.9 o posterior. Descomprima la carpeta `obsidian-agent` y ejecute `start.bat` (Windows) o `start.sh` (macOS/Linux). Flask ya está incluido. Los ajustes se guardan entonces en la carpeta del programa. Para la sincronización diaria en Linux, añada `0 4 * * * cd /ruta/obsidian-agent && python3 agent.py sync --geplant` con `crontab -e`.

## 2. Primeros pasos

1. **Ajustes**: compruebe la ruta de la bóveda y elija el idioma.
2. **Equipo**: registre a los miembros con nombre e iniciales.
3. **Proyectos**: cree el primer proyecto. Se crea la estructura de carpetas de abajo.
4. Cree **tareas** y documentos del proyecto en **Documentos**.
5. Para reuniones regulares, cree una serie de **Reuniones periódicas**.

## 3. Áreas de la interfaz

| Área | Finalidad |
|---|---|
| **Hoy** | Tareas de hoy y vencidas, próximos vencimientos, notas modificadas recientemente, nueva tarea. |
| **Tareas** | Todas las tareas por grupos, filtro por proyecto, completar con un clic, cambiar el estado, mover «+1 día». |
| **Proyectos** | Crear proyectos con estructura fija, completar proyectos incompletos. |
| **Documentos** | Documentos del proyecto a partir de plantillas, guardados automáticamente en la carpeta adecuada. |
| **Desde plantilla** | Nueva nota a partir de cualquier plantilla de la carpeta de plantillas, también de las propias. |
| **Reuniones periódicas** | Series de reuniones con frecuencia, notas de reunión y acciones. Cada reunión nueva incluye las acciones abiertas. |
| **Equipo** | Fichas con rol, contacto, suplente y las tareas abiertas de cada persona. |
| **Búsqueda** | Búsqueda de texto completo en toda la bóveda. |
| **Ajustes** | Idioma, ruta de la bóveda, nombres de carpeta, hora de sincronización, registro. |

Cada título es un enlace `obsidian://` que abre la nota directamente en Obsidian.

## 4. Carpetas de la bóveda

| Carpeta | Contenido |
|---|---|
| `Proyectos/` | Una subcarpeta por proyecto (estructura abajo) |
| `Tareas/` | Tareas sin proyecto |
| `Notas/` | Documentos sin proyecto |
| `_Plantillas/` | Plantillas, editables en Obsidian |
| `Agenda/` | Resumen del día y archivo (automático) |
| `Equipo/` | Una nota por miembro del equipo |
| `Reuniones/` | Una subcarpeta por serie con reuniones y acciones |

## 5. Estructura del proyecto

Cada proyecto recibe una nota de resumen `_Proyecto_<Nombre>.md` (objetivos, hitos, tareas abiertas) y estas subcarpetas, cada una con un archivo `readme`:

| Carpeta | Contenido |
|---|---|
| `01_Encargo_y_Contratos/` | Encargo del proyecto, ofertas, contratos, pedidos y anexos. |
| `02_Partes_interesadas/` | Patrocinador, contactos, roles, escalado y comunicación. |
| `03_Planificacion/` | Plan del proyecto, hitos, recursos, presupuesto y decisiones. |
| `04_Ejecucion/` | Entregables, conceptos, documentación técnica y pruebas. |
| `05_Riesgos_y_Cambios/` | Riesgos, puntos abiertos y solicitudes de cambio. |
| `06_Informes/` | Informes de estado, indicadores y comité de dirección. |
| `07_Actas/` | Actas de reuniones, reuniones periódicas y correspondencia importante. |
| `08_Cierre/` | Aceptación, traspaso a operaciones y lecciones aprendidas. |

«Completar todos los proyectos» añade las carpetas que faltan a los proyectos existentes. Nunca se sobrescribe nada.

## 6. Documentos del proyecto

| Documento | Carpeta | Nombre de archivo |
|---|---|---|
| **Acta de reunión** | `07_Actas/` | `YYYY-MM-DD_Acta_….md` |
| **Decisión** | `03_Planificacion/` | `Decision_YYYY-MM-DD_….md` |
| **Riesgo** | `05_Riesgos_y_Cambios/` | `Riesgo_….md` |
| **Solicitud de cambio** | `05_Riesgos_y_Cambios/` | `Cambio_YYYY-MM-DD_….md` |
| **Parte interesada / contacto** | `02_Partes_interesadas/` | `Parte_interesada_….md` |
| **Informe de estado** | `06_Informes/` | `Informe_YYYY-MM_….md` |
| **Cierre del proyecto** | `08_Cierre/` | `Cierre_….md` |

Cree también una tarea para cada acción de un acta, para que aparezca en Hoy y en el equipo.

## 7. Formato de las tareas

```markdown
---
typ: task
titel: Preparar el kick-off
projekt: Migración M365
start: 2026-11-18
ende: 2026-11-20
status: offen            # offen | in_arbeit | wartend | erledigt
prioritaet: hoch         # hoch | mittel | niedrig
verantwortlich: AM       # nombre o iniciales de un miembro del equipo
---
- [ ] Paso 1
- [x] Paso 2
```

- **Hoy**: inicio ≤ hoy ≤ fin · **Vencida**: fin < hoy · **Planificada**: inicio > hoy.
- Si falta `status`, una tarea se considera completada cuando todas las casillas están marcadas.
- Los nombres de los campos del frontmatter (`typ`, `titel`, `ende` = fin, `verantwortlich` = responsable …) son iguales en todos los idiomas. Así el agente puede leer cualquier bóveda, incluso después de cambiar de idioma.

## 8. Resumen del día y sincronización

Cada día a las 04:00 (configurable) el agente lee todas las notas y escribe el resumen del día en `Agenda/Hoy.md`, además de un archivo por día. Así también ve el resumen en Obsidian y en el móvil. Si el ordenador estaba apagado, la ejecución se recupera. «Actualizar ahora» lee la bóveda al instante.

## 9. Cambiar el idioma

Abajo a la izquierda en la navegación o en **Ajustes**. La interfaz cambia al instante. Las nuevas plantillas se crean en el idioma elegido. En una bóveda sin proyectos también se adaptan los nombres de carpeta y la estructura del proyecto. Las carpetas y notas existentes nunca se renombran.

## 10. Adaptar las plantillas

Todas las plantillas están en la carpeta de plantillas de la bóveda y se pueden editar en Obsidian. Marcadores: `{{title}}`, `{{date}}`, `{{projekt}}`. Con `zielordner: 03_…` en el frontmatter de una plantilla propia define la carpeta preseleccionada. Las plantillas estándar eliminadas se vuelven a crear en la siguiente sincronización.

## 11. Opcional: Dataview

Los resúmenes de proyecto incluyen una consulta Dataview de las tareas abiertas. Para ello, active en Obsidian el plugin de la comunidad **Dataview**. El agente en sí no lo necesita.

## 12. Actualización, copia de seguridad, desinstalación

- **Actualización**: instale simplemente el nuevo instalador o paquete. Los ajustes y la base de datos se conservan.
- **Copia de seguridad**: la bóveda es la fuente de verdad. La base de datos solo añade el historial diario.
- **Desinstalación en Windows**: *Configuración → Aplicaciones → Obsidian-Agent → Desinstalar*.
- **Desinstalación en macOS**: *Aplicaciones → Obsidian-Agent → Desinstalar Obsidian-Agent*.
- Ambas guardan `config.json` y `planer.db` en una carpeta `obsidian-agent-backup_<fecha>` en el escritorio. **Su bóveda de Obsidian nunca se modifica ni se elimina.**

## 13. Solución de problemas

| Problema | Solución |
|---|---|
| El navegador muestra «no se puede acceder al sitio» | Abra el agente desde el menú Inicio / Aplicaciones. Registro: `logs/gui.log` en la carpeta de ajustes. |
| Faltan notas nuevas en la interfaz | Haga clic en «Actualizar ahora». Compruebe el nombre de archivo `Task_…` o el campo `typ:`. |
| Una tarea no aparece en un miembro del equipo | Use en el campo `verantwortlich` el nombre completo o las iniciales del equipo. |
| macOS: falla la sincronización en segundo plano | Permita el acceso total al disco para el archivo de Python indicado (véase instalación). |
| El puerto 5055 está ocupado | Cambie `port` en `config.json` y reinicie el agente. |

Línea de comandos: `python agent.py sync` · `python agent.py heute` (hoy) · `python agent.py projekt "Nombre"` · `python agent.py info`

---
[Deutsch](Anleitung_DE.md) · [English](Guide_EN.md) · [Français](Guide_FR.md) · [Italiano](Guida_IT.md) · [Română](Ghid_RO.md)
