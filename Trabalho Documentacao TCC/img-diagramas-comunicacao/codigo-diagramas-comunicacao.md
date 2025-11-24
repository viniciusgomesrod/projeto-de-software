## Gerenciar Orçamento:

```plantuml
@startuml
title UC-01 - Comunicacao - Gerenciar Orçamento

[**Auxiliar Comercial**] -> [Sistema]: 1. solicitarOrcamento()
[**Auxiliar Comercial**] -> [Modulo Orcamentos]: 2. inserirDados()
[**Auxiliar Comercial**] -> [Modulo Orcamentos]: 3. selecionarProdutos()
[**Auxiliar Comercial**] -> [Modulo Orcamentos]: 4. salvarOrcamento()
[**Auxiliar Comercial**] -> [Modulo Orcamentos]: 5. aprovarOrcamento()

[Modulo Orcamentos] -> [Banco Dados]: 6. consultarDados()
[Banco Dados] -> [Modulo Orcamentos]: 7. retornarDados()

[Modulo Orcamentos] -> [Modulo Orcamentos]: 8. calcularPreco()
[Modulo Orcamentos] -> [**Auxiliar Comercial**]: 9. exibirOrcamento()

[Modulo Orcamentos] -> [Modulo Producao]: 10. gerarDocumentos()
[Modulo Producao] -> [Banco Dados]: 11. salvarDocumentos()

[Modulo Orcamentos] -> [Modulo Estoque]: 12. gerarMateriais()
[Modulo Estoque] -> [Banco Dados]: 13. salvarMateriais()

[Modulo Orcamentos] -> [**Auxiliar Comercial**]: 14. notificarSucesso()
@enduml
```

---

## Emitir Relatórios de Obra:

```plantuml
@startuml
title UC-02 - Comunicacao - Emitir Relatórios de Obra

[**Auxiliar Comercial**] -> [Sistema]: 1. acessarObra()
[**Auxiliar Comercial**] -> [Modulo Obras]: 2. solicitarRelatorios()

[Modulo Obras] -> [Banco Dados]: 3. buscarDadosObra()
[Banco Dados] -> [Modulo Obras]: 4. retornarDados()

[Modulo Obras] -> [Modulo Producao]: 5. gerarProducao()
[Modulo Producao] -> [Banco Dados]: 6. salvarDocumentos()

[Modulo Obras] -> [Modulo Estoque]: 7. gerarMateriais()
[Modulo Estoque] -> [Banco Dados]: 8. salvarMateriais()

[Modulo Producao] -> [**Almoxarife**]: 9. notificarMateriais()
[**Almoxarife**] -> [Modulo Estoque]: 10. acessarListas()

[Modulo Estoque] -> [Banco Dados]: 11. buscarMateriais()
[Banco Dados] -> [Modulo Estoque]: 12. retornarMateriais()

[Modulo Estoque] -> [**Almoxarife**]: 13. exibirDocumentos()
[**Almoxarife**] -> [Modulo Estoque]: 14. confirmarSeparacao()

[Modulo Obras] -> [**Auxiliar Comercial**]: 15. notificarConclusao()
@enduml
```

---

## Gerenciar Clientes:

```plantuml
@startuml
title UC-03 - Comunicacao - Gerenciar Clientes

[**Auxiliar Comercial**] -> [Sistema]: 1. acessarClientes()
[**Auxiliar Comercial**] -> [Modulo Clientes]: 2. cadastrarCliente()
[**Auxiliar Comercial**] -> [Modulo Clientes]: 3. pesquisarCliente()
[**Auxiliar Comercial**] -> [Modulo Clientes]: 4. editarCliente()

[Modulo Clientes] -> [Banco Dados]: 5. verificarCliente()
[Banco Dados] -> [Modulo Clientes]: 6. retornarVerificacao()

[Modulo Clientes] -> [Banco Dados]: 7. salvarCliente()
[Banco Dados] -> [Modulo Clientes]: 8. confirmarSalvamento()

[Modulo Clientes] -> [Banco Dados]: 9. buscarClientes()
[Banco Dados] -> [Modulo Clientes]: 10. retornarLista()

[Modulo Clientes] -> [**Auxiliar Comercial**]: 11. exibirResultados()
[Modulo Clientes] -> [**Auxiliar Comercial**]: 12. exibirConfirmacao()
@enduml
```

---

## Gerenciar Obras:

