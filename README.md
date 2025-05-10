# PEEK
Somos el peak


# COMANDOS PARA HACER EL VLAN

CONFIGURAR VLANS

Switch>ENA

Switch#configure ter

Switch(config)#vlan 10     //Cambiar el número de área

Switch(config-vlan)#NAME VLAN10     //Cambiar el número de área

Switch(config-vlan)#exit

Switch(config)#interface range f0/1-7     //Si solo se usa un puerto se usa interface f0/10 donde los o el número es el número de puerto o puertos válidos

Switch(config-if-range)#switchport mode access

Switch(config-if-range)#switchport access vlan 10       //Cambiar el número de área

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

Switch(config-if)#switchport trunk allowed vlan 10,20,30,40,50,60

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

Router(config)#access-list 101 deny ip 130.10.0.0 0.0.0.63 130.10.0.80 0.0.0.15      //Administración -> Marketing ❌
Router(config)#access-list 101 deny ip 130.10.0.0 0.0.0.63 130.10.0.96 0.0.0.15      //Administración -> Ventas ❌
Router(config)#access-list 101 deny ip 130.10.0.0 0.0.0.63 130.10.0.128 0.0.0.31      //Administración -> Finanzas ❌
Router(config)#access-list 101 deny ip 130.10.0.0 0.0.0.63 130.10.0.160 0.0.0.31      //Administración -> Logística ❌
Router(config)#access-list 101 deny ip 130.10.0.0 0.0.0.63 130.10.0.64 0.0.0.15      //Administración -> Sistemas ❌
Router(config)#access-list 101 deny ip 130.10.0.0 0.0.0.63 130.10.2.0 0.0.0.63      //Administración -> Administración ❌
Router(config)#access-list 101 deny ip 130.10.0.0 0.0.0.63 130.10.2.80 0.0.0.15      //Administración -> Marketing ❌
Router(config)#access-list 101 deny ip 130.10.0.0 0.0.0.63 130.10.2.96 0.0.0.15      //Administración -> Ventas ❌
Router(config)#access-list 101 deny ip 130.10.0.0 0.0.0.63 130.10.2.128 0.0.0.31      //Administración -> Finanzas ❌
Router(config)#access-list 101 deny ip 130.10.0.0 0.0.0.63 130.10.2.160 0.0.0.31      //Administración -> Logística ❌
Router(config)#access-list 101 deny ip 130.10.0.0 0.0.0.63 130.10.2.64 0.0.0.15      //Administración -> Sistemas ❌
Router(config)#access-list 101 deny ip 130.10.0.0 0.0.0.63 130.10.1.0 0.0.0.63      //Administración -> Administración ❌
Router(config)#access-list 101 deny ip 130.10.0.0 0.0.0.63 130.10.1.80 0.0.0.15      //Administración -> Marketing ❌
Router(config)#access-list 101 deny ip 130.10.0.0 0.0.0.63 130.10.1.96 0.0.0.15      //Administración -> Ventas ❌
Router(config)#access-list 101 deny ip 130.10.0.0 0.0.0.63 130.10.1.128 0.0.0.31      //Administración -> Finanzas ❌
Router(config)#access-list 101 deny ip 130.10.0.0 0.0.0.63 130.10.1.160 0.0.0.31      //Administración -> Logística ❌
Router(config)#access-list 101 deny ip 130.10.0.0 0.0.0.63 130.10.1.64 0.0.0.15      //Administración -> Sistemas ❌

Router(config)#access-list 101 deny ip 130.10.0.64 0.0.0.15 130.10.0.80 0.0.0.15      //Sistemas -> Marketing ❌
Router(config)#access-list 101 deny ip 130.10.0.64 0.0.0.15 130.10.0.96 0.0.0.15      //Sistemas -> Ventas ❌
Router(config)#access-list 101 deny ip 130.10.0.64 0.0.0.15 130.10.0.128 0.0.0.31      //Sistemas -> Finanzas ❌
Router(config)#access-list 101 deny ip 130.10.0.64 0.0.0.15 130.10.0.160 0.0.0.31      //Sistemas -> Logística ❌
Router(config)#access-list 101 deny ip 130.10.0.64 0.0.0.15 130.10.0.0 0.0.0.63      //Sistemas -> Administración ❌
Router(config)#access-list 101 deny ip 130.10.0.64 0.0.0.15 130.10.1.64 0.0.0.15      //Sistemas -> Sistemas ❌
Router(config)#access-list 101 deny ip 130.10.0.64 0.0.0.15 130.10.1.80 0.0.0.15      //Sistemas -> Marketing ❌
Router(config)#access-list 101 deny ip 130.10.0.64 0.0.0.15 130.10.1.96 0.0.0.15      //Sistemas -> Ventas ❌
Router(config)#access-list 101 deny ip 130.10.0.64 0.0.0.15 130.10.1.128 0.0.0.31      //Sistemas -> Finanzas ❌
Router(config)#access-list 101 deny ip 130.10.0.64 0.0.0.15 130.10.1.160 0.0.0.31      //Sistemas -> Logística ❌
Router(config)#access-list 101 deny ip 130.10.0.64 0.0.0.15 130.10.1.0 0.0.0.63      //Sistemas -> Administración ❌
Router(config)#access-list 101 deny ip 130.10.0.64 0.0.0.15 130.10.2.64 0.0.0.15      //Sistemas -> Sistemas ❌
Router(config)#access-list 101 deny ip 130.10.0.64 0.0.0.15 130.10.2.80 0.0.0.15      //Sistemas -> Marketing ❌
Router(config)#access-list 101 deny ip 130.10.0.64 0.0.0.15 130.10.2.96 0.0.0.15      //Sistemas -> Ventas ❌
Router(config)#access-list 101 deny ip 130.10.0.64 0.0.0.15 130.10.2.128 0.0.0.31      //Sistemas -> Finanzas ❌
Router(config)#access-list 101 deny ip 130.10.0.64 0.0.0.15 130.10.2.160 0.0.0.31      //Sistemas -> Logística ❌
Router(config)#access-list 101 deny ip 130.10.0.64 0.0.0.15 130.10.2.0 0.0.0.63      //Sistemas -> Administración ❌

