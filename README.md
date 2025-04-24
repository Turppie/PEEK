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


CONEXIÓN ENTRE 2 SWITCHS
Switch>ENA
Switch#configure ter
Switch(config)#interface g0/1      //Cambiar el número de puerto de conexión entre los switchs
Switch(config-if)#switchport mode trunk
Switch(config-if)#exit

//Hacer lo mismo en los dos switchs que se conectan