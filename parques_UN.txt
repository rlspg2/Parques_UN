import random #importe la biblioteca random
# definimos una funcion para seleccionar el modo de juego 
def seleccionar_modo_juego():
    print("Selecciona el modo de juego:")
    print("1. Modo Real")
    print("2. Modo Desarrollador")# Muestramostramos las opciones de modo de juego disponibles
    while True: # un bucle para seleccionar el modo de juego
        try:
            #Se solicita al usuario que ingrese un número para seleccionar el modo
            modo = int(input("Ingresa el número del modo que deseas jugar (1 o 2): "))
            # Verifica si el número ingresado es 1 o 2
            if modo in [1, 2]:
                # Retorna el modo seleccionado si es válido
                return modo
            else:
                # Mensaje de error si el número no es 1 ni 2
                print("Opción inválida. Por favor, ingresa 1 o 2.")
        except ValueError:
            # Maneja el error si el usuario ingresa algo que no es un número
            print("Entrada inválida. Por favor, ingresa un número.")
# Definimos el tablero como una lista de listas una matriz para poder usar coordenadas para las casillas
tablero = [
    ["*****", "*****", "*****", "*****", "*****", "*****", "*****", "____|", "_S__|", "____|", "*****", "*****", "*****", "*****", "*****", "*****", "*****"],
    ["*****", "*****", "*****", "*****", "*****", "*****", "*****", "____|", "____|", "____|", "*****", "*****", "*****", "*****", "*****", "*****", "*****"],
    ["*****", "*****", "*****", "*****", "*****", "*****", "*****", "____|", "____|", "____|", "*****", "*****", "*****", "*****", "*****", "*****", "*****"],
    ["*****", "*****", "*****", "*****", "*****", "*****", "*****", "____|", "____|", "____|", "*****", "*****", "*****", "*****", "*****", "*****", "*****"],
    ["*****", "*****", "*****", "*****", "*****", "*****", "*****", "_O__|", "____|", "__S_|", "*****", "*****", "*****", "*****", "*****", "*****", "*****"],
    ["*****", "*****", "*****", "*****", "*****", "*****", "*****", "____|", "____|", "____|", "*****", "*****", "*****", "*****", "*****", "*****", "*****"],
    ["*****", "*****", "*****", "*****", "*****", "*****", "*****", "____|", "____|", "____|", "*****", "*****", "*****", "*****", "*****", "*****", "*****"],
    ["  D |", "*****", "*****", "*****", "*****", "*****", "*****", "____|", "____|", "____|", "*****", "*****", "*****", "*****", "*****", "*****", "  C |"],
    ["____|", "____|", "____|", "____|", "_S__|", "____|", "____|", "____|", "____|", "____|", "____|", "____|", "_O__|", "____|", "____|", "____|", "____|"],
    ["_S__|", "____|", "____|", "____|", "____|", "____|", "____|", "____|", "Meta ", "____|", "____|", "____|", "____|", "____|", "____|", "____|", "_S__|"],
    ["____|", "____|", "____|", "____|", "_O__|", "____|", "____|", "____|", "____|", "____|", "____|", "____|", "_S__|", "____|", "____|", "____|", "____|"],
    ["  A |", "*****", "*****", "*****", "*****", "*****", "*****", "____|", "____|", "____|", "*****", "*****", "*****", "*****", "*****", "*****", "*****"],
    ["*****", "*****", "*****", "*****", "*****", "*****", "*****", "____|", "____|", "____|", "*****", "*****", "*****", "*****", "*****", "*****", "  B |"],
    ["*****", "*****", "*****", "*****", "*****", "*****", "*****", "____|", "____|", "____|", "*****", "*****", "*****", "*****", "*****", "*****", "*****"],
    ["*****", "*****", "*****", "*****", "*****", "*****", "*****", "_S__|", "____|", "_O__|", "*****", "*****", "*****", "*****", "*****", "*****", "*****"],
    ["*****", "*****", "*****", "*****", "*****", "*****", "*****", "____|", "____|", "____|", "*****", "*****", "*****", "*****", "*****", "*****", "*****"],
    ["*****", "*****", "*****", "*****", "*****", "*****", "*****", "____|", "____|", "____|", "*****", "*****", "*****", "*****", "*****", "*****", "*****"],
    ["*****", "*****", "*****", "*****", "*****", "*****", "*****", "____|", "____|", "____|", "*****", "*****", "*****", "*****", "*****", "*****", "*****"],
    ["*****", "*****", "*****", "*****", "*****", "*****", "*****", "____|", "_S__|", "____|", "*****", "*****", "*****", "*****", "*****", "*****", "*****"]
]
# definimos las rutas de casillas para donde se moveran las fichas de cada equipo
ruta_equipo_A = [
    (10, 4), (10, 5), (10, 6), (10, 7), (11, 7), (12, 7), (13, 7), (14, 7), (15, 7),
    (16, 7), (17, 7), (18, 7), (18, 8), (18, 9), (17, 9), (16, 9), (15, 9), (14, 9), (13, 9),
    (12, 9), (11, 9), (10, 9), (10, 10), (10, 11), (10, 12), (10, 13), (10, 14), (10, 15), (10, 16),
    (9, 16), (8, 16), (8, 15), (8, 14), (8, 13), (8, 12), (8, 11), (8, 10), (8, 9), (7, 9),
    (7, 9), (6, 9), (5, 9), (4, 9), (3, 9), (2, 9), (1, 9), (0, 9), (0, 8),
    (0, 7), (1, 7), (2, 7), (3, 7), (4, 7), (5, 7), (6, 7), (7, 7), (8, 7),
    (8, 6), (8, 5), (8, 4), (8, 3), (8, 2), (8, 1), (8, 0), (9, 0), (9, 1),
    (9, 2), (9, 3), (9, 4), (9, 5), (9, 6), (9, 7), (9, 8)
]

