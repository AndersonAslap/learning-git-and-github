# learning-git-and-github

- Git Flow
- Configurações das branches
- Pull Requests / Templates para PR
- Code Review
- Plugin do VSCode
- CODEOWNERS
- SemVer
- Conventional Commits

> Git Flow

- https://github.com/petervanderdoes/gitflow-avh/wiki/Installing-on-Linux,-Unix,-etc.

> Configurar Assinaturas

- chave privada
- chave pública

> Criando chave com gpg

```bash
gpg --full-generate-key

Por favor selecione o tipo de chave desejado:
   (1) RSA e RSA (padrão)
   (2) DSA e Elgamal
   (3) DSA (apenas assinatura)
   (4) RSA (apenas assinar)
Sua opção? 1
RSA chaves podem ter o seu comprimento entre 1024 e 4096 bits.
Que tamanho de chave você quer? (3072) 4096
O tamanho de chave pedido é 4096 bits
Por favor especifique por quanto tempo a chave deve ser válida.
         0 = chave não expira
      <n>  = chave expira em n dias
      <n>w = chave expira em n semanas
      <n>m = chave expira em n meses
      <n>y = chave expira em n anos
A chave é valida por? (0) 1y
A chave expira em dom 01 out 2023 21:39:03 -03
Está correto (s/N)? y

GnuPG precisa construir uma ID de usuário para identificar sua chave.

Nome completo: Anderon Adolfo
Endereço de correio eletrônico: <EMAIL>
Comentário: (opcional)
Você selecionou este identificador de usuário:
    "Anderson Adolfo <anderson.adolfo1998@gmail.com>"

Muda (N)ome, (C)omentário, (E)ndereço ou (O)k/(S)air? o

> Após isso é solicitado uma senha para sua chave

Precisamos gerar muitos bytes aleatórios. É uma boa idéia realizar outra
atividade (digitar no teclado, mover o mouse, usar os discos) durante a
geração dos números primos; isso dá ao gerador de números aleatórios
uma chance melhor de conseguir entropia suficiente.
Precisamos gerar muitos bytes aleatórios. É uma boa idéia realizar outra
atividade (digitar no teclado, mover o mouse, usar os discos) durante a
geração dos números primos; isso dá ao gerador de números aleatórios
uma chance melhor de conseguir entropia suficiente.
gpg: chave F9C2A3C5078474CF marcada como plenamente confiável
gpg: directory '/home/cmtech/.gnupg/openpgp-revocs.d' created
gpg: revocation certificate stored as '/home/cmtech/.gnupg/openpgp-revocs.d/702306B0214FF7DB3BAC681AF9C2A3C5078474CF.rev'
chaves pública e privada criadas e assinadas.

pub   rsa4096 2022-10-02 [SC] [expira: 2023-10-02]
      702306B0214FF7DB3BAC681AF9C2A3C5078474CF
uid                      Anderson Adolfo <anderson.adolfo1998@gmail.com>
sub   rsa4096 2022-10-02 [E] [expira: 2023-10-02]

```

- Comando para listar as chaves

```bash
gpg --list-secret-key --keyid-form LONG
```

- Comando para listar o endereço da chava

```bash
gpg --armor --export $ID_CHAVE
```

- Com isso acesse o github
  -> Configurações
  -> SSH and GPG keys
  -> New GPG key
  -> Colar a chave

- No terminal

```bash
git congif --global user.signingkey $ID_CHAVE
```

- Obeservação se você não quiser sempre ter que rodar o comando abaixo, cploque no arquivo de variáveis de ambiente

```bash
export GPG_TTY=$(tty)
```

- O comando abaixo faz com que por padrão os commits sejam assinadas, se você não colocar o [ --global ] o comando só terá efeito no repositório atual em que você esteja naquele momento.

```bash
git config --global commit.gpgsign true
```

- O comando abaixo faz com que por padrão as tags sejam assinadas, se você não colocar o [ --global ] o comando só terá efeito no repositório atual em que você esteja naquele momento.

