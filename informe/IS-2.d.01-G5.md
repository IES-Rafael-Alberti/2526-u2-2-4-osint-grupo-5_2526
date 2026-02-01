# IS 2.d.02 (a) - Auditoría de Superficie de Exposición Post-Incidente (OSINT pasivo)

- ***Entidad objetivo:*** Clínica de San Rafael de Cádiz
- ***Equipo/Grupo:*** Grupo 5
- ***Integrantes:*** Sergio González Noria (SGN), Iván Paúl Alba (IPA), Manuel Pérez Romero (MPR), Javier Calvillo Acebedo (JCA).
- ***Fecha(s) de investigación:*** [2026-01-28 a 2026-02-01]
- ***Versión:*** 1.0
- ***Límite de entrega (a):*** máximo 6 folios (12 caras) en PDF (si aplica)

## 1. Resumen ejecutivo

**Objetivo.** En este trabajo hemos investigado qué información del Hospital San Rafael de Cádiz está disponible públicamente en Internet y que un posible atacante podría usar para preparar un ataque: datos de empleados, correos, teléfonos, páginas web, documentos públicos, etc.

**Lo que encontramos (principales descubrimientos):**
- Encontramos información personal de 10 empleados en Internet: teléfonos, correos, apodos que usan en redes sociales, etc. Esta información la podría usar alguien para hacerse pasar por otra persona o engañar a los empleados
- Descubrimos 4 servidores que gestionan los nombres de dominio del hospital (dns1, dns2, dns3 y dns4.sered.net), todos en la misma empresa externa
- Vimos que hay varias páginas web relacionadas con el hospital: una para el correo (mail.hospitalespascual.com), otra también para correo (correo.hospitalespascual.com) y una de pruebas (www.test.hospitalespascual.com) que no debería estar visible
- El hospital publica en su web detalles de los equipos médicos que tiene (escáneres, resonancias, etc.), lo que podría ayudar a alguien a saber qué tecnología usan
- También encontramos datos personales como dónde estudiaron algunos empleados, direcciones de sus consultas privadas y números de colegiado

**Nivel de riesgo que vemos:**
- Consideramos que el riesgo es **ALTO** porque hay mucha información personal de los empleados accesible, se puede ver toda la infraestructura de Internet del hospital, y hay una página de pruebas que cualquiera puede encontrar.

**Nuestras recomendaciones más importantes:**
- Quitar o esconder la información personal de los empleados de Internet (teléfonos, correos personales, direcciones)
- Cerrar o proteger la página de pruebas (test.hospitalespascual.com) que no debería ser pública
- Dar formación sobre ciberseguridad a los empleados que tienen más información expuesta
- No publicar tantos detalles técnicos sobre los equipos médicos en la web pública
- Crear unas normas sobre qué información se puede publicar y cuál no

## 2. Alcance, supuestos y reglas de compromiso

**Alcance.**

Se ha realizado únicamente OSINT pasivo sobre la Clínica San Rafael de Cádiz y su huella pública asociada, es decir, toda la información accesible en Internet relacionada con la entidad: dominios y subdominios, registros DNS históricos, certificados, datos de contacto, perfiles públicos de empleados y menciones en la web.  
No se incluye investigación individual (apartado b) ni se ha interactuado con los sistemas de la clínica.

**Fuentes permitidas (usadas en el estudio).**

- Google Search (búsquedas generales y Google Dorks)
- crt.sh (certificados públicos)
- dnsdumpster.com (DNS pasivo e histórico)
- Have I Been Pwned (consulta de correos y dominio en brechas)
- Sherlock (búsqueda de nicks en redes sociales)
- TinEye Reverse Image Search (búsqueda inversa de imágenes)
- Epieos (consultas pasivas de correos y perfiles)  
- PimEyes (búsqueda facial sobre imágenes públicas)  

Todas estas fuentes se consultaron de forma pasiva, utilizando únicamente información ya disponible públicamente y sin generar tráfico hacia los sistemas de la clínica.

**Regla crítica.**

No se realizaron acciones activas: no se hicieron escaneos de puertos, pruebas de login, enumeración directa de servicios ni interacción con formularios o sistemas de la entidad.  
En herramientas que podrían tener funciones activas, solo se usaron los resultados pasivos que la propia plataforma ofrecía (por ejemplo, dnsdumpster y crt.sh).

**Minimización y privacidad.**

- Evitar incluir datos personales innecesarios.
- Si aparecen datos personales de terceros (p. ej., correos de empleados), aplicar reducción: mostrar solo lo imprescindible o enmascarar parcialmente cuando no aporte valor al riesgo.

## 3. Metodología (cómo hicimos la investigación)

Aquí explicamos los pasos que seguimos para hacer nuestra investigación de forma ordenada.

### 3.1 Planificación

