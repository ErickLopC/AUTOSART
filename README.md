# AUTOSTART

## Configuraciones iniciales 
1. Dirijirse a la Pagina de NVIDIA para desargar el jetpack (Dependiendo de la versión de Ubuntu que se tenga instalada en la computadora se elegirá la versión de Jetpack).

    En nuestro caso tenemos instalado Ubuntu 18.04 en la computadora por lo cual            instalaremos[Jetpack 3.3.3](https://developer.nvidia.com/embedded/jetpack-3_3_3)


3. Grabar la imagen en la SD


   Posteriormente se coloca la SD en la jetson para poder conertarla a la alimeacion y      poder inciar con la configuracion. 

4. Instalar los drives para WIFI  "rtl88x2bu".  

5. Istatalar ROS en la Jetson

6. Confifurar el host
   En la terminal ejecutar

```
sudo gedit hosts
```
   Una vez despliega un archivo se configura de la manera siguiente. 
   
8. Copiar las carpetas o descargaslas desde

9.Si se tiene configuradas varias redes de internet se tendría que realizar la siguiente configuración para que cuando esta inicie se conecte automáticamente a la red que se espera.

## --

Una vez conectada la Jetson a la fuente de alimentacion se ejecuta la terminal

```
User=robotica
[Install]
WantedBy=multi-user.target
```
Una vez configurado 

Se abre la carpeta del autostart.sh 
```
sudo gedit /usr/local/bin/autostart.sh
```
se copian las siguientes lineas

```
#!/bin/bash
passord='robotica'
source /opt/ros/melodic/setup.bash
source ~/Turtlebot2/devel/setup.bash
export ROS_MASTER_URI=http://192.168.43.178:11311
export ROS_IP=192.168.43.178
sleep 15

echo $passwor | sudo -S chmod 777 /dev/ttyUSB0 

sleep 15

roscore &
sleep 15

roslaunch rplidar_ros rplidar_a1.launch &
sleep 15

roslaunch turtlebot_bringup minimal.launch & 
```
Se aguardan los cambios y se ejecutan los siguientes comandos

```
sudo systemctl enable autostart.service
sudo systemctl start autostart.service
sudo systemctl status autostart.service 
```

## Instlacion de los drives para leer el Lidar desde la Jetson

rplidar a1 Githud       

clonar el git                 

Turtlebot2_src

Turtlebot2$ catkin_make

Verifica el puerto ls/dev/tty*        (en que puerto esta instalado el LIDAR )

sudo chmod 777/dev/ttyUSB0                                                  ← (Se le asigna permiso)

roslaunch rplidar_ros view_rplidar_a1.launch









## Control del turtlebot2 desde la Jetson mediante cable





*********************************************
Turtlebot Fisico
-------------------------------
*****
roscore
cd catkin_ws
source ./devel/setup.bash
 roslaunch turtlebot_bringup minimal.launch --screen
roslaunch turtlebot_teleop keyboard_teleop.launch


**************************************














# Observaciones durante el proceso 

Para conectar la pantalla a la Jetson(conectar sin conversores, Direccto a la HMI(1 cable) )



 --------------------
 en la jetson se debe de levantar el turtlebot 
 --------------------
 NO OLVIDAR EL SOURCE 
  rosrun mov_turtle control_trayectoria_recta.py 
