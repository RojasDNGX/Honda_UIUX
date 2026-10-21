# Biometria / Assinatura Digital — Feedback dos usuários

Consolidação das avaliações deixadas pelos assinantes ao final do fluxo (tela 017, R02), ordenadas da crítica mais repetida (prioridade alta) para a menos comentada (prioridade baixa). Serve de base para o remake (`biometria-remake.html`), junto com as regras do [REGRAS.md](REGRAS.md).

## Base analisada

- **Fonte:** planilha `avaliacoes_assinatura_remota_honda_estudo_caso.xlsx`, aba "Comentarios_Anonimos" (nota, comentário e data).
- **Período:** 01/09/2026 a 15/10/2026.
- **Total:** 305 avaliações com comentário.

| Nota | Avaliações | % |
|------|-----------:|--:|
| ★ 1 | 52 | 17% |
| ★★ 2 | 43 | 14% |
| ★★★ 3 | 100 | 33% |
| ★★★★ 4 | 108 | 35% |
| ★★★★★ 5 | 2 | 1% |

**Média: 2,9.** Quase não há notas 5 porque o pedido de comentário só aparece com nota até 4 (R02). A planilha mostra, portanto, **quem teve alguma insatisfação**, e não a satisfação geral de todos os assinantes.

**Do que tratam os 305 comentários:**
- **82 (27%)** são elogios, comentários neutros ou vazios ("Bom", "Ok", ".");
- **24 (8%)** são críticas genéricas, sem dizer o motivo ("Péssimo", "Muito ruim");
- **199** têm crítica ou sugestão específica. Somados às genéricas, são **223 comentários com crítica**, e é sobre esse total que os percentuais abaixo são calculados.

## Ranking das críticas

| # | Tema | Menções | % das críticas | Prioridade |
|---|------|--------:|---------------:|-----------|
| 1 | Rubrica / assinar com o dedo na tela | 73 | 33% | **Alta** |
| 2 | Leitura do contrato e dos termos no celular | 41 | 18% | **Alta** |
| 3 | Pedido de outra forma de assinar (gov.br, digitada, papel) | 27 | 12% | **Alta** |
| 4 | Captura facial / selfie difícil | 20 | 9% | Média |
| 4 | Lentidão, travamentos e erros | 20 | 9% | Média |
| 6 | Processo longo, burocrático ou em ordem ruim | 12 | 5% | Média |
| 7 | Envio do documento de identificação | 11 | 5% | Média |
| 8 | Dispositivo e navegador (só celular, Chrome) | 7 | 3% | Baixa |
| 9 | Pontuais (token, atendimento, seguro, contraste, acessibilidade…) | 12 | 5% | Baixa |

---

### 1. Rubrica / assinar com o dedo na tela — 73 menções · prioridade alta

**O que os usuários dizem:**
- "Campo para assinatura muito pequeno" — o motivo mais citado: espaço, quadrado ou campo pequeno.
- "Muito ruim pra assinar com o dedo", "assinar nesse touch é impossível".
- "Melhorar a espessura do traço, deixá-lo mais fino", "deveria ter uma suavidade a mais no toque".
- "Seria bom se desse pra limpar só uma parte e não tudo", "ter opção de apagar ou de retroceder a ação".
- "Achei estranho, não apareceu minha escrita! Fiquei na dúvida se concretizei a assinatura".
- "Poderia ser digitado", "deixe um nome já pronto para usar", "deixar assinar com caneta".

**Causa no fluxo atual:**
- A rubrica (016) **não é obrigatória** (R09): dá para seguir com a área em branco.
- Mesmo assim, a tela parece uma etapa obrigatória e traz uma frase confusa ("Não é necessário realizar assinatura conforme o documento").
- O campo é pequeno, o traço é grosso, e o único jeito de corrigir é limpar tudo.

> Observação: pela R05, a rubrica só existe no presencial. "Assinatura Remota" provavelmente é o nome do produto, e não do canal (ver dúvida 19 no REGRAS.md).

