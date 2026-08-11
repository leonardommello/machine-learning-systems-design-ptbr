# Introdução

Esta parte contém 27 questões abertas que testam sua capacidade de reunir o que você aprendeu para projetar sistemas que resolvam problemas práticos. O entrevistador apresenta um problema, possivelmente relacionado aos produtos da empresa, e pede que você projete um sistema de aprendizado de máquina para resolvê-lo. Esse tipo de questão ficou tão popular que é quase garantido que você receba pelo menos uma durante seu processo de entrevistas. Em uma entrevista de uma hora, talvez dê tempo de cobrir só uma ou duas questões.

Essas questões não têm resposta única correta, embora existam respostas consideradas corretas. Há muitas maneiras de resolver um problema, e há muitas perguntas de acompanhamento que o entrevistador pode fazer para avaliar o conhecimento, a capacidade de implementação e o pensamento crítico do candidato. Os entrevistadores costumam concordar que, mesmo que você não chegue a uma solução funcional, basta comunicar seu processo de raciocínio de modo a mostrar que você entende as diferentes restrições, os compromissos e as preocupações do seu sistema.

Esse é o tipo de questão que os candidatos frequentemente amam e odeiam ao mesmo tempo. Os candidatos amam essas questões porque são divertidas, práticas, flexíveis e exigem o mínimo de memorização. Os candidatos odeiam essas questões por vários motivos.

Primeiro, faltam critérios de avaliação. É frustrante para o candidato quando o entrevistador faz uma pergunta aberta mas espera apenas uma resposta certa: a resposta que ele conhece. É difícil chegar a uma solução perfeita na hora, e o candidato pode precisar de ajuda para superar obstáculos. No entanto, muitos entrevistadores descartam rapidamente soluções ainda pela metade porque não enxergam aonde elas vão dar.

Segundo, essas questões são ambíguas. Não existe estrutura típica para essas entrevistas. Cada entrevista começa com uma tarefa propositalmente vaga: projete X. Cabe a você, como candidato, pedir esclarecimentos e delimitar o problema. Você conduz a entrevista e escolhe em que focar. Aquilo que você escolhe focar diz muito sobre seu interesse, sua experiência e seu entendimento do problema.

Muitos candidatos nem sabem como é uma boa resposta. Isso não se ensina na faculdade. Se você nunca implantou um sistema de aprendizado de máquina para usuários, talvez nem saiba com o que precisa se preocupar ao projetar um sistema.

