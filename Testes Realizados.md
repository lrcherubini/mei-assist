## **Cenários de Teste para o Assistente Financeiro MEI**

Aqui estão dois cenários para testar o sistema de ponta a ponta, focando no fluxo de onboarding, na inteligência do CashFlowAgent e na robustez do Coordinator.

### **Cenário 1: Caminho Feliz (Onboarding \+ CashFlow Inteligente \+ Academy)**

**Objetivo:** Validar o fluxo completo para um novo usuário, a capacidade do CashFlowAgent de entender informações fornecidas de uma vez, e a transição suave para o AcademyAgent.

**Usuário (Exemplo):** MEIstar (use este nome quando o script perguntar "Qual seu usuário:")

**(Suposição: Perfil de MEIstar não existe. O sistema iniciará o Onboarding na sessão OB\_SESSION\_ID)**

1. **Início e Onboarding**  
   * 👤 MEIstar: Olá, preciso de uma ajuda para organizar minhas finanças\!  
   * **🤖 OnboardingAgent (Esperado):** Mensagem de boas-vindas e primeira pergunta do onboarding: "1 de 3 \- Qual o seu tipo de negócio? (ex: salão, e‑commerce, serviços)"  
     * *(O agente deve seguir o ONBOARD\_PROMPT, fazendo uma pergunta por vez e usando a onboarding\_session)*  
2. **Respostas do Onboarding**  
   * 👤 MEIstar: Sou designer gráfico freelancer.  
   * **🤖 OnboardingAgent (Esperado):** "2 de 3 \- Faixa de faturamento mensal? (ex: Até 1 mil / 3–10 mil / Acima 30 mil)"  
   * 👤 MEIstar: Por volta de 4 mil.  
   * **🤖 OnboardingAgent (Esperado):** "3 de 3 \- Objetivo principal com este assistente? (ex.: separar PF/PJ / controlar caixa / crédito)"  
   * 👤 MEIstar: Quero principalmente controlar meu fluxo de caixa e ver se consigo separar melhor meu dinheiro pessoal do da empresa.  
   * **🤖 OnboardingAgent (Esperado):**  
     * Chamada interna para save\_profile com os dados corretos.  
     * Mensagem: "Cadastro concluído\! Vamos começar 💰 Sou seu assistente financeiro MEI e posso te ajudar com: \* **Controle de Caixa:** ... \* **Educação Financeira:** ... Como posso te ajudar agora?"  
     * *(A partir daqui, as interações usam a session principal e o Coordinator)*  
3. **Interação com CashFlowAgent (Inteligente)**  
   * 👤 MEIstar: Quero registrar um pagamento que recebi de um cliente. Foi um projeto de logo, R$850, recebi hoje.  
   * **🤖 Coordinator (Esperado, internamente):** Chama get\_profile, analisa a intenção e transfere para CashFlowAgent.  
   * **🤖 CashFlowAgent (Esperado):** "Entendido, MEIstar\! Registrando uma ENTRADA de R$850,00 para 'Pagamento projeto de logo' (ou algo similar inferido) que aconteceu hoje. Como você é designer gráfico freelancer, em qual categoria podemos classificar essa entrada? Geralmente é 'Vendas de Serviços' ou 'Recebimento por Projeto'."  
     * *(Observar: O agente deve ter extraído ttype='entrada', amount=850, description (inferida), date='hoje'. Ele só pergunta pela category e personaliza com o sector.)*  
4. **Continuando com CashFlowAgent**  
   * 👤 MEIstar: Pode ser 'Vendas de Serviços'.  
   * **🤖 CashFlowAgent (Esperado):** "Perfeito\! Então ficou assim: uma entrada de R$850,00 no dia \[data atual\], referente a 'Pagamento projeto de logo', na categoria 'Vendas de Serviços'. Tudo certo?"  
   * 👤 MEIstar: Sim\!  
   * **🤖 CashFlowAgent (Esperado):** "Anotado com sucesso\! 📝 Cada registro é um passo firme para o sucesso do seu negócio\!"  
     * *(Verificar se add\_transaction foi chamado corretamente).*  
