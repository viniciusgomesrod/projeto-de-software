## Gerenciar Orçamento:

``` plantuml
@startuml
title Caso de Uso: Gerenciar Orçamento

actor "Auxiliar Comercial" as AC
participant "Sistema" as S
participant "Banco de Dados" as BD

== Criação do Orçamento ==

AC -> S: Acessar módulo de orçamentos
S -> AC: Exibir formulário de orçamento

AC -> S: Inserir dados do cliente (novo ou existente)
S -> BD: Buscar/validar dados do cliente
BD --> S: Retornar dados do cliente

AC -> S: Selecionar produtos (perfis, vidros, ferragens)
S -> BD: Consultar estoque e preços
BD --> S: Retornar disponibilidade e preços

AC -> S: Definir quantidades e especificações técnicas
S -> S: Calcular preço automaticamente
S -> AC: Exibir orçamento calculado

AC -> S: Salvar orçamento (rascunho)
S -> BD: Armazenar orçamento
BD --> S: Confirmação de salvamento
S -> AC: Exibir confirmação e número do orçamento

== Aprovação do Orçamento ==

AC -> S: Consultar orçamentos pendentes
S -> BD: Buscar orçamentos em aberto
BD --> S: Retornar lista de orçamentos
S -> AC: Exibir orçamentos disponíveis

AC -> S: Selecionar orçamento para aprovação
S -> BD: Buscar dados completos do orçamento
BD --> S: Retornar detalhes do orçamento
S -> AC: Exibir orçamento completo

AC -> S: Registrar aprovação do cliente (fora do sistema)
S -> S: Marcar orçamento como aprovado
S -> BD: Atualizar status do orçamento
BD --> S: Confirmação de atualização

== Processamento Pós-Aprovação ==

S -> S: Processar aprovação automaticamente
S -> S: Gerar documentos de produção
note over S: Gera Ordem de Produção\nGera Lista de Corte\nGera Relatório de Materiais

S -> BD: Armazenar documentos gerados
BD --> S: Confirmação de salvamento

S -> AC: Notificar geração de documentos\ncom sucesso
S -> BD: Atualizar status geral do processo
BD --> S: Confirmação de atualização

== Consulta e Acompanhamento ==

AC -> S: Consultar histórico de orçamentos
S -> BD: Buscar todos os orçamentos
BD --> S: Retornar histórico completo
S -> AC: Exibir lista com status e detalhes
@enduml
```
---

## Gerenciar Clientes:

@startuml
title Caso de Uso: Gerenciar Clientes

actor "Auxiliar Comercial" as AC
participant "Sistema" as S
participant "Banco de Dados" as BD

== Cadastrar Novo Cliente ==

AC -> S: Acessar módulo de clientes
S -> AC: Exibir lista de clientes cadastrados

AC -> S: Solicitar cadastro de novo cliente
S -> AC: Exibir formulário de cadastro

AC -> S: Preencher dados do cliente\n(nome, CPF/CNPJ, telefone, email, endereço)
S -> BD: Verificar se cliente já existe
BD --> S: Retornar resultado da verificação

S -> BD: Armazenar novo cliente
BD --> S: Confirmação de cadastro
S -> AC: Exibir confirmação de cadastro

== Consultar Clientes ==

AC -> S: Pesquisar cliente por nome/CPF/CNPJ
S -> BD: Buscar clientes conforme critério
BD --> S: Retornar lista de clientes
S -> AC: Exibir resultados da pesquisa

AC -> S: Selecionar cliente para visualizar detalhes
S -> BD: Buscar dados completos do cliente
BD --> S: Retornar dados completos
S -> AC: Exibir perfil completo do cliente

== Editar Cliente ==

AC -> S: Solicitar edição de cliente
S -> BD: Buscar dados atuais do cliente
BD --> S: Retornar dados do cliente
S -> AC: Exibir formulário com dados preenchidos

AC -> S: Atualizar dados do cliente
S -> BD: Validar alterações
BD --> S: Confirmação de validação
S -> BD: Atualizar dados do cliente
BD --> S: Confirmação de atualização
S -> AC: Exibir confirmação de edição

== Histórico do Cliente ==

AC -> S: Consultar histórico do cliente
S -> BD: Buscar orçamentos e obras do cliente
BD --> S: Retornar histórico completo
S -> AC: Exibir histórico de orçamentos e obras

== Desativar/Reativar Cliente ==

