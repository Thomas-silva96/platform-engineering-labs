# Linux — Fundamentos e Laboratórios

## 1. Objetivo

Desenvolver conhecimentos fundamentais de Linux para aplicação em Cloud Computing, DevOps, SRE e Platform Engineering.

O primeiro laboratório tem como objetivo compreender a estrutura de diretórios, navegar pelo filesystem e manipular arquivos utilizando o terminal.

## 2. Formação

**Curso:** Linux Foundation — Introduction to Linux (LFS101)

**Plataforma:** Linux Foundation

**Início:** 21/09/2026

**Status:** Em andamento

**Progresso:** Linux Philosophy and Concepts

**Link:** https://training.linuxfoundation.org/training/introduction-to-linux/

## 3. Ambiente do laboratório

* Sistema operacional: Ubunto 26.04.1
* Ambiente: WSL2
* Terminal: PowerShell
* Diretório de trabalho: `~/platform-labs/session-02`

## 4. Comandos estudados

| Comando | Finalidade                                                         |
| ------- | ------------------------------------------------------------------ |
| `pwd`   | Exibir o diretório de trabalho atual.                              |
| `ls`    | Listar arquivos e diretórios.                                      |
| `cd`    | Alterar o diretório de trabalho.                                   |
| `mkdir` | Criar diretórios.                                                  |
| `touch` | Criar um arquivo vazio ou atualizar seus timestamps.               |
| `cat`   | Exibir ou concatenar o conteúdo de arquivos.                       |
| `less`  | Visualizar arquivos de forma paginada.                             |
| `cp`    | Copiar arquivos ou diretórios.                                     |
| `mv`    | Mover ou renomear arquivos e diretórios.                           |
| `rm`    | Remover arquivos ou diretórios, conforme os parâmetros utilizados. |

## 5. Laboratório prático

O laboratório foi realizado em um diretório isolado para evitar alterações em arquivos pessoais ou de sistema.

As operações estudadas envolveram:

1. Criação de um diretório de trabalho.
2. Navegação entre diretórios.
3. Criação de arquivos.
4. Escrita e leitura de conteúdo.
5. Cópia e renomeação.
6. Listagem e inspeção.
7. Remoção controlada de um arquivo de teste.

### Validação

Todo o fluxo de criação e modificação direto pelo terminal executando os comandos foi possivel validar e ideintificar o sucesso através do comando ls, onde listamos os arquivos e conforme o comando de criação, alteração ou remoção e possivel validar os resuultados.

## 6. Aprendizados

Descrever com suas próprias palavras:

* O que é o diretório de trabalho? É a pasta ou local onde se encontra para realização dos processos.
* Qual é a diferença entre caminhos absolutos e relativos? O caminho absoluto aponta a localização a partir da raiz do sistema, e o relativo depende do diretorio onde está. 
* Qual é a diferença entre `cp` e `mv`? O cp copiamos arquivos ouu diretórios, enquanto o mv usamos para mover ou renomear arquivos ou diretórios.
* Por que precisamos ter cuidado com o comando `rm`? Pois esse comando e utilizado para remoção de arquivos ou diretorios
* Como esses conhecimentos serão úteis na administração de servidores Linux? Eles serão uteis pois é a base de navegação e organização de arquivos no sistema.

## 7. Erros e troubleshooting

Registrar erros reais encontrados durante o laboratório.

Para cada erro, documentar:

**Sintoma:** o que aconteceu.

**Diagnóstico:** como foi identificada a causa.

**Correção:** qual ação resolveu o problema.

**Validação:** como foi confirmado que a correção funcionou.

Caso nenhum erro tenha ocorrido, registrar que não houve falhas observadas e descrever um risco operacional identificado.

Não teve falhas.

## 8. Decisão técnica

Utilizar um ambiente Linux isolado para os laboratórios, mantendo os projetos comerciais separados das atividades de estudo.

Executar operações potencialmente destrutivas somente em diretórios de teste e evitar o uso desnecessário de privilégios administrativos.

## 9. Evidências

* GitHub Skills — Review Pull Requests: https://github.com/Thomas-silva96/skills-review-pull-requests
* GitHub Skills — Resolve Merge Conflicts: https://github.com/Thomas-silva96/skills-resolve-merge-conflicts
* Laboratório Linux: thomaSilva96@thomas-silva96:~$ mkdir -p ~/platform-labs/session-02

cd ~/platform-labs/session-02

pwd
/home/thomaSilva96/platform-labs/session-02
thomaSilva96@thomas-silva96:~/platform-labs/session-02$ mkdir arquivos
thomaSilva96@thomas-silva96:~/platform-labs/session-02$ cd arquivos
thomaSilva96@thomas-silva96:~/platform-labs/session-02/arquivos$ touch exemplo.txt
thomaSilva96@thomas-silva96:~/platform-labs/session-02/arquivos$ printf 'Meu primeiro laboratorio Linux\n' > exemplo.txt
thomaSilva96@thomas-silva96:~/platform-labs/session-02/arquivos$ cat exemplo.txt
Meu primeiro laboratorio Linux
thomaSilva96@thomas-silva96:~/platform-labs/session-02/arquivos$ cp exemplo.txt copia.txt
thomaSilva96@thomas-silva96:~/platform-labs/session-02/arquivos$ mv copia.txt resultado.txt
thomaSilva96@thomas-silva96:~/platform-labs/session-02/arquivos$ ls -la
total 16
drwxr-xr-x 2 thomaSilva96 thomaSilva96 4096 Sep 21 12:37 .
drwxr-xr-x 3 thomaSilva96 thomaSilva96 4096 Sep 21 12:35 ..
-rw-r--r-- 1 thomaSilva96 thomaSilva96   31 Sep 21 12:36 exemplo.txt
-rw-r--r-- 1 thomaSilva96 thomaSilva96   31 Sep 21 12:37 resultado.txt
thomaSilva96@thomas-silva96:~/platform-labs/session-02/arquivos$ less resultado.txt
thomaSilva96@thomas-silva96:~/platform-labs/session-02/arquivos$ cd ..
thomaSilva96@thomas-silva96:~/platform-labs/session-02$ pwd
/home/thomaSilva96/platform-labs/session-02
thomaSilva96@thomas-silva96:~/platform-labs/session-02$ ls -la arquivos
total 16
drwxr-xr-x 2 thomaSilva96 thomaSilva96 4096 Sep 21 12:37 .
drwxr-xr-x 3 thomaSilva96 thomaSilva96 4096 Sep 21 12:35 ..
-rw-r--r-- 1 thomaSilva96 thomaSilva96   31 Sep 21 12:36 exemplo.txt
-rw-r--r-- 1 thomaSilva96 thomaSilva96   31 Sep 21 12:37 resultado.txt
thomaSilva96@thomas-silva96:~/platform-labs/session-02$ rm arquivos/resultado.txt
thomaSilva96@thomas-silva96:~/platform-labs/session-02$ ls -la arquivos
total 12
drwxr-xr-x 2 thomaSilva96 thomaSilva96 4096 Sep 21 12:41 .
drwxr-xr-x 3 thomaSilva96 thomaSilva96 4096 Sep 21 12:35 ..
-rw-r--r-- 1 thomaSilva96 thomaSilva96   31 Sep 21 12:36 exemplo.txt
thomaSilva96@thomas-silva96:~/platform-labs/session-02$

## 10. Próxima etapa

Aprofundar Linux com foco em processos, serviços, permissões, conectividade, logs e troubleshooting.