**Oportunidade no remake:**
- Decidir com o negócio se a rubrica continua.
- Se continuar:
  - deixar claro que é opcional, com um "Pular" visível;
  - abrir uma área grande, em tela cheia ou com o celular deitado;
  - usar um traço mais fino e suave;
  - ter botão para desfazer o último traço;
  - oferecer a rubrica digitada (nome em fonte manuscrita);
  - mostrar uma confirmação clara de que a rubrica foi registrada.

### 2. Leitura do contrato e dos termos no celular — 41 menções · prioridade alta

**O que os usuários dizem:**
- "Letras muito pequenas, difíceis de ler", "Letras muuuito miúdas. Tem q ficar maximizado".
- "Não consegui dar um zoom pra ler o contrato", "com zoom tem que deslocar o documento para ler".
- "Deveria haver a opção de baixar o documento", "gostaria de poder imprimir o que estou assinando".
- "Deveria enviar antes para o cliente dar uma pré-lida e a possibilidade de correção nos dados".
- "Permitir ver o contrato sem a necessidade de subir a CNH e selfie".
- "Poderia realçar os pontos fundamentais como valores para facilitar a conferência".

**Causa no fluxo atual:** o contrato é um PDF dentro de um visualizador pequeno, embutido na página (013 a 015). Não dá para ampliar de forma confortável, nem baixar, nem ler antes da biometria.

**Oportunidade no remake:**
- Abrir o documento em tela cheia, com texto que se ajusta à largura do celular e zoom com dois dedos.
- Mostrar um resumo com os números principais em destaque (valor financiado, parcela, quantidade de parcelas, CET).
- Permitir baixar e compartilhar o PDF.
- Mostrar o progresso entre os documentos ("1 de 2").
- Avaliar mostrar o contrato **antes** da biometria (ver tema 6).

### 3. Pedido de outra forma de assinar — 27 menções · prioridade alta

**O que os usuários dizem:**
- **gov.br (14):** "Poderia ser assinatura digital pelo gov", "via gov seria melhor e mais moderno".
- **Papel ou presencial (5):** "Melhor assinar no papel", "pessoalmente é melhor".
- **Outras:** assinatura digitada ou por aplicativo, "assinatura digital ao invés de fotografia", "dar opções de assinaturas".

**Causa no fluxo atual:** existe um único caminho (selfie, documento e rubrica), sem alternativa.

**Oportunidade no remake:**
- Oferecer a assinatura via **gov.br** é uma **decisão de negócio e jurídica**, porque depende de integração. Vale levar ao P.O. como um dado de peso: é o pedido espontâneo mais repetido.
- Enquanto isso não for decidido, o remake pode atender boa parte desse incômodo com a rubrica digitada ou opcional (tema 1).

### 4. Captura facial / selfie — 20 menções · prioridade média

**O que os usuários dizem:**
- "A parte de tirar a foto não funciona com nenhuma luz do mundo".
- "Demora muito para capturar a foto", "Biometria facial tem muita dificuldade para capturar".
- "Só no Mozilla funcionou".
- "Colocar auxílio sonoro para ajudar pessoas com visão reduzida na hora de fazer a selfie".

**Causa no fluxo atual:**
- As dicas aparecem só antes da captura (003), num modal estático.
- Na falha, a mensagem é genérica (R10).
- Com SPF, a selfie é feita duas vezes (R06).

**Oportunidade no remake:**
- Orientar em tempo real durante a captura ("aproxime o rosto", "procure mais luz", "tire os óculos").
- Na falha, dizer o motivo provável e quantas tentativas restam (R08 e R10).
- Usar uma selfie só quando o SPF permitir (R06).
- Incluir apoio de acessibilidade, como áudio e vibração.

### 4. Lentidão, travamentos e erros — 20 menções · prioridade média

**O que os usuários dizem:**
- "O 'aguarde instantes' demora MUITO, não são instantes".
- "Muito lento e às vezes fica voltando tudo pro início".
- "Voltar a página anterior e depois avançar não funciona. Fica informando que arquivo não existe".
- "Site pesado para processar. Arquivo de termos não apareceu".

