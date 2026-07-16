# User Story — Manifestação de Interesse para o Diário de Classe

**Como** representante legal de um município,
**Quero** formalizar meu interesse na utilização do Diário de Classe,
**Para** que a Secretaria da Educação possa avaliar e disponibilizar o módulo para a minha rede de ensino.

---

## Critérios de Aceite

### Fluxo geral

- O fluxo é composto por 4 etapas sequenciais: **Município → Resumo → Aceite → Confirmação**
- As etapas são acessíveis por um menu horizontal posicionado abaixo do cabeçalho
- O cabeçalho exibe o título "Manifestação de Interesse - Diário de Classe Municípios"
- Apenas etapas já concluídas e a etapa atual são clicáveis no menu
- Etapas futuras ficam desabilitadas e com aparência esmaecida
- Cada etapa concluída recebe um indicador visual de conclusão (cor de destaque + número)

### Etapa 1 — Município

- Exibe dois campos de seleção lado a lado: **Unidade Regional de Ensino (URE)** e **Município**
- O campo Município é desabilitado até que uma URE seja selecionada
- Ao selecionar uma URE, o campo Município é populado apenas com os municípios vinculados àquela URE
- Os dados de URE e Município devem ser carregados de uma base de dados (API ou tabela)
- O botão "Continuar" fica desabilitado até que URE e Município sejam selecionados

### Etapa 2 — Resumo

- Exibe o título "Manifestação de Interesse" e um parágrafo explicativo
- Apresenta 4 cards informativos em grade 2x2 (empilhados no mobile):
  - **Módulos disponíveis**: lista com Frequência, Registro de Aulas, Avaliações, Fechamento, Boletim
  - **Configuração obrigatória**: texto sobre a necessidade dos módulos integrados configurados
  - **Perfis de acesso**: texto sobre concessão de acesso conforme vínculos e permissões
  - **Infraestrutura**: texto sobre responsabilidade do município com equipamentos e internet
- Exibe uma caixa de destaque com aviso sobre LGPD e ciência do município
- Botões: "Voltar" (volta à etapa 1) e "Continuar" (avança à etapa 3)

### Etapa 3 — Aceite

- Exibe título "Aceite do Termo" e parágrafo instrutivo
- Botão "Ler termo completo" que expande/colapsa o texto integral do Termo de Manifestação de Interesse (10 seções)
- Checkbox de aceite com texto: "Li e concordo com o Termo de Manifestação de Interesse para utilização do Diário de Classe, estando ciente das condições e responsabilidades descritas."
- O botão "Confirmar manifestação" fica desabilitado enquanto o checkbox não estiver marcado
- Ao avançar para a etapa 4, o estado do termo (expansão) e do checkbox são resetados
- Botões: "Voltar" (volta à etapa 2) e "Confirmar manifestação"

### Etapa 4 — Confirmação

- Exibe ícone de sucesso (check em círculo)
- Título: **"Interesse registrado com sucesso"**
- Texto: "A manifestação de interesse do município foi enviada com sucesso."
- Texto complementar: "A Secretaria da Educação realizará a definição do público-alvo para utilização do Diário de Classe. Após essa etapa, o município será comunicado sobre a disponibilização do acesso e as orientações para utilização da solução."
- Botão "Voltar ao início" que retorna à etapa 1 e reseta todo o estado do formulário

---

## Regras de negócio

- A manifestação de interesse **não gera acesso imediato** ao sistema
- A disponibilização está condicionada ao atendimento dos requisitos e procedimentos da Secretaria da Educação
- O município deve possuir acesso ativo à plataforma Sala do Futuro
- Os dados do município e URE selecionados devem ser persistidos no envio da manifestação
- O termo completo deve conter as 10 seções definidas no documento oficial

---

## Requisitos técnicos

- A navegação entre etapas deve persistir o estado (se o usuário voltar, os dados anteriores devem ser mantidos)
- O scroll deve ir para o topo a cada troca de etapa
- Layout responsivo: funciona em desktop e dispositivos móveis
- O menu de etapas em telas pequenas oculta os labels e exibe apenas os números