ruta_equipo_B = [
    (14, 9), (13, 9), (12, 9), (11, 9), (10, 9), (10, 10), (10, 11),
    (10, 12), (10, 13), (10, 14), (10, 15), (10, 16), (9, 16), (8, 16), (8, 15),
    (8, 14), (8, 13), (8, 12), (8, 11), (8, 10), (8, 9), (7, 9), (7, 9), (6, 9),
    (5, 9), (4, 9), (3, 9), (2, 9), (1, 9), (0, 9), (0, 8), (0, 7), (1, 7),
    (2, 7), (3, 7), (4, 7), (5, 7), (6, 7), (7, 7), (8, 7), (8, 6), (8, 5),
    (8, 4), (8, 3), (8, 2), (8, 1), (8, 0), (9, 0), (10, 0), (10, 1), (10, 2),
    (10, 3), (10, 4), (10, 5), (10, 6), (10, 7), (11, 7), (12, 7), (13, 7), (14, 7),
    (15, 7), (16, 7), (17, 7), (18, 7), (18, 8), (17, 8), (16, 8), (15, 8), (14, 8),
    (13, 8), (12, 8), (11, 8), (10, 8), (9, 8)
]

ruta_equipo_C = [
    (8, 12), (8, 11), (8, 10), (8, 9), (7, 9), (6, 9), (5, 9), (4, 9), (3, 9), (2, 9),
    (1, 9), (0, 9), (0, 8), (0, 8), (0, 7), (1, 7), (2, 7), (3, 7), (4, 7), (5, 7),
    (6, 7), (7, 7), (8, 7), (8, 6), (8, 5), (8, 4), (8, 3), (8, 2), (8, 1), (8, 0), (9, 0),
    (10, 0), (10, 1), (10, 2), (10, 3), (10, 4), (10, 5), (10, 6), (10, 7), (11, 7), (12, 7),
    (13, 7), (14, 7), (15, 7), (16, 7), (17, 7), (18, 7), (18, 8), (18, 9), (17, 9), (16, 9),
    (15, 9), (14, 9), (13, 9), (12, 9), (11, 9), (10, 9), (10, 10), (10, 11), (10, 12), (10, 13),
    (10, 14), (10, 15), (10, 16), (9, 16), (9, 15), (9, 14), (9, 13), (9, 12), (9, 11), (9, 10),
    (9, 9), (9, 8)
]

ruta_equipo_D = [
    (4, 7), (5, 7), (6, 7), (7, 7), (8, 7), (8, 6), (8, 5), (8, 4), (8, 3), (8, 2), (8, 1),
    (8, 0), (9, 0), (10, 0), (10, 1), (10, 2), (10, 3), (10, 4), (10, 5), (10, 6), (10, 7),
    (11, 7), (12, 7), (13, 7), (14, 7), (15, 7), (16, 7), (17, 7), (18, 7), (18, 8), (18, 9),
    (17, 9), (16, 9), (15, 9), (14, 9), (13, 9), (12, 9), (11, 9), (10, 9), (10, 10),
    (10, 11), (10, 12), (10, 13), (10, 14), (10, 15), (10, 16), (9, 16), (8, 16), (8, 15),
    (8, 14), (8, 13), (8, 12), (8, 11), (8, 10), (8, 9), (7, 9), (6, 9), (5, 9), (4, 9),
    (3, 9), (2, 9), (1, 9), (0, 9), (0, 8), (1, 8), (2, 8), (3, 8), (4, 8), (5, 8), (6, 8),
    (7, 8), (8, 8), (9, 8)
]

# Inicializamos las fichas de cada equipo en la cárcel
def inicializar_fichas():
    # Equipo A = A_1, A_2, A_3, A_4
    tablero[11][0] = "A_1 |"
    tablero[11][1] = "A_2 |"
    tablero[11][2] = "A_3 |"
    tablero[11][3] = "A_4 |"

    # Equipo B = B_1, B_2, B_3, B_4
    tablero[12][13] = "B_1 |"
    tablero[12][14] = "B_2 |"
    tablero[12][15] = "B_3 |"
    tablero[12][16] = "B_4 |"

    # Equipo C = C_1, C_2, C_3, C_4
    tablero[7][13] = "C_1 |"
    tablero[7][14] = "C_2 |"
    tablero[7][15] = "C_3 |"
    tablero[7][16] = "C_4 |"

    # Equipo D = D_1, D_2, D_3, D_4
    tablero[7][0] = "D_1 |"
    tablero[7][1] = "D_2 |"
    tablero[7][2] = "D_3 |"
    tablero[7][3] = "D_4 |"

# esta funcion es para mostrar el tablero
def mostrar_tablero():
    for fila in tablero: #itera sobre las filas de el tablero
        print(" ".join(fila)) #imprime las filas
#Diccionario para guardar los mobvimientos adicionales
movimientos_adicionales = {"A": 0, "B": 0, "C": 0, "D": 0}
#Diccionario para contar los pares consecutivos para cada equipo
pares_consecutivos = {"A": 0, "B": 0, "C": 0, "D": 0}

#diccionario para guardar la ultima ficha movida por cada equipo
ultima_ficha_movida = {"A": None, "B": None, "C": None, "D": None}

