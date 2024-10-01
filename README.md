# MGLAMP

É um script que permite realizar diversas tarefas automaticamente, como:

- Instalação do Apache, MariaDB, PHP e PHPMyAdmin
- Ativar módulos de SSL e Rewrite
- Iniciar, Reiniciar e Parar o Apache e MariaDB
- Criar e remover subdomínio com certificado SSL

## Requerimento

- Linux Debian 12 ou superior de 64 bits com sudo ativado
- Linux Ubuntu 22.04 ou superior de 64 bits
- OpenSSL

Para criar subdomínios com SSL é necessário instalar o OpenSSL, use o comando abaixo:

```
sudo apt install openssl
```

## Instalação

Não requer instalação, é só extrair, aplicar permissão de execução e executar.

```
chmod +x mglamp
./mglamp
```

### Configurações

Você pode alterar a pasta de diretórios do seu projeto e a pasta de criação de certificados SSL, para isso edite o arquivo "mgconfig" e altere as variáveis "mg_diretorioprojeto" e "mg_diretoriossl".

### Certificado SSL

Para que o certificado SSL funcione corretamente, é necessário adicionar o arquivo pem no seu navegador de Internet.

No Google Chrome ou Chromium abra as Configurações > Privacidade e Segurança > Segurança > Gerenciar Certificados > Autoridades > Importar.

Importe o arquivo PEM que está na pasta "mglamp" em sua pasta principal ou caso tenha alterado a variável mg_diretoriossl abra a pasta que foi definida nessa variável.

### Instalação do PHPMyAdmin

Ao ser solicitado para selecionar o servidor, escolha o Apache2.

Ao ser solicitado para criar um banco de dados, recomendo selecionar a opção "não", após a instalação crie o banco de dados manualmente.

### Configuração de Segurança do MariaDB

Após a instalação realize as configurações de segurança do MariaDB.

- Digite no terminal: sudo mysql_secure_installation
- Pressione ENTER em Enter current password for root (enter for none):
- Pressione n para Switch to unix_socket authentication Y/n
- Pressione n para Change the root password?
- Pressione Y para Remove anonymous users?
- Pressione Y para Disallow root login remotely?
- Pressione Y para Remove test database and access to it?
- Pressione Y para Reload privilege tables now?

### Configurando o PHPMyAdmin para login automático
Edite o arquivo: /etc/phpmyadmin/config.inc.php:

Altere o auth_type para:
$cfg['Servers'][$i]['auth_type'] = 'config';

Adicione essas duas linhas:

- $cfg['Servers'][$i]['user'] = '';
- $cfg['Servers'][$i]['password'] = '';

Altere o user e password de acordo com as informações que você criou para sua conta MariaDB.

### Perguntas Frequentes

#### O que é Permissão Total?

A permissão total é realizada para permitir que usuários e grupos possam ter acesso a uma pasta específica.

Para fazer importação de SQL é necessário aplicar a permissão total na pasta "tmp" em /var/lib/phpmyadmin/, para que não ocorra o erro "Nenhum dado foi recebido na importação. Ou nenhum nome de arquivo foi enviado, ou o tamanho do arquivo excedeu o tamanho máximo permitido pela sua configuração do PHP. Verifique a FAQ 1.16. phpmyadmin"

Essa permissão total já é aplicada automaticamente durante a instalação.

# Doação

Se você puder ajudar esse projeto financeiramente, vou deixar formas de apoio abaixo.

 - PIX: pixmugomes@gmail.com
 - Asaas: https://www.asaas.com/c/72mxu6ilkis5rwxz

# License

The MGLAMP is provided under:

[SPDX-License-Identifier: MIT](https://spdx.org/licenses/MIT.html)

Licensed under the MIT license.
