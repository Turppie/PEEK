# PEEK
Somos el peak


# COMANDOS PARA HACER EL VLAN

CONFIGURAR VLANS

Switch>ENA

Switch#configure ter

Switch(config)#ADMIN 0     //Cambiar el número de área

Switch(config-vlan)#NAME VLAN10     //Cambiar el número de área

Switch(config-vlan)#exit

Switch(config)#interface range f0/1-7     //Si solo se usa un puerto se usa interface f0/10 donde los o el número es el número de puerto o puertos válidos

Switch(config-if-range)#switchport mode access

Switch(config-if-range)#switchport access ADMIN 0       //Cambiar el número de área

Switch(config-if-range)#exit

Switch(config)#exit

Switch>show vlan

//Video de referencia: https://www.youtube.com/watch?v=LEt0wEJpeoc


//Para configurar la misma VLAN en otro switch se tiene que hacer lo mismo y poner el mismo nombre que el VLAN del otro switch
//Video de referencia: https://www.youtube.com/watch?v=z3qKN9TDYjQ


# CONEXIÓN ENTRE 2 SWITCHS O CON EL ROUTER

Switch>ENA

Switch#configure ter

Switch(config)#interface g0/1      //Cambiar el número de puerto de conexión entre los switchs

Switch(config-if)#switchport mode trunk

Switch(config-if)#switchport trunk allowed ADMIN 0,20,30,40,50,60

Switch(config-if)#exit

//Hacer lo mismo en los dos switchs que se conectan


CONFIGURACIÓN DEL ROUTER

Router>ENA

Router#configure ter

Router(config)#interface g0/0/1

Router(config-if)#no shutdown      //Para levantar el router

Router(config-if)#exit

Router(config)#interface g0/0/1.10      //Cambiar el número de acuerdo al área correspondiente

Router(config-subif)#interface g0/0/1.20

Router(config-subif)#interface g0/0/1.30

Router(config-subif)#interface g0/0/1.40

Router(config-subif)#interface g0/0/1.50

Router(config-subif)#interface g0/0/1.60

Router(config-subif)#exit

Router(config)#interface g0/0/1.10      //Aquí ya comienza la encapsulación para que cada subinterface se conecte a cada vlan

Router(config-subif)#encapsulation dot1Q 10      //Cambiar el número de acuerdo al área correspondiente

Router(config-subif)#ip address 130.10.0.1 255.255.255.128      //Cambiar la IP de acuerdo al Gateway de cada área según el excel, la máscara es igual para todos

Router(config-subif)#exit

//Video de referencia: https://www.youtube.com/watch?v=74N5yCCDwW8


# CONFIGURACIÓN DE ACLS PARA LA COMUNICACIÓN ENTRE VLANS SOLO PARA MADRID

Router>ENA

Router#configure ter

access-list 102 deny ip 130.10.0.0 0.0.0.63 130.10.0.80 0.0.0.15      //Administración -> Marketing ❌
access-list 102 deny ip 130.10.0.0 0.0.0.63 130.10.0.96 0.0.0.15      //Administración -> Ventas ❌
access-list 102 deny ip 130.10.0.0 0.0.0.63 130.10.0.128 0.0.0.31      //Administración -> Finanzas ❌
access-list 102 deny ip 130.10.0.0 0.0.0.63 130.10.0.160 0.0.0.31      //Administración -> Logística ❌
access-list 102 deny ip 130.10.0.0 0.0.0.63 130.10.0.64 0.0.0.15      //Administración -> Sistemas ❌
access-list 102 deny ip 130.10.0.0 0.0.0.63 130.10.2.80 0.0.0.15      //Administración -> Marketing ❌
access-list 102 deny ip 130.10.0.0 0.0.0.63 130.10.2.96 0.0.0.15      //Administración -> Ventas ❌
access-list 102 deny ip 130.10.0.0 0.0.0.63 130.10.2.128 0.0.0.31      //Administración -> Finanzas ❌
access-list 102 deny ip 130.10.0.0 0.0.0.63 130.10.2.160 0.0.0.31      //Administración -> Logística ❌
access-list 102 deny ip 130.10.0.0 0.0.0.63 130.10.2.64 0.0.0.15      //Administración -> Sistemas ❌
access-list 102 deny ip 130.10.0.0 0.0.0.63 130.10.1.80 0.0.0.15      //Administración -> Marketing ❌
access-list 102 deny ip 130.10.0.0 0.0.0.63 130.10.1.96 0.0.0.15      //Administración -> Ventas ❌
access-list 102 deny ip 130.10.0.0 0.0.0.63 130.10.1.128 0.0.0.31      //Administración -> Finanzas ❌
access-list 102 deny ip 130.10.0.0 0.0.0.63 130.10.1.160 0.0.0.31      //Administración -> Logística ❌
access-list 102 deny ip 130.10.0.0 0.0.0.63 130.10.1.64 0.0.0.15      //Administración -> Sistemas ❌
access-list 102 deny ip 130.10.0.64 0.0.0.15 130.10.0.80 0.0.0.15      //Sistemas -> Marketing ❌
access-list 102 deny ip 130.10.0.64 0.0.0.15 130.10.0.96 0.0.0.15      //Sistemas -> Ventas ❌
access-list 102 deny ip 130.10.0.64 0.0.0.15 130.10.0.128 0.0.0.31      //Sistemas -> Finanzas ❌
access-list 102 deny ip 130.10.0.64 0.0.0.15 130.10.0.160 0.0.0.31      //Sistemas -> Logística ❌
access-list 102 deny ip 130.10.0.64 0.0.0.15 130.10.0.0 0.0.0.63      //Sistemas -> Administración ❌
access-list 102 deny ip 130.10.0.64 0.0.0.15 130.10.1.80 0.0.0.15      //Sistemas -> Marketing ❌
access-list 102 deny ip 130.10.0.64 0.0.0.15 130.10.1.96 0.0.0.15      //Sistemas -> Ventas ❌
access-list 102 deny ip 130.10.0.64 0.0.0.15 130.10.1.128 0.0.0.31      //Sistemas -> Finanzas ❌
access-list 102 deny ip 130.10.0.64 0.0.0.15 130.10.1.160 0.0.0.31      //Sistemas -> Logística ❌
access-list 102 deny ip 130.10.0.64 0.0.0.15 130.10.1.0 0.0.0.63      //Sistemas -> Administración ❌
access-list 102 deny ip 130.10.0.64 0.0.0.15 130.10.2.80 0.0.0.15      //Sistemas -> Marketing ❌
access-list 102 deny ip 130.10.0.64 0.0.0.15 130.10.2.96 0.0.0.15      //Sistemas -> Ventas ❌
access-list 102 deny ip 130.10.0.64 0.0.0.15 130.10.2.128 0.0.0.31      //Sistemas -> Finanzas ❌
access-list 102 deny ip 130.10.0.64 0.0.0.15 130.10.2.160 0.0.0.31      //Sistemas -> Logística ❌
access-list 102 deny ip 130.10.0.64 0.0.0.15 130.10.2.0 0.0.0.63      //Sistemas -> Administración ❌
access-list 102 deny ip 130.10.0.80 0.0.0.15 130.10.0.64 0.0.0.15      //Marketing -> Sistemas ❌
access-list 102 deny ip 130.10.0.80 0.0.0.15 130.10.0.96 0.0.0.15      //Marketing -> Ventas ❌
access-list 102 deny ip 130.10.0.80 0.0.0.15 130.10.0.128 0.0.0.31      //Marketing -> Finanzas ❌
access-list 102 deny ip 130.10.0.80 0.0.0.15 130.10.0.160 0.0.0.31      //Marketing -> Logística ❌
access-list 102 deny ip 130.10.0.80 0.0.0.15 130.10.0.0 0.0.0.63      //Marketing -> Administración ❌
access-list 102 deny ip 130.10.0.80 0.0.0.15 130.10.1.64 0.0.0.15      //Marketing -> Sistemas ❌
access-list 102 deny ip 130.10.0.80 0.0.0.15 130.10.1.96 0.0.0.15      //Marketing -> Ventas ❌
access-list 102 deny ip 130.10.0.80 0.0.0.15 130.10.1.128 0.0.0.31      //Marketing -> Finanzas ❌
access-list 102 deny ip 130.10.0.80 0.0.0.15 130.10.1.160 0.0.0.31      //Marketing -> Logística ❌
access-list 102 deny ip 130.10.0.80 0.0.0.15 130.10.1.0 0.0.0.63      //Marketing -> Administración ❌
access-list 102 deny ip 130.10.0.80 0.0.0.15 130.10.2.64 0.0.0.15      //Marketing -> Sistemas ❌
access-list 102 deny ip 130.10.0.80 0.0.0.15 130.10.2.96 0.0.0.15      //Marketing -> Ventas ❌
access-list 102 deny ip 130.10.0.80 0.0.0.15 130.10.2.128 0.0.0.31      //Marketing -> Finanzas ❌
access-list 102 deny ip 130.10.0.80 0.0.0.15 130.10.2.160 0.0.0.31      //Marketing -> Logística ❌
access-list 102 deny ip 130.10.0.80 0.0.0.15 130.10.2.0 0.0.0.63      //Marketing -> Administración ❌
access-list 102 deny ip 130.10.0.96 0.0.0.15 130.10.0.64 0.0.0.15      //Ventas -> Sistemas ❌
access-list 102 deny ip 130.10.0.96 0.0.0.15 130.10.0.80 0.0.0.15      //Ventas -> Marketing ❌
access-list 102 deny ip 130.10.0.96 0.0.0.15 130.10.0.128 0.0.0.31      //Ventas -> Finanzas ❌
access-list 102 deny ip 130.10.0.96 0.0.0.15 130.10.0.160 0.0.0.31      //Ventas -> Logística ❌
access-list 102 deny ip 130.10.0.96 0.0.0.15 130.10.0.0 0.0.0.63      //Ventas -> Administración ❌
access-list 102 deny ip 130.10.0.96 0.0.0.15 130.10.1.64 0.0.0.15      //Ventas -> Sistemas ❌
access-list 102 deny ip 130.10.0.96 0.0.0.15 130.10.1.80 0.0.0.15      //Ventas -> Marketing ❌
access-list 102 deny ip 130.10.0.96 0.0.0.15 130.10.1.128 0.0.0.31      //Ventas -> Finanzas ❌
access-list 102 deny ip 130.10.0.96 0.0.0.15 130.10.1.160 0.0.0.31      //Ventas -> Logística ❌
access-list 102 deny ip 130.10.0.96 0.0.0.15 130.10.1.0 0.0.0.63      //Ventas -> Administración ❌
access-list 102 deny ip 130.10.0.96 0.0.0.15 130.10.2.64 0.0.0.15      //Ventas -> Sistemas ❌
access-list 102 deny ip 130.10.0.96 0.0.0.15 130.10.2.80 0.0.0.15      //Ventas -> Marketing ❌
access-list 102 deny ip 130.10.0.96 0.0.0.15 130.10.2.128 0.0.0.31      //Ventas -> Finanzas ❌
access-list 102 deny ip 130.10.0.96 0.0.0.15 130.10.2.160 0.0.0.31      //Ventas -> Logística ❌
access-list 102 deny ip 130.10.0.96 0.0.0.15 130.10.2.0 0.0.0.63      //Ventas -> Administración ❌
access-list 102 deny ip 130.10.0.128 0.0.0.31 130.10.0.64 0.0.0.15      //Finanzas -> Sistemas ❌
access-list 102 deny ip 130.10.0.128 0.0.0.31 130.10.0.80 0.0.0.15      //Finanzas -> Marketing ❌
access-list 102 deny ip 130.10.0.128 0.0.0.31 130.10.0.96 0.0.0.15      //Finanzas -> Ventas ❌
access-list 102 deny ip 130.10.0.128 0.0.0.31 130.10.0.160 0.0.0.31      //Finanzas -> Logística ❌
access-list 102 deny ip 130.10.0.128 0.0.0.31 130.10.0.0 0.0.0.63      //Finanzas -> Administración ❌
access-list 102 deny ip 130.10.0.128 0.0.0.31 130.10.1.64 0.0.0.15      //Finanzas -> Sistemas ❌
access-list 102 deny ip 130.10.0.128 0.0.0.31 130.10.1.80 0.0.0.15      //Finanzas -> Marketing ❌
access-list 102 deny ip 130.10.0.128 0.0.0.31 130.10.1.96 0.0.0.15      //Finanzas -> Ventas ❌
access-list 102 deny ip 130.10.0.128 0.0.0.31 130.10.1.160 0.0.0.31      //Finanzas -> Logística ❌
access-list 102 deny ip 130.10.0.128 0.0.0.31 130.10.1.0 0.0.0.63      //Finanzas -> Administración ❌
access-list 102 deny ip 130.10.0.128 0.0.0.31 130.10.2.64 0.0.0.15      //Finanzas -> Sistemas ❌
access-list 102 deny ip 130.10.0.128 0.0.0.31 130.10.2.80 0.0.0.15      //Finanzas -> Marketing ❌
access-list 102 deny ip 130.10.0.128 0.0.0.31 130.10.2.96 0.0.0.15      //Finanzas -> Ventas ❌
access-list 102 deny ip 130.10.0.128 0.0.0.31 130.10.2.160 0.0.0.31      //Finanzas -> Logística ❌
access-list 102 deny ip 130.10.0.128 0.0.0.31 130.10.2.0 0.0.0.63      //Finanzas -> Administración ❌
access-list 102 deny ip 130.10.0.160 0.0.0.31 130.10.0.64 0.0.0.15      //Logística -> Sistemas ❌
access-list 102 deny ip 130.10.0.160 0.0.0.31 130.10.0.80 0.0.0.15      //Logística -> Marketing ❌
access-list 102 deny ip 130.10.0.160 0.0.0.31 130.10.0.96 0.0.0.15      //Logística -> Ventas ❌
access-list 102 deny ip 130.10.0.160 0.0.0.31 130.10.0.128 0.0.0.31      //Logística -> Finanzas ❌
access-list 102 deny ip 130.10.0.160 0.0.0.31 130.10.0.0 0.0.0.63      //Logística -> Administración ❌
access-list 102 deny ip 130.10.0.160 0.0.0.31 130.10.1.64 0.0.0.15      //Logística -> Sistemas ❌
access-list 102 deny ip 130.10.0.160 0.0.0.31 130.10.1.80 0.0.0.15      //Logística -> Marketing ❌
access-list 102 deny ip 130.10.0.160 0.0.0.31 130.10.1.96 0.0.0.15      //Logística -> Ventas ❌
access-list 102 deny ip 130.10.0.160 0.0.0.31 130.10.1.128 0.0.0.31      //Logística -> Finanzas ❌
access-list 102 deny ip 130.10.0.160 0.0.0.31 130.10.1.0 0.0.0.63      //Logística -> Administración ❌
access-list 102 deny ip 130.10.0.160 0.0.0.31 130.10.2.64 0.0.0.15      //Logística -> Sistemas ❌
access-list 102 deny ip 130.10.0.160 0.0.0.31 130.10.2.80 0.0.0.15      //Logística -> Marketing ❌
access-list 102 deny ip 130.10.0.160 0.0.0.31 130.10.2.96 0.0.0.15      //Logística -> Ventas ❌
access-list 102 deny ip 130.10.0.160 0.0.0.31 130.10.2.128 0.0.0.31      //Logística -> Finanzas ❌
access-list 102 deny ip 130.10.0.160 0.0.0.31 130.10.2.0 0.0.0.63      //Logística -> Administración ❌