# Función para lanzar los dados
def lanzar_dados(modo):
    """
    Lanza los dados según el modo de juego seleccionado.
    - Modo 1 (Real): Lanza dados aleatorios.
    - Modo 2 (Desarrollador): Permite elegir entre lanzar dados aleatorios o ingresar valores manualmente.
    """
    if modo == 1:  # condicional por si el modo es real
        dado1 = random.randint(1, 6)
        dado2 = random.randint(1, 6)
        print(f"Resultado de los dados: {dado1}, {dado2}")
        return dado1, dado2 #muestra el resultado de los dados ya que son automaticos

    elif modo == 2:  # el elif por si se elige el modo desarrollador 
        print("Modo Desarrollador: ¿Deseas lanzar los dados o ingresar valores manualmente?")
        print("1. Lanzar dados aleatorios")
        print("2. Ingresar valores manualmente")
        #pregunta si va a lanzar los dados o pone los valores
        while True:
            try:
                opcion = int(input("Elige una opción (1 o 2): "))
                #este bucle es por si eligen algo que no sea 1 o 2 
                if opcion == 1:  # si elige lanzar los dados aleatorios
                    dado1 = random.randint(1, 6)
                    dado2 = random.randint(1, 6)
                    print(f"Resultado de los dados: {dado1}, {dado2}") #imprime los resultados de los dados
                    return dado1, dado2 

                elif opcion == 2:  #si se elige escoger el numero de los daods
                    while True:
                        try: #bucle para que si elige numeros distintos que del 1 al 6 o letras toque repetir
                            dado1 = int(input("Ingresa el valor del primer dado (1-6): "))
                            dado2 = int(input("Ingresa el valor del segundo dado (1-6): "))
                            if 1 <= dado1 <= 6 and 1 <= dado2 <= 6:
                                print(f"Valores ingresados: {dado1}, {dado2}")
                                return dado1, dado2
                            else:
                                print("Los valores deben estar entre 1 y 6. Inténtalo de nuevo.")
                        except ValueError:
                            print("Entrada inválida. Por favor, ingresa números.")

                else:
                    print("Opción inválida. Por favor, ingresa 1 o 2.")

            except ValueError: #estos son para por si no se eligio una opcion de lanzar dados y se puso un numero invalido o letra
                print("Entrada inválida. Por favor, ingresa un número.")

# Función para sacar una ficha de la cárcel con el max_fichas para que si saca un 5 solo pueda sacar una ficha 
def sacar_ficha(equipo, max_fichas=1):
    """
    Saca una o más fichas de la cárcel (salida) y las mueve a la casilla de inicio del equipo.
    :param equipo: Equipo cuyas fichas se sacan ("A", "B", "C", "D").
    :param max_fichas: Número máximo de fichas que se pueden sacar (por defecto, 1).
    :return: True si se logró sacar al menos una ficha, False en caso contrario.
    """
    if equipo == "A": #definios en este caso usamos las casillas salida para dednotar las casillas de carcel y las de inicio para donde inicia cada ficha luego de salir da la carcel
        casillas_salida = [(11, 0), (11, 1), (11, 2), (11, 3)] #y las de inicio para donde inicia cada ficha luego de salir da la carcel
        casilla_inicio = (10, 4)
    elif equipo == "B":
        casillas_salida = [(12, 13), (12, 14), (12, 15), (12, 16)]
        casilla_inicio = (14, 9)
    elif equipo == "C":
        casillas_salida = [(7, 13), (7, 14), (7, 15), (7, 16)]
        casilla_inicio = (8, 12)
    elif equipo == "D":
        casillas_salida = [(7, 0), (7, 1), (7, 2), (7, 3)]
        casilla_inicio = (4, 7)
    #sacamos la fila y la columna de la casilla de inicio
    fila_inicio, columna_inicio = casilla_inicio
    casilla_actual = tablero[fila_inicio][columna_inicio].strip()#obtenemos el contenido actual de la casilla inicio con strip para quitar espacio o ago que pueda interferir

    fichas_en_carcel = [] #lista para almacenar las fichas en la carcel
    for fila, columna in casillas_salida: #recorremos las fichas para encontrar las que estan en la carcel
        casilla_carcel = tablero[fila][columna].strip()
        if casilla_carcel.startswith(f"{equipo}_") and casilla_carcel.endswith("|"):
            fichas_en_carcel.append((fila, columna, casilla_carcel)) #verificamos si estan hay fichas en la carcel

    if not fichas_en_carcel:
        print("No hay fichas en la cárcel para sacar.") #por si no hay fichas en la carcel enviamos este mensaje
        return False

    fila, columna, ficha_seleccionada = fichas_en_carcel[0]#seleccionamos la primera ficha en la carcel para moverla
    #verificamos si la casilla de inicio esta ocupada o es una casilla especial
    if casilla_actual == "____|" or casilla_actual.startswith(('_S__|', '_O__|')):
        tablero[fila_inicio][columna_inicio] = ficha_seleccionada #movemos la ficha a la casilla de inicio
    elif casilla_actual.startswith(f"{equipo}_"):
        tablero[fila_inicio][columna_inicio] = f"{equipo}_BLOQUEO|" #si la casilla esta ocupada marca un bloqueo
    else:
        print(f"No se puede sacar la ficha: la casilla de inicio está ocupada por {casilla_actual}.")
        return False

    tablero[fila][columna] = "____|"
    print(f"Ficha {ficha_seleccionada} sacada y movida a la casilla de inicio.")
    return True