```plantuml
@startuml
title UC-04 - Comunicacao - Gerenciar Obras

[**Auxiliar Comercial**] -> [Sistema]: 1. acessarObras()
[**Auxiliar Comercial**] -> [Modulo Obras]: 2. cadastrarObra()
[**Auxiliar Comercial**] -> [Modulo Obras]: 3. vincularOrcamento()
[**Auxiliar Comercial**] -> [Modulo Obras]: 4. consultarStatus()

[Modulo Obras] -> [Banco Dados]: 5. buscarDados()
[Banco Dados] -> [Modulo Obras]: 6. retornarDados()

[Modulo Obras] -> [Modulo Orcamentos]: 7. buscarOrcamentos()
[Modulo Orcamentos] -> [Banco Dados]: 8. consultarOrcamentos()
[Banco Dados] -> [Modulo Orcamentos]: 9. retornarOrcamentos()
[Modulo Orcamentos] -> [Modulo Obras]: 10. retornarLista()

[Modulo Obras] -> [Banco Dados]: 11. salvarObra()
[Banco Dados] -> [Modulo Obras]: 12. confirmarSalvamento()

[Modulo Obras] -> [**Auxiliar Comercial**]: 13. exibirStatus()
[Modulo Obras] -> [**Auxiliar Comercial**]: 14. exibirConfirmacao()
@enduml
```

---

## Gerenciar Produtos:

```plantuml
@startuml
title UC-05 - Comunicacao - Gerenciar Produtos

[**Auxiliar Comercial**] -> [Sistema]: 1. acessarProdutos()
[**Auxiliar Comercial**] -> [Modulo Produtos]: 2. cadastrarProduto()
[**Auxiliar Comercial**] -> [Modulo Produtos]: 3. pesquisarProduto()
[**Auxiliar Comercial**] -> [Modulo Produtos]: 4. editarProduto()
[**Auxiliar Comercial**] -> [Modulo Produtos]: 5. atualizarPrecos()

[Modulo Produtos] -> [Banco Dados]: 6. verificarProduto()
[Banco Dados] -> [Modulo Produtos]: 7. retornarVerificacao()

[Modulo Produtos] -> [Banco Dados]: 8. salvarProduto()
[Banco Dados] -> [Modulo Produtos]: 9. confirmarSalvamento()

[Modulo Produtos] -> [Banco Dados]: 10. buscarProdutos()
[Banco Dados] -> [Modulo Produtos]: 11. retornarLista()

[Modulo Produtos] -> [Banco Dados]: 12. atualizarPrecosLote()
[Banco Dados] -> [Modulo Produtos]: 13. confirmarAtualizacao()

[Modulo Produtos] -> [**Auxiliar Comercial**]: 14. exibirResultados()
[Modulo Produtos] -> [**Auxiliar Comercial**]: 15. exibirConfirmacao()
@enduml
```

---

## Gerenciar Conta:

```plantuml
@startuml
title UC-06 - Comunicacao - Gerenciar Conta

[**Usuário**] -> [Sistema]: 1. login()
[**Usuário**] -> [Modulo Autenticacao]: 2. alterarSenha()
[**Usuário**] -> [Modulo Usuarios]: 3. editarPerfil()

[Modulo Autenticacao] -> [Banco Dados]: 4. validarCredenciais()
[Banco Dados] -> [Modulo Autenticacao]: 5. retornarValidacao()

[Modulo Autenticacao] -> [Banco Dados]: 6. atualizarSenha()
[Banco Dados] -> [Modulo Autenticacao]: 7. confirmarAtualizacao()

[Modulo Usuarios] -> [Banco Dados]: 8. buscarDadosUsuario()
[Banco Dados] -> [Modulo Usuarios]: 9. retornarDados()

[Modulo Usuarios] -> [Banco Dados]: 10. atualizarPerfil()
[Banco Dados] -> [Modulo Usuarios]: 11. confirmarAtualizacao()

[Modulo Autenticacao] -> [**Usuário**]: 12. redirecionarDashboard()
[Modulo Usuarios] -> [**Usuário**]: 13. exibirConfirmacao()
@enduml
```

---

## Gerenciar Usuários:

```plantuml
@startuml
title UC-07 - Comunicacao - Gerenciar Usuários

[**Administrador**] -> [Sistema]: 1. acessarUsuarios()
[**Administrador**] -> [Modulo Usuarios]: 2. cadastrarUsuario()
[**Administrador**] -> [Modulo Usuarios]: 3. editarUsuario()
[**Administrador**] -> [Modulo Usuarios]: 4. desativarUsuario()

[Modulo Usuarios] -> [Banco Dados]: 5. verificarUsuario()
[Banco Dados] -> [Modulo Usuarios]: 6. retornarVerificacao()

[Modulo Usuarios] -> [Banco Dados]: 7. salvarUsuario()
[Banco Dados] -> [Modulo Usuarios]: 8. confirmarSalvamento()

[Modulo Usuarios] -> [Banco Dados]: 9. buscarUsuarios()
[Banco Dados] -> [Modulo Usuarios]: 10. retornarLista()

[Modulo Usuarios] -> [Banco Dados]: 11. atualizarStatus()
[Banco Dados] -> [Modulo Usuarios]: 12. confirmarAtualizacao()

[Modulo Usuarios] -> [**Administrador**]: 13. exibirLista()
[Modulo Usuarios] -> [**Administrador**]: 14. exibirConfirmacao()
@enduml
```

