# Sessão 01 — Git e GitHub

**Data:** 20/09/2026

**Tema:** Fundamentos de Git, GitHub e versionamento.

## 1. Objetivo

Compreender o funcionamento fundamental do Git e do GitHub, criar um repositório de estudos e estabelecer um padrão de documentação técnica.

## 2. Conteúdo estudado

* Repositórios locais e remotos.
* Working directory e staging area.
* Commits e histórico de alterações.
* Branches.
* Pull Requests.
* Merge.

## 3. Laboratório realizado

Repositório: https://github.com/Thomas-silva96/platform-engineering-labs

Exercício: https://github.com/Thomas-silva96/skills-introduction-to-github

Commit inicial: `821a2f8`

## 4. Comandos utilizados

| Comando                          | Finalidade                                                    |
| -------------------------------- | ------------------------------------------------------------- |
| `git status`                     | Verificar o estado dos arquivos e da branch atual.            |
| `git switch -c <branch>`         | Criar uma branch e alternar para ela.                         |
| `git add <arquivo>`              | Adicionar alterações à staging area.                          |
| `git diff --cached`              | Inspecionar as alterações preparadas para o próximo commit.   |
| `git commit -m "mensagem"`       | Registrar as alterações preparadas no histórico local.        |
| `git push -u origin <branch>`    | Publicar a branch e configurar seu vínculo com o remoto.      |
| `git switch main`                | Alternar para a branch principal.                             |
| `git pull --ff-only origin main` | Atualizar a branch local sem criar um merge commit adicional. |
| `git log --oneline`              | Consultar o histórico resumido de commits.                    |

Os comandos utilizados neste laboratório permitiram acompanhar o fluxo completo de uma alteração, desde sua criação local até a integração no repositório remoto.

## 5. Aprendizados

### Diferença entre Git e GitHub

Git é um sistema de controle de versão distribuído que permite registrar alterações, manter históricos e trabalhar com diferentes branches.

GitHub é uma plataforma de hospedagem de repositórios Git que oferece funcionalidades adicionais de colaboração, como Pull Requests, revisões de código e automações.

### O que acontece durante um commit?

Um commit registra no repositório local um novo estado das alterações previamente preparadas na staging area.

Ele não envia automaticamente as alterações ao GitHub. Para publicar os commits no repositório remoto, utilizamos `git push`.

Também não é obrigatório abrir um Pull Request após cada commit. O PR faz parte de um fluxo de colaboração e integração, não do funcionamento obrigatório do Git.

### Por que utilizar branches e Pull Requests?

Branches permitem desenvolver alterações em linhas de histórico independentes, sem modificar diretamente a branch principal.

Pull Requests permitem propor a integração dessas alterações, examinar as diferenças, discutir decisões e realizar revisões antes do merge.

Esse processo reduz riscos e melhora a rastreabilidade, mas não garante sozinho a qualidade ou a segurança do código. Para isso, também são necessários testes, revisões adequadas e outras práticas de engenharia.

## 6. Erros e troubleshooting

Não ocorreram erros durante a execução do laboratório.

Entretanto, foram identificados riscos operacionais importantes:

* Realizar alterações na branch incorreta.
* Incluir arquivos indesejados ou informações sensíveis em um commit.
* Executar um merge sem revisar as alterações.
* Trabalhar com uma branch local desatualizada.

Como medidas preventivas, utilizaremos `git status` para verificar o estado do repositório, `git diff --cached` para revisar alterações preparadas e Pull Requests para inspecionar mudanças antes de integrá-las.

O laboratório também demonstrou a importância de sincronizar a branch local após um merge realizado no GitHub.

## 7. Decisão técnica

Para os próximos laboratórios, adotaremos um fluxo de desenvolvimento baseado em branches e Pull Requests.

Cada alteração ou conjunto pequeno de alterações relacionadas poderá utilizar uma branch própria, com nome descritivo.

Os commits deverão representar mudanças lógicas e possuir mensagens claras.

Antes de integrar uma alteração à `main`, verificaremos seu conteúdo, os resultados dos testes aplicáveis e a documentação necessária.

Após o merge, atualizaremos a branch principal local e removeremos branches temporárias que não forem mais necessárias.

Esse fluxo será utilizado para praticar versionamento, revisão de código e, futuramente, integração contínua e GitOps.


## 8. Próxima etapa

Praticar revisão de Pull Requests, resolução de conflitos e fundamentos de Linux.