Quando perguntei no Twitter o que os entrevistadores procuram nesse tipo de questão, recebi respostas variadas. [Dmitry Kislyuk](https://twitter.com/dkislyuk/status/1152246124960350208?s=20), gerente de engenharia de visão computacional no Pinterest, se interessa mais pelas partes que não envolvem modelagem:

"*A maioria dos candidatos conhece as classes de modelos (lineares, árvores de decisão, LSTM, redes neurais convolucionais) e memoriza as informações relevantes, então, para mim, as partes interessantes das entrevistas de sistemas de aprendizado de máquina são limpeza de dados, preparação de dados, registro de logs, métricas de avaliação, inferência escalável e repositórios de atributos (recomendação/ordenação).*"

[Ravi Ganti](https://twitter.com/gmravi2003/status/1152284255671599104?s=20), cientista de dados no WalmartLabs, procura a capacidade de dividir para conquistar:

"*Quando faço esse tipo de pergunta, é isto que procuro. 1. O candidato consegue decompor o problema aberto em componentes simples (blocos de construção)? 2. O candidato consegue identificar quais blocos exigem aprendizado de máquina e quais não exigem?*"

Na mesma linha, [Illia Polosukhin](https://twitter.com/ilblackdragon/status/1152648214203363330?s=20), cofundador da startup de blockchain NEAR Protocol e que antes passou pelo Google e pela MemSQL, procura as habilidades fundamentais de resolução de problemas:

"*Acho que esta [a de projeto de sistemas de aprendizado de máquina] é a pergunta mais importante. A pessoa consegue definir o problema, identificar métricas relevantes, imaginar fontes de dados e possíveis atributos importantes, entende a fundo o que o aprendizado de máquina pode fazer? Os métodos de aprendizado de máquina mudam todo ano; resolver problemas continua igual.*"

Este livro não tenta dar respostas perfeitas, elas não existem. Em vez disso, busca oferecer um arcabouço para abordar essas questões.

## Pesquisa versus produção

Para abordar essas questões, vamos primeiro examinar as diferenças fundamentais entre aprendizado de máquina no meio acadêmico e aprendizado de máquina em produção.

No meio acadêmico, as pessoas se importam mais com o treinamento; em produção, importam-se mais com o serviço de inferência. Candidatos que só estudaram aprendizado de máquina mas nunca implantaram um sistema no mundo real costumam cometer o erro de focar inteiramente no treinamento: fazer o modelo ir bem em alguma tarefa de benchmark sem pensar em como ele seria usado.

### Requisitos de desempenho
Na pesquisa em aprendizado de máquina, há uma obsessão por alcançar resultados de estado da arte (SOTA) em tarefas de benchmark. Para arrancar um pequeno ganho de desempenho, os pesquisadores muitas vezes recorrem a técnicas que tornam os modelos complexos demais para serem úteis.

Uma técnica frequentemente usada pelos vencedores de competições de aprendizado de máquina, inclusive o famoso Netflix Prize de US$ 1 milhão e muitas competições do Kaggle, é a [combinação de modelos](https://en.wikipedia.org/wiki/Ensemble_learning), ou *ensembling*: combinar "*múltiplos algoritmos de aprendizado para obter desempenho preditivo melhor do que o que se obteria com qualquer um dos algoritmos constituintes isoladamente.*" Embora possa render alguns pontos percentuais a mais de desempenho, a combinação de modelos torna seu sistema mais complexo, exige muito mais tempo de desenvolvimento e treinamento e custa mais caro.

Alguns pontos percentuais podem ser um grande feito em um placar, mas podem nem ser perceptíveis para os usuários. Do ponto de vista do usuário, um aplicativo com 95% de acurácia não é tão diferente de um aplicativo com 96% de acurácia.
<br><br><br><br>

------
__*Nota*__

Já se argumentou muitas vezes que competições no estilo placar, especialmente o Kaggle, não são aprendizado de máquina. Um argumento óbvio é que o Kaggle já faz por você boa parte das etapas necessárias ao aprendizado de máquina ([Machine learning isn't Kaggle competitions](https://jvns.ca/blog/2014/06/19/machine-learning-isnt-kaggle-competitions/), Julia Evans).

Um argumento menos óbvio, mas fascinante, é que, por causa do cenário de testes de hipóteses múltiplas que surge quando várias equipes testam no mesmo conjunto de teste reservado, um modelo pode superar os demais apenas por acaso ([AI competitions don't produce useful models](https://lukeoakdenrayner.wordpress.com/2019/09/19/ai-competitions-dont-produce-useful-models/), Luke Oakden-Rayner, 2019).

------

### Requisitos de computação
Na última década, os sistemas de aprendizado de máquina ficaram exponencialmente maiores, exigindo exponencialmente mais poder de computação e exponencialmente mais dados para treinar. Segundo a [OpenAI](https://openai.com/blog/ai-and-compute/), "*a quantidade de computação usada nas maiores execuções de treinamento de IA dobrou a cada 3,5 meses.*"

Do AlexNet em 2012 ao AlphaGo Zero em 2018, o poder de computação necessário aumentou 300.000 vezes. A busca de arquitetura que resultou nas AmoebaNets, da equipe de AutoML do Google, exigiu 450 GPUs K40 durante 7 dias ([Regularized Evolution for Image Classifier Architecture Search](https://arxiv.org/abs/1802.01548), Real et al., 2018). Em uma única GPU, teriam sido 9 anos.

<center>
<img
    alt="AI and Compute"
    src="ai_compute.png"
    style="float: center; max-width: 60%; margin: 0 0 1em 1em">
</center>

Esses modelos gigantescos rendem manchetes ideais, não produtos ideais. São caros demais para treinar, grandes demais para caber em dispositivos de consumo e lentos demais para serem úteis aos usuários. Quando converso com empresas que querem usar aprendizado de máquina em produção, muitas me dizem que querem fazer o que os principais laboratórios de pesquisa fazem, e eu preciso explicar a elas que não querem.

Há inegavelmente muito valor na pesquisa fundamental. Esses modelos grandes podem acabar sendo úteis conforme a comunidade descobre como torná-los menores e mais rápidos, ou podem servir como modelos pré-treinados sobre os quais se desenvolvem produtos de consumo. No entanto, os objetivos da pesquisa são muito diferentes dos objetivos da produção. Quando engenheiros pedem que você desenvolva sistemas para uso em produção, é preciso manter em mente os objetivos de produção.
