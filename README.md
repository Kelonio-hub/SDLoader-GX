# SDLOADER-GX
Método de Instaalación de cias en Nintendo 3DS mediante Godmode9
- Revisión 2025 -
_____________________________________________________________

set PREVIEW_MODE 0:/gm9/imagenes/imagenGX.png
cp -w -o -s 0:/gm9/scripts/AyudaTécnica.txt 0:/AyudaTécnica.txt	          

##################### Menu Principal ####################
@Start

labelsel -s "Selecciona una opcion." Menu19_*
goto Start

################################ INSTALACIÓN MANUAL ################################
@Menu19_Instalación_Manual

# Comprobamos si en la particion A: estan los archivos title.db e import.db
	if	not find A:/dbs/title.db NULL
		cp -w -o -s 0:/gm9/out/dbs/title.db A:/dbs/title.db
		fixcmac A:/dbs/title.db
	end
	
	if	not find A:/dbs/import.db NULL
		cp -w -o -s 0:/gm9/out/dbs/import.db A:/dbs/import.db
		fixcmac A:/dbs/import.db
	end

if	not filesel -d "Seleccione el archivo .cia" 0:/*.cia CIABAK 
			goto Start
		end
		if	not ask "Es esto correcto?\n \n$[CIABAK]?"
			goto Start
		end
install $[CIABAK] -s

echo "CIA instalado en tu Consola. \n#TeAmoKelonio"

if	not ask "Eliminar el CIA ya instalado?"
	goto Start
end
rm -o -s $[CIABAK]

echo "CIA eliminado de tu Tarjeta SD. \n#TeAmoKelonio"
goto Start
end

################################ INSTALACIÓN AUTOMÁTICA ################################
@Menu19_Instalación_Automática

# Comprobamos si en la particion A: estan los archivos title.db e import.db
	if	not find A:/dbs/title.db NULL
		cp -w -o -s 0:/gm9/out/dbs/title.db A:/dbs/title.db
		fixcmac A:/dbs/title.db
	end
	
	if	not find A:/dbs/import.db NULL
		cp -w -o -s 0:/gm9/out/dbs/import.db A:/dbs/import.db
		fixcmac A:/dbs/import.db
	end
	
@CIALLBAK

    if find 0:/GX/*.cia CIALLBAK 
		install $[CIALLBAK] -s
		rm -o -s $[CIALLBAK]
		goto CIALLBAK
	else 
	if not find 0:/GX/*.cia CIALLBAK 
	echo "CIAs instalados en tu consola. \n#TeAmoKelonio"
	goto Start
	end
end

####################### Opciones de Apagado ######################
@Menu19_Opciones_de_Apagado
labelsel -s "Selecciona una opcion." Power_*

####################### Reiniciar consola ######################
@Power_Reiniciar_Consola
reboot

####################### Apagar consola ######################
@Power_Apagar_Consola
poweroff

####################### Salir ######################
@Power_Salir_a_Godmode9
