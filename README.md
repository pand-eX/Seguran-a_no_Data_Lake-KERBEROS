# Configurando Segurança no Cluster Hadoop Data Lake com Kerberos.

[![NPM](https://img.shields.io/npm/l/react)](https://github.com/pand-eX/Alta_disponibilidade_Streaming/blob/main/LICENSE) 

# About the project

Essa é a parte 2 do projeto. Na primeira instalamos e configurando um Data Lake com clustere Hadoop e nesse segundo projeto implementamos Segurança com Kerberos.

Como engenheiro de Dados, precisamos aprender como implementar políticas de autenticação, autorização e auditoria para acessar e usar dados armazenados no cluster Hadoop, bem como proteger os dados em trânsito e em repouso.



## Porque? 

Porque conforme o Ambiente Hadoop se amadurece umas das preocupações de quem utiliza é a segurança dos dados nesse projeto iremos aprender mais sobre como isso tudo funciona.

-Este projeto faz parte do meu portfólio pessoal, então ficarei feliz se você puder me fornecer qualquer feedback sobre o projeto, código, estrutura ou qualquer coisa que você possa relatar que possa me fazer um melhor engenheiro de dados!

Email-me: henricao_7@yahoo.com.br

Connect with me at [LinkedIn](https://www.linkedin.com/in/henrique-castro-484269203//).

## Segurança no Data Lake

O Hadoop, como sabemos é um projeto de código aberto que inclui vários módulos que foram desenvolvidos independentemente ao longo do tempo para adicionar vários tipos de funcionalidades às suas principais capacidades.
A segurança foi realmente uma reflexão tardia, e o Hadoop não possui um modelo de segurança coerente. Por padrão, o Hadoop pressupõe um ambiente confiável. À medida que o Hadoop amadurece, as empresas estão preocupadas, é claro, com a segurança de dados comerciais confidenciais que estão armazenados cada vez mais em ambientes baseados no Hadoop. Diferentemente do caso de um banco de dados tradicional, no Hadoop não há servidor ou mecanismo de autenticação central. Se os usuários conseguirem acessar o servidor que executa o NameNode e tiverem permissões apropriadas nos binários do Hadoop, poderão ler dados que não foram autorizados a ler e até mesmo excluir esses dados. Não há controle de acesso baseado em função (RBAC – Role Based Access Control), nível de objeto ou outros recursos de autenticação granular no Hadoop.
Como você armazena dados em vários DataNodes, cada um deles é um possível ponto de entrada para um invasor e você deve proteger todos os nós em um cluster. Para criptografar dados fluindo entre os clientes e os DataNodes, você deve usar o Kerberos ou uma estrutura SASL (Simple Authentication and Security Layer). A comunicação entre os DataNodes e o NameNode também precisa ser protegida.

![1](https://github.com/pand-eX/Seguran-a_no_Data_Lake-KERBEROS/blob/main/Seguran%C3%A7a%20no%20Data%20Lake/assets/1.png)

A criptografia é um requisito importante para proteger dados confidenciais. A falta de criptografia e a criptografia de dados em “Trânsito” significa que as comunicações do internode podem ser interceptadas e as informações privadas armazenadas no disco podem ser acessadas. 


## A segurança do Hadoop envolve três conceitos principais – Autenticação, Autorização e Auditoria.

- Autenticação: A melhor e mais aceita forma de fornecer autenticação para o Hadoop é através da segurança do Kerberos. O Kerberos fornece autenticação forte de usuários e serviços que trabalham com um cluster do Hadoop.

- Autorização: A autorização, que determina quem pode acessar os dados de um cluster Hadoop, é uma das principais preocupações de segurança em qualquer ambiente. Você usa listas de controle de acesso (ACLs) para configurar a autorização. O Apache Sentry permite que você configure autenticação forte e detalhada para os dados.

- Auditoria: A auditoria é o acompanhamento da atividade dentro do cluster e pode incluir atividade de usuário e administrativa. Criptografar dados em trânsito pela rede e dados em repouso (armazenados em disco) é extremamente importante, especialmente quando você lida com o que é conhecido como informações pessoalmente identificáveis, como número de identididade, CPF ou carteira de motorista.


![2](https://github.com/pand-eX/Seguran-a_no_Data_Lake-KERBEROS/blob/main/Seguran%C3%A7a%20no%20Data%20Lake/assets/2.png)


![3](https://github.com/pand-eX/Seguran-a_no_Data_Lake-KERBEROS/blob/main/Seguran%C3%A7a%20no%20Data%20Lake/assets/3.png)

## Hadoop Security Design


Como engenheiro de Dados, precisamos aprender como implementar políticas de autenticação, autorização e auditoria para acessar e usar dados armazenados no cluster Hadoop, bem como proteger os dados em trânsito e em repouso.

![4](https://github.com/pand-eX/Seguran-a_no_Data_Lake-KERBEROS/blob/main/Seguran%C3%A7a%20no%20Data%20Lake/assets/4.png)

![5](https://github.com/pand-eX/Seguran-a_no_Data_Lake-KERBEROS/blob/main/Seguran%C3%A7a%20no%20Data%20Lake/assets/5.png)

Juntando as duas imagens fica mais ou menos assim.

![6](https://github.com/pand-eX/Seguran-a_no_Data_Lake-KERBEROS/blob/main/Seguran%C3%A7a%20no%20Data%20Lake/assets/6.png)

## Princípios gerais que fundamentam a segurança corporativa em um ambiente Hadoop:


- Idealmente, um cluster Hadoop deve estar em seu próprio segmento de rede, separado do restante do ambiente de TI com firewall apropriados, bem como medidas de segurança como sistemas de detecção de intrusão e invasão.

- É uma prática comum configurar uma VLAN protegida para um cluster Hadoop e limitar as conexões aquelas iniciadas somente a partir dos servidores de gateway.

- Em geral, os firewalls de rede devem permitir o tráfego entre os servidores do cluster e para o gateway. Eles também devem permitir que os nós datanode se conectem aos serivodres de banco de dados para enviar e receber dados em portas específicas.

- Dependendo de como os clientes podem acessar seu cluster – algumas organizações permitem que os clientes acessem diretamente o cluster e outros não – você precisa configurar as políticas de firewall de rede apropriadas entre os aplicativos e o cluster Hadoop, bem como entre os aplicativos e os usuários finais.
Precisa chamar o administrador de rede e orientá-lo as portas para ele abrir.

- Os usuários (Cientista ou Analista de Dados) podem executar scripts MapRedunce e Hive a partir da linha de comando em um dos nós do cluster ou podem usar o Hue ou uma ferramenta diferente para se conectar e trabalhar com o cluster ou ainda usar um servidor intermediário como acesso ao cluster.
Como os usuários faram acesso? Eles vão conectar diretamente em um dos servidores do cluster? Eles vão utilizar uma ferramenta visual gráfica via browser como o Hue? Eles vão acessar um servidor intermediário que você configura e desse servidor intermediário tenha um client por exemplo eles acessam o cluster? Depende de como a empresa quer implementar a segurança e também do nível dos usuários finais. Porque muito cientista de dados não sabe trabalhar com linha de comando


## O que é protocolo Kerberos?

O Kerberos é um requisito para autenticação do usuário no Hadoop. O Kerberos é a maneira mais comum de proteger um cluster Hadoop, por meio de seu mecanismo de autenticação.
Na mitologia grega, Kerberos (em grego, Cerberos) é o feroz cão de várias cabeças que guarda os portões de Hades para garantir que ninguém saia.

![7](https://github.com/pand-eX/Seguran-a_no_Data_Lake-KERBEROS/blob/main/Seguran%C3%A7a%20no%20Data%20Lake/assets/7.png)


No mundo de segurança o kerberos adquiriu fama como um mecanismo de autenticação forte, ao mesmo tempo que intimidava muitos administradores como sua aparente complexidade.
O Kerberos é um protocolo de autenticação no qual os hosts são confiáveis, mas a rede não é. O kerberos trabalha na premissa que os hosts em um cluster são confiáveis e sua chave secreta não é comprometida. O design de segurança do Kerberos envolve três entidades principais:

- Usuário que desejam se autentica.

- O serviço para o qual o usuário está tentando se autenticar.

-Servidor de segurança Kerberos (Key Distribution Center ou KDC), confiável tanto pelo usuário quanto pelo serviço. É o KDC que armazena as chaves secretas para os usuários e Serviços.


O Kerberos usa um servidor central. Como uma falha deste servidor significa que ninguém pode efetuar login em seu cluster, você tem permissão para configurar mais de um servidor. As senhas são altamente seguras, pois o Kerberos as salva no servidor central e não replica as informações de senha em nenhum outro lugar.
Depois que um usuário efetua login em um sistema autenticado pelo Kerberos (também chamado de cluster Kerberizado), ess usuário pode continuar a acessar todos os serviços autorizados sem ter que autenticar novamente durante essa sessão. Nesse sentido, é semelhante ao conceito de Logon Único (Single Sign-on).
O Kerberos usa conjunto de termos exclusivos e, para entender como a autenticação Kerberos funciona, é importante entender o significado desses termos. Também emprega várias entidades administrativas exclusivas para impor a segurança. Entender essas entidades é crucial para configurar e gerenciar a segurança baseada em Kerberos.
Um KDC é um servidor Kerberos que contém um banco de dados criptografado no qual armazena todas as entradas pertencentes a usuários, hosts e serviços (também chamados principals), incluindo suas informações de domínio.
Além do banco de dados que é armazenado na forma de um arquivo, um KDC também contém dois componentes importantes, denominados Authentication Service (AS) e o Ticket Granting Server (TGS).
O AS e o TGS juntos tratam de todas as solicitações de autenticação e acesso feitas a um cluster do Hadoop protegido por Kerberos. O banco de dados Kerberos armazena as informações principais. 


![9](https://github.com/pand-eX/Seguran-a_no_Data_Lake-KERBEROS/blob/main/Seguran%C3%A7a%20no%20Data%20Lake/assets/9.png)


![10](https://github.com/pand-eX/Seguran-a_no_Data_Lake-KERBEROS/blob/main/Seguran%C3%A7a%20no%20Data%20Lake/assets/10.png)


Uma boa prática e você isolar o seus servidores, ou seja, seu ambiente com hadoop, banco de dados e etc... da rede do usuários. Muitas empresas, já utiliza essa estratégia ela tem uma rede interna para os servidores e uma outra rede interna para os usuários e então configura algumas rotas para que os usuários possam acessar especificamente os servidores. Quando você coloca o Hadoop nessa história você pode ter o hadoop em um domínio e configurar o Kerberos KDC para esse domínio e os usuários estará em um outro domínio Kerberos para esse cenário você configura o Kerberos Trusts uma relação de confiança entre os Domínios então o usuário na hora de utilizar seu UPN ele vai continuar usando o mesmo do seu próprio domínio só que esse domínio tem permissão, confiança para acessar recursos de um outro domínio.

## Instalando e configurando Kerberos.

A configuração é feita através do special principal usado pelo AS e pelo TGS, chamado krbgt/<REALM>@<REALM>.
1) Instalar o Kerberos no cluster Hadoop
2) Configurar o Kerberos, o que envolve a criação do banco de dados Kerberos, o administrador Kerberos, os user e service principals e seus keytabs.
3) Iniciar os Daemons Kerberos.
4) Configurar o Hadoop para o Kerberos, o que envolve o mapeamento de entidades de serviço para nomes de usuários do SO e a adição de vários parâmetros relacionados ao Kerberos aos arquivos de configuração do Hadoop, como hdfs-site.xml e yarn-site.xml
5) Inicializar o Hadoop Cluster (como HDFS e YARN) no modo seguro.
6) Testar conexões seguras para o cluster do Hadoop.

Depois de baixar o processo e descompactar entre no diretório que está o binário e executá-lo entrar como root e compila-lo e instalar pronto e agora precisamos de algumas biblioteca para o sistema operacional comando  > yum install krb5-libs krb5-server krb5-workstation
e pronto agora pode executar o Kerberos próxima etapa e configurar os arquivo de configuração. São 2 arquivos principais o arquivo de configuração do próprio Kerberos e os arquivos com parâmetro do KDC, ou seja, do centro de distribuição de chaves
Diretório > /etc/krb5.conf
Repare que o arquivo tem 4 grandes áreas tenho logging, libdefaults, realm e domain_realm
a primeira e a logging que basicamente é os arquivos de log aonde você vai buscar informação no caso de problemas no caso de troubleshooting e lá que você vai buscar a resolução depois disso temos o libdefaults que são conjuntos de parâmetros para que você possa gerenciar o seu Kerberos depois é o realms que nesse caso é um único domínio dentro das chaves eu tenho 2 parâmetros o kdc e o endereço do admin_server eu poderia ter o admin em uma máquina e o kdc em outra no meu caso os 2 serviços estará na mesma máquina e por último nós temos o domain_realm com o nome do domínio e tem uma informação importante em minúsculo do lado esquerdo eu tenho o nome do domínio do lado direito eu tenho o nome do realms.
O Kerberos é o protocolo agora vamos configura o KDC que é o serviço de fornecimento de tickets dentro de todo o processo de autenticação do kerberos 
Diretório > /var/kerberos/krb5kdc/ e vamos criar o arquivo kdc.conf e colocar os parâmetros
Temos duas áreas uma com o kdcdefaults e com realms no kdcdefaults temos o endereço da porta do KDC. Na outra o realms onde eu vou colocar as informações do domínio veja que temos informações por exemplo como criptografia porque o kdc é que fornece a chave de segurança o Kerberos gerencia o processo o kdc é quem emiti o ticket o primeiro parâmetro por padrão a criptografia fornecido pelo KDC e de 128 bits se você quiser habilitar a criptografia de 256 temos que instalar uma extensão do JAVA que por padrão não vem instalada aí é só descomentar a primeira linha.
Agora precisamos dizer quem vai administrar, quem vai pode acessar especificamente todo nosso ambiente utilizando acesso administrativo fazemos isso no arquivo ACL esse arquivo fica no mesmo diretório do kdc.conf e cria o arquivo kadm5.acl e temos o */admin que significa nesse momento do jeito que estamos configurando qualquer usuário que tive como principals alguma coisa /admin poderá ter acesso administrativo ao Kerberos exemplo se eu criar um principals Hadoop/admin@DSA.com ele vai ter acesso administrativo e claro que você pode especificar o nome do usuário.
  
  
![11](https://github.com/pand-eX/Seguran-a_no_Data_Lake-KERBEROS/blob/main/Seguran%C3%A7a%20no%20Data%20Lake/assets/11.png)
  
  
Agora que terminamos os arquivos de configuração precisamos criar um banco de dados aonde o KDC vai organiza suas informações afinal de contas ele precisa organizar os Principals, guardar a senha de alguma forma e etc...
Nada mais que um arquivo. O comando é > kdb5_util create -s 
Cada realm tem o seu próprio banco de dados eu posso configurar vários realm dentro de um ambiente, configurar relação de confiança e etc... Pronto já temos o banco de dados.
Por enquanto nós não configuramos o Hadoop estamos apenas configurando o Kerberos quando configurarmos o Hadoop o Cluster passara receber autenticação via Kerberos e claro o KDC que distribuí a chaves se eu perder esse banco de dados do KDC eu não consigo acessar os dados dentro do meu Cluster Hadoop então atenção para não ter problema com o Cluster Hadoop.
Último processo e criar o nosso primeiro Principals, ou seja, o primeiro grande administrador dentro desse ambiente Kerberos comando > kadmin.local –q “addprinc hadoop/admin” e pronto principals criado.
Vamos inicializar o ambiente de autenticação e nós temos que inicializar 2 serviços o KDC que é o serviço responsável pelo controle das chaves que vai permite a emissão dos tickets e também o admin_server que basicamente é o gerenciador de todos os serviços do Kerberos lembrando que os arquivos do banco de dados inclusive os ocultos precisa estar no mesmo diretório que criamos os arquivos kadm5.acl e kdc.conf

 ![12](https://github.com/pand-eX/Seguran-a_no_Data_Lake-KERBEROS/blob/main/Seguran%C3%A7a%20no%20Data%20Lake/assets/12.png)
  
Agora é só iniciar o kerbero> service krb5kdc start e tbm o admin_server > service kadmin start
Agora para finalizar vamos deixa o serviço automático caso eu desligue a máquina não precisa executar novamente > chkconfig krb5kdc on também no admin > chkconfig kadmin on
E para testar > kadmin e irá abrir um shell indicando que a partir daqui você pode administrar seu ambiente Kerberos 

## Compreendendo o Kerberos Workflow
  
![13](https://github.com/pand-eX/Seguran-a_no_Data_Lake-KERBEROS/blob/main/Seguran%C3%A7a%20no%20Data%20Lake/assets/13.png)
  

Usaremos um exemplo imagine que um usuário qualquer quer usar um serviço gerenciado pelo protocolo Kerberos que no caso é o MyService esse serviço poderia ser o Apache Hadoop eu tenho dados armazenados no HDFS lá no Data Lake e Alice precisa acessar esses dados eu preciso estabelecer um protocolo de autorização e autenticação com o Kerberos é feito através de 2 serviços do AS(authentication Service) e do TGS(ticket granting service).
Os 2 primeiro passos são a comunicação do usuário com AS ela deve estar listada naquela ACL(lista de controle de acesso) que configuramos ela entra em contato com o AS e ele verifica se ela pode ou não acessar o serviço e entrega de volta para Alice um TGT esse ainda não é um Ticket final é uma espécie de pedido para o ticket uma pré autorização com isso em mãos ela valida esse TGT com a senha dela uma espécie de carimbo e ela envia esse pedido para o TGS passo número 4 esse passo já tem a senha da alice e já tem essa Pré-Autorização ela está pedindo ao TGS para fornecer um Ticket para que ela possa acessar os dados lá no serviço o TGS então simplesmente emite um ticket e devolve isso para Alice e os 2 últimos passo e Alice utilizar esse ticket para acessar o serviço tudo isso é feito sobre o protocolo Kerberos.
Então o passo agora é criar o Service Principals com o Kadmin nós criamos o Principals agora precisamos criar o Service Principals(entidade de serviços) nada mais é que conta de serviços. Cada serviço que for autenticado pelo protocolo kerberos ele precisa de um service principals que nada mais é que uma entrada no banco de dados do kerberos. Precisamos do service principals para o HDFS e o Yarn para que ambos os serviços possam ser autenticados via kerberos e depois receber conexões de usuários.
Precisamos criar principals para cada daemon do cluster no caso será 3 serviços o HDFS o YARN e o HTTP isso e para cada daemon se você tiver 1000 daemon você terá que criar para cada um deles e também para cada DataNode. Se um DataNode for comprometido por invasão você não compromete os outros DataNode se eu utilizar o mesmo service principals para todos os datanodes se alguém obter esse acesso consegue ter acesso de todos os datanodes do meu Cluster.
Comando para adicionar o service principals addprinc (princ é uma conta de serviço e precisa de uma senha ou uma chave de segurança então usaremos o comando> -randkey para gerar uma chave randômica) addprinc –randkey (depois é só digitar o nome do serviço)
  
  
  
![14](https://github.com/pand-eX/Seguran-a_no_Data_Lake-KERBEROS/blob/main/Seguran%C3%A7a%20no%20Data%20Lake/assets/14.png)
  
  
DSA.COM maiúsculo é o domínio realm do Kerberos o domínio minúsculo é o qualificado de cada uma das máquinas do Cluster você pode verificar o arquivo hosts o NN é o service principals do HDFS. Com isso nós temos o service principals necessários criados se eventualmente você depois quiser implementar por exemplo o HIVE dentro do seu cluster tem que vir aqui e criar o service principals configurar os arquivos de configuração do Hive e então realização autenticação via Kerberos isso vale para qualquer produto do ecossistema você pode fazer isso via demanda à medida que você vai adicionando outros componentes ao ecossistema você cria o service principals de acordo com a necessidade uma outra coisa importante é em qual servidor que eu tenho que criar esse service principals? Na verdade, você pode fazer o acesso de qualquer máquina nesse caso o meu Namenode1 ele é o NameNode e por acaso também é o KDC mas não precisa ser a mesma máquina. Eu poderia ter o KDC em outro servidor poderia fazer o acesso remoto a esse KDC via kadmin basta colocar o endereço completo e então eu crio o service principals, ou seja, eu faço isso apenas uma vez porque afinal de conta o banco de dados do KDC é apenas um banco de dados centralizados.
Agora precisamos criar o Keytab Files que são arquivos de autenticação para o service principals mas porque precisamos do Keytab Files? 
Para testar a conexão usaremos o kinit (nome do user principals /admin) e depois usa o comando > klist para verificar se fez a autenticação.
  
  
![15](https://github.com/pand-eX/Seguran-a_no_Data_Lake-KERBEROS/blob/main/Seguran%C3%A7a%20no%20Data%20Lake/assets/15.png)
  

O default principal é o usuário e ele já recebeu um Ticket de acesso.
Quando usarmos o kinit para o service principals que nós criamos para verificar se tem acesso ele vai pedir uma senha, mas nós não colocamos uma senha na criação do service principals nós usamos o -randkey para gerar uma chave de segurança de maneira randômica é essa chave vamos usar para autenticação e essa chave fica no Keytab Files! Por isso precisamos desses arquivos temos que cria o Keytab Files para armazenar aquela chave e com isso via o Keytab File pode fazer a autenticação do service principals. Lembrando que ele é um serviço.
Para criar o Keytab File é bem fácil entrando pelo kadmin agora vamos criar um keytab files para grupo de service principals comando é > xst -k nn.service.keytab nn/nn1.dsa.com@DSA.COM nn/nn2.dsa.com@DSA.COM nn/dn1.dsa.com@DSA.com nn/dn2.dsa.com@DSA.com (basicamente é o serviço e os daemon que configurando no service principals) quando executarmos esse comando o kadmin vai pegar aquelas chaves que foram criadas durante o service principals e vai adicionar em um arquivo chamado nn.service.keytab depois esse arquivo nós vamos adicionar no arquivo de configuração do hadoop para dizer para o hadoop quando você quiser fazer a autenticação via um desses serviços busque a chave de segurança no nn.service.keytab
  
![16](https://github.com/pand-eX/Seguran-a_no_Data_Lake-KERBEROS/blob/main/Seguran%C3%A7a%20no%20Data%20Lake/assets/16.png)
  
Agora é só fazer isso para os datanode o yarn e o http para o http é um pouco diferente os outro são iguais mas o http fica assim> xst –k spnego.service.keytab (e o http que configuramos)
Agora você usa o ls -la *.keytab para ver os arquivos é movê-los para o hadoop conf dir é uma variável de ambiente que configuramos na criação do hadoop para ver você usa o comando> cat.bashrc e ele aponta para o /opt/hadoop na minha máquina. Porém os 4 arquivos estão com privilégio de leitura e escrita, mas como esses arquivos são críticos porque se alguém obter pode fazer o acesso no service principals a recomendação é você colocar apenas privilégio de leitura então usamos o comando > chmod 400 *.keytab
  
  
![17](https://github.com/pand-eX/Seguran-a_no_Data_Lake-KERBEROS/blob/main/Seguran%C3%A7a%20no%20Data%20Lake/assets/17.png)
  
essa é uma medida de segurança importante e claro garantir que esses arquivos estejam o mais protegido possível caso contrário alguém com esse arquivo acessa diretamente o KDC com a conta de service principals.
Você pode fazer um keytab para os usuários para conecta sem senha mesmo procedimento para o service principals.
Agora vamos testar a conexão com o kinit porém precisamos colocar o endereço onde colocamos o arquivo para ele ler os arquivos.
  
  
![18](https://github.com/pand-eX/Seguran-a_no_Data_Lake-KERBEROS/blob/main/Seguran%C3%A7a%20no%20Data%20Lake/assets/18.png)
  
  
pronto. Isso é necessário exatamente porque estamos configurando conta de serviços para os serviços do nosso cluster nesse caso o HDFS, yarn, HTTP e uma para o DataNode.
Até aqui nós não configuramos nada do Apache Hadoop. Primeiro nós configuramos e instalamos o KDC e agora nós criamos o service principals também no KDC e o keytab files.
E vamos fazer isso agora o primeiro passo é mapear os services principals porque apenas criamos o nn/nn1 e os outros daemon para o HDFS, mas só o fato de criamos nn (HDFS) não significa que ele está sendo mapeado para o HDFS, ou seja, nós criamos o service principals para que eles possam ser usados com os serviços para os Daemon do HDFS nas 4 máquinas do Cluster, mas aonde eu digo isso? Onde eu configuro essa informação? Então precisamos fazer o mapeamento do service principals
Configuração à Autenticação do Kerberos no Cluster Hadoop
Basicamente é seguir as recomendações do apache hadoop para configuração dos parâmetros segue em anexo.
A configuração do Yarn não é obrigatório ele é um gerenciador de recursos para o cluster hadoop e você vai usar o YARN se você for executa Jobs MapRedunce alguns componente do ecossistema hadoop utilizam Jobs mapredunce o Pig por exemplo ele converte o código em Pig para um Jobs mapredunce logo ele executa um job e nesse caso precisaria do Yarn caso eu não queira usar o Yarn eu posso usar diretamente o mapredunce teria que fazer as configurações também é possível usar apenas o HDFS para o armazenamento distribuído.
Repare que em muitos parâmetros coloquei o _HOST pois para cada daemon é um service principals e para adicionar nos parâmetros de configuração imagina o trabalho se eu tivesse um cluster de 1000 máquinas não seria viável por isso o PlaceHolder para nomes FQDN ele apenas vai substitui o _HOST pelo nome local da máquina que nós configuramos na criação do Service Principals o nn1, nn2 e etc...
Lembre-se de usar a Documentação para auxiliar na montagem dos parâmetros. 
Terminamos as configurações mas repare que eu fiz isso apenas no NameNode 1 e agora nós precisamos fazer nas demais máquinas do cluster no meu caso são 4 máquinas 2 NameNode e 2 DataNodes.
As configurações do Kerberos KDC pode ser feito em outra máquina externa que você tiver no meu caso estou usando tudo no NameNode 1 mas as configurações que serão passadas via SCP para os outros Daemon e só os arquivos Keytab e os arquivos XML que configuramos que foi o Core-site.xml, hdfs-site.xml, e o yarn-site.xml seque em anexo os comandos. Para você fazer isso precisa estar no mesmo diretório onde estão os arquivos.
  
![19](https://github.com/pand-eX/Seguran-a_no_Data_Lake-KERBEROS/blob/main/Seguran%C3%A7a%20no%20Data%20Lake/assets/19.png)
  
pronto lá estão os 4 arquivos
Como sabemos que o DataNode que armazena os dados do cluster hadoop nós temos que fazer algumas configurações adicionais para ele rodar em modo seguro. E esse procedimento precisa ser feito em cada DataNode do Cluster a recomendação é faz em uma máquina depois replica para as demais. Para um melhor entendimento busque a documentação e busque Secure DataNode tem a explicação mais detalhada. Mas porque isso aqui é necessário? Como o DataNode ele armazena os dados para que nós possamos colocar ele em modo seguro o serviço DataNode será inicializado como root até aqui nós inicializamos os serviços como usuário hadoop que é o Onwer do hadoop que roda sem nem um problema só que o DataNode requer uma configuração adicional só que por conta disso quando você executa o comando hdfs datanode o processo servidor faz uma ligação para as portas privilegiada primeiro depois ele simplesmente faz um drop, ou seja, ele reduz o privilégio e executa os serviços como uma conta de usuário que nós especificarmos no parâmetro HDFS_DATANODE_SECURE_USER só que para que isso funcione nós precisamos inicializar o processo utilizando o JSVC ele basicamente faz uma ligação para permitir essa configuração embora eu for iniciar como root eu vou conseguir reduzir o privilégio para que apenas o usuário owner realmente consiga executar aquele serviço, o daemon.
Essa etapa é para fazer apenas no DataNode. 1 Coisa é instalar o jsvc ele é basicamente um pequeno daemon que permiti inicializar ou parar uma jvm(java virtual machine) de acordo com o tipo de aplicação rodando no servidor, ou seja, nós precisamos do jsvc porque nós vamos inicializar o serviço do DataNode como root mas para garantir q ele seja reduzido para o usuário depois que o serviço tiver em execução o jsvc precisa estar instalado e apontar isso nas configurações do hadoop é ele que vai garantir o nível de acesso para a jvm.
Temos que fazer isso no arquivo hadoop-env.sh onde são as variáveis de ambiente do hadoop.
  
![20](https://github.com/pand-eX/Seguran-a_no_Data_Lake-KERBEROS/blob/main/Seguran%C3%A7a%20no%20Data%20Lake/assets/20.png)
  
E também descomentar esses outros dois parâmetros no mesmo arquivo ele fica um pouco mais a baixo
  
![21](https://github.com/pand-eX/Seguran-a_no_Data_Lake-KERBEROS/blob/main/Seguran%C3%A7a%20no%20Data%20Lake/assets/21.png)
  
esses são diretórios onde estará os arquivos de log do serviço com DataNode porque na prática o serviço será inicializado com o usuário root por conta disso o ideal e que você tenha um diretório específico para gravar o PID e o Logs porque isso não pode estar disponível para outros usuários que acessam aquela máquinas, somente para o root que vai inicializar o serviço e descendo mais um pouco precisamos habilitar o usuário que será o responsável pelo processo no momento que houver a redução de privilégio.
  
![22](https://github.com/pand-eX/Seguran-a_no_Data_Lake-KERBEROS/blob/main/Seguran%C3%A7a%20no%20Data%20Lake/assets/22.png)
  
descomenta e colocar o seu usuário. Basicamente está dizendo para o hadoop nós estamos habilitando o modo seguro no datanode quem vai inicializar o serviço é o root só que quando ele inicializar utilize o jsvc para reduzir o privilégio daquele processo para esse usuário que é o hadoop e pronto.
Não podemos esquecer de enviar a copiar dos arquivos do krb5.conf se não ele não vai encontrar e não vai fazer a conexão. Os arquivos estão no diretório krb5.conf e precisamos colocar em todas as máquinas.
  
![23](https://github.com/pand-eX/Seguran-a_no_Data_Lake-KERBEROS/blob/main/Seguran%C3%A7a%20no%20Data%20Lake/assets/23.png)
  
Eepare que ele teve sucesso no modo Seguro e está funcionando.
Quando for iniciar o DataNode lembre-se que precisa estar em modo root para isso pode utilizar o comando sudo /opt/hadoop/bin/hdfs --daemon start datanode (lembre-se de colocar o caminho onde ele encontra o binário do HDFS) se você digitar jps ele não vai aparecer o DataNode porque ele foi inicializado agora em outro nível de privilégio, mas isso também não é problema você pode usar o comando ps -ax | grep datanode para verificar se esse serviço foi inicializado. E ele foi inicializado naquele padrão, ou seja, o root inicializou o serviço habilitou naquelas portas privilegiadas feito isso o jsvc reduziu a prioridade para que na prática o usuário hadoop seja o responsável pela execução desse serviço se alguém invadir por essas portas o máximo que vai conseguir é executar com nível hadoop e não com nível do usuário root. 
Pronto finalizamos nosso cluster de Alta Disponibilidade em modo seguro com o Kerberos
  
![24](https://github.com/pand-eX/Seguran-a_no_Data_Lake-KERBEROS/blob/main/Seguran%C3%A7a%20no%20Data%20Lake/assets/24.png)

  
![25](https://github.com/pand-eX/Seguran-a_no_Data_Lake-KERBEROS/blob/main/Seguran%C3%A7a%20no%20Data%20Lake/assets/25.png)
  
conectando via Browse.
Lembrando que você precisa criar um User Principals para acessar o HDFS no nosso caso não criamos o User principals nós criamos um Service Principals que foi o nn(HDFS), Yarn e o HTTP então vamos criar o User Principal.
Com o usuário administrador hadoop entramos no kadmin depois é só criar o user com addprinc (nome do user principal e @realm) digitar a senha e pronto user criado.

![26](https://github.com/pand-eX/Seguran-a_no_Data_Lake-KERBEROS/blob/main/Seguran%C3%A7a%20no%20Data%20Lake/assets/26.png)
  
Depois disso precisamos usar o kinit para fazer a conexão com o KDC para pegar um ticket como ele ainda não tem um ticket ele vai gerar um. Quando você cria o User Principals você não tem um ticket automático eu preciso fazer a conexão ao KDC com o usuário para que o ticket seja gerado.
  
![27](https://github.com/pand-eX/Seguran-a_no_Data_Lake-KERBEROS/blob/main/Seguran%C3%A7a%20no%20Data%20Lake/assets/27.png)
  
Pronto agora sim ticket gerado e com prazo de validade.
  
![28](https://github.com/pand-eX/Seguran-a_no_Data_Lake-KERBEROS/blob/main/Seguran%C3%A7a%20no%20Data%20Lake/assets/28.png)
  
Agora acabamos de listar exatamente o conteúdo que nós temos no HDFS e com isso fizemos o acesso de forma segura via Kerberos ao nosso cluster de Alta disponibilidade que representa nosso Data Lake.

