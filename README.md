# wsl-config
Repositório criado para deixar salvo minhas configs WSL2.

> ## Windows 11

Execute o comando:

```bash
wsl --install
```

Este comando irá instalar todas as dependências do WSL instalando o `Ubuntu` como o Linux padrão. 

Se quiser instalar uma versão diferente do Ubuntu, execute o comando `wsl -l -o`, será listado todas as versões de Linux disponíveis. Instale a versão escolhida com o comando `wsl --install -d nome-da-distribuicao`.

Prefiro a versão 22.04.

## Escolha sua distribuição Linux no Windows Store

Também é possível instalar distribuições Linux pelo Windows Store. Escolha sua distribuição Linux preferida no aplicativo Windows Store, sugiro o Ubuntu (sem versão) por ser uma distribuição popular e que já vem com várias ferramentas instaladas por padrão.

Ao iniciar o Linux instalado, você deverá criar um **nome de usuário** que poderá ser o mesmo da sua máquina e uma **senha**, este será o usuário **root da sua instância WSL**.

Parabéns, seu WSL2 já está funcionando:


## (Opcional) Usar Windows Terminal como terminal padrão de desenvolvimento para Windows

Uma deficiência que o Windows sempre teve era prover um terminal adequado para desenvolvimento. Agora temos o **Windows Terminal** construído pela própria Microsoft que permite rodar terminais em abas, alterar cores e temas, configurar atalhos e muito mais.

1 - Instale-o pelo Windows Store<br>
2 - Abra-o e clique na setinha que fica ao lado das abas.<br>
3 - Vá em configurações e sete o ubuntu como inicializador padrão do terminal.<br>


## Configurações WSL2
- Gosto de limitar os recursos que o WSL2 vai utilizar da minha máquina. Para limitar a quantidade de recursos edito o arquivo .wslconfig dentro da pasta do usuário no próprio Windows, no meu caso c:\Users\user.

### instalando vim
Antes de tudo, é provável que o windows não tenha instalado o `vim`, vamos fazer isso!

Em resumo, basta baixar o seguinte arquivo e ir clicando em next: https://ftp.nluug.nl/pub/vim/pc/gvim82.exe

Caso queira saber mais:
Recomendo essa documentação: [VIM](https://www.freecodecamp.org/portuguese/news/guia-de-instalacao-do-vim-no-windows-como-executar-o-editor-de-texto-vim-no-powershell-do-seu-pc/)


### Utilizando vim para alterar .wslconfig no windows
1- vim .wslconfig<br>
2- adicionar: 
```
[wsl2]
memory=4GB
processors=4
swap=2GB
```
Para aplicar estas configurações é necessário reiniciar as distribuições Linux, então sugiro executar no PowerShell o comando: `{wsl --shutdown` (Este comando vai desligar todas as instâncias WSL 2 ativas e basta abrir o terminal novamente para usa-la já com as novas configurações).
