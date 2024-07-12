import os
import random
import csv
L_P="cls"
inv={}
trabajadores=["Juan Perez","Maria garcia","Carlos Lopez","Ana Martinez","Pedro Rodriguez","Laura Hernandez","Miguel Sanchez","Isabel Gomez","Francisco Diaz","Elena Fernandez"]
os.system(L_P)

def asignacion_sueldos():
    global inv
    inv={}
    for trabajador in trabajadores:
        inv[trabajador]={"sueldo":random.randint(300000,2500000)}
    print("Sueldos asignados aleatoriamente")



def clasificacion_sueldos():
    clasificacion={"Menor":[],"Mediano":[],"Mayor":[]}
    for trabajador,datos in inv.items():
        sueldo=datos["sueldo"]
        if sueldo < 800000:
            clasificacion["Menor"].append(trabajador)
        elif sueldo >=800000 or sueldo <2000000:
            clasificacion["Mediano"].append(trabajador)
        else: 
            clasificacion["Mayor"].append(trabajador)
    print("Clasificación de sueldo")
    for categoria,lista in clasificacion.items():
        print(f"{categoria}: {','.join(lista)}")
    print()


def estadisticas():
    sueldos=[datos["sueldo"] for datos in inv.values()]
    try:
        estadisticas={
            "sueldo mas alto":max(inv, key=lambda k:  inv[k]["sueldo"]),
            "sueldo mas bajo":min(inv, key=lambda k: inv[k]["sueldo"]),
            "promedio de sueldos":sum(sueldos)/ len(sueldos),
            
            }
        for clave,valor in estadisticas.items():
            print(f"{clave}: {valor}")
    except ValueError:
        print("")


def reporte_sueldos():
    guardar_csv="datos.csv"
    try:
        with open(guardar_csv, mode="w", newline="") as guardar:
            escritor=csv.writer(guardar)
            escritor.writerow(["trabajador","sueldo","descuento_afp","descuento_salud","sueldo_total"])
            for trabajador,datos in inv.items():
                sueldo=datos["sueldo"]
                descuento_afp=sueldo*0.12
                descuento_salud=sueldo*0.07
                sueldo_total=sueldo-descuento_afp-descuento_salud
                escritor.writerow([trabajador,sueldo,descuento_afp,descuento_salud,sueldo_total])
            print(f"reporte generado: {guardar}")
    except ValueError:
        print("")


def menu():
    mainmenu=1
    while mainmenu==1:
        print("\n****ANALIZADOR DE DATOS****\n1. Asignacón de sueldos aleatorios\n2. Clasificación de sueldos\n3. Ver estadísticas\n4. Reporte de sueldos\n5. Salir del programa")
        try:
            opcion=int(input("Ingrese la opción que desea ver: "))
            if opcion==1:
                asignacion_sueldos()
            elif opcion==2:
                clasificacion_sueldos()
            elif opcion==3:
                estadisticas()
            elif opcion==4:
                reporte_sueldos()
            elif opcion==5:
                print("Finalizando programa...\nDesarrollo por: Deyanira Leyton\nRut: 20.204.511-1 \n\n")
                mainmenu=0
            else:
                print("Ingrese una opcion valida.")
        except ValueError:
            print("Ingrese una opcion del 1 al 5")
menu()
