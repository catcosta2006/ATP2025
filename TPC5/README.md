# TPC5
## Autor
Catarina Pereira Costa, A111924, (![foto](foto.jpg))
## Resumo
Desenvolvimento de uma aplicação que gere alunos em turmas através de um menu com tarefas.
## Resultados
* Res1:
# TPC5 - Aplicação de gestão de alunos em turmas
# aluno = (nome, id, [notaTPC, notaProj, notaTeste])
# turma = [aluno]

def menu():
    print("""
(1) Criar uma turma;
(2) Inserir um aluno na turma;
(3) Listar a turma;
(4) Consultar um aluno por id;
(5) Guardar a turma em ficheiro;
(6) Carregar uma turma dum ficheiro;
(0) Sair da aplicação
    """)
    return


def criar_turma():
    print("A turma foi criada! Já pode adicionar alunos.")
    return []


def inserir_aluno(turma):
    if turma is None: 
        print("Ainda não criaste a turma!")
        return turma

    if len(turma) == 5:
        print("Turma cheia!")
        return turma
    nome = str(input("Nome do aluno: "))

    id_valido = False
    while id_valido == False:
        id = str(input("Id do aluno: "))
        existe_id = False
        for aluno in turma:
            if aluno[1] == id:
                existe_id = True

        if existe_id:
            print("Já existe um aluno com esse id nesta turma! Tente novamente")
        else:
            id_valido = True
       
    cond = True
    while cond == True:
        nota_TPC = float(input("Nota do TPC: "))
        nota_Proj = float(input("Nota do projeto: "))
        nota_Teste = float(input("Nota do teste: "))     

        if 0 <= nota_TPC <= 20 and 0 <= nota_Proj <= 20 and 0 <= nota_Teste <= 20:
            cond = False  # sai do ciclo, todas válidas
        else:
            print("Erro: todas as notas devem estar entre 0 e 20. Tente novamente.")

    aluno = (nome, id, [nota_TPC, nota_Proj, nota_Teste])
    turma.append(aluno)
    print("Aluno inserido na turma com sucesso!")
    return turma


def listar_turma(turma):
    if turma is None or turma == []:
        print("Turma vazia! Insira os alunos na turma.")
    else:
        for aluno in turma:
            print("Nome:", aluno[0], "ID:", aluno[1], "Notas:", aluno[2] )


def consultar_aluno(turma):
    if turma is None:
        print("Ainda não criaste turma!")
        return
    id = input("Id do aluno: ")
    encontrado = False
    for aluno in turma:
        if aluno[1] == id:
            print("Aluno encontrado:", aluno[0],"; Notas:", aluno[2])
            encontrado = True
    if not encontrado: 
        print("Aluno não encontrado! Tente novamente.")
    return
        


def guardar_turma(turma, f_nome):
    if turma is None:
        print("Ainda não criaste turma!")
    file = open(f_nome,"w")
    res = ""
    for aluno in turma:
        nome, id, notas = aluno
        nota_TPC, nota_Proj, nota_Teste = notas
        res = res + "Nome: " + str(nome) + "; " + "Id: " + str(id) + "; " +  "Nota_TPC: " + str(nota_TPC) + "; " + "Nota_Proj: " + str(nota_Proj) + "; " + "Nota_Teste: " + str(nota_Teste) + "\n"
    file.write(res)
    file.close()


def carregar_turma(turma, f_nome): 
    turma = []
    file = open(f_nome, "r")
    text = file.read()
    aluno_text = text.split("\n")
    for x_text in aluno_text[:-1]:
        y_text = x_text.split(";")
        nome = y_text[0]
        id = y_text[1]
        notas = [(y_text[2]), (y_text[3]), (y_text[4])]
        aluno = (nome, id, notas)
        turma.append(aluno)
    file.close()
    return turma


turma_no_momento = None
cond = True

while cond == True:
    menu()
    escolha = input("Escolha um número entre 0 e 6, consoante o menu: ")
    if escolha == "":
        n_menu = -1
    else:
        n_menu = int(escolha)
    
    if n_menu == 1:
        turma_no_momento = criar_turma()
    elif n_menu == 2:
        turma_no_momento = inserir_aluno(turma_no_momento)
    elif n_menu == 3:
        listar_turma(turma_no_momento)
    elif n_menu == 4:
        consultar_aluno(turma_no_momento)
    elif n_menu == 5:
        guardar_turma(turma_no_momento, "turma.txt")
        print("Turma guardada com sucesso no ficheiro turma.txt!")
    elif n_menu == 6:
        turma_no_momento = carregar_turma(turma_no_momento, "turma.txt")
        print(turma_no_momento)
    elif n_menu == 0:
        print("Saiu da aplicação! Até breve!")
        cond = False
    else:
        print("Opção inválida! Escolha um número entre 0 e 6, consoante o menu: ")