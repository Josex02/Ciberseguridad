````

import os
import csv

def menu():
    print("""
    Menú de Opciones:
    1.- EJECUTAR COPIA DE SEGURIDAD
    2.- DAR DE ALTA USUARIO
    3.- DAR DE BAJA AL USUARIO
    4.- MOSTRAR USUARIOS
    5.- MOSTRAR LOG DEL SISTEMA
    6.- SALIR
    """)

def verifica_archivo():
    if not os.path.exists("usuarios.csv"):
        with open("usuarios.csv", "w", newline='') as archivo:
            writer = csv.writer(archivo, delimiter=':')
            writer.writerow(["Nombre", "Apellido1", "Apellido2", "Dni", "NombreDeUsuario"])

def generauser(nombre, apellido1, apellido2, dni):
    nombre_usuario = (nombre[0] + apellido1[:3] + apellido2[:3] + dni[-3:]).lower()
    return nombre_usuario

def ejecutar_copia_seguridad():
    print("Ejecutando copia de seguridad...")
    # Simulación de la copia de seguridad
    print("Copia de seguridad completada.")

def dar_alta_usuario():
    nombre = input("Introduce el nombre: ").strip()
    apellido1 = input("Introduce el primer apellido: ").strip()
    apellido2 = input("Introduce el segundo apellido: ").strip()
    dni = input("Introduce el DNI (8 dígitos y letra): ").strip().upper()

    if len(dni) != 9 or not dni[:-1].isdigit() or not dni[-1].isalpha():
        print("Error: El DNI no es válido.")
        return

    nombre_usuario = generauser(nombre, apellido1, apellido2, dni)

    with open("usuarios.csv", "a", newline='') as archivo:
        writer = csv.writer(archivo, delimiter=':')
        writer.writerow([nombre, apellido1, apellido2, dni, nombre_usuario])
    print(f"Usuario {nombre_usuario} dado de alta correctamente.")

def dar_baja_usuario():
    nombre_usuario = input("Introduce el nombre de usuario a dar de baja: ").strip().lower()
    encontrado = False
    usuarios = []

    with open("usuarios.csv", "r", newline='') as archivo:
        reader = csv.reader(archivo, delimiter=':')
        for linea in reader:
            if linea[4].lower() != nombre_usuario:
                usuarios.append(linea)
            else:
                encontrado = True
    
    if encontrado:
        with open("usuarios.csv", "w", newline='') as archivo:
            writer = csv.writer(archivo, delimiter=':')
            writer.writerows(usuarios)
        print(f"Usuario {nombre_usuario} dado de baja correctamente.")
    else:
        print("Usuario no encontrado.")

def mostrar_usuarios():
    try:
        with open("usuarios.csv", "r", newline='') as archivo:
            reader = csv.reader(archivo, delimiter=':')
            for linea in reader:
                print(":".join(linea))
    except FileNotFoundError:
        print("El archivo de usuarios no existe.")

def mostrar_log_sistema():
    print("Mostrando log del sistema (simulado)...")
    # Aquí se podría implementar la lógica de lectura de un archivo de log real

if __name__ == "__main__":
    verifica_archivo()
    while True:
        menu()
        opcion = input("Selecciona una opción (1-6): ").strip()

        if opcion == "1":
            ejecutar_copia_seguridad()
        elif opcion == "2":
            dar_alta_usuario()
        elif opcion == "3":
            dar_baja_usuario()
        elif opcion == "4":
            mostrar_usuarios()
        elif opcion == "5":
            mostrar_log_sistema()
        elif opcion == "6":
            print("Saliendo del programa...")
            break
        else:
            print("Opción no válida. Por favor, selecciona un número del 1 al 6.")
````

````
import os
import csv

def menu():
    print("""
    Menú de Opciones:
    1.- EJECUTAR COPIA DE SEGURIDAD
    2.- DAR DE ALTA USUARIO
    3.- DAR DE BAJA AL USUARIO
    4.- MOSTRAR USUARIOS
    5.- MOSTRAR LOG DEL SISTEMA
    6.- SALIR
    """)

