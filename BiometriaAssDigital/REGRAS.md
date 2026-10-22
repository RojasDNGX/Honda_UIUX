# Biometria / Assinatura Digital — Regras do processo

Registro das regras de negócio do fluxo **atual** de biometria facial e assinatura digital, informadas pelo time.

- **Réplica** (`biometria-atual.html`): a réplica do fluxo atual precisa respeitar todas as regras abaixo.
- **Remake** (`biometria-remake.html`): cada regra traz uma nota de impacto, que diz o que pode ou não ser mudado no fluxo remodelado.

## Contexto: como se chega ao fluxo

> Este trecho é o **caminho até o fluxo** e não faz parte dele. Não entra na réplica nem no remake, a não ser que algo dele seja informado mais tarde como regra.

- **Negócio:** concessão de financiamento para o proponente comprar um veículo (carro ou motocicleta) numa concessionária Honda.
- **Quem dispara:** o colaborador da concessionária que está abrindo a proposta de financiamento para o proponente.
- **Quando:** num certo momento da abertura da proposta, o colaborador envia ao proponente um link para fazer a assinatura digital.
- **Como o link chega ao proponente:**
  - por **QR Code**; ou
  - por **envio remoto** via SMS, e-mail ou WhatsApp, com um **token de acesso**.
- **A partir daí:** o proponente entra, no próprio celular, no fluxo de assinatura digital e biometria facial. Esse fluxo é o que vamos replicar e melhorar.

## Mapa de telas do fluxo atual

Prints de referência: `C:\Users\Thiago.Rojas\Downloads\UX_Biometria` (Android, 720x1612).

**Convenção de nomes dos prints:** um sufixo `-1`, `-2`, … depois do número de origem (ex.: `017-1`) marca uma **ramificação condicional**, como um "se" num diagrama. A ramificação só acontece quando a condição é atendida. Ela sai da tela de origem, percorre `-1`, `-2`, … em ordem e, depois da última, volta para a sequência principal na tela seguinte à de origem.
> **Estados de erro** (confirmado): quando os prints `-N` de uma mesma origem são **erros alternativos** (ex.: 000-1 e 000-2, 006-3/4/5, 009-1/009-2), cada um é um "se" independente e volta para a própria tela de origem para nova tentativa, em vez de formar uma sequência.

**Dois padrões visuais:** as telas "Honda" (cabeçalho com logo, fundo cinza, botões retos em vermelho, rodapé "Honda Serviços Financeiros") se alternam com as telas do **componente de captura** (fundo branco, sem logo, X no canto, botões arredondados de largura total). Estas são: 004, 006-1 a 006-5, 007 a 011 e 016-2.

### Entrada e lista de assinantes

| # | Tela | Conteúdo observado |
|---|------|--------------------|
| 000 | **Identificação** (só envio remoto) | Campo "Digite o Token:" (6 dígitos) e botão CONTINUAR. Abaixo, "Dicas para facilitar o processo de assinatura." com botão "CLIQUE AQUI E CONFIRA". |
| 000-1 | Erro: token incorreto | Mensagem em vermelho "Código incorreto, tente novamente." e campo limpo. |
| 000-2 | Erro: token incompleto | Mensagem em vermelho "O Token deve possuir 6 dígitos". |
| 000-V | Vídeo tutorial (_sem print_) | Abre pelo "CLIQUE AQUI E CONFIRA". Vídeo 16:9 centralizado na vertical da tela e botão **"Entendi"** abaixo, que volta para a 000. |
| 001 | **Assinantes Concessionária** (só presencial) | Tabela NOME / CPF/CNPJ com link "Assinar" em cada assinante e botão "Atualizar Lista". |
| 001-1 | Lista com parte não liberada | 2 assinantes: o primeiro com "Assinar", o segundo com **"Aguarde"** (texto sem link). |
| 001-2 | Lista com todos liberados | 2 assinantes, os dois com "Assinar". |

### Biometria facial

| # | Tela | Conteúdo observado |
|---|------|--------------------|
| 002 | **Captura da Foto** (consentimento) | Termo de autorização da captura da imagem facial (identificação, prevenção a fraude, compartilhamento com o grupo Honda e terceiros). Switch "Li e aceito os termos" e botão CONTINUAR. |
| 003 | **Modal "Dicas importantes para Captura da Selfie"** | 5 dicas com ícone: autorizar a câmera, câmera no nível dos olhos, local iluminado, sem acessórios (óculos, boné, máscara, chapéu), não sorrir nem fazer careta. Botão "OK, Entendi" e X para fechar. |
| 004 | **Captura facial (liveness)** | Componente de captura. São **2 capturas seguidas**: a 1ª normal e a 2ª com o **rosto mais próximo** (sem print, mesmo visual). O indicador de 2 bolinhas no topo marca cada captura concluída. Texto "Tente não se mexer", moldura oval com progresso verde e check. Falha: ver 004-1. |
| 004-1 | Falha na captura facial (_sem print_) | Layout da 009-2 ("Atenção!") com o texto "Não foi possível realizar a captura facial. Por favor, tente novamente." e botão "Tentar novamente", que volta para a 003 (R10). |
| 005 | **Processando** | Spinner vermelho e "Aguarde um instante...". |

### Documento de identificação