---

## Gerenciar Estoque:

```plantuml
@startuml
title UC-08 - Comunicacao - Gerenciar Estoque

[**Almoxarife**] -> [Sistema]: 1. acessarEstoque()
[**Almoxarife**] -> [Modulo Estoque]: 2. consultarEstoque()
[**Almoxarife**] -> [Modulo Estoque]: 3. registrarEntrada()
[**Almoxarife**] -> [Modulo Estoque]: 4. emitirRelatorio()

[Modulo Estoque] -> [Banco Dados]: 5. buscarSituacao()
[Banco Dados] -> [Modulo Estoque]: 6. retornarDados()

[Modulo Estoque] -> [Banco Dados]: 7. atualizarQuantidades()
[Banco Dados] -> [Modulo Estoque]: 8. confirmarAtualizacao()

[Modulo Estoque] -> [Banco Dados]: 9. gerarDadosRelatorio()
[Banco Dados] -> [Modulo Estoque]: 10. retornarDadosConsolidados()

[Modulo Estoque] -> [**Almoxarife**]: 11. exibirEstoque()
[Modulo Estoque] -> [**Almoxarife**]: 12. exibirRelatorio()
[Modulo Estoque] -> [**Almoxarife**]: 13. exibirAlertas()
@enduml
```

---

## Emitir Relatórios Financeiros:

```plantuml
@startuml
title UC-09 - Comunicacao - Emitir Relatórios Financeiros

[**Administrador**] -> [Sistema]: 1. acessarFinanceiro()
[**Administrador**] -> [Modulo Financeiro]: 2. solicitarRelatorios()

[Modulo Financeiro] -> [Banco Dados]: 3. buscarDadosFinanceiros()
[Banco Dados] -> [Modulo Financeiro]: 4. retornarDados()

[Modulo Financeiro] -> [Modulo Financeiro]: 5. processarGraficos()
[Modulo Financeiro] -> [Modulo Financeiro]: 6. consolidarDados()

[Modulo Financeiro] -> [**Administrador**]: 7. exibirRelatorios()
[Modulo Financeiro] -> [**Administrador**]: 8. exibirGraficos()
@enduml
```

---

## Emitir Relatórios Comerciais:

```plantuml
@startuml
title UC-10 - Comunicacao - Emitir Relatórios Comerciais

[**Auxiliar Comercial**] -> [Sistema]: 1. acessarComercial()
[**Auxiliar Comercial**] -> [Modulo Comercial]: 2. solicitarRelatorios()

[Modulo Comercial] -> [Banco Dados]: 3. buscarDadosComerciais()
[Banco Dados] -> [Modulo Comercial]: 4. retornarDados()

[Modulo Comercial] -> [Modulo Comercial]: 5. processarEstatisticas()
[Modulo Comercial] -> [Modulo Comercial]: 6. consolidarVendas()

[Modulo Comercial] -> [**Auxiliar Comercial**]: 7. exibirRelatorios()
[Modulo Comercial] -> [**Auxiliar Comercial**]: 8. exibirMetricas()
@enduml
```

---

## Consultar Estoque:

```plantuml
@startuml
title UC-12 - Comunicacao - Consultar Estoque

[**Almoxarife**] -> [Sistema]: 1. acessarEstoque()
[**Almoxarife**] -> [Modulo Estoque]: 2. consultarItens()
[**Almoxarife**] -> [Modulo Estoque]: 3. filtrarCategoria()

[Modulo Estoque] -> [Banco Dados]: 4. buscarItensEstoque()
[Banco Dados] -> [Modulo Estoque]: 5. retornarItens()

[Modulo Estoque] -> [Banco Dados]: 6. verificarNiveis()
[Banco Dados] -> [Modulo Estoque]: 7. retornarAlertas()

[Modulo Estoque] -> [**Almoxarife**]: 8. exibirItens()
[Modulo Estoque] -> [**Almoxarife**]: 9. exibirAlertas()
[Modulo Estoque] -> [**Almoxarife**]: 10. exibirEstatisticas()
@enduml
```

---
