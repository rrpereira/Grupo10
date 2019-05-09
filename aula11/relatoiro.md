# TP - 29/Abr/2019

## 1. Buffer Overflow

### Experi�ncia 1.1
Em rela��o ao segmento de dados, verifica-se que o *size4* possui mais 4 bytes em rela��o ao *size1* e o *size5* mais 4 bytes em rela��o ao *size4*. Isto deve-se ao facto de no *size4* existe uma vari�vel static int inicializada, que corresponde a mais 4 bytes de data. No *size5* a vari�vel global int tamb�m inicializada, correspondendo a um acr�scimo de 4 bytes no segmento data.

No segmento de text, as instru��es s�o as mesmas em todos os programas, logo os valores s�o os esperados.

No segmento de bss, as diferen�as entre *size1*, *size2* e *size3* n�o s�o as esperdas, pois era de esperar que no *size2* o bss tivesse alocado mais 4 bytes relativamente ao *size1* e no *size3* mais 4 bytes que o bss do *size2*. No entanto, estes factos podem ser otimiza��es feitas pelo compilador.

![Exp1.1](e11.png)

### Experi�ncia 1.3
No caso do programa em *C++*, este entra em loop pois n�o s�o verificados os limites do array. Quando o programa escreve fora do limite do array, est� a escrever na vari�vel i, fazendo com que esta seja mudada para o valor 7.

No caso dos programas em *Java* e *Python*, os programas terminam com uma exce��o porque se tenta aceder a um �ndice inv�lido do array.

### Pergunta 1.1
Os programas *Java* e *Python* terminam com um erro se introduzir um n�mero de elementos superior ao tamanho com que o array foi inicializado (10).

No caso do programa em *C++*, o programa entra em loop quando escrevemos al�m do limite do array, ou seja vai ser escrito na vari�vel i, e assim continua a ter chegar ao valor introduzido como tamanho do array.

### Pergunta 1.2
Nos programas *Java* e *Python*, se o n�mero de valores a guardar no array for igual ou inferior ao tamanho do array, o programa corre sem problemas. Caso se pretenda guardar mais elementos no array do que o tamanho do mesmo, o programa termina com uma exce��o.

No programa *C++*, se o n�mero de valores a guardar no array for igual ou inferior ao tamanho do array, o programa corre sem problemas. Caso seja inserido um valor entre 10 e 19, o programa entra em loop, porque quando o valor de *i* ultrapassa o tamanho m�ximo do array, ent�o ele escrever� na posi��o da vari�vel *i*, continuando a escrever dentro dos limites do array.
Caso o valor seja superior a 19, o programa tem dois comportamentos:
- Por vezes, termina em segmentation fault, isto porque se escreveu no endere�o de retorno;
- Outra vezes, caso sejam pedidos resultados que estivesse num indice inferior ou igual a 9, o resultado estaria certo mas caso fosse superior, a resposta conteria valores errados dado que o ciclo terminou antes destes valores serem calculados.

### Pergunta 1.3
No ficheiro *RootExploit.c* a vulnerabilidade de buffer overflow existe porque a fun��o gets n�o valida o tamanho do input. Logo � poss�vel escrever na vari�vel *pass* caso seja inserido um input com tamanho superior a 4 e assim, dando a mensagem "Foram-lhe atribuidas permiss�es de root/admin". 

No ficheiro *0-simple.c* a vulnerabilidade que existe � a mesma que no ficheiro anterior. No entanto para ser explorada � necess�rio que o input seja maior por uma unidade do que o tamanho do buffer. Isto porque � preciso que seja escrito na atribui��o da vari�vel *control*. No entanto, existe casos em que n�o foi poss�vel conseguir a mensagem "YOU WIN" devido ao alinhamento de mem�ria for�ado pelo compilador. 

![Perg1.3](p13.png)