5. **Transição para AcademyAgent**  
   * 👤 MEIstar: Agora, fiquei curioso sobre o que é pró-labore, já que quero separar o dinheiro.  
   * **🤖 Coordinator (Esperado, internamente):** Analisa a intenção e transfere para AcademyAgent.  
   * **🤖 AcademyAgent (Esperado):** "Olá, MEIstar\! Pró-labore é como se fosse o 'salário do dono' do negócio. É um valor fixo que você define para retirar da sua empresa MEI para seus gastos pessoais, ajudando a separar as finanças. Essa ideia inicial ajudou a clarear um pouco? Quer que eu explique com um pouco mais de detalhe, talvez mostrando como isso te ajuda a separar o dinheiro pessoal do da sua atividade como designer gráfico freelancer?"  
     * *(Observar a micro-pílula, a oferta de aprofundamento e a personalização).*  
6. **Finalização**  
   * 👤 MEIstar: Por enquanto é só, obrigado\!  
   * **🤖 AcademyAgent (Esperado):** "De nada, MEIstar\! Se tiver mais dúvidas, é só chamar. Sucesso com seus projetos de design\! 👍"  
   * 👤 MEIstar: sair  
   * *(Sistema encerra)*

#### **Teste realizado**

Digite 'sair' para terminar.  
🤖 OnboardingAgent: Boas vindas\! Que bom ter você por aqui. 😊

Para começarmos, preciso te fazer 3 perguntinhas rápidas para te conhecer melhor, ok?

1 de 3 \- Qual o seu tipo de negócio? (ex: salão, e‑commerce, serviços)

👤 MEIstar: Sou designer gráfico freelancer.  
🤖 OnboardingAgent: 2 de 3 \- Qual sua faixa de faturamento mensal? (ex: Até 1 mil / 1-2 mil / 2-3 mil / 3-4 mil / 4-5 mil / 5-6 mil / 6-8 mil / 8-10 mil / 10-15 mil / 15-20 mil / 20-25 mil / 25-30 mil / Acima 30 mil)

👤 MEIstar:  Por volta de 4 mil.  
🤖 OnboardingAgent: 3 de 3 \- Qual o seu objetivo principal com este assistente? (ex.: separar PF/PJ / controlar caixa / crédito)

👤 MEIstar: Quero principalmente controlar meu fluxo de caixa e ver se consigo separar melhor meu dinheiro pessoal do da empresa.  
save profile  
🤖 OnboardingAgent: Cadastro concluído\! Vamos começar 💰

Sou seu assistente financeiro MEI e posso te ajudar com:  
\* \*\*Controle de Caixa:\*\* Registre suas vendas e despesas, e veja resumos do seu fluxo de caixa. (Ex: "registrar uma venda de R$50" ou "qual meu saldo este mês?")  
\* \*\*Educação Financeira:\*\* Tire dúvidas sobre conceitos financeiros para gerenciar melhor seu negócio. (Ex: "o que é capital de giro?" ou "como faço para calcular o preço de um produto?")

Como posso te ajudar agora?

👤 MEIstar: Quero registrar um pagamento que recebi de um cliente. Foi um projeto de logo, R$850, recebi hoje.  
🤖 CashFlowAgent: Olá\! Que bom que está registrando essa entrada no seu negócio de serviços\! Vi aqui que seu objetivo é controlar o caixa e separar suas finanças pessoais das do MEI, então bora lá\!

Entendi\! Você recebeu R$850,00 hoje por um projeto de logo. Para finalizarmos o lançamento, em qual categoria podemos classificar esse recebimento? Podemos usar "Serviços Prestados", por exemplo.  
👤 MEIstar: Pode ser 'Vendas de Serviços'.  
🤖 CashFlowAgent: Excelente\! Então ficou assim: uma ENTRADA de R$850,00 no dia de hoje, referente a 'projeto de logo', na categoria 'Vendas de Serviços'. Tudo certo?

👤 MEIstar: sim  
🤖 CashFlowAgent: Anotado com sucesso\! 📝 Cada registro é um passo firme para o sucesso do seu negócio\!

