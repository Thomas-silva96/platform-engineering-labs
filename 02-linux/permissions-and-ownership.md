# Linux — Users, Groups, Permissions and Ownership

**Data:** 21/09/2026  
**Sessão:** 02 — Platform Engineering Labs  
**Ambiente:** Ubuntu em WSL2  
**Status:** Laboratório concluído

## 1. Objetivo

Compreender como o Linux utiliza usuários, grupos, ownership e permissões para controlar o acesso a arquivos e diretórios.

Aplicar esses conceitos em um laboratório isolado, reproduzindo e diagnosticando uma falha de permissão.

Os conhecimentos serão utilizados posteriormente na administração de servidores, containers, pipelines de CI/CD e ambientes Kubernetes.

## 2. Conceitos fundamentais

### Usuários e grupos

O Linux utiliza identificadores numéricos para representar usuários e grupos.

- UID (User ID): identificador numérico do usuário.
- GID (Group ID): identificador numérico do grupo.
- Owner: usuário proprietário de um arquivo ou diretório.
- Group: grupo associado ao arquivo ou diretório.
- Others: usuários que não são o proprietário nem pertencem ao grupo associado ao arquivo.

As permissões tradicionais são avaliadas conforme a identidade do processo que tenta acessar o recurso, considerando também outros mecanismos de segurança aplicáveis.

### Permissões

As três permissões básicas são:

| Permissão | Valor | Significado em arquivos |
|---|---:|---|
| Read (`r`) | 4 | Ler o conteúdo |
| Write (`w`) | 2 | Modificar o conteúdo |
| Execute (`x`) | 1 | Executar o arquivo |

Em diretórios, essas permissões possuem significados específicos relacionados à listagem, alteração de entradas e travessia.

### Representação octal

As permissões podem ser representadas numericamente.

Exemplo:

`644`

- Proprietário: `6` = leitura + escrita.
- Grupo: `4` = leitura.
- Outros: `4` = leitura.

Outro exemplo:

`600`

- Proprietário: leitura + escrita.
- Grupo: nenhuma permissão.
- Outros: nenhuma permissão.

Esses valores representam os bits tradicionais de permissão. O controle efetivo de acesso também pode envolver ACLs, privilégios administrativos e outros mecanismos.

## 3. Ambiente do laboratório

O laboratório foi executado no Ubuntu utilizando WSL2, dentro de um diretório isolado.

Diretório utilizado:

```bash
~/platform-labs/session-02/permissions
```

Não foram realizadas alterações em usuários reais, grupos do sistema ou arquivos comerciais.

Os comandos de administração executados neste laboratório não utilizaram `sudo`.

## 4. Identificação do usuário

### Comandos executados

```bash
whoami
id
groups
```

### Resultados observados

```text
thomaSilva96

uid=1000(thomaSilva96)
gid=1000(thomaSilva96)
groups=1000(thomaSilva96),4(adm),20(dialout),
24(cdrom),25(floppy),27(sudo),29(audio),
30(dip),44(video),46(plugdev),100(users),
105(netdev)
```

O comando `groups` também confirmou os grupos associados ao usuário.

### Aprendizado

O usuário do laboratório possui UID `1000` e grupo primário com GID `1000`.

Ele também pertence a grupos suplementares, incluindo `sudo`.

A associação ao grupo `sudo` não significa que todos os processos executados por esse usuário possuem automaticamente privilégios de root.

O uso efetivo de privilégios elevados depende dos mecanismos de autorização configurados no sistema.

## 5. Criação do laboratório

### Comandos executados

```bash
mkdir -p ~/platform-labs/session-02/permissions

cd ~/platform-labs/session-02/permissions

printf 'Laboratorio de permissoes\n' > arquivo.txt

ls -l arquivo.txt
```

### Resultado observado

```text
-rw-r--r-- 1 thomaSilva96 thomaSilva96 26 Sep 21 13:43 arquivo.txt
```

O arquivo foi criado com sucesso.

O usuário `thomaSilva96` aparece como proprietário e o grupo associado também possui o nome `thomaSilva96`.

As permissões iniciais observadas foram `644`.

Essas permissões resultaram das configurações do ambiente, incluindo a máscara de criação de arquivos (*umask*).

## 6. Inspeção das permissões

### Comando executado

```bash
stat -c '%a %A %U %G' arquivo.txt
```

### Resultado observado

```text
644 -rw-r--r-- thomaSilva96 thomaSilva96
```

### Interpretação

- `%a`: permissões em formato octal.
- `%A`: tipo de arquivo e permissões em formato simbólico.
- `%U`: nome do usuário proprietário.
- `%G`: nome do grupo associado.

O resultado confirmou que o proprietário possuía leitura e escrita, enquanto grupo e outros possuíam apenas leitura nos bits tradicionais de permissão.

## 7. Modificação das permissões

### Primeiro teste — chmod 600

```bash
chmod 600 arquivo.txt

ls -l arquivo.txt
```

Resultado:

```text
-rw------- 1 thomaSilva96 thomaSilva96 26 Sep 21 13:43 arquivo.txt
```