Router(config)#access-list 101 deny ip 130.10.0.80 0.0.0.15 130.10.0.64 0.0.0.15      //Marketing -> Sistemas ❌
Router(config)#access-list 101 deny ip 130.10.0.80 0.0.0.15 130.10.0.96 0.0.0.15      //Marketing -> Ventas ❌
Router(config)#access-list 101 deny ip 130.10.0.80 0.0.0.15 130.10.0.128 0.0.0.31      //Marketing -> Finanzas ❌
Router(config)#access-list 101 deny ip 130.10.0.80 0.0.0.15 130.10.0.160 0.0.0.31      //Marketing -> Logística ❌
Router(config)#access-list 101 deny ip 130.10.0.80 0.0.0.15 130.10.0.0 0.0.0.63      //Marketing -> Administración ❌
Router(config)#access-list 101 deny ip 130.10.0.80 0.0.0.15 130.10.1.80 0.0.0.15      //Marketing -> Marketing ❌
Router(config)#access-list 101 deny ip 130.10.0.80 0.0.0.15 130.10.1.64 0.0.0.15      //Marketing -> Sistemas ❌
Router(config)#access-list 101 deny ip 130.10.0.80 0.0.0.15 130.10.1.96 0.0.0.15      //Marketing -> Ventas ❌
Router(config)#access-list 101 deny ip 130.10.0.80 0.0.0.15 130.10.1.128 0.0.0.31      //Marketing -> Finanzas ❌
Router(config)#access-list 101 deny ip 130.10.0.80 0.0.0.15 130.10.1.160 0.0.0.31      //Marketing -> Logística ❌
Router(config)#access-list 101 deny ip 130.10.0.80 0.0.0.15 130.10.1.0 0.0.0.63      //Marketing -> Administración ❌
Router(config)#access-list 101 deny ip 130.10.0.80 0.0.0.15 130.10.2.80 0.0.0.15      //Marketing -> Marketing ❌
Router(config)#access-list 101 deny ip 130.10.0.80 0.0.0.15 130.10.2.64 0.0.0.15      //Marketing -> Sistemas ❌
Router(config)#access-list 101 deny ip 130.10.0.80 0.0.0.15 130.10.2.96 0.0.0.15      //Marketing -> Ventas ❌
Router(config)#access-list 101 deny ip 130.10.0.80 0.0.0.15 130.10.2.128 0.0.0.31      //Marketing -> Finanzas ❌
Router(config)#access-list 101 deny ip 130.10.0.80 0.0.0.15 130.10.2.160 0.0.0.31      //Marketing -> Logística ❌
Router(config)#access-list 101 deny ip 130.10.0.80 0.0.0.15 130.10.2.0 0.0.0.63      //Marketing -> Administración ❌

Router(config)#access-list 101 deny ip 130.10.0.96 0.0.0.15 130.10.0.64 0.0.0.15      //Ventas -> Sistemas ❌
Router(config)#access-list 101 deny ip 130.10.0.96 0.0.0.15 130.10.0.80 0.0.0.15      //Ventas -> Marketing ❌
Router(config)#access-list 101 deny ip 130.10.0.96 0.0.0.15 130.10.0.128 0.0.0.31      //Ventas -> Finanzas ❌
Router(config)#access-list 101 deny ip 130.10.0.96 0.0.0.15 130.10.0.160 0.0.0.31      //Ventas -> Logística ❌
Router(config)#access-list 101 deny ip 130.10.0.96 0.0.0.15 130.10.0.0 0.0.0.63      //Ventas -> Administración ❌
Router(config)#access-list 101 deny ip 130.10.0.96 0.0.0.15 130.10.1.96 0.0.0.15      //Ventas -> Ventas ❌
Router(config)#access-list 101 deny ip 130.10.0.96 0.0.0.15 130.10.1.64 0.0.0.15      //Ventas -> Sistemas ❌
Router(config)#access-list 101 deny ip 130.10.0.96 0.0.0.15 130.10.1.80 0.0.0.15      //Ventas -> Marketing ❌
Router(config)#access-list 101 deny ip 130.10.0.96 0.0.0.15 130.10.1.128 0.0.0.31      //Ventas -> Finanzas ❌
Router(config)#access-list 101 deny ip 130.10.0.96 0.0.0.15 130.10.1.160 0.0.0.31      //Ventas -> Logística ❌
Router(config)#access-list 101 deny ip 130.10.0.96 0.0.0.15 130.10.1.0 0.0.0.63      //Ventas -> Administración ❌
Router(config)#access-list 101 deny ip 130.10.0.96 0.0.0.15 130.10.2.96 0.0.0.15      //Ventas -> Ventas ❌
Router(config)#access-list 101 deny ip 130.10.0.96 0.0.0.15 130.10.2.64 0.0.0.15      //Ventas -> Sistemas ❌
Router(config)#access-list 101 deny ip 130.10.0.96 0.0.0.15 130.10.2.80 0.0.0.15      //Ventas -> Marketing ❌
Router(config)#access-list 101 deny ip 130.10.0.96 0.0.0.15 130.10.2.128 0.0.0.31      //Ventas -> Finanzas ❌
Router(config)#access-list 101 deny ip 130.10.0.96 0.0.0.15 130.10.2.160 0.0.0.31      //Ventas -> Logística ❌
Router(config)#access-list 101 deny ip 130.10.0.96 0.0.0.15 130.10.2.0 0.0.0.63      //Ventas -> Administración ❌