```bash
git config --global tag.gpgSign true
```

- Após realizar algum commit o comando abaixo mostrará se seu commit foi assinado

```bash
git log --show-signature -1
```

> Adicionando mais emails na chave

```bash
gpg --edit-key $ID_CHAVE
```

```bash
gpg (GnuPG) 2.2.4; Copyright (C) 2017 Free Software Foundation, Inc.
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.

Chave secreta disponível.

sec  rsa4096/F9C2A3C5078474CF
     criado: 2022-10-02  expira: 2023-10-02  uso: SC
     confiança: final         validade: final
ssb  rsa4096/25E27F9C873712CA
     criado: 2022-10-02  expira: 2023-10-02  uso: E
[final] (1). Anderson Adolfo <anderson.adolfo1998@gmail.com>

gpg> adduid
Nome completo: Anderson Aslap
Endereço de correio eletrônico: $EMAIL
Comentário:
Você selecionou este identificador de usuário:
    "Anderson Aslap <anderson.works1998@gmail.com>"

Muda (N)ome, (C)omentário, (E)ndereço ou (O)k/(S)air? o

sec  rsa4096/F9C2A3C5078474CF
     criado: 2022-10-02  expira: 2023-10-02  uso: SC
     confiança: final         validade: final
ssb  rsa4096/25E27F9C873712CA
     criado: 2022-10-02  expira: 2023-10-02  uso: E
[final] (1)  Anderson Adolfo <anderson.adolfo1998@gmail.com>
[ desconhecida] (2). Anderson Aslap <anderson.works1998@gmail.com>

gpg> uid 2

sec  rsa4096/F9C2A3C5078474CF
     criado: 2022-10-02  expira: 2023-10-02  uso: SC
     confiança: final         validade: final
ssb  rsa4096/25E27F9C873712CA
     criado: 2022-10-02  expira: 2023-10-02  uso: E
[final] (1)  Anderson Adolfo <anderson.adolfo1998@gmail.com>
[ desconhecida] (2)* Anderson Aslap <anderson.works1998@gmail.com>
gpg> trust
sec  rsa4096/F9C2A3C5078474CF
     criado: 2022-10-02  expira: 2023-10-02  uso: SC
     confiança: final         validade: final
ssb  rsa4096/25E27F9C873712CA
     criado: 2022-10-02  expira: 2023-10-02  uso: E
[final] (1)  Anderson Adolfo <anderson.adolfo1998@gmail.com>
[ desconhecida] (2)* Anderson Aslap <anderson.works1998@gmail.com>

Por favor decida quanto você confia neste usuário para
verificar corretamente as chaves de outros usuários
(olhando em passaportes, checando impressões digitais
de outras fontes...)

  1 = Eu não sei ou nem direi
  2 = Eu NÃO confio
  3 = Eu tenho pouca confiança
  4 = Eu confio totalmente
  5 = Eu confio ao extremo
  m = voltar ao menu principal

Sua decisão? 5
Você quer realmente definir esta chave à confiança final? y

gpg> save
```

## SemVer

https://semver.org/lang/pt-BR/

2.1.4

(2) -> MAJOR => Versão principal do sistema -> API PÚBLICA DISPONÍVEL
(1) -> MINOR -> Adicionado funcionalidades, mas compatível com a API
(4) -> PATCH -> Bugs, ajustes que não foram feita na aplicação.

MAJOR = 0 - API Instável. Pode mudar a qualquer momento.

1.0.0-alpha < 1.0.0

## Conventional Commits

https://www.conventionalcommits.org/en/v1.0.0/

<type>[optional scope]: <description>

[optional body]

[optional footer(s)]

types

fix : resolvendo bug
feat : nova feature ou seja novo recurso ao sistema
breaking change : quebrando a compatibilidade da api pública
build : gerando build
chore :
ci :
docs : alteração ou criação ou remoção de documentos
style :
refactor :
test :
perf :
