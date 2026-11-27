Buenasss, este sherlock es bien diferente a los demás que he hecho, aca no hay pcap ni logs que analizar, es un reto 100% de Threat Intelligence usando MITRE ATT&CK.

<img width="1650" height="616" alt="image" src="https://github.com/user-attachments/assets/a96c218b-3042-4486-b459-f96759033db7" />

El escenario nos pone como intern de Threat Intelligence en una empresa del sector ICS (Industrial Control Systems). El equipo nos pide investigar a fondo al grupo Sandworm Team, tambien conocido como BlackEnergy Group y APT44, y mapear su comportamiento usando el framework de MITRE ATT&CK. Empiezo directo en la pagina de Sandworm Team (ID G0034) en attack.mitre.org, donde se confirma que es un grupo atribuido al GRU ruso (unidad militar 74455) y que tiene varios alias asociados: ELECTRUM, Telebots, IRON VIKING, BlackEnergy, Quedagh, Voodoo Bear, IRIDIUM, Seashell Blizzard, FROZENBARENTS y APT44.

Bajando en esa misma pagina hasta Procedure Examples, en el procedimiento C0025 (2016 Ukraine Electric Power Attack) aparece el detalle de como Sandworm uso un script VBS para mover sus payloads lateralmente dentro de la red ICS, con el comando "cscript C:\Backinfo\ufn.vbs C:\Backinfo\101.dll C:\Delta\101.dll". Esta tecnica queda categorizada dentro de Brute Force y Command and Scripting Interpreter.

<img width="1917" height="875" alt="image" src="https://github.com/user-attachments/assets/fe7f93d1-58fd-4d2c-b424-1ff08237f8ad" />

Vuelvo a repasar la ficha de Sandworm Team para confirmar bien los datos base (ID del grupo, grupos asociados, contribuidores) antes de seguir, porque varias respuestas dependen de esta info.

<img width="1367" height="311" alt="image" src="https://github.com/user-attachments/assets/00458014-ed2c-4d29-ac4d-b67092ef7315" />

Hago zoom a la fila de C0025 para identificar bien cual es la primera tecnica listada en ese procedimiento, que es Brute Force.

<img width="1385" height="541" alt="image" src="https://github.com/user-attachments/assets/91ba1209-b341-4e5e-8907-1b6138cf8e87" />

Zoom a la tabla de Procedure Examples para leer completo el comando del script VBS mencionado arriba y confirmar la ruta exacta.

<img width="1440" height="728" alt="image" src="https://github.com/user-attachments/assets/a95cdd2c-71da-4daf-af8c-e884890473fb" />

Despues me voy a la tecnica Server Software Component: Web Shell (T1505.003) para revisar el procedimiento C0034 (2022 Ukraine Electric Power Attack), donde Sandworm Team desplego el webshell Neo-REGEORG en un servidor expuesto a internet.

<img width="1381" height="909" alt="image" src="https://github.com/user-attachments/assets/8bb47b63-2992-47f0-9de3-20608c8da04b" />

Siguiendo con el ataque de 2022, reviso las tecnicas ICS (T1701 y T0894) donde Sandworm utilizo un script VBS (lun.vbs) para ejecutar un batch (n.bat) que terminaba corriendo el binario de MicroSCADA scilc.exe con el comando "C:\sc\prog\exec\scilc.exe -do pack\scil\s1.txt", usado para enviar instrucciones SCADA no autorizadas a las subestaciones remotas.

<img width="1375" height="133" alt="image" src="https://github.com/user-attachments/assets/c6ea0585-6fb6-4a4e-b15b-06b4ea143296" />

En la tecnica T1485 (Data Destruction) confirmo las herramientas de borrado que ha usado el grupo: CaddyWiper, SDelete, el componente KillDisk de BlackEnergy, y la herramienta JUNKMAIL para sobrescribir archivos con bytes nulos.

<img width="1399" height="871" alt="image" src="https://github.com/user-attachments/assets/7c9fbcd9-d015-49a9-8224-4533f684a9f9" />

Entro al perfil del malware CaddyWiper (S0693) para revisar sus tecnicas asociadas: descubrimiento de archivos y directorios, modificacion de permisos ACL, y uso de la API SeTakeOwnershipPrivilege para tomar control de los archivos antes de sobrescribirlos.

<img width="1373" height="91" alt="image" src="https://github.com/user-attachments/assets/002808bc-be59-407e-9cbf-bd3e665e5c1b" />

Tambien reviso la tecnica T1593 (Search Open Websites/Domains), donde Sandworm investigo el identificador legal unico de Ucrania (EDRPOU) como parte de la preparacion del ataque NotPetya, ademas de otros sitios de terceros para armar correos de phishing creibles.

<img width="1416" height="245" alt="image" src="https://github.com/user-attachments/assets/d0bf3086-9203-42a2-833d-e67f78b99215" />

Otro dato relevante es el malware AcidRain (S1125), vinculado a Sandworm Team y usado en el incidente de Viasat KA-SAT en 2022, que dejo sin servicio a miles de terminales satelitales al inicio de la invasion a Ucrania.

<img width="1364" height="43" alt="image" src="https://github.com/user-attachments/assets/e4d8a8c5-8a93-491f-b234-7f9c0b19d61b" />

Por ultimo reviso la tecnica T1571 (Non-Standard Port), donde se confirma que Sandworm Team ha usado el puerto 6789 para aceptar conexiones en su servidor SSH.
<img width="1393" height="214" alt="image" src="https://github.com/user-attachments/assets/a289a4f2-0135-492f-80dd-d8f4d1eb4b8b" />

Con toda esta info mapeada en MITRE ATT&CK completo el reto. Este sherlock me sirvio bastante para practicar como hacer Threat Intelligence research de forma estructurada en vez de solo analizar paquetes o logs: aprendi a moverme en el framework de ATT&CK para sacar TTPs, software y procedimientos asociados a un grupo APT real.
