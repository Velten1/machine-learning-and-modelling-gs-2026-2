# VIGIA · Machine Learning & Modelling

FIAP · Global Solution 2026.2 · 1TIAPZ

- Caio Ryan Velten Alves · RM 572913
- João Vitor Fernandes Gomes · RM 573882
- Igor Cypriano Moreno da Silva · RM 570353

## Trabalho apresentado

O VIGIA acompanha uma travessia sujeita a alagamento. Neste trabalho, avaliamos se dados meteorológicos recentes ajudam a identificar janelas de chuva acumulada na região de São Paulo. Essa informação pode ser consultada no painel junto das medições de nível da estação.

| Material | Conteúdo |
|---|---|
| [Notebook de Machine Learning](VIGIA-Machine-Learning.ipynb) | Preparação dos dados, treinamento, ajuste, avaliação e demonstração em dados de teste. |
| [Slides da apresentação](VIGIA%20-%20Slides%20de%20Machine%20Learning.pdf) | Problema, metodologia, resultados e aplicação ao VIGIA. |
| [Vídeo pitch](VIGIA%20-%20Pitch%20de%20Machine%20Learning.mp4) | Apresentação narrada de 4 min 25 s com uma previsão reproduzida do período de teste. |

## Reproduzir o experimento

Abra um terminal nesta pasta com Python 3.13.

```powershell
python -m venv .venv
.\.venv\Scripts\python.exe -m pip install -r requirements.txt
.\.venv\Scripts\python.exe -m jupyter lab
```

Abra o notebook e execute todas as células. Usamos a [cópia da série histórica](dados/era5-sao-paulo-2018-2024.json) incluída no repositório. O notebook gera a [tabela de métricas](metricas-ml.csv) e o [JSON de demonstração](reproducao-ml.json), com um acerto, um falso aviso e uma janela positiva que o modelo deixou passar.

## Fonte e definição do evento

A série usada é a reanálise horária ERA5 do ECMWF, distribuída pela [API histórica da Open-Meteo](https://open-meteo.com/en/docs/historical-weather-api), de 2018 a 2024. A consulta usou latitude −23,50 e longitude −46,62, e a célula retornada tem coordenadas −23,50 e −46,50. Os horários estão em UTC. A série é regional e representa precipitação estimada pela reanálise. O CSV de leituras simuladas da API do VIGIA tem finalidade separada.

Definimos como alvo **pelo menos 10 mm acumulados nas três horas seguintes**. Para uma previsão às 14h, as entradas usam o histórico disponível até 14h e o rótulo usa as horas 15h, 16h e 17h. A série não apresentou exemplos de 20 mm em uma única hora, o limiar inicialmente cogitado.

## Resultados e limites

Separamos treino em 2018–2021, validação em 2022–2023 e teste em 2024. Comparamos uma referência majoritária, regressão logística e Random Forest. Escolhemos a regressão logística pela maior precisão média (AP) na validação. No teste, ela obteve AP de 0,172, identificou 14 de 54 janelas positivas e gerou 58 falsos avisos. Janelas próximas podem representar o mesmo episódio de chuva.

A avaliação usa precipitação regional estimada pela reanálise. O JSON permite apresentar o resultado no painel como reprodução histórica, com o horário da previsão e o acumulado posterior. A calibração do escore como probabilidade ficou fora da avaliação. A API de Python classifica o nível na travessia por regras aplicadas às medições do dispositivo.
