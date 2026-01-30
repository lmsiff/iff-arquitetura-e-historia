# Historia e Arquitetura - Resumo

## Camadas e Responsabilidades

Em um sistema composto pelas camadas de **apresentação**, **negócio**, **persistência** e **banco de dados**, é fundamental respeitar a ordem dessas camadas. A camada de apresentação **não deve** acessar diretamente o banco de dados. Quando isso acontece, temos o chamado **Architecture Sinkhole Anti-Pattern**.

Esse antipadrão gera diversos problemas:

* Dificulta a reutilização de código
* Prejudica a escalabilidade
* Mistura responsabilidades que não pertencem à camada de apresentação
* Torna os testes mais complexos

Cada camada deve ter uma responsabilidade clara, comunicando-se apenas com a camada imediatamente abaixo.

---

## Antipadrões e Evolução das Arquiteturas

Um **antipadrão** é uma solução recorrente que parece funcionar, mas que na prática quebra a eficiência na resolução de um problema.

Na era dos **mainframes**, tudo era centralizado em uma única máquina robusta. Os usuários acessavam o sistema por meio de terminais burros que apenas enviavam comandos e recebiam respostas. Essa arquitetura monolítica centralizada apresentava **baixa flexibilidade** e alto acoplamento.

Com a evolução para o modelo **cliente-servidor**, vários clientes passaram a acessar diversos servidores por meio de uma rede, trazendo mais flexibilidade e abrindo espaço para arquiteturas distribuídas.

---

## Arquitetura em 2 Camadas

A arquitetura em **2 camadas (UI + Regras – Banco de Dados)** concentra a lógica de negócio no cliente. O software é instalado no computador do usuário e se conecta diretamente ao banco de dados em um servidor robusto.

Esse modelo pode funcionar bem para sistemas pequenos, mas apresenta limitações importantes:

* Necessidade de reinstalar o software a cada mudança
* Processo de atualização lento e custoso
* Dificuldade de escalar com muitos usuários

---

## Arquitetura em 3 Camadas

Na arquitetura em **3 camadas (Cliente – Servidor de Aplicação – Banco de Dados)**, a lógica de negócio é movida para uma camada intermediária.

O cliente passa a ser responsável apenas pela interface gráfica, enquanto o servidor de aplicação concentra as regras de negócio. Isso permite:

* Atualização centralizada das regras
* Manutenção mais simples e barata
* Menor esforço para corrigir bugs

O principal desafio desse modelo era atualizar a interface gráfica sem depender de instaladores locais.

---

## Arquitetura em 4 Camadas

A arquitetura em **4 camadas (Navegador – Servidor Web – Servidor de Aplicação – Banco de Dados)** leva a descentralização ainda mais longe.

* O navegador entrega a interface
* O servidor web entrega páginas e arquivos estáticos
* O servidor de aplicação processa regras de negócio
* O banco de dados armazena os dados

Tecnologias como **HTML, CSS e JavaScript** passam a compor a interface. Essa abordagem mostrou como a separação de camadas melhora:

* Desacoplamento
* Velocidade de atualização
* Redução de custos
* Escalabilidade

---

## Estilos Arquiteturais vs Padrões Arquiteturais

**Estilos arquiteturais** definem a estrutura geral do sistema e como os componentes se comunicam. Exemplos:

* Monolítico
* Em camadas
* Cliente-servidor
* P2P

Já os **padrões arquiteturais** oferecem soluções reutilizáveis para problemas recorrentes de organização do código e responsabilidades. Exemplos:

* MVC
* MVVM
* Arquitetura Hexagonal
* Clean Architecture

De forma simples: o **estilo define o tipo do sistema**, enquanto o **padrão define como organizar o código**.

---

## MVC – Model, View, Controller

O **MVC** é uma receita clássica para organizar código:

* **Model**: manipula os dados e regras relacionadas ao banco
* **View**: cuida da interface
* **Controller**: coordena a comunicação entre view e model

É amplamente utilizado em frameworks como **Spring**, **Laravel** e **ASP.NET**. Apesar disso, conforme o sistema cresce, surgem limitações:

* Código duplicado
* Baixa coesão
* Dificuldade em testar regras de negócio
* Problemas de escalabilidade em times grandes

Conceitos como **alta coesão** e **baixo acoplamento** são fundamentais para mitigar esses problemas, assim como os **princípios SOLID**.

---

## Modelo em 4 Camadas Lógicas

Uma evolução comum do MVC é o modelo com camadas lógicas bem definidas:

* **View**: interface
* **Controller**: recebe ações do usuário
* **Service**: aplica regras de negócio
* **Model**: representa os dados
* **Infra/Repository**: persistência