| # | Tela | Conteúdo observado |
|---|------|--------------------|
| 006 | **Escolha da forma de captura** | "Agora vamos capturar seu documento de identificação. Escolha Forma de Captura". Dois botões: **Documentos Digitais → "CNH Digital"** e **Documentos Físicos → "RG, CNH, DNI, RNE e CIN"**. |
| 006-1 | CNH Digital: instruções | "Envio de documento digital": 1) acessar a pasta "Arquivos"; 2) localizar o documento digital válido; 3) conferir se está em **PDF**; 4) enviar o arquivo **original**, prints de tela não são aceitos. Botão "Escolher arquivo". |
| 006-2 | CNH Digital: adicionar arquivo | "Adicione o documento — Envie um arquivo único no formato PDF com tamanho máximo de 4MB". Card "Escolher arquivo / Toque para selecionar", link "Como enviar meu documento digital" (ⓘ) e seta de voltar. |
| 006-3 | Erro: páginas demais | Arquivo selecionado (card "Toque para substituir") com "Arquivo com páginas além do permitido". Botão "Enviar arquivo" desabilitado. |
| 006-4 | Erro: tamanho | "Arquivo com o tamanho maior que o permitido" (ex.: 55,5MB). "Enviar arquivo" desabilitado. |
| 006-5 | Erro: tipo | "Tipo de documento não aceito, envie uma CNH Digital". "Enviar arquivo" desabilitado. |
| 007 | Documento físico: instruções | "Fotografe o documento" com ilustração e 4 dicas: local iluminado, tirar do plástico, aproximar a câmera, um lado de cada vez. Botão "Avançar". |
| 008 | Captura da **frente** | Câmera com moldura verde, "Tente não se mexer" e contagem regressiva (captura automática). |
| 009 | Revisão da frente | "DNI lado com foto" com a imagem capturada. Botões "Avançar" e "Substituir Imagem". |
| 009-1 | Falha na validação | "Vamos tentar novamente — Não foi possível validar a imagem enviada…", ilustração de foto ruim x boa e botão "Tentar novamente". Vale para a frente e para o verso. |
| 009-2 | Falha definitiva (3ª falha) | Tela Honda "Atenção! Desculpe, não foi possível seguir com a assinatura. Por favor, gere um novo QR code ou anexe os documentos via IHS." Sem botão: a **assinatura é cancelada**. No remoto o texto muda (R08). |
| 010 | Captura do **verso** | "Enquadre o documento na posição vertical", moldura verde e miniatura da frente. O print mostra um **botão de disparo manual**, mas isso é um **bug conhecido** (ver R07): o certo é captura automática, como na frente. |
| 011 | Revisão do verso | "DNI lado sem foto". Botões "Avançar" e "Substituir Imagem". |
| 011-1 | Falha: ordem invertida (_sem print_) | Quando o verso é fotografado antes da frente: aviso genérico de imagem de baixa qualidade (visual da 009-1), sem botão. O fluxo termina aqui (R11). |

### Autorizações, termos e assinatura

| # | Tela | Conteúdo observado |
|---|------|--------------------|
| 012 | **Autorizações** | "Eu autorizo:" com 3 switches, **nenhum obrigatório** (R09): **Boleto por E-mail e Comunicações** (ligado por padrão), **Receber** (ofertas do Banco Honda, desligado) e **Compartilhar** (dados com o grupo Honda, desligado, com link da política de privacidade). Botão CONTINUAR. |
| 013 | **Termos** — documento 1 de 2 | Visualizador de PDF embutido com "Proposta de Financiamento – Pessoa Física". Botões Anterior (desabilitado) e Próximo. São **sempre 2 documentos** (R09). |
| 014 | **Termos** — documento 2 de 2 | "Orçamento de Operação de Crédito Direto ao Consumidor (CDC)". Anterior e Próximo. |
| 015 | **Termos** — documento 2, com aceite | Próximo desabilitado. Só nesse momento aparecem o switch "Li e aceito os termos" e o botão ASSINAR. |
| 016 | **Rubrica** (só presencial) | "Não é necessário realizar assinatura conforme o documento." Área de desenho, botão "Limpar" e botão ASSINAR. **Opcional**: ASSINAR com a área em branco segue sem rubrica (R09). |
| 016-1 | SPF: modal de dicas | "Dicas importantes da Captura da Selfie para Assinatura do SPF", com as mesmas 5 dicas da 003 e "OK, Entendi". |
| 016-2 | SPF: nova captura facial | Igual à 004, com as mesmas 2 capturas e as mesmas regras de falha da selfie padrão. |
| 016-3 | SPF: processando | Igual à 005. |
| 016-4 | SPF: termo do seguro | "Termos" com o PDF "Proposta de Adesão — Seguro Proteção Financeira" (BNP Paribas Cardif), **2 páginas** num documento só. Switch "Li e aceito os termos" e ASSINAR direto, sem Anterior/Próximo. |
| 016-5 | SPF: rubrica (só presencial) | Igual à 016. |

### Encerramento

| # | Tela | Conteúdo observado |
|---|------|--------------------|
| 017 | **Obrigado!** | "Estamos formalizando seu contrato, aguarde o contato da sua concessionária." Avaliação de 1 a 5 estrelas e botão INÍCIO. |
| 017-1 | Nota ≤ 4 | Aparece o botão "SUGERIR MELHORIAS". |
| 017-2/3 | Modal "Deixe sua opinião" | Campo de texto livre e botão Enviar. |
| 017-4 | Opinião enviada | "Sua opinião foi enviada com sucesso. Obrigado!" e botão INÍCIO. |
| 018 | **Fim** | **Presencial:** "Assinantes Concessionária — Assinatura finalizada para todos os assinantes", aberta pelo INÍCIO. **Remoto:** só informa que a assinatura foi finalizada com sucesso, e abre **sozinha** depois da avaliação (R02). |

### Sequência

```
[remoto]     000 ─(token ok)──────────────────┐   (000-1 / 000-2: erro, volta à 000; 000-V: vídeo → Entendi → 000)
[presencial] QR Code → 001 ─(Assinar na parte)─┴→ 002 → 003 → 004 (2 capturas) → 005 → 006
                                                         (004-1: falha facial → Tentar novamente → 003)
                       (001-1: "Aguarde" + Atualizar Lista → 001-2)

006 ─ CNH Digital ──→ 006-1 → 006-2 ─(PDF válido)→ 012
    │                          └(erros 006-3/4/5: substituir arquivo)
    └ Documento físico → 007 → 008 → 009 → 010 → 011 → 012
                         (009-1 na frente ou no verso: tentar de novo; na 3ª falha → 009-2, assinatura cancelada)

012 → 013 → 014 → 015 ─(ASSINAR)→ [presencial: 016 rubrica]
    → [se SPF: 016-1 → 016-2 → 016-3 → 016-4 → [presencial: 016-5 rubrica]]
    → 017 ─(5★)─────────────────────────────┐
          └(≤4★) 017-1 → 017-2 → 017-3 → 017-4 ┤
                                                ├ [presencial] INÍCIO → 001 (próxima parte) ou 018 (todas assinaram)
                                                └ [remoto] automático → 018 "assinatura finalizada com sucesso"
```

## Regras

