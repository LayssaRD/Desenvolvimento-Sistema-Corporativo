## ETAPA 1 — Apresentação do sistema

* **Nome do sistema:** Sistema de Agendamento de Serviços (Salão, Clínica, Oficina)

* **Apresentação:**
O sistema é uma plataforma desenvolvida para atuar como um catálogo centralizado de serviços e gerenciador de agendas, conectando clientes a pequenos e médios prestadores de serviços, como salões de beleza, clínicas e oficinas mecânicas (com atuação restrita ao agendamento de diagnósticos e revisões). O objetivo principal da solução é estabelecer um ambiente organizado e seguro para marcações, oferecendo autonomia para os prestadores controlarem suas agendas e permitindo que os clientes solicitem horários de forma centralizada e prática, fundamentando a segurança da plataforma em um fluxo de aprovação manual e em um sistema obrigatório de avaliações mútuas (reputação).

* **Problema:**
Pequenos e médios prestadores de serviços e seus clientes enfrentam problemas crônicos decorrentes da utilização de agendas manuais e processos informais. Essa dinâmica gera:
  * Conflitos de horários e sobreposição de marcações.
  * Esquecimentos, desorganização operacional e falta de histórico das interações.
  * Prejuízos financeiros e operacionais para os profissionais devido a ausências sem aviso prévio (no-shows) e falta de garantias de compromisso.
  * Dificuldade e atritos para os clientes localizarem profissionais, verificarem disponibilidades reais e realizarem marcações.

* **Contexto:**
O problema ocorre no ecossistema de atendimento de prestadores de serviços de pequeno e médio porte — abrangendo múltiplos domínios como salões de beleza, clínicas e oficinas mecânicas. Nesses ambientes, a marcação de horários costuma ocorrer de forma manual ou descentralizada. No caso específico das oficinas mecânicas, o contexto restringe-se exclusivamente à etapa de agendamento de revisões e diagnósticos (cujos tempos são definidos por blocos cadastrados), enquanto os serviços de conserto e execução de manutenção ocorrem de maneira independente da plataforma.

## ETAPA 2 — Quadro de conhecimento atual

