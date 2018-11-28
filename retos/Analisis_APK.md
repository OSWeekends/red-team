# Analizar un APK

Hola gente!

Viniendo del canal [#07-recursos](https://osweekends.slack.com/archives/C8GLKD8M9/p1542018838037300) estábamos hablando de la herramienta de Cloudflare para iOS/Android y nada, me he puesto a ver qué es lo que hace y me ha parecido interesante compartirlo por aquí con vosotros.

La app en cuestión es: https://play.google.com/store/apps/details?id=com.cloudflare.onedotonedotonedotone

Bueno. Hay varias maneras de hacer esto, voy a ir a por la más rápida (que no es la mejor) pero para empezar creo que vale para que analicéis un poco alguna app Android rápidamente.

Primero instalamos la app desde la app store en un terminal (como digo hay otras maneras pero vamos a hacerlo rápido).


## Fase 1 - Adquisición del apk

 1. Ponemos el teléfono en modo USB Debugging para poder acceder via adb
 1. Entramos en el teléfono: `adb shell`
 1. Listamos los paquetes y buscamos por el nombre de cloudflare: `pm list packages | grep cloudflare`
 1. Vemos la ruta del archivo apk. Normalmente se llama base.apk y está en una ruta concreta: `pm path com.cloudflare.onedotonedotonedotone`
[La ruta en mi caso es “/data/app/com.cloudflare.onedotonedotonedotone-9kt36J1VN3veL1DlHyOKXA==/base.apk”]
 1. Descargamos el archivo a una carpeta usando adb: `adb pull /data/app/com.cloudflare.onedotonedotonedotone-9kt36J1VN3veL1DlHyOKXA==/base.apk`
 1. Renombramos el archivo base.apk a algo como cloudflare.apk


## Fase 2 - Extraer las fuentes

 1. Descargamos apktool: https://ibotpeaches.github.io/Apktool/
 1. Descomprimirmos la herramienta en la carpeta y con Java instalado ejecutamos: `java -jar apktool.jar d base.apk`

```
ibotpeaches.github.io
Apktool - A tool for reverse engineering 3rd party, closed, binary Android apps.
Apktool - A tool for reverse engineering 3rd party, closed, binary Android apps. It can decode resources to nearly original form and rebuild them after making some modifications
I: Using Apktool 2.3.4 on cloudflare.apk
I: Loading resource table...
I: Decoding AndroidManifest.xml with resources...
S: WARNING: Could not write to (/var/root/Library/apktool/framework), using /var/folders/zz/zyxvpxvq6csfxvn_n0000000000000/T/ instead...
S: Please be aware this is a volatile directory and frameworks could go missing, please utilize --frame-path if the default storage directory is unavailable
I: Loading resource table from file: /var/folders/zz/zyxvpxvq6csfxvn_n0000000000000/T/1.apk
I: Regular manifest package...
I: Decoding file-resources...
I: Decoding values */* XMLs...
I: Baksmaling classes.dex...
I: Copying assets and libs...
I: Copying unknown files...
I: Copying original files...
```

## Fase 3 - Ver cosicas

Ahora en la carpeta cloudflare tenéis las fuentes descomprimidas. Podemos ver cosas interesantes como...

```
AndroidManifest.xml
apktool.yml
assets
kotlin
lib
original
res
smali
unknown
```

Por comentar algo interesante... en lib se suele encontrar bibliotecas compiladas para diferentes arquitecturas (normalmente ARM) que no se suelen mirar...
Tenemos 4 arquitecturas:

 * arm64-v8a
 * armeabi
 * armeabi-v7a
 * x86

Y varios libcproxy.so (bibliotecas dinámicas). Nos vamos a centrar en la de armeabi

```
$ file libcproxy.so
libcproxy.so: ELF 32-bit LSB shared object ARM, EABI5 version 1 (SYSV), dynamically linked, interpreter /system/bin/linker, with debug_info, not stripped
```

¿Veis algo interesante en la descripción del fichero...?

“with debug_info” y “not stripped” os deberían de llamar la atención...
Con esta información... volcamos las cadenas de texto a un fichero para analizarlas después...
`strings libcproxy.so > lista.txt`
y abrimos el archivo lista.txt

🏁 A ver si alguien es capaz de llegar hasta aquí y completa las dos claves que hay aparte de esta:

```
-----BEGIN RSA PRIVATE KEY-----
...
-----END RSA PRIVATE KEY-----
```

Y ahora la parte más importante... ¿Cómo protegerse ante este robo de información?

Sencillo en este caso: No meter debug info y strippear el fichero antes de ponerlo en producción.

Como veis en muchos casos no es muy complicado conseguir información comprometida...  Podríamos seguir con las fuentes Kotlin y Java pero con esto de primeras ya podéis cacharrear a ver si alguien consigue llegar hasta aquí y poner las que faltan ^^
