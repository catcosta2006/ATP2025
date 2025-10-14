# TPC4
## Autor
Catarina Pereira Costa, A111924, (![foto](foto.jpg))
## Resumo
Desenvolvimento de uma aplicação que gere um cinema através de um menu com tarefas.
## Resultados
* Res1:
# TPC4 - Aplicação de gestão de um cinema

## Modelo:
# Cinema = [Sala]
# Sala = [nlugares, vendidos, filme]
# n lugares = Int
# filme = String
# vendidos = Int

Sala1 = (150, [1, 2, 3, 10, 86, 87, 142, 143],"Missão Impossível" )
Sala2 = (100, [14, 15, 16, 17, 80, 81], "Wicked")
Sala3 = (180, [1, 2, 3, 18, 19, 60, 61], "Anyone but you")
Sala4 = (150,[147, 148, 120, 121, 5, 6], "Moana 2")
Sala5 = (200,[102, 103, 45, 12, 13], "It")
cinema_no_momento = [Sala1 , Sala2, Sala3, Sala4, Sala5]

def menu():
    print("""
Menu:
(1) Listar filmes
(2) Lugares disponíveis
(3) Vender bilhete
(4) Disponibilidade
(5) Inserir nova sala
(6) Remover sala
(0) Sair
""")
    return
    
def filmes():
    print("""
FILMES EM EXIBIÇÃO:
- Missão Impossível
- Velocidade Furiosa 7
- Wicked
- Anyone but you
- Moana 2
- It
""")

def listar(cinema): # menu1
    if cinema == []:
        print("Não há filmes em exibição!")
    else:
        filmes()

def lugares_disponíveis(cinema): # menu2
    filme = input("Indique o nome do filme: ")
    encontrado = False
    for sala in cinema:
        if sala[2] == filme:
            encontrado = True
            lotação = sala[0]
            vendidos = sala[1]
            disponíveis = lotação - len(vendidos)
            print("O filme",filme,"tem", disponíveis,"lugares disponíveis.")
    if encontrado == False:
        print("Filme não encontrado!")

def vender_bilhete(cinema): # menu3
    filme = input("Deseja comprar bilhete para que filme?")
    encontrado1 = False
    for sala in cinema:
        if sala[2] == filme:
            encontrado1 = True
            vendido = False
            while vendido == False:
                lugar = int(input("Que lugar deseja?"))
                if lugar in sala[1]:
                    print("Esse lugar não está disponível! Escolha outro.")
                elif 1 > lugar or lugar > sala[0]:
                    print("Este lugar não existe! Escolha outro.")
                else:
                    sala[1].append(lugar)
                    print("Bilhete vendido com sucesso! O seu lugar é", lugar, "!")
                    vendido = True
    if encontrado1 == False:
        print("Filme não encontrado!")

def disponibilidade(cinema): # menu4
    print("Disponibilidade das salas: ")
    for sala in cinema:
        lotação = sala[0]
        vendidos = sala[1]
        disponíveis = lotação - len(vendidos)
        print(sala[2], "-", disponíveis, "lugares disponíveis de", lotação)

def inserir_sala(cinema): # menu5
    nome_filme = input("Qual o nome do novo filme?")
    existir = True
    while existir == True:
        existir = False
        for sala in cinema:
            if sala[2] == nome_filme:
                existir = True
        if existir == True:
            print("Essa sala já existe! Escolha outro filme.")
            nome_filme = input("Qual o nome do novo filme?")
    
    lotação_novo_filme = int(input("Qual a lotação da nova sala?"))
    nova_sala = (lotação_novo_filme, [], nome_filme)
    cinema.append(nova_sala)
    print("Sala adicionada com sucesso!")

def remover_sala(cinema): # menu6
    if cinema == []:
        print("Não há salas para remover!")
    else:
        print("Salas disponíveis")
        for sala in cinema:
            print("-", sala[2])
        nome_filme = input("Qual o filme que quer eliminar? ")
        encontrada = False
        while encontrada == False:
            for sala in cinema:
                if nome_filme == sala[2]:
                    cinema.remove(sala)
                    print("Sala de", nome_filme, "eliminada com sucesso!")
                    encontrada = True
            if encontrada == False:
                print("Essa sala não existe para poder ser removida! Escolhe outro filme que esteja nas salas disponíveis.")
                nome_filme = input("Qual o filme que quer eliminar? ")

cond = True
while cond == True:
    menu()
    escolha = input("Escolha um número entre 0 e 6, consoante o menu: ")

    if escolha == "":
        n_menu = -1
    else:
        n_menu = int(escolha)

    if n_menu == 1:
        listar(cinema_no_momento)
    elif n_menu == 2:
        lugares_disponíveis(cinema_no_momento)
    elif n_menu == 3:
        vender_bilhete(cinema_no_momento)
    elif n_menu == 4:
        disponibilidade(cinema_no_momento)
    elif n_menu == 5:
        inserir_sala(cinema_no_momento)
    elif n_menu == 6:
        remover_sala(cinema_no_momento)
    elif n_menu == 0:
        print("Saiu da aplicação! Até à próxima.")
        cond = False
    else:
        print("Opção inválida! Escolha um número de 0-6, consoante o menu.")
