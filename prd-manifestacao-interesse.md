# PRD — Manifestação de Interesse para o Diário de Classe Municipal

**Produto:** Sala do Futuro  
**Módulo:** Manifestação de Interesse — Diário de Classe  
**Versão:** 1.1  
**Autora:** Aline Da Silva Amorim  
**Status:** Aguardando revisão  

---

## 1. Objetivo do Documento

Este PRD descreve as regras de negócio, os fluxos, os requisitos funcionais e as condições de uso do sistema **Manifestação de Interesse para o Diário de Classe Municipal**. O documento é destinado à equipe de desenvolvimento que implementará a solução com seu próprio layout e stack tecnológico.

> **Importante:** Este documento contém apenas regras. Não há especificações técnicas, de interface ou de infraestrutura. A equipe de desenvolvimento é responsável pela tradução destas regras em solução técnica.

> **Nota sobre a Manifestação:** A manifestação é **apenas para conhecimento** da Secretaria da Educação. Não há fluxo de aprovação, rejeição ou análise formal no sistema.

---

## 2. Visão Geral do Sistema

### 2.1 O que é

A Manifestação de Interesse é o mecanismo pelo qual municípios da rede estadual formalizam seu interesse em utilizar o módulo **Diário de Classe** na plataforma Sala do Futuro.

### 2.2 Como funciona

O fluxo é um **formulário guiado em 4 etapas sequenciais**, acessível pelo representante legal do município:

```
[1. Município] → [2. Resumo] → [3. Aceite] → [4. Confirmação]
```

### 2.3 O que NÃO é

- Não concede acesso imediato ao Diário de Classe
- Não substitui cadastro de turmas, matrículas ou outros módulos
- Não possui fluxo de aprovação — a manifestação é apenas para conhecimento da Secretaria
- Não permite configuração dos módulos integrados

---

## 3. Personas

### 3.1 Representante Legal do Município

- **Quem é:** Prefeito, Secretário de Educação ou servidor com poder de representação legal
- **O que quer:** Formalizar o interesse da rede municipal no Diário de Classe
- **Como acessa:** Plataforma Sala do Futuro com credenciais ativas

### 3.2 Gestor Administrativo (Secretaria da Educação)

- **Quem é:** Equipe técnica/pedagógica da Secretaria responsável pela Sala do Futuro
- **O que quer:** Visualizar as manifestações de interesse recebidas dos municípios
- **Como acessa:** Relatório de manifestações na plataforma

---

## 4. Fluxo do Sistema — Regras por Etapa

### 4.1 Etapa 1 — Identificação do Município

**Objetivo:** Identificar qual município está manifestando interesse e a qual URE pertence.

#### Regras

| RN | Regra | Detalhe |
|----|-------|---------|
| RN01 | URE e Município são campos obrigatórios | Ambos devem ser preenchidos para avançar à próxima etapa |
| RN02 | O campo Município é dependente da URE | Só deve ser exibido/populado após a seleção de uma URE |
| RN03 | Municípios exibidos são filtrados pela URE | Apenas municípios vinculados à URE selecionada devem aparecer |
| RN04 | Botão "Continuar" desabilitado até preenchimento completo | URE + Município selecionados → botão habilitado |
| RN05 | O município selecionado deve ser validado contra a base da plataforma | Dados devem conferir com o cadastro oficial de UREs e municípios |
| RN06 | Município já manifestou interesse → exibir aviso | Se o município já possui manifestação registrada, exibir mensagem informando e bloquear nova manifestação |

#### Dados de referência

Os dados de URE e Município devem ser carregados de uma tabela de referência ou API. A base real deve ser alimentada pelo cadastro de UREs e municípios da plataforma.

**Exemplo de vínculo URE → Municípios:**

