# Criado um servidor de e-mail 🖥️

## Prática 🥼

## Objetivo

- Criar um servidor de e-mail para envio (local e remoto)

### Diagrama do fluxo ✅

![cenário](https://github.com/user-attachments/assets/edbde7bc-bbc1-4a89-b8ce-6077e267ff0e)

Realizado:

![postfix](https://github.com/user-attachments/assets/fd9d9d53-429d-4b5f-8730-dba4120059ee)



# Execução 🚀

### Configuração do Servidor SMTP (Postfix)
1. **Instalação**: 
   - Comando: `sudo apt-get install postfix`
   - Teste de funcionamento: `telnet localhost 25`

2. **Configuração**:
   - Editar o arquivo de configuração: `nano /etc/postfix/main.cf`
   - Parâmetros importantes:
     - `$myhostname`: Nome do host do servidor.
     - `$mydomain`: Domínio do servidor.
     - `home_mailbox = Maildir/`: Diretório para armazenamento de e-mails.
     - `resolve_numeric_domain = yes`: Permitir envio de e-mails usando IP.

3. **Características**:
   - Permite notificações de novos e-mails (geralmente desabilitadas por questões de performance).
   - Restrições de acesso para controle de retransmissão de e-mails.

### Configuração do Servidor IMAP (Dovecot)
1. **Instalação**:
   - Comando: `sudo apt-get install dovecot-core dovecot-imapd`

2. **Configuração**:
   - Editar o arquivo: `nano /etc/dovecot/dovecot.conf`
     - Descomentar a linha: `listen = *, ::`
   - Alterar configurações em:
     - `10-auth.conf`: 
       - `disable_plaintext_auth = no`
       - `auth_mechanisms = plain login`
     - `10-mail.conf`: 
       - `mail_location = maildir:~/Maildir`
     - `10-master.conf`: 
       - Configurar `unix_listener` para integração com Postfix.

### Instalação do Cliente de E-mail (Thunderbird)
- Comando: `sudo apt-get install thunderbird`

### Referências
- Links para documentação e guias sobre Postfix e Dovecot.

https://tools.ietf.org/html/rfc3501

http://www.postfix.org/postconf.5.html

https://tools.ietf.org/html/rfc6851

https://www.tecmint.com/install-postfix-mail-server-with-webmail-in-debian/

https://serverfault.com/questions/373350/postfix-allow-sending-to-raw-ip-address

https://www.dovecot.org/
