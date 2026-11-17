# VIGIA · Machine Learning & Modelling

FIAP · Global Solution 2026.2 · 1TIAPZ

- Caio Ryan Velten Alves · RM 572913
- João Vitor Fernandes Gomes · RM 573882
- Igor Cypriano Moreno da Silva · RM 570353

## Reproduzir o experimento

Abra um terminal nesta pasta com Python 3.13.

```powershell
python -m venv .venv
.\.venv\Scripts\python.exe -m pip install -r requirements.txt
.\.venv\Scripts\python.exe -m jupyter lab
```

Abra `VIGIA-Machine-Learning.ipynb` e execute todas as células. A base congelada fica em `dados/`. A execução gera `metricas-ml.csv` e `reproducao-ml.json`. O JSON contém um acerto, um falso aviso e um caso perdido para exibir na plataforma.

## Fonte e definição do evento

A série usada é a reanálise horária ERA5 do ECMWF, distribuída pela [API histórica da Open-Meteo](https://open-meteo.com/en/docs/historical-weather-api), de 2018 a 2024. A consulta usou latitude −23,50 e longitude −46,62, e a célula retornada tem coordenadas −23,50 e −46,50. Os horários estão em UTC. A série é regional e representa precipitação estimada pela reanálise. O CSV de leituras simuladas da API do VIGIA tem finalidade separada.

O alvo didático indica **pelo menos 10 mm acumulados nas três horas seguintes**, definido para obter exemplos em todos os períodos desta série. Em uma observação às 14h, o rótulo usa as horas 15h, 16h e 17h. O modelo recebe somente valores até 14h. A regra de 20 mm em uma única hora do plano inicial não gerava positivos na grade analisada. Os modelos são experimentais e o resultado é apresentado como reprodução histórica. O alvo não é uma cota de rio ou alagamento.

## Entrega

O PDF de slides resume o problema, os dados, os modelos, o ajuste, as métricas, as variáveis importantes e a aplicação. O MP4 é o pitch narrado com voz sintetizada e a demonstração de uma previsão do período de teste. Para submissão, hospede o vídeo no YouTube como não listado ou no Google Drive com acesso habilitado, conforme o enunciado.
