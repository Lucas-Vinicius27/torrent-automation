# Torrent Automation
Projeto que automatiza download via torrent com serviços em docker compose.

## Dependências
### S.O. Unix
Necessário ter instalado `Docker` e o `Docker Compose`.
### S.O. Windows
Necessário configurar `WSL2` com `Docker Desktop`.

## Comandos no Terminal
Para subir os serviços execute:
```bash
docker-compose up -d
```
Para remover os serviços execute:
```bash
docker-compose down
```

## Passos para implementação
* Clone este projeto onde irá subir os serviços.
* Copiar e colocar arquivo `.env.example` transformar a copia no arquivo `.env`.
* Criar uma frase, com a frase criar uma hash MD5 ou usar outro algoritmo que irá produzir uma hash, com a hash aplicar na variável de ambiente (no arquivo `.env`) `API_KEY_JACKET`, assim colocando sua hash no lugar da palavra `minhachave`.
* Criar um nome de usuário para aplicar na variável de ambiente `WEB_UI_USERNAME_JACKETT` colocando o nome no lugar da pralavra `meuusuario`, criar uma senha e aplicar na variável `WEB_UI_PASSWORD_JACKETT` colocando assim a senha no lugar da palavra `minhasenha`, esse usuário e senha serão para acessar o ambiente de interface do usuário do serviço `JACKETT`, caso ao abrir o UI do `JACKETT` não necessite colocar usuário e senha, é melhor configurar para pedir usuário e senha aumentando sua segurança.
* Criar uma senha de preferência diferente da senha utilizada no `JACKETT`, para aplicar na variável `DELUGE_WEB_PASSWORD`, colocando no lugar da palavra `mysecretpassword`, se a senha da variável não funcionar, será porque ela não foi aplicada e o serviço `DELUGE` está utilizando a senha padrão que é `deluge`, na UI do `DELUGE` em `preferences -> interface -> WebUI Password` é possível alterar a senha, altere para aumentar sua segurança.
* UI do serviço `DELUGE` irá aparecer no link `http://localhost:8112/`.
* UI do serviço `JACKETT` irá aparecer no link `http://localhost:9117/`.
* Caso você vá subir os serviços em um servidor descomentar as linhas que possuem o comando `network_mode: host` no arquivo `docker-compose.yml`, e para acessar as UIs no lugar da palavra `localhost` será o IP do seu servidor.
* Suba os serviços para que os diretórios sejam criados, na pasta de configurações do `DELUGE` (caminho da pasta `services/deluge/config`), encontrar o arquivo `core.conf` e adicionar a linha `"tracker_host": "ìp_maquina:porta_jackett"`, onde `ìp_maquina` será o IP da sua máquina ou servidor, `porta_jackett` será a porta de acesso ao serviço `JACKETT` se você não alterar será `9117`, salve o arquivo, remova os serviços e suba novamente, para que o `DELUGE` possa pegar a nova configuração.