AC -> S: Solicitar desativação de cliente
S -> BD: Verificar se cliente tem orçamentos ativos
BD --> S: Retornar situação do cliente
S -> BD: Atualizar status para inativo
BD --> S: Confirmação de desativação
S -> AC: Exibir confirmação de desativação

AC -> S: Solicitar reativação de cliente
S -> BD: Atualizar status para ativo
BD --> S: Confirmação de reativação
S -> AC: Exibir confirmação de reativação

== Relatórios de Clientes ==

AC -> S: Solicitar relatório de clientes
S -> BD: Buscar dados consolidados de clientes
BD --> S: Retornar dados para relatório
S -> AC: Exibir relatório com estatísticas\n(clientes ativos, inativos, frequência)
@enduml

---

## Gerenciar Obras:

@startuml
title Caso de Uso: Gerenciar Obras

actor "Auxiliar Comercial" as AC
participant "Sistema" as S
participant "Banco de Dados" as BD

== Cadastrar Nova Obra ==

AC -> S: Acessar módulo de obras
S -> AC: Exibir lista de obras cadastradas

AC -> S: Solicitar cadastro de nova obra
S -> AC: Exibir formulário de cadastro

AC -> S: Preencher dados da obra\n(nome, endereço, cliente, tipo de obra, data prevista)
S -> BD: Buscar dados do cliente
BD --> S: Retornar dados do cliente
S -> BD: Armazenar nova obra
BD --> S: Confirmação de cadastro
S -> AC: Exibir confirmação de cadastro

== Vincular Orçamento à Obra ==

AC -> S: Selecionar obra para vincular orçamento
S -> BD: Buscar orçamentos disponíveis
BD --> S: Retornar lista de orçamentos
S -> AC: Exibir orçamentos para vínculo

AC -> S: Selecionar orçamento a ser vinculado
S -> BD: Vincular orçamento à obra
BD --> S: Confirmação de vínculo
S -> AC: Exibir confirmação de vínculo

== Consultar Obras ==

AC -> S: Pesquisar obra por nome/cliente/endereço
S -> BD: Buscar obras conforme critério
BD --> S: Retornar lista de obras
S -> AC: Exibir resultados da pesquisa

AC -> S: Selecionar obra para visualizar detalhes
S -> BD: Buscar dados completos da obra
BD --> S: Retornar dados completos (dados da obra + orçamento vinculado)
S -> AC: Exibir detalhes completos da obra

== Acompanhar Status da Obra ==

AC -> S: Consultar status da obra
S -> BD: Buscar status atual da produção
BD --> S: Retornar status (planejada, em produção, concluída)
S -> AC: Exibir status e andamento

AC -> S: Atualizar status da obra
S -> BD: Atualizar status no sistema
BD --> S: Confirmação de atualização
S -> AC: Exibir confirmação

== Editar Dados da Obra ==

AC -> S: Solicitar edição de obra
S -> BD: Buscar dados atuais da obra
BD --> S: Retornar dados da obra
S -> AC: Exibir formulário com dados preenchidos

AC -> S: Atualizar dados da obra
S -> BD: Validar alterações
BD --> S: Confirmação de validação
S -> BD: Atualizar dados da obra
BD --> S: Confirmação de atualização
S -> AC: Exibir confirmação de edição

== Histórico da Obra ==

AC -> S: Consultar histórico completo da obra
S -> BD: Buscar todo o histórico\n(orçamento, produção, materiais, alterações)
BD --> S: Retornar histórico completo
S -> AC: Exibir linha do tempo da obra

== Relatórios de Obras ==

AC -> S: Solicitar relatório de obras
S -> BD: Buscar dados consolidados de obras
BD --> S: Retornar dados para relatório
S -> AC: Exibir relatório com estatísticas\n(obras ativas, concluídas, prazos)
@enduml

---

## Gerenciar Produtos:

@startuml
title Caso de Uso: Gerenciar Produtos

actor "Auxiliar Comercial" as AC
participant "Sistema" as S
participant "Banco de Dados" as BD

== Cadastrar Novo Produto ==

AC -> S: Acessar módulo de produtos
S -> AC: Exibir lista de produtos cadastrados

AC -> S: Solicitar cadastro de novo produto
S -> AC: Exibir formulário de cadastro com categorias

AC -> S: Preencher dados do produto\n(tipo: perfil/vidro/ferragem/acessório, código, descrição, preço, unidade)
S -> BD: Verificar se produto já existe
BD --> S: Retornar resultado da verificação

