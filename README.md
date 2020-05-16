# kiosk

### Configurar kiosk

#### Instalar dependencias

```
sudo apt-get update && sudo apt-get upgrade -y
sudo apt-get install xdotool unclutter sed docker.io docker-compose vim -y
```

#### Configurar raspberry para que inicie UI

```
sudo raspi-config
```

Ir a **3 Boot options -> B1 Desktop / CLI -> B4 Desktop Autologin**

##### Crear, activar e iniciar el servicio

```
sudo cp kiosk.service /lib/systemd/system/kiosk.service
sudo systemctl enable kiosk
sudo service kiosk start

```

#### Configurar docker

Agregamos el user `pi` al grupo `docker`:

```
sudo usermod -a -G docker pi
```

Iniciamos el servicio

```
docker-compose up -d 
```

#### Útiles:
Configuramos crontab para que la pantalla se apague a las 19:00 y se prenda a las 10:00

```
crontab -e
```
```
# Estas 2 lineas prenden y apagan la pantalla a las 8 y 20 horas respectivamente
0 8 * * * DISPLAY=":0.0" xset dpms force on
0 20 * * * DISPLAY=":0.0" xset dpms force off
```
