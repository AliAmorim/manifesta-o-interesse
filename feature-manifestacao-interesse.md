# Feature: Manifestação de Interesse para o Diário de Classe Municipal

**Status:** Em especificação
**Autora:** Aline Da Silva Amorim
**Plataforma:** Sala do Futuro
**Versão:** 1.0

---

## 1. Visão Geral

A Manifestação de Interesse é o mecanismo pelo qual municípios da rede estadual formalizam seu interesse em utilizar o módulo **Diário de Classe** na plataforma Sala do Futuro. O fluxo substitui a adesão direta por um processo de manifestação, cuja aprovação e disponibilização dependem de análise pela Secretaria da Educação.

A feature é um formulário guiado em 4 etapas, acessível pelo representante legal do município, que coleta a identificação do município, apresenta um resumo dos requisitos, registra o aceite formal do Termo de Manifestação de Interesse e confirma o envio.

---

## 2. Contexto e Problema

### 2.1 Situação atual

Atualmente, não existe um canal formal para que municípios expressem interesse na utilização do Diário de Classe. A Secretaria da Educação precisa de um mecanismo estruturado para:

- Mapear quais municípios desejam utilizar a solução
- Garantir que o município ciente dos requisitos técnicos e funcionais antes de receber acesso
- Registrar formalmente a manifestação, incluindo ciência das responsabilidades e da LGPD
- Criar uma base de dados para planejamento de implantação

### 2.2 Por que isso importa

Sem esse fluxo, a Secretaria não tem visibilidade sobre a demanda, e municípios interessados não têm um caminho claro para iniciar o processo. A feature resolve ambos os lados: fornece um canal de entrada padronizado e gera os dados necessários para o planejamento operacional.

---

## 3. Personas

### 3.1 Representante Legal do Município

- **Quem é:** Prefeito, Secretário de Educação ou servidor com poder de representação legal do município
- **Objetivo:** Formalizar o interesse da rede municipal de ensino no Diário de Classe
- **Contexto:** Acessa a plataforma Sala do Futuro com credenciais ativas; precisa compreender os requisitos antes de manifestar interesse
- **Frustração:** Falta de um caminho claro para aderir a módulos da plataforma

### 3.2 Gestor Administrativo da Plataforma (Secretaria da Educação)

- **Quem é:** Equipe técnica e pedagógica da Secretaria responsável pela gestão da Sala do Futuro
- **Objetivo:** Receber, analisar e processar as manifestações de interesse dos municípios
- **Contexto:** Precisa de dados consolidados para definir público-alvo e sequência de implantação
- **Frustração:** Falta de dados sobre demanda e ausência de processo padronizado

---

## 4. Objetivos e Não-Objetivos

### 4.1 Objetivos

| # | Objetivo | Métrica de sucesso |
|---|----------|-------------------|
| O1 | Permitir que municípios manifestem interesse de forma autônoma | 100% dos municípios interessados conseguem completar o fluxo |
| O2 | Garantir que o município compreenda os requisitos antes de confirmar | Taxa de conclusão do fluxo > 80% |
| O3 | Registrar formalmente a manifestação com ciência dos termos | Log de aceite com timestamp, município e URE persistidos |
| O4 | Fornecer dados consolidados para planejamento de implantação | Dashboard de manifestações disponível para a Secretaria |

### 4.2 Não-Objetivos

- **NO1:** Conceder acesso imediato ao Diário de Classe após a manifestação
- **NO2:** Permitir configuração dos módulos integrados neste fluxo
- **NO3:** Substituir os processos de cadastro de turmas, matrículas ou outros módulos
- **NO4:** Criar um painel de gestão de manifestações neste escopo (será fase futura)

---

## 5. Descrição da Feature

### 5.1 Fluxo principal

A manifestação de interesse é um formulário guiado em **4 etapas sequenciais**, apresentadas por um menu de progresso horizontal:

```
[1. Município] → [2. Resumo] → [3. Aceite] → [4. Confirmação]
```

#### Etapa 1 — Identificação do Município

**Objetivo:** Identificar qual município está manifestando interesse e a qual Unidade Regional de Ensino (URE) pertence.

**Componentes:**
- Campo "Unidade Regional de Ensino" (select/dropdown)
- Campo "Município" (select/dropdown, dependente da URE)
- Botão "Continuar" (desabilitado até ambos os campos serem preenchidos)

**Comportamento:**
- O campo Município é desabilitado até que uma URE seja selecionada
- Ao selecionar uma URE, o campo Município é populado apenas com os municípios vinculados àquela URE
- Os dados são carregados de uma tabela de referência ou API
- O botão "Continuar" só é habilitado quando URE e Município estão selecionados