Router(config)#access-list 101 deny ip 130.10.0.128 0.0.0.31 130.10.0.64 0.0.0.15      //Finanzas -> Sistemas ❌
Router(config)#access-list 101 deny ip 130.10.0.128 0.0.0.31 130.10.0.80 0.0.0.15      //Finanzas -> Marketing ❌
Router(config)#access-list 101 deny ip 130.10.0.128 0.0.0.31 130.10.0.96 0.0.0.15      //Finanzas -> Ventas ❌
Router(config)#access-list 101 deny ip 130.10.0.128 0.0.0.31 130.10.0.160 0.0.0.31      //Finanzas -> Logística ❌
Router(config)#access-list 101 deny ip 130.10.0.128 0.0.0.31 130.10.0.0 0.0.0.63      //Finanzas -> Administración ❌
Router(config)#access-list 101 deny ip 130.10.0.128 0.0.0.31 130.10.1.128 0.0.0.31      //Finanzas -> Finanzas ❌
Router(config)#access-list 101 deny ip 130.10.0.128 0.0.0.31 130.10.1.64 0.0.0.15      //Finanzas -> Sistemas ❌
Router(config)#access-list 101 deny ip 130.10.0.128 0.0.0.31 130.10.1.80 0.0.0.15      //Finanzas -> Marketing ❌
Router(config)#access-list 101 deny ip 130.10.0.128 0.0.0.31 130.10.1.96 0.0.0.15      //Finanzas -> Ventas ❌
Router(config)#access-list 101 deny ip 130.10.0.128 0.0.0.31 130.10.1.160 0.0.0.31      //Finanzas -> Logística ❌
Router(config)#access-list 101 deny ip 130.10.0.128 0.0.0.31 130.10.1.0 0.0.0.63      //Finanzas -> Administración ❌
Router(config)#access-list 101 deny ip 130.10.0.128 0.0.0.31 130.10.2.128 0.0.0.31      //Finanzas -> Finanzas ❌
Router(config)#access-list 101 deny ip 130.10.0.128 0.0.0.31 130.10.2.64 0.0.0.15      //Finanzas -> Sistemas ❌
Router(config)#access-list 101 deny ip 130.10.0.128 0.0.0.31 130.10.2.80 0.0.0.15      //Finanzas -> Marketing ❌
Router(config)#access-list 101 deny ip 130.10.0.128 0.0.0.31 130.10.2.96 0.0.0.15      //Finanzas -> Ventas ❌
Router(config)#access-list 101 deny ip 130.10.0.128 0.0.0.31 130.10.2.160 0.0.0.31      //Finanzas -> Logística ❌
Router(config)#access-list 101 deny ip 130.10.0.128 0.0.0.31 130.10.2.0 0.0.0.63      //Finanzas -> Administración ❌

Router(config)#access-list 101 deny ip 130.10.0.160 0.0.0.31 130.10.0.64 0.0.0.15      //Logística -> Sistemas ❌
Router(config)#access-list 101 deny ip 130.10.0.160 0.0.0.31 130.10.0.80 0.0.0.15      //Logística -> Marketing ❌
Router(config)#access-list 101 deny ip 130.10.0.160 0.0.0.31 130.10.0.96 0.0.0.15      //Logística -> Ventas ❌
Router(config)#access-list 101 deny ip 130.10.0.160 0.0.0.31 130.10.0.128 0.0.0.31      //Logística -> Finanzas ❌
Router(config)#access-list 101 deny ip 130.10.0.160 0.0.0.31 130.10.0.0 0.0.0.63      //Logística -> Administración ❌
Router(config)#access-list 101 deny ip 130.10.0.160 0.0.0.31 130.10.1.160 0.0.0.31      //Logística -> Logística ❌
Router(config)#access-list 101 deny ip 130.10.0.160 0.0.0.31 130.10.1.64 0.0.0.15      //Logística -> Sistemas ❌
Router(config)#access-list 101 deny ip 130.10.0.160 0.0.0.31 130.10.1.80 0.0.0.15      //Logística -> Marketing ❌
Router(config)#access-list 101 deny ip 130.10.0.160 0.0.0.31 130.10.1.96 0.0.0.15      //Logística -> Ventas ❌
Router(config)#access-list 101 deny ip 130.10.0.160 0.0.0.31 130.10.1.128 0.0.0.31      //Logística -> Finanzas ❌
Router(config)#access-list 101 deny ip 130.10.0.160 0.0.0.31 130.10.1.0 0.0.0.63      //Logística -> Administración ❌
Router(config)#access-list 101 deny ip 130.10.0.160 0.0.0.31 130.10.2.160 0.0.0.31      //Logística -> Logística ❌
Router(config)#access-list 101 deny ip 130.10.0.160 0.0.0.31 130.10.2.64 0.0.0.15      //Logística -> Sistemas ❌
Router(config)#access-list 101 deny ip 130.10.0.160 0.0.0.31 130.10.2.80 0.0.0.15      //Logística -> Marketing ❌
Router(config)#access-list 101 deny ip 130.10.0.160 0.0.0.31 130.10.2.96 0.0.0.15      //Logística -> Ventas ❌
Router(config)#access-list 101 deny ip 130.10.0.160 0.0.0.31 130.10.2.128 0.0.0.31      //Logística -> Finanzas ❌
Router(config)#access-list 101 deny ip 130.10.0.160 0.0.0.31 130.10.2.0 0.0.0.63      //Logística -> Administración ❌

Router(config)#access-list 101 permit ip any any      //Permitir el resto (como respuestas, navegación, etc.)

Router(config)#interface g0/1.10      //Cambiar el número de acuerdo al área correspondiente

Router(config-if)#ip access-group 101 in

Router(config-if)#exit


# CONFIGURACIÓN DE ACLS PARA LA COMUNICACIÓN ENTRE VLANS SOLO PARA LONDRES

Router>ENA

Router#configure ter

Router(config)#access-list 101 deny ip 130.10.1.0 0.0.0.63 130.10.1.80 0.0.0.15      //Administración -> Marketing ❌
Router(config)#access-list 101 deny ip 130.10.1.0 0.0.0.63 130.10.1.96 0.0.0.15      //Administración -> Ventas ❌
Router(config)#access-list 101 deny ip 130.10.1.0 0.0.0.63 130.10.1.128 0.0.0.31      //Administración -> Finanzas ❌
Router(config)#access-list 101 deny ip 130.10.1.0 0.0.0.63 130.10.1.160 0.0.0.31      //Administración -> Logística ❌
Router(config)#access-list 101 deny ip 130.10.1.0 0.0.0.63 130.10.1.64 0.0.0.15      //Administración -> Sistemas ❌
Router(config)#access-list 101 deny ip 130.10.1.0 0.0.0.63 130.10.2.0 0.0.0.63      //Administración -> Administración ❌
Router(config)#access-list 101 deny ip 130.10.1.0 0.0.0.63 130.10.2.80 0.0.0.15      //Administración -> Marketing ❌
Router(config)#access-list 101 deny ip 130.10.1.0 0.0.0.63 130.10.2.96 0.0.0.15      //Administración -> Ventas ❌
Router(config)#access-list 101 deny ip 130.10.1.0 0.0.0.63 130.10.2.128 0.0.0.31      //Administración -> Finanzas ❌
Router(config)#access-list 101 deny ip 130.10.1.0 0.0.0.63 130.10.2.160 0.0.0.31      //Administración -> Logística ❌
Router(config)#access-list 101 deny ip 130.10.1.0 0.0.0.63 130.10.2.64 0.0.0.15      //Administración -> Sistemas ❌
Router(config)#access-list 101 deny ip 130.10.1.0 0.0.0.63 130.10.0.0 0.0.0.63      //Administración -> Administración ❌
Router(config)#access-list 101 deny ip 130.10.1.0 0.0.0.63 130.10.0.80 0.0.0.15      //Administración -> Marketing ❌
Router(config)#access-list 101 deny ip 130.10.1.0 0.0.0.63 130.10.0.96 0.0.0.15      //Administración -> Ventas ❌
Router(config)#access-list 101 deny ip 130.10.1.0 0.0.0.63 130.10.0.128 0.0.0.31      //Administración -> Finanzas ❌
Router(config)#access-list 101 deny ip 130.10.1.0 0.0.0.63 130.10.0.160 0.0.0.31      //Administración -> Logística ❌
Router(config)#access-list 101 deny ip 130.10.1.0 0.0.0.63 130.10.0.64 0.0.0.15      //Administración -> Sistemas ❌