S -> BD: Armazenar novo produto
BD --> S: Confirmação de cadastro
S -> AC: Exibir confirmação de cadastro

== Consultar Produtos ==

AC -> S: Pesquisar produto por código/descrição/categoria
S -> BD: Buscar produtos conforme critério
BD --> S: Retornar lista de produtos
S -> AC: Exibir resultados da pesquisa

AC -> S: Selecionar produto para visualizar detalhes
S -> BD: Buscar dados completos do produto
BD --> S: Retornar dados completos
S -> AC: Exibir perfil completo do produto

== Editar Produto ==

AC -> S: Solicitar edição de produto
S -> BD: Buscar dados atuais do produto
BD --> S: Retornar dados do produto
S -> AC: Exibir formulário com dados preenchidos

AC -> S: Atualizar dados do produto (preço, descrição, etc.)
S -> BD: Validar alterações
BD --> S: Confirmação de validação
S -> BD: Atualizar dados do produto
BD --> S: Confirmação de atualização
S -> AC: Exibir confirmação de edição

== Gerenciar Categorias e Tipos ==

AC -> S: Acessar categorias de produtos
S -> BD: Buscar categorias existentes
BD --> S: Retornar lista de categorias
S -> AC: Exibir categorias (Perfis, Vidros, Ferragens, Acessórios)

AC -> S: Adicionar nova categoria/subcategoria
S -> BD: Armazenar nova categoria
BD --> S: Confirmação de cadastro
S -> AC: Exibir confirmação

== Atualizar Preços ==

AC -> S: Solicitar atualização em massa de preços
S -> BD: Buscar lista de produtos
BD --> S: Retornar produtos e preços atuais
S -> AC: Exibir tabela de preços

AC -> S: Aplicar reajuste percentual ou valor fixo
S -> BD: Atualizar preços em lote
BD --> S: Confirmação de atualização
S -> AC: Exibir confirmação e resumo das alterações

== Histórico de Preços ==

AC -> S: Consultar histórico de preços do produto
S -> BD: Buscar variações de preço
BD --> S: Retornar histórico de preços
S -> AC: Exibir gráfico/tabela de evolução de preços

== Desativar/Reativar Produto ==

AC -> S: Solicitar desativação de produto
S -> BD: Verificar se produto está em uso
BD --> S: Retornar situação do produto
S -> BD: Atualizar status para inativo
BD --> S: Confirmação de desativação
S -> AC: Exibir confirmação de desativação

AC -> S: Solicitar reativação de produto
S -> BD: Atualizar status para ativo
BD --> S: Confirmação de reativação
S -> AC: Exibir confirmação de reativação

== Relatórios de Produtos ==

AC -> S: Solicitar relatório de produtos
S -> BD: Buscar dados consolidados de produtos
BD --> S: Retornar dados para relatório
S -> AC: Exibir relatório com estatísticas\n(produtos ativos, mais vendidos, categorias)
@enduml

---

## Gerenciar Conta:

@startuml
title Caso de Uso: Gerenciar Conta de Usuário

actor "Usuário" as U
participant "Sistema" as S
participant "Banco de Dados" as BD

== Login no Sistema ==

U -> S: Acessar sistema
S -> U: Exibir tela de login

U -> S: Inserir email e senha
S -> BD: Validar credenciais
BD --> S: Retornar dados do usuário e perfil

alt Credenciais válidas
    S -> U: Redirecionar para dashboard conforme perfil
else Credenciais inválidas
    S -> U: Exibir mensagem de erro
end

== Alterar Dados Pessoais ==

U -> S: Acessar perfil da conta
S -> BD: Buscar dados pessoais do usuário
BD --> S: Retornar dados do usuário
S -> U: Exibir formulário de perfil

U -> S: Atualizar dados pessoais\n(nome, email, telefone)
S -> BD: Validar email único
BD --> S: Confirmação de validação
S -> BD: Atualizar dados pessoais
BD --> S: Confirmação de atualização
S -> U: Exibir confirmação de atualização

== Alterar Senha ==

U -> S: Solicitar alteração de senha
S -> U: Exibir formulário de alteração de senha

U -> S: Inserir senha atual e nova senha
S -> BD: Validar senha atual
BD --> S: Confirmação de validação

alt Senha atual correta
    S -> BD: Atualizar senha
    BD --> S: Confirmação de atualização
    S -> U: Exibir confirmação de alteração
