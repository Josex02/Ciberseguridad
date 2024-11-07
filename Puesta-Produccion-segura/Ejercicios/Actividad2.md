# 1. Haz un script llamado multiplo10.sh que pida un número por teclado e indique si es un múltiplo de 10 o no.

````
#!/bin/bash
read -p "Introduce un número: " num
if (( num % 10 == 0 )); then
    echo "$num es múltiplo de 10."
else
    echo "$num no es múltiplo de 10."
fi
````

# 2. Haz un script llamado altura_mayor.sh, que pida por teclado la altura en centímetros
de tres personas y nos diga la más alta de las tres en metros.

````
#!/bin/bash
read -p "Introduce la altura de la primera persona en cm: " altura1
read -p "Introduce la altura de la segunda persona en cm: " altura2
read -p "Introduce la altura de la tercera persona en cm: " altura3

mayor=$(( altura1 > altura2 ? altura1 : altura2 ))
mayor=$(( altura3 > mayor ? altura3 : mayor ))

echo "La mayor altura es: $((mayor / 100)).$((mayor % 100)) metros."
````

# 3. Haz un script llamado cuenta10ficheros.sh, que nos diga si en el directorio pasado
como parámetro hay más de 10 ficheros o no, es decir, los directorios no deben ser
contados.

````
#!/bin/bash
if [ -d "$1" ]; then
  num_files=$(ls -l "$1" | grep -c '^-')
  if (( num_files > 10 )); then
    echo "Hay más de 10 archivos."
  else
    echo "No hay más de 10 archivos."
  fi
else
  echo "El directorio no existe."
fi
````

# 4. Haz un script llamado decada_edad.sh que, dada una edad introducida por teclado,
nos devuelva como resultado la década en la que nacimos (ejemplo 1970, 1980, etc.).
Suponemos que la edad introducida está entre 15 y 60 años. El script debe coger el año
actual de forma automática.
La salida debe producirse en el siguiente formato: “Si naciste en 1983, naciste en la
década de 1980”.

````
#!/bin/bash
read -p "Introduce tu edad: " edad
año_actual=$(date +%Y)
año_nacimiento=$((año_actual - edad))
decada=$(( (año_nacimiento / 10) * 10 ))

echo "Si naciste en $año_nacimiento, naciste en la década de $decada."
````

# 5. Haz un script llamado diadelmes.sh que nos diga cuántos días tiene el mes actual en
el momento de su ejecución (se considera que febrero tiene 28 días). La salida debe
producirse en el siguiente formato: “Estamos en noviembre, un mes con 30 días”.

````
#!/bin/bash
mes_actual=$(date +%B)
dias=$(cal | awk 'NF {DAYS = $NF}; END {print DAYS}')

echo "Estamos en $mes_actual, un mes con $dias días."
````

# 6. Haz un script llamado horoscopochino.sh, que pida el año en que nacimos (4 cifras) y
nos diga por pantalla qué animal nos corresponde según el horóscopo chino. Para
calcularlo debemos dividir el año entre 12 y el resto nos indicará el animal según la
siguiente tabla

````
#!/bin/bash
read -p "Introduce tu año de nacimiento (4 cifras): " año
animales=("La rata" "El buey" "El tigre" "El conejo" "El dragón" "La serpiente" "El caballo" "La cabra" "El mono" "El gallo" "El perro" "El cerdo")

resto=$(( año % 12 ))
echo "Según el horóscopo chino, eres ${animales[resto]}."
````

# 7. Haz un script llamado sumarango.sh, que pida dos números por teclado y calcule la
suma de los números que conforman ese rango. Por ejemplo: Si introducimos el 5 y el
8 debemos mostrar el 26 por pantalla que es el resultado de sumar 5+6+7+8.
El programa comprobará qué número es menor antes de calcular la suma del rango
para poder invertir el orden en caso necesario.

````
#!/bin/bash
read -p "Introduce el primer número: " num1
read -p "Introduce el segundo número: " num2

if (( num1 > num2 )); then
  temp=$num1
  num1=$num2
  num2=$temp
fi

suma=0
for (( i = num1; i <= num2; i++ )); do
  suma=$((suma + i))
done

echo "La suma del rango es: $suma"
````

# 8. Realizar un script llamado usuarios.sh que muestre la siguiente información de un
usuario del sistema pasado por parámetro: nombre de usuario, UID, GID y directorio de
trabajo.
Cuando se muestre la información el script debe preguntar si quiere introducir otro
usuario para mostrar su información o si se quiere salir del programa.
Se debe verificar que ese usuario está dado de alta en el sistema y por supuesto deberá
mostrarse por pantalla el mensaje oportuno de darse tal circunstancia. Los errores
arrojados por los comandos empleados serán enviados a un log destinado a ello,
aunque el script avisará por pantalla si el usuario no existe.

````
#!/bin/bash
while true; do
  read -p "Introduce el nombre de usuario: " usuario
  if id "$usuario" &>/dev/null; then
    echo "Nombre de usuario: $usuario"
    echo "UID: $(id -u $usuario)"
    echo "GID: $(id -g $usuario)"
    echo "Directorio de trabajo: $(eval echo ~$usuario)"
  else
    echo "El usuario $usuario no existe."
  fi
  read -p "¿Quieres introducir otro usuario? (s/n): " respuesta
  [[ "$respuesta" != "s" ]] && break
done
````

# 9. Hacer un script llamado copia_scripts.sh, que haga un copiado de los scripts (archivos
con extensión sh) creados en la carpeta pasada como parámetro, deben ser
empaquetados con el comando tar y el nombre del archivo debe tener el siguiente
formato: “copia_scripts_ddmmaaaa.tar” siendo dd el día, mm el mes y aaaa el año en el
que se produce la copia.

````
#!/bin/bash
if [ -d "$1" ]; then
  fecha=$(date +%d%m%Y)
  tar -cvf "copia_scripts_$fecha.tar" "$1"/*.sh
  echo "Copia creada: copia_scripts_$fecha.tar"
else
  echo "El directorio no existe."
fi
````









