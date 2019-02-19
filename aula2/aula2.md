
#  TP1 - 11/Fev/2019

## 1-Números aleatórios/pseudoaleatórios 


### Pergunta 1.1
Este comandos são geradores de números pseudo-aleatórios, acedem ao ruído do ambiente do sistema operativo recolhido dos controladores de dispositivos e outras fontes.
O <em>/dev/random</em> normalmente bloqueia quando não há entropia suficiente para gerar o tamanho da sequêcia pretendido. 
O <em>/dev/urandom</em> normalmente nunca bloqueia, mesmo se não existir entropia suficiente pois reutiliza a <em>entropy pool</em> para produzir mais bits aleatórios.

No entanto deve ser utilizado o <em>/dev/random</em> sempre que possível, isto é que o desempenho não seja muito demorado, apesar de o /dev/urandom ser criptograficamente seguro. 
  
### Pergunta 1.2
Segundo os links disponibilizados no enunciado, **HAVEGE (HArdware Volatile Entropy Gathering and Expansion)** é um user-level software de gerador de números imprevisíveis aleatórios para vários propósitos. Dezenas de centenas de bits imprevisíveis podem ser gerados pelo sistema operativo, explorando os vários estados do sistema operativo como fonte de entropia. Desta forma, o <em>/dev/random</em> já não bloqueia. 
     
     
### Pergunta 1.3
Analisando o código presente na biblioteca <em>shamirsecret</em>, verifica-se que é na função generateSecret no ficheiro <em>shamirsecret.py</em>, que é especificado como são gerados os segredos (<em>string.ascii_letters + string.digits</em>). 
     
![](imagem1.png)     


     
## 2-Partilha/Divisão de segredo (Secret Sharing/Splitting) 

 
### Pergunta 2.1
    
A  - Para a execução dos programas propostos foi necessário, primeiramente, criar uma chave privada pois esta faz parte dos argumentos do primeiro programa. Assim foi gerada através do comando **openssl genrsa -aes128 -out mykey.pem 1024**. De seguida, é executado o comando **python createSharedSecret-app.py 8 5 1 mykey.pem**. 

Para a verificar se as 5 partes conseguem recuperar o segredo original foi necessário criar um certificado para a chave <em>mykey.pem</em> através do comando **openssl req -key mykey.pem -new -x509 -days 365 -out mykey.crt**. De seguida, foi executado o comando **python recoverSecretFromComponents-app.py 5 1 mykey.crt** e verificou-se: 


![](imagem2.png) 
 
**B** - A diferença entre <em>recoverSecretFromComponents-app.py</em> e <em>recoverSecretFromAllComponents-app.py</em> está nas partes que são necessárias para reconstruir o segredo. O primeiro é usado quando se pretende que o segredo possa ser recuperado com pelo menos quorum utilizadores, não sendo necessário todos as partes nas quais o segredo foi dividido. O segundo deve ser usado apenas quando se pretende que sejam necessárias todas as n partes nas quais o segredo foi dividido para que seja possível recuperá-lo. 

## 3-Authenticated Encryption 

Utilizando **Authenticated Encryption** conseguimos garantir confidencialidade, integridade e autenticidade do segredo e da sua etiqueta(tag), através do método **Encrypt-then-Mac**.

```Python

k = getRandomBytes(16)

def Cifrar(tag, segredo):
    cypher_text = cifra(segredo)
    h = hmac(k, tag+cypher_text)
    cypher = (h,tag,cypher_text)
    
    return cypher
    
def Decifrar(cypher, key):
    tag = cypher[1]
    cypher_text = cypher[2]
    if (cypher[0] == hmac(k, tag+cypher_text))       
        segredo = decifra(cypher_text,key)
        return segredo
    
    return None
```

Foi considerada a etiqueta(tag) como pública, pelo que não é garantida a sua confidencialidade, para o utilizador conseguir ver a mesma antes de decifrar.
A chave secreta <em>k</em> do HMAC foi gerada aleatoriamente e está definada como global para exemplificar. 
A chave de cifra <em>key</em> é identifcada pelo ano.mes.dia.

## 4-Algoritmos e tamanhos de chaves 



### Grupo 10 - Bélgica, para as ECs "Zetes S.A./N.V.", "Portima s.c.r.l. c.v.b.a.";



### **Zetes S.A./N.V.**

Esta entidade certificadora usa o algoritmo **sha256WithRSAEncryption** para assinatura digital e o algoritmo de chave pública **rsaEncryption** com tamanho de 4096 bits. Este tipo de algoritmo com este comprimento de chaves é apenas adequado se considerar-mos um curto prazo.

