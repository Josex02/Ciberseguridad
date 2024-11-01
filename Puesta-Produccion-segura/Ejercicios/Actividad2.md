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
