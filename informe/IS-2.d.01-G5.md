# IS 2.d.02 (a) - Auditoría de Superficie de Exposición Post-Incidente (OSINT pasivo)

- ***Entidad objetivo:*** Clínica de San Rafael de Cádiz
- ***Equipo/Grupo:*** Grupo 5
- ***Integrantes:*** Sergio González Noria (SGN), Iván Paúl Alba (IPA), Manuel Pérez Romero (MPR), Javier Calvillo Acebedo (JCA).
- ***Fecha(s) de investigación:*** 2026-01-28 a 2026-02-01
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
  - Encontrar correos + nombres + puestos de trabajo = alguien podría hacerse pasar por un jefe para engañar a empleados
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

| Herramienta   | Tipo                          | Uso concreto                                           | Salida/evidencia                                   |
|---------------|-------------------------------|-------------------------------------------------------|---------------------------------------------------|
| Google Search | Buscador                      | Búsqueda de dominios, subdominios, PDFs y menciones | - |
| crt.sh        | Certificados SSL              | Comprobación de certificados asociados a dominios    | `evidencias/crtsh_hospitalespascual.png`         |
| dnsdumpster.com | DNS pasivo                   | Identificación de subdominios y registros históricos| `evidencias/dnsdumpster_hospitalespascual.png`  |
| Have I Been Pwned | Brechas de datos           | Verificación de emails y dominios en leaks          | -          |
| Sherlock      | Redes sociales / Identidad     | Búsqueda de nicks y alias de empleados              | -                  |
| TinEye        | Búsqueda inversa de imágenes  | Verificación de fotos públicas de empleados         | -                   |
| Epieos        | Correo / perfiles             | Consulta pasiva de correos y perfiles vinculados    | -                |
| PimEyes       | Reconocimiento facial         | Verificación de imágenes públicas de empleados      | -                  |
| SpiderFoot    | OSINT automatizado            | Análisis de superficie digital, dominios, subdominios, certificados y hosting | `evidencias/SpiderFoot_HospitalSanRafael.csv`   |


## 5. Resultados (lo que encontramos)

A continuación detallamos cada descubrimiento importante que hicimos, con pruebas de dónde lo vimos y por qué creemos que es peligroso.

### 5.1 Identidades de empleados (apodos, perfiles, cuentas)

**A-01: Dra. Ana De Lacour Juliá**
- **Categoría:** Identidad
- **Qué encontramos:** Apodo en redes "anuskalaq", trabaja en Neurología, número de colegiado: 111107282
- **Dónde lo vimos:** Perfiles públicos profesionales
- **Cuándo:** 20 de enero de 2026
- **Por qué es peligroso:** Alguien podría hacerse pasar por ella usando esta información para engañar a otros empleados
- **Nivel de riesgo:** Alto
- **Qué recomendamos:** Darle formación sobre cómo detectar intentos de engaño y activar la verificación en dos pasos en sus cuentas

**A-02: Ignacio Ortiz Acero**
- **Categoría:** Identidad
- **Qué encontramos:** Es el Director Médico, apodo "sinueioa", número de colegiado: 111105853. Le gusta mucho la Semana Santa, estudió en la Universidad de Cádiz y en Salesianos. Incluso tiene un premio de una hermandad
- **Dónde lo vimos:** Redes sociales y noticias locales
- **Cuándo:** 20 de enero de 2026
- **Por qué es peligroso:** Es un cargo importante y hay MUCHA información personal sobre él. Alguien podría usar sus aficiones para ganarse su confianza y engañarle (por ejemplo, hablándole de Semana Santa)
- **Nivel de riesgo:** Alto
- **Qué recomendamos:** Avisarle específicamente de que tenga cuidado con contactos que mencionen sus aficiones personales, podrían estar intentando manipularle

**A-03: Sandra Brenes Reyes**
- **Categoría:** Identidad
- **Qué encontramos:** Psicóloga del hospital, número de colegiado AN08392. Tiene un Gmail personal (psicologasandrabrenes@gmail.com), teléfono móvil (693406050), dirección de su consulta (Avenida Buenavista 29, Vejer de la Frontera) y web personal propia
- **Dónde lo vimos:** Su página web personal y directorios de psicólogos
- **Cuándo:** 22 de enero de 2026
- **Por qué es peligroso:** Su correo personal y teléfono están totalmente expuestos. Alguien puede contactarla directamente haciéndose pasar por un paciente o colega
- **Nivel de riesgo:** Alto
- **Qué recomendamos:** Que use solo el correo y teléfono del hospital para temas de trabajo, y proteja mejor sus datos personales

