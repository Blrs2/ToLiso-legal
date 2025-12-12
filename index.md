# POLÍTICA DE PRIVACIDADE E TERMOS DE USO

**Última atualização:** 11 de dezembro de 2025

Esta Política de Privacidade descreve como o aplicativo (doravante "Aplicativo") coleta, usa e protege os dados do usuário. Ao instalar e utilizar o Aplicativo, você concorda com os termos aqui descritos.

## 1. Coleta e Uso de Dados

A nossa coleta de dados é minimizada e restrita às funcionalidades essenciais encontradas no código do aplicativo:

### 1.1. Dados de Autenticação
Para permitir o acesso, sincronização e segurança da sua conta, utilizamos o **Google Firebase Authentication**. Coletamos:
* Endereço de e-mail e senha (para login via e-mail).
* Credenciais de autenticação Google (para login via Google Sign-In).
* Identificadores únicos de usuário (UID).

### 1.2. Leitura de Notificações (Automação Financeira)
O Aplicativo solicita a permissão `BIND_NOTIFICATION_LISTENER_SERVICE`. Conforme implementado em nosso serviço (`NotificationService.kt`), esta permissão é utilizada estritamente para:
* Identificar notificações provenientes de aplicativos financeiros e bancários pré-selecionados pelo usuário.
* Ler o **Título** e o **Texto** da notificação para extrair automaticamente informações sobre gastos e transações.
* **Privacidade:** O processamento inicial ocorre localmente no seu dispositivo. Os dados extraídos são convertidos em lançamentos financeiros no banco de dados local (`Room Database`).

### 1.3. Dados Financeiros Locais
Seus registros de ganhos, gastos e categorias são armazenados localmente no dispositivo utilizando a tecnologia **Android Room Database**.

#### **1.4. Uso de Microfone e Áudio (Interação com IA)**
[cite_start]O aplicativo solicita a permissão `RECORD_AUDIO` [cite: 4] exclusivamente para permitir que você interaja com o "Tutor Financeiro" através de comandos de voz.
* [cite_start]**Processamento:** O áudio capturado é convertido em texto ou enviado para processamento pela API do **Google Gemini (Firebase AI)** [cite: 2] para interpretar sua dúvida financeira.
* **Armazenamento:** O aplicativo **não** armazena gravações de voz permanentemente. O áudio é processado de forma efêmera apenas para a execução do comando imediato no chat.


## 2. Uso de Inteligência Artificial (Isenção de Responsabilidade)

O aplicativo utiliza a API **Google Firebase AI (Gemini 2.0 Flash Lite)** através do componente `AnalisarGastosAgent` para fornecer insights sobre seus gastos.

**AVISO IMPORTANTE DE ISENÇÃO DE RESPONSABILIDADE (DISCLAIMER):**
**O recurso de "Tutor Financeiro" deste aplicativo utiliza Inteligência Artificial Generativa para analisar dados agregados e fornecer dicas. Embora o sistema seja projetado para ser útil, a Inteligência Artificial pode cometer erros, gerar informações imprecisas ("alucinações") ou interpretar dados de forma equivocada. As orientações fornecidas pelo Aplicativo NÃO constituem aconselhamento financeiro, contábil ou jurídico profissional. O usuário deve sempre verificar os cálculos e tomar decisões financeiras baseadas em seu próprio julgamento ou na consulta de um profissional humano qualificado. O desenvolvedor não se responsabiliza por prejuízos decorrentes de decisões tomadas com base nas sugestões da IA.**

## 3. Compartilhamento e Serviços de Terceiros

Não vendemos seus dados. Compartilhamos informações estritamente com os provedores de infraestrutura listados abaixo, necessários para o funcionamento do app (conforme consta em nosso `build.gradle`):

* **Google Firebase Auth:** Gerenciamento de identidade e login.
* **Google Firebase Analytics:** Coleta de métricas de uso anônimas para melhoria do app.
* **Google Firebase AI (Vertex AI/Gemini):** Processamento de texto para o Tutor Financeiro.
* **Google Firebase App Check (via Play Integrity):** Para proteger o aplicativo contra fraudes, abusos e acessos não autorizados.
* **Google Play Billing:** Processamento de pagamentos e compras no app.

## 4. Exclusão de Dados e Direitos do Usuário

[cite_start]Respeitamos a sua autonomia sobre os dados, que são armazenados primariamente no seu dispositivo ("Local First") utilizando o banco de dados **AppDatabase (Room)**[cite: 1].

* **Exclusão Parcial (Sem excluir a conta):** Como os dados financeiros residem no seu dispositivo, você possui total liberdade para excluir transações individuais, categorias ou limpar o armazenamento do app através das configurações do Android a qualquer momento, sem a necessidade de excluir sua conta de login.
Em conformidade com a LGPD e GDPR, você tem total controle sobre seus dados. O aplicativo possui uma funcionalidade nativa de **Exclusão de Conta** (`AuthViewModel.deleteAccount`), acessível nas configurações, que executa as seguintes ações irreversiveis:
1.  Exclusão da sua conta de usuário nos servidores do Firebase Auth.
2.  Limpeza completa do banco de dados local (`AppDatabase.clearAllTables()`).
3.  Remoção de todas as preferências salvas no dispositivo (`SharedPreferences`).* **Solicitação via Web (Caso tenha perdido o dispositivo):** Caso você não tenha mais acesso ao aplicativo, poderá solicitar a exclusão da sua conta e dados associados (e-mail e UID) através do nosso canal de suporte descrito abaixo.
Caso ocorra uma falha técnica durante a exclusão automática (ex: necessidade de re-login recente), o aplicativo o notificará para realizar o login novamente e concluir o processo.

---

# POLÍTICA DE REEMBOLSO E BENS DIGITAIS

Esta política aplica-se a todas as compras realizadas dentro do aplicativo, processadas através do sistema **Google Play Billing Library**.

## 1. Natureza dos Bens Digitais
O aplicativo comercializa **"Moedas" (Coins)** (referenciadas internamente como `coins_100`, `coins_500`, `coins_1000`).
De acordo com a nossa arquitetura técnica (`BillingManager.kt`), estes itens são classificados como **Bens Digitais Consumíveis**. Isso significa que, uma vez adquiridos e creditados na sua conta, eles são "consumidos" para uso imediato (como troca por tokens de IA) e não podem ser reutilizados.

## 2. Política de Reembolso
Devido à natureza consumível e imediata das Moedas Virtuais:
* **Todas as vendas são finais.** Não oferecemos reembolsos para Moedas que já foram creditadas na sua carteira e/ou consumidas pelo uso da Inteligência Artificial.
* **Direito de Arrependimento:** O direito de arrependimento poderá ser exercido apenas **antes** do consumo ou uso das moedas no aplicativo, e dentro do prazo estipulado pela legislação local (7 dias no Brasil), desde que o produto não tenha sido utilizado.

## 3. Exceções Técnicas
O reembolso será concedido **exclusivamente** nos seguintes casos:
1.  **Falha na Entrega:** O usuário foi cobrado pela Google Play Store, mas as moedas não foram adicionadas ao saldo do aplicativo devido a um erro de comunicação com o servidor ou falha no método `consumePurchase`.
2.  **Cobrança Duplicada:** Erro no processamento resultando em duas cobranças para a mesma transação.

## 4. Como Solicitar Reembolso
Para casos de falha técnica, o usuário deve entrar em contato conosco enviando:
1.  O comprovante de compra da Google Play (contendo o ID do Pedido começando com `GPA.`).
2.  O e-mail da conta cadastrada no app.

Envie sua solicitação para: **tolisosuporte@gmail.com**