# Función para verificar si una ficha especifica está en la cárcel
def es_ficha_en_carcel(equipo, ficha):
    """
    Verifica si una ficha específica de un equipo está en la cárcel.
    :param equipo: Equipo al que pertenece la ficha ("A", "B", "C", "D").
    :param ficha: Número de la ficha (1, 2, 3, 4).
    :return: True si la ficha está en la cárcel, False en caso contrario.
    """
    # Validamos que el equipo sea válido
    equipos_validos = ["A", "B", "C", "D"]
    if equipo not in equipos_validos:
        print(f"Error: El equipo '{equipo}' no es válido.")
        return False #error por si no es un equipo valido de los 4 que tenemos 

    # Validamos que la ficha sea válida
    fichas_validas = ["1", "2", "3", "4"]
    if ficha not in fichas_validas:
        print(f"Error: La ficha '{ficha}' no es válida.")
        return False #validar que la ficha exista y sea una de las 4 de cada equipo

    # Definimos las casillas de cárcel para cada equipo
    if equipo == "A":
        casillas_salida = [(11, 0), (11, 1), (11, 2), (11, 3)]
    elif equipo == "B":
        casillas_salida = [(12, 13), (12, 14), (12, 15), (12, 16)]
    elif equipo == "C":
        casillas_salida = [(7, 13), (7, 14), (7, 15), (7, 16)]
    elif equipo == "D":
        casillas_salida = [(7, 0), (7, 1), (7, 2), (7, 3)]

    # Verificamos si la ficha está en una de las casillas de la carcel
    for fila, columna in casillas_salida:
        if tablero[fila][columna].strip() == f"{equipo}_{ficha}|":  # Usamos strip() para eliminar espacios adicionales
            return True #retornamos si la casilla esta en la carcel

    return False

# Define las casillas especiales (seguros y inicios)
casillas_especiales = {
    "seguros": [
        (9, 0),   # Seguro cerca de la salida del equipo A
        (14, 7),  # Seguro en el camino del equipo B
        (18, 8),  # Seguro cerca de la meta
        (10, 12), # Seguro en el camino del equipo C
        (9, 16),  # Seguro cerca de la salida del equipo D
        (4, 9),   # Seguro en el camino del equipo A
        (0, 8),   # Seguro cerca de la meta
        (8, 4)    # Seguro en el camino del equipo D
    ],
    "salidas": [
        (10, 4),  # inicio del equipo A
        (14, 9),  # inicio del equipo B
        (9, 13),  # inicio del equipo C
        (4, 7)    # inicio del equipo D
    ]
}

# Función para validar que las casillas especiales estén dentro del tablero
def validar_casillas_especiales(tablero, casillas_especiales):
    """
    Verifica que todas las casillas especiales estén dentro de los límites del tablero.
    :param tablero: El tablero del juego (matriz).
    :param casillas_especiales: Diccionario con las casillas especiales.
    :return: True si todas las casillas son válidas, False en caso contrario.
    """
    filas = len(tablero)
    columnas = len(tablero[0]) if filas > 0 else 0 #contar el numero de filas y columnas del tablero

    for tipo, casillas in casillas_especiales.items():
        for fila, columna in casillas:
            if fila >= filas or columna >= columnas: #recorremos las casillas especiales y vemos si estan en los limites del tablero
                print(f"Error: Casilla especial ({fila}, {columna}) fuera de los límites del tablero.")
                return False
    print("Todas las casillas especiales son válidas.")
    return True

# Marcar las casillas especiales en el tablero para facilitar la visualización
def marcar_casillas_especiales(tablero, casillas_especiales):
    """
    Marca las casillas especiales en el tablero con símbolos específicos.
    :param tablero: El tablero del juego (matriz).
    :param casillas_especiales: Diccionario con las casillas especiales.
    """
    for fila, columna in casillas_especiales["seguros"]:
        if tablero[fila][columna] == "____|":
            tablero[fila][columna] = "_S__|"  # Marca los seguros con "_S__|"

    for fila, columna in casillas_especiales["salidas"]:
        if tablero[fila][columna] == "____|":
            tablero[fila][columna] = "_O__|"  # Marca las salidas con "_O__|"

# Llamamos a las funciones para validar y marcar las casillas especiales
validar_casillas_especiales(tablero, casillas_especiales)
marcar_casillas_especiales(tablero, casillas_especiales)
#definimos la funcion que nos ayudra a enviar a la carcel a las fichas
def enviar_a_carcel(equipo, ficha_capturada):
    """
    Envía una ficha capturada de vuelta a su posición en la cárcel.
    :param equipo: Equipo al que pertenece la ficha ("A", "B", "C", "D").
    :param ficha_capturada: Ficha que será enviada a la cárcel (ejemplo: "B_1 |").
    """
    # Definimos las casillas de cárcel para cada equipo
    if equipo == "A":
        casillas_salida = [(11, 0), (11, 1), (11, 2), (11, 3)]
    elif equipo == "B":
        casillas_salida = [(12, 13), (12, 14), (12, 15), (12, 16)]
    elif equipo == "C":
        casillas_salida = [(7, 13), (7, 14), (7, 15), (7, 16)]
    elif equipo == "D":
        casillas_salida = [(7, 0), (7, 1), (7, 2), (7, 3)]

    # Buscamos una casilla vacía en la cárcel del equipo
    for fila, columna in casillas_salida:
        if tablero[fila][columna] == "____|":  # Casilla vacía
            # Movemos la ficha capturada a la cárcel
            tablero[fila][columna] = ficha_capturada
            print(f"Ficha {ficha_capturada} enviada a la cárcel en la posición ({fila}, {columna}).")
            return

    # Si no hay casillas vacías en la cárcel, mostramos un mensaje de error
    print(f"Error: No hay espacio disponible en la cárcel para la ficha {ficha_capturada}.")


