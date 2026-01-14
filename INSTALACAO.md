# Instalação e Configuração do Módulo NFS-e (WHMCS)

Este documento descreve **passo a passo** como instalar e configurar o módulo **Notas Fiscais (NFS-e)** no WHMCS, desde o envio dos arquivos via FTP até o preenchimento completo dos campos do módulo definidos em `Nfse_config()`.

---

## 1. Pré-requisitos

Antes de iniciar, verifique se o ambiente atende aos requisitos abaixo:

- WHMCS funcionando corretamente
- PHP com as extensões habilitadas:
  - `curl`
  - `openssl`
  - `zip` (ZipArchive)
- Acesso FTP ou SFTP ao servidor
- Certificado digital A1 (`.pfx`)
- Código IBGE do município do prestador
- Chave de licença válida do módulo (se aplicável)

---

## 2. Envio dos Arquivos via FTP

### 2.1 Caminho correto do módulo

Envie a pasta **Nfse** para o seguinte diretório do WHMCS:

/public_html/modules/addons/Nfse/


### 2.2 Estrutura esperada

modules/
└── addons/
└── Nfse/
├── Nfse.php
├── NfseCore.php
├── hooks.php
├── lang/
│ └── portuguese-br.php
├── lib/
├── notas/
├── sql/
│ └── install.sql
└── templates/

> **Importante:**  
> As pastas `notas`, `lib`, `templates` e `lang` devem possuir permissão **755**.

---

## 3. Ativação do Módulo no WHMCS

1. Acesse o **Admin do WHMCS**
2. Vá em **Configurações → Addon Modules**
3. Localize **Notas Fiscais (NFS-e)**
4. Clique em **Ativar**
5. Defina os grupos de administradores com permissão

Durante a ativação:
- As tabelas do banco de dados são criadas
- O template de e-mail **Nota Fiscal** é criado automaticamente (se não existir)

---

## 4. Acessando a Configuração do Módulo

1. Vá em **Configurações → Addon Modules**
2. Clique em **Configurar** no módulo **Notas Fiscais (NFS-e)**

A seguir está a explicação de cada grupo de campos conforme definido em `Nfse_config()`.

---

## 5. Configuração dos Campos

### 5.1 Licença

#### Chave da Licença
- **Campo:** `licensekey`
- Informe a chave de licença fornecida
- O status da licença será exibido automaticamente

---

### 5.2 Dados da Empresa (Prestador)

#### CNPJ da Empresa
- **Campo:** `cnpj_prestador`
- Apenas números  
  Exemplo: `12345678000199`

#### E-mail da Empresa
- **Campo:** `email_prestador`
- E-mail oficial do prestador

#### Telefone da Empresa
- **Campo:** `telefone_prestador`
- Apenas números com DDD  
  Exemplo: `11999998888`

#### Código do Município (IBGE)
- **Campo:** `codigo_municipio`
- Apenas números  
- Consulte em:  
  https://www.ibge.gov.br/explica/codigos-dos-municipios.php

---

### 5.3 Nota Fiscal

#### Endpoint da API Nacional
- **Campo:** `api_base_url`
- Valor padrão:

https://sefin.nfse.gov.br/SefinNacional

#### Código de Serviço Padrão (LC 116)
- **Campo:** `subitem_lc116_padrao`
- Apenas números
- Utilizado quando não houver código específico por produto
- Consulta: https://www.gov.br/nfse

#### Série da NFS-e
- **Campo:** `serie_nf`
- Exemplo: `900`

#### Caminho do Certificado A1
- **Campo:** `cert_path`
- Caminho completo do arquivo `.pfx`

/home/usuario/certificados/certificado.pfx

#### Senha do Certificado
- **Campo:** `cert_password`
- Deixe em branco se não houver senha

---

### 5.4 Campos Personalizados do Cliente

#### Campo CPF/CNPJ (Obrigatório)
- **Campo:** `customfield_cpf_cnpj`
- Selecione o custom field que armazena CPF ou CNPJ

> Sem este campo configurado, a emissão da NFS-e não funcionará.

#### Campo Inscrição Municipal (Opcional)
- **Campo:** `customfield_im_cliente`
- Utilizado apenas para clientes **CNPJ**

---

### 5.5 Descrição da Nota

#### Exibir Número da Fatura
- **Campo:** `exibir_numero_fatura_descricao`
- Exemplo exibido: `Fatura #123`

#### Descrição Adicional
- **Campo:** `descricao_manual_fatura`
- Texto opcional exibido entre o número da fatura e os itens

---

### 5.6 Impostos

#### Retenção de ISS Padrão (%)
- **Campo:** `iss_retencao`
- Exemplo:

2.00


#### ISS Personalizado por Cliente
- **Campo:** `customfield_iss_cliente`
- Sobrescreve o ISS padrão quando preenchido

---

### 5.7 Configurações de Emissão

#### Modo de Emissão
- **Campo:** `modo_emissao`
- Opções:
  - `Manual`
  - `Imediato`

---

### 5.8 Modo Imediato – Filtros

#### Gateways de Pagamento
- **Campo:** `gateways_habilitados_raw`
- Define quais meios de pagamento disparam a emissão automática

#### Grupos de Clientes
- **Campo:** `clientgroups_habilitados_raw`
- Permite restringir a emissão automática por grupo
- Opção **Sem Grupo** inclui clientes sem grupo definido

---

### 5.9 Outras Opções

#### Criar Tarefas em Caso de Erro
- **Campo:** `criar_todo_erro`
- Cria um *To Do* no WHMCS quando ocorre erro na emissão

#### Enviar E-mail ao Cliente
- **Campo:** `enviar_email`
- Envia automaticamente o e-mail da nota fiscal

#### DEBUG
- **Campo:** `debug`
- Exibe o erro real retornado pela API  
- Use apenas para diagnóstico

---

## 6. Configuração de Subitens (Códigos de Serviço)

1. Acesse o módulo **Notas Fiscais (NFS-e)**
2. Vá até a aba **Código de Serviço**
3. Configure:
   - Código específico para **Domínios**
   - Código específico por **Produto/Serviço**
4. Campos vazios utilizarão o código padrão

---

## 7. Validação Final

- Gere uma fatura de teste
- Emita a NFS-e
- Verifique:
  - XML gerado corretamente
  - Arquivo salvo em `modules/addons/Nfse/notas/MM-AAAA`
  - E-mail enviado (se habilitado)
  - Registro criado na tabela `tblnotasfiscais`

---

## 8. Suporte

Para dúvidas ou suporte técnico:

🔗 https://cliente.ddrhost.com.br/

---