**A-04: Antonio Linares Moreno**
- **Categoría:** Identidad
- **Descripción:** Oncología Radioterápica, Nick "Tony Sugar" en luchawike.org, Núm. Colegiado: 111807100
- **Evidencia:** Perfiles en foros temáticos
- **Fecha evidencia:** 2026-01-25
- **Impacto:** Nick en foros permite rastreo de actividad online y construcción de perfil personal
- **Riesgo:** Medio
- **Recomendación:** Concienciación sobre separación de identidades personal/profesional

**A-05: Guido Weisman**
- **Categoría:** Identidad
- **Descripción:** Medicina Interna, Nicks "batataweis" y "gugaweis", Fellowship
- **Evidencia:** Perfiles públicos en redes sociales
- **Fecha evidencia:** 2026-01-25
- **Impacto:** Múltiples nicks facilitan rastreo de actividad en diferentes plataformas
- **Riesgo:** Medio
- **Qué recomendamos:** Revisar qué información tienen publicada en redes sociales y auditar su presencia online

**A-06: Otros empleados que encontramos**
- Camila Raduan Tozzini (Ginecología, Núm. Colegiado: 080865499)
- Zulika Riveros (Podología, Tel: 956252624, Dirección: Avenida Padre de las Casas nº 4, Local 14, Cádiz)
- Juan Manuel Fariñas Varo (Urología, encontramos varias direcciones de sus consultorios)
- María Súnico Rodríguez (Psicología, Núm. Colegiado: AN06945, correo de la universidad: maria.sunico@uca.es)
- Jorge Ortega García (Medicina Interna)
- Manuel Casanova Ramón (Medicina Interna)

### 5.2 Datos de contacto (correos y teléfonos)

**A-07: Muchos teléfonos de empleados publicados**
- **Categoría:** Contacto
- **Qué encontramos:** Varios números de teléfono directos:
  - 956017270 y 956048000 (Dra. Ana De Lacour Juliá)
  - 693406050 (Sandra Brenes Reyes - su móvil personal)
  - 956252624 (Zulika Riveros)
- **Dónde lo vimos:** Directorios de médicos y páginas web públicas
- **Cuándo:** 20 de enero de 2026
- **Por qué es peligroso:** Alguien puede llamar directamente a estos empleados haciéndose pasar por un paciente, familiar o compañero para engañarles por teléfono
- **Nivel de riesgo:** Alto
- **Qué recomendamos:** Que todas las llamadas pasen por la centralita del hospital, no publicar teléfonos directos de empleados

**A-08: Correos electrónicos de empleados**
- **Categoría:** Contacto
- **Qué encontramos:** Correos que usan para trabajo:
  - psicologasandrabrenes@gmail.com (Sandra Brenes - ¡su Gmail personal!)
  - maria.sunico@uca.es (María Súnico - correo de la universidad, no del hospital)
- **Dónde lo vimos:** Páginas web personales y directorios de universidades
- **Cuándo:** 22 de enero de 2026
- **Por qué es peligroso:** Usan cuentas personales o de otras instituciones en lugar del correo del hospital. El hospital no puede proteger esas cuentas y es más fácil engañarles
- **Nivel de riesgo:** Alto
- **Qué recomendamos:** Crear una norma para que TODOS usen solo correos del hospital (@hospitalespascual.com) para temas de trabajo

### 5.3 Páginas web y servidores del hospital

**A-09: Página web principal**
- **Categoría:** Páginas web
- **Qué encontramos:** 
  - Página principal: hospitalespascual.com
  - También se menciona como: hospital-san-rafael
- **Dónde lo vimos:** Consultas WHOIS (registro de dominios) y búsquedas en Google
- **Cuándo:** 18 de enero de 2026
- **Por qué es peligroso:** Solo tienen una página. No han registrado páginas parecidas, así que alguien podría comprar "hospitalpascual.com" o similar para engañar a la gente
- **Nivel de riesgo:** Medio
- **Recomendación:** Registrar variantes comunes del dominio para prevenir typosquatting

**A-10: Páginas web adicionales encontradas**
- **Categoría:** Páginas web
- **Qué encontramos:** Varias páginas relacionadas con el hospital:
  - mail.hospitalespascual.com (para el correo electrónico)
  - correo.hospitalespascual.com (otra también para correo)
  - www.test.hospitalespascual.com (¡una página de PRUEBAS que está visible!)
  - hospitalespascual.com.josemanuelpascualpascual.es (página en el dominio de otra persona)