# Función para capturar una ficha
def capturar_ficha(equipo_capturador, ficha_capturada):
    """
    Captura una ficha enemiga y la envía a su cárcel.
    :param equipo_capturador: Equipo que realiza la captura ("A", "B", "C", "D").
    :param ficha_capturada: Ficha que será capturada (ejemplo: "B_1 |").
    """
    # Extraemos el equipo de la ficha capturada
    equipo_capturado = ficha_capturada.split("_")[0]

    # Validamos que la ficha capturada pertenezca a otro equipo
    if equipo_capturado == equipo_capturador:
        print("Error: No puedes capturar una ficha de tu propio equipo.")
        return

    # Buscamos la ficha capturada en el tablero
    ficha_encontrada = False
    for fila in range(len(tablero)):
        for columna in range(len(tablero[fila])):
            if tablero[fila][columna] == ficha_capturada:
                ficha_encontrada = True
                break
        if ficha_encontrada:
            break

    # Si la ficha no está en el tablero, mostramos un mensaje de error
    if not ficha_encontrada:
        print(f"Error: La ficha {ficha_capturada} no se encontró en el tablero.")
        return

    # Enviamos la ficha capturada a su cárcel
    enviar_a_carcel(equipo_capturado, ficha_capturada)
    print(f"Ficha {ficha_capturada} capturada y enviada a la cárcel.")

    # Asignamos 20 movimientos adicionales al equipo capturador
    movimientos_adicionales[equipo_capturador] += 20
    print(f"El equipo {equipo_capturador} obtiene 20 movimientos adicionales.")

# Función para manejar la llegada a la meta
def llegar_a_meta(equipo):
    """
    Maneja la llegada de una ficha a la meta.
    :param equipo: Equipo cuya ficha llegó a la meta ("A", "B", "C", "D").
    """
    # Validamos que el equipo exista en el diccionario de movimientos adicionales
    if equipo not in movimientos_adicionales:
        print(f"Error: El equipo {equipo} no está registrado en el sistema.")
        return

    # Asignamos 10 movimientos adicionales al equipo
    movimientos_adicionales[equipo] += 10
    print(f"El equipo {equipo} obtiene 10 movimientos adicionales.")

    # Verificamos si el equipo ha ganado el juego
    if verificar_victoria(equipo):
        print(f"¡El equipo {equipo} ha ganado el juego!")
#definimos la funcion de mover fichas con las reglas propuestas
def mover_ficha(equipo, ficha, movimientos):
    """
    Mueve una ficha en el tablero según los movimientos dados.
    :param equipo: Equipo al que pertenece la ficha ("A", "B", "C", "D").
    :param ficha: Número de la ficha (1, 2, 3, 4).
    :param movimientos: Número de casillas que la ficha debe moverse.
    :return: True si el movimiento fue exitoso, False en caso contrario.
    """
    # Buscamos la posición actual de la ficha
    posicion_actual = None
    for fila in range(len(tablero)):
        for columna in range(len(tablero[fila])):
            if tablero[fila][columna] == f"{equipo}_{ficha} |":
                posicion_actual = (fila, columna)
                break
        if posicion_actual: 
            break
    if posicion_actual is None: #si no se encuentra la ficha retornamos false
        print(f"Error: La ficha {equipo}_{ficha} no se encontró en el tablero.")
        return False

    # Determinamos la ruta del equipo segun la ficha
    rutas = {
        "A": ruta_equipo_A,
        "B": ruta_equipo_B,
        "C": ruta_equipo_C,
        "D": ruta_equipo_D
    }
    ruta = rutas.get(equipo)

    # Calculamos el índice actual en la ruta
    try:
        indice_actual = ruta.index(posicion_actual)
    except ValueError:
        print(f"Error: La ficha {equipo}_{ficha} no está en su ruta.")
        return False

    # Calculamos la nueva posición en la ruta
    nuevo_indice = indice_actual + movimientos

    # Verificamos si la ficha llega a la meta
    if nuevo_indice >= len(ruta):
        distancia_a_meta = len(ruta) - indice_actual - 1
        if movimientos != distancia_a_meta:
            print(f"No se puede mover la ficha: se necesita un número exacto de movimientos ({distancia_a_meta}) para llegar a la meta.")
            return False #imprimimos mensaje por si no se puede mover

        # Movemos la ficha a la meta
        tablero[posicion_actual[0]][posicion_actual[1]] = "____|"
        tablero[9][8] = f"{equipo}_{ficha} |"
        print(f"Ficha {equipo}_{ficha} ha llegado exactamente a la meta.")
        return True #por si llega a la meta en ese tiro exacto

    # Obtenemos la nueva posición
    nueva_fila, nueva_columna = ruta[nuevo_indice]

    # Verificamos si la casilla de destino es válida
    casilla_destino = tablero[nueva_fila][nueva_columna]
    if casilla_destino.startswith("____|") or casilla_destino.startswith(("_S__|", "_O__|")):
        # Permitimos mover a la casilla si es especial o está vacía
        tablero[posicion_actual[0]][posicion_actual[1]] = "____|"
        tablero[nueva_fila][nueva_columna] = f"{equipo}_{ficha} |"
        print(f"Ficha {equipo}_{ficha} movida {movimientos} casillas.")
        return True

    # Si hay una ficha del mismo equipo, formamos un bloqueo
    if casilla_destino.startswith(f"{equipo}_"):
        tablero[nueva_fila][nueva_columna] = f"{equipo}_BLOQUEO |"
        tablero[posicion_actual[0]][posicion_actual[1]] = "____|"
        print("Formando un bloqueo con otra ficha del mismo equipo.")
        return True

    # Si hay una ficha de otro equipo, la capturamos
    ficha_capturada = tablero[nueva_fila][nueva_columna]
    equipo_capturado = ficha_capturada.split("_")[0]
    capturar_ficha(equipo, ficha_capturada)
    print(f"Ficha {ficha_capturada} capturada y enviada a la cárcel.")

    # Movemos la ficha
    tablero[posicion_actual[0]][posicion_actual[1]] = "____|"
    tablero[nueva_fila][nueva_columna] = f"{equipo}_{ficha} |"
    print(f"Ficha {equipo}_{ficha} movida {movimientos} casillas.")
    return True