Esse modelo aumenta a clareza das responsabilidades e facilita testes, embora seja mais complexo. Ele se alinha diretamente ao **Single Responsibility Principle (SRP)** do SOLID.

---

## Injeção de Dependência e Inversão de Controle

**Injeção de dependência** consiste em fornecer a uma classe aquilo de que ela precisa, em vez de ela criar dependências diretamente.

O núcleo do sistema **não deve depender de detalhes externos**. Pelo contrário: os detalhes devem depender do núcleo. Isso é feito por meio de **interfaces**, invertendo as dependências.

Benefícios:

* Facilidade para testes (uso de mocks)
* Flexibilidade para trocar banco de dados
* Melhor controle do design

---

## Deploy e Infraestrutura

Colocar um sistema em produção exige mais do que fazê-lo rodar localmente. Ferramentas comuns incluem:

* **Docker**: empacota dependências em containers previsíveis
* **VPS**: ambiente dedicado para produção
* **Nginx**: servidor web e proxy reverso

Esses elementos tornam o deploy mais confiável e padronizado.

---

## Qualidade de Código e Design

Qualidade de código envolve:

* Alta coesão
* Baixo acoplamento
* Manutenibilidade
* Escalabilidade

Padrões e princípios importantes:

* DRY
* YAGNI
* Encapsular o que varia
* Composição sobre herança

Padrões de projeto como **Factory**, **Builder**, **Adapter** e **Strategy** ajudam a manter o código claro. **TDD** reforça qualidade ao priorizar testes.

---

## Arquitetura de Produção Escalável

Uma arquitetura moderna de produção pode incluir:

* Load balancer
* API Gateway
* Serviços backend
* Cache
* Mensageria
* Workers
* Banco de dados confiável
* Object storage
* Integração com APIs externas

Esses elementos seguem princípios de sistemas distribuídos, com foco em escalabilidade horizontal, desacoplamento e performance.

---

## Arquitetura Hexagonal

Na **Arquitetura Hexagonal**, o núcleo contém entidades e casos de uso. A comunicação com o mundo externo ocorre por meio de **portas (interfaces)** e **adaptadores**.

O núcleo não conhece detalhes externos, o que torna o sistema:

* Mais testável
* Mais resiliente a mudanças
* Fortemente alinhado à inversão de dependência

---

## Clean Architecture e Onion Architecture

A **Clean Architecture** se destaca pela clareza na separação de camadas e foco nos casos de uso. O princípio fundamental é que **as dependências sempre apontam para as camadas mais internas e abstratas**.

Isso facilita:

* Testes
* Evolução tecnológica
* Escalabilidade

---

## Microserviços

Microserviços são serviços autônomos, focados em um único domínio de negócio.

Vantagens:

* Escalabilidade horizontal
* Deploy independente
* Isolamento de falhas

Desvantagens:

* Complexidade operacional
* Testes distribuídos
* Comunicação mais difícil

---

## Publish / Subscribe

Na arquitetura **publish-subscribe**, um serviço publica eventos e outros reagem a eles por meio de um event center.

Isso permite alta modularidade e facilidade de extensão sem modificar o publicador.

---

## Comunicação entre Serviços

### APIs HTTP

APIs REST com JSON são simples, mas falham se o serviço estiver indisponível e podem ter alta latência.

### GraphQL

GraphQL permite consultas específicas, reduzindo dados desnecessários, porém aumenta a complexidade no backend e dificulta cache.

### Mensageria

Com **Kafka** ou **RabbitMQ**, serviços enviam mensagens para filas, permitindo comunicação assíncrona, maior resiliência e desacoplamento.

---

## SOA – Service Oriented Architecture

SOA organiza serviços corporativos reutilizáveis com contratos bem definidos, geralmente integrados por um **ESB**.

### Vantagens

* Alta reutilização
* Integração com sistemas legados
* Governança forte

### Desafios

* ESB como gargalo
* Overhead de governança
* Serviços grandes demais
* Complexidade de orquestração

Não existe arquitetura perfeita, apenas a mais adequada ao contexto.

---

## CQRS – Separando Leitura e Escrita

O **CQRS (Command Query Responsibility Segregation)** separa:

* **Commands**: escritas com regras de negócio
* **Queries**: leituras otimizadas para performance

Isso traz benefícios em cenários com:

* Alto volume de leitura
* Relatórios em tempo real
* Validações complexas

---

## No fim, um sistema bem arquitetado é:

* Modular
* Reativo
* Escalável
* Resiliente
* Organizado
