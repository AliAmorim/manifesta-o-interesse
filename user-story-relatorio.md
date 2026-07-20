# User Story — Relatório de Manifestações

**Na situação atual, o município que manifesta interesse no Diário de Classe não possui uma forma padronizada de consultar o histórico de manifestações realizadas, dificultando o acompanhamento e a transparência do processo.**

**Nesta história, vamos criar uma tela de Relatório de Manifestações que permita à Secretaria da Educação visualizar, filtrar e consultar todos os municípios que já manifestaram interesse, com dados de município e data da manifestação.**

**Regras de Negócio:**

- O Relatório deve ser acessado por meio de uma aba de navegação no topo da página, compartilhando o mesmo ambiente visual da Manifestação
- O Relatório deve exibir um card de resumo com o total de manifestações registradas
- O sistema deve disponibilizar filtros por município (dropdown com todos os municípios de SP) e por busca livre (campo de texto)
- O filtro por município deve listar todos os 645 municípios do estado de São Paulo
- A busca livre deve filtrar pelo nome do município em tempo real
- Os filtros devem ser cumulativos: ao aplicar município + busca, o sistema retorna apenas os registros que atendem aos dois critérios
- O botão "Limpar" deve resetar todos os filtros e exibir a lista completa novamente
- A tabela de resultados deve exibir duas colunas: **Município** e **Data da Manifestação**
- A data da manifestação deve ser exibida no formato brasileiro (DD/MM/AAAA)
- A tabela deve exibir os registros de forma ordenada por data (mais recente primeiro)
- O sistema deve implementar paginação com 8 registros por página
- A paginação deve exibir botões de navegação (anterior/próximo) e números de página
- Quando não houver registros para os filtros aplicados, o sistema deve exibir uma mensagem amigável "Nenhuma manifestação encontrada"
- A contagem de registros deve ser atualizada dinamicamente ao aplicar filtros

**Exemplo:**

- Usuário acessa a aba "Relatório" no topo da página
- O card de resumo exibe "12" como total de manifestações
- A tabela lista os 12 municípios com suas respectivas datas
- O usuário seleciona o município "Bauru" no dropdown e clica em "Filtrar"
- A tabela exibe apenas o registro de Bauru com a data de sua manifestação
- O usuário clica em "Limpar" e a tabela retorna a exibição completa com 12 registros
- O usuário digita "Campinas" no campo de busca e clica em "Filtrar"
- A tabela exibe todos os municípios que contenham "Campinas" no nome

**Considero aceito se, o usuário consiga acessar o Relatório pela aba de navegação, visualizar o total de manifestações, filtrar por município e por busca livre, navegar pelas páginas da tabela e limpar os filtros para voltar à visualização completa.**