| URE | Municípios |
|-----|-----------|
| P.M. Araraquara | Araraquara, Américo Brasiliense, Boa Esperança do Sul, Gavião Peixoto, Motuca, Rincão, Santa Lúcia, Trabiju |
| P.M. Bauru | Bauru, Agudos, Arealva, Avaí, Balbinos, Duartina, Pirajuí, Presidente Alves, Reginópolis |
| P.M. Franca | Franca, Cristais Paulista, Itirapuã, Patrocínio Paulista, Pedregulho, Restinga, Ribeirão Corrente, São José da Bela Vista |
| P.M. Marília | Marília, Assis, Cândido Mota, Echaporã, Lutécia, Ocauçu, Paraguaçu Paulista, Pompeia |
| P.M. Presidente Prudente | Presidente Prudente, Álvares Machado, Anhumas, Martinópolis, Pirapozinho, Presidente Bernardes, Regente Feijó, Santo Anastácio |
| P.M. Ribeirão Preto | Ribeirão Preto, Barrinha, Cravinhos, Dumont, Guatapará, Jardinópolis, Pradópolis, Sertãozinho, Serrana |
| P.M. São Carlos | São Carlos, Descalvado, Dourado, Ibaté, Itirapina, Porto Ferreira, Ribeirão Bonito |
| P.M. São José do Rio Preto | São José do Rio Preto, Bady Bassitt, Bálsamo, Guapiaçu, Ibirá, Mirassol, Mirassolândia, Neves Paulista, Nova Granada |

> **Nota:** Os dados acima são exemplos didáticos. A base real deve ser alimentada pelo cadastro de UREs e municípios da plataforma.

---

### 4.2 Etapa 2 — Resumo da Manifestação

**Objetivo:** Apresentar ao município um resumo claro do que está sendo solicitado, dos módulos disponíveis e das responsabilidades envolvidas.

#### Regras

| RN | Regra | Detalhe |
|----|-------|---------|
| RN07 | O resumo deve exibir 4 cards informativos | Módulos disponíveis, Configuração obrigatória, Perfis de acesso, Infraestrutura |
| RN08 | Caixa de destaque obrigatória com aviso sobre LGPD | Texto deve informar que o município declara estar ciente dos requisitos, dependências, responsabilidades e proteção de dados |
| RN09 | Botão "Voltar" retorna à etapa 1 sem perda de dados | URE e Município selecionados devem ser mantidos |
| RN10 | Botão "Continuar" avança à etapa 3 | Sem bloqueios nesta etapa (após visualização) |

#### Conteúdo dos cards

| Card | Conteúdo |
|------|----------|
| Módulos disponíveis | Frequência, Registro de Aulas, Avaliações, Fechamento, Boletim |
| Configuração obrigatória | Necessidade dos módulos integrados configurados (Coleta de Classes, Matrícula, Fundamento Legal, Matriz Curricular, Quadro Aula, Calendário Escolar, Atribuição de Professores) |
| Perfis de acesso | Acesso conforme vínculos e permissões cadastrados |
| Infraestrutura | Responsabilidade do município com equipamentos e internet |

#### Texto da caixa de destaque (LGPD)

> Ao manifestar interesse, o município declara estar ciente dos requisitos para utilização do Diário de Classe, das dependências entre os módulos da plataforma, das responsabilidades previstas neste processo e das disposições relativas à proteção de dados pessoais (LGPD).

---

### 4.3 Etapa 3 — Aceite do Termo

**Objetivo:** Apresentar o Termo de Manifestação de Interesse completo e obter o aceite formal do município.

#### Regras

| RN | Regra | Detalhe |
|----|-------|---------|
| RN11 | O Termo deve conter 10 seções obrigatórias | Objetivo, Sobre o Diário, Requisitos, Dependências, Perfis, Responsabilidades, Infraestrutura, LGPD, Considerações Gerais, Manifestação |
| RN12 | O termo deve estar oculto por padrão | Toggle "Ler termo completo" expande/colapsa o texto integral |
| RN13 | Checkbox de aceite desmarcado por padrão | Texto: "Li e concordo com o Termo de Manifestação de Interesse para utilização do Diário de Classe, estando ciente das condições e responsabilidades descritas." |
| RN14 | Botão "Confirmar manifestação" desabilitado até checkbox marcado | Marca checkbox → botão habilitado |
| RN15 | Aceite deve registrar timestamp e identificação do usuário | Dados de quem confirmou devem ser persistidos |
| RN16 | Botão "Voltar" retorna à etapa 2 sem perda de dados | Estado mantido entre etapas |

