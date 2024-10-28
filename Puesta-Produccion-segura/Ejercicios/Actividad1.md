# 1. Script que muestra en pantalla el nombre del script

````
#!/bin/bash

echo "El nombre del script es: $0"
````

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





