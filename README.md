# Software Architecture: The Hard Parts | Leitura e Análise
![image](https://github.com/user-attachments/assets/a4c00792-3f35-4fa6-a464-14deb3f4425c)

## Descrição
Aqui coloco o resumo da minha leitura sobre o livro Software Architecture: The Hard Parts

## O que acontece quando não há melhores práticas?

### Dando conselhos atemporais sobre arquitetura de software
O autor inicia o texto, descrevendo o contexto antigo e novo de desenvolvimento de software.
Segundo ele, arquiteturas baseadas em microsserviço estão sendo preteridas no lugar de arquiteturas baseadas em serviços.

`NOTA: em 2023, as empresas começaram a realizar um movimento para a volta de arquiteturas monoliticas, o primeiro caso notável foi o Prime Vídeo da Amazon, vou deixar o link com um artigo escrito no Tab News.`

[Link do artigo no Tab News](https://www.tabnews.com.br/uriel/a-volta-dos-monolitos-adeus-microservicos-amazom-prime-video-90-por-cento-de-economia)

`NOTA: Apenas para entendimento, vou deixar uma imagem da "evolução" das arquiteturas.`

![image](https://github.com/user-attachments/assets/0bd4e922-ca47-45f4-bb64-0ccf5eba82ec)

É citado que, o contexto para essa revolução de microsserviços foi muito influênciado pela ascenção do código aberto, onde ferramentas como o Puppet e Chef tornou a infraestrutura mais automatizável.
Consequentemente, isso influênciou a criação de novas técnologias incríveis, como **Docker**, **Kubernets** e etc.

### A importância dos dados na arquitetura
O capítulo inicia ressaltando um ponto, em toda arquitetura, os dados são extremamente importante, independente de alterações, indo de correção de bugs, refatorações complexas até a reescrita completa do sistema, os dados de negócio precisam manter-se vivos.

Os dados gerados de um produto são de valor inestimável para o negócio, pois apenas apartir deles é possível tomar decisões mais acertivas para a evolução do negócio.

O autor cita que uma das maiores dificuldades na implementação de microsserviços foi a decentralização das informações em vários bancos de dados, tornando assim a coleta e análise das métricas um pouco mais complexas e um desafio a se resolver na época. 

#### Tipos de dados
**Dados transacionais:** São dados fundamentais para o funcionamento do negócio. Caso esses dados não sejam computados, a organização pode sofrer o risco de parar.

**Dados analiticos:** São dados usados para realizar previsões, análises de inteligência do negócio e etc.

### Regístros de decisão de arquitetura
Em arquitetura, é extremamente importante documentar as decisões tomadas, seus motivos, e suas consequências. Para realizar isso o autor indica o uso de **ADRs (Architectural Decision Records)**.

Esse tipo de documentação deve ser bem direto e normalmente escrito em markdown

exemplo:

```m̀arkdown
# ADR - [Título da Decisão]

## Contexto
Descreva o cenário que levou à tomada de decisão. Inclua detalhes do problema que precisa ser resolvido e quaisquer requisitos, restrições, ou limitações que influenciam essa decisão.

## Decisão
Declare a decisão que foi tomada. Seja específico sobre o que foi escolhido e como a decisão será implementada. Inclua detalhes sobre a abordagem, tecnologias envolvidas, ou padrões adotados.

## Alternativas Consideradas
Liste e descreva as alternativas que foram consideradas durante o processo de decisão. Inclua vantagens e desvantagens de cada alternativa.

1. **Alternativa 1**: [Descrição]
   - **Vantagens**: [Detalhe]
   - **Desvantagens**: [Detalhe]

2. **Alternativa 2**: [Descrição]
   - **Vantagens**: [Detalhe]
   - **Desvantagens**: [Detalhe]

## Consequências
Descreva as consequências da decisão tomada. Inclua impactos positivos e negativos, bem como possíveis riscos e como eles serão mitigados. Explique o que precisará ser feito para implementar essa decisão e o que será afetado por ela.

## Status
Indique o status da decisão: "Proposta", "Aceita", "Em andamento", "Implementada", "Rejeitada", etc.

## Data
Data em que a decisão foi tomada.

## Responsável
Nome do responsável pela decisão ou do time que a tomou.

## Anexos (Opcional)
Inclua qualquer informação adicional, como diagramas, referências a documentos externos, links para conversas, ou outras anotações que sejam relevantes para o entendimento completo da decisão.
```

`NOTA: Acredito que RFCs também podem auxiliar no processo de tamada das decisões`

### Fitness Functions de Arquiteturas
A definição de Fitness Functions é de que qualquer mecanismo usado para garantir a integridade de alguma característica de arquitetura.

É possível realizar testes de estrutura da arquitetura, esse teste é a nível de abstração do código. E também testes de arquitetura a nível operacional, onde já envolve quesitos como desempenho e escalabilidade.

Esses testes devem ser objetivos e mensuráveis, para que seja possível realizar automações para manter certos padrões de qualidade.

## Separando as coisas
O capítulo é introduzido com dois conceitos, **acoplamento estático**, e **acoplamento dinâmico**
- **Estático:** envolve dependências entre, classes, componentes e serviços são conectados.
- **Dinâmico:** envolve como os serviços se comunicam, quais informações são enviadas, o quão rígido é esse contrato de comunicação.

### Discernindo o acoplamento na Arquitetura de Software
Em arquitetura de software em geral, normalmente é dado que **acoplamento** é algo pejorativo, porém o autor diz que isso não é necessáriamente ruim, depende do nível de acoplamento. Sistemas extremamente desacoplados trazem outros tipos de problemas em transacionalidade, orquestração e assincrônicidade.

### Arquitetura Quantum
A definição formal de Quantum em arquiteturade software é: Um artefato independente implementavel, com alta coesão funcional, alto acoplamento estático, e acoplamento dinâmico sincrono.

Em arquiteturas monolíticas, o monolito seria **um quantum de arquitetura**, em casos de microsserviços, cada microsserviço seria **um quantum de arquitetura**.

#### Definindo alguns conceitos
- *Alta coesão funcional*: Tem uma fucionalidade bem definida
- *Forte acoplamento estático*: Significa que outros componentes do sistemas possuem uma depedência alta entre si, por exemplo, vários serviços dependendo de apenas um banco
- *Comunicação dinâmica síncrona*: Significa que a comunicação é direta, com respostas em tempo real. (Nisso se enquadra por exemplo, chamadas Http REST e Websocket).

```
NOTA:

No livro é dado vários outros exemplos com outros detalhes.

Um ponto importante é que o autor por várias vezes cita que, sistemas com alta coesão funcional
e com baixo acoplamento estático, normalmente é feito em microsserviços.

E para que os sistemas isolados sejam caracterizados como tal, não pode existir pontos de acoplamento em conjunto.

Exemplificando:
- Se você tem vários backends, e todos grudados no mesmo banco, NÃO É MICROSSERVIÇO.
- Se você tem vários backends, cada um com bases de dados diferentes, mas a interface de usuário(FRONTEND) é única, NÃO É MICROSSERVIÇO.
```