Router(config)#access-list 102 permit ip any any      //Permitir el resto (como respuestas, navegación, etc.)

Router(config)#interface f0/0.10      //Cambiar el número de acuerdo al área correspondiente

Router(config-if)#ip access-group 102 in

Router(config-if)#exit


# CONFIGURACIÓN DE ACLS PARA LA COMUNICACIÓN ENTRE VLANS SOLO PARA LONDRES

Router>ENA

Router#configure ter

access-list 102 deny ip 130.10.1.0 0.0.0.63 130.10.1.80 0.0.0.15      //Administración -> Marketing ❌
access-list 102 deny ip 130.10.1.0 0.0.0.63 130.10.1.96 0.0.0.15      //Administración -> Ventas ❌
access-list 102 deny ip 130.10.1.0 0.0.0.63 130.10.1.128 0.0.0.31      //Administración -> Finanzas ❌
access-list 102 deny ip 130.10.1.0 0.0.0.63 130.10.1.160 0.0.0.31      //Administración -> Logística ❌
access-list 102 deny ip 130.10.1.0 0.0.0.63 130.10.1.64 0.0.0.15      //Administración -> Sistemas ❌
access-list 102 deny ip 130.10.1.0 0.0.0.63 130.10.2.80 0.0.0.15      //Administración -> Marketing ❌
access-list 102 deny ip 130.10.1.0 0.0.0.63 130.10.2.96 0.0.0.15      //Administración -> Ventas ❌
access-list 102 deny ip 130.10.1.0 0.0.0.63 130.10.2.128 0.0.0.31      //Administración -> Finanzas ❌
access-list 102 deny ip 130.10.1.0 0.0.0.63 130.10.2.160 0.0.0.31      //Administración -> Logística ❌
access-list 102 deny ip 130.10.1.0 0.0.0.63 130.10.2.64 0.0.0.15      //Administración -> Sistemas ❌
access-list 102 deny ip 130.10.1.0 0.0.0.63 130.10.0.80 0.0.0.15      //Administración -> Marketing ❌
access-list 102 deny ip 130.10.1.0 0.0.0.63 130.10.0.96 0.0.0.15      //Administración -> Ventas ❌
access-list 102 deny ip 130.10.1.0 0.0.0.63 130.10.0.128 0.0.0.31      //Administración -> Finanzas ❌
access-list 102 deny ip 130.10.1.0 0.0.0.63 130.10.0.160 0.0.0.31      //Administración -> Logística ❌
access-list 102 deny ip 130.10.1.0 0.0.0.63 130.10.0.64 0.0.0.15      //Administración -> Sistemas ❌
access-list 102 deny ip 130.10.1.64 0.0.0.15 130.10.1.80 0.0.0.15      //Sistemas -> Marketing ❌
access-list 102 deny ip 130.10.1.64 0.0.0.15 130.10.1.96 0.0.0.15      //Sistemas -> Ventas ❌
access-list 102 deny ip 130.10.1.64 0.0.0.15 130.10.1.128 0.0.0.31      //Sistemas -> Finanzas ❌
access-list 102 deny ip 130.10.1.64 0.0.0.15 130.10.1.160 0.0.0.31      //Sistemas -> Logística ❌
access-list 102 deny ip 130.10.1.64 0.0.0.15 130.10.1.0 0.0.0.63      //Sistemas -> Administración ❌
access-list 102 deny ip 130.10.1.64 0.0.0.15 130.10.0.80 0.0.0.15      //Sistemas -> Marketing ❌
access-list 102 deny ip 130.10.1.64 0.0.0.15 130.10.0.96 0.0.0.15      //Sistemas -> Ventas ❌
access-list 102 deny ip 130.10.1.64 0.0.0.15 130.10.0.128 0.0.0.31      //Sistemas -> Finanzas ❌
access-list 102 deny ip 130.10.1.64 0.0.0.15 130.10.0.160 0.0.0.31      //Sistemas -> Logística ❌
access-list 102 deny ip 130.10.1.64 0.0.0.15 130.10.0.0 0.0.0.63      //Sistemas -> Administración ❌
access-list 102 deny ip 130.10.1.64 0.0.0.15 130.10.2.80 0.0.0.15      //Sistemas -> Marketing ❌
access-list 102 deny ip 130.10.1.64 0.0.0.15 130.10.2.96 0.0.0.15      //Sistemas -> Ventas ❌
access-list 102 deny ip 130.10.1.64 0.0.0.15 130.10.2.128 0.0.0.31      //Sistemas -> Finanzas ❌
access-list 102 deny ip 130.10.1.64 0.0.0.15 130.10.2.160 0.0.0.31      //Sistemas -> Logística ❌
access-list 102 deny ip 130.10.1.64 0.0.0.15 130.10.2.0 0.0.0.63      //Sistemas -> Administración ❌
access-list 102 deny ip 130.10.1.80 0.0.0.15 130.10.1.64 0.0.0.15      //Marketing -> Sistemas ❌
access-list 102 deny ip 130.10.1.80 0.0.0.15 130.10.1.96 0.0.0.15      //Marketing -> Ventas ❌
access-list 102 deny ip 130.10.1.80 0.0.0.15 130.10.1.128 0.0.0.31      //Marketing -> Finanzas ❌
access-list 102 deny ip 130.10.1.80 0.0.0.15 130.10.1.160 0.0.0.31      //Marketing -> Logística ❌
access-list 102 deny ip 130.10.1.80 0.0.0.15 130.10.1.0 0.0.0.63      //Marketing -> Administración ❌
access-list 102 deny ip 130.10.1.80 0.0.0.15 130.10.0.64 0.0.0.15      //Marketing -> Sistemas ❌
access-list 102 deny ip 130.10.1.80 0.0.0.15 130.10.0.96 0.0.0.15      //Marketing -> Ventas ❌
access-list 102 deny ip 130.10.1.80 0.0.0.15 130.10.0.128 0.0.0.31      //Marketing -> Finanzas ❌
access-list 102 deny ip 130.10.1.80 0.0.0.15 130.10.0.160 0.0.0.31      //Marketing -> Logística ❌
access-list 102 deny ip 130.10.1.80 0.0.0.15 130.10.0.0 0.0.0.63      //Marketing -> Administración ❌
access-list 102 deny ip 130.10.1.80 0.0.0.15 130.10.2.64 0.0.0.15      //Marketing -> Sistemas ❌
access-list 102 deny ip 130.10.1.80 0.0.0.15 130.10.2.96 0.0.0.15      //Marketing -> Ventas ❌
access-list 102 deny ip 130.10.1.80 0.0.0.15 130.10.2.128 0.0.0.31      //Marketing -> Finanzas ❌
access-list 102 deny ip 130.10.1.80 0.0.0.15 130.10.2.160 0.0.0.31      //Marketing -> Logística ❌
access-list 102 deny ip 130.10.1.80 0.0.0.15 130.10.2.0 0.0.0.63      //Marketing -> Administración ❌
access-list 102 deny ip 130.10.1.96 0.0.0.15 130.10.1.64 0.0.0.15      //Ventas -> Sistemas ❌
access-list 102 deny ip 130.10.1.96 0.0.0.15 130.10.1.80 0.0.0.15      //Ventas -> Marketing ❌
access-list 102 deny ip 130.10.1.96 0.0.0.15 130.10.1.128 0.0.0.31      //Ventas -> Finanzas ❌
access-list 102 deny ip 130.10.1.96 0.0.0.15 130.10.1.160 0.0.0.31      //Ventas -> Logística ❌
access-list 102 deny ip 130.10.1.96 0.0.0.15 130.10.1.0 0.0.0.63      //Ventas -> Administración ❌
access-list 102 deny ip 130.10.1.96 0.0.0.15 130.10.0.64 0.0.0.15      //Ventas -> Sistemas ❌
access-list 102 deny ip 130.10.1.96 0.0.0.15 130.10.0.80 0.0.0.15      //Ventas -> Marketing ❌
access-list 102 deny ip 130.10.1.96 0.0.0.15 130.10.0.128 0.0.0.31      //Ventas -> Finanzas ❌
access-list 102 deny ip 130.10.1.96 0.0.0.15 130.10.0.160 0.0.0.31      //Ventas -> Logística ❌
access-list 102 deny ip 130.10.1.96 0.0.0.15 130.10.0.0 0.0.0.63      //Ventas -> Administración ❌
access-list 102 deny ip 130.10.1.96 0.0.0.15 130.10.2.64 0.0.0.15      //Ventas -> Sistemas ❌
access-list 102 deny ip 130.10.1.96 0.0.0.15 130.10.2.80 0.0.0.15      //Ventas -> Marketing ❌
access-list 102 deny ip 130.10.1.96 0.0.0.15 130.10.2.128 0.0.0.31      //Ventas -> Finanzas ❌
access-list 102 deny ip 130.10.1.96 0.0.0.15 130.10.2.160 0.0.0.31      //Ventas -> Logística ❌
access-list 102 deny ip 130.10.1.96 0.0.0.15 130.10.2.0 0.0.0.63      //Ventas -> Administración ❌
access-list 102 deny ip 130.10.1.128 0.0.0.31 130.10.1.64 0.0.0.15      //Finanzas -> Sistemas ❌
access-list 102 deny ip 130.10.1.128 0.0.0.31 130.10.1.80 0.0.0.15      //Finanzas -> Marketing ❌
access-list 102 deny ip 130.10.1.128 0.0.0.31 130.10.1.96 0.0.0.15      //Finanzas -> Ventas ❌
access-list 102 deny ip 130.10.1.128 0.0.0.31 130.10.1.160 0.0.0.31      //Finanzas -> Logística ❌
access-list 102 deny ip 130.10.1.128 0.0.0.31 130.10.1.0 0.0.0.63      //Finanzas -> Administración ❌
access-list 102 deny ip 130.10.1.128 0.0.0.31 130.10.0.64 0.0.0.15      //Finanzas -> Sistemas ❌
access-list 102 deny ip 130.10.1.128 0.0.0.31 130.10.0.80 0.0.0.15      //Finanzas -> Marketing ❌
access-list 102 deny ip 130.10.1.128 0.0.0.31 130.10.0.96 0.0.0.15      //Finanzas -> Ventas ❌
access-list 102 deny ip 130.10.1.128 0.0.0.31 130.10.0.160 0.0.0.31      //Finanzas -> Logística ❌
access-list 102 deny ip 130.10.1.128 0.0.0.31 130.10.0.0 0.0.0.63      //Finanzas -> Administración ❌
access-list 102 deny ip 130.10.1.128 0.0.0.31 130.10.2.64 0.0.0.15      //Finanzas -> Sistemas ❌
access-list 102 deny ip 130.10.1.128 0.0.0.31 130.10.2.80 0.0.0.15      //Finanzas -> Marketing ❌
access-list 102 deny ip 130.10.1.128 0.0.0.31 130.10.2.96 0.0.0.15      //Finanzas -> Ventas ❌
access-list 102 deny ip 130.10.1.128 0.0.0.31 130.10.2.160 0.0.0.31      //Finanzas -> Logística ❌
access-list 102 deny ip 130.10.1.128 0.0.0.31 130.10.2.0 0.0.0.63      //Finanzas -> Administración ❌
access-list 102 deny ip 130.10.1.160 0.0.0.31 130.10.1.64 0.0.0.15      //Logística -> Sistemas ❌
access-list 102 deny ip 130.10.1.160 0.0.0.31 130.10.1.80 0.0.0.15      //Logística -> Marketing ❌
access-list 102 deny ip 130.10.1.160 0.0.0.31 130.10.1.96 0.0.0.15      //Logística -> Ventas ❌
access-list 102 deny ip 130.10.1.160 0.0.0.31 130.10.1.128 0.0.0.31      //Logística -> Finanzas ❌
access-list 102 deny ip 130.10.1.160 0.0.0.31 130.10.1.0 0.0.0.63      //Logística -> Administración ❌
access-list 102 deny ip 130.10.1.160 0.0.0.31 130.10.0.64 0.0.0.15      //Logística -> Sistemas ❌
access-list 102 deny ip 130.10.1.160 0.0.0.31 130.10.0.80 0.0.0.15      //Logística -> Marketing ❌
access-list 102 deny ip 130.10.1.160 0.0.0.31 130.10.0.96 0.0.0.15      //Logística -> Ventas ❌
access-list 102 deny ip 130.10.1.160 0.0.0.31 130.10.0.128 0.0.0.31      //Logística -> Finanzas ❌
access-list 102 deny ip 130.10.1.160 0.0.0.31 130.10.0.0 0.0.0.63      //Logística -> Administración ❌
access-list 102 deny ip 130.10.1.160 0.0.0.31 130.10.2.64 0.0.0.15      //Logística -> Sistemas ❌
access-list 102 deny ip 130.10.1.160 0.0.0.31 130.10.2.80 0.0.0.15      //Logística -> Marketing ❌
access-list 102 deny ip 130.10.1.160 0.0.0.31 130.10.2.96 0.0.0.15      //Logística -> Ventas ❌
access-list 102 deny ip 130.10.1.160 0.0.0.31 130.10.2.128 0.0.0.31      //Logística -> Finanzas ❌
access-list 102 deny ip 130.10.1.160 0.0.0.31 130.10.2.0 0.0.0.63      //Logística -> Administración ❌


