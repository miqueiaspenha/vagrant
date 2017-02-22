Instlando e configurando o mysql no vagrant

Instalar o mysql
# sudo apt-get install mysql-server mysql-client

Editar o arquivo para ter acesso externo
# sudo nano /etc/mysql/mysql.conf.d/mysqld.cnf

Editar a linha
bind-address            = 0.0.0.0 #127.0.0.1

Logar no mysql
# mysql -u root -p

Marcando que vai usar o banco de dados mysql
# use mysql

Visualizar os usuarios
-> select user,host from mysql.user where user='root';

Criando o usuario pra o vagrant
-> create user 'vagrant'@'10.0.2.2' identified by 'vagrant';
-> grant all privileges on *.* to 'vagrant'@'10.0.2.2' with grant option;
-> flush privileges;

Obs.: Não esquecer de liberar a porta 3306 do mysql no seu Vagrantfile
config.vm.network "forwarded_port", guest: 3306, host: 3306

Reiniciar a vm do vagrant para concluir as alterações