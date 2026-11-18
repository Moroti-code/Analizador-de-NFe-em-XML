# Analisador de NF-e

Ferramenta web, 100% local, para extração e organização de dados de NF-e (XML) com foco em **cadastro de produtos e fornecedores** e **pedido de compra ao financeiro**.

**Autor:** Denis Moroti de Souza Campos (denis.campos)
**Versão atual:** v10.0.0
**Data de consolidação:** 14 de novembro de 2026
**Licença:** Uso por licença pessoal — ver seção *Licença de Uso*

---

## 📌 Sobre este README

Este documento é mantido **junto com o código** e serve como:

1. **Registro de autoria e titularidade** da ferramenta
2. **Histórico cronológico** de versões e modificações
3. **Documentação dos termos legais** aplicáveis ao uso
4. **Prova documental** do desenvolvimento independente do autor

Cada versão publicada no GitHub corresponde a um marco documentado abaixo.

> **Nota sobre datas:** todas as versões abaixo foram desenvolvidas, revisadas e consolidadas **em 14 de novembro de 2026**, na mesma sessão de trabalho. O histórico está ordenado pela **sequência de iteração** (v1 → v10), não por diferença de dias. O registro cronológico oficial de cada versão é o **histórico de commits do GitHub**.

---

## 🎯 O que a ferramenta faz

- Lê um ou mais arquivos **XML de NF-e** (layout 4.00) diretamente no navegador
- Extrai dados para **cadastro de produto**: código, descrição, NCM, CEST, CFOP, origem/CST, quantidade, unidade, valor unitário, valor total
- Extrai **ficha completa do emitente** (distribuidor) para cadastro de novos fornecedores: razão social, CNPJ, IE, regime tributário, endereço completo, CEP, telefone
- Apresenta **resumo financeiro agregado**: valor dos produtos, descontos, acréscimos e total da nota
- Exibe **formas de pagamento** (inclusive múltiplas) e **duplicatas/boletos** quando presentes
- Detecta **situação da NF-e** (autorizada, cancelada, evento de cancelamento pendente)
- Compara **código de barras × código do produto** e evita duplicação quando são iguais
- Exporta **CSV** ou permite **copiar tabela** (TSV) pronta para colar em planilha
- Suporta **tema claro/escuro** e layout **responsivo** (retrato e paisagem)
- Processa tudo **localmente no navegador** — nenhum XML é enviado a servidor

---

## 🧭 Escopo e não-escopo

**É escopo desta ferramenta:**
- Apoiar cadastro de produto (SKU, NCM, CEST, CFOP, O/CST, unidade, valor)
- Apoiar cadastro de fornecedor (ficha completa do emitente)
- Fornecer ao financeiro os valores agregados para o pedido de compra (produtos, desconto, acréscimo, total)

**Não é escopo (decisão explícita):**
- Conferência fiscal detalhada (CST de IPI/PIS/COFINS, alíquotas, IBS/CBS, classificação tributária) — atribuição do setor fiscal da empresa
- Validação fiscal completa da NF-e contra a SEFAZ (assinatura, protocolo, correspondência de chave)
- Cálculos fiscais de qualquer natureza

---

## 🛠️ Histórico de versões

> Todas as versões foram desenvolvidas em **14/11/2026**. A ordem abaixo é a **sequência de iteração** (do mais antigo ao mais recente da mesma data).

v12.0.0 — Melhorias de cadastro e produtividade

Interface / layout:
- Cards compactos (3 linhas) em modo retrato com ciclo de 3 cores
- Detecção de modo: automático (largura < 700px), monitor ou celular
- Zoom 75% compatível
- Descrições longas não truncam (whitespace normalizado)
- Unidade não quebra linha quando ≤3 caracteres

Cadastro:
- Marcar produto como cadastrado (checkbox, esmaece)
- Botão "Desmarcar todos"
- Origem: chip com tooltip (não copia)
- CFOP movido para modo tributário
- NCM e CEST formatados na tela (XXXX.XX.XX), crus na cópia
- Numeração #1, #2 visível por linha
- Último copiado destacado (amarelo) até nova cópia
- CNPJ copiável no título da NF-e
- Ação "copiar código+nome" removida (só 🔍)

Cópia / formatação:
- Valores copiados sem R$, com vírgula padrão (configurável para ponto)
- Valor original (10 casas) preservado no tooltip

Blocos:
- Info (chave/natureza/destinatário) recolhido por padrão
- Natureza movida para modo tributário
- Pagamento compacto (só boleto/venc/valor no summary)
- Emitente recolhido por padrão
- Minimizar NF-e inteira (▼) e fechar individual (✕)

Modo tributário (toggle):
- Botão 🎯 na toolbar + config para padrão
- FCI, IPI, PIS, COFINS, alíquotas, ICMS-ST, FCP por produto
- Totais fiscais no rodapé

Configurações:
- Separador decimal (vírgula/ponto)
- Modo de visualização
- Padrão dos blocos (info/pagamento/emitente/tributário)
- Site de pesquisa, URL personalizada

v11.0.0 — Melhorias de usabilidade e produtividade

