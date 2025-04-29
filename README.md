# Script para instalação do Apache2
Inicialmente é preciso crir um arquivo para a criação do _script_. 
Para isso utilizamos o comando:
```
sudo nano script.sh
``` 
Isso permite criar o arquivo e editá-lo diretamente.
## Primeira parte do Script
```
#!/bin/bash
if[!-X /etc/init.d/apache2];then
  echo “Apache não encontrado, iniciando a instalação
sudo apt-get update
sudo apt-get install apache2 -y

else
echo “Você já possui o apache instalado”
fi
```
Esta condicional vai verificar se o Apache está instalado e exibir uma mensagem, caso não esteja instalado, vai instalar automaticamente. Caso já o tenha instalado irá exibir uma mensagem informando.
## Criação de site (colocando o site dentro do script)
```
sudo mkdir -p /var/www/ifrn/public_html
cd /var/www/ifrn/public_html

```
Criação de estrutura para hospedar os arquivos do site
```
sudo git clone https://github.com/matheusmanuel/site-simples-com-html-e-css-.git
```
Fazendo clone do repositório do GitHub que contem o site a ser utilizado
```
sudo cp -r site-simples-com-html-e-css/* .
sudo rm -rf site-simples-com-html-e-css/
```
Move todos os arquivos do repositório para o diretório criado e remove a pasta que foi clonada.
```
cd /etc/apache2/sites-available/
udo tee ifrn.conf<<EOF
<VirtualHost *:80>
	serverAdmin admin@ifrn
ServerName ifrn
ServerAlias  www.ifrn
DocumentRoot /var/www/ifrn/public_html
	Errorlog ${APACHE_LOG_DIR}/error.log
	Customlog ${APACHE_LOG_DIR}acess.log combined
</VirtualHost>
EOF
```
Cria um arquivo de configuração virtual Host e realiza a configuração, como onde está a pasta do site e o nome a ser pesquisado no navegador.
```
sudo a2ensite ifrn.conf
sudo echo “127.0.0.1 		ifrn” | sudo tee -a /etc/hosts
sudo /etc/init.d/apache2 restart
sudo /etc/init.d/apache2 status
```
Ativa o site e adiciona o arquivo ao /etc/hosts.
Reinicia o apache e verifica seu status
## Para executar o Script
```
sudo chmod +x script. sh -> muda as permissões
./script.sh
```
Muda as permissões do arquivo e executa.