else Senha atual incorreta
    S -> U: Exibir mensagem de erro
end

== Visualizar Perfil e Permissões ==

U -> S: Consultar perfil de acesso
S -> BD: Buscar perfil e permissões do usuário
BD --> S: Retornar perfil e funcionalidades permitidas
S -> U: Exibir perfil e permissões atribuídas

== Logout do Sistema ==

U -> S: Solicitar logout
S -> BD: Registrar horário de logout
BD --> S: Confirmação de registro
S -> U: Redirecionar para tela de login

== Recuperação de Senha ==

U -> S: Solicitar recuperação de senha
S -> U: Exibir formulário de recuperação

U -> S: Inserir email cadastrado
S -> BD: Verificar existência do email
BD --> S: Retornar resultado da verificação

alt Email encontrado
    S -> S: Gerar token de recuperação
    S -> BD: Armazenar token temporário
    BD --> S: Confirmação de armazenamento
    S -> U: Exibir mensagem de instruções\n(email enviado com link)
else Email não encontrado
    S -> U: Exibir mensagem de email não cadastrado
end

U -> S: Acessar link de recuperação com token
S -> BD: Validar token
BD --> S: Retornar validade do token

alt Token válido
    S -> U: Exibir formulário para nova senha
    U -> S: Inserir nova senha
    S -> BD: Atualizar senha
    BD --> S: Confirmação de atualização
    S -> BD: Invalidar token usado
    BD --> S: Confirmação de invalidação
    S -> U: Exibir confirmação de senha alterada
else Token inválido/expirado
    S -> U: Exibir mensagem de link inválido
end
@enduml

---

## Emitir Relatórios Financeiros:

@startuml
title Caso de Uso: Emitir Relatórios Financeiros

actor "Administrador" as ADM
participant "Sistema" as S
participant "Banco de Dados" as BD

ADM -> S: Acessar módulo financeiro
S -> ADM: Exibir menu de relatórios

ADM -> S: Solicitar relatório de contas a pagar
S -> BD: Buscar contas a pagar
BD --> S: Retornar dados financeiros
S --> ADM: Exibir relatório de contas a pagar

ADM -> S: Solicitar relatório de contas a receber
S -> BD: Buscar contas a receber
BD --> S: Retornar dados de recebíveis
S --> ADM: Exibir relatório de contas a receber

ADM -> S: Solicitar fluxo de caixa
S -> BD: Buscar movimentações financeiras
BD --> S: Retornar histórico financeiro
S -> S: Consolidar fluxo de caixa
S --> ADM: Exibir relatório de fluxo de caixa

ADM -> S: Solicitar relatório de faturamento
S -> BD: Buscar dados de orçamentos aprovados
BD --> S: Retornar dados de vendas
S -> S: Calcular faturamento consolidado
S --> ADM: Exibir relatório de faturamento
@enduml

---

## Gerenciar Usuários:

@startuml
title Caso de Uso: Gerenciar Usuários

actor "Administrador" as ADM
participant "Sistema" as S
participant "Banco de Dados" as BD

ADM -> S: Acessar módulo de usuários
S -> BD: Buscar lista de usuários
BD --> S: Retornar dados dos usuários
S --> ADM: Exibir lista de usuários

ADM -> S: Cadastrar novo usuário
S -> ADM: Exibir formulário de cadastro
ADM -> S: Preencher dados do usuário
S -> BD: Verificar se usuário já existe
BD --> S: Retornar resultado da verificação
S -> BD: Armazenar novo usuário
BD --> S: Confirmação de cadastro
S --> ADM: Exibir confirmação

ADM -> S: Editar usuário existente
S -> BD: Buscar dados do usuário
BD --> S: Retornar dados do usuário
S --> ADM: Exibir formulário com dados
ADM -> S: Atualizar dados do usuário
S -> BD: Atualizar registro do usuário
BD --> S: Confirmação de atualização
S --> ADM: Exibir confirmação

ADM -> S: Desativar usuário
S -> BD: Atualizar status do usuário
BD --> S: Confirmação de desativação
S --> ADM: Exibir confirmação
@enduml

---

## Gerenciar Estoque:

@startuml
title Caso de Uso: Gerenciar Estoque

actor "Almoxarife" as ALM
participant "Sistema" as S
participant "Banco de Dados" as BD

