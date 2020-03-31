# Corona-Simulation

<!-- TOC -->

- [Corona-Simulation](#checklist-de-operação-de-serviços-de-nuvem)
    - [Contextualização](#introdução)
    - [Objetivo](#monitoração-pró-ativa)
    - [Resultados Esperados](#logdna-para-análise-de-problemas-e-troubleshooting)
    - [*Seções*](#checklists-operacionais-e-de-saúde-do-ambiente)
        - [*Parâmetros do COVID-19*](#checklist-operacional)
        - [*Cálculo da probabilidade de mortes*](#checklist-adicional-de-validação-de-saúde-do-ambiente)
        - [*Aumento e Diminuição do tamanho do dataset*](#checklist-adicional-de-validação-de-saúde-do-ambiente)
        - [*Mapas*](#checklist-adicional-de-validação-de-saúde-do-ambiente)
        - [*Animações*](#checklist-adicional-de-validação-de-saúde-do-ambiente)
        - [*Modelagem Matemática*](#checklist-adicional-de-validação-de-saúde-do-ambiente)
        - [*Dados*](#checklist-adicional-de-validação-de-saúde-do-ambiente)
<!-- /TOC -->

## Contextualização

A rápida propagação do vírus COVID-19 e suas implicações no âmbitos de saúde pública e econômico pegaram o mundo de surpresa em 2020. Por se tratar de uma nova situação, há muitas dúvidas e perguntas não respondidas, fazendo com que os gestores públicos sintam-se despreparados para tomar decisões.

Mesmo quando as decisões são tomadas, não há consenso quanto à sua efetividade, devido à falta de conhecimento científico e empírico sobre a doença e suas formas de propagação. O campo da simulação computacional pode ser de grande valia na tomada de decisões de combate à pandemias. 

Nesse ímpeto, a turma de Métodos Computacionais Intensivos para Mineração de Dados do Programa de Pós-Graduação Aplicada - PPCA da UnB recebeu a incumbência de, orientados pelo professor [Guilherme Rodrigues](https://github.com/Guilherme-Souza-Rodrigues), desenvolver em conjunto um modelo de simulação de resposta ao COVID_19.

## Objetivo

Este trabalho aspira modelar como as cidades pequenas devem se proteger do vírus.  As três políticas analisadas são:

* isolamento [vide exemplo em Minas Gerais](https://oglobo.globo.com/sociedade/coronavirus-cidade-no-interior-de-mg-se-isola-por-conta-propria-controla-entrada-de-visitantes-24320734)
* minimização das interações sociais
* combinação dessas estratégias.

Através dos resultados de simulação obtidos será possível determinar qual das três opções é a mais efetiva.

## Resultados esperados

Atualmente é possível realizar monitoração pró-ativa dos componentes da solução utilizando as ferramentas Sysdig e LogDNA. Esses serviços capturam métricas de requisições chegando aos clusters Kubernetes da aplicação QA Manager, dados de mensagens que chegam através de coletores do Watson, informações sobre as bases de dados PostgreSQL e logs da aplicação.
Segundo as práticas de SRE, os serviços expostos em nuvem devem ser observados sob quatro óticas:

## Seções

Atualmente é possível realizar monitoração pró-ativa dos componentes da solução utilizando as ferramentas Sysdig e LogDNA. Esses serviços capturam métricas de requisições chegando aos clusters Kubernetes da aplicação QA Manager, dados de mensagens que chegam através de coletores do Watson, informações sobre as bases de dados PostgreSQL e logs da aplicação.
Segundo as práticas de SRE, os serviços expostos em nuvem devem ser observados sob quatro óticas:

*Parâmetros do COVID-19*

É o tempo que se leva para envio de uma requisição e o recebimento de uma resposta. Geralmente é medido a partir do lado do servidor, embora muitas vezes a transação completa (do clique no botão em um browser do cliente até o recebimento do retorno positivo) precisa ser considerado por conta de velocidade de rede entre as pontas. 

*Cálculo da probabilidade de mortes*

Mede a quantidade de requisições que chegam aos serviços medidos. No caso das soluções atuais dos serviços implantados na nuvem, a principal medida de tráfego é média de requisições por segundo. Durante os horários de pico eles devem ser observados por pressionar a infra-estrutura, podendo levar ao limite dos recursos de infra-estrutura, tendo efeitos colaterais na solução como um todo. A observação contínua do tráfego do serviço auxilia no planejamento da capacidade computacional no curto e médio prazo.

*Aumento e Diminuição do tamanho do dataset*

Erros podem mostrar problemas de configuração de infra-estrutura, problemas nos aplicativos ou quebra de dependências. Um pico na taxa pode indicar um problema em algum serviço utilizado, como Watson Assistant ou base de dados, por exemplo. Pode indicar problemas no código da aplicação, como por exemplo, locks gerados na base de dados em decorrência de transações de escrita longas demais para um ambiente concorrente. Atualmente, a taxa de erros HTTP (código HTTP maior ou igual a 400) é a principal métrica utilizada nas soluções implementadas na nuvem IBM. Ela é expressa em requisições por segundo com falha.

*Mapas*

Mede o quão 'carregado' o serviço se encontra, comparando a capacidade dos recursos de infra mais importantes para o funcionamento do serviço com a carga atual sobre esses recursos. Em aplicações três camadas, métricas que medem saturação podem incluir memória em uso pelo webserver e banco, banda de rede para recepção das requisições e disco para armazenamento dos dados da aplicação.
A saturação ajuda a entender se um serviço conseguirá absorver mais carga ou se uma ação deve ser tomada anteriormente a um problema como falta de espaço em disco por exemplo. Geralmente, o aumento da latência de um serviço está frequentemente ligado a saturação do serviço.

Uma monitoração mínima consiste em observar ao menos essas quatro óticas e acionar em um humano em caso de problemas. Entretanto, as práticas de serviço em operação em nuvem nos dizem que, uma vez identificado os limites de cada métrica de cada ótica, alertas possam ser gerados para que o time fique ciente de um eventual/possível problema. Em casos mais maduros, o próprio sistema pode se recuperar desse limite ou da falha e somente notificar o time caso o procedimento automatizado falhe ou não gere o esperado efeito.

*Animações*

lalalalala

*Modelagem Matemática*

lalalal

*Dados*

lalalal














