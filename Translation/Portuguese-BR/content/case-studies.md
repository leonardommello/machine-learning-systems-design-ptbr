# Estudos de caso

Para aprender a projetar sistemas de aprendizado de máquina, ajuda muito ler estudos de caso e ver como equipes reais lidam com diferentes requisitos e restrições de implantação. Muitas empresas, como Airbnb, Lyft, Uber e Netflix, mantêm excelentes blogs técnicos em que compartilham sua experiência usando aprendizado de máquina para melhorar produtos e/ou processos. Se você tem interesse em uma empresa, visite o blog técnico dela para ver no que anda trabalhando -- pode ser que apareça nas suas entrevistas! Abaixo estão alguns desses ótimos estudos de caso.

1. [Using Machine Learning to Predict Value of Homes On Airbnb](https://medium.com/airbnb-engineering/using-machine-learning-to-predict-value-of-homes-on-airbnb-9272d3d4739d) (Robert Chang, Airbnb Engineering & Data Science, 2017)
	
	Nesse post detalhado e bem escrito, Chang descreve como o Airbnb usou aprendizado de máquina para prever uma métrica de negócio importante: o valor dos imóveis no Airbnb. O texto percorre todo o fluxo de trabalho: engenharia de atributos, seleção de modelo, prototipagem e passagem dos protótipos para produção. Vem completo, com lições aprendidas, ferramentas usadas e trechos de código.

2. [Using Machine Learning to Improve Streaming Quality at Netflix](https://medium.com/netflix-techblog/using-machine-learning-to-improve-streaming-quality-at-netflix-9651263ef09f) (Chaitanya Ekanadham, Netflix Technology Blog, 2018)
	
	Em 2018, a Netflix transmitia para mais de 117 milhões de membros no mundo todo, metade deles fora dos Estados Unidos. Esse post descreve alguns dos desafios técnicos da empresa e como ela usa aprendizado de máquina para superá-los, incluindo prever a qualidade da rede, detectar anomalias em dispositivos e alocar recursos para cache preditivo.

3. [150 Successful Machine Learning Models: 6 Lessons Learned at Booking.com](https://blog.acolyer.org/2019/10/07/150-successful-machine-learning-models/) (Bernardi et al., KDD, 2019).
	
	Em 2019, a Booking.com tinha cerca de 150 modelos de aprendizado de máquina em produção. Esses modelos resolvem uma gama ampla de problemas de previsão (por exemplo, prever as preferências de viagem dos usuários e com quantas pessoas eles viajam) e de otimização (por exemplo, otimizar as imagens de fundo e as avaliações exibidas para cada usuário). Adrian Colyer fez um bom resumo das seis lições aprendidas:
	* Modelos aprendidos por máquina entregam forte valor de negócio.
	* Desempenho do modelo não é a mesma coisa que desempenho de negócio.
	* Seja claro sobre o problema que você está tentando resolver.
	* A latência do serviço de previsão importa.
	* Obtenha feedback cedo sobre a qualidade do modelo.
	* Teste o impacto de negócio dos seus modelos com ensaios controlados aleatorizados.

4. [How we grew from 0 to 4 million women on our fashion app, with a vertical machine learning approach](https://medium.com/hackernoon/how-we-grew-from-0-to-4-million-women-on-our-fashion-app-with-a-vertical-machine-learning-approach-f8b7fc0a89d7) (Gabriel Aldamiz, HackerNoon, 2018)
	
	Para oferecer conselhos automáticos de vestuário, a Chicisimo tentou qualificar o gosto de moda das pessoas usando aprendizado de máquina. Pela natureza ambígua da tarefa, os maiores desafios são formular o problema e coletar os dados para ele, e o artigo aborda os dois. Ele também trata do problema com que todo aplicativo de consumo se debate: a retenção de usuários.

5. [Machine Learning-Powered Search Ranking of Airbnb Experiences](https://medium.com/airbnb-engineering/machine-learning-powered-search-ranking-of-airbnb-experiences-110b4b1a0789) (Mihajlo Grbovic, Airbnb Engineering & Data Science, 2019)
	
	Esse artigo percorre passo a passo um exemplo canônico do problema de ordenação e recomendação. As quatro etapas principais são projeto do sistema, personalização, pontuação online e aspecto de negócio. O artigo explica quais atributos usar, como coletar e rotular dados, por que a equipe escolheu Gradient Boosted Decision Tree, quais métricas de teste usar, quais heurísticas levar em conta ao ordenar os resultados e como fazer teste A/B durante a implantação. Outra coisa admirável nesse post é que ele também cobre personalização para ordenar resultados de forma diferente para usuários diferentes. 

6. [From shallow to deep learning in fraud](https://eng.lyft.com/from-shallow-to-deep-learning-in-fraud-9dafcbcef743) (Hao Yi Ong, Lyft Engineering, 2018)
	
	A detecção de fraude é um dos casos de uso mais antigos de aprendizado de máquina na indústria. Esse artigo explora a evolução dos algoritmos de detecção de fraude usados na Lyft. No começo, um algoritmo tão simples quanto uma regressão logística com atributos construídos à mão bastava para pegar a maioria dos casos de fraude. Sua simplicidade permitiu à equipe entender a importância de cada atributo. Depois, quando as técnicas de fraude ficaram sofisticadas demais, passaram a ser necessários modelos mais complexos. Esse artigo explora o compromisso entre complexidade e interpretabilidade, desempenho e facilidade de implantação.

7. [Space, Time and Groceries](https://tech.instacart.com/space-time-and-groceries-a315925acf3a) (Jeremy Stanley, Tech at Instacart, 2017)
	
	A Instacart usa aprendizado de máquina para resolver a tarefa de otimização de rotas: como atribuir tarefas a vários compradores da forma mais eficiente e encontrar os caminhos ótimos para eles.  O artigo explica todo o processo de projeto do sistema, da formulação do problema à coleta de dados e à seleção de algoritmo e métrica, coroado com um tutorial de visualização caprichada.

8. [Uber's Big Data Platform: 100+ Petabytes with Minute Latency](https://eng.uber.com/uber-big-data-platform/) (Reza Shiftehfar, Uber Engineering, 2018)
	
	Com dados massivos vêm requisitos massivos de engenharia. Apoiando-se fortemente em dados para tomar decisões, "da previsão da demanda de passageiros em eventos de tráfego intenso à identificação e ao tratamento de gargalos no processo de cadastro de motoristas parceiros", a Uber acumulou "mais de 100 petabytes de dados que precisam ser limpos, armazenados e servidos com latência mínima". Esse artigo foca a evolução do data warehouse analítico da Uber, do Vertica ao Hadoop até a biblioteca Spark própria deles, o Hudi, com as limitações de cada etapa analisadas e resolvidas.

9. [Creating a Modern OCR Pipeline Using Computer Vision and Deep Learning](https://blogs.dropbox.com/tech/2017/04/creating-a-modern-ocr-pipeline-using-computer-vision-and-deep-learning/) (Brad Neuberg, Dropbox Engineering, 2017)
	
	Uma aplicação tão simples quanto um digitalizador de documentos tem dois componentes distintos: reconhecimento óptico de caracteres e detector de palavras. Cada um exige seu próprio pipeline de produção, e o sistema de ponta a ponta exige etapas adicionais de treinamento e ajuste. Esse artigo também detalha o esforço da equipe para coletar dados, que incluiu construir a própria plataforma de anotação.

10. [Scaling Machine Learning at Uber with Michelangelo](https://eng.uber.com/scaling-michelangelo/) (Jeremy Hermann e Mike Del Balso, Uber Engineering, 2019)
	
	A Uber usa aprendizado de máquina de forma extensiva em produção, e esse artigo oferece um panorama impressionante do fluxo de trabalho de ponta a ponta, de onde o aprendizado de máquina é aplicado na Uber e de como as equipes são organizadas.
	
11. [Deep Learning for Recommender Systems](https://bit.ly/2XXLEDV) (Justin Basilico, Research/Engineering at Netflix, 2018)
	
	As recomendações geram mais de US$ 1 bilhão de receita anual para a Netflix. O prazer de gastar alguns segundos para achar algo ótimo para assistir tem impacto direto na satisfação do cliente.	
	
12. [Making Netflix Machine Learning Algorithms Reliable](https://bit.ly/2ONtXmp) (Justin Basilico, Research/Engineering at Netflix, 2017) 

	A Netflix desenvolve uma variedade de algoritmos de aprendizado de máquina (incluindo regressão, fatoração, modelagem de tópicos, combinação de modelos, redes neurais, bandits etc.) para uma variedade de problemas (ordenação personalizada, em alta agora, similaridade entre vídeos, busca, ordenação dos top-n etc.), para ajudar os membros a encontrar conteúdo para assistir e aproveitar.


