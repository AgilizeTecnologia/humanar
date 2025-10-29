# Documentação Técnica: Sistema de Denúncias de Assédio (Assédio Zero)

## 1. Introdução e Escopo do Projeto

O projeto **Assédio Zero** visa desenvolver uma plataforma segura e acessível para o registro e gestão de denúncias de diversos tipos de assédio: moral, sexual, trabalhista, religioso, institucional, psicológico e virtual (cyberstalking). O sistema deve atender tanto a cidadãos civis quanto a militares que sofrem assédio dentro da estrutura hierárquica de suas atribuições.

### 1.1. Premissas Chave

*   **Anonimato e Confidencialidade:** Garantia de que o denunciante possa reportar o assédio de forma anônima e que todos os dados sensíveis sejam tratados com a máxima confidencialidade.
*   **Segurança de Dados:** Uso de criptografia robusta (AES-256) para dados sensíveis e autenticação segura (JWT).
*   **Acessibilidade:** Interface responsiva e acessível para uso em diversos dispositivos.
*   **Imparcialidade e Agilidade:** Processo de registro e triagem de denúncias que garanta a imparcialidade na análise e a agilidade na resposta.
*   **Escalabilidade:** Arquitetura modular e em nuvem para suportar um volume crescente de denúncias.

### 1.2. Tipos de Assédio Suportados

| Tipo de Assédio | Descrição e Contexto | Público Alvo |
| :--- | :--- | :--- |
| **Moral** | Exposição a situações humilhantes e constrangedoras, repetitivas e prolongadas. | Civil e Militar |
| **Sexual** | Constrangimento com o objetivo de obter vantagem ou favor sexual. | Civil e Militar |
| **Trabalhista** | Ações que degradam as condições de trabalho e afetam a saúde física ou mental. | Civil |
| **Religioso** | Discriminação ou perseguição baseada em crença ou ausência de crença religiosa. | Civil e Militar |
| **Institucional** | Assédio praticado por agentes públicos no exercício de suas funções. | Civil e Militar |
| **Psicológico** | Ações que visam desestabilizar emocionalmente a vítima. | Civil e Militar |
| **Virtual (Cyberstalking)** | Uso da internet ou outras tecnologias digitais para perseguir e assediar. | Civil e Militar |

## 2. Arquitetura Geral do Sistema (Adaptada de Agilize)

O sistema seguirá uma arquitetura de microsserviços desacoplados, baseada na estrutura técnica de sucesso observada na documentação "Agilize", porém adaptada para o contexto de denúncias.

| Camada | Tecnologia Principal | Ambiente de Deploy | Propósito |
| :--- | :--- | :--- | :--- |
| **Frontend** | Next.js 14 (React) + TailwindCSS | Vercel | Interface do usuário (denunciante e administrador). |
| **Backend (API)** | NestJS (Node.js/TypeScript) | Render | Regras de negócio, autenticação e gestão de denúncias. |
| **Banco de Dados** | PostgreSQL + Prisma ORM | Render (Gerenciado) | Armazenamento seguro e relacional dos dados de denúncias. |

### 2.1. Diagrama de Fluxo de Denúncia (Alto Nível)

```mermaid
graph TD
    A[Denunciante (Civil/Militar)] -->|HTTPS| B(Frontend Next.js);
    B -->|API /denuncia/nova| C[Backend NestJS - Controller];
    C --> D{Service de Denúncias};
    D --> E[Prisma/PostgreSQL - Salva Denúncia];
    E --> F[Serviço de Notificação (E-mail/SMS)];
    F --> G[Administrador/Gestor de Denúncias];
    D --> H[Módulo de Análise e Triagem];
    H --> G;
```

## 3. Frontend (Next.js)

O frontend será a interface principal para o registro de denúncias e o painel de gestão.

### 3.1. Funcionalidades Chave

*   **Formulário de Denúncia:** Interface intuitiva e guiada para o registro de denúncias, com campos opcionais para garantir o anonimato.
*   **Painel do Denunciante (Opcional):** Acesso seguro (via token) para acompanhar o status da denúncia (se não for anônima).
*   **Painel de Administração:** Interface para triagem, classificação e gestão do ciclo de vida da denúncia.
*   **Tecnologias:** Next.js 14, React, TailwindCSS, shadcn/ui (para componentes acessíveis).

## 4. Backend (NestJS)

O backend é o coração do sistema, responsável pela segurança, regras de negócio e persistência de dados.

### 4.1. Módulos Principais

