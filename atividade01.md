Cotação do Dólar e Mapas Interativos com Python

Este código faz duas coisas: pega a cotação do dólar e cria um mapa interativo de veículos.

import requests
from datetime import datetime, timedelta
import plotly.express as px
import pandas as pd
from folium import Map, Marker, Icon

def cotar(data):
    url = f"https://olinda.bcb.gov.br/olinda/servico/PTAX/versao/v1/odata/CotacaoDolarDia(dataCotacao=@dataCotacao)?%40dataCotacao='{data}'&%24format=json"
    res = requests.get(url).json()
    return res['value'][0]['cotacaoCompra'] if res['value'] else None

data_inicio = datetime(2025, 10, 1)
data_final = datetime(2025, 10, 31)
datas, valores = [], []

while data_inicio <= data_final:
    valor = cotar(data_inicio.strftime("%m-%d-%Y"))
    if valor: 
        datas.append(data_inicio.strftime("%d/%m/%Y"))
        valores.append(valor)
    data_inicio += timedelta(days=1)

df = pd.DataFrame({"Data": datas, "Valor": valores})
px.line(df, x="Data", y="Valor", title="Cotação Dólar Outubro 2025").show()

m = Map(location=[paradas[3]["py"], paradas[3]["px"]], zoom_start=14)
for i in paradas: Marker([i["py"], i["px"]], popup=i["np"]).add_to(m)
for v in veiculos: Marker([v["py"], v["px"]], popup=f"Ônibus - Última: {v['ta']}", icon=Icon(color="red")).add_to(m)
m.save("frota.html")


Resumo:

Consulta a cotação do dólar do Banco Central para outubro de 2025.

Cria gráfico interativo com Plotly.

Gera mapa interativo de paradas e veículos com Folium.
<img width="1600" height="753" alt="image" src="https://github.com/user-attachments/assets/befc973e-7256-4124-a443-79364ca43997" />

