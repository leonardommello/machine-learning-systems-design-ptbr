# Projetar um sistema de aprendizado de máquina

Projetar um sistema de aprendizado de máquina é um processo iterativo. Em geral, o processo tem quatro componentes principais: definição do projeto, pipeline de dados, modelagem (selecionar, treinar e depurar seu modelo) e serviço de inferência (testar, implantar, manter).

A saída de uma etapa pode ser usada para atualizar as etapas anteriores. Alguns cenários:
* Depois de examinar os dados disponíveis, você percebe que é impossível obter os dados necessários para resolver o problema que havia definido, então precisa formular o problema de outra forma.
* Depois do treinamento, você percebe que precisa de mais dados ou que precisa rotular os dados de novo.
* Depois de servir seu modelo aos primeiros usuários, você percebe que a forma como eles usam seu produto é muito diferente das suposições que você fez ao treinar o modelo, então precisa atualizá-lo.

Quando lhe pedirem para projetar um sistema de aprendizado de máquina, você precisa considerar todos esses componentes.

<center>
<img
    alt="Machine learning project flow"
    src="ml_project_flow.png"
    style="float: center; max-width: 45%; margin: 0 0 1em 1em">
</center>

## Definição do projeto

Antes mesmo de dizer "rede neural", você deve primeiro levantar o máximo de detalhes possível sobre o problema.

- **Objetivos**: O que você quer alcançar com este problema? Por exemplo, se lhe pedirem para criar um sistema que ordene quais atividades mostrar primeiro no feed de notícias de alguém no Facebook, alguns objetivos possíveis são: minimizar a disseminação de desinformação, maximizar a receita de conteúdo patrocinado ou maximizar o engajamento dos usuários.
- **Experiência do usuário**: Peça ao entrevistador um passo a passo de como os usuários finais devem usar o sistema. Se lhe pedirem para prever qual aplicativo o usuário do telefone quer usar em seguida, talvez você queira saber quando e como as previsões são usadas. Você mostra previsões apenas quando o usuário desbloqueia o telefone ou durante todo o tempo em que ele está com o aparelho?
- **Restrições de desempenho**: Quão rápida e quão boa a previsão precisa ser? O que é mais importante: precisão ou revocação? O que sai mais caro: falso negativo ou falso positivo? Por exemplo, se você constrói um sistema para prever se alguém é vulnerável a certos problemas médicos, seu sistema não pode ter falsos negativos. Já se você constrói um sistema para prever qual palavra o usuário vai digitar em seguida no telefone, ele não precisa ser perfeito para gerar valor.
- **Avaliação**: Como você avaliaria o desempenho do seu sistema, tanto durante o treinamento quanto durante a inferência? Durante a inferência, o desempenho de um sistema pode ser inferido pelas reações dos usuários, por exemplo, quantas vezes eles escolhem as sugestões do sistema. Se essa métrica não é diferenciável, você precisa de outra métrica para usar durante o treinamento, por exemplo, a função de perda a otimizar. A avaliação pode ser muito difícil para modelos generativos. Por exemplo, se lhe pedirem para construir um sistema de diálogo, como você avalia as respostas do seu sistema?
- **Personalização**: Quão personalizado seu modelo precisa ser? Você precisa de um modelo para todos os usuários, para um grupo de usuários ou para cada usuário individualmente? Se precisa de vários modelos, é possível treinar um modelo base com todos os dados e ajustá-lo finamente para cada grupo ou cada usuário?
- **Restrições do projeto**: São as restrições com que você precisa se preocupar no mundo real, mas menos durante as entrevistas: quanto tempo você tem até a implantação, quanto poder de computação está disponível, que tipo de talento trabalha no projeto, que sistemas já existentes podem ser usados etc.

*Recursos*