#### Conteúdo obrigatório do Termo — 10 seções

| Seção | Conteúdo |
|-------|----------|
| 1. Objetivo | Formalizar o interesse e apresentar requisitos |
| 2. Sobre o Diário de Classe | Descrição da solução e funcionalidades |
| 3. Requisitos para Utilização | Acesso à Sala do Futuro e infraestrutura |
| 4. Dependências Funcionais | 8 módulos obrigatórios (Coleta de Classes, Matrícula, Fundamento Legal, Matriz Curricular, Quadro Aula, Calendário Escolar, Atribuição de Professores, Grade Horária) |
| 5. Perfis de Acesso | Permissões conforme vínculos cadastrados |
| 6. Responsabilidades do Município | Atualização de dados, configuração, administração de usuários |
| 7. Infraestrutura e Equipamentos | Responsabilidade exclusiva do município |
| 8. Proteção de Dados Pessoais (LGPD) | Tratamento de dados, finalidade, segurança |
| 9. Considerações Gerais | Integração entre módulos e possíveis alterações futuras |
| 10. Manifestação de Interesse | Declaração de ciência e concordância |

---

### 4.4 Etapa 4 — Confirmação

**Objetivo:** Confirmar ao município que a manifestação foi registrada com sucesso e orientar sobre os próximos passos.

#### Regras

| RN | Regra | Detalhe |
|----|-------|---------|
| RN17 | A manifestação deve ser persistida ao confirmar | Dados salvos para conhecimento da Secretaria |
| RN18 | Tela de confirmação exibe mensagem de sucesso | Ícone + título + texto principal + texto complementar |
| RN19 | Texto complementar explica próximos passos | Secretaria poderá visualizar a manifestação no relatório |
| RN20 | Botão "Voltar ao início" reset completamente o formulário | Limpa todos os dados e retorna à etapa 1 |
| RN21 | Dados persistidos: URE, Município, timestamp, aceite | Todos os campos devem ser salvos no envio |

---

## 5. Relatório de Manifestações

### 5.1 Objetivo

Permitir que a Secretaria da Educação visualize as manifestações de interesse recebidas dos municípios.

### 5.2 Regras

| RN | Regra | Detalhe |
|----|-------|---------|
| RN28 | Relatório exibe cards de resumo | Total de manifestações e UREs representadas |
| RN29 | Filtros disponíveis | URE, Município e busca por nome |
| RN30 | Tabela com colunas: Município, URE, Data da Manifestação | Sem coluna de status ou responsável |
| RN31 | Paginação | 8 itens por página |
| RN32 | Manifestação é para conhecimento | Sem fluxo de aprovação, rejeição ou análise |

---

## 5. Regras de Navegação

| RN | Regra | Detalhe |
|----|-------|---------|
| RN22 | Fluxo é sequencial | Não é possível pular etapas |
| RN23 | Menu de etapas mostra progresso | Indica etapa atual, concluídas e futuras |
| RN24 | Etapas futuras ficam desabilitadas no menu | Não é possível acessar diretamente |
| RN25 | Etapas concluídas são clicáveis | Permite revisão de etapas anteriores |
| RN26 | Estado persistente entre etapas | Ao voltar, os dados preenchidos são mantidos |
| RN27 | "Voltar ao início" limpa tudo | Reset completo do formulário |

---

## 6. Requisitos Funcionais

### 6.1 Seleção de Município