👤 MEIstar: Agora, fiquei curioso sobre o que é pró-labore, já que quero separar o dinheiro.  
🤖 AcademyAgent: Pró-labore é o "salário" do MEI, ou seja, a retirada que você faz da sua empresa para pagar o seu trabalho. É diferente de lucro, que é o que sobra depois de pagar todas as contas e o seu pró-labore.

Essa ideia inicial te ajudou a clarear um pouco? Quer que eu explique com um pouco mais de detalhe ou dê um exemplo prático de como isso funciona para um negócio como o seu, de serviços?

👤 MEIstar:  Por enquanto é só, obrigado\!  
🤖 AcademyAgent: Disponha\!

👤 MEIstar: sair

### 

### ---

### **Cenário 2: Caminho Triste (Usuário Vago, Informações Picadas, Tentativa de Confundir)**

**Objetivo:** Testar a resiliência do Coordinator e a capacidade do CashFlowAgent de lidar com informações incompletas ou fornecidas de forma não ideal, além de testar a "Dica de Ouro PF/PJ".

**Usuário (Exemplo):** MEIstar (ou o ID usado no Cenário 1, garantindo que o perfil já existe).

**(Suposição: Perfil de MEIstar JÁ EXISTE. O sistema NÃO deve iniciar o Onboarding.)**

1. **Início Vago**  
   * 👤 MEIstar: E aí, preciso de ajuda.  
   * **🤖 Coordinator (Esperado):** "Olá MEIstar\! Vi que você é designer gráfico freelancer e seu objetivo é controlar o caixa e separar PF/PJ. Como posso te ajudar especificamente hoje? Quer registrar algo, tirar uma dúvida sobre finanças?"  
     * *(Coordinator usa get\_profile e tenta direcionar o usuário).*  
2. **Informação Incompleta para CashFlowAgent**  
   * 👤 MEIstar: Anota um gasto aí.  
   * **🤖 Coordinator (Esperado, internamente):** Transfere para CashFlowAgent.  
   * **🤖 CashFlowAgent (Esperado):** "Olá MEIstar\! Claro, vamos anotar esse gasto. Para começar, esse dinheiro SAIU do caixa do seu negócio, certo? E o que foi essa movimentação? Por exemplo: 'Compra de software', 'Pagamento de anúncio'."  
     * *(Inferiu ttype='saida' por "gasto", mas pede description pois não foi dada).*  
3. **Informações Picadas e Tentativa de Desvio**  
   * 👤 MEIstar: Foi um software. Mas antes, o que é melhor, pagar imposto mensal ou anual?  
   * **🤖 CashFlowAgent (Esperado):** "Entendi, um software\! Para registrar o gasto do software, preciso de mais alguns detalhes. Sobre sua pergunta do imposto, essa é uma dúvida mais conceitual. Se quiser, depois de registrarmos o gasto, posso te direcionar para o nosso especialista em educação financeira para ele te explicar sobre os impostos do MEI. Pode ser? Agora, sobre o software: qual foi o valor e quando você comprou?"  
     * *(Observar: O CashFlowAgent deve tentar manter o foco na sua tarefa atual (registrar o gasto), mas reconhecer a pergunta paralela e sugerir o AcademyAgent para DEPOIS. Ele não deve tentar responder sobre impostos nem abandonar o registro).*  
4. **Continuando o Registro Picado**  
   * 👤 MEIstar: Ah, ok. O software foi 50 reais.  
   * **🤖 CashFlowAgent (Esperado):** "Certo, R$50,00 para o software. E quando foi essa compra?"  
   * 👤 MEIstar: Semana passada.  
   * **🤖 CashFlowAgent (Esperado):** "Ok, semana passada (vou considerar \[data de 7 dias atrás formatada\]). Agora, em qual categoria essa compra de software se encaixa melhor? Talvez 'Despesas com Ferramentas/Software'? E só uma perguntinha para ajudar na organização: esse gasto com o software foi algo diretamente para seu trabalho como designer gráfico freelancer, ou foi um software para uso mais pessoal que você pagou com o dinheiro do MEI?"  
     * *(Aplica a "Dica de Ouro PF/PJ" devido à natureza do gasto).*  
