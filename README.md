# selinux-demo

## Requerimientos

* Red Hat Enterprise Linux 9.3 o Similar
* Acceso a root / sudo
* Estar susctiro de Red Hat o tener la capacidad de instalar paquetes en el sistema via DNF 

## Apache 2 (httpd)

Para demostrar el funcionamiento de SELinux, se utilizará una instalación básica de Apache

### Validar funcionamiento de Apache


* Instalar apache
```
dnf install httpd -y
```
* Iniciar apache
```
systemctl start httpd
```
* Crear contenido de ejemplo

```
echo "Hello from Apache" >  /var/www/html/index.html
```

* Validar acceso a Servicio
```
curl http://localhost
curl -I http://localhost

```

## Documentación y herramientas SELinux

* Instalación

```
dnf install policycoreutils policycoreutils-python-utils selinux-policy-doc -y
```
* Actualiación de manuales
```
mandb
```
* Obtener información de SELinux
```
man -k _selinux
man -k _selinux |grep http

```
man httpd_selinux
```

Buscar en contenido del manual ```PORT TYPES   /PORT```
Salir del manual

```
semanage port -l |grep -w -E "(http_cache_port_t|http_port_t)"
```


## Validando funcionamiento de SELinux

* Alterar configuración de Apache (cambio de puerto 80 a 82)
```
grep '^Listen' /etc/httpd/conf/httpd.conf
sed -i 's/^Listen.*/Listen 82/g' /etc/httpd/conf/httpd.conf
grep '^Listen' /etc/httpd/conf/httpd.conf

```
* Reiniciar Apache

```
systemctl restart httpd 
```
DEBE FALLAR
```
journalctl -u httpd
```