### R01 — Porta de entrada depende do canal de envio do link
**Regra:** cada canal tem a sua porta de entrada, e uma não aparece no outro:
- **Remoto** (e-mail, SMS ou WhatsApp): o fluxo começa na **000 (Identificação por token)** e, com o token certo, vai **direto para a 002**. **Não existe a 001** (lista de assinantes), porque o link já é individual e foi enviado ao celular cadastrado daquela parte (R03).
- **Presencial:** o ambiente de abertura da proposta mostra um QR Code. O proponente lê o QR Code com a câmera do celular e cai **direto na 001**, sem token. Escolhe a parte em "Assinar" e segue para a 002.
- Token errado: "Código incorreto, tente novamente." (000-1). Token com menos de 6 dígitos: "O Token deve possuir 6 dígitos" (000-2).
- **Não há limite de tentativas** de token (confirmado em teste de estresse pelo usuário).
- "CLIQUE AQUI E CONFIRA" abre um **vídeo tutorial** (000-V) com botão "Entendi", que volta para a 000.

**Onde se aplica:** entrada do fluxo (000 → 002 no remoto; 001 → 002 no presencial).
**Impacto no remake:** obrigatória. Os dois caminhos de entrada continuam existindo, e o protótipo deve deixar simular os dois. A validação dos 6 dígitos pode acontecer enquanto o proponente digita (campo de 6 casas, CONTINUAR liberado só com 6 dígitos), sem precisar de um erro depois do envio. **Melhoria de segurança:** criar um limite de tentativas de token (com bloqueio temporário ou pedido de novo link), que hoje não existe.

### R02 — Avaliação da assinatura: comentário só com nota até 4
**Regra:** na tela 017 (Obrigado!) o proponente avalia a assinatura de 1 a 5 estrelas.
- **5 estrelas:** não há comentário. Segue para a **018**.
- **4 estrelas ou menos:** entra na ramificação **017-1 → 017-2 → 017-3 → 017-4**. Aparece o botão "SUGERIR MELHORIAS", que abre o modal "Deixe sua opinião"; o proponente digita o texto e envia, e vê a confirmação "Sua opinião foi enviada com sucesso". Depois da 017-4, segue para a **018**.

**Saída da 017 depende do canal:**
- **Remoto:** a 017 aparece **sem o botão INÍCIO**. Com 5 estrelas, o fluxo vai **automaticamente** para a 018. Com 4 ou menos, passa pelo feedback e, ao enviar, vai **automaticamente** para a 018. No remoto, a 018 só informa que a assinatura foi finalizada com sucesso (não há lista de assinantes).
- **Presencial:** a 017 tem o botão INÍCIO, que volta para a 001 (próxima parte, R03) ou leva à 018 quando todas as partes assinaram. A avaliação é **opcional**: dá para tocar em INÍCIO sem dar estrelas.
- **018 do remoto:** não há print. A réplica usa o **mesmo visual da 018** com o texto "Assinatura finalizada com sucesso".

**Onde se aplica:** 017 → 018.
**Impacto no remake:** ajustável. É uma pesquisa de satisfação, não etapa legal da formalização. Dá para mudar a forma (por exemplo, pedir o comentário no mesmo passo da nota) desde que a lógica "5 = sem comentário, ≤4 = pede sugestão" continue.

### R03 — Várias partes assinando (proponente + avalistas)
**Regra:** uma proposta pode ter mais de uma parte assinando, por exemplo o proponente com um ou dois avalistas. Cada parte precisa fazer biometria e assinatura. O jeito de percorrer as partes depende do canal:
- **Envio remoto:** cada parte recebe o **próprio link com o próprio token** no número de celular cadastrado e faz o fluxo inteiro **no seu dispositivo**, independente das outras. Por isso não há lista de assinantes: da 000 vai direto para a 002.
- **Presencial (QR Code):** todas as partes usam o **mesmo dispositivo**. A tela **001** lista o proponente e os avalistas. Quando uma parte termina, o fluxo **volta para a 001**. A linha de quem já assinou continua na lista, mas **sem link nenhum** na coluna de ação. Só as partes que ainda não assinaram (ex.: o avalista) mantêm o "Assinar", e por ele começa o mesmo fluxo para a próxima parte. Isso se repete até concluir as biometrias e ações de segurança de todas. Só então aparece a 018 ("Assinatura finalizada para todos os assinantes").
- **Fluxo do avalista:** é **exatamente o mesmo do proponente** (002 a 017, não há prints próprios): consentimento e captura facial → captura do documento ou upload da CNH Digital → Autorizações → os mesmos 2 documentos de termos → rubrica (no presencial) → avaliação de 1 a 5 estrelas → finalizar.
- **O avalista não tem o fluxo de SPF** (016-1 a 016-5). O seguro é só do proponente (R06).

**Onde se aplica:** 000/001 (entrada e lista de assinantes) e o retorno 017 → 001/018.
**Impacto no remake:** obrigatória (cada parte assina por si). Dá para melhorar a forma: deixar claro quem está assinando agora, mostrar o progresso das partes (ex.: "2 de 3 concluídas") e marcar quem já terminou na lista da 001.

### R04 — Status "Aguarde" e o botão "Atualizar Lista" (tela 001)
**Regra:** na lista de assinantes da 001, a ação à direita de cada parte depende da sincronização entre o **banco de propostas** e o **sistema de biometria e assinatura**:
- **Ainda não sincronizado** (em processamento, não liberado): aparece **"Aguarde"** (texto, sem link) e não dá para assinar (001-1).
- **Sincronizado:** aparece o link **"Assinar"** (001-2).
- O botão **"Atualizar Lista"** recarrega a lista para ver se as partes em "Aguarde" já foram liberadas. A atualização é manual, não automática.

- **Remoto:** não tem esse problema de sincronização. Vai sempre da 000 (token) direto para a 002.

**Onde se aplica:** 001 (só no presencial).
**Impacto no remake:** a dependência da sincronização é obrigatória, porque é uma restrição de integração. A forma de mostrar é oportunidade de melhoria: explicar por que está aguardando, atualizar sozinho de tempos em tempos (com o botão manual como reserva) e destacar quando a parte é liberada.

### R05 — Rubrica só no presencial
**Regra:** quando a assinatura é **remota**, não existe a etapa de rubrica. As telas **016** e **016-5** só aparecem no **presencial (QR Code)**.
**Onde se aplica:** 016 e 016-5.
**Impacto no remake:** obrigatória, porque a diferença entre os canais é do processo. O remake precisa respeitar a mesma condição.

