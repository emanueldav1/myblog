📘 ATIVIDADE 1 – Cotação do Dólar por Período (API PTAX – Banco Central)
🎯 Objetivo

Criar uma rotina que:

Receba uma string no formato "MMYYYY"

Determine automaticamente o dia inicial e dia final do mês

Consulte a API PTAX do Banco Central

Retorne um gráfico de linha com a cotação de compra para cada dia do mês

Exemplo de entrada: "102025" → Outubro de 2025

import requests
from datetime import datetime, timedelta
import plotly.express as px
import pandas as pd

def obter_cotacao(data_str):
    url = (
        "https://olinda.bcb.gov.br/olinda/servico/PTAX/versao/v1/"
        f"odata/CotacaoDolarDia(dataCotacao=@dataCotacao)?@dataCotacao='{data_str}'&$format=json"
    )
    res = requests.get(url).json()
    if res["value"] == []:
        return None
    return res["value"][0]["cotacaoCompra"]

def grafico_cotacao(periodo):
    mes = int(periodo[:2])
    ano = int(periodo[2:])
    
    data_inicio = datetime(year=ano, month=mes, day=1)
    if mes == 12:
        data_final = datetime(year=ano + 1, month=1, day=1) - timedelta(days=1)
    else:
        data_final = datetime(year=ano, month=mes + 1, day=1) - timedelta(days=1)

    datas = []
    valores = []

    atual = data_inicio
    while atual <= data_final:
        data_api = atual.strftime("%m-%d-%Y")
        valor = obter_cotacao(data_api)
        if valor is not None:
            datas.append(atual.strftime("%d/%m/%Y"))
            valores.append(valor)
        atual += timedelta(days=1)

    df = pd.DataFrame({"Data": datas, "Valor": valores})

    fig = px.line(df, x="Data", y="Valor", title=f"Cotação do Dólar – {periodo}")
    fig.show()

grafico_cotacao("102025")

🧠 Explicação do Código – Passo a Passo
✔ Importações
import requests
from datetime import datetime, timedelta
import plotly.express as px
import pandas as pd
 Bibliotecas para requisição HTTP, manipulação de datas, gráficos e tabela.

 ✔ Função para consultar a API
 def obter_cotacao(data_str):
A função recebe a data no formato MM-DD-YYYY, que é exigido pela API.

A URL já está no padrão que o Banco Central exige.

Se a API não retornar cotação (feriado/fim de semana), retorna None.

✔ Função principal

def grafico_cotacao(periodo):
A string "MMYYYY" é dividida:
mes = int(periodo[:2])
ano = int(periodo[2:])

✔ Determinação do primeiro e último dia do mês

data_inicio = datetime(year=ano, month=mes, day=1)

O último dia é calculado assim:

data_final = datetime(year=ano, month=mes+1, day=1) - timedelta(days=1)

Esse método funciona para qualquer mês, inclusive fevereiro.
✔ Loop para buscar cada dia

while atual <= data_final:

Cada dia é formatado no padrão exigido pela API:

data_api = atual.strftime("%m-%d-%Y")

Se existir cotação:

Salva a data

Salva o valor

✔ Construir DataFrame

df = pd.DataFrame({"Data": datas, "Valor": valores})

✔ Gerar gráfico Plotly
fig = px.line(df, x="Data", y="Valor", title=f"Cotação do Dólar – {periodo}")

fig.show()
<img width="1877" height="897" alt="image" src="https://github.com/user-attachments/assets/129b7897-31f0-40e7-b872-81925527bcdd" />