* Choosing the Right Metric for Evaluating Machine Learning Models, por Alvira Swalin, USF-Data Science, 2018. [Part I](https://medium.com/usf-msds/choosing-the-right-metric-for-machine-learning-models-part-1-a99d7d7414e4). [Part II](https://medium.com/usf-msds/choosing-the-right-metric-for-evaluating-machine-learning-models-part-2-86d5649a5428).

## Pipeline de dados

Na faculdade, você trabalha com conjuntos de dados disponíveis e limpos e pode gastar a maior parte do tempo construindo e treinando modelos de aprendizado de máquina. Na indústria, você provavelmente gasta a maior parte do tempo coletando, anotando e limpando dados. Quando eu dava aula, notei que muitos alunos fugiam do trabalho braçal com dados por considerá-lo sem graça, do mesmo jeito que um engenheiro de backend às vezes considera o frontend sem graça, mas a realidade é que os empregadores valorizam muito tanto a habilidade de frontend quanto a de lidar com dados.

Como o aprendizado de máquina é impulsionado mais por dados do que por algoritmos, para cada formulação do problema que você propuser, deve também dizer ao entrevistador que tipo de dado e quanto dado você precisa: tanto para treinar quanto para avaliar seus sistemas.

Você precisa especificar a entrada e a saída do seu sistema. Há muitas formas diferentes de formular um problema. Considere o problema de previsão de aplicativo mencionado acima. Uma configuração ingênua seria ter um perfil de usuário (idade, gênero, etnia, ocupação, renda, familiaridade com tecnologia etc.) e um perfil de ambiente (hora, localização, aplicativos usados anteriormente etc.) como entrada e produzir uma distribuição de probabilidade para cada aplicativo disponível. Essa é uma abordagem ruim, porque há aplicativos demais e, quando um novo aplicativo é adicionado, você precisa retreinar seu modelo. Uma abordagem melhor é ter o perfil do usuário, o ambiente e o perfil do aplicativo como entrada e produzir uma classificação binária: é uma combinação ou não.

Algumas das perguntas que você deve fazer ao entrevistador:

- **Disponibilidade e coleta de dados**: Que tipo de dado está disponível? Quantos dados você já tem? Eles estão anotados e, se sim, qual é a qualidade da anotação? Quanto custa anotar os dados? De quantos anotadores você precisa para cada amostra? Como resolver discordâncias entre anotadores? Qual é o orçamento de dados deles? Você consegue usar algum método fracamente supervisionado ou não supervisionado para criar automaticamente novos dados anotados a partir de uma pequena quantidade de dados anotados por humanos?
- **Dados dos usuários**: De que dados você precisa dos usuários? Como você os coleta? Como você obtém o feedback dos usuários sobre o sistema e, se quiser usar esse feedback para melhorar o sistema, faz isso online ou periodicamente?
- **Armazenamento**: Onde os dados estão armazenados hoje: na nuvem, localmente ou nos dispositivos dos usuários? Qual é o tamanho de cada amostra? Uma amostra cabe na memória? Que estruturas de dados você pretende usar e quais são os compromissos delas? Com que frequência chegam dados novos?
- **Pré-processamento e representação dos dados**: Como você processa os dados brutos até uma forma útil para seus modelos? Vai ser preciso fazer engenharia ou extração de atributos? É preciso normalizar? O que fazer com dados faltantes? Se houver desbalanceamento de classes nos dados, como você pretende tratá-lo? Como avaliar se seu conjunto de treino e seu conjunto de teste vêm da mesma distribuição, e o que fazer se não vierem? Se você tem dados de tipos diferentes, digamos textos, números e imagens, como pretende combiná-los?
- **Desafios**: Lidar com dados de usuários exige cuidado extra, como podem atestar as muitas empresas que se meteram em encrenca por tratá-los mal. 
- **Privacidade**: Que preocupações de privacidade os usuários têm sobre seus dados? Que métodos de anonimização você quer usar nesses dados? Você pode guardar os dados dos usuários de volta nos seus servidores ou só pode acessá-los nos dispositivos deles?
- **Vieses**: Que vieses podem estar representados nos dados? Como você corrigiria esses vieses? Seus dados e sua anotação são inclusivos? Seus dados vão reforçar vieses sociais atuais?

*Recursos*

* [More data usually beats better algorithms](https://anand.typepad.com/datawocky/2008/03/more-data-usual.html), por Anand Rajaraman, Datawocky, 2008.

## Modelagem

A modelagem, que inclui seleção de modelo, treinamento e depuração, é o que a maioria dos cursos de aprendizado de máquina costuma cobrir. No entanto, é apenas um pequeno componente de todo o processo. Alguns diriam até que é o componente mais fácil.

<center>
<figure>
<img
    alt="xkcd's modeling"
    src="modeling.png"
    style="float: center; max-width: 45%; margin: 0 0 1em 1em">
<figcaption>Fonte: xkcd</figcaption>
</figure>
</center>

### Seleção de modelo
A maioria dos problemas pode ser formulada como uma das tarefas comuns de aprendizado de máquina, então a familiaridade com essas tarefas e com as abordagens típicas para resolvê-las é muito útil. Você deve primeiro descobrir a categoria do problema. Ele é supervisionado ou não supervisionado? É regressão ou classificação? Exige geração ou apenas previsão? Se for geração, seus modelos terão de aprender o espaço latente dos seus dados, tarefa bem mais difícil do que apenas prever.

Note que esses "ou" não são mutuamente exclusivos. Uma tarefa de previsão de renda pode ser regressão se produzirmos números brutos, mas, se quantizarmos a renda em faixas e previrmos a faixa, ela vira um problema de classificação. Da mesma forma, você pode usar aprendizado não supervisionado para aprender rótulos para seus dados e depois usar esses rótulos em aprendizado supervisionado.

Então você pode formular a questão como uma tarefa específica: reconhecimento de objetos, classificação de textos, análise de séries temporais, sistemas de recomendação, redução de dimensionalidade etc. Tenha em mente que há muitas formas de formular um problema, e você pode não saber qual delas funciona melhor até ter tentado treinar alguns modelos.

Ao procurar uma solução, seu objetivo não é exibir seu conhecimento dos jargões mais recentes, mas usar a solução mais simples que dê conta do trabalho. A simplicidade serve a dois propósitos. Primeiro, acrescentar componentes mais complexos aos poucos facilita depurar passo a passo. Segundo, o modelo mais simples serve de linha de base com a qual você compara seus modelos mais complexos.

Estabelecer uma linha de base apropriada é uma etapa importante que muitos candidatos esquecem. Há três linhas de base diferentes em que você deve pensar:
* _Linha de base aleatória_: se seu modelo simplesmente prevê tudo ao acaso, qual é o desempenho esperado?
* _Linha de base humana_: quão bem os humanos se sairiam nessa tarefa?
* _Heurística simples_: por exemplo, para a tarefa de recomendar o próximo aplicativo a usar no telefone, o modelo mais simples seria recomendar o aplicativo que você mais usa. Se essa heurística simples acerta o próximo aplicativo 70% das vezes, qualquer modelo que você construir precisa superá-la de forma significativa para justificar a complexidade adicional. 

Seu primeiro passo diante de qualquer problema é encontrar as heurísticas eficazes dele. Martin Zinkevich, cientista pesquisador do Google, explicou em seu manual *[Rules of Machine Learning: Best Practices for ML Engineering](http://martin.zinkevich.org/rules_of_ml/rules_of_ml.pdf)* que "*se você acha que o aprendizado de máquina vai lhe dar um ganho de 100%, então uma heurística leva você a 50% do caminho.*" No entanto, resista à armadilha das heurísticas cada vez mais complexas. Se seu sistema tem mais de 100 if-else aninhados, é hora de mudar para aprendizado de máquina.

Ao considerar modelos de aprendizado de máquina, não esqueça que existem modelos que não são de aprendizado profundo. Modelos de aprendizado profundo costumam ser caros de treinar e difíceis de explicar. Na maior parte das vezes, em produção, eles só são úteis se seu desempenho for inquestionavelmente superior. Por exemplo, para a tarefa de classificação, antes de usar um modelo baseado em transformer com 300 milhões de parâmetros, veja se uma árvore de decisão resolve. Para detecção de fraude, antes de brandir redes neurais complexas, tente uma das muitas abordagens populares que não usam redes neurais, como o classificador de k vizinhos mais próximos.

A maioria dos problemas do mundo real talvez nem precise de aprendizado profundo. Aprendizado profundo precisa de dados e, para reunir dados, você talvez precise primeiro de usuários. Para escapar desse círculo vicioso, talvez você queira lançar seu produto sem aprendizado profundo, de modo a reunir dados de usuários para treinar seu sistema.

*Recursos*

* [Machine Learning Algorithms: Which One to Choose for Your Problem](https://blog.statsbot.co/machine-learning-algorithms-183cc73197c), por Daniil Korbut, Stats and Bots, 2017.

### Treinamento
Você deve ser capaz de antecipar que problemas podem surgir durante o treinamento e de resolvê-los. Alguns dos problemas comuns são: a perda de treinamento não diminui, sobreajuste, subajuste, valores de peso oscilantes, neurônios mortos etc. Esses problemas são abordados nas seções Regularização e técnicas de treinamento, Otimização e Ativações do Capítulo 9: Deep Learning.

#### Depuração
Você já viveu a euforia de ver seu modelo funcionar perfeitamente na primeira execução? Nem eu. Depurar um modelo de aprendizado de máquina é difícil, tão difícil que tirar sarro da nossa incompetência em depurar modelos de aprendizado de máquina virou esporte.

<center>
<figure>
<img
    alt="Debugging joke"
    src="debugging.png"
    style="float: center; max-width: 50%; margin: 0 0 1em 1em">
<figcaption>Erro de digitação: idpb deveria ser ipdb, a ferramenta interativa de depuração do Python</figcaption>
</figure>
</center>

Há muitas razões que podem levar um modelo a ter desempenho ruim:

- **Restrições teóricas**: por exemplo, suposições erradas, ajuste ruim entre modelo e dados.
- **Implementação ruim do modelo**: quanto mais componentes um modelo tem, mais coisas podem dar errado, e mais difícil fica descobrir qual delas deu.
- **Técnicas de treinamento esnobes**: por exemplo, chamar `model.train()` em vez de `model.eval()` durante a avaliação.
- **Escolha ruim de hiperparâmetros**: com a mesma implementação, um conjunto de hiperparâmetros pode dar o resultado de estado da arte enquanto outro conjunto pode nunca convergir.
- **Problemas nos dados**: entradas e rótulos desalinhados, dados pré-processados em excesso, dados ruidosos etc.

A maior parte dos bugs em aprendizado profundo é invisível. Seu código compila, a perda diminui, mas seu modelo não aprende nada ou talvez nunca alcance o desempenho que deveria. Ter um procedimento de depuração e a disciplina de seguir esse princípio é crucial para desenvolver, implementar e implantar modelos de aprendizado de máquina.

Durante as entrevistas, o entrevistador pode testar suas habilidades de depuração dando a você um trecho de código com bugs e pedindo que o conserte, ou perguntando que passos você tomaria para minimizar as oportunidades de bugs proliferarem. Infelizmente, ainda não existe uma abordagem científica para depuração em aprendizado de máquina. No entanto, engenheiros e pesquisadores experientes de aprendizado de máquina já publicaram uma série de técnicas de depuração testadas e aprovadas. Aqui estão alguns dos passos que você pode dar para garantir a correção do seu modelo.

1. Comece simples e acrescente componentes aos poucos

	Comece com o modelo mais simples e depois acrescente componentes devagar, para ver se ajudam ou prejudicam o desempenho. Por exemplo, se você quer construir uma rede neural recorrente (RNN), comece com apenas um nível de célula RNN antes de empilhar várias ou de acrescentar mais regularização. Se você quer usar um modelo do tipo BERT ([Devlin et al., 2018](https://arxiv.org/pdf/1810.04805.pdf)), que usa tanto modelo de linguagem mascarado (MLM) quanto perda de previsão da próxima frase (NSP), talvez seja melhor usar só a perda MLM antes de acrescentar a perda NSP.

	Hoje, muita gente começa clonando uma implementação de código aberto de um modelo de estado da arte e plugando os próprios dados. Se por acaso funcionar, ótimo. Mas, se não funcionar, fica muito difícil depurar o sistema, porque o problema pode ter sido causado por qualquer um dos muitos componentes do modelo.

1. Sobreajuste um único lote

	Depois de ter uma implementação simples do seu modelo, tente sobreajustar uma pequena quantidade de dados de treino e rodar a avaliação nesses mesmos dados, para garantir que a perda chegue ao menor valor possível. Se for reconhecimento de imagens, sobreajuste em 10 imagens e veja se consegue chegar a 100% de acurácia; se for tradução automática, sobreajuste em 100 pares de frases e veja se consegue chegar a um escore BLEU perto de 100. Se ele não consegue sobreajustar uma pequena quantidade de dados, há algo errado na sua implementação.

1. Fixe uma semente aleatória

	São tantos os fatores que contribuem para a aleatoriedade do seu modelo: inicialização de pesos, dropout, embaralhamento dos dados etc. A aleatoriedade dificulta comparar resultados entre experimentos diferentes -- você não tem como saber se a mudança de desempenho vem de uma mudança no modelo ou de uma semente aleatória diferente. Fixar uma semente aleatória garante consistência entre execuções. Também permite que você reproduza erros e que outras pessoas reproduzam seus resultados.

*Recursos*

* [Troubleshooting Deep Neural Networks: A Field Guide to Fixing Your Model](http://josh-tobin.com/assets/pdf/troubleshooting-deep-neural-networks-01-19.pdf). Josh Tobin, 2018.
* [Things I wish we had known before we started our first Machine Learning project](https://medium.com/infinity-aka-aseem/things-we-wish-we-had-known-before-we-started-our-first-machine-learning-project-336d1d6f2184). Aseem Bansal, towards-infinity, 2018.
* [How to unit test machine learning code](https://medium.com/@keeper6928/how-to-unit-test-machine-learning-code-57cf6fd81765), por Chase Roberts, 2017
* [A Recipe for Training Neural Networks](http://karpathy.github.io/2019/04/25/recipe/). Andrej Karpathy, 2019.
* [Practical Advice for Building Deep Neural Networks](https://pcc.cs.byu.edu/2017/10/02/practical-advice-for-building-deep-neural-networks/). Matt Holt e Daniel Ricks, BYU's Perception, Control and Cognition Laboratory, 2017.
* [Top 6 errors novice machine learning engineers make](https://medium.com/ai%C2%B3-theory-practice-business/top-6-errors-novice-machine-learning-engineers-make-e82273d394db). Christopher Dossman, AI³ | Theory, Practice, Business, 2017.

#### Ajuste de hiperparâmetros
Com conjuntos diferentes de hiperparâmetros, o mesmo modelo pode dar desempenhos drasticamente diferentes no mesmo conjunto de dados. Melis et al. mostraram, no artigo de 2018 *[On the State of the Art of Evaluation in Neural Language Models](https://arxiv.org/pdf/1707.05589.pdf)*, que modelos mais fracos com hiperparâmetros bem ajustados podem superar modelos mais fortes e mais recentes.

Apesar de reconhecerem sua importância, pessoas sem experiência prática costumam ignorar abordagens sistemáticas de ajuste de hiperparâmetros em favor de um método manual, guiado pelo instinto. O método mais popular talvez seja o Graduate Student Descent (GSD), técnica em que um estudante de pós-graduação fuça os hiperparâmetros até o modelo funcionar (GSD é uma técnica bem documentada, veja [aqui](https://www.reddit.com/r/MachineLearning/comments/6hso7g/d_how_do_people_come_up_with_all_these_crazy_deep/dj0tz1c/), [aqui](https://www.reddit.com/r/MachineLearning/duplicates/8yvlzy/d_debate_about_science_at_organizations_like/), [aqui](https://sciencedryad.wordpress.com/2014/01/25/grad-student-descent/) e [aqui](https://twitter.com/guyzys/status/592847074170896384?lang=en)).

Já se pesquisou muito sobre algoritmos de busca de hiperparâmetros, assim como sobre ferramentas que ajudam a buscar automaticamente um bom conjunto de hiperparâmetros. Vale a pena conhecer alguns dos métodos populares de ajuste de hiperparâmetros, entre eles busca aleatória, busca em grade e otimização bayesiana. O livro *AutoML: Methods, Systems, Challenges*, do grupo de AutoML da Universidade de Freiburg, dedica o primeiro capítulo à otimização de hiperparâmetros, e você pode lê-lo online gratuitamente [aqui](https://www.automl.org/wp-content/uploads/2018/09/chapter1-hpo.pdf).

O desempenho de cada conjunto de hiperparâmetros é avaliado no conjunto de validação. Tenha em mente que nem todos os hiperparâmetros nascem iguais. O desempenho de um modelo pode ser mais sensível à mudança de um hiperparâmetro específico, e também já se pesquisou como aferir a importância de diferentes hiperparâmetros.

#### Escalonamento
Como os modelos estão ficando maiores e mais intensivos em recursos, as empresas se importam muito mais com treinamento em escala. Isso normalmente não aparece na lista de requisitos, já que expertise em escalabilidade é difícil de adquirir sem acesso regular a recursos massivos de computação. Para vagas de engenharia de aprendizado de máquina, você ganha muitos pontos extras se conhecer os desafios e as soluções comuns de escalabilidade. Escalabilidade é um assunto elaborado, que merece um livro só seu. Esta seção cobre alguns problemas comuns, mas apenas arranha a superfície.

Não é raro treinar um modelo com um conjunto de dados que não cabe na memória principal. Isso é especialmente comum ao lidar com dados médicos, como tomografias computadorizadas ou sequências de genoma. Se você se deparar com uma situação dessas, precisa saber como pré-processar (por exemplo, centralizar em zero, normalizar, branquear), embaralhar e agrupar em lote seus dados quando eles não cabem na memória. Quando cada amostra dos seus dados é grande demais, seu modelo só consegue lidar com um tamanho de lote muito pequeno, o que pode levar à instabilidade da otimização baseada em gradiente descendente estocástico.

Em um caso muito raro, cada amostra é tão grande que nem uma única amostra cabe na memória, e você terá de usar técnicas como checkpointing de gradiente, técnica que explora o compromisso entre uso de memória e computação para fazer seu sistema computar mais e exigir menos memória. Você pode usar o pacote de código aberto [`gradient-checkpointing`](https://github.com/cybertronai/gradient-checkpointing), desenvolvido por Tim Salimans e Yaroslav Bulatov. Segundo os autores do pacote, "*para modelos feed-forward, conseguimos encaixar modelos mais de 10x maiores na nossa GPU, com aumento de apenas 20% no tempo de computação.*"

Já é quase a norma que engenheiros e pesquisadores de aprendizado de máquina treinem seus modelos em várias máquinas (CPUs, GPUs, TPUs). Os frameworks modernos de aprendizado de máquina facilitam o treinamento distribuído. O método de paralelização mais comum com vários nós de trabalho (workers) é o paralelismo de dados: você divide seus dados em várias máquinas, treina seu modelo em todas elas e acumula os gradientes. Isso dá origem a alguns problemas.

O problema mais desafiador é como acumular com precisão e eficácia os gradientes vindos de máquinas diferentes. Como cada máquina produz o próprio gradiente, se seu modelo espera que todas terminem uma execução -- técnica chamada gradiente descendente estocástico síncrono (SSGD) --, as máquinas retardatárias deixam o modelo inteiro mais lento.

No entanto, se seu modelo atualiza os pesos usando o gradiente de cada máquina separadamente -- isso se chama SGD assíncrono (ASGD) --, isso causa obsolescência de gradiente, porque os gradientes de uma máquina já alteraram os pesos antes de chegarem os gradientes de outra. Como mitigar a obsolescência de gradiente é uma área ativa de pesquisa.

Segundo, espalhar seu modelo por várias máquinas pode deixar seu tamanho de lote muito grande. Se uma máquina processa um lote de tamanho 128, então 128 máquinas processam um lote de tamanho 16.384. Se treinar uma época em uma máquina leva 100 mil passos, treinar em 128 máquinas leva menos de 800 passos. Uma abordagem intuitiva é escalar a taxa de aprendizado nas várias máquinas para dar conta de tanto aprendizado a cada passo, mas também não podemos deixar a taxa de aprendizado grande demais, pois isso leva a uma convergência instável.

Por último, mas não menos importante, com a mesma configuração de modelo, o worker mestre usa muito mais recursos que os demais. Para aproveitar ao máximo todas as máquinas, você precisa descobrir uma forma de equilibrar a carga de trabalho entre elas. A maneira mais fácil, embora não a mais eficaz, é usar um tamanho de lote menor no worker mestre e um tamanho de lote maior nos outros workers.

Com paralelismo de dados, cada worker tem sua própria cópia do modelo e faz toda a computação necessária para ele. Paralelismo de modelo é quando componentes diferentes do seu modelo podem ser avaliados em máquinas diferentes. Por exemplo, a máquina 0 cuida da computação das duas primeiras camadas enquanto a máquina 1 cuida das duas camadas seguintes, ou algumas máquinas cuidam da passagem para a frente enquanto várias outras cuidam da passagem para trás. Em teoria, nada impede que você use paralelismo de dados e paralelismo de modelo ao mesmo tempo. Na prática, porém, isso pode representar um desafio de engenharia enorme.

Uma abordagem de escalonamento que vem ganhando popularidade é reduzir a precisão durante o treinamento. Em vez de usar 32 bits completos para representar um número de ponto flutuante, você pode usar menos bits por número mantendo o poder preditivo do modelo. O artigo *[Mixed Precision Training](https://arxiv.org/abs/1710.03740)*, de Paulius Micikevicius et al., da NVIDIA, mostrou que, alternando entre precisão de ponto flutuante completa (32 bits) e metade da precisão de ponto flutuante (16 bits), conseguimos reduzir pela metade o uso de memória de um modelo, o que nos permite dobrar o tamanho do lote. Menos precisão também acelera a computação.

A maioria dos hardwares modernos para aprendizado profundo tira proveito de treinamento com precisão mista e/ou reduzida. GPUs NVIDIA mais recentes, como as das arquiteturas Volta e Turing, trazem Tensor Cores, unidades de processamento que suportam treinamento com precisão mista. [Comparados ao FP32 padrão na P100, os Tensor Cores oferecem até 12x mais TFLOPS de pico durante o treinamento e até 6x durante a inferência](https://devblogs.nvidia.com/mixed-precision-nlp-speech-openseq2seq/). As TPUs do Google também suportam treinamento com Bfloat16 (formato Brain Floating Point de 16 bits), que a empresa apelidou de "*[o segredo do alto desempenho nas Cloud TPUs.](https://cloud.google.com/blog/products/ai-machine-learning/bfloat16-the-secret-to-high-performance-on-cloud-tpus)*"

*Recursos*

* [Training Neural Nets on Larger Batches: Practical Tips for 1-GPU, Multi-GPU & Distributed setups](https://medium.com/huggingface/training-larger-batches-practical-tips-on-1-gpu-multi-gpu-distributed-setups-ec88c3e51255). Thomas Wolf. 2018.
* [Demystifying Parallel and Distributed Deep Learning: An In-Depth Concurrency Analysis](https://arxiv.org/pdf/1802.09941.pdf). Tal Ben-Nun e Torsten Hoefler. 2018.
* [A Guide to Scaling Machine Learning Models in Production](https://medium.com/hackernoon/a-guide-to-scaling-machine-learning-models-in-production-aa8831163846). Hamza Harkous, Hackernoon. 2017.
* [Scaling SGD Batch Size to 32K for ImageNet Training](https://www2.eecs.berkeley.edu/Pubs/TechRpts/2017/EECS-2017-156.pdf). Yang You, Igor Gitman e Boris Ginsburg. Berkeley EECS. 2018.

## Serviço de inferência
Antes de servir seus modelos treinados aos usuários, você precisa pensar nos experimentos que precisa executar para garantir que os modelos atendam a todas as restrições descritas na definição do problema. Você precisa pensar em que feedback gostaria de receber dos usuários, se vai permitir que eles sugiram previsões melhores e, a partir das reações deles, como decidir se seu modelo faz um bom trabalho.

Treinamento e serviço de inferência não são dois processos isolados. Seu modelo vai melhorar continuamente conforme você recebe mais feedback dos usuários. Você quer treinar seu modelo online a cada novo dado? Você precisa personalizar seu modelo para cada usuário? Com que frequência deve atualizar seu modelo de aprendizado de máquina?

Algumas mudanças no seu modelo exigem mais esforço que outras. Se você quer acrescentar mais amostras de treino, pode continuar treinando seu modelo atual com as novas amostras. Já se quer acrescentar uma nova classe de rótulo a um modelo de classificação neural, provavelmente terá de retreinar o sistema inteiro.

Se for um modelo de previsão, talvez você queira medir a confiança do modelo em cada previsão, para mostrar apenas as previsões de que ele está confiante. Talvez queira também pensar no que fazer em caso de baixa confiança -- por exemplo, encaminhar o usuário a um especialista humano ou coletar mais dados dele?

Você também deve pensar em como executar a inferência: no dispositivo do usuário ou no servidor, e nos compromissos entre as duas opções. Inferir no telefone do usuário consome memória e bateria do aparelho e dificulta a coleta de feedback. Inferir na nuvem aumenta a latência do produto, exige que você monte um servidor para processar todas as requisições dos usuários e pode afugentar usuários preocupados com privacidade.

E há a questão da interpretabilidade. Se seu modelo prevê que alguém não deve receber um empréstimo, essa pessoa merece saber o motivo. Você precisa considerar os compromissos entre desempenho e interpretabilidade. Tornar um modelo mais complexo pode aumentar seu desempenho, mas deixa os resultados mais difíceis de interpretar.

Para modelos complexos com muitos componentes diferentes, é especialmente importante conduzir estudos de ablação -- remover cada componente mantendo o restante --  para determinar a eficiência de cada um. Você pode descobrir componentes cuja remoção não reduz significativamente o desempenho do modelo, mas reduz significativamente sua complexidade.

Você também precisa pensar nos possíveis vieses e usos indevidos do seu modelo. Ele propaga algum viés de gênero ou racial vindo dos dados e, se sim, como você vai corrigi-lo? O que acontece se alguém com intenção maliciosa tiver acesso ao seu sistema?

Do lado da engenharia, há muitos desafios envolvidos em implantar um modelo de aprendizado de máquina. No entanto, a maioria das empresas provavelmente tem as próprias equipes de implantação, que sabem muito sobre implantação e menos sobre aprendizado de máquina.


------
__*Nota*__: As suposições que seu modelo faz

O estatístico George Box disse, em 1976, que "*todos os modelos estão errados, mas alguns são úteis.*" O mundo real é intratavelmente complexo, e os modelos só conseguem aproximá-lo usando suposições. Cada modelo vem com suas próprias suposições. É importante pensar em que suposições seu modelo faz e se nossos dados as satisfazem.

Abaixo estão algumas das suposições comuns. A lista não pretende ser exaustiva, é apenas uma demonstração.

* Suposição de previsão: todo modelo que busca prever uma saída Y a partir de uma entrada X supõe que é possível prever Y com base em X.
* IID: redes neurais supõem que os dados são independentes e identicamente distribuídos.
* Suavidade: todo método supervisionado de aprendizado de máquina supõe que existe um conjunto de funções capaz de transformar entradas em saídas de modo que entradas similares se transformem em saídas similares. Se uma entrada X produz uma saída Y, então uma entrada próxima de X produziria uma saída proporcionalmente próxima de Y.
* Tratabilidade: seja X a entrada e Z a representação latente de X. Todo modelo generativo supõe que é tratável computar a probabilidade P(Z | X).
* Fronteiras: um classificador linear supõe que as fronteiras de decisão são lineares.
* Independência condicional: um classificador Naive Bayes supõe que os valores dos atributos são independentes entre si, dada a classe.
Distribuição normal: muitos métodos estatísticos supõem que os dados são normalmente distribuídos.

------
<br>

------
__*Nota*__: Dicas de preparação

A lista de passos acima é longa e intimidadora. Pense em um projeto que você fez no passado e tente responder às perguntas a seguir.

* Como você coletou os dados? Como processou seus dados?
* Como você decidiu que modelos usar? Que modelos acabou testando? Quais foram melhores? Por quê? Alguma surpresa?
* Como você avaliou seus modelos?
* Se fizesse o projeto de novo, o que faria diferente?

------

*Recursos*

* [Rules of Machine Learning: Best Practices for ML Engineering](http://martin.zinkevich.org/rules_of_ml/rules_of_ml.pdf). Martin Zinkevich, 2017.
* [How to build scalable Machine Learning systems - Part II: Architecting a Machine Learning Pipeline](https://towardsdatascience.com/architecting-a-machine-learning-pipeline-a847f094d1c7). Semi Koen, Towards Data Science, 2017.
* [A Brief History of Machine Learning Models Explainability](https://medium.com/@Zelros/a-brief-history-of-machine-learning-models-explainability-f1c3301be9dc). Zelros AI, 2018.
* [The Malicious Use of Artificial Intelligence: Forecasting, Prevention, and Mitigation](https://img1.wsimg.com/blobby/go/3d82daa4-97fe-4096-9c6b-376b92c619de/downloads/MaliciousUseofAI.pdf). Miles Brundage et al., 2018.
* [Fairness in Machine Learning Engineering crash course](https://developers.google.com/machine-learning/crash-course/fairness/video-lecture). Google.
