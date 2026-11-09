# Plume Notes

Aplicação de gerenciamento de notas pessoais desenvolvida com Angular 20 e TypeScript. A interface está em português do Brasil e oferece autenticação demonstrativa, organização de notas, busca, tags, arquivamento, anexos com recorte de imagens e tema claro/escuro.

> **Importante:** este projeto funciona inteiramente no navegador. Não possui backend, sincronização entre dispositivos ou autenticação adequada para produção. Os dados ficam no armazenamento local do navegador e podem ser alterados por alguém com acesso ao dispositivo e às ferramentas de desenvolvimento.

## Funcionalidades

- Cadastro, login e encerramento de sessão.
- Criação, edição, arquivamento, restauração e exclusão de notas.
- Busca textual e filtros por tags.
- Separação das notas por conta local.
- Anexos de imagem com visualização e recorte.
- Importação de imagens do dispositivo ou por URL, respeitando as restrições de CORS.
- Persistência de notas e preferências no `localStorage`; imagens no IndexedDB.
- Interface responsiva para desktop, tablet e celular.
- Tema claro e escuro compartilhado entre as telas.

## Tecnologias

- Angular 20
- TypeScript 5.9
- RxJS
- Angular Router e Reactive Forms
- Font Awesome
- ngx-image-cropper
- Web Crypto API (PBKDF2-SHA256)
- localStorage e IndexedDB
- Jasmine e Karma (configuração de testes do Angular)

## Requisitos

- Node.js 20 ou superior
- npm compatível com a versão do Node.js
- Navegador moderno

A Web Crypto API exige contexto seguro: execute em `localhost` ou por HTTPS.

## Executar localmente

```bash
git clone https://github.com/EDLS08/Projeto-JavaScript.git
cd Projeto-JavaScript
npm ci
npm start
```

A aplicação ficará disponível em http://localhost:4200.

## Scripts

| Comando | Descrição |
|---|---|
| `npm start` | Inicia o servidor de desenvolvimento |
| `npm run build` | Gera a versão de produção em `dist/` |
| `npm run watch` | Compila continuamente em modo de desenvolvimento |
| `npm test` | Executa os testes configurados pelo Angular/Karma |

## Estrutura do projeto

```text
src/
├── app/
│   ├── guards/          Proteção de rotas
│   ├── models/          Interfaces e tipos
│   ├── services/        Autenticação, notas, imagens, tema e armazenamento
│   ├── shared/          Componentes e utilitários compartilhados
│   ├── testing/         Apoio aos testes
│   └── user-module/     Login, cadastro e painel de notas
├── index.html
├── main.ts
└── styles.css
public/                  Ícones e recursos estáticos
docs/                    Relatório técnico e roteiro de apresentação
.github/workflows/       Automação de integração contínua
```

## Armazenamento e privacidade

| Dados | Armazenamento |
|---|---|
| Contas locais e hashes de senha | localStorage |
| Identificador da sessão | localStorage |
| Notas | localStorage |
| Preferência de tema | localStorage |
| Imagens originais e recortadas | IndexedDB |

As senhas não são armazenadas em texto puro: o projeto deriva hashes usando PBKDF2-SHA256 com salt. Isso **não transforma a autenticação local em segurança de produção**. Sem um servidor confiável, o usuário pode modificar os dados no próprio navegador. Não utilize senhas reais ou informações sensíveis neste projeto.

Para apagar os dados locais, use as ferramentas do navegador: **Application → Storage → Clear site data**.

## Imagens e CORS

O aplicativo valida o conteúdo real dos arquivos de imagem e limita o tamanho aceito. Imagens hospedadas em servidores que não autorizam CORS podem não ser importadas diretamente por URL; nesse caso, salve o arquivo e selecione-o no dispositivo.

## Testes e validação

O repositório contém testes unitários para serviços, componentes, utilitários e guards. O relatório em [docs/RELATORIO.md](docs/RELATORIO.md) registra as verificações realizadas no projeto e também as limitações conhecidas. Testes em dispositivos físicos e em todos os navegadores não devem ser considerados concluídos sem execução específica nesses ambientes.

## Documentação

- [Relatório técnico e decisões de implementação](docs/RELATORIO.md)
- [Instruções do projeto para GitHub Copilot](.github/copilot-instructions.md)

## Deploy

O arquivo `vercel.json` contém o rewrite necessário para o roteamento da aplicação Angular em hospedagens Vercel. Configure o comando de build como `npm run build` e o diretório de saída conforme o artefato gerado pela versão instalada do Angular CLI.

## Licença

Nenhuma licença foi declarada neste repositório. Até que uma licença seja adicionada, não presuma permissão para reutilizar, modificar ou redistribuir o código.
