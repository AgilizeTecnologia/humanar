# Manual do Usuário: Sistema de Denúncias de Assédio (Assédio Zero)

## 1. Introdução: O que é o Assédio Zero?

O **Assédio Zero** é uma plataforma digital desenvolvida para ser um canal seguro, confidencial e acessível para o registro de denúncias de assédio. Nosso objetivo é garantir que vítimas, sejam elas civis ou militares, tenham um meio eficaz para reportar abusos e que as denúncias sejam tratadas com a seriedade, imparcialidade e agilidade necessárias.

### 1.1. Tipos de Assédio que Você Pode Denunciar

O sistema foi desenhado para receber denúncias sobre os seguintes tipos de assédio:

*   Assédio **Moral**
*   Assédio **Sexual**
*   Assédio **Trabalhista**
*   Assédio **Religioso**
*   Assédio **Institucional**
*   Assédio **Psicológico**
*   Assédio **Virtual (Cyberstalking)**

## 2. Guia Rápido para o Denunciante

### 2.1. A Importância do Anonimato

Você tem o direito de fazer sua denúncia de forma **completamente anônima**. O sistema garante que, ao escolher esta opção, nenhuma informação de identificação pessoal será registrada ou rastreada.

**Recomendação:** Se você optar pelo anonimato, certifique-se de fornecer o máximo de detalhes possível sobre o ocorrido, pois não haverá a possibilidade de contato posterior para esclarecimentos.

### 2.2. Passo a Passo para Registrar uma Denúncia

1.  **Acesso à Plataforma:** Acesse o endereço do aplicativo Assédio Zero.
2.  **Escolha o Modo:** Selecione a opção "Registrar Nova Denúncia".
3.  **Anonimato:** O sistema perguntará se você deseja prosseguir de forma anônima.
    *   **Sim (Anônimo):** Você será direcionado diretamente para o formulário.
    *   **Não (Identificado):** Você precisará criar uma conta ou fazer login para que a equipe de gestão possa entrar em contato, se necessário.
4.  **Preenchimento do Formulário:** Preencha os campos com o máximo de detalhes:
    *   **Tipo de Assédio:** Selecione o tipo (ex: Sexual, Moral, Institucional).
    *   **Data e Local do Ocorrido:** Seja o mais preciso possível.
    *   **Descrição:** Relate o que aconteceu de forma clara e objetiva. **Lembre-se: seus dados sensíveis serão criptografados.**
5.  **Evidências (Anexos):** Se você tiver fotos, áudios, e-mails ou documentos que comprovem o assédio, utilize a função de upload seguro.
6.  **Confirmação:** Revise todas as informações e clique em "Enviar Denúncia".

### 2.3. Acompanhamento da Denúncia (Para Denúncias Não Anônimas)

Após o envio, você receberá um **código de protocolo**. Se você optou por se identificar, poderá usar este código e seu login para:

*   Consultar o **Status** da denúncia (Recebida, Em Análise, Concluída).
*   Receber **Notificações** por e-mail ou SMS sobre o andamento.
*   Adicionar **Novas Informações** ou anexos, se necessário.

## 3. Guia para o Gestor de Denúncias (Administrador)

Este guia é destinado aos profissionais responsáveis pela triagem, análise e gestão das denúncias.

### 3.1. Acesso e Segurança

*   **Login:** Acesse o Painel de Administração utilizando suas credenciais de gestor. O acesso é protegido por **JWT (JSON Web Token)**.
*   **Confidencialidade:** O acesso aos dados criptografados é restrito. Você só deve acessar a descrição completa da denúncia quando for estritamente necessário para a análise.

### 3.2. Fluxo de Triagem e Gestão

O ciclo de vida de uma denúncia segue os seguintes status:

| Status | Descrição | Ação do Gestor |
| :--- | :--- | :--- |
| **Recebida** | Denúncia recém-enviada, aguardando triagem inicial. | Classificar o tipo de assédio e a urgência. |
| **Em Análise** | A denúncia foi atribuída a um gestor e está sendo investigada. | Coletar informações adicionais, se possível. |
| **Em Diligência** | Fase de investigação ativa (entrevistas, coleta de provas). | Registrar todas as ações no **Histórico da Denúncia**. |
| **Concluída** | A investigação foi finalizada e as medidas cabíveis foram tomadas. | Registrar a conclusão e as medidas no sistema. |
| **Arquivada** | Denúncia sem elementos suficientes para prosseguir ou fora do escopo. | Justificar o arquivamento. |

### 3.3. Funcionalidades Chave do Painel

1.  **Dashboard:** Visão geral das denúncias por status, tipo de assédio e público (Civil/Militar).
2.  **Filtros Avançados:** Filtragem por data, tipo de assédio e status.
3.  **Registro de Histórico:** Toda mudança de status, observação ou ação deve ser registrada no módulo **HistoricoDenuncia** para garantir a rastreabilidade e a transparência do processo.
4.  **Módulo Militar:** Utilizar este módulo para denúncias que envolvam a estrutura hierárquica militar, garantindo que os protocolos específicos (se houver) sejam seguidos.

## 4. Melhores Práticas de Tratamento de Denúncias

Adaptando os princípios de resolução de conflitos para o contexto de assédio:

*   **Imparcialidade:** Trate todas as denúncias como verdadeiras até que a investigação prove o contrário, evitando julgamentos prévios.
*   **Agilidade:** Inicie a triagem e a análise o mais rápido possível. O tempo é crucial em casos de assédio.
*   **Confidencialidade:** Mantenha o sigilo absoluto sobre a identidade do denunciante e do denunciado durante a fase de investigação.
*   **Documentação:** Mantenha um registro completo e detalhado de cada passo tomado, utilizando o **HistoricoDenuncia** como ferramenta central.

## 5. Suporte Técnico

Em caso de problemas técnicos com a plataforma (erros, falhas de acesso, problemas de upload), entre em contato com a equipe de TI responsável.

*   **E-mail de Suporte:** [A ser definido]
*   **Telefone de Suporte:** [A ser definido]
