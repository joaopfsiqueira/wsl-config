# wsl-config
Repositório criado para deixar salvo minhas configs WSL2.

> # Windows 11

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


# Configurações WSL2
- Gosto de limitar os recursos que o WSL2 vai utilizar da minha máquina. Para limitar a quantidade de recursos edito o arquivo .wslconfig dentro da pasta do usuário no próprio Windows, no meu caso c:\Users\user.

### Instalando vim
Antes de tudo, é provável que o windows não tenha instalado o `vim`, vamos fazer isso!

Em resumo, basta baixar o seguinte arquivo e ir clicando em next: https://ftp.nluug.nl/pub/vim/pc/gvim82.exe

Caso queira saber mais:
Recomendo essa documentação: [VIM](https://www.freecodecamp.org/portuguese/news/guia-de-instalacao-do-vim-no-windows-como-executar-o-editor-de-texto-vim-no-powershell-do-seu-pc/)
[Como usar o VIM](https://www.freecodecamp.org/news/vim-beginners-guide/)


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


# Oh My ZSH

- Nesse caso, já tenho uma sequência de comando exatos para configurar o `oh my zsh` no terminal! https://github.com/joaopfsiqueira/myConfigs-linux-terminal


# Configurando git

- Vamos definir globalmente o usuário e e-mail para poder trabalhar com github nas nossas aplicações.

1- `git config --global user.name "Your Name"` <br>
2- `git config --global user.email "youremail@domain.com"`


# Configurando Node
- Agora, precisa configurar o node no nosso linux! Vamos usar [Node Version Manager(NVM)](https://github.com/nvm-sh/nvm) para isso.

Em resumo, os passos:

1- Com o curl instalado, `curl https://raw.githubusercontent.com/creationix/nvm/master/install.sh | bash `<br>
2- `source ~/.profile`<br>
3- Restart o terminal.<br>
4- Instalei a versão 18.16, a LTS da época. `nvm install 18.16.0`



# Integrar Docker com WSL 2

* [Docker Engine (Docker Nativo) diretamente instalado no WSL2](#instalar-o-docker-com-docker-engine-docker-nativo).
* [Docker Desktop com WSL2](#instalar-o-docker-com-docker-desktop).

Recomendo que escolha a 1ª opção pelos seus benefícios, já que a maioria das pessoas poderão usar o WSL 2 como ferramenta central para desenvolvimento. Mas, neste tutorial vamos mostrar as duas forma de instalação.


### <a id="instalar-o-docker-com-docker-engine-docker-nativo"></a>1 - Instalar o Docker com Docker Engine (Docker Nativo)

A instalação do Docker no WSL 2 é idêntica a instalação do Docker em sua própria distribuição Linux, portanto se você tem o Ubuntu é igual ao Ubuntu, se é Fedora é igual ao Fedora. A documentação de instalação do Docker no Linux por distribuição está [aqui](https://docs.docker.com/engine/install/), mas vamos ver como instalar no Ubuntu.


> **Quem está migrando de Docker Desktop para Docker Engine, temos duas opções**
> 1. Desinstalar o Docker Desktop.
> 2. Desativar o Docker Desktop Service nos serviços do Windows. Esta opção permite que você utilize o Docker Desktop, se necessário, para a maioria dos usuários a desinstalação do Docker Desktop é a mais recomendada.
>Se você escolheu a 2º opção, precisará excluir o arquivo ~/.docker/config.json e realizar a autenticação com Docker novamente através do comando "docker login"

> **Se necessitar integrar o Docker com outras IDEs que não sejam o VSCode**
>
> O VSCode já se integra com o Docker no WSL desta forma através da extensão Remote WSL ou Remote Container.
> 
> É necessário habilitar a conexão ao servidor do Docker via TCP. Vamos aos passos:
> 1. Crie o arquivo /etc/docker/daemon.json: `sudo echo '{"hosts": ["tcp://0.0.0.0:2375", "unix:///var/run/docker.sock"]}' > /etc/docker/daemon.json`
> 2. Reinicie o Docker: `sudo service docker restart`
> 
> Após este procedimento, vá na sua IDE e para conectar ao Docker escolha a opção TCP Socket e coloque a URL `http://IP-DO-WSL:2375`. Seu IP do WSL pode ser encontrado com o comando `cat /etc/resolv.conf`.
> 
> Se caso não funcionar, reinicie o WSL com o comando `wsl --shutdown` e inicie o serviço do Docker novamente.


Instale os pré-requisitos:

```
sudo apt update && sudo apt upgrade
sudo apt remove docker docker-engine docker.io containerd runc
sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg \
    lsb-release
```

Adicione o repositório do Docker na lista de sources do Ubuntu:

```
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
echo \
  "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

Instale o Docker Engine

```
sudo apt-get update
```
```
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin
```

Dê permissão para rodar o Docker com seu usuário corrente:

```
sudo usermod -aG docker $USER
```

Inicie o serviço do Docker:

```
sudo service docker start
```

Este comando acima terá que ser executado toda vez que Linux for reiniciado. Se caso o serviço do Docker não estiver executando, mostrará esta mensagem de erro ao rodar comando `docker`:

```
Cannot connect to the Docker daemon at unix:///var/run/docker.sock. Is the docker daemon running?
```

O Docker Compose instalado agora estará na versão 2, para executa-lo em vez de `docker-compose` use `docker compose`.

### Erro ao iniciar o Docker no Ubuntu 22.04

> Se mesmo ao iniciar o serviço do Docker acontecer o seguinte erro ou similar:
>
> `Cannot connect to the Docker daemon at unix:///var/run/docker.sock. Is the docker daemon running?`
> Rode o comando `sudo update-alternatives --config iptables` e escolha a opção 1 `iptables-legacy`
>
> Rode novamente o `sudo service docker start`. Rode algum comando Docker como `docker ps` para verificar se está funcionando corretamente. Se não mostrar o erro acima, está ok.


#### Dica para Windows 11

No Windows 11 é possível especificar um comando padrão para ser executados sempre que o WSL for iniciado, isto permite que já coloquemos o serviço do docker para iniciar automaticamente. Edite o arquivo `/etc/wsl.conf`:

Rode o comando para editar:

`sudo vim /etc/wsl.conf`

Aperte a letra `i` (para entrar no modo de inserção de conteúdo) e cole o conteúdo:

```conf
[boot]
command="service docker start" 
```

Quando terminar a edição, pressione `Esc`, em seguida tecle `:` para entrar com o comando `wq` (salvar e sair) e pressione `enter`. Pronto, para reiniciar o WSL com o comando `wsl --shutdown` no DOS ou PowerShell para testar. Após abrir o WSL novamente, digite o comando `docker ps` para avaliar se o comando não retorna a mensagem acima: `Cannot connect to the Docker daemon at unix:///var/run/docker.sock. Is the docker daemon running?`

# Docker Compose
- Eu utilizo o docker compose para orquestramento de containers. Doc oficial: [Docker-Compose](https://docs.docker.com/compose/install/standalone/)

Em resumo:

1- `curl -SL https://github.com/docker/compose/releases/download/v2.18.1/docker-compose-linux-x86_64 -o /usr/local/bin/docker-compose` <br>
2- `sudo ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose`