- Preguntas que nos hicimos al empezar:
  - ¿Qué páginas web usa el hospital?
  - ¿Podemos encontrar correos electrónicos o patrones de cómo crean los usuarios?
  - ¿Hay documentos públicos que puedan revelar información interna?
  - ¿Se menciona qué tecnologías usan, con qué empresas trabajan o quiénes son los empleados?
  - ¿Ha habido alguna filtración de datos del hospital en el pasado?

- Cómo decidimos qué era importante:
  - Si la información podría usarse para engañar a alguien del hospital
  - Si mostraba patrones que se repiten (como cómo crean las contraseñas o usuarios)
  - Si revelaba detalles de la infraestructura tecnológica del hospital

- Cuándo hicimos la investigación:
  - Realizamos las búsquedas entre el 15 de enero y el 1 de febrero de 2026
  - Todas las capturas de pantalla y pruebas las guardamos en la carpeta `evidencias/`

### 3.2 Fuentes que consultamos

Estas son las herramientas que usamos:

| Tipo de fuente | Herramienta que usamos | Para qué la usamos | Cómo la usamos (sin molestar) |
|-------------|-------------------------------------|-----------------------------|-----------------------------|
| Buscadores  | Google / Bing / DuckDuckGo          | Buscar documentos y menciones del hospital | Búsquedas normales, sin intentar entrar en paneles |
| Páginas antiguas | Wayback Machine                     | Ver cómo era la web antes | Solo lectura de archivos históricos |
| Dominios    | WHOIS (consulta pública)               | Ver quién registró el dominio | Solo consulta pública, no intentamos cambiar nada |
| DNS  | dnsdumpster, crt.sh   | Buscar subdominios y servidores | Consultas pasivas a bases de datos públicas |
| Filtraciones     | Have I Been Pwned         | Ver si hubo filtraciones de datos | Solo consulta, no intentamos usar credenciales |
| Redes sociales        | LinkedIn/Facebook (público)       | Buscar perfiles de empleados | Solo miramos lo que es público |
| Documentos   | Análisis de PDFs públicos | Ver autores y software usado | Solo documentos ya públicos |

### 3.3 Búsquedas que hicimos

- Ejemplos de búsquedas en Google:
  - Buscamos PDFs del hospital
  - Buscamos correos que terminaran en @hospitalespascual.com
  - Buscamos nombres de empleados mencionados públicamente

- Cómo guardamos las pruebas:
  - Hicimos capturas de pantalla y las guardamos con la fecha en la carpeta `evidencias/`
  - Anotamos las URLs y fechas de cada hallazgo
  - Todo lo que mencionamos en el informe tiene su prueba guardada

### 3.4 Cómo organizamos la información

- Ordenamos los datos:
  - Eliminamos duplicados (por ejemplo, si un teléfono aparecía varias veces)
  - Agrupamos por categorías: datos de contacto, identidades, páginas web, documentos

- Cómo verificamos que era fiable:
  - Miramos si la fuente era de confianza
  - Comprobamos si la información era actual o antigua
  - Cuando podíamos, verificamos con al menos 2 fuentes diferentes

### 3.5 Análisis de lo que encontramos

- Conexiones importantes que vimos:
  - Al combinar correos electrónicos, nombres completos y puestos de trabajo que encontramos, alguien podría hacerse pasar por un jefe o directivo del hospital para engañar a empleados de menor rango
  - Documentos públicos revelan nombres de usuarios y programas que usan internamente
  - Páginas web antiguas o de prueba olvidadas podrían tener vulnerabilidades

- Cómo decidimos el nivel de riesgo:
  - **Alto:** cuando la información facilita mucho un ataque o engaño
  - **Medio:** cuando la información es útil para un atacante, pero necesitaría hacer más cosas
  - **Bajo:** información muy general que no aporta mucho

### 3.6 Este informe

- En este documento presentamos lo que encontramos, con pruebas y recomendaciones prácticas
- Intentamos explicarlo de forma clara para que lo entienda cualquiera, tenga conocimientos técnicos o no

## 4. Herramientas utilizadas
<!-- AYUDA (BORRAR): Incluid solo herramientas realmente usadas y una evidencia por cada una (URL o fichero en `evidencias/`). -->

| Herramienta   | Tipo                          | Uso concreto | Salida/evidencia               |
|---------------|-------------------------------|--------------|--------------------------------|
| [Herramienta] | [Buscador/DNS/Metadatos/etc.] | [Para qué]   | [archivo en evidencias/ o URL] |

## 5. Resultados (hallazgos)
<!-- AYUDA (BORRAR): Parte principal. Cada hallazgo debe ser verificable y tener evidencia enlazada (URL y/o `evidencias/...`). -->

Formato recomendado por hallazgo:
<!-- AYUDA (BORRAR): Copiad esta tabla por cada hallazgo importante (o adaptadla si preferís una tabla global). -->

