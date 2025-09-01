## **LAB1 _Базовая настройка коммутатора_**

## **ТОПОЛОГИЯ**    
![](ТОПОЛОГИЯ)
<img width="498" height="150" alt="image" src="https://github.com/user-attachments/assets/582bda9b-dcc5-4648-8d26-b5ce8d3cef71" />

### _Задание:_
### Часть 1. Проверка конфигурации коммутатора по умолчанию
### Часть 2. Создание сети и настройка основных параметров устройства    
  2.1 Настройте базовые параметры коммутатора;  
  2.2 Настройте IP-адрес для ПК.
### Часть 3. Проверка сетевых подключеий
  3.1 Отобразите конфигурацию устройства;  
  3.2	Протестируйте сквозное соединение, отправив эхо-запрос;  
  3.3	Протестируйте возможности удаленного управления с помощью Telnet.  

### *Решение:*
### Часть 1.
1. Для первоначальной настройки _коммутатора Cisco Catalyst 2960 S (модель WS-C2960-24TT-L)_ используем консольное подключение;
2. Командой **show running-config** смотрим, что файл конфигурации пустой:  
* Имя по умолчанию, пароли не установлены, VLAN1 не настроен и выключен (Down)   
* F/Ethernet интерфейсов - 24;  
* G/Ethernet интерфейсов - 2;  
* Диапозон значений, в **vtu-линиях** 0-4, 5-15.
3. Файл загрузочной конфигурации (NVRAM) пустой, т.к. сохранение из текущей конфигурации не производилось.
4. MAC-адрес SVI 00:04:9A:76:57:0D, интерфейс выключен (shutdown), IP-адрес не назначен.   
5. Версия ОС Cisco - 15.0(2)SE4, файл образа системы - LANBASEK9-M.
6. Интерфейс fastethernet 0/6-включен, MAC-адрес-00d0.58b3.0106, скорость-100000 Kbit.
7. Имя образа Cisco IOS - 2960-lanbasek9-mz.150-2.SE4.bin.
### Часть 2.  
1. Назначил IP-адресацию коммутатору и ПК, согласно заданию

| Устройство | Интерфейс | IP-адрес/префикс           | 
| ---------- | --------- | -------------------------- |  
| S1         | VLAN1     | 192.168.1.2 255.255.255.0  | 
| PC-A       | NIC       | 192.168.1.10 255.255.255.0 | 

2. Настроил пароли для пользовательского режима line console ( cisco ),
                   для привилигированного ( class),
                   для line VTY 0 4 ( cisco ),
                   зашифровал пароли service password-encryption
### Часть 3.                      
1. Конфигурация устройства           
Building configuration...  
Current configuration : 1196 bytes  
!  
version 15.0  
no service timestamps log datetime msec  
no service timestamps debug datetime msec  
*service password-encryption*   
!  
*hostname Switch*    
!  
*enable secret 5 $1$mERr$9cTjUIEqNGurQiFU.ZeCi1*    
!  
spanning-tree mode pvst  
spanning-tree extend system-id  
!  
interface FastEthernet0/1  
!  
interface FastEthernet0/2  
!  
interface FastEthernet0/3  
!  
interface FastEthernet0/4  
!  
interface FastEthernet0/5  
!  
interface FastEthernet0/6  
!  
interface FastEthernet0/7  
!  
interface FastEthernet0/8  
!  
interface FastEthernet0/9  
!  
interface FastEthernet0/10  
!  
interface FastEthernet0/11  
!  
interface FastEthernet0/12  
!  
interface FastEthernet0/13  
!  
interface FastEthernet0/14  
!  
interface FastEthernet0/15  
!  
interface FastEthernet0/16  
!  
interface FastEthernet0/17  
!  
interface FastEthernet0/18  
!  
interface FastEthernet0/19  
!  
interface FastEthernet0/20  
!  
interface FastEthernet0/21  
!  
interface FastEthernet0/22  
!  
interface FastEthernet0/23  
!  
interface FastEthernet0/24  
!  
interface GigabitEthernet0/1  
!  
interface GigabitEthernet0/2  
!  
*interface Vlan1*    
 *ip address 192.168.1.2 255.255.255.0*    
!  
*ip default-gateway 192.168.1.1*    
!   
*line con 0*    
 *password 7 0822455D0A16*    
 *login*    
!  
*line vty 0 4*    
 *password 7 0822455D0A16*    
 *login*    
line vty 5 15  
 login  
!  
end  

2. Утилитой ping проверяю IP связность устройств    
   C:\>ping 192.168.1.2

Pinging 192.168.1.2 with 32 bytes of data:

Reply from 192.168.1.2: bytes=32 time<1ms TTL=255  
Reply from 192.168.1.2: bytes=32 time<1ms TTL=255  
Reply from 192.168.1.2: bytes=32 time<1ms TTL=255  
Reply from 192.168.1.2: bytes=32 time<1ms TTL=255  

Ping statistics for 192.168.1.2:  
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),  
Approximate round trip times in milli-seconds:  
    Minimum = 0ms, Maximum = 0ms, Average = 0ms 
   
 3. Удалил консольный провод и с помощью программы эмуляции терминала подключаюсь командой Telnet к коммутатору
  
C:\>telnet 192.168.1.2  
Trying 192.168.1.2 ...Open  
User Access Verification  

Password:   
Switch>en  
Password:   
Switch#conf  

**Вопросы для повторения:** 
1. Без настройки пароля на виртуальных линиях коммутатора ( VTY ) удаленный доступ будет невозможен
2. Чтобы пароли не отправлялись в незашифрованном виде используем удаленный доступ с помощью SSH
