# Blackjack
 Mi dirección de GitHub para este repositorio es la siguiente: [GitHub](https://github.com/alexlomu/Blackjack)
 https://github.com/alexlomu/Blackjack.
 Hemos hecho un código con el que se puede jugar al blackjack en modo un jugador (contra la banca) incluyendo las formas de las cartas y dando la posibilidad de volver a jugar al acabar una partida.
 El diagrama de flujo es el siguiente:
 ![blackjack_figma](https://user-images.githubusercontent.com/91721507/142742427-72d606c6-347f-440e-9e46-99e27cf4e58a.JPG)

El código del juego es el siguiente:
```from random import choice, sample
#Creamos una diccionario asignandole a cada carta su valor
cartas = {
    chr(0x1f0a1): 11,
    chr(0x1f0a2): 2,
    chr(0x1f0a3): 3,
    chr(0x1f0a4): 4,
    chr(0x1f0a5): 5,
    chr(0x1f0a6): 6,
    chr(0x1f0a7): 7,
    chr(0x1f0a8): 8,
    chr(0x1f0a9): 9,
    chr(0x1f0aa): 10,
    chr(0x1f0ab): 10,
    chr(0x1f0ad): 10,
    chr(0x1f0ae): 10,
}
#Creamos la función del juego
def play():
    #Mostramos las cartas y las puntuaciones de cada una
    print("Cartas: {}".format(" ".join(cartas.keys())))
    print("Puntos: {}".format(list(cartas.values())))

    print("1\ Iteración estándar sobre un diccionario")
    for carta, valor in cartas.items():
        print("la carta {} vale {}".format(carta, valor))

    print("2\ Iteración ordenada sobre un diccionario")
    for carta in sorted(cartas.keys()):
        print("la carta {} vale {}".format(carta, cartas[carta]))
    #Creamos una lista con el diccionario de cartas
    print("3\ Black Jack")
    lista_cartas = list(cartas)

    #Sacamos las dos primeras cartas del jugador, sumamos sus valores y le decimos su puntuacíon actual
    print("Ha seleccionado:", end=" ")
    carta = choice(lista_cartas)
    score = cartas[carta]
    print(carta, end=" ")
    carta = choice(lista_cartas)
    score += cartas[carta]
    print(carta, end=" ")
    print(" >>> su puntuación es de", score)

    #En el caso de que el jugador quiera pedir más cartas sólo podrá ser mientras su puntuacíon sea inferior a 21
    plantarse = False
    while score < 21 and plantarse == False:
        pedir_carta = input("¿Deseas pedir una carta? Responde si o no: ")
        pedir_carta = pedir_carta.lower()
        if pedir_carta == "si":
            carta = choice(lista_cartas)
            score += cartas[carta]
            print(carta, end=" ")
            print(" >>> su nueva puntuación es de", score)
        elif pedir_carta == "no":
            plantarse = True
        else:
            print("Introduce una respuesta válida.")
    #Le damos dos cartas a la banca y mostramos su puntuación
    main_banca = sample(lista_cartas, 2)
    score_banca = sum(cartas[carta] for carta in main_banca)
    print("La banca tiene: {} {} >> su score es {}".format(main_banca[0],
                                                            main_banca[1],
                                                            score_banca))
    #Los diferentes resultados de la partida dependiendo del score
    if score > 21:
        print("Te has pasado, gana la banca.")
    if score == score_banca:
        print("La banca y tú habéis empatado")
    if score < 21 and score < score_banca:
        print("Ha ganado la banca.")
    if score < 21 and score > score_banca:
        print("Has ganado!!")
    if score == 21 and score_banca != 21:
        print("Felicidades has hecho BLACKJACK!! Has ganado!!")
    #Preguntamos si quiere volver a jugar
    volver_jugar = input("¿Quieres volver a jugar? Responde si o no: ")
    volver_jugar = volver_jugar.lower()
    if volver_jugar == "si":
        play()
    if volver_jugar == "no":
        print("Hasta la próxima!")
#Llamamos a la función para empezar a jugar
play()
