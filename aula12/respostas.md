# Aula TP - 06/Mai/2019

## 1. Injection
#### Pergunta 1.1 - String SQL Injection
Utilização normal, com a intrudução do apelido "Smith":
![](1.png)
Resultado de SQL injection:
![](2.png)

#### Pergunta 1.2 - Numeric SQL Injection
Neste caso não é possivel inserir input escolhido por nós, só é possivel escolher um de várias opções predefenidas.
Porém, atravéz da ferramenta "inspecionar elemento", do browser, é possivel observar o htlm da página. Alterando o "value", na opção Columbia ou em qualquer outra, para uma tautologia, é mostrado todas as opções que exisem, as visiveis e as não visiveis.
![](3.png)
![](4.png)

#### Pergunta 1.3 - Database Backdoors
Utilização normal, com a intrudução do UserID 101.
![](5.png)
Depois de intruduzir o seguinte intput: 101'; UPDATE employee SET salary = '1000000', o salário é alterado.
![](6.png)



## 2. XSS
#### Pergunta 2.1 - Reflected XSS
Depois de fazer alguns testes e intruduzir varios inputs nos vários campos, detetamos que o campo dos 3 digitos não tem qualquer mecanismo de segurança. Intrudizindo o seguinte script: "<script> alert("SSA!!!")</script>" produz o efeito na imagem seguinte.
![](7.png)


## 3. Quebra na Autenticação
### Pergunta 3.1 - Forgot Password
Neste exemplo foi intruduzido o username "webgoat" e cor "red" para recuperar a password.
![](8.png)
Para descobrir a password do username admin, foram testadas várias cores, sendo que a cor correta á a "green" após poucas tentativas. Este método de recuperar passwords é muito pouco seguro, porque é fácil advinhar a cor certa.
![](9.png)
