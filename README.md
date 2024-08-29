# WFUZZ

Es una herramienta utilizada para realizar ataques de fuerza bruta, especialmente para fuzzing en aplicaciones web. Aquí te dejo algunos ejemplos de comandos de `wfuzz` para diferentes propósitos:

### 1. Fuzzing de subdominios

```bash
wfuzz -c -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt -u "http://monitorsthree.htb/" -H "Host: FUZZ.monitorsthree.htb" --hc 404 --hl 337
```

- `-c`: Muestra la salida en color.
- `-w`: Especifica la lista de palabras a utilizar (`subdomains-top1million-5000.txt`).
- `-u`: URL del sitio web a fuzzear.
- `-H`: Header personalizado donde `FUZZ` es el marcador que `wfuzz` reemplazará por cada palabra en la lista.
- `--hc 404`: Oculta resultados con el código de estado HTTP 404 (página no encontrada).
- `--hl 337`: Oculta resultados con una longitud de respuesta específica (337 caracteres).

### 2. Fuzzing de rutas/directorios

Para encontrar rutas o directorios ocultos en un servidor:

```bash
wfuzz -c -w /usr/share/seclists/Discovery/Web-Content/directory-list-2.3-medium.txt -u "http://example.com/FUZZ" --hc 404
```

- `-w`: Utiliza una lista de palabras para descubrir directorios comunes.
- `--hc 404`: Filtra las respuestas que devuelvan un código 404.

### 3. Fuzzing de parámetros GET

Para fuzzear los parámetros de una URL:

```bash
wfuzz -c -w /usr/share/seclists/Discovery/Web-Content/burp-parameter-names.txt -u "http://example.com/index.php?FUZZ=test" --hh 0
```

- `--hh 0`: Oculta las respuestas que no tengan encabezados de tamaño.

### 4. Fuzzing de parámetros POST

Para fuzzear parámetros POST de una solicitud HTTP:

```bash
wfuzz -c -w /usr/share/seclists/Discovery/Web-Content/burp-parameter-names.txt -u "http://example.com/index.php" -d "FUZZ=test" --hc 404
```

- `-d`: Define el cuerpo de la solicitud (método POST).

### 5. Fuzzing con autenticación básica

Si el sitio requiere autenticación básica HTTP, puedes usar:

```bash
wfuzz -c -w /usr/share/seclists/Passwords/darkweb2017-top1000.txt -u "http://example.com/login" --basic "admin:FUZZ" --hh 64
```

- `--basic "usuario:contraseña"`: Realiza fuzzing sobre las credenciales de autenticación básica.

### 6. Fuzzing de múltiples palabras (Fuzzing avanzado)

Si necesitas hacer fuzzing en múltiples posiciones a la vez:

```bash
wfuzz -c -w /usr/share/seclists/Discovery/Web-Content/burp-parameter-names.txt -w /usr/share/seclists/Passwords/darkweb2017-top1000.txt -u "http://example.com/index.php?param1=FUZZ&param2=FUZ2Z" --hc 404
```

- `-w`: Usa múltiples listas de palabras (`FUZZ` para la primera lista y `FUZ2Z` para la segunda lista).

### 7. Fuzzing de encabezados HTTP

Para fuzzear diferentes encabezados HTTP:

```bash
wfuzz -c -w /usr/share/seclists/Discovery/Web-Content/burp-parameter-names.txt -u "http://example.com" -H "User-Agent: FUZZ" --hl 1024
```

- `-H "User-Agent: FUZZ"`: Realiza fuzzing sobre el encabezado "User-Agent".

Estos son algunos ejemplos comunes para diferentes escenarios de fuzzing con `wfuzz`. Puedes personalizar cada comando según el objetivo de tu prueba de penetración.
