# 2023A-SO2

# Aula 1: 27-02-2023
### Instalação do Openssh
sudo apt update
sudo apt upgrade
ou
sudo apt-get update
sudo apt install openssh-server

### Acesso SSH
ssh univates@127.0.1.1 -p22

### Ajuste do keyboard
sudo nano /etc/default/keyboard
Ajustar o teclado para br

### Ajuste do time zone
sudo dpkg-reconfigure tzdata

### verificar o status de um serviço
service ssh status
service <nome-servico><comando>


### Configurar a rede Do VirtualBox
Abrir o VirtualBox

Acesse as opções de sua: VM → Rede → Redirecionamento de Portas 

A rede fica como NATNome: SSH

Tipo: TCP
Endereço IP do hospedeiro:     127.0.1.1
Porta do hospedeiro:      22
IP do host (virtual):        10.0.2.15
Porta do host (virtual):      22
Explicação:

IP do hospedeiro (Sua máquina servidor): 127.0.0.1
Porta do hospedeiro(Sua máquina servidor): 22
IP do Convidado (Máquina Virtual): 10.0.2.15 
Porta do Convidado (Máquina Virtual): 22

Para acessar com ferramentas de ssh ou pelo terminal do windows
c:\> ssh univates@127.0.1.1 -p 22

### Script instalador
#!/bin/bash

### Instalação do Openssh
sudo apt update
sudo apt upgrade -y
sudo apt install openssh-server -y

### Ajuste do time zone
sudo dpkg-reconfigure tzdata

### Para Rodar o script
sh nome-arquivo.sh

ou
./nome-arquivo.sh
ou
sudo chmos +x nome-arquivo.sh

## Aula 2: 06-03-2023

### Modificar a porta da máquina
/etc/ssh$ nano ssh_config
ou
/etc/ssh$ nano sshd_config
descomentar a linha da porta e colocar a porta desejada

### conseguir acessar por interface grafica
descomentar x11 e por yes

### atualizar o VI
/etc/ssh$ sudo apt install vim

### copiar e preservar as permissoes do arquivo .bashrc
sudo cp -p .bashrc .bashrc-20230306

### mudar o nome do arquivo
mv antigo novo

### editar o bashrc via VI
vi .bashrc

procurar linha: :numero da linha
copia uma linha: yy
colar a linha: p
editar: a -> um caracter a direita
editar: i -> permanece no caracter
salvar: esc :wq
sair sem salvar: esc:q!

### novo comando criado no alias (bashrc)
dir = ls-ahF

### Ir para novo login na máquina local
ctrl + alt + f1/f2/f3

### Novo login máquina remota
sudo login
logout para sair

### Saber qual o shell
echo $SHELL

### Para baixar um novo terminal
sudo apt install zsh
para acessar um shell: zsh (nome do shell)

### instalar git
sudo apt install git

echo "# 2023a-soii" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/larissaDSR/2023a-soii.git
git push -u origin main

git config --global user.name "Larissa Rocha"
git config --global user.email "larissa.rocha2@universo.univates.br"

## Aula 3: 13-03-2023
 
### permissões
-   0
R - 4
w - 2
X - 1

Pastas: d
arquivos: -
Programas: - (pode existir link: l)

### Localizar palavras dentro do arquivo
fgrep palavra nomedoarquivo
ou
cat nomedoarquivo |grep palavra

### Achar grupos de um usuario
fgrep univates /etc/group (mostra os codigos)
ou
groups univates (não mostra os códigos)

### Criar usuário
sudo adduser nomeuser
sudo useradd (É o melhor comando)
sudo useradd -m -b /home/gerentes -g gerentes -s /bin/sh joao
### para script:
sudo useradd -m -b /home/gerentes -g gerentes -s /bin/bash -p $(openssl passwd -1 teste123) username (Insegura: pode ser visto a senha pelo historico do terminal)

### Senhas
sudo vi shadow etc/passwd
sudo vi gshadow etc/group
sudo passwd suporte2 (muda/adiciona senha ao usuário)+fácil
ou
sudo echo teste:senha_de_teste | chpasswd
para scrip:


### Ajuda com comandos
comando --help
man comando

## Aula 4: 20-03-2023

### Procesos
cd /proc (Não é necessário estar dentro deste diretório para rodar os comandos abaixo)
ll
ps -ef |grep univates(usuario ou processo) (para vizualizar ps processos de determinado usuário)
ps -ef |grep univates(usuario ou processo) |wc -l (para contar o número de processos, não é tão preciso)
ou
ps -aux |grep bash(usuario ou processo)
htop (vizualizar processos mais precisamente)

### Ver o tamanho da pasta
sudo du -sh /var(pasta)
sudo du -sh log/

### Filtrar arquivos
ls -R /home *.mp3
ls -R /home |grep mp3 (Mostra somente o arquivo)
ll -R /home |grep mp3 (Mostra o arquivo, permissões e dono)
tree -P *.mp3 (Para mostrar a pasta onde está o arquivo)

### Instalar Tree
sudo apt instal tree

## Aula 5: 27-03-2023

### Instalar Apache
sudo apt update
sudo apt install apache2

### Instalar Zip
sudo apt install zip

### Backup de site
sudo zip -r nomedobackup.zip site/

### Firewall ufw
sudo ufw enable (Habilitar o Firewall)
sudo ufw app list
sudo ufw status numbered
sudo ufw status verbose
sudo ufw reload
sudo ufw allow 8085/tcp (liberar portas)
sudo ufw dany 8085/tcp (bloquear portas)