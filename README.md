# One Click Stacks
## Stacks prontas pra você implantar na sua VPS com poucos cliques.

Faça o deploy de mais de 5+ open-source apps usando os templates do Portainer ou com um unico comando para os mais avançados.

Aplicativos configurados e personalizados ao máximo para implantação em pouquissimos passos.

- [x] Compatibilidade com Traefik
- [x] Compatibilidade com Portainer
- [x] Sem necessidade de gerenciar .envs, mas com opção ainda disponivel para quem precisar
- [x] Compatibilidade com distribuição de armazenamento (GlusterFS, Ceph, NFS) em a variavel `VOLUME_PATH=/mnt/storage_mountpoint/`

- **Aberto para contribuição** - Qualquer pessoa pode mandar os requests e consertar erros e fornecer atualizações para as versões das aplicações.
- **Implantação simples** - Stacks prontas, com documentação e detalhes sobre cada váriavel em português.
- **Compatibilidade com Swarm e Portainer** - Templates prontos para produção com tudo semi configurado para deploy em servidores pronto para uso.

## Primeiros passos
### Documentação para noobs e intermediários em docker compose.
São usadas variáveis para que você economize tempo ao setar varios aplicativos e não precise digitar seu email ou senha todas as vezes que for fazer o deploy de uma stack.

<details><summary>Veja aqui as variáveis padrão do one click stacks.</summary>
    
- **DOMAIN** - Seu dominio padrão. Ex: seudominio.com.br
- **SUBDOMAIN** - Somente a parte que ira antes do seu dominio, para facitar a instalação de cada aplicação. Ex: portainer.seudominio.com.br
- **SMTP_SENDER** - Email que irá aparecer quando se envia um email novo pelo servidor. Ex: nao-responda@gmail.com
- **SMTP_SERVER** - Endereço do servidor SMTP que irá enviar os emails. Ex: gmail.smtp.com ou mail.seudominio.com
- **SMTP_USER** - Usuário que ira logar no servidor SMTP, normalmente é seu email principal. Ex: seuemail@gmail.com
- **SMTP_PASSWORD** - Senha do seu email ou senha de aplicativo. [Saiba mais sobre senhas de aplicativo](https://atendimento.tecnospeed.com.br/hc/pt-br/articles/4418115119127-Como-criar-senha-de-aplicativo-para-email)
- **NUMBER** - Uma aplicação pode ter varias instancias rodando, -1 -2 -3 -4, se não alterada o padrão será -1. Ex: Portainer-1
- **VERSION** - A versão da aplicação a ser usada no container, se não alterada será usada a ultima versão estável do aplicativo.
- **TRUSTED_IPS** - IP dos servidores que vão se conectar a suas aplicações, se não alterado o padrão sera somente o localhost.
- **ACME_EMAIL** - Email usado para aquisição dos certificados Let's Encrypt. SUPER IMPORTANTE
- **ACME_EMAIL** - Email usado para aquisição dos certificados Let's Encrypt. SUPER IMPORTANTE
    
</details>

Variáveis também serão disponivilzadas em arquivos .env para maior controle para quem quiser implantar pelo docker stack compose ou via interface web do portainer.

## Preparando tudo
Setando as váriaveis que irão ser usadas para a maioria das aplicações usadas nas stacks.

### 1. Deploy Docker
```bash
sudo apt-get update
sudo apt-get install \
    ca-certificates \
    curl \
    gnupg \
    lsb-release
```
```bash
 sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin
```
```bash
docker swarm init
docker network create --driver=overlay traefik-public
docker stack deploy -c stacks/traefik.yml traefik
```
[Documentação Docker](https://docs.docker.com/engine/install/ubuntu/)

### 2. Deploy Portainer
```bash
curl https://raw.githubusercontent.com/matheusmaiberg/one-click-stacks/main/portainer/portainer-exposed.yml
```

### 3. Deploy do Traefik
Clique em 

```bash
docker swarm init
docker network create --driver=overlay traefik-public
docker stack deploy -c stacks/traefik.yml traefik
```
### 4. Check your HTTP and HTTPS ports
curl https://ipv4.am.i.mullvad.net/port/80
curl https://ipv4.am.i.mullvad.net/port/443

### 5. Deploy a stack
DOMAIN=<mydomain.com> docker stack deploy -c <stack.yml> <name>

### Example
DOMAIN=ghost.example.com docker stack deploy -c stacks/ghost.yml ghost

