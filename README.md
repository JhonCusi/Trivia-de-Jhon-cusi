
GREEN = '\033[32m'
YELLOW = '\033[33m'
BLUE = '\033[34m'
RESET = '\033[39m'


print ("\033[32m Bienvenido a mi trivia sobre Capitales del Mundo \033[32m")
print ("\033[34m Pondremos a prueba tus conocimientos\033[39m")
nombre = input("Ingresa tu nombre: ")

import os  # Para limpiar la consola
import random  # Para dar la sensación de aleatoriedad


textoBaseDePreguntas = '''
Capital de Peru\tLima\tCallao\tArequipa\tBolibar
\n
Capital de Armenia\tEreván\tQuito\tBelmopán\tBridgetown
\n
Capital de Albania\tTirana\tCallao\tLuanda\tKabul
'''
n_pregunta = 0

base_de_preguntas = []
renglones = textoBaseDePreguntas.split("\n")
cantidadDePreguntas = len(renglones)

preguntaEscogida = []
opciones = []
pregunta = ""
respuesta = ""

for i in range(cantidadDePreguntas):
    if(renglones[i] == ""):
        continue
    base_de_preguntas.append(renglones[i].split("\t"))


def borrarConsola():
    os.system("cls" if os.name == "nt" else "clear")


def escogerPregunta(n):
    global opciones, respuesta, pregunta

    preguntaEscogida = base_de_preguntas[n]
    pregunta = preguntaEscogida[0]
    respuesta = preguntaEscogida[1]
    opciones = preguntaEscogida[1:]
    for i in range(4):
        random.shuffle(opciones)
    print(opciones)
    return preguntaEscogida


def mostrarPregunta():
    borrarConsola()
    print()
    print(pregunta)
    print("A)", opciones[0])
    print("B)", opciones[1])
    print("C)", opciones[2])
    print("D)", opciones[3])
    print()


def capturarRespuesta():
    respuestaUsuario = ""
    opcionesVálidas = ["a", "b", "c", "d"]
    while True:
        respuestaUsuario = input(" Ingrese su respuesta >").lower()
        if not (respuestaUsuario in opcionesVálidas):
            print(" La respuesta no está entre las opciones válidas, vuelva a intentarlo ")
            continue
        break
    return opcionesVálidas.index(respuestaUsuario)


def jugar():
    escogerPregunta(n_pregunta)
    mostrarPregunta()
    if(opciones[capturarRespuesta()]==respuesta):
        print("Su respuesta es correcta")
        input("ENTER PARA CONTINUAR")
    else:
        print("Su respuesta NO es correcta, la correcta es: "+ respuesta)
        input("ENTER PARA CONTINUAR")

while True:
    try:
        jugar()
    except:
        pass
    n_pregunta += 1
    if(n_pregunta==cantidadDePreguntas):
        borrarConsola()
        print("El juego ha finalizado ")
        input("ENTER PARA CONTINUAR")
        break