Router(config)#access-list 101 deny ip 130.10.1.64 0.0.0.15 130.10.1.80 0.0.0.15      //Sistemas -> Marketing ❌
Router(config)#access-list 101 deny ip 130.10.1.64 0.0.0.15 130.10.1.96 0.0.0.15      //Sistemas -> Ventas ❌
Router(config)#access-list 101 deny ip 130.10.1.64 0.0.0.15 130.10.1.128 0.0.0.31      //Sistemas -> Finanzas ❌
Router(config)#access-list 101 deny ip 130.10.1.64 0.0.0.15 130.10.1.160 0.0.0.31      //Sistemas -> Logística ❌
Router(config)#access-list 101 deny ip 130.10.1.64 0.0.0.15 130.10.1.0 0.0.0.63      //Sistemas -> Administración ❌
Router(config)#access-list 101 deny ip 130.10.1.64 0.0.0.15 130.10.0.64 0.0.0.15      //Sistemas -> Sistemas ❌
Router(config)#access-list 101 deny ip 130.10.1.64 0.0.0.15 130.10.0.80 0.0.0.15      //Sistemas -> Marketing ❌
Router(config)#access-list 101 deny ip 130.10.1.64 0.0.0.15 130.10.0.96 0.0.0.15      //Sistemas -> Ventas ❌
Router(config)#access-list 101 deny ip 130.10.1.64 0.0.0.15 130.10.0.128 0.0.0.31      //Sistemas -> Finanzas ❌
Router(config)#access-list 101 deny ip 130.10.1.64 0.0.0.15 130.10.0.160 0.0.0.31      //Sistemas -> Logística ❌
Router(config)#access-list 101 deny ip 130.10.1.64 0.0.0.15 130.10.0.0 0.0.0.63      //Sistemas -> Administración ❌
Router(config)#access-list 101 deny ip 130.10.1.64 0.0.0.15 130.10.2.64 0.0.0.15      //Sistemas -> Sistemas ❌
Router(config)#access-list 101 deny ip 130.10.1.64 0.0.0.15 130.10.2.80 0.0.0.15      //Sistemas -> Marketing ❌
Router(config)#access-list 101 deny ip 130.10.1.64 0.0.0.15 130.10.2.96 0.0.0.15      //Sistemas -> Ventas ❌
Router(config)#access-list 101 deny ip 130.10.1.64 0.0.0.15 130.10.2.128 0.0.0.31      //Sistemas -> Finanzas ❌
Router(config)#access-list 101 deny ip 130.10.1.64 0.0.0.15 130.10.2.160 0.0.0.31      //Sistemas -> Logística ❌
Router(config)#access-list 101 deny ip 130.10.1.64 0.0.0.15 130.10.2.0 0.0.0.63      //Sistemas -> Administración ❌

Router(config)#access-list 101 deny ip 130.10.1.80 0.0.0.15 130.10.1.64 0.0.0.15      //Marketing -> Sistemas ❌
Router(config)#access-list 101 deny ip 130.10.1.80 0.0.0.15 130.10.1.96 0.0.0.15      //Marketing -> Ventas ❌
Router(config)#access-list 101 deny ip 130.10.1.80 0.0.0.15 130.10.1.128 0.0.0.31      //Marketing -> Finanzas ❌
Router(config)#access-list 101 deny ip 130.10.1.80 0.0.0.15 130.10.1.160 0.0.0.31      //Marketing -> Logística ❌
Router(config)#access-list 101 deny ip 130.10.1.80 0.0.0.15 130.10.1.0 0.0.0.63      //Marketing -> Administración ❌
Router(config)#access-list 101 deny ip 130.10.1.80 0.0.0.15 130.10.0.80 0.0.0.15      //Marketing -> Marketing ❌
Router(config)#access-list 101 deny ip 130.10.1.80 0.0.0.15 130.10.0.64 0.0.0.15      //Marketing -> Sistemas ❌
Router(config)#access-list 101 deny ip 130.10.1.80 0.0.0.15 130.10.0.96 0.0.0.15      //Marketing -> Ventas ❌
Router(config)#access-list 101 deny ip 130.10.1.80 0.0.0.15 130.10.0.128 0.0.0.31      //Marketing -> Finanzas ❌
Router(config)#access-list 101 deny ip 130.10.1.80 0.0.0.15 130.10.0.160 0.0.0.31      //Marketing -> Logística ❌
Router(config)#access-list 101 deny ip 130.10.1.80 0.0.0.15 130.10.0.0 0.0.0.63      //Marketing -> Administración ❌
Router(config)#access-list 101 deny ip 130.10.1.80 0.0.0.15 130.10.2.80 0.0.0.15      //Marketing -> Marketing ❌
Router(config)#access-list 101 deny ip 130.10.1.80 0.0.0.15 130.10.2.64 0.0.0.15      //Marketing -> Sistemas ❌
Router(config)#access-list 101 deny ip 130.10.1.80 0.0.0.15 130.10.2.96 0.0.0.15      //Marketing -> Ventas ❌
Router(config)#access-list 101 deny ip 130.10.1.80 0.0.0.15 130.10.2.128 0.0.0.31      //Marketing -> Finanzas ❌
Router(config)#access-list 101 deny ip 130.10.1.80 0.0.0.15 130.10.2.160 0.0.0.31      //Marketing -> Logística ❌
Router(config)#access-list 101 deny ip 130.10.1.80 0.0.0.15 130.10.2.0 0.0.0.63      //Marketing -> Administración ❌