```
Certificate:
    Data:
        Version: 3 (0x2)
        Serial Number: 4044494821122691399 (0x3820ee9c74ecd147)
    Signature Algorithm: sha256WithRSAEncryption
        Issuer: C=BE, O=ZETES SA (VATBE-0408425626)/serialNumber=001, CN=ZETES TSP ROOT CA 001
        Validity
            Not Before: May 20 17:20:29 2016 GMT
            Not After : May 20 17:20:29 2026 GMT
        Subject: C=BE, O=ZETES SA (VATBE-0408425626)/serialNumber=001, CN=ZETES TSP QUALIFIED CA 001
        Subject Public Key Info:
            Public Key Algorithm: rsaEncryption
                Public-Key: (4096 bit)
                Modulus:
                    00:c3:47:8f:13:ef:9b:b6:4d:6e:62:8b:aa:0e:00:
                    a5:1a:6a:c8:7a:4c:cc:a7:c9:05:7c:3b:19:5a:b0:
                    fb:23:04:02:a4:cb:39:60:9b:fe:2e:21:a4:2c:73:
                    a1:1b:45:3c:45:06:32:f6:b5:b1:cb:7c:04:a4:c8:
                    28:e2:e3:d5:88:13:52:73:f8:0c:d2:38:c2:24:1a:
                    b7:9e:e2:dc:99:75:09:21:aa:8f:98:47:13:7e:4f:
                    1f:5b:02:46:4c:16:76:db:f1:c0:10:32:9d:04:69:
                    78:da:23:73:8a:20:2b:ab:ce:bf:fc:6c:87:94:09:
                    e8:80:86:60:ff:53:09:0a:31:05:7f:45:f2:8d:74:
                    b1:f6:84:df:1f:c4:32:83:5a:28:82:d2:34:d1:68:
                    06:f4:a6:6c:e0:89:38:a6:07:32:10:aa:cc:aa:f0:
                    fc:10:61:cd:5a:1c:0c:c8:67:46:79:7e:2c:04:8e:
                    5c:27:16:a2:da:7a:a9:fb:7f:70:2e:4c:c9:fd:2e:
                    15:e5:92:4d:35:c1:83:03:3b:e3:42:23:91:cf:9c:
                    f1:ff:ed:be:ff:d3:34:c0:f2:1b:37:1b:54:a6:7f:
                    bb:04:ce:da:cf:7b:5f:41:66:0e:20:40:cf:df:f8:
                    48:f2:9c:01:ab:e0:b9:33:5d:88:f4:fd:95:91:0a:
                    9c:91:0f:f7:dd:13:92:bf:57:34:23:88:19:49:42:
                    b1:89:33:3b:22:bc:4b:a3:d6:ef:26:2f:2c:ff:d0:
                    3d:56:d1:a6:ab:16:c4:b9:8b:38:59:db:84:12:14:
                    17:fa:18:53:06:8a:50:d0:4a:f3:8b:da:65:4c:ca:
                    6f:e7:c2:23:7c:c0:9c:f8:35:28:2e:76:82:ba:f9:
                    1b:eb:07:54:9c:a5:5f:6d:9b:0a:e2:b4:c0:a0:82:
                    f4:2b:68:9d:4c:47:fd:3c:03:f7:f4:5f:54:12:5b:
                    0b:b4:07:83:1d:1e:5e:46:c5:b0:ed:15:5a:ae:8a:
                    7c:0e:bc:7d:70:c3:9a:5e:a2:b2:bd:42:72:01:d6:
                    0b:04:78:b6:52:b8:2f:28:a1:55:69:fe:ec:ea:5a:
                    d1:6e:aa:fa:3c:c9:cf:e1:f9:e2:3c:6c:67:ae:7c:
                    55:97:80:94:77:0b:4d:84:7e:e8:76:53:3a:51:7e:
                    79:97:38:a4:3e:29:71:f6:31:85:62:b9:62:4e:ae:
                    52:62:04:21:83:42:28:57:1e:51:89:f6:4f:a4:28:
                    7a:80:5d:4e:e0:32:72:08:60:3a:5e:54:e7:39:8a:
                    0a:3d:68:3f:8a:1e:d6:a9:f8:58:e7:49:c5:bf:06:
                    ab:d1:eb:00:e5:15:2a:1d:f1:78:1a:01:6b:a9:c0:
                    ba:d7:5f
                Exponent: 65537 (0x10001)
        X509v3 extensions:
            Authority Information Access: 
                CA Issuers - URI:http://crt.tsp.zetes.com/ZETESTSPROOTCA001.crt
                OCSP - URI:http://ocsp.tsp.zetes.com

            X509v3 Subject Key Identifier: 
                E2:B4:DB:5F:6A:0F:02:50:54:D5:1D:EF:D2:76:72:72:21:95:46:2B
            X509v3 Basic Constraints: critical
                CA:TRUE, pathlen:0
            X509v3 Authority Key Identifier: 
                keyid:38:BC:5C:30:54:DC:E2:BB:20:EF:EE:6F:41:A0:31:6E:5C:FD:8B:75

            X509v3 Certificate Policies: 
                Policy: X509v3 Any Policy
                  CPS: https://repository.tsp.zetes.com
                  User Notice:
                    Explicit Text: ZETES TSP CPS for NCP+ and QCP+ certificates

            X509v3 CRL Distribution Points: 

                Full Name:
                  URI:http://crl.tsp.zetes.com/ZETESTSPROOTCA001.crl

            X509v3 Key Usage: critical
                Certificate Sign, CRL Sign
    Signature Algorithm: sha256WithRSAEncryption
         a8:7c:4d:53:16:d5:f8:35:e4:4f:f2:02:a7:b6:1c:bc:df:47:
         85:b2:54:ac:53:8b:9a:d1:2d:35:f3:70:56:75:2f:8b:ce:eb:
         40:9b:34:00:ef:ed:a9:62:95:90:9a:c5:90:a3:1a:5c:04:7a:
         3c:53:6c:9e:87:e4:70:2b:36:64:d8:52:05:9c:e5:10:79:7a:
         ec:b6:ad:a4:00:60:f9:b8:f3:f0:1b:f4:cd:51:aa:80:13:b1:
         66:2a:2b:27:90:df:d1:60:7f:d9:d0:0e:ed:a8:40:7a:52:4b:
         5f:3c:a3:be:16:04:a8:90:1e:50:50:ea:b7:c1:8e:cc:c5:12:
         d7:a6:12:0b:65:38:b2:3b:ae:75:7f:18:27:c8:86:ad:2b:1d:
         50:5d:c6:10:11:79:5f:3f:52:c2:8b:f7:26:e2:44:94:f5:66:
         46:ee:b6:f6:6f:1c:ce:28:e5:df:86:e4:71:fc:ac:78:a0:fb:
         45:f8:aa:ee:f6:fb:04:8d:59:c8:6e:98:ad:d4:3f:ce:33:3c:
         bf:98:26:fa:60:71:f7:f3:a6:64:b7:8d:c1:c5:04:e2:b0:6b:
         80:d7:3d:dd:7c:79:67:f0:10:db:f5:c4:f4:27:ce:dc:ad:4b:
         44:f3:83:c4:99:a6:0b:a7:04:9b:b8:9e:8a:c0:da:32:86:80:
         f7:84:e9:5d:51:ac:7f:57:d1:95:a3:94:a1:66:b6:90:a7:45:
         71:a3:fa:a9:09:68:55:53:12:81:0e:d3:99:2a:2a:9e:56:47:
         5b:7d:bf:4a:b9:2c:9d:9d:ed:0a:71:69:b8:45:62:50:e8:72:
         6c:72:31:8f:45:68:d2:bd:5a:84:ad:ec:cb:2f:cf:21:a1:89:
         4b:7c:1b:b9:e6:07:b8:33:d5:df:20:8f:78:56:3e:9a:d7:fc:
         8e:1d:8a:50:09:aa:82:a6:a9:b4:86:c4:3a:af:98:af:3b:5d:
         e9:ae:46:aa:19:60:2c:96:a8:67:a5:f7:b9:2e:c3:e6:45:a0:
         8b:bd:ed:70:73:a4:e6:5d:b8:ff:04:a7:a2:d6:93:5b:82:11:
         a9:94:03:66:62:f9:18:1c:f5:be:f8:04:2a:e0:e1:82:e6:0e:
         fd:6c:08:45:c5:6b:7c:37:e9:10:7a:92:5a:3c:13:62:3f:78:
         b3:5a:85:1e:2e:45:3a:58:86:c2:b2:b8:4b:6c:64:e3:f5:fb:
         4d:91:66:82:db:5f:b1:e6:64:1c:2b:6e:f0:3c:24:ca:74:49:
         99:24:b3:7c:e1:4b:f0:c8:ca:60:22:8a:83:c4:3d:c4:3d:a8:
         cc:9b:c2:4a:96:8d:b6:e2:d1:81:e6:48:37:e2:b4:78:d6:c1:
         d5:d8:ec:db:28:0d:6a:3b

```

