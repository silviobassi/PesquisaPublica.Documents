# SISTEMA DE PESQUISA PÚBLICA

## Implementação dos Componentes 

Conferir em 👇🏻

- [x] [Web Application](https://github.com/silviobassi/PesquisaPublica.WebApplication)
- [x] [Serviço de Coleta](https://github.com/silviobassi/PesquisaPublica.ServicoColeta)
- [x] [Serviço de Processamento](https://github.com/silviobassi/PesquisaPublica.ServicoProcessamento)
- [x] [Componentes Compartilhados](https://github.com/silviobassi/PesquisaPublicaShared)

## Solução Proposta

Por questões contratuais, um dos pré-requisitos para a construção da solução é que ela seja feita utilizando os componentes do .NET framework.
O sistema de questionários online terá como finalidade principal a elaboração de pesquisas públicas. Um dos alvos da startup é pesquisa pública sobre as eleições, onde seriam feitos anúncios em diversas redes sociais convidando as pessoas a responderem a pesquisa. O questionário teria uma estrutura simples de perguntas com resposta no modelo múltipla escolha. Como o alvo das pesquisas são milhões de pessoas, é preciso se preocupar com questões de escala também. Depois do período de coleta de respostas, o sistema deve disponibilizar de forma sumarizada, para alguns usuários, o resultado da pesquisa.

## Requisitos Funcionais

1. **Elaboração de questionários online:** O sistema deve permitir o gerenciamento de questionários com perguntas de múltipla escolha.
2. **Coleta de respostas:** O sistema deve permitir que os usuários preencham os questionários online.
3. **Anúncios para engajamento:** Deve ser possível integrar campanhas de divulgação em redes sociais para atrair participantes.
4. **Disponibilização de resultados:** Após o período de coleta, o sistema deve fornecer os resultados das pesquisas de forma sumarizada para usuários específicos.

## Requisitos Não Funcionais

1. **Conformidade tecnológica:** A solução deve ser desenvolvida usando o .NET Framework, devido a restrições contratuais.
2. **Escalabilidade:** O sistema deve suportar um grande volume de acessos simultâneos, considerando o alcance dos links que serão publicados e que devem alcançar milhões de pessoas.
3. **Prazo crítico:** O projeto deve ser entregue antes das eleições, sob risco de comprometer o negócio da startup.
4. **Desempenho:** O sistema deve apresentar respostas rápidas mesmo sob alta carga.
5. **Facilidade de uso:** A interface deve ser simples e intuitiva para desenvolvedores (gestão de questionários) e participantes (resposta aos questionários).
6. **Manutenção e extensibilidade:** A arquitetura deve facilitar ajustes e expansões futuras, garantindo a evolução do sistema.
7. **Segurança:** O sistema deve proteger os dados de pesquisa, evitando vazamentos e acessos não autorizados.

## Arquitetura do Sistema

<img src="C4Architecture\Images\C1Context.png">

### Container Diagram - C2

<img src="C4Architecture\Images\C2Container.png">

### Component Diagram - C3

#### 1. Fluxo para respostas de questionários
<img src="C4Architecture\Images\C3PaginaResposta.png">

#### 2. Fluxo para o processamento das respostas
<img src="C4Architecture\Images\C3ServicoProcessamento.png">

#### 3. Fluxo para a criação de questionários
<img src="C4Architecture\Images\C3PaginaCriacaoPesquisa.png">

#### 4. Fluxo para a visualização dos resultados
<img src="C4Architecture\Images\C3PaginaResultado.png">

## Justificativa dos Componentes da Arquitetura

### 1. Cloudflare

<p>Inclui funcionalidades avançadas de segurança, essenciais para atender às demandas da arquitetura, especialmente por se tratar de pesquisas públicas fortemente regulamentadas por legislações que priorizam a proteção dos dados. Isso é crucial, considerando a sensibilidade das informações e o fervor típico do debate público. </p>
<p>Como a escalabilidade da aplicação é um fator crítico, principalmente na fase da coleta das respostas ao questionário, onde o tráfego poderá atingir picos elevados. A Cloudflare pode gerenciar o aumento de tráfego redirecionado às solicitações entre seus servidores, evitando sobrecargas em uma única região. Além disso, seu sistema de cache para conteúdos estáticos reduz significativamente a carga nos servidores de origem, mesmo durante picos de tráfego intenso.</p>
<p>A Cloudflare é uma ótima escolha, pois os conteúdos que serão servidos ao público são estáticos e não sofrerão alterações. Desta forma, a ida ao servidor pode ser minimizada mais amplamente por meio de configurações no cache. Como os questionários terão um intervalo determinado para serem respondidos, pode-se configurar o TTL (Time-to-Live), para vários dias ou do tempo de vida útil do questionário. Desta forma, o conteúdo permanecerá disponível sem a necessidade de ir ao servidor de origem.</p>
<p>Poderia, também, considerar a utilização de um banco de dados como o Redis para esta aplicação, no entanto, pelo requisito abordado, entende-se que não faz sentido a adoção deste componente. Todas as respostas dos questionários, relacionadas ao período de determinada pesquisa, tem que estar armazenadas no banco de dados. Somente após essa fase, os resultados poderão ser consultados.O banco de dados demora para sofrer alteração do seu estado, por conta do período de coleta de cada pesquisa. </p>
<p>Assim, somente o cloudflare é necessário como ferramenta de cache.  O redis seria útil se os dados sofressem constante variação, assim a cloudflare seria dispensada, pois não faz sentido utilizar a cloudflare para ir constantemente ao servidor.</p>

### 2. Web Application com Blazor Web Server

<p>O Blazor Web Server oferece um carregamento inicial muito rápido. Após o carregamento inicial, o Blazor pode enfrentar desafios de escalabilidade, especialmente com muitas interações simultâneas. Como mencionado anteriormente, a nossa aplicação tem um requisito crucial: o questionário a ser respondido pode sofrer picos elevados de acessos. Assim, o desempenho se torna um fator crítico e deve ser cuidadosamente considerado. Apesar disto, com a adoção do Cloudflare, que atua como uma camada de cache e distribuição de conteúdo, esses desafios são minimizados, garantindo que o tráfego seja gerido de forma eficiente sem sobrecarregar o servidor de origem.</p>
<p>Conforme o requisito do sistema, o questionário será amplamente divulgado em redes sociais, com o objetivo de atingir milhões de pessoas. Nesse contexto, campanhas publicitárias e tráfego pago serão necessários para aumentar o alcance da pesquisa. Por isso, a renderização do lado do servidor é essencial, pois possibilita práticas de SEO (Search Engine Optimization), tornando as páginas indexáveis pelos mecanismos de busca e, assim, melhor posicionadas, o que contribui para um alcance maior e mais visibilidade nas pesquisas.</p>

### 3. Serviço de Coleta e Serviço de Processamento com Aspnet WebApi MVC

<p>Uma abordagem com Aspnet Web Application poderia ter sido considerada, caso o requisito não envolvesse a evolução contínua da arquitetura. No entanto, a modularização da arquitetura é fundamental para permitir uma evolução sustentável e sem retrabalhos dispendiosos, facilitando o desenvolvimento modular e, consequentemente, ágil. Além disso, a arquitetura MVC organiza o código de forma clara e escalável, o que contribui para a manutenção e evolução contínua do sistema. Pois, ao separar o front-end e o back-end, adotando uma API, é possível escalar cada módulo de forma independente, configurando-os conforme as necessidades específicas de cada ambiente. Assim, a escala da aplicação se torna mais eficiente e flexível, atendendo aos requisitos de crescimento de forma otimizada.</p>
<p>Ao combinar essa tecnologia com a infraestrutura robusta da Azure e a performance do Cloudflare para o Web Application com Blazor Web Server, o sistema pode lidar com aumentos significativos de tráfego sem comprometer seu desempenho. Logo, o sistema de coleta permite a configuração de escalabilidade horizontal distribuindo cargas entre múltiplas instâncias em contêineres orquestrados pelo kubernetes por meio de um Load Balancer (Balanceador de Carga), para direcionar o tráfego de forma eficiente entre os servidores. Assim esta configuração deverá ser dinâmica através do auto-scaling do kubernetes.</p>

### 4. Azure Service Bus

<p>Componente cloud robusto, altamente disponível e possui integração nativa com aplicações .net. Um canal de recebimento e envio para as respostas dos questionários que, dada a sua natureza assíncrona, garante que os dados sejam processados sem sobrecarregar o sistema. Possui configurações disponíveis para lhe dar com picos de tráfego e evitar perda de mensagens. Neste tipo de aplicação, os dados são sensíveis, registrados em órgãos públicos e altamente acoplados à legislação em vigor, portanto, o gerenciamento dessas mensagens para serem mantidas é imprescindível para a natureza do negócio. O Azure Service Bus possui configurações que se ajustam à demanda delicada do requisito proposto:</p>

- **Dead-letter queue:** Mensagens que não foram processadas após um número de tentativas configurado são movidas para uma fila de mensagens mortas, onde podem ser analisadas e tratadas posteriormente.
- **Processamento Transacional:** As mensagens devem ser garantidas no final do ciclo do processamento para atender à sensibilidade e importância das informações, como já descrito;
- **Detecção de Duplicidades:** As respostas aos questionários devem ser únicas a cada usuário devidamente registrado;
- **Hub de Eventos:** _O Event Bus_ desacopla os produtores dos consumidores de eventos, permitindo que eles operem de forma independente. Ideal para esta arquitetura, pois na aplicação o serviço de coleta é o publicador dos eventos de respostas dos questionários e por ser prioritário ao requisito  será o primeiro a ser implantado, pois o prazo é curto. O serviço de processamento poderá ser implantado até o término da coleta da pesquisa eleitoral, desta forma poderá consumir as mensagens em sua própria velocidade, garantindo que nenhum dado seja perdido.

### 5. MongoDB

<p>A natureza schema-less (menos esquema), ao contrário dos bancos de dados relacionais, pode reduzir a manutenção e modificações quando novos tipos de dados forem introduzidos, visto que, segundo o requisito, o sistema não se restringe apenas às pesquisas eleitorais. As pesquisas podem ter naturezas relativamente distintas, apesar de o questionário ter a mesma estrutura para todas as pesquisas. Dependendo da pesquisa, e considerando fatores como a volatilidade e a categorização da legislação para pesquisas, alguns dados podem ser necessários, outros não, como o formato de identificação, dados de respondedores, etc. Assim, novos tipos de pesquisa ou modificações nas mensagens podem ser facilmente incorporados sem muito retrabalho ao pensarmos na flexibilidade do MongoDB.</p>
<p>Nesta arquitetura, os usuários (Analista e Administrador) não acessarão o sistema intensamente. No caso do analista, conforme o requisito, alguns usuários acessarão o sistema para analisar os resultados das pesquisas. Quando ao administrador, este deve acessar o sistema apenas para gerenciar pesquisas. Desta forma, não há necessidade, ao menos neste momento, de performar o MongoDB.</p>
<p>Apesar do grande volume de dados a serem recebidos dos eventos com as respostas da pesquisa, no que concerne o  armazenamento, o Azure Service Bus pode ser configurado para gerenciar o recebimento desses eventos pelo serviço de processamento a fim de minimizar os recursos do MongoDB referentes ao aumento de escala e desempenho. Ainda, como já descrito detalhadamente neste documento, no item 1, não haverá muitos acessos ao servidor, pois tanto analistas como respondedores, serão servidos dos dados por páginas estáticas com os dados cacheados nos servidores da cloudflare. No entanto, isto não descarta a importância de alta disponibilidade, pois um servidor pode falhar e os dados não podem ser perdidos, pois isso colocaria em dúvida a seriedade e integridade da startup. Posto isto, o MongoDB fornece suporte nativo a réplicas (replica sets) garantindo:</p>

- Disponibilidade mesmo em caso de falhas no servidor principal;
- Proteção contra perda de dados em um ambiente distribuído.

### DESCRIÇÃO DOS TESTES DE CARGA DO SERVIÇO DE COLETA EM AMBIENTE DE DESENVOLVIMENTO

###  Objetivo

O objetivo deste teste de carga é avaliar o desempenho do serviço de coleta de respostas dos questionários, crítico para este sistema, garantindo que o sistema seja capaz de lidar com um grande volume de acessos simultâneos, conforme os requisitos não funcionais estabelecidos. Vale ressaltar que este teste visa validar a arquitetura proposta e que para obter uma melhor acurácia os testes deverão ser repetidos em ambiente de **homologação**.

1. **Segundo o requisito, o link será disponibilizado nas redes sociais para milhões de pessoas. Desta forma, devemos considerar alguns fatores, considerando horários em que parte da população está desocupada, portanto mais conectados:**

- O tráfego será mais intenso durante a semana das 19h00 e 23h00;
- Aos fins de semana: sábado após o almoço (~15h às 17h) e domingo entre 12h e 16h ;
- Como o alcance total da campanha são milhões de pessoas. Vamos utilizar como referência inicial um total de 1 milhão de pessoas que , de fato, espero que responderão a pesquisa. Este valor pode ser ajustado mais tarde por ferramentas de monitoramento quando o sistema estiver em produção;

2. **Ao considerar o número de acessos durante o pico (19h~23h e fins de semana):**

- O período de pico é de aproximadamente 4 horas = 240 minutos.
- Supondo que 50% do tráfego total ocorra nesses horários, temos 500 mil acessos concentrados em 240 minutos.

**Assim temos aproximadamente um total de:**

Acessos por minuto = 500.000 / 240 ≈ 2.083 acessos por minuto.

3. **Resumo**

- Acessos por minuto durante o pico, sem considerar usuários simultâneos ~ 2000 a 2100 acessos/minuto;

4. **Avaliando Resultados do Teste de Carga**

Para avaliar o comportamento do serviço de coleta no período de pico, foi utilizada uma amostra de 6700 usuários simultâneos num período de 8 minutos, onde cada usuário fez 2 requisições. Neste cenário não há nenhuma falha na requisição. veja a imagem a seguir:

<img src="C4Architecture\Images\TesteCarga.png">

Assim foi utilizada a seguinte fórmula: número de usuários simultâneos / 8, desta forma obteve-se o seguinte resultado:
- **6700 / 8 = 837,5** acessos por minuto

Desta forma, ao multiplicarmos este resultado pelo total de minutos contidos em 4h chegamos ao resultado:
- **837,5 x 240 = 201.000** acessos simultâneos para uma instância do **Serviço de Coleta**.

<p>Como descrito anteriormente, o número de acessos simultâneos no pico é de 540.000. Portanto, neste cenário será utilizado o auto-scaling do kubernetes, configurando-o para suportar ao menos 6 instâncias direcionadas por um Load Balancer e configurações de monitoramento com alertas para tomada de decisões. Com isso, podemos garantir alta disponibilidade ao serviço de coleta de dados, pois este é o componente mais crítico e importante para o negócio.</p>
<p>Quanto ao serviço de processamento os testes serão executados quando o mesmo for implementado, pois as respostas dos questionários, não precisarão ser processadas imediatamente, visto que o requisito para a análise dos resultados da pesquisa poderá ser disponibilizado pelo serviço de processamento após o término da coleta de respostas publicadas no “Azure Service Bus”. Desta forma, considerando o prazo apertado para implementação do sistema, este já será funcional, apenas, com a implementação do frontend (Web Application Server), o backend (Serviço de Coleta) e a integração com o canal de distribuição de mensagens (Azure Service Bus), possibilitando um deploy ao que  é necessário no momento.</p>

![GitHub](https://img.shields.io/badge/GitHub-Pesquisa%20Publica-blue?logo=github)
![Status](https://img.shields.io/badge/Status-Projeto%20Desenvolvimento-yellow)