Router(config)#access-list 102 permit ip any any      //Permitir el resto (como respuestas, navegación, etc.)

Router(config)#interface f0/0.10      //Cambiar el número de acuerdo al área correspondiente

Router(config-if)#ip access-group 102 in

Router(config-if)#exit


# CONFIGURACIÓN DE ACLS PARA LA COMUNICACIÓN ENTRE VLANS SOLO PARA París 

Router>ENA

Router#configure ter

access-list 102 deny ip 130.10.2.0 0.0.0.63 130.10.2.80 0.0.0.15      //Administración -> Marketing ❌
access-list 102 deny ip 130.10.2.0 0.0.0.63 130.10.2.96 0.0.0.15      //Administración -> Ventas ❌
access-list 102 deny ip 130.10.2.0 0.0.0.63 130.10.2.128 0.0.0.31      //Administración -> Finanzas ❌
access-list 102 deny ip 130.10.2.0 0.0.0.63 130.10.2.160 0.0.0.31      //Administración -> Logística ❌
access-list 102 deny ip 130.10.2.0 0.0.0.63 130.10.2.64 0.0.0.15      //Administración -> Sistemas ❌
access-list 102 deny ip 130.10.2.0 0.0.0.63 130.10.0.80 0.0.0.15      //Administración -> Marketing ❌
access-list 102 deny ip 130.10.2.0 0.0.0.63 130.10.0.96 0.0.0.15      //Administración -> Ventas ❌
access-list 102 deny ip 130.10.2.0 0.0.0.63 130.10.0.128 0.0.0.31      //Administración -> Finanzas ❌
access-list 102 deny ip 130.10.2.0 0.0.0.63 130.10.0.160 0.0.0.31      //Administración -> Logística ❌
access-list 102 deny ip 130.10.2.0 0.0.0.63 130.10.0.64 0.0.0.15      //Administración -> Sistemas ❌
access-list 102 deny ip 130.10.2.0 0.0.0.63 130.10.1.80 0.0.0.15      //Administración -> Marketing ❌
access-list 102 deny ip 130.10.2.0 0.0.0.63 130.10.1.96 0.0.0.15      //Administración -> Ventas ❌
access-list 102 deny ip 130.10.2.0 0.0.0.63 130.10.1.128 0.0.0.31      //Administración -> Finanzas ❌
access-list 102 deny ip 130.10.2.0 0.0.0.63 130.10.1.160 0.0.0.31      //Administración -> Logística ❌
access-list 102 deny ip 130.10.2.0 0.0.0.63 130.10.1.64 0.0.0.15      //Administración -> Sistemas ❌
access-list 102 deny ip 130.10.2.64 0.0.0.15 130.10.2.80 0.0.0.15      //Sistemas -> Marketing ❌
access-list 102 deny ip 130.10.2.64 0.0.0.15 130.10.2.96 0.0.0.15      //Sistemas -> Ventas ❌
access-list 102 deny ip 130.10.2.64 0.0.0.15 130.10.2.128 0.0.0.31      //Sistemas -> Finanzas ❌
access-list 102 deny ip 130.10.2.64 0.0.0.15 130.10.2.160 0.0.0.31      //Sistemas -> Logística ❌
access-list 102 deny ip 130.10.2.64 0.0.0.15 130.10.2.0 0.0.0.63      //Sistemas -> Administración ❌
access-list 102 deny ip 130.10.2.64 0.0.0.15 130.10.1.80 0.0.0.15      //Sistemas -> Marketing ❌
access-list 102 deny ip 130.10.2.64 0.0.0.15 130.10.1.96 0.0.0.15      //Sistemas -> Ventas ❌
access-list 102 deny ip 130.10.2.64 0.0.0.15 130.10.1.128 0.0.0.31      //Sistemas -> Finanzas ❌
access-list 102 deny ip 130.10.2.64 0.0.0.15 130.10.1.160 0.0.0.31      //Sistemas -> Logística ❌
access-list 102 deny ip 130.10.2.64 0.0.0.15 130.10.1.0 0.0.0.63      //Sistemas -> Administración ❌
access-list 102 deny ip 130.10.2.64 0.0.0.15 130.10.0.80 0.0.0.15      //Sistemas -> Marketing ❌
access-list 102 deny ip 130.10.2.64 0.0.0.15 130.10.0.96 0.0.0.15      //Sistemas -> Ventas ❌
access-list 102 deny ip 130.10.2.64 0.0.0.15 130.10.0.128 0.0.0.31      //Sistemas -> Finanzas ❌
access-list 102 deny ip 130.10.2.64 0.0.0.15 130.10.0.160 0.0.0.31      //Sistemas -> Logística ❌
access-list 102 deny ip 130.10.2.64 0.0.0.15 130.10.0.0 0.0.0.63      //Sistemas -> Administración ❌
access-list 102 deny ip 130.10.2.80 0.0.0.15 130.10.2.64 0.0.0.15      //Marketing -> Sistemas ❌
access-list 102 deny ip 130.10.2.80 0.0.0.15 130.10.2.96 0.0.0.15      //Marketing -> Ventas ❌
access-list 102 deny ip 130.10.2.80 0.0.0.15 130.10.2.128 0.0.0.31      //Marketing -> Finanzas ❌
access-list 102 deny ip 130.10.2.80 0.0.0.15 130.10.2.160 0.0.0.31      //Marketing -> Logística ❌
access-list 102 deny ip 130.10.2.80 0.0.0.15 130.10.2.0 0.0.0.63      //Marketing -> Administración ❌
access-list 102 deny ip 130.10.2.80 0.0.0.15 130.10.1.64 0.0.0.15      //Marketing -> Sistemas ❌
access-list 102 deny ip 130.10.2.80 0.0.0.15 130.10.1.96 0.0.0.15      //Marketing -> Ventas ❌
access-list 102 deny ip 130.10.2.80 0.0.0.15 130.10.1.128 0.0.0.31      //Marketing -> Finanzas ❌
access-list 102 deny ip 130.10.2.80 0.0.0.15 130.10.1.160 0.0.0.31      //Marketing -> Logística ❌
access-list 102 deny ip 130.10.2.80 0.0.0.15 130.10.1.0 0.0.0.63      //Marketing -> Administración ❌
access-list 102 deny ip 130.10.2.80 0.0.0.15 130.10.0.64 0.0.0.15      //Marketing -> Sistemas ❌
access-list 102 deny ip 130.10.2.80 0.0.0.15 130.10.0.96 0.0.0.15      //Marketing -> Ventas ❌
access-list 102 deny ip 130.10.2.80 0.0.0.15 130.10.0.128 0.0.0.31      //Marketing -> Finanzas ❌
access-list 102 deny ip 130.10.2.80 0.0.0.15 130.10.0.160 0.0.0.31      //Marketing -> Logística ❌
access-list 102 deny ip 130.10.2.80 0.0.0.15 130.10.0.0 0.0.0.63      //Marketing -> Administración ❌
access-list 102 deny ip 130.10.2.96 0.0.0.15 130.10.2.64 0.0.0.15      //Ventas -> Sistemas ❌
access-list 102 deny ip 130.10.2.96 0.0.0.15 130.10.2.80 0.0.0.15      //Ventas -> Marketing ❌
access-list 102 deny ip 130.10.2.96 0.0.0.15 130.10.2.128 0.0.0.31      //Ventas -> Finanzas ❌
access-list 102 deny ip 130.10.2.96 0.0.0.15 130.10.2.160 0.0.0.31      //Ventas -> Logística ❌
access-list 102 deny ip 130.10.2.96 0.0.0.15 130.10.2.0 0.0.0.63      //Ventas -> Administración ❌
access-list 102 deny ip 130.10.2.96 0.0.0.15 130.10.1.64 0.0.0.15      //Ventas -> Sistemas ❌
access-list 102 deny ip 130.10.2.96 0.0.0.15 130.10.1.80 0.0.0.15      //Ventas -> Marketing ❌
access-list 102 deny ip 130.10.2.96 0.0.0.15 130.10.1.128 0.0.0.31      //Ventas -> Finanzas ❌
access-list 102 deny ip 130.10.2.96 0.0.0.15 130.10.1.160 0.0.0.31      //Ventas -> Logística ❌
access-list 102 deny ip 130.10.2.96 0.0.0.15 130.10.1.0 0.0.0.63      //Ventas -> Administración ❌
access-list 102 deny ip 130.10.2.96 0.0.0.15 130.10.0.64 0.0.0.15      //Ventas -> Sistemas ❌
access-list 102 deny ip 130.10.2.96 0.0.0.15 130.10.0.80 0.0.0.15      //Ventas -> Marketing ❌
access-list 102 deny ip 130.10.2.96 0.0.0.15 130.10.0.128 0.0.0.31      //Ventas -> Finanzas ❌
access-list 102 deny ip 130.10.2.96 0.0.0.15 130.10.0.160 0.0.0.31      //Ventas -> Logística ❌
access-list 102 deny ip 130.10.2.96 0.0.0.15 130.10.0.0 0.0.0.63      //Ventas -> Administración ❌
access-list 102 deny ip 130.10.2.128 0.0.0.31 130.10.2.64 0.0.0.15      //Finanzas -> Sistemas ❌
access-list 102 deny ip 130.10.2.128 0.0.0.31 130.10.2.80 0.0.0.15      //Finanzas -> Marketing ❌
access-list 102 deny ip 130.10.2.128 0.0.0.31 130.10.2.96 0.0.0.15      //Finanzas -> Ventas ❌
access-list 102 deny ip 130.10.2.128 0.0.0.31 130.10.2.160 0.0.0.31      //Finanzas -> Logística ❌
access-list 102 deny ip 130.10.2.128 0.0.0.31 130.10.2.0 0.0.0.63      //Finanzas -> Administración ❌
access-list 102 deny ip 130.10.2.128 0.0.0.31 130.10.1.64 0.0.0.15      //Finanzas -> Sistemas ❌
access-list 102 deny ip 130.10.2.128 0.0.0.31 130.10.1.80 0.0.0.15      //Finanzas -> Marketing ❌
access-list 102 deny ip 130.10.2.128 0.0.0.31 130.10.1.96 0.0.0.15      //Finanzas -> Ventas ❌
access-list 102 deny ip 130.10.2.128 0.0.0.31 130.10.1.160 0.0.0.31      //Finanzas -> Logística ❌
access-list 102 deny ip 130.10.2.128 0.0.0.31 130.10.1.0 0.0.0.63      //Finanzas -> Administración ❌
access-list 102 deny ip 130.10.2.128 0.0.0.31 130.10.0.64 0.0.0.15      //Finanzas -> Sistemas ❌
access-list 102 deny ip 130.10.2.128 0.0.0.31 130.10.0.80 0.0.0.15      //Finanzas -> Marketing ❌
access-list 102 deny ip 130.10.2.128 0.0.0.31 130.10.0.96 0.0.0.15      //Finanzas -> Ventas ❌
access-list 102 deny ip 130.10.2.128 0.0.0.31 130.10.0.160 0.0.0.31      //Finanzas -> Logística ❌
access-list 102 deny ip 130.10.2.128 0.0.0.31 130.10.0.0 0.0.0.63      //Finanzas -> Administración ❌
access-list 102 deny ip 130.10.2.160 0.0.0.31 130.10.2.64 0.0.0.15      //Logística -> Sistemas ❌
access-list 102 deny ip 130.10.2.160 0.0.0.31 130.10.2.80 0.0.0.15      //Logística -> Marketing ❌
access-list 102 deny ip 130.10.2.160 0.0.0.31 130.10.2.96 0.0.0.15      //Logística -> Ventas ❌
access-list 102 deny ip 130.10.2.160 0.0.0.31 130.10.2.128 0.0.0.31      //Logística -> Finanzas ❌
access-list 102 deny ip 130.10.2.160 0.0.0.31 130.10.2.0 0.0.0.63      //Logística -> Administración ❌
access-list 102 deny ip 130.10.2.160 0.0.0.31 130.10.1.64 0.0.0.15      //Logística -> Sistemas ❌
access-list 102 deny ip 130.10.2.160 0.0.0.31 130.10.1.80 0.0.0.15      //Logística -> Marketing ❌
access-list 102 deny ip 130.10.2.160 0.0.0.31 130.10.1.96 0.0.0.15      //Logística -> Ventas ❌
access-list 102 deny ip 130.10.2.160 0.0.0.31 130.10.1.128 0.0.0.31      //Logística -> Finanzas ❌
access-list 102 deny ip 130.10.2.160 0.0.0.31 130.10.1.0 0.0.0.63      //Logística -> Administración ❌
access-list 102 deny ip 130.10.2.160 0.0.0.31 130.10.0.64 0.0.0.15      //Logística -> Sistemas ❌
access-list 102 deny ip 130.10.2.160 0.0.0.31 130.10.0.80 0.0.0.15      //Logística -> Marketing ❌
access-list 102 deny ip 130.10.2.160 0.0.0.31 130.10.0.96 0.0.0.15      //Logística -> Ventas ❌
access-list 102 deny ip 130.10.2.160 0.0.0.31 130.10.0.128 0.0.0.31      //Logística -> Finanzas ❌
access-list 102 deny ip 130.10.2.160 0.0.0.31 130.10.0.0 0.0.0.63      //Logística -> Administración ❌