5. **Resposta Ambígua para PF/PJ**  
   * 👤 MEIstar: Eu uso ele mais para trabalho, mas às vezes brinco com ele em casa.  
   * **🤖 CashFlowAgent (Esperado):** "Entendi\! Se o uso principal é para o seu trabalho como designer, podemos registrar como uma despesa do seu MEI. Se uma parte significativa fosse pessoal, poderíamos pensar em 'Retirada Pessoal'. Como o foco é trabalho, vamos manter como despesa do negócio na categoria 'Despesas com Ferramentas/Software'. Então ficou: uma saída de R$50,00 no dia \[data da semana passada formatada\], referente a 'Compra de software', na categoria 'Despesas com Ferramentas/Software'. Tudo certo?"  
6. **Confirmação e Tentativa de Nova Pergunta Conceitual**  
   * 👤 MEIstar: Sim. Agora me explica o imposto.  
   * **🤖 CashFlowAgent (Esperado):** "Anotado com sucesso\! 📝 Sobre sua dúvida do imposto, vou te passar para nosso especialista\!"  
     * *(Internamente, o controle volta para o Coordinator que então transfere para o AcademyAgent).*  
   * **🤖 Coordinator (Esperado, internamente):** Transfere para AcademyAgent.  
   * **🤖 AcademyAgent (Esperado):** "Olá MEIstar\! Sobre os impostos do MEI, o principal é o DAS (Documento de Arrecadação do Simples Nacional), que é um valor fixo mensal que já inclui sua contribuição para o INSS e os impostos devidos (ICMS e/ou ISS, dependendo da sua atividade como designer gráfico). Essa é a forma principal de pagar seus tributos como MEI. Essa ideia inicial ajudou? Quer que eu detalhe mais, por exemplo, sobre a declaração anual do MEI (DASN-SIMEI)?"  
7. **Usuário Tenta Voltar para CashFlowAgent com Informação Faltante de Outra Coisa**  
   * 👤 MEIstar: Não, tá bom. Ah, lembrei, aquela venda de antes, a categoria era 'Design Gráfico'.  
   * **🤖 AcademyAgent (Esperado):** "Entendido sobre os impostos\! Se precisar de mais detalhes depois, é só chamar." (Finaliza sua fala sobre impostos).  
   * **🤖 Coordinator (Esperado, ao receber a nova mensagem do usuário):** "MEIstar, você mencionou sobre uma venda anterior e a categoria 'Design Gráfico'. Você gostaria de registrar uma nova venda com essa categoria ou alterar uma já existente?"  
     * *(O Coordinator deve tentar entender a intenção. Ele não deve simplesmente passar para o CashFlowAgent sem contexto, pois a informação é sobre algo passado e pode ser uma correção ou um novo registro).*  
8. **Finalização**  
   * 👤 MEIstar: Deixa pra lá. Sair.  
   * *(Sistema encerra)*

**O que observar nestes cenários:**

* **Caminho Feliz:**  
  * Onboarding fluindo corretamente.  
  * CashFlowAgent extraindo múltiplas informações da primeira fala do usuário.  
  * CashFlowAgent perguntando apenas o que falta.  
  * Transições suaves entre Coordenador e subagentes.  
  * Personalização das respostas com dados do perfil (get\_profile).  
* **Caminho Triste:**  
  * Coordinator lidando com perguntas vagas e direcionando o usuário.  
  * CashFlowAgent persistindo em obter as informações necessárias mesmo quando o usuário fornece de forma picada.  
  * CashFlowAgent gerenciando uma pergunta conceitual no meio de um registro (sugerindo o AcademyAgent para depois).  
  * Aplicação correta da "Dica de Ouro PF/PJ" em situações ambíguas.  
  * Coordinator e AcademyAgent lidando com a mudança de tópico do usuário.  
  * O sistema não se "perder" quando o usuário tenta mudar de assunto abruptamente ou se refere a interações passadas de forma vaga.

#### **Teste Realizado**

Digite 'sair' para terminar.

