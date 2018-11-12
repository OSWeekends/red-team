## Fase 1 - Adquisición del apk

Ponemos el teléfono en modo USB Debugging para poder acceder via adb
Entramos en el teléfono : adb shell
Listamos los paquetes y buscamos por el nombre de cloudflare :pm list packages | grep cloudflare
Vemos la ruta del archivo apk. Normalmente se llama base.apk y está en una ruta concreta : pm path com.cloudflare.onedotonedotonedotone
[La ruta en mi caso es “/data/app/com.cloudflare.onedotonedotonedotone-9kt36J1VN3veL1DlHyOKXA==/base.apk”]
Descargamos el archivo a una carpeta usando adb : adb pull /data/app/com.cloudflare.onedotonedotonedotone-9kt36J1VN3veL1DlHyOKXA==/base.apk
Renombramos el archivo base.apk a algo como cloudflare.apk

## Fase 2 - Extraer las fuentes

Descargamos apktool : https://ibotpeaches.github.io/Apktool/

Descomprimirmos la herramienta en la carpeta y con Java instalado ejecutamos : java -jar apktool.jar d base.apk
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

## Fase 3 - Ver cosicas


Ahora en la carpeta cloudflare tenéis las fuentes descomprimidas. Podemos ver cosas interesantes como…

AndroidManifest.xml

apktool.yml

assets

kotlin

lib

original

res

smali

unknown

Por comentar algo interesante… en lib se suele encontrar bibliotecas compiladas para diferentes arquitecturas (normalmente ARM) que no se suelen mirar…

#### Tenemos 4 arquitecturas :

arm64-v8a

armeabi

armeabi-v7a

x86

y varios libcproxy.so (bibliotecas dinámicas). Nos vamos a centrar en la de armeabi
oot@Kr0n0s-MBP:~/temp/cloudflare/lib/armeabi$ file libcproxy.so
libcproxy.so: ELF 32-bit LSB shared object ARM, EABI5 version 1 (SYSV), dynamically linked, interpreter /system/bin/linker, with debug_info, not stripped

¿Veis algo interesante en la descripción del fichero…?

“with debug_info” y “not stripped” os deberían de llamar la atención…

Con esta información… volcamos las cadenas de texto a un fichero para analizarlas después…

strings libcproxy.so > lista.txt

y abrimos el archivo lista.txt

== A ver si alguien es capaz de llegar hasta aquí
y completa las dos claves que hay aparte de esta :

-----BEGIN RSA PRIVATE KEY-----
MIIEpAIBAAKCAQEAyHTEzLn5tXnpRdkUYLB9u5Pyax6fM60Nj4o8VmXl3ETZzGaF
B9X4J7BKNdBjngpuG7fa8H6r7gwQk4ZJGDTzqCrSV/Uu1C93KYRhTYJQj6eVSHD1
bk2y1RPD0hrt5kPqQhTrdOrA7R/UV06p86jt0uDBMHEwMjDV0/YI0FZPRo7yX/k9
Z5GIMC5Cst99++UMd//sMcB4j7/Cf8qtbCHWjdmLao5v4Jv4EFbMs44TFeY0BGbH
7vk2DmqV9gmaBmf0ZXH4yqSxJeD+PIs1BGe64E92hfx//DZrtenNLQNiTrM9AM+v
dqBpVoNq0qjU51Bx5rU2BXcFbXvI5MT9TNUhXwIDAQABAoIBAGdNtfYDiap6bzst
yhCiI8m9TtrhZw4MisaEaN/ll3XSjaOG2dvV6xMZCMV+5TeXDHOAZnY18Yi18vzz
4Ut2TnNFzizCECYNaA2fST3WgInnxUkV3YXAyP6CNxJaCmv2aA0yFr2kFVSeaKGt
ymvljNp2NVkvm7Th8fBQBO7I7AXhz43k0mR7XmPgewe8ApZOG3hstkOaMvbWAvWA
zCZupdDjZYjOJqlA4eEA4H8/w7F83r5CugeBE8LgEREjLPiyejrU5H1fubEY+h0d
l5HZBJ68ybTXfQ5U9o/QKA3dd0toBEhhdRUDGzWtjvwkEQfqF1reGWj/tod/gCpf
DFi6X0ECgYEA4wOv/pjSC3ty6TuOvKX2rOUiBrLXXv2JSxZnMoMiWI5ipLQt+RYT
VPafL/m7Dn6MbwjayOkcZhBwk5CNz5A6Q4lJ64Mq/lqHznRCQQ2Mc1G8eyDF/fYL
Ze2pLvwP9VD5jTc2miDfw+MnvJhywRRLcemDFP8k4hQVtm8PMp3ZmNECgYEA4gz7
wzObR4gn8ibe617uQPZjWzUj9dUHYd+in1gwBCIrtNnaRn9I9U/Q6tegRYpii4ys
c176NmU+umy6XmuSKV5qD9bSpZWG2nLFnslrN15Lm3fhZxoeMNhBaEDTnLT26yoi
33gp0mSSWy94ZEqipms+ULF6sY1ZtFW6tpGFoy8CgYAQHhnnvJflIs2ky4q10B60
ZcxFp3rtDpkp0JxhFLhiizFrujMtZSjYNm5U7KkgPVHhLELEUvCmOnKTt4ap/vZ0
BxJNe1GZH3pW6SAvGDQpl9sG7uu/vTFP+lCxukmzxB0DrrDcvorEkKMom7ZCCRvW
KZsZ6YeH2Z81BauRj218kQKBgQCUV/DgKP2985xDTT79N08jUo3hTP5MVYCCuj/+
UeEw1TvZcx3LJby7P6Xad6a1/BqveaGyFKIfEFIaBUBItk801sDDpDaYc4gL00Xc
7lFuBHOZkxJYlss5QrGpuOEl9ZwUt5IrFLBdYaKqNHzNVC1pCPfb/JyH6Dr2HUxq
gxUwAQKBgQCcU6G2L8AG9d9c0UpOyL1tMvFe5Ttw0KjlQVdsh1MP6yigYo9DYuwu
bHFVW2r0dBTqegP2/KTOxKzaHfC1qf0RGDsUoJCNJrd1cwoCLG8P2EF4w3OBrKqv
8u4ytY0F+Vlanj5lm3TaoHSVF1+NWPyOTiwevIECGKwSxvlki4fDAA==
-----END RSA PRIVATE KEY-----

Y ahora la parte más importante… **¿Cómo protegerse ante este robo de información?**

Sencillo en este caso : No meter debug info y strippear el fichero antes de ponerlo en producción.

Como veis en muchos casos no es muy complicado conseguir información comprometida…  Podríamos seguir con las fuentes Kotlin y Java pero con esto de primeras ya podéis cacharrear,
a ver si alguien consigue llegar hasta aquí y poner las que faltan ^^