**Dados de exemplo (URE → Municípios):**

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

#### Etapa 2 — Resumo da Manifestação

**Objetivo:** Apresentar ao município um resumo claro do que está sendo solicitado, dos módulos disponíveis e das responsabilidades envolvidas.

**Componentes:**
- Título: "Manifestação de Interesse"
- Parágrafo explicativo sobre o processo
- 4 cards informativos em grade 2×2:
  1. **Módulos disponíveis** — Frequência, Registro de Aulas, Avaliações, Fechamento, Boletim
  2. **Configuração obrigatória** — Necessidade dos módulos integrados configurados
  3. **Perfis de acesso** — Acesso conforme vínculos e permissões cadastrados
  4. **Infraestrutura** — Responsabilidade do município com equipamentos e internet
- Caixa de destaque (fundo azul claro) com aviso sobre LGPD
- Botões: "Voltar" e "Continuar"

**Texto da caixa de destaque:**
> Ao manifestar interesse, o município declara estar ciente dos requisitos para utilização do Diário de Classe, das dependências entre os módulos da plataforma, das responsabilidades previstas neste processo e das disposições relativas à proteção de dados pessoais (LGPD).

#### Etapa 3 — Aceite do Termo

**Objetivo:** Apresentar o Termo de Manifestação de Interesse completo e obter o aceite formal do município.

**Componentes:**
- Título: "Aceite do Termo"
- Parágrafo instrutivo
- Botão toggle "Ler termo completo" (expand/colapsa o texto integral)
- Checkbox de aceite: "Li e concordo com o Termo de Manifestação de Interesse para utilização do Diário de Classe, estando ciente das condições e responsabilidades descritas."
- Botão "Confirmar manifestação" (desabilitado até o checkbox ser marcado)
- Botão "Voltar"

**Termo de Manifestação de Interesse — 10 seções:**

1. **Objetivo** — Formalizar o interesse e apresentar requisitos
2. **Sobre o Diário de Classe** — Descrição da solução e funcionalidades
3. **Requisitos para Utilização** — Acesso à Sala do Futuro e infraestrutura
4. **Dependências Funcionais** — 8 módulos obrigatórios (Coleta de Classes, Matrícula, Fundamento Legal, Matriz Curricular, Quadro Aula, Calendário Escolar, Atribuição de Professores, Grade Horária)
5. **Perfis de Acesso** — Permissões conforme vínculos cadastrados
6. **Responsabilidades do Município** — Atualização de dados, configuração, administração de usuários
7. **Infraestrutura e Equipamentos** — Responsabilidade exclusiva do município
8. **Proteção de Dados Pessoais (LGPD)** — Tratamento de dados, finalidade, segurança
9. **Considerações Gerais** — Integração entre módulos e possíveis alterações futuras
10. **Manifestação de Interesse** — Declaração de ciência e concordância

#### Etapa 4 — Confirmação

**Objetivo:** Confirmar ao município que a manifestação foi registrada com sucesso e orientar sobre os próximos passos.

**Componentes:**
- Ícone de sucesso (check verde em círculo)
- Título: "Interesse registrado com sucesso"
- Texto principal: "A manifestação de interesse do município foi enviada com sucesso."
- Texto complementar: "A Secretaria da Educação realizará a definição do público-alvo para utilização do Diário de Classe. Após essa etapa, o município será comunicado sobre a disponibilização do acesso e as orientações para utilização da solução."
- Botão "Voltar ao início"

---

## 6. Regras de Negócio

| # | Regra | Detalhe |
|---|-------|---------|
| RN01 | A manifestação não gera acesso imediato | O acesso ao Diário de Classe é condicionado à aprovação da Secretaria |
| RN02 | Acesso ativo à Sala do Futuro é obrigatório | O município deve estar cadastrado e com acesso ativo |
| RN03 | URE e Município são obrigatórios | Ambos os campos devem ser preenchidos para avançar |
| RN04 | Município depende da URE | O campo Município só é populado após seleção da URE |
| RN05 | Aceite do termo é obrigatório | O checkbox deve estar marcado para permitir a confirmação |
| RN06 | O termo deve conter as 10 seções | Conteúdo completo e atualizado conforme documento oficial |
| RN07 | Estado persistente entre etapas | Ao voltar, os dados preenchidos são mantidos |
| RN08 | Reset ao reiniciar | "Voltar ao início" limpa todos os campos e retorna à etapa 1 |
| RN09 | Dados devem ser persistidos | URE, Município, timestamp e aceite devem ser salvos no envio |
| RN10 | Fluxo é sequencial | Não é possível pular etapas; apenas etapas anteriores e a atual são acessíveis |

---

## 7. Modelo de Dados

