## Pergunta 1.1
### RGPD - Artigo 25º - Proteção de dados desde a conceção e por defeito

O artigo analisado pode influir no desenvolvimento do *software* pois é necessário proteger os dados relacionados com as pessoas, pelo que é necessário uma aplicação das medidas técnicas e organizativas adequadas, destinadas a aplicar com eficácia os princípios da proteção de dados, tais como a **minimização**, e incluir as garantias necessárias no tratamento dos dados.

Estas medidas aplicadas, como por exemplo a **pseudonimização** - que é um processo que pode ser utilizado para disfarçar a identidade do titular dos dados mantendo a rastreabilidade dos dados, são feitas de forma a que o tratamento cumpra os requisitos do presente regulamento e proteja os direitos dos titulares dos dados.

Os *softwares* devem estar cientes dos critérios de privacidade de forma a que a aplicação destas medidas têm de ser realizadas pelo responsável pelo tratamento, tanto no momento de definição dos meios de tratamento como no momento do próprio tratamento, este tem de ter em conta as técnicas mais avançadas, os custos da sua aplicação, assim como o contexto e as finalidades do tratamento dos dados.

O desenvolvimento de *software* ainda pode ser condicionado pela necessidade de assegurar que o responsável pelo tratamento aplica medidas técnicas e organizativas para assegurar que, **por defeito**, apenas sejam tratados os dados pessoais que forem necessários para cada finalidade específica.
Estas medidas asseguram que, **por defeito**, os dados pessoais não sejam disponibilizados sem intervenção humana.
Isto é uma obrigação à qual o responsável pelo tratamento deve ter muita atenção e deve ser aplicado à quantidade de dados pessoais recolhidos, ao prazo de conservação dos dados e à sua acessibilidade. 

É ainda necessário garantir que, com todas estas medidas aplicadas, o *software* consiga cumprir todas as obrigações definidas nos pontos anteriores. Sendo ainda este procedimento de certificação aprovado nos termos do artigo 42º. 

## Pergunta 1.2
#### Boas práticas para proteção de dados por padrão

##### Quantidade mínima de dados pessoais 

A prática mais óbvia no que diz respeito à minimização de dados, é quanto menos dados, melhor. Outra boa prática é a coleção granular de dados com base na necessidade. Por exemplo, num cenário de comércio eletrónico, quando um utilizador navega numa loja on-line decide primeiro que itens irá comprar e, somente mais tarde, serão solicitados o nome e o endereço de entrega. A minimização de dados pode, em vários casos, ser atingida com o uso de tecnologias de segurança e aprimoramento da privacidade. Utilizando o cenário de e-commerce anterior, argumenta-se frequentemente que a data de nascimento seria necessária em caso de restrições de idade para a compra de algumas mercadorias, por ex. bebidas alcoólicas. Neste caso, as informações referentes à idade não exigem a data exata de nascimento nem o ano de nascimento, apenas é necessário saber se tem mais de 18 anos ou não. Atualmente existe uma multiplicidade de tecnologias de reforço da privacidade que podem ser utilizadas para minimizar a recolha de dados e / ou reduzir a capacidade de identificação dos utilizadores. O requisito de minimizar a quantidade de dados pessoais por padrão também abrange a redução, tanto quanto possível, de cópias temporárias ou transferência de dados relativamente à finalidade.

##### Extensão mínima do processamento dos dados pessoais

O processamento abrange vários tipos possíveis de operações ou conjunto de operações. O requisito de "extensão mínima" não significa reduzir o número de operações, mas minimizar o risco dos direitos e liberdades das pessoas singulares. Por exemplo, o processamento dos dados apenas na memória principal, em vez de em um dispositivo de armazenamento, se fosse necessário para o propósito. 

##### Período mínimo de armazenamento dos dados pessoais

Para os dados pessoais, o período de armazenamento deve ser minimizado. Às vezes, o armazenamento permanente não é necessário para o propósito. Não abrange apenas as bases de dados, mas também abrange cópias temporárias ou dados pessoais em entradas de log.

##### Acessibilidade mínima dos dados pessoais