| ID | Tipo | Descrição | Evidência / Como validar / Justificativa | Estado |
| :--- | :--- | :--- | :--- | :--- |
| F01 | FATO | Agendas manuais geram conflitos, esquecimentos e falta de histórico. | Constatado na análise inicial do problema e validado no contexto de pequenos e médios prestadores de serviços. | Confirmado |
| F02 | FATO | O tempo e o valor de uma manutenção veicular (após diagnóstico) são variáveis e não padronizáveis em um catálogo simples. | Evidência: Afirmação do usuário durante a conversa. | Confirmado |
| F03 | FATO | A plataforma opera sem processamento de pagamentos ou cobranças financeiras em sua versão inicial. | Constatado pela decisão de escopo do MVP focada apenas em agendamento e reputação. | Confirmado |
| F04 | FATO | O fluxo de agendamento exige a aprovação manual prévia por parte do prestador de serviços. | Constatado nas premissas de autonomia e segurança da agenda. | Confirmado |
| F05 | FATO | A avaliação mútua entre cliente e prestador é obrigatória após a conclusão do atendimento. | Constatado nas regras de segurança sistêmica adotadas para substituir o módulo financeiro. | Confirmado |
| H01 | HIPÓTESE | O sistema de avaliações mútuas e o limite numérico de agendamentos inibirão reservas falsas e faltas, mesmo sem cobrança financeira. | *Por que é hipótese:* O comportamento humano pode não ser totalmente contido apenas por reputação, especialmente em contas recém-criadas.<br>*Como validar:* Monitorar a taxa de no-show (não comparecimento) e de perfis falsos durante os primeiros meses de operação do sistema. | Aberta |
| H02 | HIPÓTESE | Os prestadores terão o hábito e a disponibilidade de aprovar ou recusar solicitações manualmente em tempo hábil. | *Por que é hipótese:* Em oficinas ou salões movimentados, o profissional pode não olhar o aplicativo com frequência.<br>*Como validar:* Acompanhar o tempo médio de resposta dos prestadores e a taxa de agendamentos expirados automaticamente. | Aberta |
| H03 | HIPÓTESE | A exigência de antecedência mínima de 12 horas reduzirá cancelamentos em cima da hora por parte dos clientes. | *Por que é hipótese:* Clientes ainda podem tentar desmarcar de última hora por imprevistos pessoais.<br>*Como validar:* Analisar o volume de cancelamentos ocorridos fora da janela permitida. | Aberta |
| H04 | HIPÓTESE | O bloqueio sistêmico (Hard Block) por falta de avaliação forçará o preenchimento dos dados sem afastar os usuários da plataforma. | *Por que é hipótese:* Usuários podem se irritar com o bloqueio e abandonar o aplicativo em vez de avaliar.<br>*Como validar:* Medir a taxa de retenção e o tempo médio que os usuários demoram para destravar a conta após uma pendência. | Aberta |
| H05 | HIPÓTESE | A restrição de oficinas mecânicas estritamente a diagnósticos e revisões simplificará a adoção da ferramenta sem gerar atritos operacionais. | *Por que é hipótese:* Oficinas podem esperar que a plataforma faça a gestão completa do tempo de reparo físico.<br>*Como validar:* Coletar feedback qualitativo dos mecânicos durante o uso piloto. | Aberta |
| Q01 | QUESTÃO EM ABERTO | Qual é o tempo exato de tolerância (timeout) até que uma solicitação pendente seja considerada recusada automaticamente? | *Quem pode responder:* Equipe de negócios/Produto. | Aberta |
| Q02 | QUESTÃO EM ABERTO | Como será calculado o limite de agendamentos por cliente (ex.: limite diário, semanal, ou apenas solicitações pendentes simultâneas)? | *Quem pode responder:* Equipe de negócios/Produto. | Aberta |
| Q03 | QUESTÃO EM ABERTO | Como os clientes e prestadores novos (sem histórico de avaliação) serão tratados na plataforma? | *Quem pode responder:* Equipe de negócios/Produto. | Aberta |
| D01 | DECISÃO | O sistema agendará apenas diagnósticos/revisões para oficinas mecânicas. | *Justificativa:* Isola a plataforma da complexidade de rastrear tempos e valores variáveis da execução do serviço corretivo. | Atual |
| D02 | DECISÃO | A plataforma não processará pagamentos. | *Justificativa:* Atuará apenas como catálogo e organizador de agenda, reduzindo drasticamente a complexidade técnica e a responsabilidade legal do MVP. | Atual |
| D03 | DECISÃO | O fluxo de agendamento exigirá aprovação manual do prestador. | *Justificativa:* Permite que o profissional avalie a reputação do cliente antes de confirmar, mitigando riscos de cancelamento e trotes. | Atual |
| D04 | DECISÃO | O horário ficará bloqueado durante a pendência de aprovação e será exigida antecedência mínima de 12 horas. | *Justificativa:* Impede concorrência direta pelo mesmo horário e garante tempo hábil para o prestador se organizar e responder. | Atual |

## ETAPA 3 — Escolha do fluxo principal

* **Objetivo do fluxo:** Permitir que o cliente solicite um agendamento de serviço ou diagnóstico, que passa por validações de regras de negócio e aprovação manual do prestador, garantindo a reserva do horário, a execução do atendimento e a alimentação do sistema de reputação por meio de avaliações mútuas obrigatórias.
* **Quem inicia:** O cliente.
* **Ponto de início:** O cliente acessa o catálogo da plataforma, seleciona um prestador e um serviço específico, define a data e o horário desejados (com antecedência mínima de 12 horas) e aciona a opção de envio da solicitação de agendamento.
* **Resultado esperado que indica sua conclusão:** O ciclo de vida do agendamento é encerrado após a realização do serviço (ou registro de ausência), com o envio bem-sucedido das avaliações obrigatórias por parte do cliente e do prestador (ou a aplicação dos bloqueios sistêmicos correspondentes por falta de preenchimento), restabelecendo a regularidade das contas envolvidas.

## ETAPA 4 — Reconstrução do fluxo principal

Para cumprir o objetivo de estruturar o fluxo de ponta a ponta — integrando recuperação de dados, escolhas, validações, processamentos e tomadas de decisão —, o ciclo principal do sistema encadeia-se da seguinte forma:

