# TPC3
## Autor
Catarina Pereira Costa, A111924, (![foto](foto.jpg))
## Resumo
Desenvolvimento de uma aplicação que cria e lê listas e de seguida faz operações a essas listas.
## Resultados
* Res1:
import random

def menu(): #menu
    print("""
    Menu:
    (1) Criar Lista 
    (2) Ler Lista
    (3) Soma
    (4) Média
    (5) Maior
    (6) Menor
    (7) estaOrdenada por ordem crescente
    (8) estaOrdenada por ordem decrescente
    (9) Procura um elemento
    (0) Sair
    """)
    return

def criar_lista_aleatória(N): #menu 1
    res = []
    i = 0
    while i < N:
        nums_aleatório = random.randint(1, 100)
        res.append(nums_aleatório)
        i = i + 1
    return res

def ler_lista(N): #menu 2
    res = []
    i = 1
    while i <= N:
        nums_pedidos = int(input(f"Escolha o {i}º número: "))
        res.append(nums_pedidos)
        i = i + 1
    return res

def somar_lista(lista): #menu 3
    res = 0
    for num in lista:
        res = num + res
    return res

def media_lista(lista): #menu 4
    res = 0
    for num in lista:
        res = num + res
    return res / len(lista)

def maior_lista(lista): #menu 5
    res = lista[0]
    for num in lista[1:]:
        if num > res:
            res = num
    return res

def menor_lista(lista): #menu 6
    res = lista[0] 
    for num in lista[1:]:
        if num < res:
            res = num
    return res

def estar_ordenada_crescente(lista): #menu 7
    cond1 = "SIM"
    i = 0
    while i < len(lista) - 1 and cond1:
        if lista[i] > lista[i + 1]:
            cond1 = "NÃO"
        i = i + 1
        return cond1
    
def estar_ordenada_decrescente(lista): #menu 8
    cond2 = "SIM"
    i = 0
    while i < len(lista) - 1 and cond2:
        if lista[i] < lista[i + 1]:
            cond2 = "NÃO"
        i = i + 1
        return cond2
    
def procurar_elemento(lista, elem): #menu 9
    i = 0
    cond3 = False
    while i < len(lista) and cond3 == False:
        if lista[i] == elem:
           cond3 = True
        i = i + 1
    if cond3 == False:
        return "-1"
    else:
        return i - 1


lista_no_momento = []
cond4 = True
while cond4 == True: #aplicação
    menu()
    n_menu = int(input("Escolha um número entre 0 e 9, consoante o menu: "))
    if n_menu == 1:
        N = int(input("Quantos elementos quer ter na lista: "))
        lista_no_momento = criar_lista_aleatória(N)
        print(lista_no_momento)
    elif n_menu == 2:
        N = int(input("Quantos elementos quer ter na lista: "))
        lista_no_momento = ler_lista(N)
        print(lista_no_momento)
    elif 3 <= n_menu <= 9:
        if lista_no_momento == []:
            print("A lista está vazia! Deve selecionar inicialmente a opção 1 ou 2 para obter uma lista!") #necessário uma lista para as seguintes operações
        else:
            if n_menu == 3:
                print(somar_lista(lista_no_momento))
            elif n_menu == 4:
                print(media_lista(lista_no_momento))
            elif n_menu == 5:
                print(maior_lista(lista_no_momento))
            elif n_menu == 6:
                print(menor_lista(lista_no_momento))
            elif n_menu == 7:
                print(estar_ordenada_crescente(lista_no_momento))
            elif n_menu == 8:
                print(estar_ordenada_decrescente(lista_no_momento))
            elif n_menu == 9:
                n_procurar = int(input("Que número quer pocurar na lista? "))
                print(procurar_elemento(lista_no_momento, n_procurar))

    elif n_menu == 0:
        print(f"Saiu da aplicação! A última lista guardada é {lista_no_momento}.") #fim do programa

        cond4 = False

    else:
        print("Opção inválida! Escolha um número que corresponda a uma operação do menu (0-9): ") #números fora do intervalo pedido