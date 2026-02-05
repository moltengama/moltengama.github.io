---
title: "dlovelive"
date: 2026-02-04 00:00:00 +0800
categories: [forensics,reversing, .net,c#]
tags: [forensics,reversing,scripting]
image:
  path: /assets/img/banners/Screenshot_1.png
---



## Enunciado:
Tu sobrinito, un fanático de Umamusume Pretty Derby, intentó instalar un mod no oficial y su PC quedó comprometida. Los atacantes dejaron un payload que se comunica con un servidor C2 para descargar órdenes y exfiltrar datos. Tu misión es analizar el servidor C2, extraer la evidencia y recuperar la flag que probarán que has sido capaz de comprometer la infraestructura atacante.

Preguntas:
- IP del C2:`
- IP de la victima: 
- A que grupo famoso de ciberdelincuentes pertenece la wallet:
- Nombre del comprimido:
- hash md5 de la libreria del binario malicioso:
- Nombre de la funcion que envia datos del host al c2:
- Clave estatica en ejecutable:
- Clave Maestra del C2:
- Comando que ejecuta el C2:
- INFORMACION DEL USUARIO DECODIFICADA:
- Endpoint de descarga remota de archivos del C2:
- Intenta descargar el archivo flag.txt:

Para extraer o replicar usar esta URL: 
https://apuntesciberseguridad.vercel.app/

## Preguntas:

| Pregunta                                       | Respuesta                             |
| ---------------------------------------------- | ------------------------------------- |
| Ip del C2                                      | 192.168.106.129                       |
| Hostname de la victima                         | DESKTOP-15VR2CC                       |
| A que grupo famoso pertenece la wallet         | LockBit                               |
| Nombre del comprimido                          | /download_crack                       |
| Hash md5 de la libreria del binario malicioso  | e3a1d9397c068e2b4e556861dca05330      |
| Nombre de la funcion que envia datos al C2     | SendInfo                              |
| Clave estatica del C2                          | lxia                                  |
| clave maestra del C2                           | ks0008                                |
| Comando que ejecuta el c2                      | whoami /all                           |
| Endpoint de descarga remota ed archivos del C2 | /weaponizeeeeeee                      |
| Obten flag.txt                                 | flag_{Chiste.Reversing_Apoco.notilin} |

### Pregunta1:

Comunicacion elevada de `17.258` paquetes 
![](/assets/img/dlovelive/Pasted image 20260205090901.png)
### Pregunta2:
Evaluando el protocolo SMB daremos con el hostname usado por el host de la victima
![](/assets/img/dlovelive/Pasted image 20260205091001.png)


### pregunta 3:

![](/assets/img/dlovelive/Pasted image 20260205091304.png)
![[Pasted image 20260205091336.png)


### PREGUNTA4
![](/assets/img/dlovelive/Pasted image 20260205091425.png)

### pregunta 5:

![](/assets/img/dlovelive/Pasted image 20260205091621.png)

```
molten@DESKTOP-77RDABS:/mnt/d/CTFs$ md5sum  DirectLoveLive.dll
5edfa6ea6608c27f44d9bf687afe64d3  DirectLoveLive.dll
molten@DESKTOP-77RDABS:/mnt/d/CTFs$
```

### PREGUNTA 6-7
![](/assets/img/dlovelive/Pasted image 20260205092016.png)
### PREGUNTA 8:
![](/assets/img/dlovelive/Pasted image 20260205092105.png)

```
molten@DESKTOP-77RDABS:/mnt/d/CTFs$ curl -k -X POST "https://apuntesciberseguridad.vercel.app/ConstKey" -H "Content-Type: application/json" -d '{"GETKEY":"lagarto"}'
{"key":"BwtZUVxA"}
```
![](/assets/img/dlovelive/Pasted image 20260205092703.png)


### PREGUNTA 9
![](/assets/img/dlovelive/Pasted image 20260205092733.png)
![](/assets/img/dlovelive/Pasted image 20260205092758.png)


### pregunta 10
![](/assets/img/dlovelive/Pasted image 20260205093043.png)
### pregunta 11
![](/assets/img/dlovelive/Pasted image 20260205093128.png)
![](/assets/img/dlovelive/Pasted image 20260205093147.png)
![](/assets/img/dlovelive/Pasted image 20260205093202.png)

``` bash
molten@DESKTOP-77RDABS:/mnt/d/CTFs$ curl -k -X POST "https://apuntesciberseguridad.vercel.app/weaponizeeeeeeee"   -H "Content-Type: application/json" -d '{"DOWN": "ZmRhby58eHw="}'
flag_{Chiste.Reversing_Apoco.notilin}
```