### R06 — Seguro de Proteção Financeira (SPF): biometria e termo extras
**Regra:** se o **SPF** foi contratado na abertura da proposta, depois da assinatura dos termos do financiamento (e da rubrica, no presencial) entra a ramificação **016-1 → 016-5**:
1. modal de dicas da selfie "para Assinatura do SPF" (016-1);
2. **nova captura facial** (016-2) e processamento (016-3);
3. termo "Proposta de Adesão — Seguro Proteção Financeira" (BNP Paribas Cardif), com aceite e ASSINAR (016-4);
4. rubrica do SPF (016-5), **só no presencial** (R05).

Depois, segue para a 017. Sem SPF, a 016 (ou a 015, no remoto) vai direto para a 017.
**Só o proponente** passa pelo SPF. Os avalistas nunca têm essa ramificação (R03).
A selfie do SPF segue **o mesmo processo da selfie padrão** (2 capturas, mesmas regras de falha).
**Onde se aplica:** 016-1 a 016-5.
**Impacto no remake:** a assinatura separada do termo do SPF parece obrigatória, por ser outro contrato (com a seguradora). A **segunda selfie** é o ponto a avaliar com o negócio: se a seguradora não exigir uma captura própria, a biometria da 004 pode servir às duas assinaturas e o termo do SPF entra junto com os outros documentos. Isso economiza 2 capturas faciais.

### R07 — Captura do documento: CNH Digital ou documento físico
**Regra:** o proponente escolhe como enviar o documento de identificação (006):
- **CNH Digital:** envio de **arquivo PDF original**, num **arquivo único** de no **máximo 4MB**, sem prints de tela. O arquivo é recusado (com "Enviar arquivo" desabilitado e opção de substituir) quando:
  - tem **páginas além do permitido** (006-3);
  - é **maior que 4MB** (006-4);
  - **não é uma CNH Digital** (006-5).
- **Documento físico** (RG, CNH, DNI, RNE ou CIN): fotos da **frente** (008) e do **verso** (010), as duas com **captura automática** e contagem regressiva. Cada uma tem tela de revisão ("Avançar" ou "Substituir Imagem").
  - _Bug conhecido do fluxo atual:_ às vezes o verso aparece com disparo **manual**, como no print 010. A falha já foi identificada e o time de DEVs está corrigindo. **A réplica usa o comportamento correto (automático)**, e o bug fica só registrado.
  - Falha na validação da imagem, na frente ou no verso: tela "Vamos tentar novamente" (009-1).
  - Na **3ª falha**, a assinatura é cancelada (009-2, ver R08).
- **CNH Digital válida:** vai direto para a 012, sem passar pelas fotos do documento físico.

**Onde se aplica:** 006 a 011.
**Impacto no remake:** os tipos aceitos e os limites do arquivo (PDF, único, 4MB, CNH Digital) são do componente de captura e da validação antifraude, então são obrigatórios. A forma pode melhorar: dizer os limites antes de escolher o arquivo (hoje o limite de páginas só aparece depois do erro), trocar o rótulo "DNI lado com foto" por algo que valha para qualquer documento, mostrar quantas tentativas restam antes do cancelamento e deixar o caminho de saída da 009-2 mais claro.

### R08 — Cancelamento depois de 3 falhas no documento
**Regra:** depois de **3 falhas no total** na validação da foto do documento, **somando frente e verso** (ex.: 2 na frente + 1 no verso), a **assinatura é cancelada** (009-2) e não dá para continuar no celular. A saída depende do canal:
- **Presencial:** o colaborador precisa **pedir o reenvio da assinatura** no ambiente de abertura da proposta (gerar novo QR Code) ou anexar os documentos via IHS. É o texto do print 009-2.
- **Remoto:** a assinatura também é cancelada, e é preciso gerar um **novo pedido / reenvio do link**. _(Não há print; a réplica usa o visual da 009-2 com um texto que fale em novo link em vez de QR Code.)_

**Onde se aplica:** 009-1 → 009-2.
**Impacto no remake:** o limite de 3 tentativas e o cancelamento são regra antifraude, então obrigatórios. Melhorias de forma: avisar antes da última tentativa ("você tem mais 1 tentativa"), explicar ao proponente o que vai acontecer agora (ex.: "a concessionária vai enviar um novo link") e não usar termos internos como "IHS" numa tela do cliente.

### R11 — Ordem obrigatória: frente primeiro, depois verso
**Regra:** na captura do documento físico, é **obrigatório** fotografar **primeiro a frente** (lado com foto, 008/009) e **depois o verso** (010/011).

**Falha conhecida do fluxo atual:**
- Nenhuma tela avisa que a ordem é frente → verso. As dicas da 007 só dizem "Fotografe um lado de cada vez".
- O sistema **deixa capturar o verso primeiro e a frente depois**, e **reconhece o lado certo** em cada revisão: a 1ª confirmação mostra "DNI lado sem foto" (verso) e a 2ª mostra "DNI lado com foto" (frente). Mesmo sabendo que a ordem está invertida, aceita as duas fotos. Só depois das duas capturas, em vez de seguir, mostra um aviso **genérico de imagem de baixa qualidade**, sem relação com o problema real.
- _Na réplica_ (tela **011-1**), o aviso usa o visual da 009-1 **sem botão e sem X**: o cenário termina ali. _O usuário vai confirmar se existe botão de tentar novamente; até lá, a réplica simula sem retorno._ Esse aviso não conta nas 3 falhas da R08.

**Onde se aplica:** 007 a 011.
**Impacto no remake:** a ordem frente → verso é obrigatória (exigência do componente de validação). A forma é a principal oportunidade de melhoria: dizer a ordem na 007 e no título de cada captura ("1 de 2: frente, o lado com foto"), usar a detecção de lado que o sistema **já tem** (a revisão já identifica frente e verso) para barrar o lado errado na 1ª captura, com uma mensagem específica ("Este é o verso. Fotografe primeiro a frente."), com opção de refazer.

### R12 — Pessoa jurídica (CNPJ) segue o mesmo fluxo da pessoa física
**Regra:** qualquer parte (proponente ou avalista) pode ser **pessoa física (CPF)** ou **pessoa jurídica (CNPJ)**. No fluxo atual, a pessoa jurídica passa **exatamente pelo mesmo fluxo** da física: consentimento, selfie, documento de identificação, autorizações, termos, rubrica e avaliação. Só muda o cadastro exibido (razão social e CNPJ na lista da 001).
- _Na réplica:_ o painel de simulação permite escolher CPF ou CNPJ para o proponente e para cada avalista.