1. **Início:** O fluxo é iniciado por iniciativa do cliente, que acessa a plataforma com o propósito de agendar um atendimento em um salão de beleza, clínica ou oficina mecânica (estritamente para diagnósticos/revisões).
2. **Recuperar:** O sistema consulta o catálogo centralizado e recupera os dados dos prestadores cadastrados, suas respectivas especialidades e a grade de horários disponíveis em suas agendas base.
3. **Escolha:** O cliente seleciona o prestador desejado, escolhe o tipo de serviço e define a data e o horário pretendidos para o atendimento.
4. **Validar:** O sistema intercepta a intenção de compra e executa checagens críticas de elegibilidade:
   * Verifica se a antecedência da solicitação atende à regra mínima de 12 horas.
   * Checa se o cliente excedeu o limite máximo de agendamentos pendentes simultâneos.
   * Avalia se o cliente possui pendências de avaliações anteriores que resultem em bloqueio sistêmico (*Hard Block*).
5. **Processar (Reserva Temporária):** Caso todas as validações sejam bem-sucedidas, o sistema gera o registro do agendamento com o status **"Pendente"** e aplica um bloqueio provisório no horário correspondente dentro da agenda do prestador, impedindo concorrência de reservas simultâneas.
6. **Decisão (Aprovação do Prestador):** O prestador analisa a solicitação pendente, verificando o histórico e a reputação do cliente na plataforma. A partir disso, ocorre uma bifurcação decisória:
   * *Caminho A (Aprovação):* O prestador aceita o pedido, transformando o status em **"Confirmado"** e tornando o bloqueio da agenda definitivo.
   * *Caminho B (Recusa ou Timeout):* O prestador recusa o pedido ativamente, ou o tempo limite de resposta (*timeout*) expira; o sistema cancela a solicitação e libera o horário imediatamente de volta ao catálogo.
7. **Processamento Pós-Atendimento:** Na data marcada, após a realização física do serviço, o prestador registra o comparecimento (marcando como **"Concluído"** ou **"Não Compareceu"**), dando início ao processo obrigatório de feedback.
8. **Resultado Final:** O fluxo atinge sua conclusão com o preenchimento das avaliações mútuas. O sistema atualiza as notas de reputação de ambas as partes (aplicando eventuais bloqueios de conta se os prazos de avaliação forem estourados), encerrando o ciclo de vida do agendamento e restabelecendo a aptidão dos usuários para novas interações na plataforma.

## ETAPA 5 — Análise das etapas do fluxo

**Passo 1: Cliente solicita agendamento (Reserva Temporária)**
* **Quem age:** Cliente (inicia) e Sistema (valida).
* **Entrada:** ID do prestador, ID do serviço/diagnóstico, data e horário desejados.
* **Saída:** Um registro de agendamento criado com status **"Pendente"** e o horário selecionado sendo **bloqueado temporariamente** na disponibilidade do prestador.
* **Decisão:** (Decisão do Sistema). O sistema avalia: A antecedência é igual ou maior que 12 horas? O cliente possui reputação mínima? O cliente excedeu o limite de agendamentos pendentes simultâneos?
* **O que pode impedir:** 
  * Regra de negócio: A antecedência solicitada ser inferior a 12 horas.
  * Regra de negócio: O cliente ter atingido o limite máximo de agendamentos em aberto.
  * Concorrência de banco de dados: Outro usuário ter reservado o mesmo horário uma fração de segundo antes.

---

**Passo 2: Prestador avalia a solicitação**
* **Quem age:** Prestador (decide) e Sistema (executa).
* **Entrada:** A solicitação "Pendente" gerada na Etapa 1 e os dados do cliente (histórico e média de avaliações).
* **Saída:** Atualização do status do agendamento para **"Confirmado"** (mantendo o bloqueio da agenda de forma definitiva) OU **"Recusado"** (liberando o horário imediatamente de volta no catálogo).
* **Decisão:** (Decisão Humana). O prestador decide, com base na avaliação do cliente, se deseja assumir o compromisso e prestar o serviço.
* **O que pode impedir:** 
  * Situação de negócio: O prestador esquecer de responder, demorar demais ou não ver a notificação.
  * Restrição de Sistema: O tempo de tolerância (timeout) para a resposta expirar, forçando o sistema a cancelar o pedido automaticamente antes que o prestador consiga interagir com ele.

---