**Causa no fluxo atual:**
- As telas de espera (005) não têm progresso nem previsão.
- O botão "voltar" do navegador quebra o fluxo.
- O fluxo perde o estado e volta ao início.

**Oportunidade no remake:**
- Na espera, mostrar o que está sendo feito e quanto falta.
- Guardar o progresso, para que voltar e avançar não percam etapas.
- Tratar o botão "voltar" do celular.
- Deixar as telas mais leves (é uma questão técnica para o time de desenvolvimento).

### 6. Processo longo, burocrático ou em ordem ruim — 12 menções · prioridade média

**O que os usuários dizem:**
- "Muita coisa para formalizar", "Muito burocrático".
- "Reconhecimento facial e mais anexo de documentos que já foram enviados".
- "Biometria facial deveria ser no final e não no início", "anexar os documentos e selfie no final".

**Causa no fluxo atual:** a pessoa faz selfie e documento **antes** de ver o que está assinando, e não sabe quantas etapas faltam.

**Oportunidade no remake:**
- Mostrar um indicador de etapas e o tempo estimado logo no início.
- Validar com o negócio se é possível **ler o contrato primeiro** e fazer a biometria por último, como confirmação de identidade.

### 7. Envio do documento de identificação — 11 menções · prioridade média

**O que os usuários dizem:**
- "Difícil anexar documento", "Leitor de documentação não reconhece o documento".
- "Não aceitou o documento em PDF", "pede pra exportar documento em PDF e é onde fica complicado".
- "Problema por conta do RG digital".
- "Não dá pra incluir passaporte".

**Causa no fluxo atual:**
- A CNH Digital tem regras rígidas e só mostradas depois do erro (R07).
- Não há aviso da ordem frente → verso (R11).
- RG digital e passaporte não são aceitos.

**Oportunidade no remake:**
- Mostrar as regras do arquivo antes de escolher, e o passo a passo de como exportar a CNH Digital.
- Usar mensagens de erro específicas, incluindo a de lado errado (R11).
- Levar ao negócio a aceitação do RG digital (CIN) e do passaporte.

### 8. Dispositivo e navegador — 7 menções · prioridade baixa

**O que os usuários dizem:**
- "Poder fazer via computador", "deixar ler em dispositivo computador".
- "Não abre no Google Chrome".
- "Poderia permitir a abertura em iPad".

**Oportunidade no remake:** a biometria precisa da câmera do celular. Mas a **leitura do contrato** poderia ser feita também no computador, por um link ou PDF enviado antes (ligação com o tema 2). Testar a compatibilidade com os principais navegadores.

### 9. Pontuais — 12 menções · prioridade baixa

- **Token:** "Sobre o código tem q ser mais claro" (000).
- **Navegação:** "O botão próximo fica escondido" (termos).
- **Contraste:** "A cor está preto no preto".
- **Orientação:** "Mais explicação".
- **Canal de envio:** "Melhorar o envio por WhatsApp", e um link que não registrou o rosto e demorou um dia para ser reenviado.
- **Fora do escopo de UX** (atendimento, preço, opinião sobre o SPF): registrados, mas não tratados no remake.

---

## Diretrizes para o remake (em ordem de prioridade)

1. **Rubrica:** opcional de verdade, com área grande, traço fino, desfazer e versão digitada. Ou deixar de existir, se o negócio permitir.
2. **Leitura do contrato:** em tela cheia, legível, com resumo dos valores, download do PDF e possibilidade de ler antes da biometria.
3. **Alternativa gov.br:** levar como proposta de negócio. No remake, deixar um ponto de entrada previsto.
4. **Captura facial:** orientação em tempo real, motivo da falha, tentativas restantes, selfie única com SPF e acessibilidade.
5. **Desempenho e estabilidade:** esperas com progresso, estado preservado e "voltar" seguro.
6. **Etapas claras:** indicador de progresso e tempo estimado. Avaliar a ordem contrato → biometria.
7. **Documento:** regras antes do envio, erros específicos e ordem frente → verso guiada.
8. **Dispositivo:** leitura do contrato também no computador e compatibilidade de navegadores.