- Ficha do emitente minimizável, recolhida por padrão
- Consulta por chave de acesso (44 dígitos) com decodificação e link para Portal SEFAZ
- Download individual de XML e impressão/PDF por NF-e
- Campos copiáveis com 1 clique (sem ícone de copiar)
- Ação "copiar código + nome" para pesquisa de imagem
- Pesquisa configurável (Google Images, Google, Bing, Mercado Livre, custom)
- Detecção de campo "marca" (custom tag ou obsCont)
- Modo de visualização manual: monitor / celular / automático
- Remoção de zeros à esquerda em códigos numéricos
- O/CST: apenas a origem recebe cor; CST exibido como texto puro
- Atualização do README e da versão

### v10.0.0 — 14/11/2026
**Adição de disclaimers legais e proteção jurídica**
- Banner bloqueante de aviso no primeiro acesso
- Modal de termos com 5 seções (Autor e Titularidade, Responsabilidade, Uso de IA, Dados e Privacidade, Licença)
- Rodapé permanente com texto legal resumido
- Marcação de versão visível na interface
- **Sem alterações funcionais** em relação à v9

### v9.0.0 — 14/11/2026
**Correções da terceira revisão técnica**
- Classificação de evento de cancelamento em **confirmado** (retorno cStat 135/155) ou **pendente** (sem retorno)
- Evento de cancelamento pendente exibido com banner amarelo, sem marcar a NF-e como cancelada
- Sanitização de TSV contra injeção de fórmulas e contra tab/newline dentro de campos
- Pill de valor neutro quando não há protocolo de autorização

### v8.0.0 — 14/11/2026
**Correções da segunda revisão técnica**
- Detecção de evento de cancelamento via `<procEventoNFe>`
- Sanitização de fórmula também no TSV (antes só o CSV era protegido)
- `csvSafe` checa primeiro caractere significativo após espaços/controles
- Renomeação da coluna `Acréscimos NF` para `Ajuste NF` no CSV

### v7.0.0 — 14/11/2026
**Correções da primeira revisão técnica**
- Preservação da precisão decimal do valor unitário (até 10 casas)
- Suporte a múltiplos pagamentos (`<detPag>`)
- Aviso visual de `cStat` da NF-e (autorizada, cancelada, denegada)
- Exportação de Origem, CST e CSOSN em colunas separadas
- Detecção de upload duplicado pela chave de acesso
- Acréscimos negativos exibidos como "Outras Deduções"

### v6.0.0 — 14/11/2026
**Resumo financeiro**
- Rodapé com Valor dos Produtos, Descontos, Acréscimos e Total da Nota
- Fórmula garantida: `Total = vProd − vDesc + ajuste`
- Colunas extras no CSV: Valor Produtos NF, Descontos NF, Ajuste NF, Total NF

### v5.0.0 — 14/11/2026
**Comparação de código de barras**
- Detecção de `cEAN` igual ao `cProd`
- Célula mostra `= código` em vez de repetir valor
- Coluna inteira oculta quando todos os produtos têm barcode = código
- Célula vazia no CSV quando barcode = código

### v4.0.0 — 14/11/2026
**Ficha do emitente e campos adicionais**
- Card completo do emitente (CNPJ, IE, regime, endereço em 2 linhas, CEP, telefone)
- Cópia individual de cada campo (CNPJ puro, IE, endereço, fone)
- Botão "Copiar ficha" gera bloco pronto para cadastro
- Extração de `xPed` (pedido de compra) e `cEAN` (código de barras)
- Colunas de EAN e unidade tributável aparecem só se o XML trouxer dados

### v3.0.0 — 14/11/2026
**Responsividade e tema**
- Layout adaptável a monitores retrato e paisagem
- Tabela vira cards empilhados em telas estreitas
- Tema claro e escuro com persistência
- Ajustes de impressão para formato compacto

### v2.0.0 — 14/11/2026
**Interface simplificada**
- Remoção do painel de configuração de cores
- O/CST com cores semânticas fixas (azul = origem, verde = CST)
- Tooltip com descrição de cada código

### v1.0.0 — 14/11/2026
**Versão inicial**
- Analisador HTML autônomo
- Parser de XML de NF-e com DOMParser
- Extração de dados de produto
- Interface com painel de configuração de cores por dígito

---

## ⚖️ Termos legais

### 1. Titularidade e autoria

Esta ferramenta é de **propriedade intelectual de Denis Moroti de Souza Campos (denis.campos)**, nos termos da **Lei 9.609/98 (Lei do Software)** e da **Lei 9.610/98 (Lei de Direitos Autorais)**.

Foi desenvolvida de forma **independente**, em ambiente e equipamento **pessoais**, **fora do horário de trabalho** e **sem utilização de dados, sistemas ou recursos de qualquer empresa**.

A utilização desta ferramenta por qualquer pessoa ou empresa configura **licença de uso**, de caráter **não exclusivo, não transferível, revogável e gratuito**, limitada a **uso interno**, e **não implica cessão, total ou parcial, dos direitos autorais ou de propriedade intelectual**.

### 2. Limitação de responsabilidade