Router(config)#access-list 102 permit ip any any      //Permitir el resto (como respuestas, navegación, etc.)

Router(config)#interface f0/0.1      //Cambiar el número de acuerdo al área correspondiente

Router(config-if)#ip access-group 102 in

Router(config-if)#exit



# EXTRA

Mostrar interfaces trunkas:
show interfaces trunk

Mostrar ips:
show ip int brief

Mostrar VLANs:
show vlan brief

Mostrar ACLs con matches:
show access-lists 100

Mostrar configuración:
show running-config


╒════════╤════════╤═════════════════╤═══════════╤═══════════════╤═══════════════╤═══════════════════════════════╤═══════════════╤═════════════════════╤════════════════════╤═══════════════════╤═════════════════╕
│ Sede   │ VLAN   │ Máscara         │ Prefijo   │ Red           │ Gateway       │ Rango usable                  │ Broadcast     │   Hosts disponibles │   Hosts requeridos │   Hosts sobrantes │ Wildcard Mask   │
╞════════╪════════╪═════════════════╪═══════════╪═══════════════╪═══════════════╪═══════════════════════════════╪═══════════════╪═════════════════════╪════════════════════╪═══════════════════╪═════════════════╡
│ Madrid │ ADMIN  │ 255.255.255.192 │ /26       │ 130.10.0.0    │ 130.10.0.1    │ 130.10.0.2 - 130.10.0.62      │ 130.10.0.63   │                  62 │                 31 │                31 │ 0.0.0.63        │
├────────┼────────┼─────────────────┼───────────┼───────────────┼───────────────┼───────────────────────────────┼───────────────┼─────────────────────┼────────────────────┼───────────────────┼─────────────────┤
│ Madrid │ VOICE  │ 255.255.255.192 │ /26       │ 130.10.0.64   │ 130.10.0.65   │ 130.10.0.66 - 130.10.0.126    │ 130.10.0.127  │                  62 │                 31 │                31 │ 0.0.0.63        │
├────────┼────────┼─────────────────┼───────────┼───────────────┼───────────────┼───────────────────────────────┼───────────────┼─────────────────────┼────────────────────┼───────────────────┼─────────────────┤
│ Madrid │ LOGIST │ 255.255.255.224 │ /27       │ 130.10.0.128  │ 130.10.0.129  │ 130.10.0.130 - 130.10.0.158   │ 130.10.0.159  │                  30 │                 17 │                13 │ 0.0.0.31        │
├────────┼────────┼─────────────────┼───────────┼───────────────┼───────────────┼───────────────────────────────┼───────────────┼─────────────────────┼────────────────────┼───────────────────┼─────────────────┤
│ Madrid │ FINANZ │ 255.255.255.224 │ /27       │ 130.10.0.160  │ 130.10.0.161  │ 130.10.0.162 - 130.10.0.190   │ 130.10.0.191  │                  30 │                 15 │                15 │ 0.0.0.31        │
├────────┼────────┼─────────────────┼───────────┼───────────────┼───────────────┼───────────────────────────────┼───────────────┼─────────────────────┼────────────────────┼───────────────────┼─────────────────┤
│ Madrid │ MARKET │ 255.255.255.240 │ /28       │ 130.10.0.192  │ 130.10.0.193  │ 130.10.0.194 - 130.10.0.206   │ 130.10.0.207  │                  14 │                  9 │                 5 │ 0.0.0.15        │
├────────┼────────┼─────────────────┼───────────┼───────────────┼───────────────┼───────────────────────────────┼───────────────┼─────────────────────┼────────────────────┼───────────────────┼─────────────────┤
│ Madrid │ SISTEM │ 255.255.255.240 │ /28       │ 130.10.0.208  │ 130.10.0.209  │ 130.10.0.210 - 130.10.0.222   │ 130.10.0.223  │                  14 │                  7 │                 7 │ 0.0.0.15        │
├────────┼────────┼─────────────────┼───────────┼───────────────┼───────────────┼───────────────────────────────┼───────────────┼─────────────────────┼────────────────────┼───────────────────┼─────────────────┤
│ Madrid │ VENTAS │ 255.255.255.248 │ /29       │ 130.10.0.224  │ 130.10.0.225  │ 130.10.0.226 - 130.10.0.230   │ 130.10.0.231  │                   6 │                  6 │                 0 │ 0.0.0.7         │
├────────┼────────┼─────────────────┼───────────┼───────────────┼───────────────┼───────────────────────────────┼───────────────┼─────────────────────┼────────────────────┼───────────────────┼─────────────────┤
│ London │ ADMIN  │ 255.255.255.192 │ /26       │ 130.10.32.0   │ 130.10.32.1   │ 130.10.32.2 - 130.10.32.62    │ 130.10.32.63  │                  62 │                 31 │                31 │ 0.0.0.63        │
├────────┼────────┼─────────────────┼───────────┼───────────────┼───────────────┼───────────────────────────────┼───────────────┼─────────────────────┼────────────────────┼───────────────────┼─────────────────┤
│ London │ VOICE  │ 255.255.255.192 │ /26       │ 130.10.32.64  │ 130.10.32.65  │ 130.10.32.66 - 130.10.32.126  │ 130.10.32.127 │                  62 │                 31 │                31 │ 0.0.0.63        │
├────────┼────────┼─────────────────┼───────────┼───────────────┼───────────────┼───────────────────────────────┼───────────────┼─────────────────────┼────────────────────┼───────────────────┼─────────────────┤
│ London │ LOGIST │ 255.255.255.224 │ /27       │ 130.10.32.128 │ 130.10.32.129 │ 130.10.32.130 - 130.10.32.158 │ 130.10.32.159 │                  30 │                 17 │                13 │ 0.0.0.31        │
├────────┼────────┼─────────────────┼───────────┼───────────────┼───────────────┼───────────────────────────────┼───────────────┼─────────────────────┼────────────────────┼───────────────────┼─────────────────┤
│ London │ FINANZ │ 255.255.255.224 │ /27       │ 130.10.32.160 │ 130.10.32.161 │ 130.10.32.162 - 130.10.32.190 │ 130.10.32.191 │                  30 │                 15 │                15 │ 0.0.0.31        │
├────────┼────────┼─────────────────┼───────────┼───────────────┼───────────────┼───────────────────────────────┼───────────────┼─────────────────────┼────────────────────┼───────────────────┼─────────────────┤
│ London │ MARKET │ 255.255.255.240 │ /28       │ 130.10.32.192 │ 130.10.32.193 │ 130.10.32.194 - 130.10.32.206 │ 130.10.32.207 │                  14 │                  9 │                 5 │ 0.0.0.15        │
├────────┼────────┼─────────────────┼───────────┼───────────────┼───────────────┼───────────────────────────────┼───────────────┼─────────────────────┼────────────────────┼───────────────────┼─────────────────┤
│ London │ SISTEM │ 255.255.255.240 │ /28       │ 130.10.32.208 │ 130.10.32.209 │ 130.10.32.210 - 130.10.32.222 │ 130.10.32.223 │                  14 │                  7 │                 7 │ 0.0.0.15        │
├────────┼────────┼─────────────────┼───────────┼───────────────┼───────────────┼───────────────────────────────┼───────────────┼─────────────────────┼────────────────────┼───────────────────┼─────────────────┤
│ London │ VENTAS │ 255.255.255.248 │ /29       │ 130.10.32.224 │ 130.10.32.225 │ 130.10.32.226 - 130.10.32.230 │ 130.10.32.231 │                   6 │                  6 │                 0 │ 0.0.0.7         │
├────────┼────────┼─────────────────┼───────────┼───────────────┼───────────────┼───────────────────────────────┼───────────────┼─────────────────────┼────────────────────┼───────────────────┼─────────────────┤
│ París  │ ADMIN  │ 255.255.255.192 │ /26       │ 130.10.64.0   │ 130.10.64.1   │ 130.10.64.2 - 130.10.64.62    │ 130.10.64.63  │                  62 │                 31 │                31 │ 0.0.0.63        │
├────────┼────────┼─────────────────┼───────────┼───────────────┼───────────────┼───────────────────────────────┼───────────────┼─────────────────────┼────────────────────┼───────────────────┼─────────────────┤
│ París  │ VOICE  │ 255.255.255.192 │ /26       │ 130.10.64.64  │ 130.10.64.65  │ 130.10.64.66 - 130.10.64.126  │ 130.10.64.127 │                  62 │                 31 │                31 │ 0.0.0.63        │
├────────┼────────┼─────────────────┼───────────┼───────────────┼───────────────┼───────────────────────────────┼───────────────┼─────────────────────┼────────────────────┼───────────────────┼─────────────────┤
│ París  │ LOGIST │ 255.255.255.224 │ /27       │ 130.10.64.128 │ 130.10.64.129 │ 130.10.64.130 - 130.10.64.158 │ 130.10.64.159 │                  30 │                 17 │                13 │ 0.0.0.31        │
├────────┼────────┼─────────────────┼───────────┼───────────────┼───────────────┼───────────────────────────────┼───────────────┼─────────────────────┼────────────────────┼───────────────────┼─────────────────┤
│ París  │ FINANZ │ 255.255.255.224 │ /27       │ 130.10.64.160 │ 130.10.64.161 │ 130.10.64.162 - 130.10.64.190 │ 130.10.64.191 │                  30 │                 15 │                15 │ 0.0.0.31        │
├────────┼────────┼─────────────────┼───────────┼───────────────┼───────────────┼───────────────────────────────┼───────────────┼─────────────────────┼────────────────────┼───────────────────┼─────────────────┤
│ París  │ MARKET │ 255.255.255.240 │ /28       │ 130.10.64.192 │ 130.10.64.193 │ 130.10.64.194 - 130.10.64.206 │ 130.10.64.207 │                  14 │                  9 │                 5 │ 0.0.0.15        │
├────────┼────────┼─────────────────┼───────────┼───────────────┼───────────────┼───────────────────────────────┼───────────────┼─────────────────────┼────────────────────┼───────────────────┼─────────────────┤
│ París  │ SISTEM │ 255.255.255.240 │ /28       │ 130.10.64.208 │ 130.10.64.209 │ 130.10.64.210 - 130.10.64.222 │ 130.10.64.223 │                  14 │                  7 │                 7 │ 0.0.0.15        │
├────────┼────────┼─────────────────┼───────────┼───────────────┼───────────────┼───────────────────────────────┼───────────────┼─────────────────────┼────────────────────┼───────────────────┼─────────────────┤
│ París  │ VENTAS │ 255.255.255.248 │ /29       │ 130.10.64.224 │ 130.10.64.225 │ 130.10.64.226 - 130.10.64.230 │ 130.10.64.231 │                   6 │                  6 │                 0 │ 0.0.0.7         │
├────────┼────────┼─────────────────┼───────────┼───────────────┼───────────────┼───────────────────────────────┼───────────────┼─────────────────────┼────────────────────┼───────────────────┼─────────────────┤
│   RM -> RL      │ 255.255.255.252 │ /30       │ 130.10.96.0   │               │ 130.10.96.1 - 130.10.96.2     │ 130.10.96.3   │                   2 │                  2 │                 0 │ 0.0.0.3         │
├─────────────────┼─────────────────┼───────────┼───────────────┼───────────────┼───────────────────────────────┼───────────────┼─────────────────────┼────────────────────┼───────────────────┼─────────────────┤
│   RM -> RP      │ 255.255.255.252 │ /30       │ 130.10.128.0  │               │ 130.10.128.1 - 130.10.128.2   │ 130.10.128.3  │                   2 │                  2 │                 0 │ 0.0.0.3         │
├─────────────────┼─────────────────┼───────────┼───────────────┼───────────────┼───────────────────────────────┼───────────────┼─────────────────────┼────────────────────┼───────────────────┼─────────────────┤
│   RMadrid       │ 255.255.255.252 │ /30       │ 130.10.160.0  │               │ 130.10.160.1 - 130.10.160.2   │ 130.10.160.3  │                   2 │                  1 │                 1 │ 0.0.0.3         │
├─────────────────┼─────────────────┼───────────┼───────────────┼───────────────┼───────────────────────────────┼───────────────┼─────────────────────┼────────────────────┼───────────────────┼─────────────────┤
│   RLondres      │ 255.255.255.252 │ /30       │ 130.10.192.0  │               │ 130.10.192.1 - 130.10.192.2   │ 130.10.192.3  │                   2 │                  1 │                 1 │ 0.0.0.3         │
├─────────────────┼─────────────────┼───────────┼───────────────┼───────────────┼───────────────────────────────┼───────────────┼─────────────────────┼────────────────────┼───────────────────┼─────────────────┤
│   RParis        │ 255.255.255.252 │ /30       │ 130.10.224.0  │               │ 130.10.224.1 - 130.10.224.2   │ 130.10.224.3  │                   2 │                  1 │                 1 │ 0.0.0.3         │
├─────────────────┼─────────────────┼───────────┼───────────────┼───────────────┼───────────────────────────────┼───────────────┼─────────────────────┼────────────────────┼───────────────────┼─────────────────┤
│   RCMadrid      │ 255.255.255.252 │ /30       │ 130.10.129.0  │               │ 130.10.129.1 - 130.10.129.2   │ 130.10.129.3  │                   2 │                  2 │                 0 │ 0.0.0.3         │
├─────────────────┼─────────────────┼───────────┼───────────────┼───────────────┼───────────────────────────────┼───────────────┼─────────────────────┼────────────────────┼───────────────────┼─────────────────┤
│   RCLondres     │ 255.255.255.252 │ /30       │ 130.10.130.0  │               │ 130.10.130.1 - 130.10.130.2   │ 130.10.130.3  │                   2 │                  2 │                 0 │ 0.0.0.3         │
├─────────────────┼─────────────────┼───────────┼───────────────┼───────────────┼───────────────────────────────┼───────────────┼─────────────────────┼────────────────────┼───────────────────┼─────────────────┤
│   RCParis       │ 255.255.255.252 │ /30       │ 130.10.131.0  │               │ 130.10.131.1 - 130.10.131.2   │ 130.10.131.3  │                   2 │                  2 │                 0 │ 0.0.0.3         │
├─────────────────┼─────────────────┼───────────┼───────────────┼───────────────┼───────────────────────────────┼───────────────┼─────────────────────┼────────────────────┼───────────────────┼─────────────────┤
│   MServer       │ 255.255.255.252 │ /30       │ 130.10.132.0  │ 130.10.132.1  │ 130.10.132.2                  │ 130.10.132.3  │                   2 │                  2 │                 0 │ 0.0.0.3         │
├─────────────────┼─────────────────┼───────────┼───────────────┼───────────────┼───────────────────────────────┼───────────────┼─────────────────────┼────────────────────┼───────────────────┼─────────────────┤
│   LServer       │ 255.255.255.252 │ /30       │ 130.10.133.0  │ 130.10.133.1  │ 130.10.133.2                  │ 130.10.133.3  │                   2 │                  2 │                 0 │ 0.0.0.3         │
├─────────────────┼─────────────────┼───────────┼───────────────┼───────────────┼───────────────────────────────┼───────────────┼─────────────────────┼────────────────────┼───────────────────┼─────────────────┤
│   FServer       │ 255.255.255.252 │ /30       │ 130.10.134.0  │ 130.10.134.1  │ 130.10.133.2                  │ 130.10.134.3  │                   2 │                  2 │                 0 │ 0.0.0.3         │
├─────────────────┼─────────────────┼───────────┼───────────────┼───────────────┼───────────────────────────────┼───────────────┼─────────────────────┼────────────────────┼───────────────────┼─────────────────┤
│   RM -> C1      │ 255.255.255.252 │ /30       │ 130.10.135.0  │               │ 130.10.135.1 - 130.10.135.2   │ 130.10.135.3  │                   2 │                  2 │                 0 │ 0.0.0.3         │
├─────────────────┼─────────────────┼───────────┼───────────────┼───────────────┼───────────────────────────────┼───────────────┼─────────────────────┼────────────────────┼───────────────────┼─────────────────┤
│   RL -> C1      │ 255.255.255.252 │ /30       │ 130.10.136.0  │               │ 130.10.136.1 - 130.10.136.2   │ 130.10.136.3  │                   2 │                  2 │                 0 │ 0.0.0.3         │
├─────────────────┼─────────────────┼───────────┼───────────────┼───────────────┼───────────────────────────────┼───────────────┼─────────────────────┼────────────────────┼───────────────────┼─────────────────┤
│   RP -> C1      │ 255.255.255.252 │ /30       │ 130.10.137.0  │               │ 130.10.137.1 - 130.10.137.2   │ 130.10.137.3  │                   2 │                  2 │                 0 │ 0.0.0.3         │
├─────────────────┼─────────────────┼───────────┼───────────────┼───────────────┼───────────────────────────────┼───────────────┼─────────────────────┼────────────────────┼───────────────────┼─────────────────┤
│   RM -> C2      │ 255.255.255.252 │ /30       │ 130.10.138.0  │               │ 130.10.138.1 - 130.10.138.2   │ 130.10.138.3  │                   2 │                  2 │                 0 │ 0.0.0.3         │
├─────────────────┼─────────────────┼───────────┼───────────────┼───────────────┼───────────────────────────────┼───────────────┼─────────────────────┼────────────────────┼───────────────────┼─────────────────┤
│   RL -> C2      │ 255.255.255.252 │ /30       │ 130.10.139.0  │               │ 130.10.139.1 - 130.10.139.2   │ 130.10.139.3  │                   2 │                  2 │                 0 │ 0.0.0.3         │
├─────────────────┼─────────────────┼───────────┼───────────────┼───────────────┼───────────────────────────────┼───────────────┼─────────────────────┼────────────────────┼───────────────────┼─────────────────┤
│   RP -> C2      │ 255.255.255.252 │ /30       │ 130.10.140.0  │               │ 130.10.140.1 - 130.10.140.2   │ 130.10.140.3  │                   2 │                  2 │                 0 │ 0.0.0.3         │
├─────────────────┼─────────────────┼───────────┼───────────────┼───────────────┼───────────────────────────────┼───────────────┼─────────────────────┼────────────────────┼───────────────────┼─────────────────┤
│   RM -> RSM     │ 255.255.255.252 │ /30       │ 130.10.141.0  │               │ 130.10.141.1 - 130.10.141.2   │ 130.10.141.3  │                   2 │                  2 │                 0 │ 0.0.0.3         │
├─────────────────┼─────────────────┼───────────┼───────────────┼───────────────┼───────────────────────────────┼───────────────┼─────────────────────┼────────────────────┼───────────────────┼─────────────────┤
│   RL -> RSL     │ 255.255.255.252 │ /30       │ 130.10.142.0  │               │ 130.10.142.1 - 130.10.142.2   │ 130.10.142.3  │                   2 │                  2 │                 0 │ 0.0.0.3         │
├─────────────────┼─────────────────┼───────────┼───────────────┼───────────────┼───────────────────────────────┼───────────────┼─────────────────────┼────────────────────┼───────────────────┼─────────────────┤
│   RP -> RSP     │ 255.255.255.252 │ /30       │ 130.10.143.0  │               │ 130.10.143.1 - 130.10.143.2   │ 130.10.143.3  │                   2 │                  2 │                 0 │ 0.0.0.3         │
├─────────────────┼─────────────────┼───────────┼───────────────┼───────────────┼───────────────────────────────┼───────────────┼─────────────────────┼────────────────────┼───────────────────┼─────────────────┤
│   MServer2      │ 255.255.255.252 │ /30       │ 130.10.144.0  │               │ 130.10.144.1 - 130.10.144.2   │ 130.10.144.3  │                   2 │                  2 │                 0 │ 0.0.0.3         │
├─────────────────┼─────────────────┼───────────┼───────────────┼───────────────┼───────────────────────────────┼───────────────┼─────────────────────┼────────────────────┼───────────────────┼─────────────────┤
│   MServer3      │ 255.255.255.252 │ /30       │ 130.10.145.0  │               │ 130.10.145.1 - 130.10.145.2   │ 130.10.145.3  │                   2 │                  2 │                 0 │ 0.0.0.3         │
├─────────────────┼─────────────────┼───────────┼───────────────┼───────────────┼───────────────────────────────┼───────────────┼─────────────────────┼────────────────────┼───────────────────┼─────────────────┤
│   LServer2      │ 255.255.255.252 │ /30       │ 130.10.146.0  │               │ 130.10.146.1 - 130.10.146.2   │ 130.10.146.3  │                   2 │                  2 │                 0 │ 0.0.0.3         │
├─────────────────┼─────────────────┼───────────┼───────────────┼───────────────┼───────────────────────────────┼───────────────┼─────────────────────┼────────────────────┼───────────────────┼─────────────────┤
│   LServer3      │ 255.255.255.252 │ /30       │ 130.10.147.0  │               │ 130.10.146.1 - 130.10.146.2   │ 130.10.146.3  │                   2 │                  2 │                 0 │ 0.0.0.3         │
├─────────────────┼─────────────────┼───────────┼───────────────┼───────────────┼───────────────────────────────┼───────────────┼─────────────────────┼────────────────────┼───────────────────┼─────────────────┤
│   FServer2      │ 255.255.255.252 │ /30       │ 130.10.148.0  │               │ 130.10.146.1 - 130.10.146.2   │ 130.10.146.3  │                   2 │                  2 │                 0 │ 0.0.0.3         │
├─────────────────┼─────────────────┼───────────┼───────────────┼───────────────┼───────────────────────────────┼───────────────┼─────────────────────┼────────────────────┼───────────────────┼─────────────────┤
│   FServer3      │ 255.255.255.252 │ /30       │ 130.10.149.0  │               │ 130.10.147.1 - 130.10.147.2   │ 130.10.147.3  │                   2 │                  2 │                 0 │ 0.0.0.3         │┤
╘═════════════════╧═════════════════╧═══════════╧═══════════════╧═══════════════╧═══════════════════════════════╧═══════════════╧═════════════════════╧════════════════════╧═══════════════════╧═════════════════╛

