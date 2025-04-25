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


CONEXIÓN ENTRE 2 SWITCHS O CON EL ROUTER
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
Router(config)#interface g0/0/0
Router(config-if)#no shutdown      //Para levantar el router
Router(config-if)#exit
Router(config)#interface g0/0/0.10      //Cambiar el número de acuerdo al área correspondiente
Router(config-subif)#interface g0/0/0.20
Router(config-subif)#interface g0/0/0.30
Router(config-subif)#interface g0/0/0.40
Router(config-subif)#interface g0/0/0.50
Router(config-subif)#interface g0/0/0.60
Router(config-subif)#exit
Router(config)#interface g0/0/0.10      //Aquí ya comienza la encapsulación para que cada subinterface se conecte a cada vlan
Router(config-subif)#encapsulation dot1Q 10      //Cambiar el número de acuerdo al área correspondiente
Router(config-subif)#ip address 130.10.0.1 255.255.255.128      //Cambiar la IP de acuerdo al Gateway de cada área según el excel, la máscara es igual para todos
Router(config-subif)#exit

//Video de referencia: https://www.youtube.com/watch?v=74N5yCCDwW8