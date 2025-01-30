# Dinâmica: Design Estratégico do Projeto

## Objetivo
Identificar os subdomínios do projeto, classificá-los (Core, Supporting, Generic) e desenhar os bounded contexts, incluindo suas interações. Esse exercício ajudará a criar uma visão clara e estratégica do domínio.

---

## 1. Nome do Projeto
**Gestor De Filas**

---

## 2. Objetivo Principal do Projeto
**Melhorar a experiência de visita à restaurantes com alta demanda, através de gestão de filas virtuais.**  


---

## 3. Identificação dos Subdomínios
Liste os subdomínios do sistema e classifique-os como **Core Domain**, **Supporting Subdomain** ou **Generic Subdomain**.

### Visão cliente
| **Subdomínio**              | **Descrição**                                                                                      | **Tipo**         |
|-----------------------------|--------------------------------------------------------------------------------------------------|------------------|
| Gestão de filas             | Gerenciamento de fila online e fast pass                                                        | Core Domain      |
| Mapa                        | Mapa com restaurantes proximos                                                                  | Generic          |
| Pagamentos                  | Gestao de pagamentos dentro da plataforma                                                       | Generic          |
| Cadastro de usuários        | Cadastro de usuarios na plataforma                                                              | Supporting       |
| Menu online        | Menu onde o usuário pode fazer pedidos durante a fila                                                    | Supporting       |

---
### Visão restaurante
| **Subdomínio**              | **Descrição**                                                                                      | **Tipo**         |
|-----------------------------|--------------------------------------------------------------------------------------------------|------------------|
| Controle de ocupação        | Controle de mesas e filas para gerenciamento da ocupação e dos pedidos                           | Core Domain      |
| Análise dos dados           | Análise de dados para o restaurante (ocupação, picos)                                            | Core domain      |
| Cadastro do Estabelecimento | Cadastro do estabelecimento no sistema                                                           | Supporting       |
| Menu                        | Cadastro do menu do restaurante online                                                           | Supporting       |
| Gestão dos pedidos          | Gestao da conta das mesas                                                                        | Supporting       |

---

## 4. Desenho dos Bounded Contexts
Liste e descreva os bounded contexts identificados no projeto. Explique a responsabilidade de cada um.

| **Bounded Context**           | **Responsabilidade**                                                                                 | **Subdomínios Relacionados** |
|-------------------------------|-----------------------------------------------------------------------------------------------------|-----------------------------|
| Contexto de reserva filas  | Levanta informações de ocupação e gerencia estado atual da fila         | Gestão de filas, Controle de Ocupação, Mapa         |
| Contexto de Pagamentos   | Processa reservas de restaurantes e repassa para os estabelecimentos.                              | Pagamentos                  |
| Contexto de Analise dos dados   | Responsavel por levantar dados da ocupação, horários e pedidos mais feitos.                              | Analise de dados |

---

## 5. Comunicação entre os Bounded Contexts
Explique como os bounded contexts vão se comunicar. Use os padrões de comunicação, como:
- **Mensageria/Eventos (desacoplado):** Ex.: O Contexto de Consultas emite um evento "Consulta Finalizada", consumido pelo Contexto de Pagamentos.
- **APIs (síncrono):** Ex.: O Contexto de Pagamentos consulta informações de preços no Contexto de Consultas.

| **De (Origem)**              | **Para (Destino)**          | **Forma de Comunicação**    | **Exemplo de Evento/Chamada**                  |
|------------------------------|-----------------------------|-----------------------------|-----------------------------------------------|
| Contexto de Filas            | Contexto de Estabelicimentos      | Mensageria (Evento)         | Solicitar reservar ou local na fila                        |
| Contexto de Esbelecimentos   | Contexto De Filas      | Mensageria (Evento)                         | Confirmar que a reserva ou local na fila está ativa      |

---

## 6. Definição da Linguagem Ubíqua
Liste os termos principais da Linguagem Ubíqua do projeto. Explique brevemente cada termo.

| **Termo**                    | **Descrição**                                                                                   |
|------------------------------|-----------------------------------------------------------------------------------------------|
| Pedido              | É feito o pedido entre o cliente e restaurante.                                                       |
| Reserva              | Representa uma reserva entre o cliente e o estabelecimento                                                       |
| Cliente               | Usuário que reserva, paga e faz os pedidos.                                                      |
| Estabelecimento                 | É o estabelecimento (restaurante)                                                 |
| Fila                 | Fila de pessoas esperando uma mesa no restaurante desejado.                                                 |

---

## 7. Estratégia de Desenvolvimento
Para cada tipo de subdomínio, explique a abordagem para implementação:
- **Core Domain:** Controle de mesas e filas para gerenciamento da ocupação e dos pedidos.
- **Supporting Subdomain:** Cadastro de usuarios na plataforma.
- **Generic Subdomain:** Mapa com restaurantes proximos.

| **Subdomínio**              | **Estratégia**                         | **Ferramentas ou Serviços (se aplicável)** |
|-----------------------------|----------------------------------------|-------------------------------------------|
| Controle de Fila            | Desenvolvimento interno                |                                           |
| Controle de Mesas           | Desenvolvimento interno   |                                      |
| Crud de Usuários            | Terceirizar usando API          | Auth0                                    |
| Mapa            | Google Maps          | Google                                    |

---

## 8. Diagrama Visual (Opcional, mas Recomendado)
Desenhe um diagrama que mostre:
- Os bounded contexts.
- Como eles se comunicam.
- A relação com os subdomínios.

Use ferramentas como **Miro**, **Lucidchart** ou mesmo papel e caneta para criar seu diagrama e adicionar ao projeto.

---

## Dicas para Apresentação
- Explique cada parte do design, focando no **Core Domain** (o coração do negócio).
- Justifique por que certos subdomínios foram classificados como Supporting ou Generic.
- Destaque como a comunicação entre bounded contexts foi pensada para ser escalável.

---

Boa sorte com a dinâmica! 🚀