| ID | Requisito | Prioridade |
|----|-----------|------------|
| RF01 | Exibir campo de seleção de URE carregado com as UREs cadastradas | P0 |
| RF02 | Ao selecionar URE, popular campo Município apenas com municípios daquela URE | P0 |
| RF03 | Campo Município desabilitado até que URE seja selecionada | P0 |
| RF04 | Botão "Continuar" desabilitado até URE e Município serem selecionados | P0 |
| RF05 | Validar município selecionado contra a base de dados da plataforma | P0 |

### 6.2 Resumo

| ID | Requisito | Prioridade |
|----|-----------|------------|
| RF06 | Exibir resumo com 4 cards informativos | P0 |
| RF07 | Conteúdo dos cards refletir módulos, requisitos e responsabilidades atuais | P0 |
| RF08 | Exibir caixa de destaque com aviso sobre LGPD | P0 |
| RF09 | Botão "Voltar" retornar à etapa 1 sem perder dados | P0 |

### 6.3 Aceite do Termo

| ID | Requisito | Prioridade |
|----|-----------|------------|
| RF10 | Exibir texto completo do Termo de Manifestação de Interesse | P0 |
| RF11 | Termo oculto por padrão, com toggle para expandir | P1 |
| RF12 | Checkbox de aceite desmarcado por padrão | P0 |
| RF13 | Botão "Confirmar manifestação" desabilitado até checkbox marcado | P0 |
| RF14 | Registrar timestamp e identificação do usuário no aceite | P0 |

### 6.4 Confirmação

| ID | Requisito | Prioridade |
|----|-----------|------------|
| RF15 | Exibir tela de confirmação com mensagem de sucesso | P0 |
| RF16 | Persistir manifestação no banco de dados ao confirmar | P0 |
| RF17 | Dados persistidos: URE, Município, timestamp, aceite | P0 |
| RF18 | Botão "Voltar ao início" resetar completamente o formulário | P0 |

### 6.5 Navegação

| ID | Requisito | Prioridade |
|----|-----------|------------|
| RF19 | Menu de etapas indicar etapa atual, concluídas e futuras | P0 |
| RF20 | Etapas futuras desabilitadas no menu | P0 |
| RF21 | Etapas concluídas clicáveis para revisão | P0 |
| RF22 | Navegação manter estado dos dados entre etapas | P0 |
| RF23 | Scroll ir para o topo a cada troca de etapa | P1 |

### 6.6 Relatório de Manifestações

| ID | Requisito | Prioridade |
|----|-----------|------------|
| RF24 | Exibir cards de resumo (Total de manifestações, UREs representadas) | P0 |
| RF25 | Filtros por URE, Município e busca por nome | P0 |
| RF26 | Tabela com colunas: Município, URE, Data da Manifestação | P0 |
| RF27 | Paginação com 8 itens por página | P0 |

---

## 7. Requisitos Não-Funcionais

| ID | Requisito | Detalhe |
|----|-----------|---------|
| RNF01 | Responsividade | Fluxo deve funcionar em desktop, tablet e mobile |
| RNF02 | Acessibilidade | Campos com labels associados; contraste adequado; navegação por teclado |
| RNF03 | Performance | Tempo de carregamento < 3s em conexão 3G |
| RNF04 | Segurança | Dados transmitidos via HTTPS; validação server-side |
| RNF05 | LGPD | Termo de consentimento explícito; dados tratados conforme Lei 13.709/2018 |
| RNF06 | Compatibilidade | Chrome, Firefox, Safari, Edge (últimas 2 versões) |

---

## 8. Modelo de Dados (Entidade Principal)

### 8.1 Entidade: Manifestação de Interesse