**Onde se aplica:** todo o fluxo (002 a 018); a diferença visível hoje é só na 001.
**Impacto no remake:** ponto a tratar. Uma empresa não tem rosto nem RG: quem faz a selfie e mostra o documento é o **representante legal**. O remake deve considerar o cenário PJ, por exemplo identificando o representante (nome e CPF) antes da biometria, ajustando os textos ("Você está assinando em nome de EXEMPLO LTDA") e, se o negócio exigir, pedindo documentos da empresa.

### R13 — A assinatura digital não altera a proposta
**Regra:** o ambiente de assinatura digital **só estrutura e apresenta** as informações que já foram digitadas, selecionadas e ativadas no **sistema de abertura de proposta** (o sistema base). Ele não ativa nem desativa nada na proposta. Exemplo: o **SPF é ativado pelo colaborador** na abertura da proposta, antes de a pessoa chegar à assinatura.
**Onde se aplica:** todo o fluxo, em especial os documentos do contrato e o termo do SPF.
**Impacto no remake:** obrigatória. Nenhuma tela da assinatura pode oferecer recusar, retirar ou mudar itens da proposta (como "não quero o seguro"). Mudanças são feitas pelo colaborador no sistema base, que gera um novo acesso à assinatura.

### R10 — Falha na captura facial
**Regra:** quando a captura facial não dá certo (004, ou 016-2 no SPF), aparece uma tela com o **mesmo layout da tela de cancelamento** (009-2: cabeçalho Honda, título "Atenção!" e texto centralizado). O texto informa que **não foi possível realizar a captura facial** e pede para **tentar novamente**.
- _Não há print._ Na réplica, a tela é a **004-1**, com o texto "Não foi possível realizar a captura facial. Por favor, tente novamente." e um botão **"Tentar novamente"**, que volta para as dicas da selfie (003, ou 016-1 no SPF).
- **Máximo de 3 tentativas.** Na 3ª falha, a assinatura é **cancelada** igual à R08: tela "Atenção!" sem botão, reenvio pelo ambiente de abertura no presencial e novo link no remoto. _(Confirmado pelo usuário.)_

**Onde se aplica:** 004 → 004-1 → 003 (e 016-2 → 016-1 no SPF).
**Impacto no remake:** a validação facial é obrigatória (antifraude). Dá para melhorar a forma: dizer o motivo provável da falha (pouca luz, rosto fora da moldura, acessórios), com o mesmo estilo da 009-1 do documento, em vez de uma mensagem genérica.

### R09 — Autorizações, termos e rubrica: o que é obrigatório
**Regra:**
- **Autorizações (012):** **nenhum switch é obrigatório**. "Boleto por E-mail e Comunicações" vem **ligado por padrão**; "Receber" e "Compartilhar" vêm desligados.
- **Termos (013–015):** são **sempre 2 documentos** (Proposta de Financiamento e Orçamento CDC). O aceite e o ASSINAR só aparecem no último.
- **Rubrica (016 / 016-5, só presencial):** **não é obrigatória** no fluxo atual. Tocar em ASSINAR com a área em branco segue sem rubrica.

**Onde se aplica:** 012 a 016-5.
**Impacto no remake:** ajustável. O switch já ligado por padrão merece revisão de LGPD (consentimento precisa ser ativo). A rubrica opcional mas com destaque de etapa obrigatória confunde: ou deixa claro que é opcional, ou some. Com sempre 2 documentos, dá para mostrar "1 de 2 / 2 de 2" com clareza.

<!--
Modelo por regra:

### R01 — <título curto>
**Regra:** <descrição como informada>
**Onde se aplica:** <tela/etapa do fluxo>
**Impacto no remake:** <obrigatória (legal/segurança/integração) | ajustável | oportunidade de melhoria> — <comentário>
-->

## Decisões para o remake

> Decisões do usuário, tomadas a partir do [FEEDBACK.md](FEEDBACK.md). Valem **só para o remake** (`biometria-remake.html`); a réplica do fluxo atual continua igual.

### D01 — Retirar a rubrica
A rubrica (016 e 016-5) **sai do remake**, também no presencial e no SPF.
**Motivo:** ela não precisa ser igual a nenhuma assinatura oficial de documento de identidade, e a selfie e a captura do documento já garantem a identificação. Era a crítica nº 1 do feedback (73 menções, 33%) e já não era obrigatória no fluxo atual (R09).
**Efeito no fluxo:** depois do aceite dos termos vem a próxima etapa direto (SPF, se houver, ou a avaliação). A R05 (rubrica só no presencial) deixa de valer no remake.

### D02 — Contrato em texto, com aceite liberado ao fim da rolagem
- **Ordem mantida:** o contrato continua no mesmo ponto do fluxo, **depois** da biometria e do documento. A ideia de ler antes não será adotada.
- **Formato novo:** o contrato deixa de ser um PDF num visualizador pequeno e passa a ser **reescrito como texto** legível no celular, no estilo dos termos de instalação de jogos e aplicativos.
- **Aceite:** o botão **"Aceito"** só fica liberado para toque depois que a pessoa **rolar o texto até o fim**.

**Motivo:** a leitura do contrato foi a crítica nº 2 (41 menções, 18%): letras pequenas e falta de zoom.
**A definir no desenvolvimento:**
- como mostrar os dois documentos (Proposta e Orçamento CDC) e o termo do SPF;
- se o resumo dos valores principais fica no topo.

### D03 — Entrada remota (000): token mais claro e seguro
- **Campo de 6 casas**, com teclado numérico e preenchimento automático do código do SMS. "Continuar" só libera com os 6 dígitos, então o erro "token incompleto" (000-2) deixa de existir.
- A tela mostra **para onde o código foi enviado** (telefone mascarado), com **"Reenviar código"** liberado depois de 30 s.
- **Limite de 5 tentativas.** A cada erro, a tela mostra quantas restam. Na 5ª, o acesso fica **bloqueado por 5 minutos**, com a opção de **solicitar um novo código** na hora, o que zera as tentativas.
- O vídeo tutorial continua, agora como "Ver como funciona".