| Campo           | Contenido                                                                  |
|-----------------|----------------------------------------------------------------------------|
| ID              | A-01                                                                       |
| Categoría       | Contacto / Identidad / Dominio-DNS / Documentos-Metadatos / RRSS / Brechas |
| Descripción     | [Qué se encontró, claro y verificable]                                     |
| Evidencia       | [URL] + `evidencias/...`                                                   |
| Fecha evidencia | [YYYY-MM-DD]                                                               |
| Impacto         | [Qué permite a un atacante]                                                |
| Riesgo          | Alto / Medio / Bajo                                                        |
| Recomendación   | [Mitigación concreta]                                                      |

### 5.1 Identidades digitales (nicks, perfiles, cuentas)
<!-- AYUDA (BORRAR): Perfiles corporativos, posibles empleados/roles (solo info pública), y “pivots” para ingeniería social. -->

- A-01
- A-02

### 5.2 Datos de contacto (emails, teléfonos, estructuras)
<!-- AYUDA (BORRAR): Patrones de correo (si se infieren), teléfonos publicados, extensiones, formularios de contacto y riesgos asociados. -->

- A-03
- A-04

### 5.3 Dominios, subdominios y huella DNS (pasivo)
<!-- AYUDA (BORRAR): Dominios oficiales/variantes y subdominios observados en fuentes pasivas/históricas. Evitad enumeración activa. -->

- A-05
- A-06

### 5.4 Huella documental y metadatos (documentos públicos)
<!-- AYUDA (BORRAR): Documentos públicos y metadatos relevantes (autor, software, rutas, fechas). Adjuntad evidencia. -->

- A-07
- A-08

### 5.5 Brechas y filtraciones (consulta pasiva)
<!-- AYUDA (BORRAR): Aparición del dominio/correos en brechas conocidas. No incluyáis contraseñas. Priorizad mitigaciones (2FA, rotación, etc.). -->

- A-09

## 6. Resumen de riesgos
<!-- AYUDA (BORRAR): Tabla para priorizar: qué arreglar primero (P1), después (P2) y al final (P3). -->

| ID   | Hallazgo (resumen) | Riesgo | Prioridad | Acción recomendada |
|------|--------------------|--------|-----------|--------------------|
| A-01 | [..]               | Alto   | P1        | [..]               |
| A-02 | [..]               | Medio  | P2        | [..]               |
| A-03 | [..]               | Bajo   | P3        | [..]               |

## 7. Conclusiones
<!-- AYUDA (BORRAR): 3-6 bullets: qué superficie pública existía y qué vector pudo facilitar. Sin repetir texto, aportad síntesis. -->

- [Conclusión 1: qué explica la exposición encontrada y por qué importa]
- [Conclusión 2]
- [Conclusión 3]

## 8. Recomendaciones
<!-- AYUDA (BORRAR): Convertid hallazgos en acciones concretas. Si podéis, asignad responsable sugerido (IT/Seguridad/RRHH/Comunicacion). -->

**Quick wins (0-30 días)**
<!-- AYUDA (BORRAR): Cambios rápidos: retirar/editar documentos, sanear metadatos, ajustar contenidos públicos, concienciación inmediata. -->
- [..]
- [..]

**Medio plazo (1-3 meses)**
<!-- AYUDA (BORRAR): Cambios estructurales: políticas de publicación, revisión periódica, procesos, formación, controles de identidad. -->
- [..]

**Mejora continua**
<!-- AYUDA (BORRAR): Medidas recurrentes: monitorización de menciones, revisiones trimestrales de exposición, playbook OSINT. -->
- [..]

## 9. Anexos
<!-- AYUDA (BORRAR): Trazabilidad. Esta sección facilita la corrección: fuentes, consultas y evidencias enlazadas. -->

### 9.1 Registro de fuentes
<!-- AYUDA (BORRAR): Fuentes base consultadas (URL + fecha). No hace falta duplicar cada evidencia si ya está en hallazgos, pero sí lo principal. -->

| Fuente   | URL  | Fecha acceso | Nota |
|----------|------|--------------|------|
| [Fuente] | [..] | [YYYY-MM-DD] | [..] |

### 9.2 Consultas (dorks) empleadas
<!-- AYUDA (BORRAR): Dejad 5-15 consultas representativas. Deben ser pasivas y reproducibles. -->

(Registrar aquí las consultas utilizadas. Evitar incluir acciones activas o instrucciones de acceso.)

- `site:[dominio] filetype:pdf [palabra clave]`
- `site:[dominio] "@[dominio]"`
- `"Clínica San Rafael" "Cádiz" [palabra clave]`

### 9.3 Evidencias (índice)
<!-- AYUDA (BORRAR): Índice con enlaces relativos a ficheros dentro de `evidencias/`. Debe permitir abrir cada evidencia sin buscar. -->

<!-- AYUDA (BORRAR): Ejemplo de enlace: `[2026-01-27 - Google - PDF organigrama](../evidencias/2026-01-27_google_organigrama.pdf)` -->

- `evidencias/`:
  - `YYYY-MM-DD_fuente_tema.ext` - [descripción]
