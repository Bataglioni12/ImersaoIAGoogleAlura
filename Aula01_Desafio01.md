# Prompt Gemini

# Sou Analista de Testes/QA, então pedi ajuda ao Gemini para me ajudar com possíveis casos de testes para uma determinadas regras de negócio.

# REQUISIÇÃO 
(

    ## "Sou Analista de Testes e estou precisando escrever cenários de testes baseado nas seguintes regras de negócio onde estamos implantando Dashboards para os usuários. Me informe todas as opções de cenários de testes com a escrita em BDD separando cada campo por um cenário de teste diferente. Os campos de filtro devem ser testados juntos conforme regra de negócio"

    RN01 - O acesso a ferramenta ‘Dashboard’ será concedido pela área de negócio, por meio da aplicação ‘gestão de acesso’. Somente terão acesso aos painéis os usuários autorizados em sistema.

    RN02 - Serão criados três campos como opção de filtros de pesquisa para o módulo ‘Atendimento Presencial’:
    Filtros de pesquisa:
    Unidade – campo de seleção contendo a lista de TODAS as unidades de atendimento cadastradas no banco de dados  e uma opção igual a: ‘Geral – todas as unidades’. 

    O campo Unidade será de preenchimento obrigatório e sempre virá preenchido default igual a ‘Geral – todas as unidades’.

    Data início – campo de seleção do tipo calendário de preenchimento obrigatório. Esse campo será preenchido default com a data útil (Segunda a Sábado) imediatamente anterior a data corrente. 
    Será permitida a seleção de data anterior a data corrente, limitado ao ano anterior ao ano corrente.
    A data de início não poderá se maior que a data corrente. O componente do calendário será disponibilizado com as datas posteriores à data corrente desabilitadas.

    Data fim - campo de seleção do tipo calendário de preenchimento obrigatório.  Esse campo será preenchido default com a data útil imediatamente anterior a data corrente.
    Será permitida a seleção de data anterior à data corrente, desde que maior ou igual a data de início.
    Não será permitido inserir data futura. O componente de calendário será habilitado conforme essa regra.
    O calendário de data fim será limitado ao ano anterior ao ano corrente.
    
    O botão ‘Solicitar dados’ tem a funcionalidade de executar a pesquisa e retornar os resultados com base nos dados informados nos campos: Unidade, data de início e data fim.
    Sempre que forem alteradas as informações dos campos: Unidade, data de início e data fim, será necessário acionar o botão ‘Solicitar dados’ para que o sistema faça nova busca e atualize os indicadores do painel.

    Regras Gerais: 
    Caso não haja resultados com os dados informados nos filtros de pesquisa, o sistema deverá apresentar a mensagem: “Não existem resultados para os dados informados”
    Não será permitido digitação nos campos de datas, somente a seleção no calendário.
    Todos os campos descritos acima: Unidade, data início e data fim, serão de preenchimento obrigatório e a pesquisa será feita utilizando a combinação desses três campos.
    Os campos ficarão sempre habilitados para a atualização de novas informações." 
)

# RESPOSTA 
(

    ## Cenários de Teste BDD para Dashboards - Regras de Negócio

    1. Cenário: Acesso à Ferramenta Dashboard

    **Dado** que o usuário não possui acesso à ferramenta Dashboard
    **Quando** o usuário tenta acessar a ferramenta
    **Então** o sistema deve exibir uma mensagem informando que o acesso não está autorizado

    2. Cenário: Filtro de Unidade

    **Dado** que o campo Unidade esteja presente na tela de filtros
    **Quando** o usuário não seleciona nenhuma unidade
    **Então** o sistema deve exibir uma mensagem informando que a seleção da unidade é obrigatória

    **Dado** que o campo Unidade esteja presente na tela de filtros
    **Quando** o usuário tenta selecionar uma unidade inexistente
    **Então** o sistema deve exibir uma mensagem informando que a unidade selecionada não é válida

    **Dado** que o campo Unidade esteja presente na tela de filtros
    **Quando** o usuário seleciona a opção "Geral - Todas as unidades"
    **Então** o sistema deve considerar a seleção como um filtro para todas as unidades

    **Cenário: Filtro de Data de Início**

    **Dado** que o campo Data de Início esteja presente na tela de filtros
    **Quando** o usuário não seleciona nenhuma data
    **Então** o sistema deve exibir uma mensagem informando que a seleção da data de início é obrigatória

    **Dado** que o campo Data de Início esteja presente na tela de filtros
    **Quando** o usuário tenta selecionar uma data futura
    **Então** o sistema deve exibir uma mensagem informando que a data de início não pode ser futura

    **Dado** que o campo Data de Início esteja presente na tela de filtros
    **Quando** o usuário tenta selecionar uma data anterior à data útil (Segunda a Sábado) imediatamente anterior à data corrente
    **Então** o sistema deve exibir uma mensagem informando que a data de início não pode ser anterior à data útil

    **Dado** que o campo Data de Início esteja presente na tela de filtros
    **Quando** o usuário seleciona uma data válida
    **Então** o sistema deve considerar a data selecionada como filtro

    **Cenário: Filtro de Data Fim**

    **Dado** que o campo Data Fim esteja presente na tela de filtros
    **Quando** o usuário não seleciona nenhuma data
    **Então** o sistema deve exibir uma mensagem informando que a seleção da data fim é obrigatória

    **Dado** que o campo Data Fim esteja presente na tela de filtros
    **Quando** o usuário tenta selecionar uma data futura
    **Então** o sistema deve exibir uma mensagem informando que a data fim não pode ser futura

    **Dado** que o campo Data Fim esteja presente na tela de filtros
    **Quando** o usuário tenta selecionar uma data anterior à data de início
    **Então** o sistema deve exibir uma mensagem informando que a data fim não pode ser anterior à data de início

    **Dado** que o campo Data Fim esteja presente na tela de filtros
    **Quando** o usuário seleciona uma data válida
    **Então** o sistema deve considerar a data selecionada como filtro

    **Cenário: Botão Solicitar Dados**

    **Dado** que os campos Unidade, Data de Início e Data Fim estejam preenchidos com dados válidos
    **Quando** o usuário clica no botão "Solicitar Dados"
    **Então** o sistema deve executar a pesquisa com base nos dados informados nos filtros

    **Dado** que os campos Unidade, Data de Início e Data Fim estejam preenchidos com dados válidos
    **Quando** o usuário clica no botão "Solicitar Dados" e não há resultados para os dados informados
    **Então** o sistema deve exibir a mensagem "Não existem resultados para os dados informados"

    **Cenário: Alteração dos Filtros**

    **Dado** que os campos Unidade, Data de Início e Data Fim estejam preenchidos com dados válidos
    **Quando** o usuário altera qualquer um dos campos de filtro
    **Então** o sistema deve desativar o botão "Solicitar Dados" até que o usuário clique novamente no botão

    **Dado** que os campos Unidade, Data de Início e Data Fim estejam preenchidos com dados válidos
    **Quando** o usuário altera qualquer um dos campos de filtro e clica no botão "Solicitar Dados"
    **Então** o sistema deve executar a pesquisa com base nos novos dados informados nos filtros

    **Cenários Adicionais:**

    * Testar a validação de formatos de data nos campos Data de Início e Data Fim.
    * Testar o comportamento do sistema quando há erros na comunicação com o servidor durante a execução da pesquisa.
    * Testar a performance do sistema em diferentes cenários de carga, com grande volume de dados.
    * Testar a acessibilidade da interface para usuários com deficiências.
    * Testar a usabilidade da interface,
)