A ferramenta é fornecida **"no estado em que se encontra" ("as is")**, **sem garantia de qualquer espécie**, expressa ou implícita, incluindo, mas não se limitando a, garantias de comerciabilidade, adequação a um propósito específico, ausência de erros ou de vulnerabilidades.

Na máxima extensão permitida pela legislação aplicável, **o autor não será responsável** por quaisquer danos diretos, indiretos, incidentais, especiais, consequenciais ou punitivos — incluindo lucros cessantes, perda de dados, interrupção de atividade, erros de cadastro, pagamentos indevidos, autuações fiscais ou prejuízos de qualquer natureza — decorrentes do uso, do mau uso ou da impossibilidade de uso da ferramenta, **ainda que o autor tenha sido avisado da possibilidade de tais danos**.

**A responsabilidade final pela conferência dos dados e pelas decisões tomadas com base neles é integralmente do usuário e da empresa utilizadora.**

### 3. Uso de inteligência artificial

Esta ferramenta foi **desenvolvida com auxílio de inteligência artificial** e **supervisionada, revisada e validada por responsável humano identificado** (Denis Moroti de Souza Campos — denis.campos).

O código foi revisado e testado antes da disponibilização, mas **pode conter erros, imprecisões ou vulnerabilidades**.

A inteligência artificial **não detém responsabilidade legal** sobre a ferramenta. A responsabilidade pela revisão, aprovação e uso é **humana**, e recai sobre o usuário e a empresa utilizadora.

### 4. Dados e privacidade

Esta ferramenta processa os arquivos **exclusivamente no navegador do usuário**. Nenhum dado é enviado a servidores, serviços externos ou terceiros. Os arquivos XML **não são armazenados, transmitidos ou compartilhados** pela ferramenta.

Ainda assim, **a responsabilidade pela guarda, pelo tratamento e pela proteção dos dados pessoais e fiscais contidos nos XMLs é integralmente do usuário e da empresa utilizadora**, nos termos da **LGPD (Lei 13.709/18)** e da legislação aplicável.

### 5. Licença de uso e restrições

**É vedado**, sem autorização prévia e por escrito do autor:

- Copiar, modificar, distribuir, sublicenciar, vender, alugar ou disponibilizar a ferramenta a terceiros
- Utilizar a ferramenta em **outras empresas do grupo empresarial**, em filiais, coligadas ou controladas, sem autorização formal
- Utilizar a ferramenta para finalidades ilícitas, fraudulentas ou que violem direitos de terceiros
- Remover, ocultar ou alterar avisos de autoria, disclaimers ou marcas

**O uso em outras empresas do grupo depende de autorização prévia e por escrito do autor (Denis Moroti de Souza Campos).**

---

## 📬 Canal de reporte de falhas

Encontrou erro, imprecisão, vulnerabilidade ou comportamento inesperado?

**Comunique imediatamente ao autor antes de aprovar, distribuir ou ampliar o uso da ferramenta.**

- Autor: Denis Moroti de Souza Campos (denis.campos)
- Preferencialmente por **issue no repositório** ou **contato direto** com o autor

Relatos de falhas são **bem-vindos** e serão tratados com prioridade. A colaboração do usuário na identificação de problemas é o principal mecanismo de melhoria contínua da ferramenta.

---

### Política de segurança

Vulnerabilidades de segurança são tratadas com **prioridade máxima**. 
Se você identificar uma falha que possa comprometer dados, integridade 
ou disponibilidade, **não abra issue pública** — entre em contato 
diretamente com o autor para tratamento reservado antes da divulgação.

---

## 🔒 Nota sobre o desenvolvimento

- Desenvolvido em **14/11/2026**, em ambiente pessoal, **fora do horário de trabalho**
- **Sem utilização de dados, sistemas, equipamentos ou recursos** de qualquer empresa
- Dados de teste originais: XML de compra pessoal do autor no Mercado Livre
- **Sem vínculo com projeto interno** de qualquer empregador
- Código mantido neste repositório como **registro público de autoria e histórico**

---

## 🧪 Como usar

1. Baixe o arquivo `analisadornfe.html`
2. Abra no navegador (duplo clique)
3. Aceite o aviso legal no primeiro acesso
4. Arraste um ou mais XMLs de NF-e
5. Confira os dados exibidos
6. Use **Copiar tabela** ou **Exportar CSV** conforme necessário

**Requisitos:** navegador moderno (Chrome, Edge, Firefox, Safari). Não requer instalação, servidor, internet ou conta.

---

## 🚫 Limitações conhecidas

- Não valida assinatura digital da NF-e
- Não verifica a nota em tempo real na SEFAZ
- Não substitui o DANFE (PDF) para fins fiscais
- Não detecta todos os eventos possíveis (só cancelamento via `110111`)
- Não lê PDFs — apenas XMLs
- Não faz conferência fiscal detalhada por decisão de escopo

---

## 📄 Licença

**Todos os direitos reservados ao autor.** Uso por licença, não cessão. Consulte a seção *5. Licença de Uso e Restrições* acima para os termos completos.

© 2026 Denis Moroti de Souza Campos (denis.campos)