| Campo | Tipo | Obrigatório | Descrição |
|-------|------|-------------|-----------|
| `id` | UUID | Sim | Identificador único |
| `municipio_id` | FK | Sim | Referência ao município |
| `ure_id` | FK | Sim | Referência à URE |
| `municipio_nome` | VARCHAR | Sim | Nome do município |
| `ure_nome` | VARCHAR | Sim | Nome da URE |
| `usuario_id` | FK | Sim | Usuário que realizou a manifestação |
| `aceite_termo` | BOOLEAN | Sim | Confirmação de leitura e concordância |
| `aceite_lgpd` | BOOLEAN | Sim | Confirmação de ciência sobre tratamento de dados |
| `data_manifestacao` | TIMESTAMP | Sim | Data/hora do envio |

### 8.2 Natureza da Manifestação

A manifestação é registrada **apenas para conhecimento** da Secretaria da Educação. Não há fluxo de aprovação, rejeição ou análise formal no sistema. A Secretaria visualiza as manifestações recebidas por meio de um relatório simplificado.

---

## 9. Conformidade — LGPD (Lei 13.709/2018)

### 9.1 Dados coletados

| Dado | Base legal | Finalidade | Retenção |
|------|-----------|-----------|----------|
| Nome do município | Art. 7º, III (execução de política pública) | Identificação da rede de ensino | Indeterminada |
| Nome do representante legal | Art. 7º, III | Registro da manifestação | Indeterminada |
| E-mail do representante | Art. 7º, III | Comunicação sobre status | Até conclusão do processo |
| Aceite do termo | Art. 7º, I (consentimento) | Registro de ciência e concordância | Indeterminada |

### 9.2 Obrigações

- O município deve ser informado sobre o tratamento de dados **antes** de manifestar interesse
- O aceite deve ser granular (termo de uso separado de tratamento de dados)
- Os dados devem ser acessíveis apenas por usuários autorizados da Secretaria
- O município pode solicitar acesso, correção ou exclusão de seus dados

---

## 10. Dependências Funcionais

A Manifestação de Interesse em si não depende de outros módulos para seu fluxo de coleta. No entanto, a utilização **posterior** do Diário de Classe requer:

| Módulo | Dependência | Obrigatório |
|--------|------------|-------------|
| Coleta de Classes | Criação de turmas | Sim |
| Matrícula | Vínculo estudante-turma | Sim |
| Fundamento Legal | Componentes curriculares | Sim |
| Matriz Curricular | Disciplinas ofertadas | Sim |
| Quadro Aula | Distribuição de aulas | Sim |
| Calendário Escolar | Dias letivos e não letivos | Sim |
| Atribuição de Professores | Vínculo docente-turma | Sim |
| Grade Horária | Organização de horários | Não |

---

## 11. Métricas de Sucesso

| Métrica | Meta | Período |
|---------|------|---------|
| Taxa de conclusão do fluxo | > 80% | Mensal |
| Tempo médio de preenchimento | < 5 minutos | Mensal |
| Número de manifestações recebidas | — | Mensal (benchmark) |
| Taxa de rejeição (campos obrigatórios vazios) | < 5% | Mensal |

---

## 12. Perguntas em Aberto

| # | Pergunta | Impacto | Decisão necessária até |
|---|----------|---------|----------------------|
| Q1 | Os dados de URE e município serão carregados de API existente ou tabela estática? | RF01, RF02 | Início do desenvolvimento |
| Q2 | Como a Secretaria será notificada sobre novas manifestações? | Fase 2 | Fase 1 |
| Q3 | O representante legal deve ser identificado automaticamente pelo login ou preencher dados manualmente? | RF14 | Início do desenvolvimento |
| Q4 | É necessário log de auditoria completo (quem acessou, quando, o que alterou)? | RNF04 | Início do desenvolvimento |
| Q5 | O termo de manifestação terá versionamento (caso o texto mude no futuro)? | RF10 | Fase 2 |

---

## 13. Anexos

- **Protótipo visual (Manifestação + Relatório):** `adesao-diario-classe.html`
- **User Story:** `user-story-adesao.md`
- **Feature completa:** `feature-manifestacao-interesse.md`

---

*Documento gerado por Aline Da Silva Amorim — Sala do Futuro / Secretaria da Educação.*