**Passo 3: Registro de Comparecimento e Avaliações Obrigatórias**
* **Quem age:** Prestador (registra comparecimento e avalia), Cliente (avalia) e Sistema (processa reputação e aplica bloqueios).
* **Entrada:** O agendamento com status "Confirmado" cujo horário já tenha passado, o status informando se o cliente compareceu ou não, e as notas das avaliações.
* **Saída:** O status do agendamento muda para **"Concluído"** (se compareceu) ou **"Não Compareceu"**; as médias de reputação de ambos são recalculadas no banco de dados.
* **Decisão:** 
  * (Decisão do Prestador): O serviço foi realizado ou o cliente faltou?
  * (Decisão do Sistema - Hard Block): O sistema verifica se o cliente realizou a avaliação imediata para liberar novos agendamentos. O sistema verifica se o prestador estourou a janela de 24 horas para avaliar, ativando o bloqueio da conta dele caso verdadeiro.
* **O que pode impedir:**
  * Regra de tempo: O prestador tentar marcar como "Concluído" antes de a data/hora agendadas realmente passarem.
  * Falha humana punida (Enforcement): O fluxo travar porque o sistema impede o cliente de acessar o catálogo, ou impede o prestador de ver sua agenda, até que a pendência de avaliação obrigatória seja resolvida.

## ETAPA 6 — Caminho feliz, variação e falha

Para demonstrar que o sistema opera considerando múltiplos desdobramentos reais além do sucesso absoluto, a modelagem contempla os seguintes caminhos:

* **1. Fluxo Principal (Caminho Feliz):**
  * **Descrição:** Representa o percurso ideal de ponta a ponta sem intercorrências. O cliente localiza um serviço no catálogo, envia uma solicitação de agendamento com mais de 12 horas de antecedência e sem pendências de avaliações. O sistema valida as regras, cria o pedido com status **"Pendente"** e bloqueia temporariamente o horário. O prestador analisa o perfil do cliente e **aprova** o pedido, alterando o status para **"Confirmado"** (consolidando o bloqueio da agenda). Na data marcada, o atendimento ocorre, o prestador registra a conclusão (**"Concluído"**) e ambas as partes preenchem as avaliações mútuas obrigatórias no prazo, encerrando o ciclo com sucesso.

* **2. Variação de Negócio:**
  * **Descrição:** Condição válida de negócio que altera o percurso padrão após a solicitação. O cliente envia o pedido de agendamento e o sistema bloqueia temporariamente o horário. Contudo, ao analisar a solicitação, o prestador decide **recusar** ativamente o atendimento (ou o tempo limite de resposta do prestador – *timeout* – expira sem interação). O sistema intercepta essa condição de negócio, cancela o pedido e **libera imediatamente o horário bloqueado** de volta ao catálogo público, permitindo que o cliente busque outra alternativa.

* **3. Situação de Falha:**
  * **Descrição:** Ocorre quando um elemento necessário ao processamento falha ou sofre impedimento técnico/operacional. Um exemplo crítico é o **conflito de concorrência por concorrência de banco de dados**: dois clientes distintos tentam solicitar o mesmo horário exato na agenda do prestador em uma fração de milissegundo. O sistema processa com sucesso a primeira transação (bloqueando o slot), mas a segunda requisição falha ao tentar efetivar o bloqueio físico no banco de dados. O sistema intercepta a falha de concorrência, aborta a segunda solicitação e exibe um aviso imediato na interface informando que o horário acabou de ser ocupado, solicitando que o usuário escolha outro slot disponível.

## ETAPA 7 — Operações derivadas do fluxo

Com base no fluxo principal, nas variações e nas falhas mapeadas, o sistema precisa ser capaz de sustentar todas as etapas por meio de operações de domínio específicas. As 7 principais operações identificadas diretamente a partir do fluxo são:

1. **Consultar Catálogo de Serviços:** Recuperar os dados dos prestadores, suas especialidades e a grade de horários disponíveis para que o cliente realize a busca e a seleção inicial.
2. **Validar Elegibilidade do Cliente:** Checar se a solicitação atende à antecedência mínima de 12 horas, se o cliente não estourou o limite de agendamentos pendentes e se não possui bloqueios ativos (*Hard Block*) decorrentes de avaliações pendentes.
3. **Criar Solicitação e Bloquear Horário:** Registrar o agendamento com o status **"Pendente"** e aplicar um bloqueio provisório no slot correspondente da agenda do prestador para evitar concorrência de reservas simultâneas.
4. **Processar Decisão do Prestador:** Permitir que o prestador analise o perfil e o histórico do cliente, decidindo por **aprovar** (tornando o agendamento definitivo) ou **recusar** o pedido.
5. **Expirar Solicitações Automaticamente (*Job* de Timeout):** Monitorar o tempo limite de resposta das solicitações pendentes, cancelando de forma automática os pedidos que estouraram o prazo e liberando os horários de volta ao catálogo.
6. **Registrar Desfecho do Atendimento:** Permitir que o prestador informe o status real após a data agendada, definindo se o serviço foi **"Concluído"** ou se ocorreu ausência (**"Não Compareceu"**).
7. **Registrar Avaliações Mútuas:** Coletar as notas e comentários de cliente e prestador após o atendimento, atualizando o histórico de reputação e aplicando eventuais bloqueios de conta se os prazos de preenchimento estourarem.

