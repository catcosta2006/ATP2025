# TPC7
## Autor
Catarina Pereira Costa, A111924, (![foto](foto.jpg))
## Resumo
Resolução do teste de aferição.
## Resultados
* Res1:
* tpc1
(a)
lista1 = [1, 2, 3, 4, 5]
lista2 = [4, 5, 6, 7, 8]  
ncomuns = []

só_na_lista1 = []
for elem in lista1:
    if elem not in lista2:
        só_na_lista1.append(elem)

só_na_lista2 = []
for elem in lista2:
    if elem not in lista1:
        só_na_lista2.append(elem)

ncomuns = só_na_lista1 + só_na_lista2
        
print(ncomuns)

(b)
texto = """Vivia há já não poucos anos algures num concelho do Ribatejo 
    um pequeno lavrador e negociante de gado chamado Manuel Peres Vigário"""

lista_palavras = texto.split()
lista_3 = []
for palavra in lista_palavras:
    if len(palavra) > 3 :
        lista_3.append(palavra)

print(lista_3)

(c)
lista = ['anaconda', 'burro', 'cavalo', 'macaco']
lista_pares = []
for índice in range(len(lista)):
    nome = lista[índice]
    par = (índice + 1, nome)
    lista_pares.append(par)
print(lista_pares)

* tpc2
(a)
def strCount(s, subs):
    contador = 0
    i = 0
    while i <= len(s) - len(subs):
        if s[i:i + (len(subs))] == subs:
            contador = contador + 1
            i = i + len(subs)
        else:
            i = i + 1
    return contador

print(strCount("catcowcat", "cat")) # --> 2
print(strCount("catcowcat", "cow")) # --> 1
print(strCount("catcowcat", "dog")) # --> 0

(b)
def produtoM3(lista):
    menores = []
    valores_produto = 0
    while valores_produto < 3:
        menor = lista[0]
        for num in lista[1:]:
            if num < menor:
                menor = num

        menores.append(menor)
        lista.remove(menor)
        valores_produto = valores_produto + 1
    produto = menores[0] * menores[1] * menores[2]
    return produto


print(produtoM3([12,3,7,10,12,8,9]))

(c)
def reduxInt(n):
    n_atual = n
    while len(str(n_atual)) > 1:
        soma = 0
        digitos_n = 0
        for elem in str(n_atual) :
            soma = soma + int(elem)
            digitos_n = digitos_n + 1
        n_atual = soma
    return soma

print(reduxInt(38))
print(reduxInt(777))

(d)
def myIndexOf(s1, s2):
    if s2 not in s1:
        return '-1'
    else:
        frase = s1
        palavra = s2
        índice_palavra = frase.index(palavra)
    return índice_palavra

print(myIndexOf("Hoje está um belo dia de sol!", "chuva"))
print(myIndexOf("Hoje está um belo dia de sol!", "belo"))

* tpc3 - rede social
(a)
def quantosPost(redeSocial):
    return len(MyFaceBook)

print(quantosPost(MyFaceBook))

(b)
def postsAutor(redeSocial, autor):
    lista_posts_autor = []
    for post in redeSocial:
        if post['autor'] == autor:
            lista_posts_autor.append(post)

    if len(lista_posts_autor) == 0:
        return "Esse autor não tem posts!"

    return lista_posts_autor
print(postsAutor(MyFaceBook, 'Luís'))

(c)
def autores(redeSocial):
    autor_redeSocial = [] # lista dos autores dos posts sem repetições
    for post in redeSocial:
        autor_atual = post['autor']
        if autor_atual not in autor_redeSocial: # se alguém postar mais que uma vez o nome só aparece uma vez nesta lista
            autor_redeSocial.append(autor_atual)

    n = len(autor_redeSocial)
    for i in range(n - 1):
        for j in range(0, n - i - 1):
            if autor_redeSocial[j] > autor_redeSocial[j + 1]: # primeira letra do 1º nome > primeira letra do 2º
                autor_redeSocial[j], autor_redeSocial[j + 1] = autor_redeSocial[j + 1], autor_redeSocial[j]
    return autor_redeSocial

print(autores(MyFaceBook))

(d)
def insPost(redeSocial, conteudo, autor, dataCriacao, comentarios):
    
    novo_post = {
        "id": "post" + str(int(redeSocial[-1]['id'][4:])+ 1),
        "conteudo": conteudo,
        "autor": autor,
        "dataCriacao": dataCriacao,
        "comentarios": comentarios
    }
    redeSocial.append(novo_post)
    return redeSocial

MyFaceBook = insPost(MyFaceBook, 'Que bela paisagem!', "Ana", "2025-05-15", [{'comentario': 'É a primavera...', 'autor': 'Clara'}])
print(MyFaceBook)

(e)
def remPost(redeSocial, id):
    n_lista = []
    for elem in redeSocial:
        if elem['id'] != id:
            n_lista.append(elem)
    if n_lista == redeSocial:
        print("Não existe esse id. O post não será removido!")
    return n_lista

MyFaceBook = remPost(MyFaceBook, "post2")
print(MyFaceBook)

(f)
def postsPorAutor(redeSocial):
    distrib = {}
    for elem in redeSocial:
        if elem['autor'] in distrib:
            distrib[elem['autor']] = distrib[elem['autor']] + 1
        else:
            distrib[elem['autor']] = 1
    return distrib
print(postsPorAutor(MyFaceBook))

(g)
def comentadoPor(redeSocial, autor):
    comentado = []
    cond = False
    for elem in redeSocial:
        for comentario in elem['comentarios']:
            if comentario['autor'] == autor:
                comentado.append(elem)
                cond = True
    if cond == False:
        print("Não foi encontrado!")
        cond = False
    return comentado
print(comentadoPor(MyFaceBook, "Carlos"))