def verifica_archivo():
    if not os.path.exists("usuarios.csv"):
        with open("usuarios.csv", "w", newline='', encoding='utf-8') as archivo:
            writer = csv.writer(archivo, delimiter=':')
            writer.writerow(["Nombre", "Apellido1", "Apellido2", "Dni", "NombreDeUsuario"])

def generauser(nombre, apellido1, apellido2, dni):
    return (nombre[0] + apellido1[:3] + apellido2[:3] + dni[-3:]).lower()

def ejecutar_copia_seguridad():
    print("Ejecutando copia de seguridad...")
    # Simulación de la copia de seguridad
    print("Copia de seguridad completada.")

def dar_alta_usuario():
    nombre = input("Introduce el nombre: ").strip()
    apellido1 = input("Introduce el primer apellido: ").strip()
    apellido2 = input("Introduce el segundo apellido: ").strip()
    dni = input("Introduce el DNI (8 dígitos y letra): ").strip().upper()

    if len(dni) != 9 or not dni[:-1].isdigit() or not dni[-1].isalpha():
        print("Error: El DNI no es válido.")
        return

    nombre_usuario = generauser(nombre, apellido1, apellido2, dni)

    try:
        with open("usuarios.csv", "a", newline='', encoding='utf-8') as archivo:
            writer = csv.writer(archivo, delimiter=':')
            writer.writerow([nombre, apellido1, apellido2, dni, nombre_usuario])
        print(f"Usuario {nombre_usuario} dado de alta correctamente.")
    except IOError as e:
        print(f"Error al escribir en el archivo: {e}")

def dar_baja_usuario():
    nombre_usuario = input("Introduce el nombre de usuario a dar de baja: ").strip().lower()
    encontrado = False
    usuarios = []

    try:
        with open("usuarios.csv", "r", newline='', encoding='utf-8') as archivo:
            reader = csv.reader(archivo, delimiter=':')
            header = next(reader)  # Leer la cabecera
            usuarios.append(header)  # Mantener la cabecera
            for linea in reader:
                if linea[4].lower() != nombre_usuario:
                    usuarios.append(linea)
                else:
                    encontrado = True
        
        if encontrado:
            with open("usuarios.csv", "w", newline='', encoding='utf-8') as archivo:
                writer = csv.writer(archivo, delimiter=':')
                writer.writerows(usuarios)
            print(f"Usuario {nombre_usuario} dado de baja correctamente.")
        else:
            print("Usuario no encontrado.")
    except FileNotFoundError:
        print("El archivo de usuarios no existe.")
    except IOError as e:
        print(f"Error al leer o escribir en el archivo: {e}")

def mostrar_usuarios():
    try:
        with open("usuarios.csv", "r", newline='', encoding='utf-8') as archivo:
            reader = csv.reader(archivo, delimiter=':')
            for linea in reader:
                print(":".join(linea))
    except FileNotFoundError:
        print("El archivo de usuarios no existe.")
    except IOError as e:
        print(f"Error al leer el archivo: {e}")

def mostrar_log_sistema():
    print("Mostrando log del sistema (simulado)...")
    # Aquí se podría implementar la lógica de lectura de un archivo de log real

if __name__ == "__main__":
    verifica_archivo()
    while True:
        menu()
        opcion = input("Selecciona una opción (1-6): ").strip()

        if opcion == "1":
            ejecutar_copia_seguridad()
        elif opcion == "2":
            dar_alta_usuario()
        elif opcion == "3":
            dar_baja_usuario()
        elif opcion == "4":
            mostrar_usuarios()
        elif opcion == "5":
            mostrar_log_sistema()
        elif opcion == "6":
            print("Saliendo del programa...")
            break
        else:
            print("Opción no válida. Por favor, selecciona un número del 1 al 6.")
````