Madrid (Router)

ip route 130.10.32.0 255.255.255.192 130.10.96.2
ip route 130.10.32.64 255.255.255.192 130.10.96.2
ip route 130.10.32.208 255.255.255.240 130.10.96.2
ip route 130.10.32.160 255.255.255.224 130.10.96.2
ip route 130.10.32.128 255.255.255.224 130.10.96.2
ip route 130.10.32.192 255.255.255.240 130.10.96.2
ip route 130.10.32.224 255.255.255.248 130.10.96.2
ip route 130.10.64.0 255.255.255.192 130.10.128.2
ip route 130.10.64.64 255.255.255.192 130.10.128.2
ip route 130.10.64.208 255.255.255.240 130.10.128.2
ip route 130.10.64.160 255.255.255.224 130.10.128.2
ip route 130.10.64.128 255.255.255.224 130.10.128.2
ip route 130.10.64.192 255.255.255.240 130.10.128.2
ip route 130.10.64.224 255.255.255.248 130.10.128.2
ip route 130.10.132.0 255.255.255.252 130.10.141.2

network 130.10.0.0
network 130.10.0.65
network 130.10.0.208
network 130.10.0.160
network 130.10.0.128
network 130.10.0.192
network 130.10.0.224
network 130.10.160.0
network 130.10.96.0
network 130.10.128.0


