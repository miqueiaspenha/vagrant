Instalando o postgres
```
sudo apt-get update
sudo apt-get install postgresql postgresql-contrib
```

Entrando como postgres
```
sudo -u postgres psql
```

Alterar senha do usuario postgres
```
ALTER USER postgres WITH PASSWORD 'suasenha';
```

Saindo
```
potgres=# \q
```

Configurando o postgres
Edite o arquivo /etc/postgresql/VERSAO/main/pg_hba.conf
```
host all all 0.0.0.0/0 trust
```

Depois edite esse /etc/postgresql/VERSAO/main/postgresql.conf
```
listen_addresses = '*'
```

Reiniciei o postgres
```
sudo /etc/init.d/postgresql restart
```

Configure o seu vagrantfile
```
config.vm.network :forwarded_port, host: 5432, guest: 5432
```

Agora tente conectar com o usuario postgres