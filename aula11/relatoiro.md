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

No caso do programa em *C++*, 


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

### Experi�ncia 1.9