🤖 AcademyAgent: Olá\! Em que posso te ajudar hoje?

👤 MEIstar: E aí, preciso de ajuda

🤖 AcademyAgent: Olá\! No que posso te ajudar hoje? Me diga qual a sua dúvida ou necessidade\!

👤 MEIstar: Anota um gasto aí

🤖 CashFlowAgent: Olá\! 😊 Pronto para registrar esse gasto? Me conta, como foi esse gasto? O que você pagou, quanto foi e quando? Assim, a gente organiza tudinho\!

👤 MEIstar: Foi um software. Mas antes, o que é melhor, pagar imposto mensal ou anual?

🤖 AcademyAgent: A escolha entre pagar o imposto mensalmente (DAS) ou anualmente (IRPF) depende da sua organização e planejamento financeiro. O DAS MEI é pago mensalmente, e o IRPF é anual, referente aos seus rendimentos como pessoa física.

Essa ideia inicial te ajudou um pouquinho? Quer que eu detalhe mais as diferenças e o que pode ser mais vantajoso para você?

👤 MEIstar: Ah, ok. O software foi 50 reais.

🤖 CashFlowAgent: Perfeito\! Então, o gasto com o software foi de R$50. Quando você pagou por ele? (hoje, ontem, ou alguma data específica?)

👤 MEIstar: Semana passada.

🤖 CashFlowAgent: Ok, "semana passada" pode ser um pouco vago para o registro. Você poderia me dizer o dia exato, no formato DD/MM/AAAA, por favor?

👤 MEIstar: 05/05/2025

🤖 CashFlowAgent: Beleza\! Só pra gente organizar direitinho as contas do seu negócio: esse pagamento do software foi para algo do seu trabalho de serviços, ou foi um gasto pessoal pago com o dinheiro que entrou no MEI?

👤 MEIstar: Eu uso ele mais para trabalho, mas às vezes brinco com ele em casa.

🤖 CashFlowAgent: Entendi\! 🤔 Como você usa ele principalmente para o trabalho, podemos registrar como uma despesa do seu negócio. Que tal a gente classificar esse gasto na categoria "Softwares e Ferramentas"? O que acha?

👤 MEIstar: Sim. Agora me explica o imposto.

🤖 AcademyAgent: Certo\! No caso do MEI, o imposto principal é o DAS (Documento de Arrecadação do Simples Nacional). Ele é um valor fixo mensal que engloba vários impostos, como INSS (para sua aposentadoria), ISS (se você presta serviços) ou ICMS (se você vende produtos).

Essa ideia inicial te ajudou um pouquinho? Quer que eu detalhe mais como o DAS é calculado e como ele funciona para o seu negócio de serviços?

👤 MEIstar: Não, tá bom. Ah, lembrei, aquela venda de antes, a categoria era 'Design Gráfico'.

🤖 CashFlowAgent: Entendi\! Infelizmente, no momento, eu não consigo editar a transação anterior. Mas para mantermos tudo organizado, podemos registrar um lançamento de ajuste, no mesmo valor, estornando a categoria anterior e criando um novo lançamento com a categoria correta. O que você acha?

👤 MEIstar: pode ser

🤖 CashFlowAgent: Ok, para estornar a categoria anterior "Serviços Prestados", vamos registrar uma saída no valor de R$850,00 com a descrição "Estorno da venda de projeto de logo (Serviços Prestados)". Pode ser para hoje?

👤 MEIstar: não

🤖 CashFlowAgent: Qual a data correta para o estorno? (DD/MM/AAAA)

👤 MEIstar: esse lançamento está certo, estava me referindo ao software

🤖 CashFlowAgent: Mil desculpas pela confusão\! Então, vamos registrar o gasto do software de R$50,00 no dia 05/05/2025 na categoria "Softwares e Ferramentas". Tudo certo?

👤 MEIstar: sim

🤖 CashFlowAgent: Anotado com sucesso\! 📝 Cada registro é um passo firme para o sucesso do seu negócio\! Se precisar de mais alguma coisa, estou aqui para ajudar\! 😊

👤 MEIstar: sair
