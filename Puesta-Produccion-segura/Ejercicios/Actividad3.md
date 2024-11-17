````
#!/bin/bash

# Función para mostrar el menú
menu() {
    echo "1.- EJECUTAR COPIA DE SEGURIDAD"
    echo "2.- DAR DE ALTA USUARIO"
    echo "3.- DAR DE BAJA AL USUARIO"
    echo "4.- MOSTRAR USUARIOS"
    echo "5.- MOSTRAR LOG DEL SISTEMA"
    echo "6.- SALIR"
}

# Función para la copia de seguridad
copia() {
    if [ ! -f "usuarios.csv" ]; then
        echo "Archivo usuarios.csv no existe. Creando archivo..."
        touch usuarios.csv
    fi
    fecha=$(date +"%d%m%Y_%H-%M-%S")
    zip "copia_usuarios_$fecha.zip" usuarios.csv
    echo "Copia de seguridad realizada: copia_usuarios_$fecha.zip"
    # Elimina copias antiguas manteniendo solo las 2 más recientes
    ls -t copia_usuarios_*.zip | tail -n +3 | xargs -d '\n' rm -f
    echo "COPIA realizada el $fecha" >> log.log
}

# Función para dar de alta un usuario
alta() {
    read -p "Nombre: " nombre
    read -p "Apellido1: " apellido1
    read -p "Apellido2: " apellido2
    read -p "DNI: " dni
    nombre_usuario=$(echo "${nombre:0:1}${apellido1:0:3}${apellido2:0:3}${dni: -3}" | tr '[:upper:]' '[:lower:]')

    if grep -q ":$nombre_usuario$" usuarios.csv; then
        echo "Usuario ya existe. No se puede agregar."
    else
        echo "$nombre:$apellido1:$apellido2:$dni:$nombre_usuario" >> usuarios.csv
        echo "INSERTADO $nombre:$apellido1:$apellido2:$dni:$nombre_usuario el $(date '+%d/%m/%Y a las %H:%M')h" >> log.log
        echo "Usuario $nombre_usuario añadido correctamente."
    fi
}

# Función para dar de baja un usuario
baja() {
    read -p "Introduzca el nombre de usuario a eliminar: " nombre_usuario
    if grep -q ":$nombre_usuario$" usuarios.csv; then
        grep -v ":$nombre_usuario$" usuarios.csv > temp.csv && mv temp.csv usuarios.csv
        echo "BORRADO $nombre_usuario el $(date '+%d/%m/%Y a las %H:%M')h" >> log.log
        echo "Usuario $nombre_usuario eliminado."
    else
        echo "Usuario no encontrado."
    fi
}

# Función para mostrar los usuarios
mostrar_usuarios() {
    if [ ! -s usuarios.csv ]; then
        echo "No hay usuarios registrados."
        return
    fi
    echo "Usuarios registrados:"
    sort -t ':' -k5 usuarios.csv | cut -d':' -f5
}

# Función para mostrar el log del sistema
mostrar_log() {
    if [ ! -f log.log ]; then
        echo "No hay registros de log disponibles."
    else
        cat log.log
    fi
}

# Pantalla de login
login() {
    intentos=0
    while [ $intentos -lt 3 ]; do
        read -sp "Ingrese su usuario: " usuario
        echo
        if [ "$usuario" == "admin" ]; then
            return 0
        elif grep -q ":$usuario$" usuarios.csv; then
            return 0
        else
            echo "Usuario no válido."
            ((intentos++))
        fi
    done
    echo "Número máximo de intentos alcanzado."
    exit 1
}

# Ejecuta la pantalla de login antes del menú
login

# Bucle para mostrar el menú y seleccionar opciones
while true; do
    menu
    read -p "Seleccione una opción: " opcion
    case $opcion in
        1) copia ;;
        2) alta ;;
        3) baja ;;
        4) mostrar_usuarios ;;
        5) mostrar_log ;;
        6) echo "Saliendo..."; exit 0 ;;
        *) echo "Opción no válida. Intente de nuevo." ;;
    esac
done
````
