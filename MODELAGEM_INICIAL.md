## A. Entendimento do problema
O sistema visa resolver a desorganização, os conflitos de horários e a falta de histórico no agendamento de pequenos e médios prestadores de serviços. O contexto abrange salões de beleza, clínicas e oficinas mecânicas (estas últimas restritas apenas ao agendamento de diagnósticos/revisões). Os grupos afetados são os clientes, que precisam de um catálogo centralizado para buscar e solicitar serviços, e os prestadores, que necessitam de controle sobre suas agendas, proteção contra ausências (no-shows) e autonomia para aceitar ou recusar clientes.

## B. Fatos identificados
* Agendas manuais geram conflitos, esquecimentos e falta de histórico.
* O tempo e o valor de uma manutenção veicular (após diagnóstico) são variáveis e não padronizáveis em um catálogo simples. Evidência: Afirmação do usuário durante a conversa.

## C. Hipóteses identificadas
* **Hipótese:** O sistema de avaliações mútuas e o limite numérico de agendamentos inibirão reservas falsas e faltas, mesmo sem cobrança financeira.
  * *Por que é hipótese:* O comportamento humano pode não ser totalmente contido apenas por reputação, especialmente em contas recém-criadas.
  * *Validação:* Monitorar a taxa de no-show (não comparecimento) e de perfis falsos durante os primeiros meses de operação do sistema.
* **Hipótese:** Os prestadores terão o hábito e a disponibilidade de aprovar ou recusar solicitações manualmente em tempo hábil.
  * *Por que é hipótese:* Em oficinas ou salões movimentados, o profissional pode não olhar o aplicativo com frequência.
  * *Validação:* Acompanhar o tempo médio de resposta dos prestadores e a taxa de agendamentos expirados automaticamente.

## D. Questões em aberto
* Qual é o tempo exato de tolerância (timeout) até que uma solicitação pendente seja considerada recusada automaticamente? 
  * *Fonte:* Equipe de negócios/Produto.
* Como será calculado o limite de agendamentos por cliente (ex.: limite diário, semanal, ou apenas solicitações pendentes simultâneas)?
  * *Fonte:* Equipe de negócios/Produto.
* Como os clientes e prestadores novos (sem histórico de avaliação) serão tratados na plataforma?
  * *Fonte:* Equipe de negócios/Produto.

## E. Decisões identificadas
* **Decisão:** O sistema agendará apenas diagnósticos/revisões para oficinas mecânicas.
  * *Justificativa:* Isola a plataforma da complexidade de rastrear tempos e valores variáveis da execução do serviço corretivo. 
* **Decisão:** A plataforma não processará pagamentos.
  * *Justificativa:* Atuará apenas como catálogo e organizador de agenda, reduzindo drasticamente a complexidade técnica e a responsabilidade legal do MVP.
* **Decisão:** O fluxo de agendamento exigirá aprovação manual do prestador.
  * *Justificativa:* Permite que o profissional avalie a reputação do cliente antes de confirmar, mitigando riscos de cancelamento e trotes.
* **Decisão:** O horário ficará bloqueado durante a pendência de aprovação e será exigida antecedência mínima de 12 horas.
  * *Justificativa:* Impede concorrência direta pelo mesmo horário e garante tempo hábil para o prestador se organizar e responder.

## F. Fluxo principal compreendido
1. O cliente localiza um prestador no catálogo e solicita um horário (com no mínimo 12 horas de antecedência).
2. O sistema valida se o cliente não excedeu seu limite de agendamentos.
3. O sistema bloqueia o horário temporariamente na agenda do prestador e altera o status do pedido para "Pendente".
4. O prestador avalia a solicitação (baseando-se no perfil e nas avaliações prévias do cliente).
5. O prestador aceita o pedido (o horário é confirmado definitivamente) OU o prestador recusa (o horário volta a ficar disponível no catálogo).
6. Após a realização do serviço, cliente e prestador avaliam um ao outro.

## G. Pontos de decisão, variações e falhas
* **Condições que alteram o fluxo:** Solicitação feita com menos de 12 horas de antecedência (deve ser bloqueada logo na interface); cliente ter atingido o limite máximo de agendamentos simultâneos.
* **Variações de negócio:** O prestador recusar ativamente o agendamento; a solicitação expirar por falta de resposta do prestador dentro do tempo limite.
* **Situações de falha:** O cliente faltar ao agendamento confirmado (impactará a avaliação, mas não há transação financeira a reverter).

## H. Operações identificadas
* Consultar catálogo (filtrando por disponibilidade, categoria e avaliação).
* Solicitar agendamento.
* Bloquear temporariamente o horário (reserva de concorrência).
* Aprovar solicitação de agendamento.
* Recusar solicitação de agendamento.
* Liberar horário bloqueado.
* Expirar solicitação pendente automaticamente (job/worker).
* Registrar avaliação mútua (cliente e prestador).

## I. Informações necessárias ao sistema
* **Disponibilidade base do prestador:** Blocos de tempo que o profissional dedica a novos agendamentos/revisões. Necessário para compor a busca.
* **Status do Agendamento:** Precisa contemplar os estados *Pendente*, *Confirmado*, *Recusado*, *Expirado*, *Concluído* e *Não Compareceu*, para refletir o ciclo de vida da reserva.
* **Timestamp da solicitação:** A data e a hora exatas em que o pedido foi feito. Necessário para calcular a expiração automática (timeout).
* **Histórico de Avaliações:** Notas e comentários de ambas as partes. Necessário para embasar a decisão manual de aprovação do prestador.

## J. Contradições ou fragilidades
* **Fragilidade na regra de antecedência:** Se o agendamento exige 12 horas de antecedência, o tempo limite de expiração (timeout) precisa ser matematicamente inferior a isso, caso contrário, uma reserva pode expirar quando o horário já passou.
* **Decisões descartadas:** O documento inicial previa um módulo de Pagamento para processar sinais. Essa premissa foi tratada como fato na proposta, mas foi descartada na conversa para viabilizar o MVP.
* **Decisões técnicas antecipadas:** A proposta inicial fixou uma arquitetura monolítica modular e divisão estrita em quatro camadas. Embora defensável, a equipe não deve engessar essas decisões antes de mapear completamente os novos estados do agendamento (pendência, expiração automática).

## K. O que ainda não sabemos
* Como será o comportamento exato das notificações ao longo deste fluxo manual (ex.: o cliente é notificado assim que o tempo expira?).
* As regras matemáticas da reputação (se clientes com nota abaixo de um limite são banidos ou apenas sinalizados).
* O tempo exato em minutos/horas que o sistema aguardará antes de expirar uma solicitação pendente.

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