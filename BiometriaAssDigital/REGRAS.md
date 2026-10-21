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

## Pontos em aberto

> As dúvidas se acumulam aqui e o usuário responde **todas de uma vez**, quando terminar de enviar os prints. Até lá, a réplica segue o que aparece nos prints. A cada novo lote de prints (sobretudo ramificações `-1`, `-2`…), as dúvidas que os próprios prints já respondem são riscadas e indicam qual print as respondeu.

### Dúvidas abertas

18. **011-1 (ordem invertida):** o aviso genérico de baixa qualidade tem botão para tentar de novo, ou o processo trava ali? _(O usuário vai verificar; na réplica, sem retorno.)_

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
