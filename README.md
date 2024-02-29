
# Processo para trabalhar com Machine Learning no Azure ML

Para utilizar o Azure Machine Learning, foi necessário aprovisionar um espaço de trabalho do Azure Machine Learning na subscrição do Azure. Depois, você foi possível usar o estúdio Azure Machine Learning para trabalhar com os recursos do workspace

Passos necessários:

* Entrar no portal do Azure usando https://portal.azure.comsuas credenciais da Microsoft.
* Selecione + Criar um recurso , pesquise Machine Learning e crie um novo recurso do Azure Machine Learning.
* Selecione Launch Studio (ou abra uma nova guia do navegador e navegue até https://ml.azure.com e entre no Azure Machine Learning Studio usando sua conta da Microsoft). Feche todas as mensagens exibidas.
* No estúdio Azure Machine Learning, você deverá ver seu espaço de trabalho recém-criado. Caso contrário, selecione Todos os espaços de trabalho no menu à esquerda e selecione o espaço de trabalho que você acabou de criar.

## Usar aprendizado de máquina automatizado para treinar um modelo

O aprendizado de máquina automatizado permite que você experimente vários algoritmos e parâmetros para treinar vários modelos e identificar o melhor para seus dados. Neste exercício, você usará um conjunto de dados de detalhes históricos de aluguel de bicicletas para treinar um modelo que prevê o número de aluguel de bicicletas esperado em um determinado dia, com base em características sazonais e meteorológicas.

- No Azure Machine Learning Studio , veja a página Automated ML (em Authoring ).
- Crie um novo trabalho de ML automatizado com as seguintes configurações, usando Next conforme necessário para avançar pela interface do usuário:
- Envie o trabalho de treinamento. Ele inicia automaticamente.
- Espere o trabalho terminar. Pode demorar um pouco – agora pode ser um bom momento para uma pausa para o café!

## Avaliar o melhor modelo

Quando o trabalho automatizado de aprendizado de máquina for concluído, você poderá revisar o melhor modelo treinado.
- Na guia Visão geral do trabalho automatizado de aprendizado de máquina, observe o melhor resumo do modelo.
- Selecione o texto em Nome do algoritmo do melhor modelo para visualizar seus detalhes.
- Selecione a guia Métricas e selecione os gráficos residuais e predito_true se eles ainda não estiverem selecionados.

Revise os gráficos que mostram o desempenho do modelo. O gráfico de resíduos mostra os resíduos (as diferenças entre os valores previstos e reais) como um histograma. O gráfico predito_true compara os valores previstos com os valores verdadeiros.
## Implantar e testar o modelo

- Na guia Modelo do melhor modelo treinado pelo seu trabalho automatizado de machine learning, selecione Implantar e use a opção de serviço Web para implantar o modelo
- Aguarde o início da implantação – isso pode levar alguns segundos. O status de implantação do endpoint de previsão de aluguel será indicado na parte principal da página como Running .
- Aguarde até que o status da implantação mude para Succeeded . Isso pode levar de 5 a 10 minutos.

## Testar o serviço implantado

- No estúdio Azure Machine Learning, no menu esquerdo, selecione Endpoints e abra o ponto final em tempo real de previsão de alugueres .
- Na página do endpoint em tempo real de previsão de aluguel, visualize a guia Teste .
- No painel Dados de entrada para testar o endpoint , substitua o modelo JSON pelos seguintes dados de entrada:
```json
   {
   "Inputs": { 
     "data": [
       {
         "day": 1,
         "mnth": 1,   
         "year": 2022,
         "season": 2,
         "holiday": 0,
         "weekday": 1,
         "workingday": 1,
         "weathersit": 2, 
         "temp": 0.3, 
         "atemp": 0.3,
         "hum": 0.3,
         "windspeed": 0.3 
       }
     ]    
   },   
   "GlobalParameters": 1.0
 }
```
- Clique no botão Testar .
- evise os resultados do teste, que incluem um número previsto de aluguéis com base nos recursos de entrada - semelhante a este:

```json
    {
   "Results": [
     444.27799000000000
   ]
 }
```
O painel de teste pegou os dados de entrada e usou o modelo treinado para retornar o número previsto de aluguéis.