#con esta función buscamos fichas disponibles para mover
def buscar_fichas_disponibles(equipo):
    """
    Busca todas las fichas disponibles para mover de un equipo.
    Solo considera fichas que están en la ruta del equipo, excluyendo las que están en la cárcel.
    :param equipo: Equipo cuyas fichas se buscan ("A", "B", "C", "D").
    :return: Lista de fichas disponibles para mover.
    """
    # Validamos que el equipo sea válido
    equipos_validos = ["A", "B", "C", "D"]
    if equipo not in equipos_validos:
        print(f"Error: El equipo '{equipo}' no es válido.")
        return []

    # Definimos la ruta del equipo
    rutas = {
        "A": ruta_equipo_A,
        "B": ruta_equipo_B,
        "C": ruta_equipo_C,
        "D": ruta_equipo_D
    }
    ruta = rutas.get(equipo, [])

    fichas_disponibles = []

    # Recorremos la ruta del equipo para buscar fichas
    for fila, columna in ruta:
        casilla = tablero[fila][columna]

        # Verificamos si la casilla contiene una ficha del equipo
        if casilla.startswith(f"{equipo}_") and casilla.endswith("|"):
            # Extraemos el número de la ficha (ejemplo: "1", "2", etc.)
            ficha_numero = casilla.split("_")[1][0]

            # Verificamos que la ficha no esté en la cárcel
            if not es_ficha_en_carcel(equipo, ficha_numero):
                fichas_disponibles.append(casilla)

    return fichas_disponibles

# Función para verificar si una casilla es la salida del equipo
def es_casilla_salida(equipo, fila, columna):
    """
    Verifica si una casilla dada pertenece a las casillas de salida (cárcel) de un equipo.
    :param equipo: Equipo cuya casilla de salida se verifica ("A", "B", "C", "D").
    :param fila: Fila de la casilla.
    :param columna: Columna de la casilla.
    :return: True si la casilla es una salida del equipo, False en caso contrario.
    """
    # Validamos que el equipo sea válido
    equipos_validos = ["A", "B", "C", "D"]
    if equipo not in equipos_validos:
        print(f"Error: El equipo '{equipo}' no es válido.")
        return False

    # Definimos las casillas de salida (cárcel) para cada equipo
    casillas_salida = {
        "A": {(11, 0), (11, 1), (11, 2), (11, 3)},
        "B": {(12, 13), (12, 14), (12, 15), (12, 16)},
        "C": {(7, 13), (7, 14), (7, 15), (7, 16)},
        "D": {(7, 0), (7, 1), (7, 2), (7, 3)}
    }

    # Verificamos si la casilla pertenece a las salidas del equipo
    if (fila, columna) in casillas_salida.get(equipo, set()):
        return True
    return False

# Función para verificar si un movimiento es válido
def es_movimiento_valido(equipo, ficha, movimientos):
    """
    Verifica si un movimiento es válido para una ficha específica.
    :param equipo: Equipo al que pertenece la ficha ("A", "B", "C", "D").
    :param ficha: Número de la ficha (1, 2, 3, 4).
    :param movimientos: Número de casillas que la ficha debe moverse.
    :return: True si el movimiento es válido, False en caso contrario.
    """
    # Validamos que el equipo sea válido
    equipos_validos = ["A", "B", "C", "D"]
    if equipo not in equipos_validos:
        print(f"Error: El equipo '{equipo}' no es válido.")
        return False

    # Buscamos la posición actual de la ficha
    posicion_actual = None
    for fila in range(len(tablero)):
        for columna in range(len(tablero[fila])):
            if tablero[fila][columna] == f"{equipo}_{ficha} |":
                posicion_actual = (fila, columna)
                break
        if posicion_actual:
            break

    # Si no se encontró la ficha, retornamos False
    if posicion_actual is None:
        print(f"Error: La ficha {equipo}_{ficha} no se encontró en el tablero.")
        return False

    # Determinamos la ruta del equipo
    rutas = {
        "A": ruta_equipo_A,
        "B": ruta_equipo_B,
        "C": ruta_equipo_C,
        "D": ruta_equipo_D
    }
    ruta = rutas.get(equipo)

    # Calculamos el índice actual en la ruta
    try:
        indice_actual = ruta.index(posicion_actual)
    except ValueError:
        print(f"Error: La ficha {equipo}_{ficha} no está en su ruta.")
        return False

    # Calculamos la nueva posición en la ruta
    nuevo_indice = indice_actual + movimientos

    # Verificamos si la ficha llega a la meta
    if nuevo_indice >= len(ruta):
        distancia_a_meta = len(ruta) - indice_actual - 1
        if movimientos != distancia_a_meta:
            print(f"No se puede mover la ficha: se necesita un número exacto de movimientos ({distancia_a_meta}) para llegar a la meta.")
            return False

        # Movemos la ficha a la meta
        return True

    # Obtenemos la nueva posición
    nueva_fila, nueva_columna = ruta[nuevo_indice]

    # Verificamos si la casilla de destino es válida
    casilla_destino = tablero[nueva_fila][nueva_columna]
    if casilla_destino.startswith("____|") or casilla_destino.startswith("_") and casilla_destino.endswith("|"):
        return True  # Casilla vacía o especial

    # Si hay una ficha del mismo equipo, formamos un bloqueo
    if casilla_destino.startswith(f"{equipo}_"):
        return True

    # Si hay una ficha de otro equipo, verificamos si estamos en una casilla especial
    if (nueva_fila, nueva_columna) in casillas_especiales["seguros"] or (nueva_fila, nueva_columna) in casillas_especiales["salidas"]:
        return True

    print("No se puede mover la ficha: la casilla de destino está ocupada.")
    return False

