# rcnotes
Create, edit, read ... your notes in any format accessing a multitude of public clouds through rclone




Instalación
-----------

Clona el repositorio en tu máquina local

Primer uso
----------

Si hacemos un `n h` para ver la ayuda, rcnotes nos preguntará:

*   ¿Que editor de texto quieres utilizar para configurar rcnotes?:
*   No has indicado ningún archivo de configuración o no existe. ¿Quieres crearlo?:

Si le decimos que si, nos abrirá un archivo vacio, que será el archivo de configuración, con el editor que previamente habiamos inidicado.

Copia la siguiente plantilla de archivo de configuración:

    ##### Notas ############################
    CLOUDDIRNOTASLOCAL="/home/angel/Notas"
    CLOUDDIRNOTAS="wd:Notas" 
    QUICKNOTE="wd:Notas/QuickNote.md"
    MVTAG="/home/angel/Notas"          # Mover notas por etiqueta
    TIME="1"                           # Tiempo necesario para que de tiempo a montar la unidad
                                       # mínimo tiempo necesario 1. Dependerá de la máquina que utilices
    
    #### Editores ###########################
    EDITORMD="emacs -nw"
    EDITORMD2="micro"
    EDITORORG="emacs -nw "
    EDITORMEMORY="emacs -nw -f deft"
    
    
    #### logs #################################
    LOGS="wd:logs"                      # Directorio de logs
    LOGSS="wd:logs/rcnotes.log"         # Archivo de logs
    
    #### Nubes. Control de versiones, backup,...
    CLOUD="wd:"
    CLOUD2="wd2:"
    CONFIG="/home/angel/.config/rcnotes/cv.conf"
    
    #### Org #####################################
    CLOUDCONVERTORG="wd:Notas/org/convert"
    CLOUDDIRNOTASORG="wd:org"
    CLOUDCONVERTMD="wd:Notas/Zettel/ordenado/"

Si sales del archivo de configuración y quieres volver, utiliza el comando:

    n config

### Archivo logs.conf

Añade el siguiente:

    #!/bin/bash
    
    
    ## Mover archivos y clasificarlos por etiquetas
    if [ "$1" = "mv-tags" ]
    then
    echo -ne "$(rclone cat $LOGS/rcnotes.log)\n$(date +'%Y/%m/%d %T')  :  MOVE NOTES FOR TAGS" | rclone rcat $LOGS/rcnotes.log
    fi
    
    
    if [ "$1" = "d" ]
    then
    echo -ne "$(rclone cat $LOGS/rcnotes.log)\n$(date +'%Y/%m/%d %T')  :  DESCARGA DE NOTAS" | rclone rcat $LOGS/rcnotes.log
    fi
    
    
    if [ "$1" = "u" ]
    then
    echo -ne "$(rclone cat $LOGS/rcnotes.log)\n$(date +'%Y/%m/%d %T')  :  SUBIDA AL SERVIDOR NOTAS" | rclone rcat $LOGS/rcnotes.log
    fi
    
    if [ "$1" = "clean" ]
    then
    echo -ne "$(rclone cat $LOGS/rcnotes.log)\n$(date +'%Y/%m/%d %T')  :  SUBIDA AL SERVIDOR NOTAS" | rclone rcat $LOGS/rcnotes.log
    fi
    

Archivo de plugins
------------------

Crea el archivo:

    touch ~/.config/rcnotes/rcnotes.pg

En este archivo podrás añadir tus opciones personalizadas
