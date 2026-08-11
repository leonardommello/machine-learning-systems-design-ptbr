# Machine Learning Systems Design

**Leia este booklet [aqui](https://huyenchip.com/machine-learning-systems-design/toc.html).**

>>Este booklet foi minha primeira tentativa de escrever sobre projeto de sistemas de aprendizado de máquina, lá em 2019. Meu entendimento do tema passou por iterações significativas desde então. Meu livro [Designing Machine Learning Systems](https://www.amazon.com/Designing-Machine-Learning-Systems-Production-Ready/dp/1098107969) (O'Reilly, junho de 2022) é bem mais completo e atual. [O repositório do novo livro](https://github.com/chiphuyen/dmls-book) contém o sumário completo, os resumos dos capítulos e reflexões diversas sobre ferramentas de MLOps.

Este booklet cobre quatro etapas principais do projeto de um sistema de aprendizado de máquina:

1. Definição do projeto
2. Pipeline de dados
3. Modelagem: seleção, treinamento e depuração do modelo
4. Serviço de inferência: teste, implantação e manutenção

Ele vem acompanhado de links para recursos práticos que explicam cada aspecto em mais detalhe. Também sugere estudos de caso escritos por engenheiros de aprendizado de máquina de grandes empresas de tecnologia que implantaram sistemas de aprendizado de máquina para resolver problemas do mundo real.

No fim, o booklet traz 27 questões abertas de projeto de sistemas de aprendizado de máquina que podem aparecer em entrevistas da área. As respostas dessas questões serão publicadas no livro **Machine Learning Interviews**. Você pode consultar as respostas da comunidade a essas questões, e contribuir com as suas, no GitHub [aqui](https://github.com/chiphuyen/machine-learning-systems-design/tree/master/answers). Leia mais sobre o livro e inscreva-se na lista de e-mails dele [aqui](https://huyenchip.com/2019/07/21/machine-learning-interviews.html).


## Contribuir
Este é um trabalho em andamento, então qualquer tipo de contribuição é muito bem-vinda. Veja algumas formas de contribuir:

1. Melhorar o texto corrigindo qualquer erro léxico, gramatical ou técnico
1. Acrescentar mais recursos relevantes a cada aspecto do fluxo de um projeto de aprendizado de máquina
1. Adicionar/editar questões
1. Adicionar/editar respostas
1. Outros

Este livro foi criado com o excelente pacote [`magicbook`](https://github.com/magicbookproject/magicbook). Para instruções detalhadas de uso do pacote, consulte o repositório dele no GitHub. O pacote exige que você tenha o `node`. No Mac, você instala o `node` assim:

```
brew install node
```

Instale o `magicbook` com:

```
npm install magicbook
```

Clone este repositório:

```
git clone https://github.com/chiphuyen/machine-learning-systems-design.git
cd machine-learning-systems-design
```

Depois de alterar o conteúdo da pasta `content`, você gera o booklet com os seguintes passos:

```
magicbook build
```

Os arquivos HTML e PDF gerados ficam na pasta `build`.

## Agradecimento

Quero agradecer a Ben Krause por ser um grande amigo e por me ajudar com este rascunho!


## Citação