### 7.1 Entidade: Manifestação de Interesse

| Campo | Tipo | Obrigatório | Descrição |
|-------|------|-------------|-----------|
| `id` | UUID | Sim | Identificador único da manifestação |
| `municipio_id` | FK | Sim | Referência ao município na base da plataforma |
| `ure_id` | FK | Sim | Referência à Unidade Regional de Ensino |
| `municipio_nome` | VARCHAR | Sim | Nome do município |
| `ure_nome` | VARCHAR | Sim | Nome da URE |
| `usuario_id` | FK | Sim | Usuário que realizou a manifestação (representante legal) |
| `aceite_termo` | BOOLEAN | Sim | Confirmação de leitura e concordância com o termo |
| `aceite_lgpd` | BOOLEAN | Sim | Confirmação de ciência sobre tratamento de dados |
| `data_manifestacao` | TIMESTAMP | Sim | Data e hora do envio da manifestação |
| `status` | ENUM | Sim | `pendente` · `aprovada` · `rejeitada` · `em_analise` |
| `observacoes` | TEXT | Não | Observações da Secretaria sobre a manifestação |
| `data_analise` | TIMESTAMP | Não | Data da análise pela Secretaria |
| `analista_id` | FK | Não | Usuário da Secretaria que analisou a manifestação |

### 7.2 Status possíveis

```
pendente → em_analise → aprovada
                      → rejeitada
```

---

## 8. Requisitos Funcionais

### 8.1 RF — Seleção de Município

| ID | Requisito | Prioridade |
|----|-----------|------------|
| RF01 | O sistema deve exibir um campo de seleção de URE carregado com as UREs cadastradas | P0 |
| RF02 | Ao selecionar uma URE, o campo Município deve ser populado apenas com municípios daquela URE | P0 |
| RF03 | O campo Município deve ficar desabilitado até que uma URE seja selecionada | P0 |
| RF04 | O botão "Continuar" deve ficar desabilitado até que URE e Município sejam selecionados | P0 |
| RF05 | O município selecionado deve ser validado contra a base de dados da plataforma | P0 |

### 8.2 RF — Resumo

| ID | Requisito | Prioridade |
|----|-----------|------------|
| RF06 | O sistema deve exibir um resumo com 4 cards informativos | P0 |
| RF07 | O conteúdo dos cards deve refletir os módulos, requisitos e responsabilidades atuais | P0 |
| RF08 | O sistema deve exibir uma caixa de destaque com aviso sobre LGPD | P0 |
| RF09 | O botão "Voltar" deve retornar à etapa 1 sem perder os dados preenchidos | P0 |

### 8.3 RF — Aceite do Termo

| ID | Requisito | Prioridade |
|----|-----------|------------|
| RF10 | O sistema deve exibir o texto completo do Termo de Manifestação de Interesse | P0 |
| RF11 | O termo deve estar oculto por padrão, com botão toggle para expandir | P1 |
| RF12 | O checkbox de aceite deve estar desmarcado por padrão | P0 |
| RF13 | O botão "Confirmar manifestação" deve ficar desabilitado enquanto o checkbox não estiver marcado | P0 |
| RF14 | O aceite deve registrar timestamp e identificação do usuário | P0 |

### 8.4 RF — Confirmação

| ID | Requisito | Prioridade |
|----|-----------|------------|
| RF15 | O sistema deve exibir tela de confirmação com mensagem de sucesso | P0 |
| RF16 | A manifestação deve ser persistida no banco de dados ao confirmar | P0 |
| RF17 | O status inicial da manifestação deve ser `pendente` | P0 |
| RF18 | O botão "Voltar ao início" deve resetar completamente o formulário | P0 |

### 8.5 RF — Navegação

| ID | Requisito | Prioridade |
|----|-----------|------------|
| RF19 | O menu de etapas deve indicar a etapa atual, concluídas e futuras | P0 |
| RF20 | Etapas futuras devem estar desabilitadas no menu | P0 |
| RF21 | Etapas concluídas devem ser clicáveis para revisão | P0 |
| RF22 | A navegação deve manter o estado dos dados entre etapas | P0 |
| RF23 | O scroll deve ir para o topo a cada troca de etapa | P1 |

---

## 9. Requisitos Não-Funcionais

| ID | Requisito | Detalhe |
|----|-----------|---------|
| RNF01 | Responsividade | O fluxo deve funcionar em desktop, tablet e mobile |
| RNF02 | Acessibilidade | Campos de formulário com labels associados; contraste adequado; navegação por teclado |
| RNF03 | Performance | Tempo de carregamento da página < 3s em conexão 3G |
| RNF04 | Segurança | Dados transmitidos via HTTPS; validação server-side dos campos |
| RNF05 | LGPD | Termo de consentimento explícito; dados tratados conforme Lei 13.709/2018 |
| RNF06 | Compatibilidade | Suporte a Chrome, Firefox, Safari, Edge (últimas 2 versões) |