## ETAPA 8 — Detalhamento de três operações

Abaixo estão detalhadas três operações fundamentais que sustentam o fluxo principal do sistema, representadas por meio da estrutura de Entrada, Processamento, Saída, Regras e Impedimentos:

### 1. Operação: Solicitar Agendamento

| Campo | Descrição |
| :--- | :--- |
| **Nome da operação** | Solicitar Agendamento |
| **Objetivo** | Permitir que o cliente escolha um horário disponível, execute validações de elegibilidade e crie uma intenção de agendamento com status pendente e bloqueio provisório da agenda. |
| **Entrada** | ID do Cliente, ID do Prestador, ID do Serviço/Diagnóstico, Data e Horário pretendidos. |
| **Processamento** | 1. Verificar se a antecedência em relação ao horário solicitado é de pelo menos 12 horas.<br>2. Checar se o cliente não atingiu o limite de agendamentos pendentes simultâneos.<br>3. Validar se o cliente não possui bloqueios ativos (*Hard Block*) por falta de avaliações passadas.<br>4. Verificar se o slot na agenda do prestador está livre (prevenção de concorrência).<br>5. Criar registro de agendamento com status "Pendente" e aplicar bloqueio temporário no slot. |
| **Saída** | Registro de agendamento criado com status "Pendente", horário bloqueado temporariamente na agenda do prestador e notificação de solicitação enviada. |
| **Regra ou condição envolvida** | O agendamento exige antecedência matemática mínima de 12 horas e o cliente não pode possuir pendências ativas de avaliação bloqueando sua conta. |
| **Possível impedimento** | Concorrência de banco de dados (outro usuário reservar o mesmo slot milissegundos antes) ou descumprimento das regras de antecedência e limite de pedidos. |

---

### 2. Operação: Processar Decisão do Prestador

| Campo | Descrição |
| :--- | :--- |
| **Nome da operação** | Processar Decisão do Prestador (Aprovar/Recusar Solicitação) |
| **Objetivo** | Permitir que o prestador analise uma solicitação pendente e decida por efetivar o agendamento (confirmando-o) ou rejeitá-lo, liberando o horário. |
| **Entrada** | ID do Agendamento, ID do Prestador, Decisão (APROVADO ou RECUSADO). |
| **Processamento** | 1. Validar se o agendamento pertence ao prestador autenticado e está com status "Pendente".<br>2. Se a decisão for **Aprovar**: alterar o status para "Confirmado" e tornar o bloqueio da agenda definitivo.<br>3. Se a decisão for **Recusar**: alterar o status para "Recusado" e liberar o slot de horário de volta ao catálogo público.<br>4. Registrar o carimbo de tempo (*timestamp*) da decisão. |
| **Saída** | Agendamento atualizado com status "Confirmado" ou "Recusado" e agenda do prestador ajustada (bloqueada definitivamente ou liberada). |
| **Regra ou condição envolvida** | O prestador só pode responder a solicitações que estejam estritamente no estado "Pendente" e dentro do prazo limite de resposta (*timeout*). |
| **Possível impedimento** | O pedido já ter expirado automaticamente pelo sistema via rotina de *timeout* antes da ação do prestador. |

---

### 3. Operação: Registrar Avaliações Mútuas