### D04 — Lista de assinantes (001, presencial): cards com status claro
- **Um card por parte**, com nome, papel, documento **mascarado** e um selo de status: **Pronto para assinar** (com o botão "Iniciar"), **Aguardando liberação** (com explicação) ou **Concluído ✓**.
- **Progresso no topo** ("1 de 2 assinaturas concluídas").
- **Atualização automática a cada 15 s**, com o botão manual como reserva e destaque no card que acabou de ser liberado.

### D05 — Tela de boas-vindas antes da selfie (nos dois canais)
Depois do token (remoto) ou do "Iniciar" (presencial), uma tela mostra:
- **quem está assinando**: nome, papel e, para CNPJ, a empresa em nome da qual o representante assina (R12);
- **a proposta** de que se trata;
- **as etapas do processo** com o tempo estimado (o termo do SPF só aparece para o proponente com SPF);
- o que ter em mãos.

**Motivo:** críticas de processo longo e burocrático e de falta de explicação (FEEDBACK.md, temas 6 e 9).

### D06 — Selfie: dicas e consentimento numa tela só, com indicador de etapa
- As telas 002 (termo da captura facial) e 003 (modal de dicas) viram **uma tela**, "Vamos tirar uma selfie":
  - as dicas aparecem em **4 cards visuais**, sempre à vista;
  - o consentimento vira **uma frase com a caixa "Autorizo"**, que continua obrigatória para abrir a câmera;
  - o **termo completo** fica num link e abre numa folha com "Li e concordo".
- Um **indicador de etapa** ("Etapa 1 de 4 · Selfie", com barra) passa a aparecer em todas as telas do processo. As etapas seguem a lista das boas-vindas (D05).
- **Motivo:** críticas de processo longo e de selfie difícil (FEEDBACK.md, temas 4 e 6).

### D07 — Selfie: permissão da câmera, captura guiada e verificação com progresso
- O pedido de **permissão da câmera** aparece ao tocar em "Abrir câmera". Se a pessoa **bloquear**, uma tela explica como liberar e oferece "tentar de novo", sem recomeçar a assinatura.
- **Captura guiada**, mantendo as 2 capturas:
  - orientação em tempo real ("posicione o rosto", "aproxime", "fique parado");
  - aviso do problema na hora (pouca luz, óculos, fora da moldura);
  - "Captura 1 de 2 / 2 de 2" escrito;
  - **guia por voz** opcional, para acessibilidade.
- **Verificação:** diz quanto tempo leva e mostra o que está sendo conferido, no lugar do "Aguarde um instante...".
- **Selfie confirmada:** uma tela de sucesso diz qual é a próxima etapa.

### D08 — Selfie: falha com motivo, tentativas restantes e encerramento claro
- Na falha (antes 004-1, genérica), a tela mostra:
  - o **motivo provável** (pouca luz, rosto fora da moldura, óculos ou boné, movimento);
  - **dicas específicas** para esse motivo;
  - **quantas tentativas restam**, com aviso de "última tentativa".
- "Tentar novamente" abre a câmera direto.
- Na **3ª falha** (R10), a assinatura é encerrada numa tela sem jargão (sem "IHS") que diz **o que acontece agora** conforme o canal. O botão de saída também muda conforme o canal (D09).

### D09 — Saída da assinatura encerrada: novo acesso ou encerrar
- **"O que acontece agora"** muda conforme o canal:
  - **Presencial:** "Chame o vendedor da concessionária para ter acesso a um novo QR Code de acesso à assinatura digital."
  - **Remoto:** "Peça um novo acesso: a concessionária recebe um aviso e envia um novo acesso para o seu celular."
- **Botão principal:**
  - **Presencial — "Ler novo QR Code":** abre o leitor de QR Code dentro do próprio fluxo. Depois da leitura, volta para a lista de assinantes (001) com o novo acesso.
  - **Remoto — "Pedir novo acesso":** a tela confirma "Pedido enviado" e mostra o celular que vai receber o novo acesso.
- **Botão "Encerrar processo"** (nos dois canais): fecha a assinatura digital. Mostra "Assinatura encerrada" por 2 segundos e fecha.
  - No simulador, volta para a tela inicial (001 no presencial, 000 no remoto).
  - Num celular de verdade, o navegador fecha e o usuário volta para a tela inicial do aparelho.
  - _Ponto técnico para o time de desenvolvimento:_ os navegadores só deixam uma página fechar a própria aba (`window.close`) se ela tiver sido aberta por script. Quando a pessoa abre o link pelo SMS ou pelo QR Code, isso normalmente não funciona. Pode ser preciso trocar o fechamento por uma página final do tipo "pode fechar esta janela".
- **Requisito fora das telas mobile:** o pedido de novo acesso precisa gerar um **alerta para o colaborador na plataforma de assinatura digital**, para ele saber que precisa enviar um novo link.
  - **Problema de hoje:** se a pessoa a distância não termina e não avisa, o colaborador não sabe o que aconteceu nem entende a demora. Ele só descobre por suspeita, entrando em contato com o proponente.
- **Motivo:** a tela atual (009-2) não tem botão, e no remoto o colaborador fica sem informação.

### D10 — Documento: escolha clara entre físico e CNH Digital
- A tela 006 vira **"Qual documento você vai usar?"**, com indicador de etapa e **dois cartões de escolha**:
  - **Documento físico** (RG, CIN, CNH, RNE ou DNI): "você vai fotografar a frente e depois o verso";
  - **CNH Digital:** "arquivo PDF tirado do app Carteira Digital de Trânsito".
- "Continuar" só libera depois de escolher.

### D11 — Documento físico: ordem frente → verso guiada e lado errado barrado na hora
- A tela de instruções (007) deixa a **ordem explícita**, no título e num desenho de 2 passos (1. Frente, o lado com a foto; 2. Verso). O botão diz "Fotografar a frente".
- **Câmera:**
  - mostra "Frente do documento · 1 de 2" / "Verso · 2 de 2" e dá orientação em texto;
  - a moldura muda de cor (branco, amarelo de alerta, verde quando está bom);
  - frente **e** verso têm captura automática com contagem (R07).
- **Lado errado:** o sistema já reconhece o lado (R11). No remake, se a pessoa mostrar o verso na etapa da frente, o aviso aparece **na hora** ("Este é o verso. Vire o documento e mostre a frente") e a foto errada não é tirada. Acaba a falha genérica no fim (011-1).
- **Revisão:** o título vira "Frente do documento" / "Verso do documento", no lugar de "DNI lado com foto", e diz o que conferir. Os botões são "Usar esta foto" e "Tirar outra".