Router(config)#access-list 101 deny ip 130.10.1.96 0.0.0.15 130.10.1.64 0.0.0.15      //Ventas -> Sistemas ❌
Router(config)#access-list 101 deny ip 130.10.1.96 0.0.0.15 130.10.1.80 0.0.0.15      //Ventas -> Marketing ❌
Router(config)#access-list 101 deny ip 130.10.1.96 0.0.0.15 130.10.1.128 0.0.0.31      //Ventas -> Finanzas ❌
Router(config)#access-list 101 deny ip 130.10.1.96 0.0.0.15 130.10.1.160 0.0.0.31      //Ventas -> Logística ❌
Router(config)#access-list 101 deny ip 130.10.1.96 0.0.0.15 130.10.1.0 0.0.0.63      //Ventas -> Administración ❌
Router(config)#access-list 101 deny ip 130.10.1.96 0.0.0.15 130.10.0.96 0.0.0.15      //Ventas -> Ventas ❌
Router(config)#access-list 101 deny ip 130.10.1.96 0.0.0.15 130.10.0.64 0.0.0.15      //Ventas -> Sistemas ❌
Router(config)#access-list 101 deny ip 130.10.1.96 0.0.0.15 130.10.0.80 0.0.0.15      //Ventas -> Marketing ❌
Router(config)#access-list 101 deny ip 130.10.1.96 0.0.0.15 130.10.0.128 0.0.0.31      //Ventas -> Finanzas ❌
Router(config)#access-list 101 deny ip 130.10.1.96 0.0.0.15 130.10.0.160 0.0.0.31      //Ventas -> Logística ❌
Router(config)#access-list 101 deny ip 130.10.1.96 0.0.0.15 130.10.0.0 0.0.0.63      //Ventas -> Administración ❌
Router(config)#access-list 101 deny ip 130.10.1.96 0.0.0.15 130.10.2.96 0.0.0.15      //Ventas -> Ventas ❌
Router(config)#access-list 101 deny ip 130.10.1.96 0.0.0.15 130.10.2.64 0.0.0.15      //Ventas -> Sistemas ❌
Router(config)#access-list 101 deny ip 130.10.1.96 0.0.0.15 130.10.2.80 0.0.0.15      //Ventas -> Marketing ❌
Router(config)#access-list 101 deny ip 130.10.1.96 0.0.0.15 130.10.2.128 0.0.0.31      //Ventas -> Finanzas ❌
Router(config)#access-list 101 deny ip 130.10.1.96 0.0.0.15 130.10.2.160 0.0.0.31      //Ventas -> Logística ❌
Router(config)#access-list 101 deny ip 130.10.1.96 0.0.0.15 130.10.2.0 0.0.0.63      //Ventas -> Administración ❌

Router(config)#access-list 101 deny ip 130.10.1.128 0.0.0.31 130.10.1.64 0.0.0.15      //Finanzas -> Sistemas ❌
Router(config)#access-list 101 deny ip 130.10.1.128 0.0.0.31 130.10.1.80 0.0.0.15      //Finanzas -> Marketing ❌
Router(config)#access-list 101 deny ip 130.10.1.128 0.0.0.31 130.10.1.96 0.0.0.15      //Finanzas -> Ventas ❌
Router(config)#access-list 101 deny ip 130.10.1.128 0.0.0.31 130.10.1.160 0.0.0.31      //Finanzas -> Logística ❌
Router(config)#access-list 101 deny ip 130.10.1.128 0.0.0.31 130.10.1.0 0.0.0.63      //Finanzas -> Administración ❌
Router(config)#access-list 101 deny ip 130.10.1.128 0.0.0.31 130.10.0.128 0.0.0.31      //Finanzas -> Finanzas ❌
Router(config)#access-list 101 deny ip 130.10.1.128 0.0.0.31 130.10.0.64 0.0.0.15      //Finanzas -> Sistemas ❌
Router(config)#access-list 101 deny ip 130.10.1.128 0.0.0.31 130.10.0.80 0.0.0.15      //Finanzas -> Marketing ❌
Router(config)#access-list 101 deny ip 130.10.1.128 0.0.0.31 130.10.0.96 0.0.0.15      //Finanzas -> Ventas ❌
Router(config)#access-list 101 deny ip 130.10.1.128 0.0.0.31 130.10.0.160 0.0.0.31      //Finanzas -> Logística ❌
Router(config)#access-list 101 deny ip 130.10.1.128 0.0.0.31 130.10.0.0 0.0.0.63      //Finanzas -> Administración ❌
Router(config)#access-list 101 deny ip 130.10.1.128 0.0.0.31 130.10.2.128 0.0.0.31      //Finanzas -> Finanzas ❌
Router(config)#access-list 101 deny ip 130.10.1.128 0.0.0.31 130.10.2.64 0.0.0.15      //Finanzas -> Sistemas ❌
Router(config)#access-list 101 deny ip 130.10.1.128 0.0.0.31 130.10.2.80 0.0.0.15      //Finanzas -> Marketing ❌
Router(config)#access-list 101 deny ip 130.10.1.128 0.0.0.31 130.10.2.96 0.0.0.15      //Finanzas -> Ventas ❌
Router(config)#access-list 101 deny ip 130.10.1.128 0.0.0.31 130.10.2.160 0.0.0.31      //Finanzas -> Logística ❌
Router(config)#access-list 101 deny ip 130.10.1.128 0.0.0.31 130.10.2.0 0.0.0.63      //Finanzas -> Administración ❌