# Función para verificar si hay movimientos posibles para el equipo
def hay_movimientos_posibles(equipo, movimientos):
    """
    Verifica si un equipo tiene al menos una ficha que pueda moverse un número específico de casillas.
    :param equipo: Equipo cuyas fichas se verifican ("A", "B", "C", "D").
    :param movimientos: Número de casillas que las fichas deben moverse.
    :return: True si al menos una ficha puede moverse, False en caso contrario.
    """
    # Validamos que el equipo sea válido
    equipos_validos = ["A", "B", "C", "D"]
    if equipo not in equipos_validos:
        print(f"Error: El equipo '{equipo}' no es válido.")
        return False

    # Validamos que los movimientos sean mayores que cero
    if movimientos <= 0:
        print("Error: Los movimientos deben ser mayores que cero.")
        return False

    # Buscamos todas las fichas disponibles para mover
    fichas_disponibles = buscar_fichas_disponibles(equipo)

    # Si no hay fichas disponibles, retornamos False
    if not fichas_disponibles:
        print(f"No hay fichas disponibles para mover del equipo {equipo}.")
        return False

    # Verificamos cada ficha para ver si puede moverse
    for ficha in fichas_disponibles:
        ficha_numero = ficha.split("_")[1][0]  # Extraemos el número de la ficha (ejemplo: "1", "2", etc.)
        if es_movimiento_valido(equipo, ficha_numero, movimientos):
            return True  # Si al menos una ficha puede moverse, retornamos True

    # Si ninguna ficha puede moverse, retornamos False
    print(f"Ninguna ficha del equipo {equipo} puede moverse con {movimientos} movimientos.")
    return False
#con esta funcion verificamos las victorias si cumplen ciertas condiciones
def verificar_victoria(equipo):
    """
    Verifica si un equipo ha ganado el juego.
    :param equipo: Equipo cuya victoria se verifica ("A", "B", "C", "D").
    :return: True si el equipo ha ganado, False en caso contrario.
    """
    # Validamos que el equipo sea válido
    equipos_validos = ["A", "B", "C", "D"]
    if equipo not in equipos_validos:
        print(f"Error: El equipo '{equipo}' no es válido.")
        return False

    # Definimos la casilla de meta
    casilla_meta = (9, 8)

    # Buscamos todas las fichas del equipo en el tablero
    fichas_encontradas = False
    for fila in range(len(tablero)):
        for columna in range(len(tablero[fila])):
            casilla = tablero[fila][columna]
            if casilla.startswith(f"{equipo}_") and casilla.endswith("|"):
                fichas_encontradas = True
                # Si encontramos una ficha fuera de la meta, el equipo no ha ganado
                if (fila, columna) != casilla_meta:
                    return False

    # Si no se encontraron fichas del equipo, retornamos False
    if not fichas_encontradas:
        print(f"No se encontraron fichas del equipo {equipo} en el tablero.")
        return False

    # Si todas las fichas están en la meta, el equipo ha ganado
    return True
#con esta funcion solicitamos fichas para mover una en especifico
def solicitar_ficha(equipo):
    """
    Permite al jugador seleccionar una ficha disponible para mover.
    :param equipo: Equipo cuya ficha se desea mover ("A", "B", "C", "D").
    :return: Número de la ficha seleccionada (como string), o None si no hay fichas disponibles.
    """
    print(f"Fichas disponibles para mover del equipo {equipo}:")

    # Buscamos las fichas disponibles para mover
    fichas_disponibles = buscar_fichas_disponibles(equipo)

    # Si no hay fichas disponibles, mostramos un mensaje y retornamos None
    if not fichas_disponibles:
        print("No hay fichas disponibles para mover.")
        return None

    # Mostramos las fichas disponibles con opciones numeradas
    for i, ficha in enumerate(fichas_disponibles, start=1):
        ficha_numero = ficha.split("_")[1][0]  # Extraemos el número de la ficha (ejemplo: "1", "2", etc.)
        print(f"{i}. Ficha {ficha_numero}")

    # Solicitamos al jugador que elija una ficha
    while True:
        try:
            opcion = int(input("Elige el número de la ficha que deseas mover: "))
            if 1 <= opcion <= len(fichas_disponibles):
                # Extraemos el número de la ficha seleccionada
                ficha_seleccionada = fichas_disponibles[opcion - 1].split("_")[1][0]
                print(f"Has seleccionado la ficha {ficha_seleccionada}.")
                return ficha_seleccionada
            else:
                print("Opción inválida. Por favor, elige un número dentro del rango.")
        except ValueError:
            print("Entrada inválida. Por favor, ingresa un número.")

