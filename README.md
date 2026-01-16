# Módulo de Notas Fiscais (NFS-e) para WHMCS via API Nacional

> Automatize a emissão de **NFS-e** no WHMCS com integração direta ao **Ambiente Nacional** (Sefin Nacional/nfse.gov.br).

Este módulo integra o WHMCS à **API Nacional de NFS-e**, permitindo operar a rotina completa de emissão de notas fiscais de serviço **SEM DEPENDER DE TERCEIROS**, **SEM COBRANÇA POR NOTA FISCAL**: emissão manual ou imediata, cancelamento, download do XML e reenvio de e-mail, com controles por **gateway**, **grupo de cliente** e mapeamento de **Subitem** por produto e por domínios.

![](nota2.jpg)

## Principais Recursos

* [x] Emissão de NFS-e diretamente no WHMCS via **API Nacional**
* [x] **Emissão manual** (ação sob demanda no Admin)
* [x] **Emissão imediata** (após pagamento, conforme regras do módulo)
* [x] **Cancelamento** de NFS-e (quando status = emitida)
* [x] **Download do XML** da NFS-e (Admin e ClientArea)
* [x] **Reenvio de e-mail** da NFS-e pelo Admin
* [x] **Painel de listagem** de notas emitidas no Admin (com busca e ordenação)
* [x] **Acompanhamento de status**: Emitida, Cancelada, Erro
* [x] **Subitem** configurável:
  * [x] Subitem padrão global
  * [x] Subitem por Produto/Serviço
  * [x] Subitem para **Domínios** (Registro/Transferência/Renovação)

### Controles e Regras Operacionais
* [x] Restrições de emissão automática por **meios de pagamento (Gateways)**
* [x] Restrições de emissão automática por **Grupos de Clientes**
* [x] Mapeamento do **CPF/CNPJ do cliente** via Campo Personalizado (Custom Field)
* [x] Subitem vazio utiliza o **Subitem Padrão** definido nas configurações

### Operação no Admin
* [x] Botões de ação rápida na listagem:
  * [x] Emitir NFS-e
  * [x] Cancelar NFS-e
  * [x] Baixar XML
  * [x] Reenviar E-mail
* [x] Regras automáticas de habilitar/desabilitar botões por status da nota
* [x] Ordenação e pesquisa (DataTables) para operação em volume

![](nota1.jpg)

### Armazenamento e Recuperação do XML
* [x] Suporte a XML retornado pela API em formato compactado (ex.: `nfseXmlGZipB64`)
* [x] Extração automática do XML para download quando necessário

### Auditoria e Diagnóstico
* [x] Registro de eventos em **Activity Log** (sucesso, falhas, cancelamento)
* [x] Opção de criar **To-Do** no WHMCS quando ocorrer erro de emissão/cancelamento (configurável)
* [x] Preserva dados relevantes da nota no banco mesmo em fluxos de erro (para retentativas e auditoria)

### Subitem — Diferencial do Módulo

A aba **Subitem** permite controlar com precisão a classificação do serviço na NFS-e:

* [x] **Domínios** com subitem exclusivo (Registro/Transferência/Renovação)
* [x] Subitem por **Produto/Serviço** (catálogo do WHMCS)
* [x] Herança do **Subitem Padrão** quando o campo estiver em branco

### E-mails

* [x] Template “**Nota Fiscal**” (WHMCS Email Templates)
* [x] Envio/reenvio com **chave de acesso** e link para consulta pública
* [x] Reenvio sob demanda pelo Admin



## Referências

- Portal de Consulta Pública (NFS-e Nacional): https://www.nfse.gov.br/consultaPublica



## Compra

- DDR Host: [https://cliente.ddrhost.com.br/cart.php?a=add&pid=281](https://cliente.ddrhost.com.br/cart.php?a=add&pid=281)
