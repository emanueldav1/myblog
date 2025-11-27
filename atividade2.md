Atividade 2 – Monitoramento de Frota de Ônibus (SPTrans)
 Objetivo

Construir um mapa exibindo:

As paradas de uma linha de ônibus

A posição em tempo real dos veículos

Cada categoria com marcadores de cores diferentes

Utilizando a API SPTrans Olho Vivo

 Código utilizado
import os
import requests
from dotenv import load_dotenv
from folium import Map, Marker, Popup

load_dotenv(".env")

s = requests.Session()
s.post(f"http://api.olhovivo.sptrans.com.br/v2.1/Login/Autenticar?token={os.getenv('SPTRANS_TOKEN')}")

linhas_lapa = s.get("http://api.olhovivo.sptrans.com.br/v2.1/Linha/Buscar?termosBusca=Lapa").json()

paradas = s.get("http://api.olhovivo.sptrans.com.br/v2.1/Parada/BuscarParadasPorLinha?codigoLinha=2506").json()

m = Map(location=[paradas[0]["py"], paradas[0]["px"]], zoom_start=14)
for i in paradas:
    Marker(location=[i["py"], i["px"]], popup=i["np"]).add_to(m)

pos = s.get("http://api.olhovivo.sptrans.com.br/v2.1/Posicao/Linha?codigoLinha=2506").json()

for bus in pos["vs"]:
    Marker(
        location=[bus["py"], bus["px"]],
        popup=f"Ônibus {bus['p']}"
    ).add_to(m)

m.show_in_browser()

 Explicação do código — linha por linha
1. Importação das bibliotecas
import os
import requests
from dotenv import load_dotenv
from folium import Map, Marker, Popup


Essas bibliotecas permitem:

Ler variáveis de ambiente

Fazer requisições à API

Criar o mapa e os marcadores

2. Carregar o token
load_dotenv(".env")


Carrega o arquivo .env que contém a variável:
SPTRANS_TOKEN=seu_token_aqui

3. Criar sessão e autenticar no Olho Vivo
s = requests.Session()
s.post(f"http://api.olhovivo.sptrans.com.br/v2.1/Login/Autenticar?token={os.getenv('SPTRANS_TOKEN')}")


Cria uma sessão persistente e autentica na API.
Sem isso, nenhuma chamada funciona.

4. Buscar as linhas relacionadas à Lapa
linhas_lapa = s.get("http://api.olhovivo.sptrans.com.br/v2.1/Linha/Buscar?termosBusca=Lapa").json()


Retorna várias linhas que passam pela região pesquisada.

5. Buscar as paradas da linha escolhida
paradas = s.get("http://api.olhovivo.sptrans.com.br/v2.1/Parada/BuscarParadasPorLinha?codigoLinha=2506").json()


Aqui escolhemos o código da linha 2506, mas cada aluno deve usar uma linha diferente.

6. Criar o mapa e adicionar as paradas
m = Map(location=[paradas[0]["py"], paradas[0]["px"]], zoom_start=14)
for i in paradas:
    Marker(location=[i["py"], i["px"]], popup=i["np"]).add_to(m)


O mapa é centralizado na primeira parada

Cada parada recebe um marcador azul padrão

i["np"] mostra o nome da parada no popup

7. Buscar a posição em tempo real dos ônibus
pos = s.get("http://api.olhovivo.sptrans.com.br/v2.1/Posicao/Linha?codigoLinha=2506").json()


Retorna todos os veículos em operação na linha.

8. Inserir os ônibus no mapa
for bus in pos["vs"]:
    Marker(
        location=[bus["py"], bus["px"]],
        popup=f"Ônibus {bus['p']}"
    ).add_to(m)


Cada veículo recebe um marcador

O popup mostra o prefixo do ônibus

Se quiser, posso colocar cores diferentes (ex.: vermelho para ônibus).

9. Mostrar o mapa
m.show_in_browser()


Abre o mapa no navegador, permitindo visualizar tudo.

<img width="1910" height="943" alt="image" src="https://github.com/user-attachments/assets/91ecaa1b-f17f-47fe-8a66-43b7c9ac61bc" />



