---
created: 2025-03-25T13:15
updated: 2025-05-29T18:18
---
# Reconocimiento Web

## Recursos web

- [Pentest-Tools – Google Hacking](https://pentest-tools.com/information-gathering/google-hacking)  
- [Exploit-DB – Google Hacking Database](https://www.exploit-db.com/google-hacking-database)

| Google Dork                                                        | Descripción                                                 |
| ------------------------------------------------------------------ | ----------------------------------------------------------- |
| `site:example.com`                                                 | Busca todo el contenido indexado en el dominio.            |
| `filetype:pdf site:example.com`                                    | Busca archivos PDF en el dominio.                          |
| `intitle:"index of" site:example.com`                              | Busca directorios indexados en el dominio.                 |
| `inurl:admin site:example.com`                                     | Busca URLs que contengan “admin” en el dominio.            |
| `intext:"password" site:example.com`                               | Busca páginas que contengan la palabra “password”.         |
| `filetype:xls OR filetype:xlsx site:example.com`                   | Busca hojas de cálculo Excel en el dominio.                |
| `inurl:login site:example.com`                                     | Busca páginas de inicio de sesión en el dominio.           |
| `filetype:log intext:"error" site:example.com`                     | Busca archivos de registro que contengan la palabra “error”. |
| `inurl:"phpinfo.php" site:example.com`                             | Busca páginas que revelen información PHP del servidor.    |
| `site:example.com intext:"@example.com"`                           | Busca direcciones de correo electrónico en el dominio.     |
| `filetype:doc OR filetype:docx site:example.com`                   | Busca documentos de Word en el dominio.                    |
| `inurl:"/config" site:example.com`                                 | Busca archivos de configuración en el dominio.             |
| `filetype:env "DB_PASSWORD" site:example.com`                      | Busca archivos .env que contengan contraseñas de bases de datos. |
| `inurl:"/cgi-bin/" site:example.com`                               | Busca directorios CGI-BIN en el dominio.                   |
| `intitle:"index of" "backup" site:example.com`                     | Busca directorios que contengan copias de seguridad.       |
| `inurl:"wp-content/uploads" site:example.com`                      | Busca archivos subidos en instalaciones de WordPress.      |
| `site:example.com intext:"phone" OR intext:"contact" OR intext:"tel"` | Busca números de teléfono en el dominio.                |
| `inurl:wp-content/plugins/ site:example.com`                       | Busca plugins de WordPress en el dominio.                  |
| `inurl:wp-admin/ OR inurl:wp-login.php site:example.com`           | Busca paneles de administración de WordPress.              |
| `inurl:readme.html site:example.com`                               | Busca versiones de CMS u otros servicios.                  |
| `inurl:dashboard site:example.com`                                 | Busca paneles de administración en general.                |

::: quote
#### Más ejemplos de Google Dorks

- **Encontrar páginas de inicio de sesión**  
  - `site:example.com inurl:login`  
  - `site:example.com (inurl:login OR inurl:admin)`

- **Identificación de archivos expuestos**  
  - `site:example.com filetype:pdf`  
  - `site:example.com (filetype:xls OR filetype:docx)`

- **Descubrimiento de archivos de configuración**  
  - `site:example.com inurl:config.php`  
  - `site:example.com (ext:conf OR ext:cnf)`

- **Localización de copias de seguridad de bases de datos**  
  - `site:example.com inurl:backup`  
  - `site:example.com filetype:sql`
:::

---

## Archivos web

::: note
En el acelerado mundo digital, los sitios web van y vienen, dejando sólo rastros fugaces de su existencia. Gracias a [Wayback Machine de Internet Archive](https://web.archive.org/), podemos volver a visitar el pasado y explorar las huellas digitales de los sitios web tal como fueron.
:::

### ¿Qué es la Wayback Machine?

![Wayback Machine](https://academy.hackthebox.com/storage/modules/144/wayback.png)

La **Wayback Machine** es un archivo digital de sitios web creado por Internet Archive en 1996. Permite ver versiones pasadas de páginas web capturando instantáneas mediante rastreadores web y almacenando contenido y recursos (HTML, CSS, imágenes, etc.). Los usuarios acceden ingresando la URL y seleccionando una fecha.

Es valiosa para el **reconocimiento web** porque permite:

- Descubrir activos ocultos o vulnerabilidades en versiones anteriores de un sitio.  
- Rastrear cambios y patrones en la evolución de la página.  
- Recopilar inteligencia mediante contenido archivado.  
- Realizar reconocimiento pasivo sin interactuar con la infraestructura del sitio.  

---

## Automatización del reconocimiento

::: info
La automatización de las tareas de reconocimiento web mejora la eficiencia y precisión, permitiendo recopilar información a escala e identificar vulnerabilidades potenciales más rápidamente.
:::

Entre las herramientas más populares:

- **FinalRecon**: Framework modular en Python para verificación de certificados SSL, búsquedas Whois, análisis de encabezados y más.  
- **Recon-ng**: Framework en Python con módulos para DNS, subdominios, escaneo de puertos y explotación de vulnerabilidades.  
- **theHarvester**: Recopila correos electrónicos y subdominios de fuentes públicas (motores de búsqueda, SHODAN).  
- **SpiderFoot**: Plataforma de inteligencia OSINT que integra múltiples fuentes (DNS, rastreo web, escaneo de puertos).  
- **OSINT Framework**: Colección de herramientas y recursos para inteligencia de código abierto (redes sociales, registros públicos).

### FinalRecon

::: quote
- **Encabezados HTTP**: Detalles del servidor, tecnologías y posibles errores de configuración.  
- **Whois**: Información de registro del dominio (registrante, datos de contacto).  
- **SSL/TLS**: Verifica validez y emisor del certificado.  
- **Crawlers**  
  - HTML, CSS, JavaScript: Extracción de enlaces y búsqueda de vulnerabilidades.  
  - Enlaces internos/externos: Mapeo de la estructura del sitio.  
  - Imágenes, `robots.txt`, `sitemap.xml`: Rutas de rastreo.  
  - Enlaces en JavaScript y Wayback Machine: Descubrimiento de enlaces ocultos e históricos.  
- **DNS**: Más de 40 tipos de registros, incluyendo DMARC.  
- **Subdominios**: Descubrimiento mediante múltiples fuentes.  
- **Directorios**: Listas personalizadas para encontrar rutas ocultas.  
- **Wayback Machine**: Recuperación de URL de los últimos cinco años.  
:::

```bash
git clone https://github.com/thewhiteh4t/FinalRecon.git
cd FinalRecon
pip3 install -r requirements.txt
chmod +x finalrecon.py
```

| Opción         | Argumento | Descripción                                  |
| -------------- | --------- | -------------------------------------------- |
| `-h`, `--help` |           | Muestra la ayuda y sale.                     |
| `--url`        | URL       | URL de destino.                              |
| `--headers`    |           | Recupera información de encabezados HTTP.    |
| `--sslinfo`    |           | Obtiene información del certificado SSL/TLS. |
| `--whois`      |           | Búsqueda Whois del dominio.                  |
| `--crawl`      |           | Rastrea el sitio web.                        |
| `--dns`        |           | Enumeración de DNS.                          |
| `--sub`        |           | Descubre subdominios.                        |
| `--dir`        |           | Busca directorios ocultos.                   |
| `--wayback`    |           | Recupera URL archivadas en Wayback Machine.  |
| `--ps`         |           | Escaneo rápido de puertos.                   |
| `--full`       |           | Escaneo completo de reconocimiento.          |