Router(config)#access-list 101 deny ip 130.10.1.160 0.0.0.31 130.10.1.64 0.0.0.15      //Logística -> Sistemas ❌
Router(config)#access-list 101 deny ip 130.10.1.160 0.0.0.31 130.10.1.80 0.0.0.15      //Logística -> Marketing ❌
Router(config)#access-list 101 deny ip 130.10.1.160 0.0.0.31 130.10.1.96 0.0.0.15      //Logística -> Ventas ❌
Router(config)#access-list 101 deny ip 130.10.1.160 0.0.0.31 130.10.1.128 0.0.0.31      //Logística -> Finanzas ❌
Router(config)#access-list 101 deny ip 130.10.1.160 0.0.0.31 130.10.1.0 0.0.0.63      //Logística -> Administración ❌
Router(config)#access-list 101 deny ip 130.10.1.160 0.0.0.31 130.10.0.160 0.0.0.31      //Logística -> Logística ❌
Router(config)#access-list 101 deny ip 130.10.1.160 0.0.0.31 130.10.0.64 0.0.0.15      //Logística -> Sistemas ❌
Router(config)#access-list 101 deny ip 130.10.1.160 0.0.0.31 130.10.0.80 0.0.0.15      //Logística -> Marketing ❌
Router(config)#access-list 101 deny ip 130.10.1.160 0.0.0.31 130.10.0.96 0.0.0.15      //Logística -> Ventas ❌
Router(config)#access-list 101 deny ip 130.10.1.160 0.0.0.31 130.10.0.128 0.0.0.31      //Logística -> Finanzas ❌
Router(config)#access-list 101 deny ip 130.10.1.160 0.0.0.31 130.10.0.0 0.0.0.63      //Logística -> Administración ❌
Router(config)#access-list 101 deny ip 130.10.1.160 0.0.0.31 130.10.2.160 0.0.0.31      //Logística -> Logística ❌
Router(config)#access-list 101 deny ip 130.10.1.160 0.0.0.31 130.10.2.64 0.0.0.15      //Logística -> Sistemas ❌
Router(config)#access-list 101 deny ip 130.10.1.160 0.0.0.31 130.10.2.80 0.0.0.15      //Logística -> Marketing ❌
Router(config)#access-list 101 deny ip 130.10.1.160 0.0.0.31 130.10.2.96 0.0.0.15      //Logística -> Ventas ❌
Router(config)#access-list 101 deny ip 130.10.1.160 0.0.0.31 130.10.2.128 0.0.0.31      //Logística -> Finanzas ❌
Router(config)#access-list 101 deny ip 130.10.1.160 0.0.0.31 130.10.2.0 0.0.0.63      //Logística -> Administración ❌


Router(config)#access-list 101 permit ip any any      //Permitir el resto (como respuestas, navegación, etc.)

Router(config)#interface g0/1.10      //Cambiar el número de acuerdo al área correspondiente

Router(config-if)#ip access-group 101 in

Router(config-if)#exit


# CONFIGURACIÓN DE ACLS PARA LA COMUNICACIÓN ENTRE VLANS SOLO PARA PARÍS

Router>ENA

Router#configure ter

Router(config)#access-list 101 deny ip 130.10.2.0 0.0.0.63 130.10.2.80 0.0.0.15      //Administración -> Marketing ❌
Router(config)#access-list 101 deny ip 130.10.2.0 0.0.0.63 130.10.2.96 0.0.0.15      //Administración -> Ventas ❌
Router(config)#access-list 101 deny ip 130.10.2.0 0.0.0.63 130.10.2.128 0.0.0.31      //Administración -> Finanzas ❌
Router(config)#access-list 101 deny ip 130.10.2.0 0.0.0.63 130.10.2.160 0.0.0.31      //Administración -> Logística ❌
Router(config)#access-list 101 deny ip 130.10.2.0 0.0.0.63 130.10.2.64 0.0.0.15      //Administración -> Sistemas ❌
Router(config)#access-list 101 deny ip 130.10.2.0 0.0.0.63 130.10.0.0 0.0.0.63      //Administración -> Administración ❌
Router(config)#access-list 101 deny ip 130.10.2.0 0.0.0.63 130.10.0.80 0.0.0.15      //Administración -> Marketing ❌
Router(config)#access-list 101 deny ip 130.10.2.0 0.0.0.63 130.10.0.96 0.0.0.15      //Administración -> Ventas ❌
Router(config)#access-list 101 deny ip 130.10.2.0 0.0.0.63 130.10.0.128 0.0.0.31      //Administración -> Finanzas ❌
Router(config)#access-list 101 deny ip 130.10.2.0 0.0.0.63 130.10.0.160 0.0.0.31      //Administración -> Logística ❌
Router(config)#access-list 101 deny ip 130.10.2.0 0.0.0.63 130.10.0.64 0.0.0.15      //Administración -> Sistemas ❌
Router(config)#access-list 101 deny ip 130.10.2.0 0.0.0.63 130.10.1.0 0.0.0.63      //Administración -> Administración ❌
Router(config)#access-list 101 deny ip 130.10.2.0 0.0.0.63 130.10.1.80 0.0.0.15      //Administración -> Marketing ❌
Router(config)#access-list 101 deny ip 130.10.2.0 0.0.0.63 130.10.1.96 0.0.0.15      //Administración -> Ventas ❌
Router(config)#access-list 101 deny ip 130.10.2.0 0.0.0.63 130.10.1.128 0.0.0.31      //Administración -> Finanzas ❌
Router(config)#access-list 101 deny ip 130.10.2.0 0.0.0.63 130.10.1.160 0.0.0.31      //Administración -> Logística ❌
Router(config)#access-list 101 deny ip 130.10.2.0 0.0.0.63 130.10.1.64 0.0.0.15      //Administración -> Sistemas ❌