Server Madrid (Router)

ip route 130.10.0.0 255.255.255.192 130.10.141.1
ip route 130.10.0.64 255.255.255.192 130.10.141.1
ip route 130.10.0.208 255.255.255.240 130.10.141.1
ip route 130.10.0.160 255.255.255.224 130.10.141.1
ip route 130.10.0.128 255.255.255.224 130.10.141.1
ip route 130.10.0.192 255.255.255.240 130.10.141.1
ip route 130.10.0.224 255.255.255.248 130.10.141.1

ip route 130.10.32.0 255.255.255.192 130.10.142.1
ip route 130.10.32.64 255.255.255.192 130.10.142.1
ip route 130.10.32.208 255.255.255.240 130.10.142.1
ip route 130.10.32.160 255.255.255.224 130.10.142.1
ip route 130.10.32.128 255.255.255.224 130.10.142.1
ip route 130.10.32.192 255.255.255.240 130.10.142.1
ip route 130.10.32.224 255.255.255.248 130.10.142.1
ip route 130.10.64.0 255.255.255.192 130.10.143.1
ip route 130.10.64.64 255.255.255.192 130.10.143.1
ip route 130.10.64.208 255.255.255.240 130.10.143.1
ip route 130.10.64.160 255.255.255.224 130.10.143.1
ip route 130.10.64.128 255.255.255.224 130.10.143.1
ip route 130.10.64.192 255.255.255.240 130.10.143.1
ip route 130.10.64.224 255.255.255.248 130.10.143.1


router rip
version 2
no auto-summary
network 130.10.141.0
network 130.10.138.0
network 130.10.135.0
network 130.10.129.0
network 130.10.132.0



Londres (Router)

ip route 130.10.0.0 255.255.255.192 130.10.96.1
ip route 130.10.0.64 255.255.255.192 130.10.96.1
ip route 130.10.0.208 255.255.255.240 130.10.96.1
ip route 130.10.0.160 255.255.255.224 130.10.96.1
ip route 130.10.0.128 255.255.255.224 130.10.96.1
ip route 130.10.0.192 255.255.255.240 130.10.96.1
ip route 130.10.0.224 255.255.255.248 130.10.96.1
ip route 130.10.64.0 255.255.255.192 130.10.128.2
ip route 130.10.64.64 255.255.255.192 130.10.128.2
ip route 130.10.64.208 255.255.255.240 130.10.128.2
ip route 130.10.64.160 255.255.255.224 130.10.128.2
ip route 130.10.64.128 255.255.255.224 130.10.128.2
ip route 130.10.64.192 255.255.255.240 130.10.128.2
ip route 130.10.64.224 255.255.255.248 130.10.128.2

network 130.10.32.0
network 130.10.32.65
network 130.10.32.208
network 130.10.32.160
network 130.10.32.128
network 130.10.32.192
network 130.10.32.224
network 130.10.192.0
network 130.10.96.0

Server Madrid (Router)



Paris (Router)

ip route 130.10.32.0 255.255.255.192 130.10.96.2
ip route 130.10.32.64 255.255.255.192 130.10.96.2
ip route 130.10.32.208 255.255.255.240 130.10.96.2
ip route 130.10.32.160 255.255.255.224 130.10.96.2
ip route 130.10.32.128 255.255.255.224 130.10.96.2
ip route 130.10.32.192 255.255.255.240 130.10.96.2
ip route 130.10.32.224 255.255.255.248 130.10.96.2
ip route 130.10.0.0 255.255.255.192 130.10.128.1
ip route 130.10.0.64 255.255.255.192 130.10.128.1
ip route 130.10.0.208 255.255.255.240 130.10.128.1
ip route 130.10.0.160 255.255.255.224 130.10.128.1
ip route 130.10.0.128 255.255.255.224 130.10.128.1
ip route 130.10.0.192 255.255.255.240 130.10.128.1
ip route 130.10.0.224 255.255.255.248 130.10.128.1

network 130.10.64.0
network 130.10.64.65
network 130.10.64.208
network 130.10.64.160
network 130.10.64.128
network 130.10.64.192
network 130.10.64.224
network 130.10.224.0
network 130.10.128.0



access-list 100 deny ip 130.10.0.0 0.0.0.63 130.10.0.208 0.0.0.15
access-list 100 deny ip 130.10.0.0 0.0.0.63 130.10.32.208 0.0.0.15
access-list 100 deny ip 130.10.0.0 0.0.0.63 130.10.64.208 0.0.0.15
access-list 100 deny ip 130.10.0.0 0.0.0.63 130.10.0.160 0.0.0.31
access-list 100 deny ip 130.10.0.0 0.0.0.63 130.10.32.160 0.0.0.31
access-list 100 deny ip 130.10.0.0 0.0.0.63 130.10.64.160 0.0.0.31
access-list 100 deny ip 130.10.0.0 0.0.0.63 130.10.0.128 0.0.0.31
access-list 100 deny ip 130.10.0.0 0.0.0.63 130.10.32.128 0.0.0.31
access-list 100 deny ip 130.10.0.0 0.0.0.63 130.10.64.128 0.0.0.31
access-list 100 deny ip 130.10.0.0 0.0.0.63 130.10.0.192 0.0.0.15
access-list 100 deny ip 130.10.0.0 0.0.0.63 130.10.32.192 0.0.0.15
access-list 100 deny ip 130.10.0.0 0.0.0.63 130.10.64.192 0.0.0.15
access-list 100 deny ip 130.10.0.0 0.0.0.63 130.10.0.224 0.0.0.7
access-list 100 deny ip 130.10.0.0 0.0.0.63 130.10.32.224 0.0.0.7
access-list 100 deny ip 130.10.0.0 0.0.0.63 130.10.64.224 0.0.0.7

access-list 100 deny ip 130.10.32.0 0.0.0.63 130.10.0.208 0.0.0.15
access-list 100 deny ip 130.10.32.0 0.0.0.63 130.10.32.208 0.0.0.15
access-list 100 deny ip 130.10.32.0 0.0.0.63 130.10.64.208 0.0.0.15
access-list 100 deny ip 130.10.32.0 0.0.0.63 130.10.0.160 0.0.0.31
access-list 100 deny ip 130.10.32.0 0.0.0.63 130.10.32.160 0.0.0.31
access-list 100 deny ip 130.10.32.0 0.0.0.63 130.10.64.160 0.0.0.31
access-list 100 deny ip 130.10.32.0 0.0.0.63 130.10.0.128 0.0.0.31
access-list 100 deny ip 130.10.32.0 0.0.0.63 130.10.32.128 0.0.0.31
access-list 100 deny ip 130.10.32.0 0.0.0.63 130.10.64.128 0.0.0.31
access-list 100 deny ip 130.10.32.0 0.0.0.63 130.10.0.192 0.0.0.15
access-list 100 deny ip 130.10.32.0 0.0.0.63 130.10.32.192 0.0.0.15
access-list 100 deny ip 130.10.32.0 0.0.0.63 130.10.64.192 0.0.0.15
access-list 100 deny ip 130.10.32.0 0.0.0.63 130.10.0.224 0.0.0.7
access-list 100 deny ip 130.10.32.0 0.0.0.63 130.10.32.224 0.0.0.7
access-list 100 deny ip 130.10.32.0 0.0.0.63 130.10.64.224 0.0.0.7

access-list 100 deny ip 130.10.64.0 0.0.0.63 130.10.0.208 0.0.0.15
access-list 100 deny ip 130.10.64.0 0.0.0.63 130.10.32.208 0.0.0.15
access-list 100 deny ip 130.10.64.0 0.0.0.63 130.10.64.208 0.0.0.15
access-list 100 deny ip 130.10.64.0 0.0.0.63 130.10.0.160 0.0.0.31
access-list 100 deny ip 130.10.64.0 0.0.0.63 130.10.32.160 0.0.0.31
access-list 100 deny ip 130.10.64.0 0.0.0.63 130.10.64.160 0.0.0.31
access-list 100 deny ip 130.10.64.0 0.0.0.63 130.10.0.128 0.0.0.31
access-list 100 deny ip 130.10.64.0 0.0.0.63 130.10.32.128 0.0.0.31
access-list 100 deny ip 130.10.64.0 0.0.0.63 130.10.64.128 0.0.0.31
access-list 100 deny ip 130.10.64.0 0.0.0.63 130.10.0.192 0.0.0.15
access-list 100 deny ip 130.10.64.0 0.0.0.63 130.10.32.192 0.0.0.15
access-list 100 deny ip 130.10.64.0 0.0.0.63 130.10.64.192 0.0.0.15
access-list 100 deny ip 130.10.64.0 0.0.0.63 130.10.0.224 0.0.0.7
access-list 100 deny ip 130.10.64.0 0.0.0.63 130.10.32.224 0.0.0.7
access-list 100 deny ip 130.10.64.0 0.0.0.63 130.10.64.224 0.0.0.7

access-list 100 deny ip 130.10.0.208 0.0.0.15 130.10.0.0 0.0.0.63
access-list 100 deny ip 130.10.0.208 0.0.0.15 130.10.32.0 0.0.0.63
access-list 100 deny ip 130.10.0.208 0.0.0.15 130.10.64.0 0.0.0.63
access-list 100 deny ip 130.10.0.208 0.0.0.15 130.10.0.160 0.0.0.31
access-list 100 deny ip 130.10.0.208 0.0.0.15 130.10.32.160 0.0.0.31
access-list 100 deny ip 130.10.0.208 0.0.0.15 130.10.64.160 0.0.0.31
access-list 100 deny ip 130.10.0.208 0.0.0.15 130.10.0.128 0.0.0.31
access-list 100 deny ip 130.10.0.208 0.0.0.15 130.10.32.128 0.0.0.31
access-list 100 deny ip 130.10.0.208 0.0.0.15 130.10.64.128 0.0.0.31
access-list 100 deny ip 130.10.0.208 0.0.0.15 130.10.0.192 0.0.0.15
access-list 100 deny ip 130.10.0.208 0.0.0.15 130.10.32.192 0.0.0.15
access-list 100 deny ip 130.10.0.208 0.0.0.15 130.10.64.192 0.0.0.15
access-list 100 deny ip 130.10.0.208 0.0.0.15 130.10.0.224 0.0.0.7
access-list 100 deny ip 130.10.0.208 0.0.0.15 130.10.32.224 0.0.0.7
access-list 100 deny ip 130.10.0.208 0.0.0.15 130.10.64.224 0.0.0.7

