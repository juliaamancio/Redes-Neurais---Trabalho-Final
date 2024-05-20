# Redes-Neurais: Trabalho-Final
Esse repositório diz respeito ao trabalho final de 'Redes Neurais' do curso de Ciência e Tecnologia da Ilum Escola de Ciência.

### Sobre o dataset:
A proposta do trabalho é prever a temperatura de transição vítrea reduzida $T_{rg}$,, que é definida como:
$$T_{rg} = \frac{T_g}{T_l}$$ com $T_g$ sendo a temperatura de transição vítrea e $T_l$ sendo a temperatura líquida da liga metálica. Como proposto e comprovado no artigo "Reduced glass transition temperature and glass forming ability
of bulk glass forming alloys" por Z.P. Lu e Y. Li em 2000, a $T_{rg}$ permite estimar a GFA (Glass Forming Ability) de uma liga. É com base nesse artigo que fundamentamos a relevância científica do presente trabalho.

### Estratégias adotadas para a execução do trabalho:
O tratamento dos dados baseou-se na remoção da coluna de 'principal elemento'. Além disso, a coluna de 'Composição do material', que continha dados em strings, foi completamente convertida em novas colunas, nas quais cada uma delas representa um elemento químico e cada célula indicará a fração molar do respectivo elemento a respeito daquele material. Assim, removemos a coluna de 'Composição do material', já que foi completamente convertida. Por fim, removemos todos os dados 'Not a Number' possíveis, caso existissem.

Inicialmente criamos e treinamos uma rede neural com parâmetros arbitrários (mas razoáveis) para avaliar possíveis inconsistências e/ou problemas. Essa etapa foi importante para estabelecer as etapas de trabalho e garantir a reprodutibilidade, evitando P-hacking e "injustiças" na comparação entre as diferentes arquiteturas, que é o objetivo da otimização de hiperparâmetros.

Com isso, as seguintes etapas foram seguidas, para as duas versões do dataset:

* Tratamento dos dados;
* Análise exploratória;
* Coleta dos dados (definindo quais colunas são features e qual será o target);
* Separação em 3 (três) conjuntos: treino, teste e validação. (é importante fixar uma semente aleatória nessa etapa);
* Um normalizador por máximo absoluto foi aplicado ao conjunto de treino;
* Os dados foram convertidos em tensores (conversão necessária para o uso do PyTorch Lightning);
* O PyTorch Lightning permite a criação de DataLoaders que organizam e otimizam o carregamento dos dados;
* Cria-se uma rede neural MLP (Multi Layer Perceptron) seguindo a sintaxe adotada pelo PyTorch Lightning;
* Na MLP, define-se o número de dados de entrada (20 e 64, nesse trabalho), número de camadas, número de neurônios (igual para todas as camadas), função de ativação empregada, taxa de dropout (fixa para todas as camadas ocultas), número de dados de saída (1, neste trabalho) e taxa de aprendizado;
* Utilizando o optuna, foi realizada a otimização dos hiperparâmetros variando os seguintes valores:
  * Número de camadas
  * Número de neurônios das camadas
  * Função de ativação
  * Taxa de Dropout
  * Taxa de aprendizado
* De posse dos conjunto de hiperparâmetros identificados pelo optuna, treinamos a rede neural com o parâmetro de menor erro quadrático médio, e com o conjunto com menor número de parâmetros treináveis;
* Análise dos resultados, descrita no README.
  
### Organização do repositório:
* __Pasta 20 features:__ Nessa pasta estão contidos os arquivos em que trabalhamos com o dataset informações quanto à composição da liga metálica. Esse conjunto de dados está contido no arquivo _df_teste_, que é lido utilizando o módulo _pickle_.

### Bibliotecas e Módulos utilizados:
Nesta seção, listamos as bibliotecas e módulos implementados nos códigos neste repositório. A descrição de cada elemento, segue acompanhada de um link para a documentação oficial ou para uma página de tutoria.

__OBS 1:__ Todos os códigos neste repositório estão em linguagem Python.

__OBS 2:__ Os textos foram gerados por inteligência artificial (ChatGPT) e validados e editados pelos autores deste documento.

* __MatPlotLib:__ biblioteca de visualização de dados usada para criar gráficos. https://matplotlib.org/stable/index.html
  
* __NumPy:__ biblioteca de computação numérica eficiente com suporte a arrays multidimensionais. https://numpy.org/doc/
  
* __pandas:__ biblioteca para análise de dados que oferece estruturas de dados e ferramentas de manipulação, simplificando tarefas como limpeza, transformação e análise de conjuntos de dados.
https://pandas.pydata.org/docs/
  
* __pickle:__  módulo em Python que permite a serialização e desserialização de objetos Python, facilitando o armazenamento de dados.
  https://docs.python.org/3/library/pickle.html
  
* __PyTorch:__ biblioteca de código aberto que oferece suporte para criação de modelos de deep learning, permitindo fácil implementação de redes neurais e computação numérica eficiente em GPUs. https://pytorch.org/docs/stable/index.html
  
* __PyTorch Lightning:__ biblioteca que simplifica o processo de treinamento de modelos de deep learning com PyTorch, oferecendo uma estrutura organizada e padronizada para experimentação rápida, escalabilidade e reprodução de resultados.
  https://lightning.ai/docs/pytorch/stable/

* __csv:__* fornece funcionalidades para ler e escrever arquivos CSV (Comma-Separated Values), permitindo manipulação de dados tabulares.
  https://docs.python.org/3/library/csv.html

* __SciPy:__ biblioteca para computação científica e técnica, oferecendo ferramentas para análise de dados, otimização e processamento de sinais.
  https://docs.scipy.org/doc/scipy/

* __Scikit-learn:__ biblioteca para aprendizado de máquina que oferece algoritmos de classificação, regressão, agrupamento e pré-processamento de dados, além de ferramentas para avaliação de modelos e seleção de parâmetros.
  https://scikit-learn.org/stable/