### **Portima s.c.r.l. c.v.b.a.**

O último certificado concedido por esta EC foi o **PortiSighn Users CA11** e utiliza o algoritmo **sha512WithRSAEncryption** para assinatura digital e o algoritmo de chave pública **rsaEncryption** com tamanho de 4096 bits. Este tipo de algoritmo com este comprimento de chaves é apenas adequado se considerar-mos um curto prazo.

```
Certificate:
    Data:
        Version: 3 (0x2)
        Serial Number: 10019 (0x2723)
    Signature Algorithm: sha512WithRSAEncryption
        Issuer: telephoneNumber=0032 2 6614411/emailAddress=security@portima.com, C=BE, L=B-1170 Brussels, ST=Brussels/street=Terhulpsesteenweg 150 Chauss\xC3\xA9e de la Hulpe, OU=Security, O=Portima s.c.r.l. c.v.b.a., CN=PortiSign Root CA
        Validity
            Not Before: Jun 16 07:00:00 2017 GMT
            Not After : Jun 16 07:00:00 2027 GMT
        Subject: C=BE, O=Portima s.c.r.l. c.v.b.a., CN=PortiSign Users CA11 for Qualified Certificates
        Subject Public Key Info:
            Public Key Algorithm: rsaEncryption
                Public-Key: (4096 bit)
                Modulus:
                    00:d0:43:09:38:2e:24:cf:ae:9d:a4:08:85:3f:09:
                    b8:a2:92:3e:3b:5d:69:b4:a7:28:d7:1f:88:2d:85:
                    b1:4f:11:2a:dc:8a:d3:de:81:ff:d1:b5:02:8b:5f:
                    b5:9b:46:f6:80:78:fe:7a:69:81:de:57:0d:6d:ff:
                    5d:95:70:f2:58:b6:ea:ab:80:97:b5:64:70:95:2c:
                    b9:92:f0:91:75:34:78:9d:c7:68:4b:56:8b:b4:c6:
                    19:52:42:f8:a6:c7:4b:92:ab:42:da:65:6f:62:0c:
                    25:3b:0f:66:a0:28:9e:01:fe:53:de:09:c9:69:5e:
                    b5:83:10:fd:34:c5:b6:04:b1:96:be:9e:d9:dd:f8:
                    3d:15:8b:92:3c:fe:80:8f:16:20:3a:67:71:51:81:
                    86:e8:43:bf:c5:41:79:0c:ea:f2:70:fc:c9:13:42:
                    a3:2b:e1:83:ac:f9:72:cf:75:48:c1:6e:5c:84:71:
                    31:a8:27:88:ca:96:93:d8:29:23:2a:75:b0:ba:34:
                    18:4c:7f:05:a6:7e:3a:2f:99:62:a1:b7:0f:33:a7:
                    80:e8:32:15:4f:65:55:1c:a3:40:31:44:d2:53:76:
                    8c:f8:06:03:a2:7f:72:22:3b:ba:51:b4:ac:5a:70:
                    5f:03:52:d3:c8:8c:37:e7:bc:97:d2:f5:c8:81:4c:
                    e0:55:37:fa:a6:30:4e:cc:82:25:7b:39:a3:c3:40:
                    e5:42:08:c1:d5:be:a5:46:af:e4:6e:33:cf:a9:de:
                    52:b9:f9:cd:eb:ca:71:c8:c9:cd:a3:84:75:db:af:
                    86:60:ac:2e:69:2a:7b:b4:4e:4d:d6:90:f6:3a:13:
                    b5:f8:83:c1:87:c5:0a:f0:a6:20:a9:f1:94:25:ab:
                    25:14:5e:58:45:b3:19:61:bc:69:f2:69:cf:98:08:
                    d4:cb:bb:53:a6:15:d1:99:19:f3:90:33:ef:12:9a:
                    50:7a:e8:a3:9b:c3:bf:64:49:58:50:39:ff:6d:6c:
                    49:28:02:74:84:ac:44:68:f5:db:87:03:72:80:05:
                    45:03:cd:ae:7b:c2:0a:a2:e8:56:59:ea:90:ff:69:
                    57:80:b6:c0:46:9e:38:9b:9f:5d:95:23:51:06:fc:
                    84:66:ec:9c:a3:ec:e4:0a:70:2e:67:b3:83:30:bc:
                    ef:f3:f7:e3:74:5a:ad:cc:10:29:21:ff:eb:12:cd:
                    47:af:aa:2e:9c:2e:12:b8:d5:1f:f8:86:43:e9:01:
                    46:c9:c4:4a:20:bc:3f:55:65:b6:20:c4:7e:34:92:
                    03:a9:42:fc:de:af:b7:c8:27:9f:f9:0d:a5:5b:a7:
                    74:ef:cc:1a:4a:a8:44:c1:0d:0b:4d:ee:31:b5:46:
                    03:a2:91
                Exponent: 65537 (0x10001)
        X509v3 extensions:
            X509v3 Basic Constraints: critical
                CA:TRUE
            X509v3 Subject Key Identifier: 
                46:0A:BB:F7:BD:E3:4E:95
            X509v3 Certificate Policies: 
                Policy: X509v3 Any Policy

            X509v3 Authority Key Identifier: 
                keyid:4F:E2:BE:32:70:47:B2:B3

            X509v3 Key Usage: 
                Certificate Sign, CRL Sign
            X509v3 CRL Distribution Points: 

                Full Name:
                  URI:http://crl.portisign.be/crl/root.crl

    Signature Algorithm: sha512WithRSAEncryption
         4e:3d:99:d8:2d:8e:d9:f0:ff:c9:6a:bc:8a:1e:6a:a0:da:c9:
         13:d5:b7:4e:f4:65:57:ec:a6:f6:16:ce:65:71:49:30:db:bc:
         f7:82:83:f1:6c:cd:6b:ad:42:a0:3d:d3:19:8a:28:65:a2:64:
         fe:32:8d:01:dc:4a:4e:43:28:ea:d1:db:b2:40:a6:b2:c6:dd:
         99:b5:7f:37:ec:66:0e:eb:04:6f:9c:bd:ee:6a:7e:79:31:bf:
         83:86:3f:97:38:ef:12:81:23:63:d0:2d:6a:b1:e5:4d:9c:65:
         70:d0:8b:23:b7:6c:bf:50:73:46:a3:f1:1f:82:f2:18:4e:73:
         3b:9f:77:86:e9:19:6f:f4:e2:fb:d1:40:bb:71:2d:6a:d7:9b:
         7b:05:e9:6e:2a:3f:60:93:a9:30:56:7c:cb:95:8c:1f:18:0e:
         00:f3:61:b3:79:f1:df:cf:2a:c4:af:24:2b:c8:a2:17:2c:bb:
         38:61:d6:6a:51:d5:dd:58:8f:b6:a1:65:fd:73:51:88:c3:d4:
         9b:1a:c0:ec:af:da:84:62:23:b2:33:1b:23:b6:14:38:ee:de:
         f1:cf:93:d2:8f:db:0f:b6:fd:66:8b:72:7f:ef:be:1f:6a:89:
         1f:a4:ca:e4:5d:fc:70:25:1e:c2:98:f6:8d:dc:99:18:d8:b7:
         39:a1:e1:6e:3c:97:62:19:ec:35:a1:2f:44:07:11:cc:bc:d2:
         44:ac:b6:68:91:41:5b:19:45:ca:ec:92:eb:13:96:29:55:3c:
         2d:02:e9:d2:f1:3d:cd:d5:7f:af:5a:06:f7:41:ee:d7:b9:33:
         bf:38:04:a3:7a:19:0b:ed:4d:b5:c6:55:19:60:16:68:43:89:
         8e:3a:e0:d8:fb:96:e3:d1:b8:22:30:1a:ff:d9:ce:20:9a:ed:
         6a:65:da:86:9d:6c:74:d7:16:2a:e4:ec:52:2e:71:c1:c0:27:
         7b:92:2c:1c:0e:1c:ba:68:67:d1:8b:af:16:c3:e1:28:8f:48:
         d8:fa:1e:a4:23:d0:81:92:0d:f1:f0:8b:d9:20:c6:25:b8:19:
         a2:9d:59:60:d0:ef:a2:bb:2c:b4:a1:f7:d0:0a:d0:0d:2d:a9:
         a7:a0:9e:a2:1c:41:1f:9d:48:7d:0f:43:a4:fa:ea:dd:41:32:
         c4:c1:30:09:c3:f5:70:9e:fa:43:f5:c6:a0:13:97:3c:08:45:
         23:4c:68:58:38:5e:d1:e6:3d:ca:8e:24:0f:3f:4c:35:b7:98:
         2a:79:34:32:72:d3:04:8d:f5:2c:bb:ad:01:b8:c1:ad:fe:07:
         19:e2:a0:30:d9:e9:5e:d8:d9:83:c7:5b:6e:dd:8f:54:49:be:
         9e:49:1a:b8:dc:9c:e2:76

```