access-list 100 deny ip 130.10.32.208 0.0.0.15 130.10.0.0 0.0.0.63
access-list 100 deny ip 130.10.32.208 0.0.0.15 130.10.32.0 0.0.0.63
access-list 100 deny ip 130.10.32.208 0.0.0.15 130.10.64.0 0.0.0.63
access-list 100 deny ip 130.10.32.208 0.0.0.15 130.10.0.160 0.0.0.31
access-list 100 deny ip 130.10.32.208 0.0.0.15 130.10.32.160 0.0.0.31
access-list 100 deny ip 130.10.32.208 0.0.0.15 130.10.64.160 0.0.0.31
access-list 100 deny ip 130.10.32.208 0.0.0.15 130.10.0.128 0.0.0.31
access-list 100 deny ip 130.10.32.208 0.0.0.15 130.10.32.128 0.0.0.31
access-list 100 deny ip 130.10.32.208 0.0.0.15 130.10.64.128 0.0.0.31
access-list 100 deny ip 130.10.32.208 0.0.0.15 130.10.0.192 0.0.0.15
access-list 100 deny ip 130.10.32.208 0.0.0.15 130.10.32.192 0.0.0.15
access-list 100 deny ip 130.10.32.208 0.0.0.15 130.10.64.192 0.0.0.15
access-list 100 deny ip 130.10.32.208 0.0.0.15 130.10.0.224 0.0.0.7
access-list 100 deny ip 130.10.32.208 0.0.0.15 130.10.32.224 0.0.0.7
access-list 100 deny ip 130.10.32.208 0.0.0.15 130.10.64.224 0.0.0.7

access-list 100 deny ip 130.10.64.208 0.0.0.15 130.10.0.0 0.0.0.63
access-list 100 deny ip 130.10.64.208 0.0.0.15 130.10.32.0 0.0.0.63
access-list 100 deny ip 130.10.64.208 0.0.0.15 130.10.64.0 0.0.0.63
access-list 100 deny ip 130.10.64.208 0.0.0.15 130.10.0.160 0.0.0.31
access-list 100 deny ip 130.10.64.208 0.0.0.15 130.10.32.160 0.0.0.31
access-list 100 deny ip 130.10.64.208 0.0.0.15 130.10.64.160 0.0.0.31
access-list 100 deny ip 130.10.64.208 0.0.0.15 130.10.0.128 0.0.0.31
access-list 100 deny ip 130.10.64.208 0.0.0.15 130.10.32.128 0.0.0.31
access-list 100 deny ip 130.10.64.208 0.0.0.15 130.10.64.128 0.0.0.31
access-list 100 deny ip 130.10.64.208 0.0.0.15 130.10.0.192 0.0.0.15
access-list 100 deny ip 130.10.64.208 0.0.0.15 130.10.32.192 0.0.0.15
access-list 100 deny ip 130.10.64.208 0.0.0.15 130.10.64.192 0.0.0.15
access-list 100 deny ip 130.10.64.208 0.0.0.15 130.10.0.224 0.0.0.7
access-list 100 deny ip 130.10.64.208 0.0.0.15 130.10.32.224 0.0.0.7
access-list 100 deny ip 130.10.64.208 0.0.0.15 130.10.64.224 0.0.0.7

access-list 100 deny ip 130.10.0.160 0.0.0.31 130.10.0.0 0.0.0.63
access-list 100 deny ip 130.10.0.160 0.0.0.31 130.10.32.0 0.0.0.63
access-list 100 deny ip 130.10.0.160 0.0.0.31 130.10.64.0 0.0.0.63
access-list 100 deny ip 130.10.0.160 0.0.0.31 130.10.0.208 0.0.0.15
access-list 100 deny ip 130.10.0.160 0.0.0.31 130.10.32.208 0.0.0.15
access-list 100 deny ip 130.10.0.160 0.0.0.31 130.10.64.208 0.0.0.15
access-list 100 deny ip 130.10.0.160 0.0.0.31 130.10.0.128 0.0.0.31
access-list 100 deny ip 130.10.0.160 0.0.0.31 130.10.32.128 0.0.0.31
access-list 100 deny ip 130.10.0.160 0.0.0.31 130.10.64.128 0.0.0.31
access-list 100 deny ip 130.10.0.160 0.0.0.31 130.10.0.192 0.0.0.15
access-list 100 deny ip 130.10.0.160 0.0.0.31 130.10.32.192 0.0.0.15
access-list 100 deny ip 130.10.0.160 0.0.0.31 130.10.64.192 0.0.0.15
access-list 100 deny ip 130.10.0.160 0.0.0.31 130.10.0.224 0.0.0.7
access-list 100 deny ip 130.10.0.160 0.0.0.31 130.10.32.224 0.0.0.7
access-list 100 deny ip 130.10.0.160 0.0.0.31 130.10.64.224 0.0.0.7

access-list 100 deny ip 130.10.32.160 0.0.0.31 130.10.0.0 0.0.0.63
access-list 100 deny ip 130.10.32.160 0.0.0.31 130.10.32.0 0.0.0.63
access-list 100 deny ip 130.10.32.160 0.0.0.31 130.10.64.0 0.0.0.63
access-list 100 deny ip 130.10.32.160 0.0.0.31 130.10.0.208 0.0.0.15
access-list 100 deny ip 130.10.32.160 0.0.0.31 130.10.32.208 0.0.0.15
access-list 100 deny ip 130.10.32.160 0.0.0.31 130.10.64.208 0.0.0.15
access-list 100 deny ip 130.10.32.160 0.0.0.31 130.10.0.128 0.0.0.31
access-list 100 deny ip 130.10.32.160 0.0.0.31 130.10.32.128 0.0.0.31
access-list 100 deny ip 130.10.32.160 0.0.0.31 130.10.64.128 0.0.0.31
access-list 100 deny ip 130.10.32.160 0.0.0.31 130.10.0.192 0.0.0.15
access-list 100 deny ip 130.10.32.160 0.0.0.31 130.10.32.192 0.0.0.15
access-list 100 deny ip 130.10.32.160 0.0.0.31 130.10.64.192 0.0.0.15
access-list 100 deny ip 130.10.32.160 0.0.0.31 130.10.0.224 0.0.0.7
access-list 100 deny ip 130.10.32.160 0.0.0.31 130.10.32.224 0.0.0.7
access-list 100 deny ip 130.10.32.160 0.0.0.31 130.10.64.224 0.0.0.7

access-list 100 deny ip 130.10.64.160 0.0.0.31 130.10.0.0 0.0.0.63
access-list 100 deny ip 130.10.64.160 0.0.0.31 130.10.32.0 0.0.0.63
access-list 100 deny ip 130.10.64.160 0.0.0.31 130.10.64.0 0.0.0.63
access-list 100 deny ip 130.10.64.160 0.0.0.31 130.10.0.208 0.0.0.15
access-list 100 deny ip 130.10.64.160 0.0.0.31 130.10.32.208 0.0.0.15
access-list 100 deny ip 130.10.64.160 0.0.0.31 130.10.64.208 0.0.0.15
access-list 100 deny ip 130.10.64.160 0.0.0.31 130.10.0.128 0.0.0.31
access-list 100 deny ip 130.10.64.160 0.0.0.31 130.10.32.128 0.0.0.31
access-list 100 deny ip 130.10.64.160 0.0.0.31 130.10.64.128 0.0.0.31
access-list 100 deny ip 130.10.64.160 0.0.0.31 130.10.0.192 0.0.0.15
access-list 100 deny ip 130.10.64.160 0.0.0.31 130.10.32.192 0.0.0.15
access-list 100 deny ip 130.10.64.160 0.0.0.31 130.10.64.192 0.0.0.15
access-list 100 deny ip 130.10.64.160 0.0.0.31 130.10.0.224 0.0.0.7
access-list 100 deny ip 130.10.64.160 0.0.0.31 130.10.32.224 0.0.0.7
access-list 100 deny ip 130.10.64.160 0.0.0.31 130.10.64.224 0.0.0.7

access-list 100 deny ip 130.10.0.128 0.0.0.31 130.10.0.0 0.0.0.63
access-list 100 deny ip 130.10.0.128 0.0.0.31 130.10.32.0 0.0.0.63
access-list 100 deny ip 130.10.0.128 0.0.0.31 130.10.64.0 0.0.0.63
access-list 100 deny ip 130.10.0.128 0.0.0.31 130.10.0.208 0.0.0.15
access-list 100 deny ip 130.10.0.128 0.0.0.31 130.10.32.208 0.0.0.15
access-list 100 deny ip 130.10.0.128 0.0.0.31 130.10.64.208 0.0.0.15
access-list 100 deny ip 130.10.0.128 0.0.0.31 130.10.0.160 0.0.0.31
access-list 100 deny ip 130.10.0.128 0.0.0.31 130.10.32.160 0.0.0.31
access-list 100 deny ip 130.10.0.128 0.0.0.31 130.10.64.160 0.0.0.31
access-list 100 deny ip 130.10.0.128 0.0.0.31 130.10.0.192 0.0.0.15
access-list 100 deny ip 130.10.0.128 0.0.0.31 130.10.32.192 0.0.0.15
access-list 100 deny ip 130.10.0.128 0.0.0.31 130.10.64.192 0.0.0.15
access-list 100 deny ip 130.10.0.128 0.0.0.31 130.10.0.224 0.0.0.7
access-list 100 deny ip 130.10.0.128 0.0.0.31 130.10.32.224 0.0.0.7
access-list 100 deny ip 130.10.0.128 0.0.0.31 130.10.64.224 0.0.0.7

access-list 100 deny ip 130.10.32.128 0.0.0.31 130.10.0.0 0.0.0.63
access-list 100 deny ip 130.10.32.128 0.0.0.31 130.10.32.0 0.0.0.63
access-list 100 deny ip 130.10.32.128 0.0.0.31 130.10.64.0 0.0.0.63
access-list 100 deny ip 130.10.32.128 0.0.0.31 130.10.0.208 0.0.0.15
access-list 100 deny ip 130.10.32.128 0.0.0.31 130.10.32.208 0.0.0.15
access-list 100 deny ip 130.10.32.128 0.0.0.31 130.10.64.208 0.0.0.15
access-list 100 deny ip 130.10.32.128 0.0.0.31 130.10.0.160 0.0.0.31
access-list 100 deny ip 130.10.32.128 0.0.0.31 130.10.32.160 0.0.0.31
access-list 100 deny ip 130.10.32.128 0.0.0.31 130.10.64.160 0.0.0.31
access-list 100 deny ip 130.10.32.128 0.0.0.31 130.10.0.192 0.0.0.15
access-list 100 deny ip 130.10.32.128 0.0.0.31 130.10.32.192 0.0.0.15
access-list 100 deny ip 130.10.32.128 0.0.0.31 130.10.64.192 0.0.0.15
access-list 100 deny ip 130.10.32.128 0.0.0.31 130.10.0.224 0.0.0.7
access-list 100 deny ip 130.10.32.128 0.0.0.31 130.10.32.224 0.0.0.7
access-list 100 deny ip 130.10.32.128 0.0.0.31 130.10.64.224 0.0.0.7

access-list 100 deny ip 130.10.64.128 0.0.0.31 130.10.0.0 0.0.0.63
access-list 100 deny ip 130.10.64.128 0.0.0.31 130.10.32.0 0.0.0.63
access-list 100 deny ip 130.10.64.128 0.0.0.31 130.10.64.0 0.0.0.63
access-list 100 deny ip 130.10.64.128 0.0.0.31 130.10.0.208 0.0.0.15
access-list 100 deny ip 130.10.64.128 0.0.0.31 130.10.32.208 0.0.0.15
access-list 100 deny ip 130.10.64.128 0.0.0.31 130.10.64.208 0.0.0.15
access-list 100 deny ip 130.10.64.128 0.0.0.31 130.10.0.160 0.0.0.31
access-list 100 deny ip 130.10.64.128 0.0.0.31 130.10.32.160 0.0.0.31
access-list 100 deny ip 130.10.64.128 0.0.0.31 130.10.64.160 0.0.0.31
access-list 100 deny ip 130.10.64.128 0.0.0.31 130.10.0.192 0.0.0.15
access-list 100 deny ip 130.10.64.128 0.0.0.31 130.10.32.192 0.0.0.15
access-list 100 deny ip 130.10.64.128 0.0.0.31 130.10.64.192 0.0.0.15
access-list 100 deny ip 130.10.64.128 0.0.0.31 130.10.0.224 0.0.0.7
access-list 100 deny ip 130.10.64.128 0.0.0.31 130.10.32.224 0.0.0.7
access-list 100 deny ip 130.10.64.128 0.0.0.31 130.10.64.224 0.0.0.7