ALM -> S: Acessar módulo de estoque
S -> BD: Buscar situação do estoque
BD --> S: Retornar dados do estoque
S --> ALM: Exibir dashboard de estoque

ALM -> S: Consultar estoque específico
S -> BD: Buscar itens do estoque
BD --> S: Retornar lista de itens
S --> ALM: Exibir detalhes dos itens

ALM -> S: Registrar entrada de materiais
S -> BD: Atualizar quantidades em estoque
BD --> S: Confirmação de atualização
S --> ALM: Exibir confirmação

S -> S: Verificar níveis mínimos
S -> BD: Consultar itens abaixo do mínimo
BD --> S: Retornar itens críticos
S --> ALM: Exibir alertas de reposição

ALM -> S: Emitir relatório de estoque
S -> BD: Gerar dados para relatório
BD --> S: Retornar dados consolidados
S --> ALM: Exibir relatório completo
@enduml

---

## Emitir Ordem de Produção: 

@startuml
title Caso de Uso: Emitir Ordem de Produção

participant "Sistema" as S
participant "Banco de Dados" as BD
participant "Setor de Produção" as PROD
participant "Almoxarifado" as ALM

S -> S: Verificar orçamento aprovado
S -> BD: Buscar dados do orçamento aprovado
BD --> S: Retornar dados completos

S -> S: Gerar Ordem de Produção
S -> BD: Armazenar Ordem de Produção
BD --> S: Confirmação de salvamento

S -> PROD: Enviar Ordem de Produção
PROD --> S: Confirmação de recebimento

S -> S: Gerar Relatório de Materiais
S -> BD: Armazenar Relatório de Materiais
BD --> S: Confirmação de salvamento

S -> ALM: Enviar Relatório de Materiais
ALM --> S: Confirmação de recebimento

S -> S: Gerar Lista de Corte
S -> BD: Armazenar Lista de Corte
BD --> S: Confirmação de salvamento

S -> PROD: Enviar Lista de Corte
PROD --> S: Confirmação de recebimento
@enduml

---

## Emitir Relatórios de Obra:

@startuml
title Caso de Uso: Emitir Relatórios de Obra

actor "Auxiliar Comercial" as AC
actor "Almoxarife" as ALM
participant "Sistema" as S
participant "Banco de Dados" as BD
participant "Setor de Produção" as PROD

AC -> S: Acessar obra/orçamento aprovado
S -> BD: Buscar dados da obra (cliente, endereço, especificações)
BD --> S: Retornar dados completos da obra
S --> AC: Exibir detalhes da obra

AC -> S: Solicitar emissão de relatórios de obra

== Geração de Documentos de Produção ==
S -> S: Gerar Ordem de Produção
S -> BD: Armazenar Ordem de Produção
BD --> S: Confirmação de salvamento

S -> S: Gerar Lista de Corte
S -> BD: Armazenar Lista de Corte
BD --> S: Confirmação de salvamento

S -> S: Gerar Plano de Montagem
S -> BD: Armazenar Plano de Montagem
BD --> S: Confirmação de salvamento

== Geração de Documentos de Materiais ==
S -> S: Gerar Relatório de Materiais (perfis, vidros)
S -> BD: Armazenar Relatório de Materiais
BD --> S: Confirmação de salvamento

S -> S: Gerar Lista de Ferragens e Acessórios
S -> BD: Armazenar Lista de Ferragens
BD --> S: Confirmação de salvamento

S -> S: Gerar Relatório de Quantitativos
S -> BD: Armazenar Relatório de Quantitativos
BD --> S: Confirmação de salvamento

== Distribuição para Setores ==
S -> PROD: Enviar pacote de produção\n(Ordem de Produção, Lista de Corte, Plano de Montagem)
PROD --> S: Confirmação de recebimento

S -> ALM: Notificar nova lista de materiais disponível
ALM -> S: Acessar lista de materiais da obra
S -> BD: Buscar documentos de materiais
BD --> S: Retornar Relatório de Materiais, Lista de Ferragens, Quantitativos
S --> ALM: Exibir documentos completos para separação

ALM -> S: Confirmar recebimento dos materiais
S -> BD: Atualizar status dos materiais
BD --> S: Confirmação de atualização

== Finalização ==
S -> BD: Atualizar status da obra para "Em produção"
BD --> S: Confirmação de atualização

S --> AC: Notificar emissão concluída\ncom todos os relatórios gerados
@enduml

---