| Campo | Descrição |
| :--- | :--- |
| **Nome da operação** | Registrar Avaliações Mútuas |
| **Objetivo** | Coletar as notas e comentários de cliente e prestador após a conclusão do atendimento, atualizando os índices de reputação e liberando eventuais restrições sistêmicas. |
| **Entrada** | ID do Agendamento, ID do Avaliador (Cliente ou Prestador), Nota (1 a 5), Comentário opcional. |
| **Processamento** | 1. Verificar se o agendamento está com status "Concluído" (ou "Não Compareceu" elegível para avaliação).<br>2. Validar se o usuário faz parte daquela relação e ainda não realizou sua avaliação.<br>3. Salvar a nota e o comentário vinculados ao perfil avaliado.<br>4. Recalcular a média de reputação do usuário.<br>5. Remover pendências de avaliação da conta do avaliador (impedindo a incidência do *Hard Block*). |
| **Saída** | Avaliação registrada com sucesso, nota média do usuário recalculada e conta do avaliador liberada de pendências. |
| **Regra ou condição envolvida** | A avaliação é estritamente obrigatória para ambas as partes; o não preenchimento dentro da janela regulamentar resulta em bloqueio temporário da conta (*Hard Block*). |
| **Possível impedimento** | O prazo limite para avaliação ter expirado ou o usuário tentar avaliar um atendimento do qual não participou ou que não foi marcado como concluído. |

## ETAPA 9 — Informações necessárias ao sistema

A partir dos fluxos e operações analisados, o sistema precisa conhecer, processar e preservar um conjunto essencial de informações conceituais para que o modelo de negócio funcione corretamente, sem a necessidade de modelagem de tabelas, chaves estrangeiras ou atributos técnicos neste momento:

* **Disponibilidade base do prestador:** Blocos de tempo que o profissional dedica a novos agendamentos e revisões.
  * *Por que precisa existir:* O negócio precisa preservar essa informação para compor a busca centralizada no catálogo e permitir que o cliente visualize os horários reais disponíveis, evitando conflitos e sobreposições na agenda do prestador.

* **Status do Agendamento:** O ciclo de vida da reserva, contemplando estritamente os estados *Pendente*, *Confirmado*, *Recusado*, *Expirado*, *Concluído* e *Não Compareceu*.
  * *Por que precisa existir:* O negócio precisa preservar essas transições de estado para refletir a etapa real em que cada reserva se encontra, viabilizando o bloqueio temporário de horários contra concorrência de reservas e governando as ações subsequentes de aprovação, expiração automática e fechamento.

* **Timestamp da solicitação:** A data e a hora exatas em que o pedido de agendamento foi gerado.
  * *Por que precisa existir:* O negócio precisa preservar essa informação temporal para calcular matematicamente a regra de antecedência mínima de 12 horas e governar o mecanismo de expiração automática (*timeout*) das solicitações que aguardam a resposta do prestador.

* **Histórico de Avaliações e Reputação:** Notas, comentários agregados e o status de preenchimento das avaliações vinculadas a clientes e prestadores.
  * *Por que precisa existir:* O negócio precisa preservar esse histórico para alimentar o sistema de reputação (que atua como barreira de segurança na ausência de pagamentos), embasar a decisão manual de aprovação do prestador e aplicar o bloqueio sistêmico (*Hard Block*) a usuários inadimplentes em avaliações ou reincidentes em faltas (*no-shows*).

## ETAPA 10 — O que ainda não sabemos?

Ao retornar ao quadro inicial e aos limites do conhecimento atual da equipe após a modelagem do fluxo, estruturam-se os pontos de incerteza e os limites analíticos do projeto:

* **1. Quais hipóteses continuam abertas?**
  * **H01 (Eficácia da reputação sem pagamentos):** A hipótese de que o sistema de avaliações mútuas e o limite numérico de agendamentos serão suficientes para inibir reservas falsas e faltas (*no-shows*), mesmo na ausência de transações financeiras.
  * **H02 (Disponibilidade dos prestadores):** A suposição de que os prestadores (salões, clínicas e oficinas) terão hábito e disponibilidade operacional para responder às solicitações manuais dentro do prazo limite.
  * **H03, H04 e H05:** A eficácia da antecedência mínima de 12 horas na redução de cancelamentos em cima da hora, a aceitação do bloqueio sistêmico (*Hard Block*) pelos usuários e a premissa de que restringir oficinas estritamente a diagnósticos simplificará a adoção.

* **2. Quais hipóteses foram confirmadas ou rejeitadas durante o trabalho?**
  * Nenhuma hipótese foi formalmente testada, confirmada empiricamente ou rejeitada por dados de campo, uma vez que o projeto encontra-se em fase de modelagem de MVP. Contudo, conceitualmente, a premissa de que a exclusão de pagamentos exigiria um mecanismo comportamental forte foi validada e convertida em uma regra de domínio central (o sistema de avaliações obrigatórias e o *Hard Block*).

