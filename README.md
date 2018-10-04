## ¡únete al equipo!

Estamos en [Slack](https://slack.osweekends.com)

## Objetivos del Equipo

**Objetivos Individuales dentro del Red Team**
- Pasarlo bien
- Aprender mucho juntos
- compartir ese conocimiento con el resto de OSW y comunidades
- Tener un entorno sano y seguro para aprender

**Objetivos del Red team como conjunto de Guilders**
- Entrenar un Red Team (paso 1)
- Atacar nuestra propia infraestructura para detectar errores (paso 2)
- Generar un ranking que motive al equipo, al estilo CTF (paso 3)
- Abrir más adelante esta política de Bug Hunters con HackMadrid y las comunidades de %27 (paso 4)
- :trollface: dominar el mundo (paso 5)

**Como estamos hoy?**
- @Kr0n0 es el líder espiritual/guru/referencia/sabio remoto en el área que nos ayudará a tomar el camino correcto y nos determinará por donde debemos ir
- @Falocab en principio apoyará y coordinará el trabajo del equipo en el día a día
- @ulisesgascon buscarme la vida para conseguir recursos y montar una infraestructura para tener maquinas y cosas donde desplegar entornos para entrenar con máquinas vulnerables y ayudar con los ejercicios del tipo Capture The Flag del equipo


## RoadMap

### 1. ¿Qué diablos es un red team?
Vamos a intentar una definición primero... Un red team es un equipo de pentesters o hackers éticos que trabajan de forma conjunta para atacar objetivos de una empresa de forma que comprueben y ayuden a los del blue team (los “defensores”) a comprobar las defensas.

Esto no solo incluye pentesting y hacking ético, también incluye otras cosas como por ejemplo intentar entrar en las instalaciones del cliente de manera física o intentar suplantar la identidad de una persona para conseguir información.
Aunque son temas divertidos (el lockpicking es un vicio xD) si os parece nos centraremos en la parte mas “informática” del asunto.

### 2. Metodología de ataques :
**No me canso de decir esto**. No se hacen las cosas a lo loco, hay que saber seguir un plan estructurado y documentado, con fases y resultados objetivos.
Incluso para cosas las que vamos a hacer por aquí hay que tener esto aunque sea en mente. Muchísimo trabajo del hacking ético se basa en recopilar información y búsqueda en internet, por lo que hay que hacerlo bien para no generar caos incluso cuando no se hacen informes.

Hay varias maneras de hacerlo. Yo suelo dividir el tema en 6 fases (+ la inicial de requisitos) :

0) Definición, requisitos y alcance del proyecto
1) Recolección de información
2) Modelo de amenaza y estrategias de penetración
3) Análisis de vulnerabilidades : Incluye exploración y evaluación de vulnerabilidades
4) Explotación de vulnerabilidades
5) Post-explotación
6) Generación de informe final

Esto vale para cualquier tipo de proyecto, sea sistemas, redes, aplicaciones web, móviles o hardware.

Simplemente tenedlo en mente para lo que vamos a hacer.

### 3. ¿Qué se quiere atacar? ¿Cual es el objetivo?
- Sistemas
- Aplicaciones web
- Aplicaciones móviles (iOS/Android)
- Hardware dedicado
- Todo lo que tenga una empresa o persona partiendo de su nombre (Estos son los proyectos realmente divertidos!)

Dependiendo del tipo de objetivo se usa una o varias herramientas.

### 4. ¿Qué herramientas necesitamos usar?
En general con que tengáis una máquina virtual con Kali Linux configurada para tener salida a internet y os sepáis manejar un poco con ella nos vale de momento, pero hay mucho más que esto (y ya es).

### 5. Ok me gusta la idea. ¿Qué tengo que hacer primero?
Echad un ojo a esta web  para empezar : 

https://billionbytes.es/herramientas-basicas-kali-linux-21580

Una buena aproximación sería : 
1) Tener instalada Kali Rolling última versión en VMWare/Virtualbox, con salida a internet y saber manejarse un poco con ella (Si hay alguien que no sepa manejarse con línea de comando en Linux que avise!)
2) Configurar Burp Suite (incluido en Kali) con el proxy configurado y comprobando que capturáis peticiones web.
3) Leer un poco y cacharrear sobre las herramientas :
- Escaner de puertos : NMap.
- Herramienta para SQL Injection : sqlmap.
- Cracker de hashes : Hashcat
- Entorno de explotación : Metasploit
- Proxy y pentesting web : Burp
- OSINT integrado : Maltego
- Móviles : MobSF

Mientras iremos mirando cosillas que puedan estar interesantes para "jugar".

Si tenéis cualquier duda comentadla por el canal. La idea es que todos aprendamos y podamos divertirnos con esto, así que a por ello :)

Kr0n0 (ccvals@linux.com) - 181004 - Canal #red-team OSW 