### D12 — Documento: CNH Digital com regras antes, falhas com motivo e verificação
- **CNH Digital:**
  - passo a passo para exportar o PDF no app Carteira Digital de Trânsito;
  - as regras do arquivo (PDF original, só a CNH, até 4 MB) aparecem **antes** de escolher;
  - o arquivo escolhido aparece em verde ou vermelho, com uma mensagem que diz **como resolver** o erro.
- **Falha na foto:**
  - mostra o motivo provável e o lado que falhou (reflexo, desfocada, documento cortado), com dicas específicas;
  - mostra as **tentativas restantes**, somando frente e verso (R08);
  - o botão volta direto para o lado que falhou.
- **3ª falha:** encerra a assinatura na mesma tela da selfie (D08/D09), que diz que o motivo foi a foto do documento.
- **Verificação:** diz o tempo estimado e o que está sendo conferido (incluindo a comparação com a selfie), e depois confirma o documento.
- **Em aberto para o negócio:** aceitar RG digital/CIN digital e passaporte (FEEDBACK.md, tema 7).

### D13 — Autorizações mais simples, sem mudar o que é obrigatório
- Título com pergunta direta ("Como prefere receber as informações?") e o aviso de que **nenhuma opção é obrigatória** (R09).
- Cada autorização vira um **cartão** com título curto, uma frase simples e uma chave grande. O texto jurídico completo fica em **"Ver detalhes"**.
- **Mantido o padrão atual:** "Boleto e avisos digitais" vem ligado. _Ponto para o jurídico:_ o consentimento já ligado pode precisar ser revisto pela LGPD (consentimento ativo).

### D14 — Leitor do contrato (implementação da D02)
- **Resumo do financiamento no topo** do primeiro documento: parcela em destaque (36 × R$ 305,79), valor financiado, juros, CET e total a pagar. Responde ao feedback "realçar os valores".
- Os dois documentos (Proposta de financiamento e Orçamento CDC) são **reescritos em texto** legível, com seções curtas, e aparecem um de cada vez ("Documento 1 de 2").
- **Barra de leitura** que avança com a rolagem; **A− / A+** para o tamanho da letra; **"Baixar PDF"**.
- O botão **"Aceito"** só libera quando a pessoa **rola até o fim** do documento.
- _Atenção:_ a versão em texto precisa ter o mesmo conteúdo jurídico dos PDFs oficiais. A redação final é do jurídico; o texto da simulação é fictício.

### D15 — Assinatura sem rubrica, com confirmação clara
- Depois dos dois aceites, a tela "Tudo pronto para assinar" lista os documentos lidos e aceitos, com a opção de **rever** cada um.
- Explica que a assinatura eletrônica usa a **selfie e o documento** e que não precisa de rubrica (D01).
- O botão é **"Assinar contrato"**. Depois aparecem "Assinando…" e a confirmação **"Contrato assinado"**, com a próxima etapa: termo do SPF, se contratado, ou avaliação.

### D16 — SPF sem a 2ª selfie: o seguro vira o 3º documento do contrato
_Condicionada à aprovação do jurídico da Honda._
- **Por que existe a 2ª selfie hoje** (segundo os analistas e o time de desenvolvimento): foi pedido do jurídico da Honda, porque clientes alegavam que não sabiam do SPF e não queriam ter assinado. A selfie extra serve de prova de que a pessoa contratou o seguro por vontade própria, sabendo o que era.
- **Por que dá para retirar:** a causa era o seguro passar despercebido (PDF pequeno, aceite único no fim). Com as melhorias, o seguro fica explícito e tem aceite próprio. A identidade já foi confirmada pela selfie aprovada no liveness do início, e a 2ª selfie não acrescenta identidade, só atrito (FEEDBACK.md, temas 4 e 6).
- **Como fica no remake:**
  - Sem as telas 016-1 a 016-5 (dicas, 2ª selfie, processamento, termo em PDF e rubrica).
  - O seguro entra como **"Documento 3 de 3 · Seguro Proteção Financeira"**, só para o proponente com SPF (os avalistas não têm SPF, R06). A etapa nas boas-vindas passa a ser "Autorizações, contrato e seguro", e o processo fica com 4 etapas no lugar de 5.
  - **Visual próprio** (azul, da seguradora) e **resumo no topo:** "Seguro incluído na sua proposta", valor (R$ 512,30 no financiamento), vigência, coberturas e cancelamento a qualquer tempo depois de assinado.
  - **Aceite específico e afirmativo,** separado do contrato: além de rolar até o fim, marcar **"Li e concordo com a contratação do Seguro Proteção Financeira"**. Sem isso, o "Aceito" não libera.
  - **Sem opção de retirar ou recusar o seguro nesta tela** (R13): quem ativa o SPF é o colaborador, na abertura da proposta.
  - Na tela "Tudo pronto para assinar", o seguro aparece em **linha própria** ("R$ 512,30 · contratação aceita"), e a confirmação diz "Contrato e seguro assinados".
- **Requisito para o time de desenvolvimento — trilha de auditoria:** registrar data, hora, dispositivo e IP do aceite do SPF (a caixa marcada e o "Aceito"), ligados ao identificador da sessão da selfie aprovada. É a prova que substitui a 2ª selfie e o principal argumento para o jurídico.

### D17 — Avaliação e encerramento
- A tela 017 abre com uma **confirmação clara** ("Sua assinatura foi concluída" ou "Contrato e seguro assinados") e o que acontece agora. Inclui **"Baixar cópia do contrato"** em PDF.
- A **avaliação é opcional** e diz isso. Cada nota tem um rótulo (de "Muito difícil" a "Muito fácil").
- **A nota pode ser trocada à vontade** (por exemplo, de 5 para 4) e só vale ao tocar em **"Enviar avaliação"**. Esse botão aparece depois de escolher qualquer nota. Se a pessoa tocar em "Concluir" com uma nota escolhida e não enviada, a nota vai junto. Hoje o primeiro toque nas estrelas já é definitivo.
- **R02 mantida:** com 5 estrelas, não há comentário. Com até 4, os **motivos aparecem na mesma tela**, sem modal: botões de um toque ("Ler o contrato", "Selfie", "Foto do documento", "Demorou", "Entender as etapas", "Outro") e texto opcional. Os comentários passam a dizer o problema, em vez de "Péssimo" (24 críticas genéricas no FEEDBACK.md).
- **Botão "Concluir" sempre disponível:**
  - **Presencial:** "Concluir e chamar o próximo", que volta para a lista de assinantes (001).
  - **Remoto:** "Concluir". Depois de avaliar, a tela também encerra sozinha, como hoje (R02). Isso resolve quem não quer avaliar, que hoje fica parado na tela sem botão.
