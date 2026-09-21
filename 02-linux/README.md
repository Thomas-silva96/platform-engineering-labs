# Linux — Fundamentos e Laboratórios

## 1. Objetivo

Desenvolver conhecimentos fundamentais de Linux para aplicação em Cloud Computing, DevOps, SRE e Platform Engineering. Neste primeiro laboratório, praticar navegação pelo filesystem e manipulação de arquivos no terminal.

## 2. Formação

- **Curso:** Linux Foundation — Introduction to Linux (LFS101)
- **Início:** 21/09/2026
- **Status:** Em andamento, sem conclusão integral ou badge registrado.
- **Progresso informado:** Linux Philosophy and Concepts.
- **Curso:** https://training.linuxfoundation.org/training/introduction-to-linux/

## 3. Ambiente do laboratório

- **Sistema operacional:** Ubuntu em WSL2. Versão exata a confirmar com `cat /etc/os-release` (anotação inicial: "Ubunto 26.04.1").
- **Terminal:** Windows Terminal/PowerShell como aplicativo de acesso; comandos do laboratório executados no shell Linux dentro do WSL2.
- **Diretório de trabalho:** `~/platform-labs/session-02`, correspondente a `/home/thomaSilva96/platform-labs/session-02` na execução registrada.

## 4. Comandos estudados e executados

| Comando | Finalidade |
| --- | --- |
| `pwd` | Exibir o caminho absoluto do diretório de trabalho atual. |
| `ls -la` | Listar entradas, incluindo ocultas, em formato detalhado. |
| `cd` | Alterar o diretório de trabalho. |
| `mkdir` / `mkdir -p` | Criar diretórios; `-p` também cria pais ausentes e não falha se o diretório já existir. |
| `touch` | Criar arquivo vazio ou atualizar timestamps de um arquivo existente. |
| `printf ... > arquivo` | Gravar texto no arquivo; `>` substitui seu conteúdo existente. |
| `cat` | Exibir ou concatenar conteúdo de arquivos. |
| `less` | Ler conteúdo de forma paginada (pressionar `q` para sair). |
| `cp` | Copiar arquivos; para diretórios, utilizar opção apropriada como `-r` quando necessário. |
| `mv` | Mover ou renomear arquivos e diretórios. |
| `rm` | Remover arquivos; diretórios exigem opções apropriadas e cuidados adicionais. |

## 5. Laboratório prático

O laboratório foi executado em um diretório isolado, sem alterar arquivos de projetos comerciais ou arquivos de sistema. Foram criados `arquivos/exemplo.txt` e uma cópia, renomeada para `arquivos/resultado.txt`. Ao final, `resultado.txt` foi removido, enquanto `exemplo.txt` permaneceu.

### Sequência reproduzível

```bash
mkdir -p ~/platform-labs/session-02
cd ~/platform-labs/session-02
pwd
mkdir arquivos
cd arquivos
touch exemplo.txt
printf 'Meu primeiro laboratorio Linux\n' > exemplo.txt
cat exemplo.txt
cp exemplo.txt copia.txt
mv copia.txt resultado.txt
ls -la
less resultado.txt  # sair com q
cd ..
pwd
ls -la arquivos
rm arquivos/resultado.txt
ls -la arquivos
```

**Validação observada:** `cat exemplo.txt` exibiu `Meu primeiro laboratorio Linux`; a primeira listagem de `arquivos` exibiu `exemplo.txt` e `resultado.txt`, ambos com 31 bytes; depois de `rm`, a listagem exibiu apenas `exemplo.txt`. `pwd` confirmou o diretório de trabalho. Isso demonstra o fluxo de criação, cópia, renomeação, leitura e remoção neste laboratório específico — não valida o sistema Linux inteiro.

## 6. Aprendizados

- **Diretório de trabalho:** é o diretório em que o processo do shell está operando; `pwd` mostra seu caminho.
- **Caminhos absolutos e relativos:** o absoluto começa na raiz `/`; o relativo é interpretado a partir do diretório de trabalho atual. `..` referencia o diretório pai, e `~` é expandido pelo shell para o diretório pessoal.
- **`cp` e `mv`:** `cp` cria uma cópia, preservando a origem; `mv` desloca ou renomeia a entrada original. Em ambos os casos, o destino deve ser conferido para evitar substituição indesejada.
- **Risco de `rm`:** pode remover dados importantes e normalmente não os envia para a lixeira. Confirmar o diretório atual e o caminho antes de executar; evitar `sudo` e remoção recursiva em exercícios introdutórios.
- **Aplicação em servidores:** esses fundamentos ajudam a localizar configurações e logs, conferir arquivos de aplicações e trabalhar com segurança em ambientes Linux. Diagnóstico de processos, serviços e rede ficará para os próximos laboratórios.

## 7. Erros e troubleshooting

Não foram observadas falhas durante os comandos executados. Portanto, não há incidente real nem correção a atribuir a esta sessão.

**Risco operacional identificado:** `rm` ou redirecionamento com `>` no caminho errado pode remover ou substituir conteúdo. Antes de executar, conferir `pwd`, listar o diretório com `ls -la` e validar o caminho desejado. Esse risco foi discutido, mas não foi provocado como falha no laboratório.

## 8. Decisão técnica

Utilizar o Ubuntu no WSL2 e diretórios isolados para estudo, mantendo os projetos comerciais separados. Evitar privilégios administrativos desnecessários e executar operações destrutivas apenas sobre arquivos descartáveis do laboratório.

## 9. Evidências

- [GitHub Skills — Review Pull Requests](https://github.com/Thomas-silva96/skills-review-pull-requests) — exercício concluído.
- [GitHub Skills — Resolve Merge Conflicts](https://github.com/Thomas-silva96/skills-resolve-merge-conflicts) — exercício concluído.
- Captura de terminal enviada na conversa de mentoria de 21/09/2026 e comandos/saídas essenciais reproduzidos na seção 5. O laboratório local não foi executado por CI.
- [PR #3 — publicação inicial deste README](https://github.com/Thomas-silva96/platform-engineering-labs/pull/3).

## 10. Próxima etapa

Praticar usuários, grupos, permissões e ownership em ambiente isolado. Depois, avançar para processos, serviços, conectividade, logs e troubleshooting, mantendo a conclusão integral do LFS101 como objetivo de longo prazo.