A exigência de acessibilidade mínima está claramente relacionada à política de acesso e controle de acesso. Isto é alcançável por separação de dados por finalidade, por ex. em diferentes locais, servidores ou bases de dados. Além disso, as diferentes formas possíveis de compartilhamento de dados devem ser avaliadas e, sempre que possível, minimizadas pelo controlador. A acessibilidade aumenta se dados pessoais forem copiados, transferidos para outros destinatários, disponibilizados a amigos selecionados, publicados ou fornecidos a rastreadores de mecanismos de pesquisa ou outras máquinas que possam processar os dados pessoais.


## Pergunta 1.3
**1.** 
Os nove critérios que devem ser considerados para avaliação são:
- **Evaluation or Scoring** - incluindo definição de perfil e previsão de dados recolhidos.

- **Automated-decision making with legal or similar significant effect** - Processo que visa tomar decisões sobre os titulares de dados produzindo "efeitos legais sobre a pessoa" ou que "afetam de maneira parecida a pessoa".
- **Systematic monitoring** - Processo utilizado para observar, monitorizar ou controlar os dados das pessoas, incluindo dados recolhidos através de redes de monotorização. Este tipo de monitorização é um critério pois os dados pessoais podem ser recolhidos em circunstâncias em que os titulares desses dados podem não ter conhecimento de quem está a recolher os dados e a utiliza-los. Além disso, pode ser impossível para uma pessoas evitar tal processamento em espaços públicos (ou de acesso público).
- **Sensitive data or data of a highly personal nature** - isto inclui categorias especiais de dados pessoais, assim como dados pessoais relativos a condenações ou infracções penais.
- **Data processed on a large scale** - O GDPR não define o que constitui grande escala, embora o *recital 91* forneça algumas ilações. Em todo o caso, o *WP29* recomenda que sejam considerados alguns fatores ao determinar se o processamento é realizado em grande escala.
- **Matching or combining datasets** - Provenientes de duas ou mais operações de processamento de dados realizadas para finalidades diferentes e/ou por diferentes controladores, de modo a exceder as expectativas razoáveis do titular dos dados.
- **Data concerning vulnerable data subjects** - Este tipo de processamento de dados é consideredo um critério pois as pessoas podem ser incapazes de consentir ou opor-se facilmente ao processamento dos seus dados ou exercer os seus direitos, isto devido ao aumento do desequilíbrio de poder entre os titulares de dados e o controlador de dados.
- **Innovative use or applying new technological or organisational solutions** - O uso de tais tecnologias pode envolver novas formas de recolher e usar os dados, possivelmente com alto risco para os direitos e liberdades dos indivíduos. Um exemplo, de tais tecnologias, é a combinação da impressão digital e do reconhecimento da face.
- **Prevents data subjects from exercising a right or using a service or a contract** - São incluidas operações de processamento que visam permitir, modificar ou recusar o acesso de um utilizador a um serviço.

**2.** 
O nosso projeto é um site de venda de artigos de vestuário. Assim, o tipo de processamento que será feito é o de dados pessoais dos utilizadores, assim como os seus *usernames* e *passwords*, dados sobre pagamentos de artigos e ainda a recolha de informação preferencial de cada utilizador, para a seleção de artigos semelhantes para cada utilizador e também publicidade.

Por isso, uma DPIA é necessária devido ao tipo de dados que vão ser processados, em que o processamento destes dados satisfazem os critérios:
-Evaluation or Scoring;
-Systematic monitoring, pois são recolhidos dados de preferencias dos utilizadores;
-Sensitive data or data of a highly personal nature, porque serão processados dados sensíveis que contêm informação pessoal.


**3.**
O DPIA do projeto encontra-se no ficheiro [DPIA.pdf](https://github.com/uminho-miei-engseg-18-19/Grupo10/blob/master/aula7/DPIA.pdf).

## Pergunta 1.4
O PIA do projeto encontra-se no ficheiro [PIA.pdf](https://github.com/uminho-miei-engseg-18-19/Grupo10/blob/master/aula7/PIA.pdf).

