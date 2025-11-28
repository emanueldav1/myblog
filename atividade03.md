Python: Matrizes, Arquivos e Pickle com Gráficos Interativos

Este exemplo mostra como criar e manipular matrizes, trabalhar com arquivos e gerar gráficos interativos usando Python, NumPy e Plotly.

import numpy as np
import plotly.express as px
from pickle import dump, load

# MATRIZ COM LIST COMPREHENSION
matrix = [[column for column in range(4)] for row in range(4)]
print("Matrix 4x4:", matrix)

# OPERAÇÕES COM NUMPY
A = np.array([[1, 2], [4, 5]])
B = np.array([[7, 8], [9, 10]])
print("A =", A)
print("B =", B)
print("A + B =", np.add(A, B))
print("A . B =", np.dot(A, B))
print("A transposta =", np.transpose(A))

matrix2 = np.array([[1, 2], [3, 4]])
print("Inversa de [[1,2],[3,4]] =", np.linalg.inv(matrix2))

A = np.array([[1, 2], [3, -5]])
b = np.array([5, 4])
print("A⁻¹ b =", np.dot(np.linalg.inv(A), b))

X = [[1, -2], [1, -2], [1, -1], [1, -1],
     [1, 0], [1, 0], [1, 1], [1, 1],
     [1, 2], [1, 2]]
print("X =", X)

# GRÁFICO INTERATIVO COM PLOTLY
indices = list(range(len(X)))
col1 = [row[1] for row in X]
fig = px.scatter(x=indices, y=col1, labels={'x':'Índice','y':'Valor da coluna 1'})
fig.show()

# LEITURA DE ARQUIVO
with open("arquivo.txt", "r") as f:
    conteudo = f.read()
print("Conteúdo do arquivo:", conteudo)

# LEITURA LINHA A LINHA
texto = []
with open("arquivo.txt", "r") as f:
    for linha in f:
        texto.append(linha.rstrip("\n"))
print("Linhas do arquivo:", texto)

# ESCRITA EM ARQUIVO
with open("arquivo.txt", "w") as f:
    f.write("olá mundo!")

# SALVAR DADOS COM PICKLE
data = {
    'a': [1, 2.0, 3 + 4j],
    'b': "character string",
    'c': {None, True, False}
}
with open('data.pickle', 'wb') as f:
    dump(data, f)

# LER DADOS COM PICKLE
with open('data.pickle', 'rb') as f:
    data = load(f)
print("Dados lidos com pickle:", data)




Resumo

Cria matrizes com list comprehension e NumPy.

Realiza operações como soma, produto, transposição e inversa de matrizes.

Plota gráficos interativos usando Plotly.

Lê e escreve arquivos de texto de várias formas.

Salva e lê objetos Python complexos com Pickle.

