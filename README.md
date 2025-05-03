# eWPTx3X0 - Guía de Preparación y Referencia para el eWPTX

Este repositorio es una guía estructurada para ayudarte a resolver el examen **eWPTX**. Aquí encontrarás un plan de ataque con referencias cruzadas a técnicas, CVEs y máquinas útiles de **Hack The Box (HTB)** para reforzar tus habilidades.

---

##  Estructura General del Entorno

El entorno de evaluación simula un conjunto de subdominios y APIs expuestas. 

El reconocimiento inicial:

- Enumeración de puertos.
- Subdominios.
- Tecnologías: JWT, InfluxDB, Jupyter, Swagger API, Deserialización, LDAP, entre otros.

---

##  Plan General de Ataque

### 1.  Reconocimiento

- Ejecuta escaneos de puertos con `nmap -sCVS` o `nmap -sV -p-`.
- Utiliza herramientas como `ffuf`, `gobuster` o `feroxbuster` para detectar rutas ocultas y subdominios.
- Reconfirma tecnologías con `whatweb`.

### 2. 2023-28472

- Revisa los endpoints `/minio/bootstrap/`
- Se trata de una consola vulnerable en versiones antiguas.
- la forma en que interactúas puede revelar credenciales para listar buckets.

> Explora: HTB *Skyfall*

---

### 3.  


-  expone endpoints que permiten inyecciones  por medio de estructuras complejas.
- Puedes probar distintos prefijos y sufijos para confirmar la vulnerabilidad.

> Explora: HTB *MAGENTO*

---

### 4.  InfluxDB - Explotación 

- Puerto: `8086`
- Esta base de datos es accesible y tiene una vulnerabilidad donde el JWT no se valida correctamente.
- El token puede generarse manualmente con `HS256` y `jwt.encode()`.

> Explora: HTB *DEVZAT*

---

### 5.  Jupyter - Ejecución de comandos vía notebooks

- Puerto: `8888`
- Explora la posibilidad de crear notebooks, ejecutar código y extraer datos del entorno.

> Explora: HTB *JUPITER*

---

### 6.  JWT 

- Crea una cuenta y luego fuerza la clave HMAC usando `hashcat -m 16500` con diccionarios de JWT.

> Explora: HTB *BACKEND*, *UNICODE*, *BACKEND TWO*

---

### 7.  API Enumeration

- Swagger expone documentación útil.
- Intercepta las peticiones y prueba modificaciones en los JWT para acceder a endpoints privilegiados.
- Revisa endpoints y su comportamiento ante métodos distintos.

> Explora: HTB *AWKWARD*, *MENTOR*, *BOLT*, *AUTHENTICATION*

---

### 8. SQLi en Websockets (Manual)

- Algunos endpoints permiten inyecciones SQL sofisticadas.
- Ojo: existen falsos positivos y bypasses específicos que funcionan con pruebas avanzadas.

> Explora: HTB *SOCCER*, *PHOENIX*

---

### 9.  Deserialización en PHP y Java

- Algunas aplicaciones permiten carga de archivos YAML o serializados que derivan en ejecución remota de código.
- Verifica cabeceras, campos de configuración y payloads sospechosos.

> Explora: HTB *TENET*, *ARKHAM*, *JEWEL*

---

### 10. LDAP + MariaDB

- LDAP está presente en el backend. Las respuestas en login y búsqueda pueden sugerir inyecciones o enumeración.
- A veces basta con interceptar un login y analizar headers.

> Explora: HTB *SHIBOLEN*, *ANALYSIS*

---

##  Máquinas de HTB que Ayudan para eWPTX

Estas máquinas de Hack The Box contienen técnicas similares al entorno real del eWPTX:

| Categoría       | Máquinas HTB Recomendadas                     |
|-----------------|-----------------------------------------------|
|  API / JWT     | BACKEND, BACKEND TWO, AWKWARD, UNICODE, MENTOR |
|  LDAP          | ANALYSIS, SHIBOLEN                             |
|  SQLi / NoSQLi | SOCCER, PHOENIX, SHOPPY, MAGENTO, OZ           |
|  S3 / MinIO    | SKYFALL                                        |
|  SSRF          | JARMIS                                         |
|  RCE / Deser.  | TENET, ARKHAM, JEWEL                           |
|  Exploración   | DEVZAT, JUPITER                                |

---

## ⚠ Disclaimer

Este documento está diseñado con fines educativos. No contiene instrucciones completas, ni comandos automáticos, ni vulnerabilidades explotadas al 100%. El objetivo es ayudarte a razonar cada paso del eWPTX, no a ofrecer una solución directa.

---
# Revisa siempre

- https://ippsec.rocks/
- https://forum.hackthebox.com/
- https://github.com/0xdf
- - https://github.com/MrR0b0t19
- https://book.hacktricks.xyz/

---
