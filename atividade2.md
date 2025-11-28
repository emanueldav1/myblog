Mapa Interativo de Ônibus em Tempo Real com Python

import os
import requests
from dotenv import load_dotenv
from folium import Map, Marker

load_dotenv(".env")

s = requests.Session()
s.post(f"http://api.olhovivo.sptrans.com.br/v2.1/Login/Autenticar?token={os.getenv('SPTRANS_TOKEN')}")

linhas_lapa = s.get("http://api.olhovivo.sptrans.com.br/v2.1/Linha/Buscar?termosBusca=Lapa").json()
paradas = s.get("http://api.olhovivo.sptrans.com.br/v2.1/Parada/BuscarParadasPorLinha?codigoLinha=2506").json()

m = Map(location=[paradas[0]["py"], paradas[0]["px"]], zoom_start=14)
for i in paradas:
    Marker([i["py"], i["px"]], popup=i["np"]).add_to(m)

pos = s.get("http://api.olhovivo.sptrans.com.br/v2.1/Posicao/Linha?codigoLinha=2506").json()
for bus in pos["vs"]:
    Marker([bus["py"], bus["px"]], popup=f"Ônibus {bus['p']}").add_to(m)

m.show_in_browser()

Como funciona:

Faz login na API do SPTrans usando um token seguro do arquivo .env.

Busca informações da linha “Lapa” e suas paradas.

Cria um mapa com Folium mostrando todas as paradas.

Adiciona a posição dos ônibus em tempo real.

Abre o mapa no navegador para visualização interativa.