O comando removeu as permissões tradicionais de acesso do grupo e de outros usuários.

O proprietário permaneceu com leitura e escrita.

### Segundo teste — chmod 644

```bash
chmod 644 arquivo.txt

ls -l arquivo.txt
```

Resultado:

```text
-rw-r--r-- 1 thomaSilva96 thomaSilva96 26 Sep 21 13:43 arquivo.txt
```

As permissões anteriores foram restauradas.

### Aprendizado

O comando `chmod` modifica os bits de permissão de arquivos e diretórios.

Sua utilização deve considerar o princípio do menor privilégio, evitando conceder permissões além das necessárias.

## 8. Troubleshooting — Permission denied

### Objetivo

Reproduzir uma falha de execução causada pela ausência do bit de execução e identificar sua causa.

### Preparação

Foi criado um script Shell:

```bash
printf '#!/bin/sh\necho "Script executado"\n' > teste.sh

chmod 644 teste.sh
```

O arquivo possuía conteúdo executável, mas não havia recebido permissão de execução.

### Sintoma

Ao tentar executar o script diretamente:

```bash
./teste.sh
```

O terminal apresentou:

```text
-bash: ./teste.sh: Permission denied
```

### Diagnóstico

Foi utilizado o comando:

```bash
ls -l teste.sh
```

Resultado:

```text
-rw-r--r-- 1 thomaSilva96 thomaSilva96 34 Sep 21 13:47 teste.sh
```

A saída demonstrou que o arquivo existia, mas não possuía o bit de execução.

O problema não estava relacionado à inexistência do arquivo.

### Causa identificada

Ausência de permissão de execução nos bits tradicionais de permissão do arquivo.

### Correção

Foi executado:

```bash
chmod 755 teste.sh
```

O valor `755` concede:

- Proprietário: leitura, escrita e execução.
- Grupo: leitura e execução.
- Outros: leitura e execução.

Para esse script de laboratório, o objetivo era habilitar a execução. Em ambientes reais, as permissões devem ser definidas conforme os requisitos de acesso.

### Validação

Após a correção:

```bash
./teste.sh
```

Resultado:

```text
Script executado
```

O script executou corretamente.

### Conclusão do troubleshooting

A falha foi diagnosticada a partir da mensagem de erro e da inspeção das permissões.

A correção adicionou a permissão de execução necessária e o comportamento esperado foi confirmado por uma nova execução.

O laboratório demonstrou a importância de investigar a causa de uma falha antes de modificar permissões.

Não é adequado utilizar `chmod 777` indiscriminadamente para resolver problemas de acesso.

## 9. Ownership

### Comando executado

```bash
stat -c '%U:%G %a %n' arquivo.txt
```

Resultado:

```text
thomaSilva96:thomaSilva96 644 arquivo.txt
```

O comando confirmou:

- Proprietário: `thomaSilva96`.
- Grupo: `thomaSilva96`.
- Permissões: `644`.
- Arquivo: `arquivo.txt`.

### Comandos relacionados

| Comando | Finalidade |
|---|---|
| `chmod` | Modificar permissões |
| `chown` | Modificar o proprietário e, opcionalmente, o grupo |
| `chgrp` | Modificar o grupo associado |

Neste laboratório, `chown` e `chgrp` foram estudados conceitualmente, mas não executados.

A alteração de propriedade para outro usuário normalmente exige privilégios administrativos.

## 10. Decisões técnicas

As seguintes práticas serão adotadas nos próximos laboratórios:

1. Utilizar diretórios isolados para experimentos.
2. Evitar o uso desnecessário de privilégios administrativos.
3. Aplicar o princípio do menor privilégio.
4. Investigar problemas antes de modificar permissões.
5. Registrar erros, causas, correções e validações.
6. Manter os laboratórios separados de projetos comerciais.

## 11. Aplicação em Platform Engineering

Esses conceitos serão utilizados em diferentes cenários.

### Servidores Linux

Diagnosticar aplicações que não conseguem ler arquivos de configuração ou executar scripts.

### Docker

Compreender permissões e ownership de arquivos utilizados por processos dentro de containers.

### CI/CD

Investigar pipelines que falham ao executar scripts sem o bit de execução.

### Kubernetes

Compreender problemas relacionados à identidade de processos, permissões e acesso a volumes.

A aplicação em cada tecnologia será aprofundada nos respectivos laboratórios.

## 12. Evidências e referências

- [GitHub Skills — Review Pull Requests](https://github.com/Thomas-silva96/skills-review-pull-requests)
- [GitHub Skills — Resolve Merge Conflicts](https://github.com/Thomas-silva96/skills-resolve-merge-conflicts)
- [Laboratório Linux — Fundamentos](./README.md)

Os resultados dos comandos utilizados neste documento foram registrados durante a execução do laboratório em 21/09/2026.

## 13. Próxima etapa

Aprofundar os fundamentos operacionais de Linux:

- Processos e serviços.
- Filesystem e arquivos de configuração.
- Rede e conectividade.
- Logs.
- Troubleshooting de aplicações.

O objetivo é evoluir da manipulação básica de arquivos para o diagnóstico de problemas em serviços Linux.