* **3. Quais questões ainda precisam ser respondidas?**
  * **Q01:** Qual será o tempo exato de tolerância (*timeout*) em minutos ou horas até que uma solicitação pendente seja considerada recusada automaticamente?
  * **Q02:** Como será calculado matematicamente o limite de agendamentos por cliente (ex.: limite diário, semanal ou apenas solicitações simultâneas em aberto)?
  * **Q03:** Como os usuários recém-chegados (clientes e prestadores sem histórico prévio de reputação) serão inicializados e tratados pela plataforma?

* **4. Qual parte do fluxo apresenta maior incerteza?**
  * O intervalo entre a **solicitação pendente e a aprovação manual do prestador**. Esta etapa carrega a maior incerteza por depender inteiramente do fator humano (se o prestador abrirá o aplicativo a tempo) e do alinhamento matemático delicado entre o prazo de resposta (*timeout*) e a regra de antecedência de 12 horas.

* **5. Que informação nova poderia provocar mudanças no fluxo?**
  * Dados de pesquisa ou testes de usabilidade indicando que os prestadores de serviços ignoram notificações em aplicativos e preferem canais de mensagens instantâneas (como WhatsApp). Se isso se confirmar, o fluxo de aprovação precisará ser redesenhado para suportar interações via canais externos integrados.

* **6. Que decisão tomada pela equipe pode precisar ser revisada?**
  * A decisão de exigir **aprovação manual obrigatória para 100% dos agendamentos**. Essa regra pode se tornar um gargalo operacional insustentável para prestadores com alto volume de atendimento diário, exigindo futuramente uma revisão para permitir "aprovação automática" para clientes que possuem excelente reputação consolidada.

* **7. Que decisões técnicas ainda não possuem evidência suficiente para serem tomadas?**
  * A definição da arquitetura de software definitiva (ex.: escolha entre um monólito modular ou microsserviços) e a tecnologia exata de mensageria assíncrona para gerenciar os disparos de expiração por *timeout*. Como o escopo de negócio ainda está em fase de validação conceitual, detalhar a infraestrutura técnica agora seria prematuro.

## J. Contradições ou fragilidades
* **Fragilidade na regra de antecedência:** Se o agendamento exige 12 horas de antecedência, o tempo limite de expiração (timeout) precisa ser matematicamente inferior a isso, caso contrário, uma reserva pode expirar quando o horário já passou.
* **Decisões descartadas:** O documento inicial previa um módulo de Pagamento para processar sinais. Essa premissa foi tratada como fato na proposta, mas foi descartada na conversa para viabilizar o MVP.
* **Decisões técnicas antecipadas:** A proposta inicial fixou uma arquitetura monolítica modular e divisão estrita em quatro camadas. Embora defensável, a equipe não deve engessar essas decisões antes de mapear completamente os novos estados do agendamento (pendência, expiração automática).

## L. Avaliação da maturidade da análise
**RAZOAVELMENTE FUNDAMENTADA**

A conversa conseguiu contornar as principais inconsistências da proposta inicial. A exclusão dos pagamentos e a limitação do escopo das oficinas (apenas revisões/diagnósticos) removeram obstáculos críticos. O fluxo central com aprovação manual e reserva temporária de horários é sólido. Contudo, ainda não se pode avançar para a modelagem definitiva sem antes parametrizar as regras de timeout e de reputação.

## M. Recomendações para a equipe
* **Definir parâmetros de tempo:** Estabeleçam exatamente qual será o tempo limite para o prestador aprovar a solicitação, garantindo que ele não entre em conflito com a regra de antecedência de 12 horas.
* **Mapear a máquina de estados do Agendamento:** Revisem o ciclo de vida do agendamento, garantindo que os estados "Pendente" e "Bloqueado Temporariamente" estejam formalizados nas regras de domínio.
* **Modelar o sistema de reputação:** Documentem como as notas serão calculadas e se haverá consequências automáticas para clientes que faltarem seguidas vezes, já que essa é a única proteção do sistema contra fraudes na agenda.

## DISCLAIMER: Uso de Inteligência Artificial

Foi utilizado a inteligência artificial principalmente como analista crítico, todos os dados gerados por ela foram validados pelos integrantes da equipe.

* Modelo utilizado: Google Gemini Pro 3.1
* Forma de utilização: Analista crítico
* Principais contribuições: Identificar buracos na lógica de bloqueio de horários
* Algumas hipóteses reveladas, questões novas que surgiram e decisões revistas foi a remoção do módulo de pagamentos e bloqueamento dos agendamentos.