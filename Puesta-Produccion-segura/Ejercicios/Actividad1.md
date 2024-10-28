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
