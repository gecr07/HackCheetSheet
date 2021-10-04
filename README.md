# ⭐️HackCheetSheet⭐️

Este sera un repositorio en donde ire añadiendo todo el conocimiento que vaya adquiriendo sera una guia para mi ojala le pueda servir a alguien como a mi. 

<h2> 💻 Linux 💻</h2>

Checar todos los paquetes instalados.

```bash
apt list --installed
```

To add OpenSSH to the SysV script to tell the system to run this service after startup, we can link it with the following command:

```bash
systemctl enable ssh
```

The tool journalctl to view the logs. Se puede ver que usuario inicio el servicio.
 
```bash
journalctl -u ssh.service --no-pager
```

<h2> 😊 Web Servers😊 </h2>

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
$ npm install -g node-static   # install dependency
$ static -p 8000
```

