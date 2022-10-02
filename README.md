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