# Función para jugar un turno (ahora con soporte para ambos modos)
def jugar_turno(equipo_actual, modo):
    """
    Maneja el flujo completo de un turno para un equipo específico.
    :param equipo_actual: Equipo cuyo turno se juega ("A", "B", "C", "D").
    :param modo: Modo de juego seleccionado (1: Real, 2: Desarrollador).
    :return: True si el equipo ha ganado, False si el juego continúa.
    """
    # Validamos que el equipo sea válido
    equipos_validos = ["A", "B", "C", "D"]
    if equipo_actual not in equipos_validos:
        print(f"Error: El equipo '{equipo_actual}' no es válido.")
        return False

    print(f"Turno del equipo {equipo_actual}")

    while True:
        # Lanzamos los dados según el modo seleccionado
        dado1, dado2 = lanzar_dados(modo)
        movimientos_totales = dado1 + dado2

        # Verificamos si hay un "par de 5"
        if dado1 == 5 and dado2 == 5:
            print("¡Par de 5! El equipo puede sacar 2 fichas de la cárcel.")
            # Sacamos la primera ficha
            if not sacar_ficha(equipo_actual, max_fichas=1):
                print("No se pudo sacar la primera ficha.")
            else:
                # Sacamos la segunda ficha
                if not sacar_ficha(equipo_actual, max_fichas=1):
                    print("No se pudo sacar la segunda ficha.")
            continue  # Continuamos con el siguiente movimiento o turno

        # Verificamos si hay un 5 en los dados
        if dado1 == 5 or dado2 == 5 or dado1 + dado2 == 5:
            # Es obligatorio sacar una ficha con el 5
            if sacar_ficha(equipo_actual):
                # Si se sacó una ficha, consumimos el 5 y usamos el otro dado para mover
                if dado1 + dado2 == 5:
                    movimientos_restantes = 0
                elif dado1 == 5:
                    movimientos_restantes = dado2
                elif dado2 == 5:
                    movimientos_restantes = dado1
                else:
                    movimientos_restantes = 0

                if movimientos_restantes > 0:
                    # Solicitamos al jugador que elija qué ficha mover
                    ficha_a_mover = solicitar_ficha(equipo_actual)
                    if ficha_a_mover and mover_ficha(equipo_actual, ficha_a_mover, movimientos_restantes):
                        print(f"Ficha {equipo_actual}_{ficha_a_mover} movida {movimientos_restantes} casillas.")
                        if verificar_victoria(equipo_actual):
                            return True  # Finalizamos el juego
                    else:
                        print("No se pudo mover la ficha.")
                else:
                    print("Ya no hay movimientos restantes. Siguiente turno.")
            else:
                print("No se pudo sacar una ficha.")
        else:
            # Si no hay un 5, verificamos si hay movimientos posibles
            if not hay_movimientos_posibles(equipo_actual, movimientos_totales):
                print("No hay movimientos posibles para ninguna ficha. Turno pasa al siguiente jugador.")
            else:
                # Buscamos las fichas disponibles
                fichas_disponibles = buscar_fichas_disponibles(equipo_actual)

                # Si solo hay una ficha disponible, la movemos automáticamente
                if len(fichas_disponibles) == 1:
                    ficha_a_mover = fichas_disponibles[0].split("_")[1][0]  # Extraemos el número de la ficha
                    if mover_ficha(equipo_actual, ficha_a_mover, movimientos_totales):
                        print(f"Ficha {equipo_actual}_{ficha_a_mover} movida automáticamente {movimientos_totales} casillas.")
                        if verificar_victoria(equipo_actual):
                            return True  # Finalizamos el juego
                    else:
                        print("No se pudo mover la ficha automáticamente.")
                else:
                    # Solicitamos al jugador que elija qué ficha mover
                    ficha_a_mover = solicitar_ficha(equipo_actual)
                    if ficha_a_mover and mover_ficha(equipo_actual, ficha_a_mover, movimientos_totales):
                        print(f"Ficha {equipo_actual}_{ficha_a_mover} movida {movimientos_totales} casillas.")
                        if verificar_victoria(equipo_actual):
                            return True  # Finalizamos el juego
                    else:
                        print("No se pudo mover la ficha.")

        # Mostramos el tablero después del movimiento
        mostrar_tablero()

        # Verificamos si hay movimientos adicionales disponibles
        if movimientos_adicionales[equipo_actual] > 0:
            print(f"El equipo {equipo_actual} tiene {movimientos_adicionales[equipo_actual]} movimientos adicionales.")
            while True:
                continuar = input("¿Deseas usar un movimiento adicional? (s/n): ").lower()
                if continuar in ["s", "n"]: #damos a escoger si hacemos el movimiento adicional
                    break
                print("Entrada inválida. Por favor, ingresa 's' para sí o 'n' para no.")

            if continuar == "s":
                movimientos_adicionales[equipo_actual] -= 1
                print(f"Usando un movimiento adicional. Movimientos restantes: {movimientos_adicionales[equipo_actual]}")
                continue  # Permitimos otro movimiento
            else:
                print("No se usará un movimiento adicional. Finalizando el turno.")
                break  # Finalizamos el turno

        # Si los dados fueron iguales, repetimos el turno
        if dado1 == dado2:
            print("¡Dados iguales! El equipo obtiene un turno adicional.")
            continue  # Repetimos el turno completo

        # Si no hay más movimientos adicionales ni dados iguales, terminamos el turno
        print("Finalizando el turno del equipo.")
        break

    return False  # Continuamos el juego

# Función principal del juego para iniciarlo a jugar
def jugar():
    """
    Función principal para iniciar y gestionar el juego.
    """
    print("¡Bienvenido al juego de Parchís!")#imprimimos la biewnvenida al juego

    # Paso 1: Seleccionar el modo de juego
    modo = seleccionar_modo_juego()
    print(f"Modo de juego seleccionado: {'Real' if modo == 1 else 'Desarrollador'}")

    # Paso 2: Inicializar el tablero y las fichas
    inicializar_fichas()
    print("Tablero inicializado. Todas las fichas están en sus cárceles.")
    mostrar_tablero()

    # Paso 3: Definir el orden de los equipos
    equipos = ["A", "B", "C", "D"]
    indice_equipo_actual = 0

    # Paso 4: Bucle principal del juego
    while True:
        # Determinamos el equipo actual
        equipo_actual = equipos[indice_equipo_actual]

        # Jugamos el turno del equipo actual
        print("\n" + "=" * 50)
        print(f"Es el turno del equipo {equipo_actual}.")
        print("=" * 50 + "\n")

        # Llamamos a la función jugar_turno
        victoria = jugar_turno(equipo_actual, modo)

        # Verificamos si el equipo ha ganado
        if victoria:
            print(f"¡El equipo {equipo_actual} ha ganado el juego!")
            mostrar_tablero()
            break

        # Pasamos al siguiente equipo
        indice_equipo_actual = (indice_equipo_actual + 1) % len(equipos)

    print("Fin del juego. ¡Gracias por jugar!") #imprimimos al fina del juego

if __name__ == "__main__": # ejecutamos la función jugar() si este script es el programa principal
    jugar()