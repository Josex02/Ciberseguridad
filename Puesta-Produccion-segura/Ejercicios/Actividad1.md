# 1. Script que muestra en pantalla el nombre del script

````
#!/bin/bash

echo "El nombre del script es: $0"
````
![image](https://github.com/user-attachments/assets/3a8eff6e-860c-4db7-923e-36424858a4dd)

# 2. Script que muestra el contenido de un archivo (pasado como segundo parámetro) y su exit code

````
#!/bin/bash

if [ -f "$2" ]; then
    cat "$2"
    echo "El exit code es: $?"
else
    echo "El archivo no existe o no es accesible."
    exit 1
fi
````
![image](https://github.com/user-attachments/assets/9575ae5a-b6d7-45a5-a955-7c028e31909b)

# 3. Script que crea un directorio y copia un archivo dentro de él

````
#!/bin/bash

if [ ! -d "$1" ]; then
    mkdir -p "$1"
    echo "Directorio '$1' creado."
fi

if [ -f "$2" ]; then
    cp "$2" "$1"
    echo "Archivo '$2' copiado en '$1'."
else
    echo "El archivo '$2' no existe."
    exit 1
fi
````
![image](https://github.com/user-attachments/assets/be0a544f-7dd6-4e06-8c45-bb8cb7330af0)

# 4. Script que cuenta y muestra los parámetros recibidos

````
#!/bin/bash

if [ $# -eq 0 ]; then
    echo "No has introducido ningún parámetro."
else
    echo "Has introducido $# parámetros."
    echo "Parámetros recibidos: $@"
fi
````
![image](https://github.com/user-attachments/assets/5dccb7b6-f53b-4880-a3a3-8ba659bc6e9a)

# 5. Modificación del script anterior para retornar códigos de salida

````
#!/bin/bash

if [ $# -eq 0 ]; then
    echo "No has introducido ningún parámetro."
    exit 1
else
    echo "Has introducido $# parámetros."
    echo "Parámetros recibidos: $@"
    exit 0
fi
````
![image](https://github.com/user-attachments/assets/94016229-e278-426a-8f54-42a561fdd3cf)

# 6. Repetición del ejercicio 3, verificando que se le han pasado al menos 2 parámetros

````
#!/bin/bash

if [ $# -lt 2 ]; then
    echo "Error: Se necesitan al menos 2 parámetros (directorio y archivo a copiar)."
    exit 1
fi

if [ ! -d "$1" ]; then
    mkdir -p "$1"
    echo "Directorio '$1' creado."
fi

if [ -f "$2" ]; then
    cp "$2" "$1"
    echo "Archivo '$2' copiado en '$1'."
else
    echo "El archivo '$2' no existe."
    exit 1
fi
````
![image](https://github.com/user-attachments/assets/be0a544f-7dd6-4e06-8c45-bb8cb7330af0)

# 7. Script que verifica si una ruta existe y determina si es archivo o directorio

````
#!/bin/bash

if [ -e "$1" ]; then
    if [ -f "$1" ]; then
        echo "'$1' es un archivo."
    elif [ -d "$1" ]; then
        echo "'$1' es un directorio."
    else
        echo "'$1' existe pero no es ni archivo ni directorio."
    fi
else
    echo "'$1' no existe."
fi
````

![image](https://github.com/user-attachments/assets/5ac87419-da2c-4d56-bfe9-cf4c01b26074)



