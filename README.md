# Assédio Zero - Plataforma de Denúncias

Este projeto é uma adaptação da plataforma "Alô Consumidor" para se tornar o **Assédio Zero**, um canal seguro e confidencial para o registro e gestão de denúncias de assédio moral, sexual, trabalhista, religioso, institucional, psicológico e virtual, abrangendo cidadãos civis e militares.

## Estrutura e Tecnologias

O projeto é construído com base nas seguintes tecnologias:

*   **Frontend:** React (Vite)
*   **Estilização:** Tailwind CSS
*   **Gerenciador de Pacotes:** pnpm

## Documentação

A documentação técnica e de usuário para este novo sistema pode ser encontrada nos arquivos:

*   `documentacao_tecnica_app_denuncias.md`
*   `manual_usuario_app_denuncias.md`

## Como Iniciar o Projeto

### Pré-requisitos

*   Node.js (versão 18+)
*   pnpm

### Instalação

Navegue até o diretório raiz do projeto e execute:

```bash
pnpm install
```

### Desenvolvimento

Para iniciar o servidor de desenvolvimento:

```bash
pnpm run dev
```

O aplicativo estará disponível em `http://localhost:5173/` (ou a porta indicada pelo Vite).

### Build para Produção

Para gerar os arquivos estáticos para produção:

```bash
pnpm run build
```

Os arquivos de produção serão gerados na pasta `dist/`.

## Próximos Passos (Integração com Backend)

Este repositório contém apenas o código do frontend. Para que as funcionalidades de denúncia e autenticação funcionem conforme a nova documentação técnica, é necessário integrar com o backend (API NestJS) e o banco de dados (PostgreSQL) conforme especificado em `documentacao_tecnica_app_denuncias.md`.

As rotas da API devem ser configuradas no arquivo de serviço (ex: `src/services/api.js` ou similar) para apontar para o endpoint correto do backend.

---
**Desenvolvido por:** [Seu Nome/Organização]
**Baseado em:** Projeto Alô Consumidor (GDF)
**Data da Adaptação:** Outubro/2025