access-list 100 deny ip 130.10.0.192 0.0.0.15 130.10.0.0 0.0.0.63
access-list 100 deny ip 130.10.0.192 0.0.0.15 130.10.32.0 0.0.0.63
access-list 100 deny ip 130.10.0.192 0.0.0.15 130.10.64.0 0.0.0.63
access-list 100 deny ip 130.10.0.192 0.0.0.15 130.10.0.208 0.0.0.15
access-list 100 deny ip 130.10.0.192 0.0.0.15 130.10.32.208 0.0.0.15
access-list 100 deny ip 130.10.0.192 0.0.0.15 130.10.64.208 0.0.0.15
access-list 100 deny ip 130.10.0.192 0.0.0.15 130.10.0.160 0.0.0.31
access-list 100 deny ip 130.10.0.192 0.0.0.15 130.10.32.160 0.0.0.31
access-list 100 deny ip 130.10.0.192 0.0.0.15 130.10.64.160 0.0.0.31
access-list 100 deny ip 130.10.0.192 0.0.0.15 130.10.0.128 0.0.0.31
access-list 100 deny ip 130.10.0.192 0.0.0.15 130.10.32.128 0.0.0.31
access-list 100 deny ip 130.10.0.192 0.0.0.15 130.10.64.128 0.0.0.31
access-list 100 deny ip 130.10.0.192 0.0.0.15 130.10.0.224 0.0.0.7
access-list 100 deny ip 130.10.0.192 0.0.0.15 130.10.32.224 0.0.0.7
access-list 100 deny ip 130.10.0.192 0.0.0.15 130.10.64.224 0.0.0.7

access-list 100 deny ip 130.10.32.192 0.0.0.15 130.10.0.0 0.0.0.63
access-list 100 deny ip 130.10.32.192 0.0.0.15 130.10.32.0 0.0.0.63
access-list 100 deny ip 130.10.32.192 0.0.0.15 130.10.64.0 0.0.0.63
access-list 100 deny ip 130.10.32.192 0.0.0.15 130.10.0.208 0.0.0.15
access-list 100 deny ip 130.10.32.192 0.0.0.15 130.10.32.208 0.0.0.15
access-list 100 deny ip 130.10.32.192 0.0.0.15 130.10.64.208 0.0.0.15
access-list 100 deny ip 130.10.32.192 0.0.0.15 130.10.0.160 0.0.0.31
access-list 100 deny ip 130.10.32.192 0.0.0.15 130.10.32.160 0.0.0.31
access-list 100 deny ip 130.10.32.192 0.0.0.15 130.10.64.160 0.0.0.31
access-list 100 deny ip 130.10.32.192 0.0.0.15 130.10.0.128 0.0.0.31
access-list 100 deny ip 130.10.32.192 0.0.0.15 130.10.32.128 0.0.0.31
access-list 100 deny ip 130.10.32.192 0.0.0.15 130.10.64.128 0.0.0.31
access-list 100 deny ip 130.10.32.192 0.0.0.15 130.10.0.224 0.0.0.7
access-list 100 deny ip 130.10.32.192 0.0.0.15 130.10.32.224 0.0.0.7
access-list 100 deny ip 130.10.32.192 0.0.0.15 130.10.64.224 0.0.0.7

access-list 100 deny ip 130.10.64.192 0.0.0.15 130.10.0.0 0.0.0.63
access-list 100 deny ip 130.10.64.192 0.0.0.15 130.10.32.0 0.0.0.63
access-list 100 deny ip 130.10.64.192 0.0.0.15 130.10.64.0 0.0.0.63
access-list 100 deny ip 130.10.64.192 0.0.0.15 130.10.0.208 0.0.0.15
access-list 100 deny ip 130.10.64.192 0.0.0.15 130.10.32.208 0.0.0.15
access-list 100 deny ip 130.10.64.192 0.0.0.15 130.10.64.208 0.0.0.15
access-list 100 deny ip 130.10.64.192 0.0.0.15 130.10.0.160 0.0.0.31
access-list 100 deny ip 130.10.64.192 0.0.0.15 130.10.32.160 0.0.0.31
access-list 100 deny ip 130.10.64.192 0.0.0.15 130.10.64.160 0.0.0.31
access-list 100 deny ip 130.10.64.192 0.0.0.15 130.10.0.128 0.0.0.31
access-list 100 deny ip 130.10.64.192 0.0.0.15 130.10.32.128 0.0.0.31
access-list 100 deny ip 130.10.64.192 0.0.0.15 130.10.64.128 0.0.0.31
access-list 100 deny ip 130.10.64.192 0.0.0.15 130.10.0.224 0.0.0.7
access-list 100 deny ip 130.10.64.192 0.0.0.15 130.10.32.224 0.0.0.7
access-list 100 deny ip 130.10.64.192 0.0.0.15 130.10.64.224 0.0.0.7

access-list 100 deny ip 130.10.0.224 0.0.0.7 130.10.0.0 0.0.0.63
access-list 100 deny ip 130.10.0.224 0.0.0.7 130.10.32.0 0.0.0.63
access-list 100 deny ip 130.10.0.224 0.0.0.7 130.10.64.0 0.0.0.63
access-list 100 deny ip 130.10.0.224 0.0.0.7 130.10.0.208 0.0.0.15
access-list 100 deny ip 130.10.0.224 0.0.0.7 130.10.32.208 0.0.0.15
access-list 100 deny ip 130.10.0.224 0.0.0.7 130.10.64.208 0.0.0.15
access-list 100 deny ip 130.10.0.224 0.0.0.7 130.10.0.160 0.0.0.31
access-list 100 deny ip 130.10.0.224 0.0.0.7 130.10.32.160 0.0.0.31
access-list 100 deny ip 130.10.0.224 0.0.0.7 130.10.64.160 0.0.0.31
access-list 100 deny ip 130.10.0.224 0.0.0.7 130.10.0.128 0.0.0.31
access-list 100 deny ip 130.10.0.224 0.0.0.7 130.10.32.128 0.0.0.31
access-list 100 deny ip 130.10.0.224 0.0.0.7 130.10.64.128 0.0.0.31
access-list 100 deny ip 130.10.0.224 0.0.0.7 130.10.0.192 0.0.0.15
access-list 100 deny ip 130.10.0.224 0.0.0.7 130.10.32.192 0.0.0.15
access-list 100 deny ip 130.10.0.224 0.0.0.7 130.10.64.192 0.0.0.15

access-list 100 deny ip 130.10.32.224 0.0.0.7 130.10.0.0 0.0.0.63
access-list 100 deny ip 130.10.32.224 0.0.0.7 130.10.32.0 0.0.0.63
access-list 100 deny ip 130.10.32.224 0.0.0.7 130.10.64.0 0.0.0.63
access-list 100 deny ip 130.10.32.224 0.0.0.7 130.10.0.208 0.0.0.15
access-list 100 deny ip 130.10.32.224 0.0.0.7 130.10.32.208 0.0.0.15
access-list 100 deny ip 130.10.32.224 0.0.0.7 130.10.64.208 0.0.0.15
access-list 100 deny ip 130.10.32.224 0.0.0.7 130.10.0.160 0.0.0.31
access-list 100 deny ip 130.10.32.224 0.0.0.7 130.10.32.160 0.0.0.31
access-list 100 deny ip 130.10.32.224 0.0.0.7 130.10.64.160 0.0.0.31
access-list 100 deny ip 130.10.32.224 0.0.0.7 130.10.0.128 0.0.0.31
access-list 100 deny ip 130.10.32.224 0.0.0.7 130.10.32.128 0.0.0.31
access-list 100 deny ip 130.10.32.224 0.0.0.7 130.10.64.128 0.0.0.31
access-list 100 deny ip 130.10.32.224 0.0.0.7 130.10.0.192 0.0.0.15
access-list 100 deny ip 130.10.32.224 0.0.0.7 130.10.32.192 0.0.0.15
access-list 100 deny ip 130.10.32.224 0.0.0.7 130.10.64.192 0.0.0.15

access-list 100 deny ip 130.10.64.224 0.0.0.7 130.10.0.0 0.0.0.63
access-list 100 deny ip 130.10.64.224 0.0.0.7 130.10.32.0 0.0.0.63
access-list 100 deny ip 130.10.64.224 0.0.0.7 130.10.64.0 0.0.0.63
access-list 100 deny ip 130.10.64.224 0.0.0.7 130.10.0.208 0.0.0.15
access-list 100 deny ip 130.10.64.224 0.0.0.7 130.10.32.208 0.0.0.15
access-list 100 deny ip 130.10.64.224 0.0.0.7 130.10.64.208 0.0.0.15
access-list 100 deny ip 130.10.64.224 0.0.0.7 130.10.0.160 0.0.0.31
access-list 100 deny ip 130.10.64.224 0.0.0.7 130.10.32.160 0.0.0.31
access-list 100 deny ip 130.10.64.224 0.0.0.7 130.10.64.160 0.0.0.31
access-list 100 deny ip 130.10.64.224 0.0.0.7 130.10.0.128 0.0.0.31
access-list 100 deny ip 130.10.64.224 0.0.0.7 130.10.32.128 0.0.0.31
access-list 100 deny ip 130.10.64.224 0.0.0.7 130.10.64.128 0.0.0.31
access-list 100 deny ip 130.10.64.224 0.0.0.7 130.10.0.192 0.0.0.15
access-list 100 deny ip 130.10.64.224 0.0.0.7 130.10.32.192 0.0.0.15
access-list 100 deny ip 130.10.64.224 0.0.0.7 130.10.64.192 0.0.0.15

access-list 100 deny ip 130.10.0.0 0.0.0.63 130.10.132.0 0.0.0.3
access-list 100 deny ip 130.10.0.64 0.0.0.63 130.10.132.0 0.0.0.3
access-list 100 deny ip 130.10.0.128 0.0.0.31 130.10.132.0 0.0.0.3
access-list 100 deny ip 130.10.0.160 0.0.0.31 130.10.132.0 0.0.0.3
access-list 100 deny ip 130.10.0.192 0.0.0.15 130.10.132.0 0.0.0.3
access-list 100 deny ip 130.10.0.224 0.0.0.7 130.10.132.0 0.0.0.3
access-list 100 permit ip 130.10.0.208 0.0.0.15 130.10.132.0 0.0.0.3

access-list 100 deny ip 130.10.32.0 0.0.0.63 130.10.133.0 0.0.0.3
access-list 100 deny ip 130.10.32.64 0.0.0.63 130.10.133.0 0.0.0.3
access-list 100 deny ip 130.10.32.128 0.0.0.31 130.10.133.0 0.0.0.3
access-list 100 deny ip 130.10.32.160 0.0.0.31 130.10.133.0 0.0.0.3
access-list 100 deny ip 130.10.32.192 0.0.0.15 130.10.133.0 0.0.0.3
access-list 100 deny ip 130.10.32.224 0.0.0.7 130.10.133.0 0.0.0.3
access-list 100 permit ip 130.10.32.208 0.0.0.15 130.10.133.0 0.0.0.3

access-list 100 deny ip 130.10.64.0 0.0.0.63 130.10.134.0 0.0.0.3
access-list 100 deny ip 130.10.64.64 0.0.0.63 130.10.134.0 0.0.0.3
access-list 100 deny ip 130.10.64.128 0.0.0.31 130.10.134.0 0.0.0.3
access-list 100 deny ip 130.10.64.160 0.0.0.31 130.10.134.0 0.0.0.3
access-list 100 deny ip 130.10.64.192 0.0.0.15 130.10.134.0 0.0.0.3
access-list 100 deny ip 130.10.64.224 0.0.0.7 130.10.134.0 0.0.0.3
access-list 100 permit ip 130.10.64.208 0.0.0.15 130.10.134.0 0.0.0.3

access-list 100 permit ip any any



interface fa0/0.10
ip access-group 100 in
exit
interface fa0/0.20
ip access-group 100 in
exit
interface fa0/0.30
ip access-group 100 in
exit
interface fa0/0.40
ip access-group 100 in
exit
interface fa0/0.50
ip access-group 100 in
exit
interface fa0/0.60
ip access-group 100 in
exit