- **Dónde lo vimos:** En crt.sh (base de datos de certificados) y dnsdumpster.com
- **Cuándo:** 18 de enero de 2026
- **Por qué es peligroso:** La página de pruebas NO debería ser pública, puede tener vulnerabilidades o información de desarrollo. La página en dominio ajeno es extraña y podría usarse para confundir a la gente
- **Nivel de riesgo:** Alto
- **Qué recomendamos:** Cerrar o proteger urgentemente la página de pruebas. Revisar qué es esa página en el dominio de josemanuelpascualpascual.es

**A-11: Servidores que gestionan la página web**
- **Categoría:** Páginas web
- **Qué encontramos:** El hospital usa 4 servidores de una empresa llamada Sered (en España):
  - dns1.sered.net (185.37.231.10)
  - dns2.sered.net (46.175.128.146)
  - dns3.sered.net (193.84.177.223)
  - dns4.sered.net (193.84.177.125)
- **Dónde lo vimos:** Consultas públicas de DNS y registros históricos
- **Cuándo:** 18 de enero de 2026
- **Por qué es peligroso:** Cualquiera puede ver quién les da el servicio y las direcciones IP. Esto es normal en Internet, pero hay que asegurarse de que estén bien configurados
- **Nivel de riesgo:** Medio
- **Qué recomendamos:** Mejorar la seguridad de estos servidores (activar DNSSEC y limitar consultas)

### 5.4 Documentos e información publicada

**A-12: Información sobre equipos médicos**
- **Categoría:** Información pública
- **Qué encontramos:** En la web del hospital hay mucha información detallada sobre los equipos que tienen:
  - TAC (escáneres) con detalles técnicos
  - Máquinas de Resonancia Magnética de última generación
  - Equipos de Endoscopia (cámaras flexibles para mirar por dentro)
  - Ecógrafos modernos
  - Máquinas de Rayos X de alta calidad
  - Equipos de laboratorio automatizados (para analizar sangre, orina, genes, etc.)
- **Dónde lo vimos:** Página web oficial del hospital
- **Cuándo:** 28 de enero de 2026
- **Por qué es peligroso:** Si publican qué modelos exactos tienen, alguien puede buscar si esos modelos tienen fallos de seguridad conocidos
- **Nivel de riesgo:** Medio
- **Qué recomendamos:** Hablar de forma general sobre "equipos modernos" sin dar detalles técnicos específicos

**A-13: Direcciones de consultorios**
- **Categoría:** Información pública
- **Qué encontramos:** Direcciones exactas de consultas privadas:
  - C/ Feduchy, 8, Cádiz (Juan Manuel Fariñas Varo - varias consultas en esta misma calle)
  - Avenida Padre de las Casas nº 4, Local 14, Cádiz (Zulika Riveros)
  - Avenida Buenavista, 29, Centro de Negocios Horizonte, Despacho 11, Vejer de la Frontera (Sandra Brenes)
- **Dónde lo vimos:** Directorios médicos y páginas web personales
- **Cuándo:** 25 de enero de 2026
- **Por qué es peligroso:** Con estas direcciones, alguien podría presentarse en persona haciéndose pasar por paciente o hacer engaños más elaborados
- **Nivel de riesgo:** Medio
- **Qué recomendamos:** Valorar si es necesario publicar direcciones tan específicas de consultas privadas asociadas al hospital

### 5.5 Filtraciones de datos (brechas de seguridad)

**A-14: Consulta de filtraciones pasadas**
- **Categoría:** Filtraciones
- **Qué encontramos:** 
  - Sandra Brenes Reyes (psicologasandrabrenes@gmail.com): NO aparece en filtraciones conocidas
  - María Súnico Rodríguez (maria.sunico@uca.es): No pudimos verificar
  - Correos @hospitalespascual.com: NO encontramos que se hayan filtrado contraseñas en el pasado
- **Dónde lo vimos:** Bases de datos públicas de filtraciones (Have I Been Pwned)
- **Cuándo:** 30 de enero de 2026
- **Por qué es buena noticia:** No hay contraseñas del hospital filtradas en Internet (que sepamos)
- **Nivel de riesgo:** Bajo (de momento)
- **Qué recomendamos:** Activar un sistema que avise automáticamente si aparecen correos del hospital en futuras filtraciones. Poner verificación en dos pasos obligatoria para todos

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
