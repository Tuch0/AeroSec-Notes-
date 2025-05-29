
#### Recursos web
- [Pentest-Tools](https://pentest-tools.com/information-gathering/google-hacking)
- [Exploit-DB](https://www.exploit-db.com/google-hacking-database)

| **Google Dork**                                                       | **Descripción**                                                  |
| --------------------------------------------------------------------- | ---------------------------------------------------------------- |
| `site:example.com`                                                    | Busca todo el contenido indexado en el dominio.                  |
| `filetype:pdf site:example.com`                                       | Busca archivos PDF en el dominio.                                |
| `intitle:"index of" site:example.com`                                 | Busca directorios indexados en el dominio.                       |
| `inurl:admin site:example.com`                                        | Busca URLs que contengan "admin" en el dominio.                  |
| `intext:"password" site:example.com`                                  | Busca páginas que contengan la palabra "password".               |
| `filetype:xls OR filetype:xlsx site:example.com`                      | Busca hojas de cálculo Excel en el dominio.                      |
| `inurl:login site:example.com`                                        | Busca páginas de inicio de sesión en el dominio.                 |
| `filetype:log intext:"error" site:example.com`                        | Busca archivos de registro que contengan la palabra "error".     |
| `inurl:"phpinfo.php" site:example.com`                                | Busca páginas que revelen información PHP del servidor.          |
| `site:example.com intext:"@example.com"`                              | Busca direcciones de correo electrónico en el dominio.           |
| `filetype:doc OR filetype:docx site:example.com`                      | Busca documentos de Word en el dominio.                          |
| `inurl:"/config" site:example.com`                                    | Busca archivos de configuración en el dominio.                   |
| `filetype:env "DB_PASSWORD" site:example.com`                         | Busca archivos .env que contengan contraseñas de bases de datos. |
| `inurl:"/cgi-bin/" site:example.com`                                  | Busca directorios CGI-BIN en el dominio.                         |
| `intitle:"index of" "backup" site:example.com`                        | Busca directorios que contengan copias de seguridad.             |
| `inurl:"wp-content/uploads" site:example.com`                         | Busca archivos subidos en instalaciones de WordPress.            |
| `site:example.com intext:"phone" OR intext:"contact" OR intext:"tel"` | Busca números de teléfono en el dominio.                         |
| `inurl:wp-content/plugins/ site:example.com`                          | Busca plugins de WordPress en el dominio.                        |
| `inurl:wp-admin/ OR inurl:wp-login.php site:example.com`              | Busca paneles de administración de WordPress.                    |
| `inurl:readme.html site:example.com`                                  | Busca versiones de CMS u otros servicios.                        |
| `inurl:dashboard site:example.com`                                    | Busca paneles de administración en general.                      |
```ad-quote
- Encontrar páginas de inicio de sesión:
    - `site:example.com inurl:login`
    - `site:example.com (inurl:login OR inurl:admin)`
- Identificación de archivos expuestos:
    - `site:example.com filetype:pdf`
    - `site:example.com (filetype:xls OR filetype:docx)`
- Descubriendo archivos de configuración:
    - `site:example.com inurl:config.php`
    - `site:example.com (ext:conf OR ext:cnf)` (busca extensiones comúnmente utilizadas para archivos de configuración)
- Localización de copias de seguridad de bases de datos:
    - `site:example.com inurl:backup`
    - `site:example.com filetype:sql`
```

---

# Web Archives

```ad-note
En el acelerado mundo digital, los sitios web van y vienen, dejando sólo rastros fugaces de su existencia. Sin embargo, gracias a [Wayback Machine de Internet Archive](https://web.archive.org/) , tenemos una oportunidad única de volver a visitar el pasado y explorar las huellas digitales de los sitios web tal como fueron.
```

## ¿Qué es la Wayback Machine?

![](https://academy.hackthebox.com/storage/modules/144/wayback.png)

```ad-quote
La **Wayback Machine** es un archivo digital de sitios web, creado por Internet Archive en 1996, que permite ver versiones pasadas de páginas web. Funciona capturando instantáneas de sitios mediante rastreadores web, almacenando tanto el contenido como los recursos (HTML, CSS, imágenes, etc.). Los usuarios pueden acceder a estas versiones archivadas ingresando la URL y seleccionando una fecha.

Es valiosa para el **reconocimiento web** ya que permite:

- Descubrir activos ocultos o vulnerabilidades en versiones anteriores de un sitio.
- Rastrear cambios y patrones en la evolución de la página.
- Recopilar inteligencia mediante contenido archivado.
- Realizar reconocimiento pasivo sin interactuar con la infraestructura del sitio.
```

---

## Automating Recon

```ad-info
Si bien el reconocimiento manual puede ser eficaz, también puede llevar mucho tiempo y ser propenso a errores humanos. La automatización de las tareas de reconocimiento web puede mejorar significativamente la eficiencia y la precisión, permitiéndole recopilar información a escala e identificar vulnerabilidades potenciales más rápidamente.
```

- **FinalRecon**: Herramienta modular en Python que permite tareas como verificación de certificados SSL, recopilación de información Whois y análisis de encabezados, facilitando la personalización según necesidades específicas.
    
- **Recon-ng**: Un marco poderoso en Python con módulos para tareas de reconocimiento como enumeraciones de DNS, descubrimiento de subdominios y escaneo de puertos, además de la capacidad de explotar vulnerabilidades conocidas.
    
- **theHarvester**: Diseñada para recopilar información como direcciones de correo electrónico y subdominios de fuentes públicas, utilizando motores de búsqueda y bases de datos como SHODAN.
    
- **SpiderFoot**: Herramienta de automatización de inteligencia que integra múltiples fuentes de datos para obtener información sobre objetivos, realizando búsquedas de DNS, rastreo web y escaneo de puertos.
    
- **OSINT Framework**: Colección de herramientas y recursos para la recopilación de inteligencia de código abierto, abarcando diversas fuentes como redes sociales y registros públicos.

### FinalRecon

```ad-quote
- **Información de Encabezado**: Muestra detalles sobre el servidor, tecnologías utilizadas y posibles errores de configuración de seguridad.
- **Búsqueda Whois**: Revela detalles de registro del dominio, como información del registrante y datos de contacto.
- **Información del Certificado SSL**: Examina el certificado SSL/TLS para verificar su validez y el emisor.
- **Crawlers**:
    - **HTML, CSS, JavaScript**: Extrae enlaces y posibles vulnerabilidades de estos archivos.
    - **Enlaces internos/externos**: Mapea la estructura del sitio web y conexiones a otros dominios.
    - **Imágenes, robots.txt, sitemap.xml**: Recopila información sobre las rutas de rastreo del sitio.
    - **Enlaces en JavaScript, Wayback Machine**: Encuentra enlaces ocultos y datos históricos.
- **Enumeración DNS**: Consulta más de 40 tipos de registros DNS, incluidos registros DMARC.
- **Enumeración de Subdominios**: Utiliza diversas fuentes de datos para descubrir subdominios.
- **Enumeración de Directorios**: Permite listas de palabras personalizadas para encontrar directorios y archivos ocultos.
- **Wayback Machine**: Recupera URL de los últimos cinco años para analizar cambios y posibles vulnerabilidades del sitio web.
```

```bash
# Instalación
git clone https://github.com/thewhiteh4t/FinalRecon.git
cd FinalRecon
pip3 install -r requirements.txt
chmod +x ./finalrecon.py
```

| Opción         | Argumento | Descripción                                                     |
| -------------- | --------- | --------------------------------------------------------------- |
| `-h`, `--help` |           | Muestra el mensaje de ayuda y sal.                              |
| `--url`        | URL       | Especifique la URL de destino.                                  |
| `--headers`    |           | Recuperar información del encabezado de la URL de destino.      |
| `--sslinfo`    |           | Obtenga información del certificado SSL para la URL de destino. |
| `--whois`      |           | Realice una búsqueda Whois para el dominio de destino.          |
| `--crawl`      |           | Rastree el sitio web de destino.                                |
| `--dns`        |           | Realice una enumeración de DNS en el dominio de destino.        |
| `--sub`        |           | Enumere los subdominios para el dominio de destino.             |
| `--dir`        |           | Busque directorios en el sitio web de destino.                  |
| `--wayback`    |           | Recuperar URL Wayback para el objetivo.                         |
| `--ps`         |           | Realice un escaneo rápido de puertos en el objetivo.            |
| `--full`       |           | Realice un escaneo de reconocimiento completo del objetivo.     |