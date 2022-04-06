ACTIVITAT Storage Engines MySQL


ENUNCIAT 

Partint d'una màquina CentOS 7 amb el Percona Server 5.X instal·lat realitza els següents apartats a on es tracten els diferents Storage Engines que conté el MySQL i en conseqüència el Percona Server.


LLIURAMENT

L'entrega d'aquesta activitat correspon a la documentació de tots els passos corresponents a la instal·lació per tenir un SGBD MySQL Percona en funcionament.
En la documentació cal incloure les captures d'imatges que es creguin convenients.

Opcions de lliurament:
•	Utilitzar aquest document com a plantilla per l’entrega de l’activitat i penjar-la en tasca destinada a aquesta activitat dins del curs Moodle 
•	Realitzar la documentació sobre un repositori GIT (Bitbucket o GitLab). Utilitzant el format de fitxer MarkDown (MD). (1 punt)
•	Dins d'una WikiMedia. (1 punt)

Per les dues darreres opcions de lliurament caldrà indicar en el document penjat en el Moodle la URL a on es troba la documentació.




Activitat 1. REALITZA I/O RESPON ELS SEGÜENTS APARTATS (obligatòria) (1 punts)

•	Indica quins són els motors d’emmagatzematge que pots utilitzar (quins estan actius)? Mostra al comanda utilitzada i el resultat d’aquesta.