---

## 10. Dependências

### 10.1 Módulos da plataforma

A Manifestação de Interesse não depende funcionalmente de outros módulos para seu fluxo de coleta. No entanto, a utilização posterior do Diário de Classe requer:

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

### 10.2 Dados de referência

- **Tabela de UREs** — cadastro atualizado das Unidades Regionais de Ensino
- **Tabela de Municípios** — vínculo município ↔ URE
- **Base de usuários** — representantes legais com acesso ativo à Sala do Futuro

---

## 11. Conformidade — LGPD

A feature envolve tratamento de dados pessoais nos seguintes pontos:

| Dado coletado | Base legal | Finalidade | Retenção |
|---------------|-----------|-----------|----------|
| Nome do município | Execução de política pública (Art. 7º, III) | Identificação da rede de ensino | Indeterminada |
| Nome do representante legal | Execução de política pública (Art. 7º, III) | Registro da manifestação | Indeterminada |
| E-mail do representante | Execução de política pública (Art. 7º, III) | Comunicação sobre status | Até conclusão do processo |
| Aceite do termo | Consentimento (Art. 7º, I) | Registro de ciência e concordância | Indeterminada |

**Obrigações:**
- O município deve ser informado sobre o tratamento de dados antes de manifestar interesse
- O aceite deve ser granular (termo de uso separado de tratamento de dados)
- Os dados devem ser acessíveis apenas por usuários autorizados da Secretaria
- O município pode solicitar acesso, correção ou exclusão de seus dados

---

## 12. Métricas de Sucesso

| Métrica | Meta | Período de medição |
|---------|------|-------------------|
| Taxa de conclusão do fluxo | > 80% | Mensal |
| Tempo médio de preenchimento | < 5 minutos | Mensal |
| Número de manifestações recebidas | — | Mensal (benchmark) |
| Taxa de rejeição (campos obrigatórios vazios) | < 5% | Mensal |
| Tempo médio de análise pela Secretaria | < 10 dias úteis | Mensal |

---

## 13. Fases de Implementação

### Fase 1 — MVP (Este escopo)

- [x] Protótipo visual do fluxo em 4 etapas
- [ ] Implementação do formulário com seleção URE → Município
- [ ] Persistência da manifestação no banco de dados
- [ ] Tela de confirmação com mensagem de sucesso
- [ ] Integração com base de UREs e municípios

### Fase 2 — Gestão de Manifestações

- [ ] Painel administrativo para a Secretaria visualizar manifestações
- [ ] Fluxo de análise (aprovar / rejeitar)
- [ ] Notificação por e-mail ao município sobre status da manifestação
- [ ] Filtros e busca no painel de manifestações

### Fase 3 — Implantação

- [ ] Ao aprovar manifestação, criar acesso ao Diário de Classe para o município
- [ ] Wizard de configuração dos módulos integrados
- [ ] Onboarding guiado para o município

---

## 14. Perguntas em Aberto

| # | Pergunta | Impacto | Decisão necessária até |
|---|----------|---------|----------------------|
| Q1 | Os dados de URE e município serão carregados de uma API existente ou de uma tabela estática? | RF01, RF02 | Início do desenvolvimento |
| Q2 | Haverá notificação por e-mail quando a manifestação for analisada? | Fase 2 | Fase 1 |
| Q3 | O representante legal deve ser identificado automaticamente pelo login ou preencher dados manualmente? | RF14 | Início do desenvolvimento |
| Q4 | É necessário log de auditoria completo (quem acessou, quando, o que alterou)? | RNF04 | Início do desenvolvimento |
| Q5 | O termo de manifestação terá versionamento (caso o texto mude no futuro)? | RF10 | Fase 2 |
| Q6 | Um município pode manifestar interesse mais de uma vez? | RN01 | Início do desenvolvimento |

---

## 15. Próximos Passos

1. **Validar a base de dados de UREs e municípios** — confirmar se os dados estão disponíveis via API ou precisam ser cadastrados
2. **Alinhar com a equipe jurídica** — revisar o termo de manifestação e a seção de LGPD
3. **Definir o fluxo de análise** — como a Secretaria receberá e processará as manifestações
4. **Iniciar desenvolvimento da Fase 1** — formulário, persistência e tela de confirmação
5. **Revisar este documento** — atualizar com decisões tomadas nas perguntas em aberto

---

*Documento gerado a partir do protótipo `adesao-diario-classe.html` e da user story `user-story-adesao.md`.*