Router(config)#access-list 101 deny ip 130.10.2.64 0.0.0.15 130.10.2.80 0.0.0.15      //Sistemas -> Marketing ❌
Router(config)#access-list 101 deny ip 130.10.2.64 0.0.0.15 130.10.2.96 0.0.0.15      //Sistemas -> Ventas ❌
Router(config)#access-list 101 deny ip 130.10.2.64 0.0.0.15 130.10.2.128 0.0.0.31      //Sistemas -> Finanzas ❌
Router(config)#access-list 101 deny ip 130.10.2.64 0.0.0.15 130.10.2.160 0.0.0.31      //Sistemas -> Logística ❌
Router(config)#access-list 101 deny ip 130.10.2.64 0.0.0.15 130.10.2.0 0.0.0.63      //Sistemas -> Administración ❌
Router(config)#access-list 101 deny ip 130.10.2.64 0.0.0.15 130.10.1.64 0.0.0.15      //Sistemas -> Sistemas ❌
Router(config)#access-list 101 deny ip 130.10.2.64 0.0.0.15 130.10.1.80 0.0.0.15      //Sistemas -> Marketing ❌
Router(config)#access-list 101 deny ip 130.10.2.64 0.0.0.15 130.10.1.96 0.0.0.15      //Sistemas -> Ventas ❌
Router(config)#access-list 101 deny ip 130.10.2.64 0.0.0.15 130.10.1.128 0.0.0.31      //Sistemas -> Finanzas ❌
Router(config)#access-list 101 deny ip 130.10.2.64 0.0.0.15 130.10.1.160 0.0.0.31      //Sistemas -> Logística ❌
Router(config)#access-list 101 deny ip 130.10.2.64 0.0.0.15 130.10.1.0 0.0.0.63      //Sistemas -> Administración ❌
Router(config)#access-list 101 deny ip 130.10.2.64 0.0.0.15 130.10.0.64 0.0.0.15      //Sistemas -> Sistemas ❌
Router(config)#access-list 101 deny ip 130.10.2.64 0.0.0.15 130.10.0.80 0.0.0.15      //Sistemas -> Marketing ❌
Router(config)#access-list 101 deny ip 130.10.2.64 0.0.0.15 130.10.0.96 0.0.0.15      //Sistemas -> Ventas ❌
Router(config)#access-list 101 deny ip 130.10.2.64 0.0.0.15 130.10.0.128 0.0.0.31      //Sistemas -> Finanzas ❌
Router(config)#access-list 101 deny ip 130.10.2.64 0.0.0.15 130.10.0.160 0.0.0.31      //Sistemas -> Logística ❌
Router(config)#access-list 101 deny ip 130.10.2.64 0.0.0.15 130.10.0.0 0.0.0.63      //Sistemas -> Administración ❌

Router(config)#access-list 101 deny ip 130.10.2.80 0.0.0.15 130.10.2.64 0.0.0.15      //Marketing -> Sistemas ❌
Router(config)#access-list 101 deny ip 130.10.2.80 0.0.0.15 130.10.2.96 0.0.0.15      //Marketing -> Ventas ❌
Router(config)#access-list 101 deny ip 130.10.2.80 0.0.0.15 130.10.2.128 0.0.0.31      //Marketing -> Finanzas ❌
Router(config)#access-list 101 deny ip 130.10.2.80 0.0.0.15 130.10.2.160 0.0.0.31      //Marketing -> Logística ❌
Router(config)#access-list 101 deny ip 130.10.2.80 0.0.0.15 130.10.2.0 0.0.0.63      //Marketing -> Administración ❌
Router(config)#access-list 101 deny ip 130.10.2.80 0.0.0.15 130.10.1.80 0.0.0.15      //Marketing -> Marketing ❌
Router(config)#access-list 101 deny ip 130.10.2.80 0.0.0.15 130.10.1.64 0.0.0.15      //Marketing -> Sistemas ❌
Router(config)#access-list 101 deny ip 130.10.2.80 0.0.0.15 130.10.1.96 0.0.0.15      //Marketing -> Ventas ❌
Router(config)#access-list 101 deny ip 130.10.2.80 0.0.0.15 130.10.1.128 0.0.0.31      //Marketing -> Finanzas ❌
Router(config)#access-list 101 deny ip 130.10.2.80 0.0.0.15 130.10.1.160 0.0.0.31      //Marketing -> Logística ❌
Router(config)#access-list 101 deny ip 130.10.2.80 0.0.0.15 130.10.1.0 0.0.0.63      //Marketing -> Administración ❌
Router(config)#access-list 101 deny ip 130.10.2.80 0.0.0.15 130.10.0.80 0.0.0.15      //Marketing -> Marketing ❌
Router(config)#access-list 101 deny ip 130.10.2.80 0.0.0.15 130.10.0.64 0.0.0.15      //Marketing -> Sistemas ❌
Router(config)#access-list 101 deny ip 130.10.2.80 0.0.0.15 130.10.0.96 0.0.0.15      //Marketing -> Ventas ❌
Router(config)#access-list 101 deny ip 130.10.2.80 0.0.0.15 130.10.0.128 0.0.0.31      //Marketing -> Finanzas ❌
Router(config)#access-list 101 deny ip 130.10.2.80 0.0.0.15 130.10.0.160 0.0.0.31      //Marketing -> Logística ❌
Router(config)#access-list 101 deny ip 130.10.2.80 0.0.0.15 130.10.0.0 0.0.0.63      //Marketing -> Administración ❌

Router(config)#access-list 101 deny ip 130.10.2.96 0.0.0.15 130.10.2.64 0.0.0.15      //Ventas -> Sistemas ❌
Router(config)#access-list 101 deny ip 130.10.2.96 0.0.0.15 130.10.2.80 0.0.0.15      //Ventas -> Marketing ❌
Router(config)#access-list 101 deny ip 130.10.2.96 0.0.0.15 130.10.2.128 0.0.0.31      //Ventas -> Finanzas ❌
Router(config)#access-list 101 deny ip 130.10.2.96 0.0.0.15 130.10.2.160 0.0.0.31      //Ventas -> Logística ❌
Router(config)#access-list 101 deny ip 130.10.2.96 0.0.0.15 130.10.2.0 0.0.0.63      //Ventas -> Administración ❌
Router(config)#access-list 101 deny ip 130.10.2.96 0.0.0.15 130.10.1.96 0.0.0.15      //Ventas -> Ventas ❌
Router(config)#access-list 101 deny ip 130.10.2.96 0.0.0.15 130.10.1.64 0.0.0.15      //Ventas -> Sistemas ❌
Router(config)#access-list 101 deny ip 130.10.2.96 0.0.0.15 130.10.1.80 0.0.0.15      //Ventas -> Marketing ❌
Router(config)#access-list 101 deny ip 130.10.2.96 0.0.0.15 130.10.1.128 0.0.0.31      //Ventas -> Finanzas ❌
Router(config)#access-list 101 deny ip 130.10.2.96 0.0.0.15 130.10.1.160 0.0.0.31      //Ventas -> Logística ❌
Router(config)#access-list 101 deny ip 130.10.2.96 0.0.0.15 130.10.1.0 0.0.0.63      //Ventas -> Administración ❌
Router(config)#access-list 101 deny ip 130.10.2.96 0.0.0.15 130.10.0.96 0.0.0.15      //Ventas -> Ventas ❌
Router(config)#access-list 101 deny ip 130.10.2.96 0.0.0.15 130.10.0.64 0.0.0.15      //Ventas -> Sistemas ❌
Router(config)#access-list 101 deny ip 130.10.2.96 0.0.0.15 130.10.0.80 0.0.0.15      //Ventas -> Marketing ❌
Router(config)#access-list 101 deny ip 130.10.2.96 0.0.0.15 130.10.0.128 0.0.0.31      //Ventas -> Finanzas ❌
Router(config)#access-list 101 deny ip 130.10.2.96 0.0.0.15 130.10.0.160 0.0.0.31      //Ventas -> Logística ❌
Router(config)#access-list 101 deny ip 130.10.2.96 0.0.0.15 130.10.0.0 0.0.0.63      //Ventas -> Administración ❌