| Módulo | Responsabilidade |
| :--- | :--- |
| **Auth** | Login/Logout seguro (JWT), gerenciamento de usuários (administradores e denunciantes não anônimos). |
| **Denuncias** | Criação, leitura, atualização e exclusão de denúncias. Implementação de regras de validação e anonimização. |
| **Anexos** | Upload seguro de evidências (fotos, áudios, documentos), com criptografia e controle de acesso restrito. |
| **Triagem** | Funções para classificar, atribuir e alterar o status da denúncia (e.g., Recebida, Em Análise, Concluída). |
| **Militares** | Lógica específica para denúncias militares (e.g., hierarquia, canais de comunicação específicos). |
| **Notificacoes** | Envio de alertas por e-mail/SMS aos gestores e atualizações de status ao denunciante (se não anônimo). |

### 4.2. Estrutura de Dados (Schema Prisma - Adaptado)

O modelo de dados deve priorizar a segurança e a rastreabilidade.

```prisma
model Denuncia {
  id               String    @id @default(uuid())
  tipoAssedio      String    // Moral, Sexual, Trabalhista, etc.
  descricao        String    // Detalhes do ocorrido (criptografado)
  dataOcorrido     DateTime
  localOcorrido    String    // Localização ou contexto (criptografado)
  status           String    @default("Recebida") // Recebida, Em Análise, Concluída, Arquivada
  isAnonima        Boolean   @default(true)
  denuncianteId    String?   // Opcional, se não for anônima
  referenciaMilitar Boolean  @default(false) // Indica se envolve estrutura militar
  dataCriacao      DateTime  @default(now())
  dataAtualizacao  DateTime  @updatedAt
  
  // Relacionamentos
  denunciante      Usuario?  @relation(fields: [denuncianteId], references: [id])
  anexos           Anexo[]
  historico        HistoricoDenuncia[]
}

model Usuario {
  id               String    @id @default(uuid())
  nome             String    // (criptografado)
  email            String    @unique // (criptografado)
  senha            String    // Hash da senha
  perfil           String    @default("denunciante") // denunciante, administrador, gestor
  denuncias        Denuncia[]
}

model Anexo {
  id               String    @id @default(uuid())
  denunciaId       String
  caminhoArquivo   String    // Caminho para o arquivo (armazenado em S3 ou similar)
  tipoConteudo     String    // Imagem, Audio, Documento
  dataUpload       DateTime  @default(now())
  
  denuncia         Denuncia  @relation(fields: [denunciaId], references: [id])
}

model HistoricoDenuncia {
  id               String    @id @default(uuid())
  denunciaId       String
  dataMudanca      DateTime  @default(now())
  mudancaStatus    String    // Ex: "Recebida" -> "Em Análise"
  observacoes      String?   // Notas do gestor
  
  denuncia         Denuncia  @relation(fields: [denunciaId], references: [id])
}
```

## 5. Segurança e Conformidade

A segurança é o requisito mais crítico deste sistema.

### 5.1. Criptografia e Armazenamento

*   **Dados em Repouso:** A descrição da denúncia, nome do denunciante (se não anônimo) e local do ocorrido devem ser armazenados usando **criptografia AES-256** no banco de dados.
*   **Anexos:** Os arquivos de evidência devem ser armazenados em um serviço de armazenamento seguro (como AWS S3 ou similar) com criptografia e acesso restrito por tokens temporários.

### 5.2. Autenticação e Autorização

*   **JWT:** Uso de JSON Web Tokens (JWT) para autenticação de administradores e denunciantes registrados.
*   **Políticas de Acesso:** Implementação de políticas de autorização granular (RBAC - Role-Based Access Control) para garantir que apenas gestores autorizados possam acessar e triar denúncias.

## 6. CI/CD e Implantação

O processo de desenvolvimento e implantação deve ser automatizado para garantir a rapidez e a estabilidade.

*   **CI/CD:** GitHub Actions para testes automatizados e deploy contínuo.
*   **Deploy:** Frontend na Vercel, Backend e Banco de Dados no Render (ou provedores similares que suportem a stack).
*   **Monitoramento:** Implementação de logs estruturados (Winston) e monitoramento ativo com alertas para falhas de segurança ou indisponibilidade.

## 7. Próximos Passos (Desenvolvimento)

1.  Configuração do repositório e ambiente de desenvolvimento (Next.js, NestJS, Prisma).
2.  Implementação do módulo de Autenticação (Login/Registro).
3.  Desenvolvimento do Formulário de Denúncia (Frontend e API).
4.  Implementação da Criptografia de Dados Sensíveis no Backend.
5.  Desenvolvimento do Painel de Triagem e Gestão de Denúncias.
6.  Testes de Segurança e Carga.