- **018 (remoto):** "Tudo certo!", com a orientação de que já pode fechar a página.

### D18 — Confirmações intermediárias seguem sozinhas
- As telas **Selfie confirmada**, **Documento confirmado** e **Contrato assinado** não têm mais o botão "Continuar". Elas seguem para a próxima etapa **sozinhas, em 4 segundos**, porque não há decisão a tomar ali.
- Para não parecer que a tela travou, mostram **"Seguindo para a próxima etapa…"** com uma barra de progresso de 4 segundos.
- **Não vale** para a tela final (017/018), que continua com o botão "Concluir", a avaliação e o download da cópia (D17).

## Cenários futuros (só para conhecimento)

> Ainda **não entram** na réplica nem no remake. Ficam registrados para quando o usuário pedir.

### F01 — Menor Conduz: assinatura de 1 ou mais avalistas
Fonte: história do P.O. da Plataforma F&I e de Formalização (print enviado pelo usuário).

- **Objetivo:** incluir e habilitar a assinatura digital de 1 ou mais avalistas na proposta, para formalizar conforme as regras do negócio (Menor Conduz, Tutela/Curatela) e evitar retrabalho e pendências.
- **Regras de alto nível:**
  - **Menor Conduz** → mínimo de **1 avalista obrigatório**.
  - **Possui Tutela/Curatela** → mínimo de **2 responsáveis obrigatórios**.
- **Etapas impactadas** (na abertura da proposta): Subtipo → Ficha Proposta → Pré-análise → Simulador → Dados do Cliente → **novo campo TUTELA** → Dados do Avalista → **Incluir Novo Avalista** → Formalização → Documentos Obrigatórios.
- **Documentos:** laudo médico (quando aplicável), documento do proponente, documento do avalista 1/2, termo de tutela/curatela (se houver), comprovante de endereço, comprovante de óbito (se houver).
- **Valor de negócio:** reduz reprovação por ausência de responsáveis, garante conformidade regulatória e acelera o TTF (Time-to-Formalize).

**Proposta técnica "Fluxo 1"** (anotação do time; mantém a estrutura de hoje):
- Assinatura do proponente: aceite da captura da selfie → captura da selfie → envio do documento → aceite dos opt-ins → aceite dos termos → rubrica.
- Passos necessários:
  - **ignorar a selfie do proponente** na assinatura dos documentos no Ábaris;
  - armazenar a selfie e o documento de identidade do **avalista 2**;
  - assinatura da **Ficha Aval 2**;
  - ajustar o retorno dos documentos assinados pelo serviço **EnviaDocsAss**.

**Relação com o que já está mapeado:** o fluxo de cada avalista é o mesmo do proponente (R03), e a réplica já simula até 2 avalistas. O que muda no Menor Conduz é a **obrigatoriedade** (mínimo de avalistas/responsáveis) e o tratamento da selfie do proponente, que é ignorada na assinatura.

## Pontos em aberto

> As dúvidas se acumulam aqui e o usuário responde **todas de uma vez**, quando terminar de enviar os prints. Até lá, a réplica segue o que aparece nos prints. A cada novo lote de prints (sobretudo ramificações `-1`, `-2`…), as dúvidas que os próprios prints já respondem são riscadas e indicam qual print as respondeu.

### Dúvidas abertas

18. **011-1 (ordem invertida):** o aviso genérico de baixa qualidade tem botão para tentar de novo, ou o processo trava ali? _(O usuário vai verificar; na réplica, sem retorno.)_
19. **Feedback dos usuários:** a planilha se chama "assinatura_remota", mas 73 comentários criticam a rubrica, que pela R05 só existe no presencial. "Assinatura Remota" é o nome do produto (como no menu do Painel KTA) e a planilha inclui avaliações dos dois canais? _(Ver FEEDBACK.md.)_

### Prints prometidos pelo usuário

_Nenhum. O fluxo do avalista é o mesmo do proponente (R03)._

### Dúvidas respondidas

1. ~~"CLIQUE AQUI E CONFIRA" na 000~~ → abre o vídeo tutorial 000-V (R01).
2. ~~Token inválido, expiração e limite de tentativas~~ → prints 000-1/000-2; não há limite de tentativas (R01).
3. ~~Vários assinantes, 001 no remoto, sincronização no remoto e fim do remoto~~ → R01, R02, R03 e R04.
4. ~~2ª etapa do indicador da 004~~ → 2ª captura, com o rosto mais próximo (mapa, 004). Os prints de falha facial ainda vão chegar.
5. ~~Captura do documento (006–011)~~ → prints 006 a 011 (R07).
6. ~~Switches obrigatórios na 012~~ → nenhum; "Boleto por E-mail" ligado por padrão (R09).
7. ~~Quantidade de documentos nos termos~~ → sempre 2 (R09).
8. ~~Rubrica obrigatória~~ → não, segue sem rubrica (R09).
9. ~~Nota que dispara "SUGERIR MELHORIAS"~~ → 4 ou menos (R02).
10. ~~Passagem 017 → 018, avaliação opcional e 018 do remoto~~ → R02.
11. ~~Erros `-N` como alternativas que voltam à origem~~ → confirmado (convenção no mapa).
12. ~~Destino da CNH Digital válida~~ → direto para a 012 (R07).
13. ~~Selfie do SPF~~ → mesmo processo da selfie padrão (R06).
14. ~~Falhas do documento~~ → 3 falhas cancelam; vale para o verso; no remoto pede novo link (R08).
15. ~~Contagem das 3 falhas~~ → 3 no total, somando frente e verso (R08).
16. ~~Botão e limite na falha facial~~ → botão "Tentar novamente", máximo de 3 tentativas (R10).
17. ~~Fluxo do avalista~~ → exatamente o mesmo do proponente (002 a 017), sem SPF (R03).
