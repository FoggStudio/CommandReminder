# SMTP Server

## TLS connection
```
openssl s_client -starttls smtp -crlf <IP>:<port>
EHLO <domain name>
STARTTLS
EHLO <domain name>
```

## Actions
```
MAIL FROM:<<mail>>
RCPT TO:<<mail>>
DATA (You could write evrythings in the content of the mail and end it with a dot on a single line)
```