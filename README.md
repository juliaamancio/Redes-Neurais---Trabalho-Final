# Redes-Neurais: Trabalho-Final
Esse repositório diz respeito ao trabalho final de 'Redes Neurais' do curso de Ciência e Tecnologia da Ilum Escola de Ciência.
 
## Equipe
Davi José, Gabriel Torquato e Júlia Amancio. :D
 
### Organização do repositório:
* __Readme__: Contém as informações gerais sobre o trabalho abordado, levando em conta objetivo, apresentação do dataset, descrição do repositórios e bibliotecas, além das referências bibliográficas.
* __Pasta 20 features:__ Nessa pasta estão contidos os arquivos em que trabalhamos com o dataset sem a informação de fração molar dos elementos que compõem a liga metálica. Esse conjunto de dados está contido no arquivo _df_teste_, que é lido utilizando o módulo _pickle_. 
* __Pasta 64 features:__ Nessa pasta estão contidos os arquivos em que trabalhamos com o dataset com a informação da fração molar de cada elemento que compõe a liga metálica, em que contém as colunas com todos os elementos químicos presentes no dataset. Esse conjunto de dados está contido no arquivo _df_novo_, que é lido utilizando o módulo _pickle_.
* __Notebook didático__: Nesse notebook foi retratado um exemplo de treinamento de uma rede simples para a explicação do funcionamento da rede neural em relação à sua arquitetura e modo de previsão. Ele serve como guia para os demais notebooks presentes nas pastas de 20 features e 64 features.
* __Tratamento de dados__: Refere-se a um notebook contendo os dados tratados e com uma análise exploratória a partir dele.
* __metallic_glass.csv__: Refere-se ao dataset original contendo todos os dados.
 
__OBS 1:__ O notebook 'Testando e Avaliando as Redes' para ambas as pastas (20 features e 64 features) leva em conta os melhores hiperparâmetros encontrados no notebook 'Otimização de Hiperparâmetros'.
 
### Recomendação de leitura 
* __1) Tratamento de dados__
* __2) Notebook didático__
* __3) Pasta 20 features: Otimização -> Testando e avaliando as redes__
* __4) Pasta 64 features: Otimização -> Testando e avaliando as redes__
 
### Objetivo do trabalho:
A proposta do trabalho é prever a temperatura de transição vítrea reduzida $T_{rg}$,, que é definida como:
$$T_{rg} = \frac{T_g}{T_l}$$ com $T_g$ sendo a temperatura de transição vítrea e $T_l$ sendo a temperatura líquida da liga metálica. Como proposto e comprovado no artigo "Reduced glass transition temperature and glass forming ability
of bulk glass forming alloys" por Z.P. Lu e Y. Li em 2000 [6], a $T_{rg}$ permite estimar a GFA (Glass Forming Ability) de uma liga. É com base nesse artigo que fundamentamos a relevância científica do presente trabalho.
 
### Sobre o dataset:
O dataset aborda um total de 23 colunas, sendo 22 features e 1 target (Trg - temperatura de transição vítrea reduzida), contendo 585 exemplos (linhas). As features dizem respeito a valores obtidos para 585 tipos de materiais diferentes criados. De modo geral, as features são divididas em dois grupos: features que são características da liga e features relacionadas ao elemento predominante/principal da composição da liga.
 
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

### Perspectivas Futuras:
* Melhorar a representação dos dados considerando a estrura de tensores adotada pelo PyTorch. Isso é interessante para considerar o número de algarismos significativos condizente com os dados de entrada.
* Melhorar a análise SHAP buscando interpretar a correlação entre as features e o target.
* Buscar outros conjuntos de dados com valores não catalogados no dataset utilizado para testar a robustez do nosso modelo.
* Buscar detalhes sobre as escalas numéricas adotadas nas features.
  
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
 
### Referências bibliográficas
 
[1] COSTA, Breno Pontes da. Predição de resultados em partidas de League of Legends usando redes neurais e análise SHAP. 2023. Trabalho de Conclusão de Curso (Bacharelado em Ciência da Computação) – Instituto de Computação, Universidade Federal do Rio de Janeiro, Rio de Janeiro, 2023.

[2] MALTA, Fernando Augusto Melo Duarte. Redes Neurais para Dados Tabulares: Uma Comparação Empírica. 2022. Trabalho de Conclusão de Curso (Graduação em Estatística) – Instituto de Ciências Exatas, Departamento de Estatística, Universidade Federal de Minas Gerais, Belo Horizonte, 2022.

[3] Cassar, Daniel(2024). ATP-303 NN 5.3 - Notebook PyTorch Lightning.ipynb. Retirado dos arquivos de Redes Neurais e Algoritimos Genéticos da Ilum - Escola de Ciência.

[4] Cassar, Daniel(2024). ATP-303 NN 5.2 - Notebook PyTorch.ipynb. Retirado dos arquivos de Redes Neurais e Algoritimos Genéticos da Ilum - Escola de Ciência.

[5] SHAHANE, Saurabh. Metallic Glass Forming: Predict the Reduced Glass Transition Temperature. Disponível em: https://www.kaggle.com/datasets/saurabhshahane/metallic-glass-forming. Acesso em: 21 maio 2024.

[6] Lu, Z. P., Li, Y., & Ng, S. C. Reduced glass transition temperature and glass forming ability of bulk glass forming alloys. Department of Materials Science, Faculty of Science, National University of Singapore. Received 9 September 1999; revised 5 November 1999.

[7] PRAKASH, P.; AKASH, Ravi; KAILASHNATH, N. Prediction of reduced glass transition temperature using machine learning. In: DEPARTMENT OF COMPUTER SCIENCE AND ENGINEERING, Amrita School of Engineering, Coimbatore, Amrita Vishwa Vidyapeetham, India.