Router(config)#access-list 101 deny ip 130.10.2.128 0.0.0.31 130.10.2.64 0.0.0.15      //Finanzas -> Sistemas ❌
Router(config)#access-list 101 deny ip 130.10.2.128 0.0.0.31 130.10.2.80 0.0.0.15      //Finanzas -> Marketing ❌
Router(config)#access-list 101 deny ip 130.10.2.128 0.0.0.31 130.10.2.96 0.0.0.15      //Finanzas -> Ventas ❌
Router(config)#access-list 101 deny ip 130.10.2.128 0.0.0.31 130.10.2.160 0.0.0.31      //Finanzas -> Logística ❌
Router(config)#access-list 101 deny ip 130.10.2.128 0.0.0.31 130.10.2.0 0.0.0.63      //Finanzas -> Administración ❌
Router(config)#access-list 101 deny ip 130.10.2.128 0.0.0.31 130.10.1.128 0.0.0.31      //Finanzas -> Finanzas ❌
Router(config)#access-list 101 deny ip 130.10.2.128 0.0.0.31 130.10.1.64 0.0.0.15      //Finanzas -> Sistemas ❌
Router(config)#access-list 101 deny ip 130.10.2.128 0.0.0.31 130.10.1.80 0.0.0.15      //Finanzas -> Marketing ❌
Router(config)#access-list 101 deny ip 130.10.2.128 0.0.0.31 130.10.1.96 0.0.0.15      //Finanzas -> Ventas ❌
Router(config)#access-list 101 deny ip 130.10.2.128 0.0.0.31 130.10.1.160 0.0.0.31      //Finanzas -> Logística ❌
Router(config)#access-list 101 deny ip 130.10.2.128 0.0.0.31 130.10.1.0 0.0.0.63      //Finanzas -> Administración ❌
Router(config)#access-list 101 deny ip 130.10.2.128 0.0.0.31 130.10.0.128 0.0.0.31      //Finanzas -> Finanzas ❌
Router(config)#access-list 101 deny ip 130.10.2.128 0.0.0.31 130.10.0.64 0.0.0.15      //Finanzas -> Sistemas ❌
Router(config)#access-list 101 deny ip 130.10.2.128 0.0.0.31 130.10.0.80 0.0.0.15      //Finanzas -> Marketing ❌
Router(config)#access-list 101 deny ip 130.10.2.128 0.0.0.31 130.10.0.96 0.0.0.15      //Finanzas -> Ventas ❌
Router(config)#access-list 101 deny ip 130.10.2.128 0.0.0.31 130.10.0.160 0.0.0.31      //Finanzas -> Logística ❌
Router(config)#access-list 101 deny ip 130.10.2.128 0.0.0.31 130.10.0.0 0.0.0.63      //Finanzas -> Administración ❌

Router(config)#access-list 101 deny ip 130.10.2.160 0.0.0.31 130.10.2.64 0.0.0.15      //Logística -> Sistemas ❌
Router(config)#access-list 101 deny ip 130.10.2.160 0.0.0.31 130.10.2.80 0.0.0.15      //Logística -> Marketing ❌
Router(config)#access-list 101 deny ip 130.10.2.160 0.0.0.31 130.10.2.96 0.0.0.15      //Logística -> Ventas ❌
Router(config)#access-list 101 deny ip 130.10.2.160 0.0.0.31 130.10.2.128 0.0.0.31      //Logística -> Finanzas ❌
Router(config)#access-list 101 deny ip 130.10.2.160 0.0.0.31 130.10.2.0 0.0.0.63      //Logística -> Administración ❌
Router(config)#access-list 101 deny ip 130.10.2.160 0.0.0.31 130.10.1.160 0.0.0.31      //Logística -> Logística ❌
Router(config)#access-list 101 deny ip 130.10.2.160 0.0.0.31 130.10.1.64 0.0.0.15      //Logística -> Sistemas ❌
Router(config)#access-list 101 deny ip 130.10.2.160 0.0.0.31 130.10.1.80 0.0.0.15      //Logística -> Marketing ❌
Router(config)#access-list 101 deny ip 130.10.2.160 0.0.0.31 130.10.1.96 0.0.0.15      //Logística -> Ventas ❌
Router(config)#access-list 101 deny ip 130.10.2.160 0.0.0.31 130.10.1.128 0.0.0.31      //Logística -> Finanzas ❌
Router(config)#access-list 101 deny ip 130.10.2.160 0.0.0.31 130.10.1.0 0.0.0.63      //Logística -> Administración ❌
Router(config)#access-list 101 deny ip 130.10.2.160 0.0.0.31 130.10.0.160 0.0.0.31      //Logística -> Logística ❌
Router(config)#access-list 101 deny ip 130.10.2.160 0.0.0.31 130.10.0.64 0.0.0.15      //Logística -> Sistemas ❌
Router(config)#access-list 101 deny ip 130.10.2.160 0.0.0.31 130.10.0.80 0.0.0.15      //Logística -> Marketing ❌
Router(config)#access-list 101 deny ip 130.10.2.160 0.0.0.31 130.10.0.96 0.0.0.15      //Logística -> Ventas ❌
Router(config)#access-list 101 deny ip 130.10.2.160 0.0.0.31 130.10.0.128 0.0.0.31      //Logística -> Finanzas ❌
Router(config)#access-list 101 deny ip 130.10.2.160 0.0.0.31 130.10.0.0 0.0.0.63      //Logística -> Administración ❌

Router(config)#access-list 101 permit ip any any      //Permitir el resto (como respuestas, navegación, etc.)

Router(config)#interface g0/1.10      //Cambiar el número de acuerdo al área correspondiente

Router(config-if)#ip access-group 101 in

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