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


### Visão cliente
| **Subdomínio**              | **Descrição**                                                                                      | **Tipo**         |
|-----------------------------|--------------------------------------------------------------------------------------------------|------------------|
| Gestão de filas             | Gerenciamento de fila online e fast pass                                                        | Core Domain      |
| Mapa                        | Mapa com restaurantes proximos                                                                  | Generic          |
| Pagamentos                  | Gestao de pagamentos dentro da plataforma                                                       | Generic          |
| Cadastro de usuários        | Cadastro de usuarios na plataforma                                                              | Supporting       |
| Menu        | Menu onde o usuário pode fazer pedidos durante a fila                                                    | Supporting       |
| Gestão dos pedidos          | Gestao da conta das mesas                                                                        | Supporting       |

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


| **Bounded Context**           | **Responsabilidade**                                                                                 | **Subdomínios Relacionados** |
|-------------------------------|-----------------------------------------------------------------------------------------------------|-----------------------------|
| Contexto de reserva  | Gerencia as reservas        | Gestão de filas, Controle de Ocupação, Mapa         |
| Contexto de Filas   | Responsavel por gerenciar a ordem de pessoas na fila.                              | Gestão de Filas, Mapa |
| Contexto de Ocupação   | Responsavel por levantar dados da ocupação e das mesas naquele momento.  | Contole de ocupacao |
| Contexto de Pagamentos   | Processa reservas de restaurantes e repassa para os estabelecimentos.                              | Pagamentos                  |
| Contexto de Analise dos dados   | Responsavel por levantar dados da ocupação, horários e pedidos mais feitos.                              | Analise de dados |
| Contexto de Cadastro  | Responsavel por fazer o cadastro de usuários e estabelecimentos                 | Cadastro de usuarios, cadastro de estabelecimentos |
| Contexto de pedidos   | Responsavel por gerenciar os pedidos feitos nas filas ou nas mesas.                              | Gestão de pedidos, Menu |
| Contexto de Conta   | Responsavel por gerenciar a conta dos usuarios                               | Gestão de pedidos, Usuarios |

---

## 5. Comunicação entre os Bounded Contexts

- **Mensageria/Eventos (desacoplado):** Ex.: O Contexto de Consultas emite um evento "Consulta Finalizada", consumido pelo Contexto de Pagamentos.
- **APIs (síncrono):** Ex.: O Contexto de Pagamentos consulta informações de preços no Contexto de Consultas.

| **De (Origem)**              | **Para (Destino)**          | **Forma de Comunicação**    | **Exemplo de Evento/Chamada**                  |
|------------------------------|-----------------------------|-----------------------------|-----------------------------------------------|
| Contexto de Reserva          | Contexto de Ocupaçao        | API                         | Solicitar reserva.                            |
| Contexto de Filas            | Contexto De Ocupação        | Mensageria (Evento)         | Confirmar que a reserva ou local na fila está ativa      |

---

## 6. Definição da Linguagem Ubíqua
Liste os termos principais da Linguagem Ubíqua do projeto. Explique brevemente cada termo.

| **Termo**                    | **Descrição**                                                                                   |
|------------------------------|-----------------------------------------------------------------------------------------------|
| Pedido              | É o pedido feito peloo cliente ao estabelcimento.                                                       |
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