### Experi�ncia 1.5
Na fun��o segura, o output da fun��o printf � formatado pela string *%s* sendo que qualquer sequ�ncia de formata��o no input ("%s", "%d", "%i, etc) vai ser lida de forma literal.

Na fun��o vulner�vel, a string passada � fun��o *printf* � diretamente aquela que � lida e caso esta contenha alguma sequ�ncia de formata��o, esta vai ser substitu�da por um valor indeterminado, como podemos observar na figura seguinte.

![Exp1.5](e5.png)

### Pergunta 1.4
No programa *ReadOverflow.c* podemos observar que a leitura das strings est� protegida por invoca��es da fun��o *fgets*, o n�mero de bytes no output � apenas limitado pelo n�mero dado como resposta � primeira pergunta do programa. Assim, � poss�vel obter o conte�do de outras posi��es da mem�ria. 

![Perg1.4](p14.png)

### Pergunta 1.5
Para conseguir a mensagem 'Congratulations, you win!!!', o programa foi testado em tentativa erro para determinar quantos bytes tem de ter o input para come�ar a alterar o valor da vari�vel. De seguida, dado que se pretende obter o valor 0x61626364, ou seja abcd em *ASCII*, temos de inserir uma string qualquer de 78 bytes como input, concatenada com a string dcba, devido � disposi��o em little-endian. Podemos observar na figura seguinte um exemplo:

![Perg1.5](p15.png)

### Experi�ncia 1.8
Inicialmente, compilou-se o programa com a flag *-g* para podermos analisar os endere�os das vari�veis do programa. De seguida, verificou-se que a fun��o *win* est� no endere�o 0x555555554740 e converteu-se o endere�o da fun��o para ASCII (UUUUGD). De seguida, verificou-se que a vari�vel *fp* � alterada a partir do byte 73. Sendo assim, foi concatenada uma string com 73 bytes e o endere�o da fun��o *win* em *little endian* (DGUUUU). O resultado pode ser observado na figura seguinte:

![Exp1.8](e18.png)

### Experi�ncia 1.9

![Exp1.9](e19.png)

## 2. Vulnerabilidade de inteiros

### Experi�ncia 2.1
![Exp2.1](e21.png)
### Experi�ncia 2.2
![Exp2.2](e22.png)

Se for necess�rio inteiros maiores pode-se utilizar a classe *BigInteger*, que permite representar inteiros com precis�o arbitr�ria.

### Experi�ncia 2.3
![Exp2.3](e23.png)

- O valor � truncado para o tamanho da vari�vel de destino, mantendo os bytes menos significativos.

- Verifica se o valor lido se encontra dentro do intervalo de valores suportado pelo tipo onde vai ser armazenado lan�ando uma exce��o caso tal n�o se verifique.

### Pergunta 2.1
![Perg2.1](p21.png)

Ao analisar o c�digo do programa, vemos que os valores de x e y s�o do tipo *size_t*, ou seja  correspondem a um inteiro unsigned. Logo se for chamada a fun��o com valores de x ou y cujo produto exceda o limite superior deste tipo, pode ocorrer que o valor da multiplica��o de x e y seja inferior ao valor real.

Quando � executado o c�digo, d� segmentation fault porque n�o � poss�vel alocar a quantidade de mem�ria pretendida.

### Pergunta 2.2
![Perg2.2](p22.png)

A vulnerabilidade existente deve-se ao facto de n�o ser verificado o limite inferior da vari�vel *tamanho*.

Se for passado como argumento *tamanho* o valor 0 � fun��o vulner�vel, como na vari�vel *size_t* tamanho_real vai ser armazenado o valor tamanho-1, ou seja -1. Mas como a vari�vel n�o suporta valores negativos vai ser armazenado um valor muito grande, no qual n�o � poss�vel fazer o malloc.

Sendo assim, quando executamos o programa este d� segmentation fault porque n�o e poss�vel alocar a quantidade de mem�ria pretendida.

### Experi�ncia 2.4
![Exp2.4](e24.png)

A vulnerabilidade existente resulta da convers�o de valores de vari�veis entre tipos signed (int) e unsigned (size_t). 

Caso se passe no argumento *tamanho* um valor que exceda o limite superior de um int, na instru��o tamanho_real = tamanho - 1 a vari�vel *tamanho_real* passa a armazenar uma valor negativo, devido ao cast para um tipo signed. No entanto, quando se passa o *tamanho_real* como argumento da fun��o malloc ele � convertido para *size_t* e passa a representar um valor positivo, superior ao do limite superior do tipo int.

Quando � executado o c�digo, d� segmentation fault porque n�o � poss�vel alocar a quantidade de mem�ria pretendida.

