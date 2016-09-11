# Usando o vagrant

### O que é o vagrant?

O vagrant é uma ferramenta usada para criar ambientes virtuais de uma forma fácil, ele faz uso de programas de virtuallização como o Virtual Box, VMWare, AWS... dentre outros... você pode usa-lo para desenvolver, testar e compartilha o seu ambiente de desenvolvimento.

### Porque usar o vagrant?

Se você já usou o Virtual Box ou qualquer outro programa de vistualização, sabe como é chato ficar copiando VM's... depois configurar rede e outras coisas, sem falar o espaço em disco que é consumido... que no vagrant isso se resume em alterar um arquivo e pronto sua VM já está pronta.

Agora vamos por a mão no teclado. =D

#### Instalando o vagrant

Efetue o [download](https://www.vagrantup.com/downloads.html) aqui, baixe e instale a versão adequada para o seu sistema operacional.

Efetue o teste para ver se ele está funcionando corretamente:

Abra o console de vc estiver no GNU Linux/MAC ou cmd se estiver no Windows:
```
$ vagrant
```

Saída:
```
Usage: vagrant [options] <command> [<args>]

    -v, --version                    Print the version and exit.
    -h, --help                       Print this help.

Common commands:
     box             manages boxes: installation, removal, etc.
     destroy         stops and deletes all traces of the vagrant machine
     global-status   outputs status Vagrant environments for this user
     halt            stops the vagrant machine
     help            shows the help for a subcommand
     init            initializes a new Vagrant environment by creating a Vagrantfile
     login           log in to HashiCorp's Atlas
     package         packages a running vagrant environment into a box
     plugin          manages plugins: install, uninstall, update, etc.
     port            displays information about guest port mappings
     powershell      connects to machine via powershell remoting
     provision       provisions the vagrant machine
     push            deploys code in this environment to a configured destination
     rdp             connects to machine via RDP
     reload          restarts vagrant machine, loads new Vagrantfile configuration
     resume          resume a suspended vagrant machine
     snapshot        manages snapshots: saving, restoring, etc.
     ssh             connects to machine via SSH
     ssh-config      outputs OpenSSH valid configuration to connect to the machine
     status          outputs status of the vagrant machine
     suspend         suspends the machine
     up              starts and provisions the vagrant environment
     version         prints current and latest Vagrant version

For help on any individual command run 'vagrant COMMAND -h'

Additional subcommands are available, but are either more advanced
or not commonly used. To see all subcommands, run the command
'vagrant list-commands'.
```

### Local de trabalho

Eu recomendo fortemente que vc tenha um local para colocar seus projetos, os meus sempre ficam em:
```
/home/miqueias/projetos/
```

### O que é uma box

Uma box é uma imagem configurada, pronta para ser usada, ou não pode ser também somente um sistema operacional por exemplo um Ubuntu 16.04 somente com o básico instalado nele.

### Baixando uma box

Você ir no [vagrant cloud](https://atlas.hashicorp.com/boxes/search?utm_source=vagrantcloud.com&vagrantcloud=1) para escolher uma imagem.

Ps. No momento que escrevi esse tutorial a versão atual do ubuntu era 16.04 então aconselho fazer uso dessa imagem:

```
ubuntu/trusty64
```

### Instalando um box no vagrant

Existe duas formas para instalar uma imagem, a primeira é via vagrant cloud e a outra manualmente(Ps. A configuração manual irei fazer posteriormente...):

#### Vagrant cloud

```
vagrant box add ubuntu/trusty64
```  

### Visualizar imagens

Para visulizar as imagens:
```
vagrant box list
```

Saída:
```
ubuntu/trusty64   (virtualbox, 20160816.0.0)
```

### Quase tudo pronto

Nesse momento você tem quase tudo pronto, agora precisamos criar uma nova VM.

### Criando uma VM

Vamos criar uma nova pasta para o nosso novo projeto, no meu ficou assim:
```
/home/miqueias/projetos/meunovoprojeto
```

Execute o comando abaixo dentro da pasta, para criar o arquivo de configuração
```
vagrant init ubuntu/trusty64
```

Saída:
```
A 'Vagrantfile' has been placed in this directory. You are now
ready to 'vagrant up' your first virtual environment! Please read
the comments in the Vagrantfile as well as documentation on
'vagrantup.com' for more information on using Vagrant.
```

O arquivo de configuração da nossa VM foi criado e agora você pode abri-lo, o meu está assim:

```
# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure(2) do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://atlas.hashicorp.com/search.
  config.vm.box = "ubuntu/trusty64"

  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  # config.vm.box_check_update = false

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  # config.vm.network "forwarded_port", guest: 80, host: 8080

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  # config.vm.network "private_network", ip: "192.168.33.10"

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network "public_network"

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  # config.vm.synced_folder "../data", "/vagrant_data"

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
  # config.vm.provider "virtualbox" do |vb|
  #   # Display the VirtualBox GUI when booting the machine
  #   vb.gui = true
  #
  #   # Customize the amount of memory on the VM:
  #   vb.memory = "1024"
  # end
  #
  # View the documentation for the provider you are using for more
  # information on available options.

  # Define a Vagrant Push strategy for pushing to Atlas. Other push strategies
  # such as FTP and Heroku are also available. See the documentation at
  # https://docs.vagrantup.com/v2/push/atlas.html for more information.
  # config.push.define "atlas" do |push|
  #   push.app = "YOUR_ATLAS_USERNAME/YOUR_APPLICATION_NAME"
  # end

  # Enable provisioning with a shell script. Additional provisioners such as
  # Puppet, Chef, Ansible, Salt, and Docker are also available. Please see the
  # documentation for more information about their specific syntax and use.
  # config.vm.provision "shell", inline: <<-SHELL
  #   sudo apt-get update
  #   sudo apt-get install -y apache2
  # SHELL
end
```

Ps. Sim o vagrant é feito em Ruby. =P

Ele tem muitas configurações, mas iremos fazer a mais simples para ão complicar o tutorial

### Configurando o Vagrantfile

Copie a linha, descomente e altere a para a porta que deseja liberar para ter acesso no seu sistema operacional.
Ps. Aqui vc pode liberar portas que o seu Framework usa no meu caso o Django configuro para a porta 3000, também pode liberar as portas de outros aplicativos como Postgre, MongoDB..

```
# config.vm.network "forwarded_port", guest: 80, host: 8080
```

No meu caso ficaria assim
```
config.vm.network "forwarded_port", guest: 3000, host: 3000
```

De acordo com a quantidade porta q você for precisando é só ir adiconando, nesse momento só iremos fazer essa configuração.


### Iniciando a VM

Para inciar a VM ou melhor dar o boot:
```
vagrant up
```

Como é a primeira vez que iniciamos a VM ela vai demorar um pouco para concluir isso é normal, das próximas vezes ela irá iniciar bem mais rápido.

Saída:
```
Bringing machine 'default' up with 'virtualbox' provider...
==> default: Importing base box 'ubuntu/trusty64'...
==> default: Matching MAC address for NAT networking...
==> default: Checking if box 'ubuntu/trusty64' is up to date...
==> default: A newer version of the box 'ubuntu/trusty64' is available! You currently
==> default: have version '20160816.0.0'. The latest is version '20160907.0.0'. Run
==> default: `vagrant box update` to update.
==> default: Setting the name of the VM: meunovoprojeto_default_1473554710159_95445
==> default: Clearing any previously set forwarded ports...
==> default: Clearing any previously set network interfaces...
==> default: Preparing network interfaces based on configuration...
    default: Adapter 1: nat
==> default: Forwarding ports...
    default: 3000 (guest) => 3000 (host) (adapter 1)
    default: 22 (guest) => 2222 (host) (adapter 1)
==> default: Booting VM...
==> default: Waiting for machine to boot. This may take a few minutes...
    default: SSH address: 127.0.0.1:2222
    default: SSH username: vagrant
    default: SSH auth method: private key
    default:
    default: Vagrant insecure key detected. Vagrant will automatically replace
    default: this with a newly generated keypair for better security.
    default:
    default: Inserting generated public key within guest...
    default: Removing insecure key from the guest if it's present...
    default: Key inserted! Disconnecting and reconnecting using new SSH key...
==> default: Machine booted and ready!
==> default: Checking for guest additions in VM...
    default: The guest additions on this VM do not match the installed version of
    default: VirtualBox! In most cases this is fine, but in rare cases it can
    default: prevent things such as shared folders from working properly. If you see
    default: shared folder errors, please make sure the guest additions within the
    default: virtual machine match the version of VirtualBox you have installed on
    default: your host and reload your VM.
    default:
    default: Guest Additions Version: 4.3.36
    default: VirtualBox Version: 5.0
==> default: Mounting shared folders...
    default: /vagrant => /home/miqueias/projetos/js/meunovoprojeto
```

### Usando a sua nova VM

Para usar a sua VM se você estiver no GNU Linux/MAC é só abrir o console e digitar:

```
vagrant ssh
```

Ps. Você pode usar no Windows o Git Bash seria o mesmo procemento acima.

No windows você pode usar o [Putty](http://www.putty.org/), no endereço de ip você coloca
```
vagrant@localhost
```

Porta padrão 2222

Depois de executar o comando você receberá uma mensagem de boas vindas do Ubuntu
Ps. Essa mensagem pode variar dependendo da distro q você escolheu

```
Welcome to Ubuntu 14.04.5 LTS (GNU/Linux 3.13.0-93-generic x86_64)

 * Documentation:  https://help.ubuntu.com/

  System information as of Sun Sep 11 11:34:21 UTC 2016

  System load:  0.16              Processes:           94
  Usage of /:   3.5% of 39.34GB   Users logged in:     0
  Memory usage: 18%               IP address for eth0: 10.0.2.15
  Swap usage:   0%

  Graph this data and manage this system at:
    https://landscape.canonical.com/

  Get cloud support with Ubuntu Advantage Cloud Guest:
    http://www.ubuntu.com/business/services/cloud

0 packages can be updated.
0 updates are security updates.

New release '16.04.1 LTS' available.
Run 'do-release-upgrade' to upgrade to it.
```

Obs.: Se você quiser outros ambientes é só criar uma nova pasta, criar a VM, configurar, iniciar e usar. =)

### Comandos do vagrant para adiministrar a suas VM's

Criar
```
$ vagrant init
```

Apagar
```
$ vagrant destroy
```

Iniciar
```
$ vagrant up
```

Reiniciar
```
$ vagrant reload
```

Deligar
```
$ vagrant halt
```
Suspender
```
$ vagrant suspend
```

Voltando do modo de suspenção
```
$ vagrant resume
```

Acessar
```
$ vagrant ssh
```

Status
```
$ vagrant status
```

Ajuda
```
$ vagrant help
```

### Obervações:
Sempre quando vou iniciar o servidor web de desenvolvimento, configuro o host para 0.0.0.0:3000 sem isso provavelmente você não terá acesso a sua aplicação.

Chegamos ao final desse tutorial, existe muitas configurações que você pode fazer no vagrant, meu foco foi fazer a configuração mais simples possível para que você não tenha problemas com eu tive no começo.

Abraços. Qualquer dúvida estarei no grupo de Python Brasil e no meu email: [miqueiaspenha@gmail.com](mailto:https://www.vagrantup.com/docs/getting-started/)

### Referencias

[https://www.vagrantup.com/docs/getting-started/](https://www.vagrantup.com/docs/getting-started/)
