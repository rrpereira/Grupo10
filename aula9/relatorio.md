# TP - 01/Abr/2019

## 1. Vulnerabilidade de codificação

### Pergunta 1.1
**1.** Estimativas de linhas de código:
 - **Facebook**: 62 000 000
 - **Software de automóveis**: 100 000 000
 - **Linux 3.1**: 15 000 000
 - **Todos os serviços Internet da Google**:  2 000 000 000

Estima-se que em qualquer pacote de de software tem uma média de 5 a 50 bugs por cada 1000 linhas de código fonte, alguns dos quais são vulnerabilidades.
Portanto, estima-se que número de bugs sejam:
- **Facebook**: entre 310 000 e 3 100 000 
- **Software de automóveis**: entre 500 000 e 5 000 000 
- **Linux 3.1**: entre 1 000 e 750 000
- **Todos os serviços Internet da Google**: entre 10 000 000 e 100 000 000

**2.** Não é possível responder a esta pergunta porque não existe uma estimativa do número de vulnerabilidades que se possa fazer a partir do número das linhas de código e do número de bugs.

### Pergunta 1.2
##### Vulnarabilidades de Projeto
- CWE-494: Download of Code Without Integrity Check
https://cwe.mitre.org/data/definitions/494.html

O código-fonte ou um executável é descarregado de um local remoto sem verificar suficientemente a origem e a integridade do código.

Uma solução para esta vulnerabilidade é cifrar o código com uma cifra confiável antes de transmitir.
Esta é só uma solução parcial, pois não deteta spoofing de DNS e não impede que o código seja modificado no site de host.

- CWE-414: Missing Lock Check
https://cwe.mitre.org/data/definitions/414.html

Não é verificado se está presente um "lock" antes de realizar uma operação sensível num recurso.

Uma solução para esta vulnerabilidade é implementar um mecanismo de "reliable lock".

##### Vulnarabilidades de Codificação
- CWE-12: ASP.NET Misconfiguration: Missing Custom Error Page https://cwe.mitre.org/data/definitions/12.html

Uma aplicação ASP.NET deve possibilitar páginas de erro personalizadas, para impedir que atacantes extraiam informações das respostas internas da estrutura.

Uma solução para esta vulnerabilidade é verificar se os valores de retorno estão corretos e não fornecer informações confidenciais sobre o sistema.

- CWE-767: Access to Critical Private Variable via Public Method
https://cwe.mitre.org/data/definitions/767.html

O software define uma método público que lê ou modifica variáveis privadas.

Uma solução para esta vulnerabilidade é fazer uma validação quadno aceitamos dados de um método público que se destina a modificar uma variável privada crítica. Além disso, convém certificar de que os controlos de acesso apropriados estão a ser aplicados quando um método público acede a dados críticos.

##### Vulnarabilidades Operacionais
- CWE-22: Improper Limitation of a Pathname to a Restricted Directory ('Path Traversal')
https://cwe.mitre.org/data/definitions/22.html

O software utiliza um *input* externo para construir um *pathname* que é suposto identificar uma diretoria que está localizada sob uma diretoria pai. No entanto o software não neutraliza adequadamente elementos especiais dentro do nome do caminho, o que pode fazer com que o nome do caminho seja transformado para um local que esteja fora da diretória restrita.

Uma solução para esta vulnerabilidade seria usar uma *firewall* de aplicação que possa detectar ataques contra esta vulnerabilidade. Esta solução pode ser benéfica em casos em que o código não pode ser corrigido (porque é controlado por terceiros), como uma medida de prevenção de emergência, enquanto são aplicadas medidas mais abrangentes de garantia de software ou para fornecer defesa em profundidade.

- CWE-94: Improper Control of Generation of Code ('Code Injection')
https://cwe.mitre.org/data/definitions/94.html

O software constrói todo ou parte de um segmento de código usando um *input* externo de um componente *upstream*, mas não neutraliza ou neutraliza incorretamente elementos especiais que podem modificar a sintaxe ou o comportamento do segmento de código pretendido.

Uma solução para esta vulnerabilidade é executar o código num ambiente que execute a propagação de contaminação automática e evite qualquer execução de comando que use variáveis contaminadas, como a opção "-T" do Perl. Isso força o programa a executar etapas de validação que removem a contaminação, embora seja preciso ter o cuidado de validar corretamente as entradas para que não se marque acidentalmente entradas perigosas como não contaminadas.

### Pergunta P1.3
As vulnerabilidades zero-day (ou de dia zero) são aquelas que são encontradas ou já previamente conhecidas num meio restrito de pessoas, e que podem ser exploradas antes que a comunidade informática tenha tempo de reagir a respeito. As outras vulnerabilidades já são conhecidas toda a comunidade informática.