![image](https://user-images.githubusercontent.com/103138933/162034808-4f366bd8-9d71-44aa-9300-0845b5ff47b8.png)


•	Com puc saber quin és el motor d’emmagatzematge per defecte. Mostra com canviar aquest paràmetre de tal manera que les noves taules que creem a la BD per defecte utilitzin el motor MyISAM? 
Com podem veure a la comanda anterior per defecte el nostre motor d’emmagatzematge es InnoDB.

-Com canviar el motor d’emmagatzematge per defecte? Apliquem la seguent configuració en el arxiu /etc/my.cnf 
![image](https://user-images.githubusercontent.com/103138933/162034897-2b01649b-eeaa-405c-83b0-b193e604b352.png)

-Reiniciem el servei
 ![image](https://user-images.githubusercontent.com/103138933/162034964-02d1458a-6c01-44ff-8096-7abc2fe22ba4.png)

-Comprovem que ha canviat el MyISAM a default.
 ![image](https://user-images.githubusercontent.com/103138933/162034987-8caf240c-327c-4036-ae08-092fb2f3d73e.png)

•	Com podem saber quin és el motor d'emmagatzematge per defecte?
 ![image](https://user-images.githubusercontent.com/103138933/162035010-8a3f927b-c582-46a9-ad99-f329beda3849.png)
 
•	Explica els passos per instal·lar i activar l'ENGINE MyRocks. MyRocks és un motor d'emmagatzematge per MySQL basat en RocksDB (SGBD incrustat de tipus clau-valor). Aquest tipus d’emmagatzematge està optimitzat per ser molt eficient en les escriptures amb lectures acceptables.
-Instalem el MyRocks per Centos 7
![image](https://user-images.githubusercontent.com/103138933/162035065-6b83c212-3e41-4a47-ba2b-86ad4ac69c4b.png)
![image](https://user-images.githubusercontent.com/103138933/162035075-39bcb044-f8f9-4b9c-b58c-159f9df00f84.png)
![image](https://user-images.githubusercontent.com/103138933/162035089-57cdc0b9-f997-431e-ac1f-4cfd00f9f239.png)
![image](https://user-images.githubusercontent.com/103138933/162035102-ff315e66-eea8-4ac8-bb75-c9c3dfd05e55.png)

•	Importa la BD Sakila com a taules MyISAM. Fes els canvis necessaris per importar la BD Sakila perquè totes les taules siguin de tipus MyISAM. 
-Canviar directament la inserció de les taules ja que en els creates esta especificat que les taules siguin InnoDB
![image](https://user-images.githubusercontent.com/103138933/162035158-3a09cc28-cd31-4054-907a-3f1487155da1.png)
![image](https://user-images.githubusercontent.com/103138933/162035178-078d9dfe-de78-49a9-a411-74f69231bd84.png)
![image](https://user-images.githubusercontent.com/103138933/162035191-6e3ade25-be16-4802-b529-1c7f21ceffe0.png)
Mira quins són els fitxers físics que ha creat, quan ocupen i quines són les seves extensions. Mostra'n una captura de pantalla i indica què conté cada fitxer.
Un cop fet això torna a deixar el motor InnoDB per defecte.

![image](https://user-images.githubusercontent.com/103138933/162035239-ab88a763-e990-4e70-be97-482b55447405.png)

-Tornem a configurar el arxiu /etc/my.cnf
Esborrem o comentem la seguent linea

![image](https://user-images.githubusercontent.com/103138933/162035313-7eb67391-01c4-4342-9730-3d8b0f6fdecd.png)

-Reiniciem el servei i tornem a mirar els engines per veure que tornem a tindre per defecte el InnoDB
![image](https://user-images.githubusercontent.com/103138933/162035364-eb7f84a3-a259-4692-af5f-3557f10ed359.png)

![image](https://user-images.githubusercontent.com/103138933/162035385-a806b54b-53ad-4871-b341-1b8e2decd314.png)

•	A partir de MySQL apareixen els schemas de metadades i informació guardats amb InnoDB. Busca informació d'aquests schemas. Indica quin és l'objectiu de cadascun d'ells i posa'n un exemple d'ús.
![image](https://user-images.githubusercontent.com/103138933/162035535-a41cdfd5-8073-43e9-8973-1683c53faccb.png)
- La INNODB_BUFFER_PAGE conté informació sobre cada pàgina a l'InnoDB grup de buffer.
-![image](https://user-images.githubusercontent.com/103138933/162035589-62deb7a5-9ecd-4f88-9178-72d9d137d083.png)
Aquesta taula és principalment útil per a la supervisió del rendiment de nivell expert o quan es desenvolupen extensions relacionades amb el rendiment per a MySQL.

- Quan s'eliminen taules, files de taules, particions o índexs, les pàgines associades romanen al grup de memòria intermitja fins que es requereix espai per a altres dades.
La INNODB_BUFFER_PAGE_LRU proporciona informació sobre aquestes pàgines fins que s'eliminen del grup de memòria intermèdia.
- La INNODB_BUFFER_POOL_STATS proporciona gran part de la mateixa informació del grup d'emmagatzematge intermedi proporcionada a SHOW ENGINE INNODB STATUS
![image](https://user-images.githubusercontent.com/103138933/162035661-ad2c2619-3e1d-43a0-9fd4-01676f86616f.png)

- Les taules INNODB_CMP i INNODB_CMP_RESET contenen informació d'estat sobre operacions relacionades amb taules comprimides. InnoDB
- ![image](https://user-images.githubusercontent.com/103138933/162035692-60437a6c-a9eb-48e9-9dd2-73c4fe40a202.png)

- Les taules INNODB_CMPMEM y INNODB_CMPMEM_RESET contenen informació d'estat sobre pàgines comprimides dins del grup de memòria intermèdia . InnoDB
- ![image](https://user-images.githubusercontent.com/103138933/162035807-de030b3b-9798-4204-8da2-aa9c6438c70c.png)

- Les taules INNODB_CMP_PER_INDEX i INNODB_CMP_PER_INDEX_RESET contenen informació d'estat sobre operacions relacionades amb taules i índexs comprimits InnoDB, amb estadístiques separades per a cada combinació de base de dades, taula i índex, per ajudar-lo a avaluar el rendiment i la utilitat de la compressió per a taules específiques.

- La INNODB_FT_BEING_DELETED és una instantània de la INNODB_FT_DELETED que només s'utilitza durant una OPTIMIZE TABLE ,operació de manteniment. Quan OPTIMIZE TABLE s'executa, la INNODB_FT_BEING_DELETED és buida i els DOC_ID s'eliminen de la INNODB_FT_DELETED.
 Com que els continguts d'INNODB_FT_BEING_DELETED solen tenir una vida útil curta, aquesta taula té una utilitat limitada per a la supervisió o la depuració.
- La INNODB_FT_CONFIG mostra metadades sobre l' FULLTEXT índex i el processament associat per a una InnoDB.
Abans de consultar aquesta taula, establiu la variable de configuració innodb_ft_aux_table amb el nom (inclòs el nom de la base de dades) de la taula que conté l' FULLTEXTíndex, per exemple test/articles.
- La INNODB_FT_DEFAULT_STOPWORD conté una llista de paraules limitades que s'utilitzen per defecte quan es crea un FULLTEXTíndex en una InnoDBtaula.
- La INNODB_FT_DELETED registra les files que s'eliminen de l' FULLTEXTíndex d'una InnoDB taula. Per evitar una costosa reorganització de l'índex durant les operacions de DML per a un InnoDB FULLTEXTíndex, la informació sobre les paraules acabades de suprimir s'emmagatzema per separat, es filtra dels resultats de la cerca quan feu una cerca de text i s'elimina de l'índex de cerca principal només quan emeteu la OPTIMIZE TABLEdeclaració de la InnoDBtaula. 
- INNODB_FT_INDEX_CACHE: Conté informació de testimoni sobre les files recentment inserides en un FULLTEXTíndex. Per evitar una costosa reorganització de l'índex durant les operacions DML, la informació sobre les paraules indexades noves s'emmagatzema per separat i es combina amb l'índex de cerca principal només quan OPTIMIZE TABLEs'executa, quan s'apaga el servidor o quan la mida de la memòria cau supera un límit definit per innodb_ft_cache_sizeo innodb_ft_total_cache_size.
- La INNODB_FT_INDEX_TABLE mostra informació sobre l'índex invertit utilitzat per processar cerques de text amb l' FULLTEXTíndex d'una InnoDBtaula.
- La INNODB_LOCKS conté informació sobre cada bloqueig que una InnoDBtransacció ha sol·licitat però encara no adquirit, i sobre cada bloqueig que té una transacció que està bloquejant una altra transacció.
- INNODB_TEMP_TABLE_INFO conté metadades sobre InnoDBtaules temporals actives. 

•	Posa un exemple que produeix un DEADLOCK i mostra-ho al professor.
L'anomenat punt mort DeadLock fa referència a un fenomen de dos o més processos que s'esperen l'un a l'altre a causa de la competència pels recursos durant el procés d'execució, sense força externa, no podran continuar. 
El sistema és en un estat de punt mort o el sistema té un punt mort. Aquests processos que sempre s'esperen entre ells es denominen processos de punt mort.
![image](https://user-images.githubusercontent.com/103138933/162035872-af06638b-9900-4e0d-8854-2755a4ad35b0.png)

Activitat 2. INNODB part I. REALITZA ELS SEGÜENTS APARTATS (obligatòria)  (2 punts)

•	Desactiva l’opció que ve per defecte de innodb_file_per_table
-Afegim la seguent linea en el arxiu my.cnf
![image](https://user-images.githubusercontent.com/103138933/162035888-21bd147a-75d1-419c-a119-07c078f4f9cd.png)
![image](https://user-images.githubusercontent.com/103138933/162035905-cf0e608b-3351-4ed1-b326-b826117ab49a.png)
![image](https://user-images.githubusercontent.com/103138933/162035941-97be29bc-e9ef-4f20-8d79-24119303044d.png)


•	Importa la BD Sakila com a taules InnoDB
•	Quin/quins són els fitxers de dades? A on es troben i quin és la seva mida?
![image](https://user-images.githubusercontent.com/103138933/162035953-6f033c59-ec5c-488b-a46b-f105ea5f244a.png)
![image](https://user-images.githubusercontent.com/103138933/162036109-eb61a6a7-2333-4fba-be93-4aab2d3536bd.png)

-Canvia la configuració del MySQL per:
•	Canviar la localització dels fitxers del tablespace de sistema per defecte a /discs-mysql/
Primer de tot crearem el nou directori
![image](https://user-images.githubusercontent.com/103138933/162036144-3066f341-b108-4091-b5df-b7f1eaacdb93.png)
Donem permisos pertinents
![image](https://user-images.githubusercontent.com/103138933/162036166-9f901f41-5090-4ec4-8f9b-0f71d1216423.png)

Aturem el servei per evitar problemes
![image](https://user-images.githubusercontent.com/103138933/162036227-920bcb70-ca97-4ac8-b8a1-07d5867af189.png)

Copiem les dades del antic directori al nou que hem creat
![image](https://user-images.githubusercontent.com/103138933/162036421-2f1db093-2cf6-4426-b966-f94019892ca4.png)
Instalem el seguent paquet per tal de aplicar polítiques al nou directori i així poder utilitzar-lo.
![image](https://user-images.githubusercontent.com/103138933/162036438-ee0dc118-6cc8-4212-8a52-16595f4079ab.png)

![image](https://user-images.githubusercontent.com/103138933/162036471-28c994eb-6ad1-4285-b1ba-4bf0c9cf9fb8.png)
Apliquem les polítiques
![image](https://user-images.githubusercontent.com/103138933/162036988-063b414b-235b-46a4-8fc7-2bb2b7af37f2.png)
Editem el arxiu my.cnf i posem la nova ruta del datadir

![image](https://user-images.githubusercontent.com/103138933/162037019-5ded2b20-3f42-4de2-8a20-52c3acd660ee.png)
Tornem a iniciar el servei de mysql i comprovem que tot funciona correctament
![image](https://user-images.githubusercontent.com/103138933/162037053-23b08bdd-8528-487c-b84d-a6189132633e.png)
Comprovem que el datadir ha canviat
![image](https://user-images.githubusercontent.com/103138933/162037121-d9ea1cf3-3a97-45f9-bd95-0e685d6feeea.png)
•	Tinguem dos fitxers corresponents al tablespace de sistema.
•	Tots dos han de tenir la mateixa mida inicial (10MB) 
•	El tablespace ha de créixer de 5MB en 5MB.
-Situa aquests fitxers (de manera relativa a la localització per defecte) en una nova localització simulant el següent:
•	/discs-mysql/disk1/primer fitxer de dades → simularà un disc dur
•	/discs-mysql/disk2/segon fitxer de dades → simularà un segon disc dur.

-Primer de tot crearem els fitxers i els i donarem els permisos corresponents
![image](https://user-images.githubusercontent.com/103138933/162037135-1f1977d7-0e82-4626-bdb4-16c9bd39e179.png)
![image](https://user-images.githubusercontent.com/103138933/162037167-b10ee62c-c583-4596-b05e-3c87af7ed08b.png)
![image](https://user-images.githubusercontent.com/103138933/162037221-824124f5-3cf9-453b-973a-588730a0db57.png)

-Esborrem els següents arxius per que tenen una mida molt mes gran a la que nosaltres volem configurar i per tant ens pot donar error
![image](https://user-images.githubusercontent.com/103138933/162037241-2c5a2aaf-c03c-43c1-9726-264581a2785c.png)
![image](https://user-images.githubusercontent.com/103138933/162037288-b25fc7ec-bf9c-46d0-9aff-d5e5de1e2342.png)

-Aturem el servei
![image](https://user-images.githubusercontent.com/103138933/162037340-faf9bf59-876e-4ced-8f39-f90a594d693f.png)

-Tornem a configurar el arxiu my.cnf
	-Apliquem la mida dels fitxers i la ruta que volem
![image](https://user-images.githubusercontent.com/103138933/162037484-bde682a6-c496-480f-b8fc-9799f355fc96.png)

Just aquí em falla i no se si es per la versió com ja ens vas dir.


Activitat 3. INNODB part II. REALITZA ELS SEGÜENTS APARTATS (obligatòria)  (1 punt)

•	Partint de l'esquema anterior configura el Percona Server perquè cada taula generi el seu propi tablespace en una carpeta anomenada tspaces (aquesta pot estar situada a on vulgueu).
•	Indica quins són els canvis de configuració que has realitzat.

-Apliquem la configuració per que cada taula generi el seu propi tablespace en aquest cas ja ho teníem aplicat anteriorment.
![image](https://user-images.githubusercontent.com/103138933/162037545-464e06e8-cd64-4ee7-b66d-a508502a3f05.png)

-Crearem el nou directori tspaces
![image](https://user-images.githubusercontent.com/103138933/162037580-2b69990e-bcf8-41a2-9194-dfccf098a608.png)

-Donem els permisos
![image](https://user-images.githubusercontent.com/103138933/162037703-c8d92287-80a9-4bcb-9bc2-8a9d29c36cc2.png)

-Aturem el servei per evitar problemes
![image](https://user-images.githubusercontent.com/103138933/162037740-c204014d-f21d-4e16-8bc3-3d0c96db9e5b.png)
-Copiem les dades del directori antic en el nou que hem creat
![image](https://user-images.githubusercontent.com/103138933/162037780-3d2515de-4541-44d7-bf72-a11a1a85dc0d.png)

-Apliquem les polítiques per poder utilitzar el directori
![image](https://user-images.githubusercontent.com/103138933/162037823-f9c59a81-7f32-4b59-b87c-157330668529.png)

-Tornem a iniciar el servei
![image](https://user-images.githubusercontent.com/103138933/162037872-a33fa373-732e-4d30-ae91-207da23a9729.png)

-Configurem el axiu my.cnf i apliquem la ruta del nou datadir
![image](https://user-images.githubusercontent.com/103138933/162037901-c745e8a2-2c9e-4655-a5a4-d644487ebf4f.png)

-Comprovem el nou datadir
![image](https://user-images.githubusercontent.com/103138933/162037958-8ae96305-c441-467d-b711-aab738ae676e.png)

Activitat 4. INNODB part III. REALITZA ELS SEGÜENTS APARTATS (obligatòria)  (1 punt)

•	Crea un tablespace anomenat 'ts1' situat a /discs-mysql/disc1/ i col·loca les taules actor, address i category de la BD Sakila.
![image](https://user-images.githubusercontent.com/103138933/162038048-7fb10147-6f55-4751-8f55-67e0da414c31.png)
![image](https://user-images.githubusercontent.com/103138933/162038083-44136af0-bec1-437f-9923-ae61a9e7dd9d.png)
•	Crea un altre tablespace anomenat 'ts2' situat a /discs-mysql/disc2/ i col·loca-hi la resta de taules.
![image](https://user-images.githubusercontent.com/103138933/162038104-d7935688-e325-478d-9b8c-3baa0a7436f4.png)
![image](https://user-images.githubusercontent.com/103138933/162038121-0d59e58a-b146-4852-b397-bec94a572396.png)
![image](https://user-images.githubusercontent.com/103138933/162038139-7ee096a7-dea7-4178-9710-d2515c05b47b.png)
![image](https://user-images.githubusercontent.com/103138933/162038177-eff26fb6-1274-4696-8409-bd8954f9c38c.png)

•	Comprova que pots realitzar operacions DML a les taules dels dos tablespaces.
![image](https://user-images.githubusercontent.com/103138933/162038188-f5a633a8-edca-4743-8df8-6cac9f6095f8.png)
![image](https://user-images.githubusercontent.com/103138933/162038238-87249815-e7f1-48b6-a5bb-f608ad5b2536.png)

•	Quines comandes i configuracions has realitzat per fer els dos apartats anteriors?
-Per tal de poder crear el ts1i el ts2, els e creat a /var/lib/mysql i despres els e mogut a la carpeta que hem demanes.
![image](https://user-images.githubusercontent.com/103138933/162038293-9c5740f2-be36-4c05-a8fb-1965762d8490.png)

Activitat 5. REDOLOG. REALITZA ELS SEGÜENTS APARTATS. (2 punt)

•	Com podem comprovar (Innodb Log Checkpointing):
![image](https://user-images.githubusercontent.com/103138933/162038414-ef9dba19-db76-409d-a632-617b7ea33c0b.png)
•	LSN (Log Sequence Number)
•	L'últim LSN actualitzat a disc
•	Quin és l'últim LSN que se li ha fet Checkpoint

![image](https://user-images.githubusercontent.com/103138933/162038431-03328cc0-454a-45e6-b2d0-930961ad7490.png)
![image](https://user-images.githubusercontent.com/103138933/162038486-0ec6a5ee-8d15-40ef-90b1-253eb2bcf3be.png)
![image](https://user-images.githubusercontent.com/103138933/162038555-27e79c7a-3b23-440d-8684-1202575727ce.png)

•	Proposa un exemple a on es vegi l'ús del redolog

•	Com podem mirar el número de pàgines modificades (dirty pages)? I el número total de pàgines?
![image](https://user-images.githubusercontent.com/103138933/162038679-35c5f306-c3d8-4c06-adda-b86029880ae5.png)

Activitat 6. Implentar BD Distribuïdes. (1,5 punts)

Com s'ha vist a classe MySQL proporciona el motor d'emmagatzemament FEDERATED que té com a funció permetre l'accés remot a bases de dades MySQL en un servidor local sense utilitzar tècniques de replicació ni clustering.

•	Prepara un Servidor Percona Server amb la BD de Sakila
•	Prepara un segon servidor Percona Server a on hi hauran un conjunt de taules FEDERADES al primer servdor.
•	Per realitzar aquest link entre les dues BD podem fer-ho de dues maneres:
•	Opció1: especificar TOTA la cadena de connexió a CONNECTION 
•	Opció2: especifficar una connexió a un server a CONNECTION que prèviament s'ha creat mitjançant CREATE SERVER
•	Posa un exemple de 2 taules de cada opció. 
Tingues en compte els permisos a nivell de BD i de SO així com temes de seguretat com firewalls, etc...
•	Detalla quines són els passos i comandes que has hagut de realitzar en cada màquina.

Activitat 7. Storage Engine CSV (0,5  punts)

•	Documenta i posa exemple de com utilitzar ENGINE CSV.
•	Cal documentar els passos que has hagut de realitzar per preparar l'exemple: configuracions, instruccions DML, DDL, etc....
![image](https://user-images.githubusercontent.com/103138933/162038706-641d1c7f-c033-4ba3-b557-ce81885c8c17.png)
![image](https://user-images.githubusercontent.com/103138933/162038742-f6792ead-1b06-4f88-8f93-622690b444f3.png)
-Modifiquem el arxiu manualment
![image](https://user-images.githubusercontent.com/103138933/162038764-2faaf014-4607-41f6-baf2-e0414531331d.png)
![image](https://user-images.githubusercontent.com/103138933/162038802-6d3128a5-9428-4e98-8c2b-f9b0915df977.png)
-Podem veure com també ha canviat a la base de dades.
![image](https://user-images.githubusercontent.com/103138933/162038844-6add7cd0-17a3-4de2-8d2a-68f7ef0733ea.png)

Activitat 8. Storage Engine MyRocks (1 punt)

A tenir en compte en cas de treballar amb Persona Server 8.x:
https://www.percona.com/doc/percona-server/8.0/upgrading_guide.html

![image](https://user-images.githubusercontent.com/103138933/162038900-54f4130f-865a-4aa4-b9b9-3791322bc0b1.png)
•	Documenta i posa exemple de com utilitzar ENGINE MyRocks. Crea una Base de dades amb 2 o 3 taules i inserta-hi contingut.
![image](https://user-images.githubusercontent.com/103138933/162038914-d8fb8ef1-8afc-4ee7-8b34-fec645d1966b.png)
![image](https://user-images.githubusercontent.com/103138933/162038944-5804ba36-6d69-4c4f-aaf7-f63c5c50cd18.png)
![image](https://user-images.githubusercontent.com/103138933/162038977-47c6240f-fc08-44b7-8c52-baef52521106.png)
![image](https://user-images.githubusercontent.com/103138933/162039002-01f316d2-90a0-4031-bd7a-e79c623368af.png)
![image](https://user-images.githubusercontent.com/103138933/162039043-1e1e5683-bb2d-4747-982f-001f5103e379.png)
![image](https://user-images.githubusercontent.com/103138933/162039053-b212351f-3408-48a1-be75-8c855a4fd524.png)
![image](https://user-images.githubusercontent.com/103138933/162039127-97d0ba4c-6430-4f30-ae32-8817e8c999e0.png)

•	Cal documentar els passos que has hagut de realitzar per preparar l'exemple: configuracions, instruccions DML, DDL, etc....
•	A quin directori es guarden els fitxers de dades? Fes un llistat de a on són els fitxers i què ocupen.

![image](https://user-images.githubusercontent.com/103138933/162039142-98e24ad4-52cd-43af-a33a-34da67979250.png)
![image](https://user-images.githubusercontent.com/103138933/162039191-e332053b-549e-4ca9-a2bd-050a87bc539c.png)
•	Quina és la compressió per defecte que utilitza per les taules? Com ho faries per canviar-lo. Per exemple utilitza Zlib o ZSTD o sense compressió.
![image](https://user-images.githubusercontent.com/103138933/162039249-8c0935cb-473a-4120-b6c9-b36c067dcfba.png)
-Configurem el arxiu my.cnf per tal de canviar el tipus de compressió
![image](https://user-images.githubusercontent.com/103138933/162039302-dde7054f-ba9b-45f3-aea9-2130d7c3565f.png)
-Comprovem que els canvis s’han efectuat correctament.
![Uploading image.png…]()
