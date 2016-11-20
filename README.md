# whatsapp-iptables-allow
Tutorial liberando serviços do Whatsapp em sua rede com o Iptables

Primeiro de tudo você precisará  liberar tráfego na saída xmpp.
Para isso iremos utilizar o seguinte comando no terminal, o mesmo irá atribuir a regra ao Iptables:

#Nota: Para evitar erros, execute todos os comandos na raiz principal do sistema, caso esteja com dúvidas, digite o seguinte comando:

cd ~

Agora já pode executar os comandos normalmente.

#/------------ LIBERAR TRÁFEGO NA SAÍDA XMPP------------/

iptables -A FORWARD -p tcp --dport xmpp-client -j ACCEPT


Agora precisaremos abrir algumas portas para que o serviço de voz possa operar normalmente:

TCP: 4244,5222,5223,5228,5242 
TCP / UDP: 59234, 50318 
UDP: 3478,45395

Comandos a serem atribuídos a regra do Firewall:

#/------------ LIBERAR PORTAS TCPs ------------/

iptables -A FORWARD -p tcp --dport 4244 -j ACCEPT # WhatsApp

iptables -A FORWARD -p tcp --dport 5222 -j ACCEPT # WhatsApp

iptables -A FORWARD -p tcp --dport 5223 -j ACCEPT # WhatsApp

iptables -A FORWARD -p tcp --dport 5228 -j ACCEPT # WhatsApp

iptables -A FORWARD -p tcp --dport 5242 -j ACCEPT # WhatsApp

#/------------ LIBERAR PORTAS TCPs e UDPs -----------/

iptables -A FORWARD -p tcp --dport 59234 -j ACCEPT # WhatsApp

iptables -A FORWARD -p tcp --dport 50318 -j ACCEPT # WhatsApp

iptables -A FORWARD -p udp --dport 59234 -j ACCEPT # WhatsApp

iptables -A FORWARD -p udp --dport 50318 -j ACCEPT # WhatsApp

#/------------ LIBERAR PORTS UDPs ------------/

iptables -A FORWARD -p udp --dport 3478 -j ACCEPT # WhatsApp

iptables -A FORWARD -p udp --dport 45395 -j ACCEPT # WhatsApp


Pronto! Já liberamos todas as portas necessárias. O Próximo passo será liberar as cidrs(ips) do whatsapp em nosso firewall(iptables) e atribui-los a porta 443

Para isso iremos rodar o seguinte script:

http://pastebin.com/raw/EsE1XZ80

Execute cada uma dessas linhas em seu terminal

#/----------- ADICIONANDO E EXECUTANDO O SCRIPT NA VPS ------------/

# Baixe o script com o comando: 
wget http://pastebin.com/raw/EsE1XZ80 -O Whatsapp.sh 
# Converta o final das linhas para Unix com o comando: 
dos2unix Whatsapp.sh  
# Torne o script executável: 
chmod +x Whatsapp.sh  
Execute com: 
./Whatsapp.sh

#Importante: Caso dê alguns erros após executar o script, não se preocupe, pois o erro é referente ao sistema IPV6 não existir na sua máquina.

Estamos quase lá!

Após ter feito todos os procedimentos acima descritos, é hora de testar.

Para isso ative a opção Encaminhamento UDP e inicie a conexão com as informações da sua VPS

Use o HTTP Injector 
