# DESCRIÇÃO ARQUITETURAL DO SISTEMA DE PESQUISA PÚBLICA

- `Authors`: Silvio Bassi
- `Description`: Contratos para integrações de mensagens entre serviços
- `RepositoryUrl`: [GitHub Repository](https://github.com/silviobassi?tab=repositories)

## Implementação dos Componentes 

Conferir em 👇🏻

- [x] [Web Application](https://github.com/silviobassi/PesquisaPublica.WebApplication)
- [x] [Serviço de Coleta](https://github.com/silviobassi/PesquisaPublica.ServicoColeta)
- [x] [Serviço de Processamento](https://github.com/silviobassi/PesquisaPublica.ServicoProcessamento)
- [x] [Componentes Compartilhados](https://github.com/silviobassi/PesquisaPublicaShared)

## Solução Proposta

Por questões contratuais, um dos pré-requisitos para a construção da solução é que ela seja feita utilizando os componentes do .NET _framework._
O sistema de questionários _online_ terá como finalidade principal a elaboração de pesquisas públicas. Um dos alvos da startup é pesquisa pública sobre as eleições, onde seriam feitos anúncios em diversas redes sociais convidando as pessoas para responderem à pesquisa. O questionário teria uma estrutura simples de perguntas com resposta no modelo múltipla escolha. Como o alvo das pesquisas são milhões de pessoas, é preciso se preocupar com questões de escala também. Depois do período de coleta de respostas, o sistema deve disponibilizar de forma sumarizada, para alguns usuários, o resultado da pesquisa.

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

### Context System Diagram - C1
![](http://www.plantuml.com/plantuml/png/hLF1JXin4BtdAqpK0vKQScXxgLG9246jL20Yq1xHP3r9HlBQYyS6ojzmwXVqmdL_h6EpPbbwwQ6dEEEPzzuylztd03x4senso5OcQbJR41h-D9rwkDtRKDZ6LMJqbRC1RTYhN3rj3DWqC-6W3Qscim-JHIfTddoRri01lPIkPcdYBkmr2Nsqet5D5jNH_FlNsTdfyXzeGcn0-_Sz7SdjP2qT4suy1UJ2fl4ctV4po_7PwSN1Z_dox6J-Nubo3MwHNOsJZyMp0TyqeNEtzKAEpkxcqZirlkJOFdXoF9O_1nKoGwsQzc535bW9ZaUE9e1sqYtdnbcDjKArGO-s8kc-ZiY1d7t6UVCayVCuaupVZfO_HMgzo_b7U9QK3f3W5yZNaHWIlRnOWBNpSjE0Xvv2N77IF6GIFPKp639CLiP19AC2kJV4g4Jp2_bAostJqScfVLmPgY3fwmHUpU_2RgMjI9aP5_NQWCSax4ZqUbf5KlcDsaVjb2Xf7m9LBdaXQgMkGF1zNi1McFcAaxq9jRCRfrU2Uf9EHuVPU1cvHmlAyQibY-VqzmQehBiPLB9hZ1xhVgnmb_taMfA9ahZ4UnyzgkLJIHt6d89ZCjq3DDxbH7W5t5kS_CvBoe6XSf9H3Sd5SpHNvxJPTYQMYCrjyBY1FbKUhKPFzpAM2RzSN2oM0Y3p9PTTL4ea-zdNAL0uU69yuGR76ZABumuyoUgXvxQ2ckmMdhPBKzJ-QdzZQI-TvSdwT-hDUDKwSFSoa15-jIw6Te7r2djh1r2ZVR4cVQP_0000)

### Container Diagram - C2
![](http://www.plantuml.com/plantuml/png/hLLDRzj64BthLqo476H0Zb2qlHGG45bMq1QLhPXASZI6t96yw79tixkq4nVzCJxrF_IgFzOPKgB8n0eAjBfekH_llNdpk7mT4uPKbMRmGjl2L8hWBYKVVvfC0ZwyskfqL-LLf50ucyYcLuKh9zwWbJFdCIcZyydyX_ELJBrR_ZOfCIOAF7KxvnEeBOLNNl07CwKMXae6MUDsD2nr4Ln6uLuND1p3otY7dgOBlRrBcLQaCdaUdV6AeIrPjQPFQTgSWjWSWn79TeYo_mn6ra7YNMFWGOx5xr0uuyBPy4ouRyZKlFkptmcdx9xBdkamaE9zWnUADgmPBXVlVvbVNsN_merKULJX-wChcbVFDxpZFFgW4yM3AOhkPIssB6-khzQp3uliUhduNudgENoWw4ew_x5jRPTl8kXntveL3vqTrLDZ6BwBrUufQ1U7_30hA4OimU-UjjfY1CO952kJKBaubh5tLb4915iAP0lDkpzM59DsjiLvsKYS3ciIiJhxp5hBsyMdD2gKPQQvSPNQ60mal9Swfg3pIaFjmUvlvO0nTq-9onOk3CZpWE0fR5meqHO42cEhb4dQ3BwjgAAQwn0UjbUgUwm2mJw6S57L9R_H1kL_5LnTF61ioeofgR-cuq74mdc32hjwJE8bBQReN1kjK56dt0jNMONXyoZMpyoIQHaqm2kA7oiTSNZsnm3ur-eVvGOVNU3j7oY7cVT65oW6GvRTYDQBUXraLQgX89ESRKhOrUxY5wq1WkWOJ2Vij9K5z-aVA4UlRuiQK4IBOxk_d8XkMEgiH7z5IKJCl8Rb-tdFHG9asnx9Yg7V52LvIRYDq_ujSKAKtnF8rUA-qBRghfsKo93ogdGr8MoqmR64JqpfcWEnAZ7eHnbtGWz-tpoM_xpwOnmlyn6KpcwTofb-AQFBYphrc337IBNKWrjV-NDuwRGeaCYtr41WtNrlncD02JsLnsDuwF0DcJPQ9-oSV-t0k4ywxZao7F-yNg-ooQ_PzTL9aZP82tkl4Lo_m4vzpwCzBxLrjBLkVEmE7Lj9PQVwlg3-xR2gSddFJee3syG4h6Hhjboz_RR47dmRkzFmQW-lcZmmFWl_Sp0OC45pQRRNGdPuYLUTUxeFJDqCAshxrmzq8AkeVi0ehBNzJ2kKpGUY9Tr_6y3_Dye6_FP6lkLDLGsFX2C5shO4fyKDNlE2VCh-0G00)

### Component Diagram - C3

#### 1. Fluxo para respostas dos questionários
![](http://www.plantuml.com/plantuml/png/dLN1RXit4BthArYr1mbmj4MGNWe4YAAeS0hBbhLASnH6oub4W4jkXgHRk-Z763tu7thLZtN8tLMbjIeOaG_cpdBU3DzxmttdF90FfUvzfqoXWqInzRvoFsSPmU-ZZVBRi0uEgR36e_6ZmfPPfS74d5VEIwtMsUJDgtaCVPfTPIKuZyIXrSIMbJKnfuhulR6K2zHBs0pwuEvDqRyGFsXbCFVt6iLRyG7S5kKLHmR3OQ-NNzvyNisdY_pcUdNpQNdryNewuF0SoLap87GCBb5QkX3znNzFVNwS4w8fjYZupzmf46cty-141GJ2Ygy1dLVMx1v9sVwmbzzpr-Lg-eSV5D8mn4JR8Bze88o07vJpfDP1YKJ3xXzf1GFi7hqgU2KsZCfn0Q92-cAf15EWaB7Uxd6Z33YkqPjmBYY3T1imO2ec7DATAf0fvZBZXq0eyZeatWSNQ_-YDDI7iWKw1mBSmNaaYbIF5muAoyf8E6n8Utwb8ZjghRII8F6ebTLx6um4kXzynlMughWGBmIlj2eWKYJoVD4VYZzxWdzxJPC0jmsBm2J63kkprXotaf2uFU8wgWKFKRNBvUpgGao-Zw6FnZDnK62TJ6roLwXE4o3Bqpr4NYQaOFUq-zlomxSqKN0-HIwHq1HnNQ7x6fIBQZvd8sZ__xqiqdkGrhsmjZKf8URIFbUuK3BsGrnp2t-Tr37QPs8rUc3OvANTKwAW3fwGCdgQabuk9KLGibeZnRHvM4Shx9biDwQJZFFvw7gw5CayIin-cyJer7aAFX28_UWrhk1_1t3FQ8pJqDGhm7RwFzj8Oh7jdEiqfptUrorNaPNJErxLuoM3j_MH6vrR4oi9_NOyHxCuXAphPjGCQZEdJNj7itbitqQp1UhZw-l4A8thKSToxxc6jmmrAcuJTFOJ_rx_-FgDI7w-N2xdURnIFMpSs-Q67JR5klZr7RT0xe3jb6GvcDtpSAk5scoRQ_Bu5fuo-RWvHAEsWdm9SjU8NJUqhDZJsTtjX-gUpppOUNGVDsZTxqLxR2KjAvISCRkTlvZxphHDpPqwvvf4NDS6wJFSnbo64ODMBKYouqs-p1BNsQ_y2NtUtJlM9dsN_mK0)

#### 2. Fluxo para o processamento das respostas
![](http://www.plantuml.com/plantuml/png/pPJ1RXCn48Rl-nHcuP18RNBXX5IfRG9S6gb9uLpDhgTRIrvxwx5BMyJ380vz0CGJvCMOsMwWraeHGXp89UDPs_FD_zi-fWWXfjOMBuohRTAehcFiwCry7k3Jh37nEbM9CDJUHNHnLljstbbmikQGehQccYzU7vvBwkFgRDu2HGoSkbpujlDErdIo_udM6xGVe9cKGFUkBW_KAsiSNiHxY-f8BO6kKPznPZAT5iM2wm4FmhAQgDQxnklgG9KhYPQd9OTBY501eSGdeOK7TA0ygPk458rtsw_1y30WCOOsccCDf3gacsI88rJEtsQP3W8eme3jxsL0vNESTSA4bs_luaGctfeQMHuXU4W1rSLJIfqc4gntneBydmTV8n4e67WeSiHQNta6vu2Wzgog1ePg68ArLc0ZVpA2OIfZcKHZXd9vwfFJ4EudKdPNesN5FTViKRQFNifatygf-bme_lqoQ1Amy-j1DWX6bcyuHIPkl_DGjbXdgafJYvS7Qh1ZjWpc5aFc16ixDWFtkCEzvLIYBpTBgSKWzVgGPmRXsUnatA7q1inMqcPZN3CRh60d_hK3OyfCk_8z1dIrUL9RSMSZyHXOeCJ9u6r_QgziklCzKHqCR1-ttzW56CGSTi9dw4pNyOW_oEGVo4j7SZFh_-dpbwBOe1tZx2xwtzvev-LLYT3GqV38JALGVfBoUojftwBoUPLdHLYLlk7L-VfFTy_FmydJoTl3beimbcNF5iVej3olnKy0)

#### 3. Fluxo para a criação dos questionários
![](http://www.plantuml.com/plantuml/png/dLRDRjj64BxhAQPC3nAWM9UU2WI88Wbr2lyefD8SXH5tB2z0xjApIpTsqOSnUiW35BtqgXVh3ibOeaWLYNNHOgZvlczclXtghVF8liopmG_Qf5cf26wzBzpFamdZxsTRxM_BJUc8Ksiy6N-MsdnIP6WavxNpAjERoUodrqi9VRoycEJeF748hMSsBwoHd4Bm1rEbOifMk1r6w1vC6etXnqmRIln3Hl06vkXkILs4o70q6YJdrv_MoqMSN5-jhp-kBjvVBOQZmM19xAmPeigr6KCqbM_jFAEo78N0ByHaKermLvBpsfhT4slhW839bPb7PLqKS9A783DVBpxxOQe4QPRPKjrao2GmSy7Kcr93LVVkNsKXuEsUl4x32RR86EA0K13VMCxHf0GA7HIxfwqsA2Ipa8hQ4CytGyYjsLgr2TYNSfg_gsZGumPTHJaD88za4Amx5i_aGYUL3jfh3d9tfNOLoPvb_SwMHY4_33_HPbeK0JCS89modQB0GPB4qGZ-643uF8zdAF0V6aOCX25nMLS11J92NDCJmuT3NI8wnaVBOpXVNLwCOVPAGk-D3ot1bEfaVaw-QoMFsY9aeYSqA88PQznzsVrbGT5BHAGXdsLiZJjutyAEaDedfxN4Unzz6xSrLGAeGm-2A_E0_TZuyS_UEIR4zqksAJc7UT0cIYIcTr-gJhIUzGnMlCj7bGWDsqpkYq0qzwM606MxtPqcoxEhnGegKscu_6qcqONpNFgI4MnxiFk6LmCRTvxlpLp_r08spgyr45Xteb5r0XPCZeol2JhpSw51hPgZunfTgqYPOoIJs_T65DnavMUvRdHOIrkfeheOvz41jNJzGo6rSv5xl5ROe_d48UIqt_tDkkjsLwbyDOPcXvpDMTyJjzQ7iVSTOg3JAwMnNqpPrwtQlOhJocP0-VEzASgDR9M9D2T52vLLpbUhPI9htUFMlMcs_AY2xc3MMpSceqYcAvlqOEVyFzewrjlRPd4tcgE5yKpRGnp-YgrgpEzLsBqzmdAlJrZU4LTMKRRJfBi345UtQdcTh2QLcicluHNNBwb7WRYxVpYs7wER8ARxBeXkGlCoU-5R2qmFqM3mbeog_YZy1m00)

#### 4. Fluxo para a visualização dos resultados
![](http://www.plantuml.com/plantuml/png/hLNDRjj64BxhARPg3pAWc4MGNWe4Y289TGh_A9JI78KXTq8liDnbPfTfvQ8FO_IGT-XLBzOPhajR4TqMHdWQpMg-xvkVdNqL8b1iQplwnhZIjXhLTOnD-37B27uzhKoyReis89NUHNJnjFHrrbXm4lCiH6rDaSrVF5k9wzt5ULP3Y4ZisivztNWdCOtWZsPQvsWtK4t647Qk74_LTzOuNCUTHVLIBI1Sepvdp-JaP3HQdrsztwwM-VhgSdlrRdF-vd8vOVSAANWt0GTs5-9KZMTicH1XpFRSkz3Q2Ce7HTYPcitGra3cfhCrg0R3nzO460iBWs2zNVuM9wLs0c5zgpzO81J01IEJALgZklptVsclCCJzRJGbMwe20lOh0QKFdcfm9J97KCt-jZ8EWf2mh0Z68IsAYQgzgxmk6Fn2hCNhZWSY511Gx1cZtA3halZOCflnRdzB9kN49TKc9HBwJ0vPjgzzwpJGRl8UYrdJC2ORYYrhIX0ujLxdunFr-qZnr_Tf8l1lxnY12JbmbT9G3H2eFD4ZgRSFTOde76uyJTNPvk9ygkRVYkkDYrmJA345Knzya1GhFnG1kdv4WqOr9mFxp_i_lVnuWeYIuqdwXeIk5BiluP6GD42FQydx0VkVt6au9NPuE4N27qDjN2DzMf4lCGIeMPe84P_PV_Q2Td0sq5UPNVeY4Q4XRvcM1EAdL904eRG_BkvilJgzN6vKDrD6NVmo5-yoH6fZIw3yOL_xUgT-JO_ExsSv_TKhI8D_fm4VlyGf01e-HHSJmL7xc8rsnqaBtb7x-hjukY3p2MdyHO49oxP1Iap_qRzHZlP-FGqEqQphbiAwdxwcBUHkPcZHH4zWin_uU_xzynTPJwMwDfnjDgkrhCu8LNYPDYdp2kaGLrfgEJgD8b8MrOCR_U-0sznKrtTxyNxVBbqah1uYqJ_eEg4-HQPCuzUkKlOplnt36WRuqhmCIl338CSH_N9_z2bo0rYlqEdkXVmR)

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
![Status](https://img.shields.io/badge/Status-Projeto%20em%20Desenvolvimento-yellow)

