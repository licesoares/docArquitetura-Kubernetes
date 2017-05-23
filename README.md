# Documentação Arquitetural do Sistema Kubenetes

**Alunos:** Alice Soares, Luisa Cunha e Maxmillian Araújo

**Professor:** Marco Túlio de Oliveira Valente

**Disciplina:** Engenharia de Software II

**Repositório Github:** https://github.com/kubernetes/kubernetes

Descrição do sistema
--------------------

#### Contexto
<p align="justify">
A utilização de máquinas virtuais atualmente é consolidada e auxilia no desenvolvimento de software em empresas e até para desenvolvedores individuais. Hoje existem diversas plataformas que permitem configurações dinâmicas de máquinas virtuais na nuvem que possibilitam a construção de ambientes de desenvolvimento escaláveis e padronizados a um valor acessível. No entanto, as aplicações que são executadas na máquina virtual compartilham os recursos de memória, disco rígido, bibliotecas, configurações e processos do Sistema Operacional hospedeiro, fazendo com que o teste de aplicações distintas precise considerar estes fatores. Os containers virtuais vêm resolver esta questão, eles promovem a virtualização a nível de sistema operacional encapsulando a aplicação e os recursos de memória, disco e rede requeridos por ela. Dessa forma, apesar de o Container e as máquinas virtuais trabalharem com virtualização e isolamento, os Containers criam ambientes isolados onde diferentes aplicações podem ser executadas simultaneamente.
</p>

#### Objetivo
<p align="justify">
O Kubernetes além de prover o escalonamento e execução de containers de aplicações em clusters de máquinas físicas ou virtuais, oferece uma infraestrutura centrada em container que permite construir ambientes de desenvolvimento centrados em containers.
</p>

#### Kubenertes

O Kubernetes satisfaz diversas necessidades comuns de aplicações:
- *Co-alocação de processos auxiliares*: <p align="justify"> O Kubernetes trabalha com o conceito de Pod, que é a menor unidade de computação que pode ser criada e gerenciada. Um Pod é um grupo de um ou mais containers, o armazenamento compartilhado entre eles e as opções de como executar este grupo. </p>
- *Montagem de sistemas de armazenamento para persistência de dados*: <p align="justify"> Um container sempre é iniciado no estado “limpo”, a consequência disso é que caso um container falhe e seja reiniciado (o que ocorre automaticamente) os arquivos são perdidos. Outro problema é que na execução simultânea de containers de uma mesma aplicação é possível que seja necessário compartilhar recursos. Para resolver estes problemas o Kubernetes possui uma abstração de Volume. </p>
- *Proteção à informação sensível*: <p align="justify"> O Kubernetes chama de ‘Secret’ um objeto que contém algum tipo de informação sensível, como uma senha ou token. </p>
- *Checagem da aplicação*: <p align="justify">São providas configurações diversas de Debug, Logging, Monitoramento, Tasks, Jobs, etc. de forma que o usuário consiga monitorar o funcionamento e execução dos containers.</p>
- *Replicação de instâncias*: <p align="justify">Duplicação de instâncias de Pods garantindo alta disponibilidade das aplicações.</p>
- *Dimensionamento automático horizontal*: <p align="justify">Ajusta automaticamente o número de Pods em um controlador de replicação coincidindo com a utilização média de CPU observada.</p>
- *Sistema de nomes*: <p align="justify">O Kubernetes oferece serviço de DNS para atribuir nomes de DNS’s a serviços das aplicações.</p>
- *Balanceamento de carga*: <p align="justify">Pods são criados e destruídos dinamicamente de forma a não sobrecarregar a máquina.</p>
- *Atualização Contínua*: <p align="justify">Provê atualização individual de Pod, de modo que não seja necessário desativar todo o serviço ao mesmo tempo.</p>
- *Monitoramento de Recursos*:<p align="justify"> Verificação de utilização de recursos a nível de Pod ou clusters inteiros.</p>
- *Logging* :<p align="justify"> O Kubernetes permite logs das aplicações recipientes.</p>
- *Segurança* :<p align="justify"> Níveis de autorização e autenticação para acesso às aplicações.</p>

<p align="justify">
Kubernetes é de código aberto, está disponível no GitHub no link https://github.com/kubernetes/kubernetes e possui extensa documentação que pode ser acessada no link https://kubernetes.io/. Essa disponibilidade e documentação permite que os usuários vejam como toda a programação funciona, bem como os incentiva a criar novas funcionalidades ou melhorias que os ajudem em seus cenários. O sistema não limita os tipos de aplicativos suportados, não fornece middleware, estrutura de processamento de dados, bases de dados ou sistemas de armazenamento em cluster, apesar disso, é capaz de executar todos estes aplicativos.
</p>

#### O Desenvolvimento do Projeto

<p align="justify">
O Kubernetes é um conjunto de projetos, sendo que cada projeto é liderado por um grupo denominado SIG, abreviação para Special Interest Group (Grupo de interesse especial). A comunicação é organizada através de uma lista que contém canais de comunicação, como bate-papo, listas de discussão, conferências, problemas que precisam ser resolvidos e etc.. Os SIGs funcionam como estados em um país, podendo conter suas próprias políticas de contribuição, listas de discussão e etc.. 
</p><p align="justify">
Existe uma auto organização entre todos os colaboradores e desenvolvedores do sistema. Com isso, se uma pessoa/desenvolvedor deseja se tornar um colaborador, este pode escolher um SIG e procurar dentre uma lista de problemas um problema a ser resolvido, preferenciamente que não precise de conhecimento profundo do sistema, já que é o primeiro desenvolvimento do programador no Kubernetes. Para trabalhar em uma nova ideia com escopo pequeno, o desenvolvedor pode enviar o problema descrevendo a alteração proposta ao repositório em questão e os proprietários do repositório irão responder de forma rápida (dentro do possível) dando aval ou não para a ideia proposta. Outra possibilidade de contribuição é encontrando bugs, nesse caso basta que a pessoa envie para os proprietários documentando o problema ou requisito que o sistema não captura. 
</p><p align="justify">
Para o desenvolvimento no Kubernetes, é necessário que os desenvolvedores tenham familiaridade com conceitos de administração de cluster e arquitetura de software, de forma a responder se “pull request” se trata de uma questão de arquitetura ou se apenas resolve um bug. Para validar a correção de erros elaborada pelo desenvolvedor, o sistema se baseia, além do código, na cobertura de testes. Dessa forma, todas as modificações devem ser enviadas com a documentação dos testes e os testes realizados. Os testes também podem ser usados no apontamento de bugs, em que o contribuinte pode elaborar ou modificar um teste unitário de forma a encontrar o erro.
</p><p align="justify">
Também é possível fazer melhorias na arquitetura adicionando novos recursos ou tornando um recurso mais modular, convertendo estruturas para interfaces, melhorando os testes ou mesmo tornando o código mais robusto. Geralmente essas melhorias diminuem as linhas de código e mantém as funcionalidades.
</p><p align="justify">
Por fim, as alterações podem ser na melhoria de testes ou até alterações de arquitetura, em que geralmente um recurso é tornado mais modular, ou é feito um investimento para tornar o código mais robusto. De qualquer forma, todas as alterações passam por revisores, que possuem regras claras (e documentadas) para a submissão dos ajustes/novas funcionalidades. A seguir um fluxograma demonstrando quais os passos devem ser seguidos pelos programadores:
</p>

![git_workflow](
  https://raw.githubusercontent.com/licesoares/docArquitetura-Kubernetes/master/img/git_workflow.png)

#### Linguagem de programação utilizadas
<p align="justify">
A maior parte do sistema é escrita na linguagem “Go”, essa linguagem foi criada pela Google, e é de código livre desde 2009. A linguagem em questão tem o objetivo de acelerar o desenvolvimento e manutenção de programas complexos. Seguem algumas de suas características:</p>

- *Programação concorrente/paralela nativa*: Não são usadas bibliotecas ou extensões para prover essas funcionalidades.
- *Desempenho*: Baseada na linguagem C, Go tem foco em desempenho sendo altamente otimizado.
- *Multiplataforma*: Linguagem possui suporte para Linux, Windows, MAC OS, FreeBSD e mobile.
- *Escalável*: Permite escalabilidade de forma quase transparente ao programador.
- *Compilado*: Linguagem do tipo Compilada que utiliza os compiladores gc e gccgo.
- *Garbage Collector nativo*: Incorporação de funcionalidade de linguagens de alto nível, de forma que o programador não precise se preocupar em limpar a memória utilizada.
- *Memory Safe*: Go possui gestão de memória e threads de forma transparente ao programador, fazendo a gestão automática evitanto problemas de alocação e invasão de memória.
- *Simples*: Com o foco em velocidade, vários recursos de linguagens de alto nível não estão presentes em Go, como Classes, Heranças, Overloads, Hierarquia de Tipos, Exceções e Ternários.

<p align="justify">
Apesar da linguagem Go não oferecer vários recursos considerados necessários para orientação a objetos, ela possui algumas características que a caracterizam nesse paradigma:
</p>

- *Estruturas*: Go não possui classes ou métodos mas possui Estruturas. Estruturas são tipos definidos pelo usuário, que podem conter métodos (se assemelhando a uma classe).

![Estruturas](
  https://raw.githubusercontent.com/licesoares/docArquitetura-Kubernetes/master/img/Estruturas.png)
  
Fonte: Arquivo healthcheck.go do pacote Proxy Kubernetes/Proxy/HealthCheck.


- *Métodos*: Os métodos em Go são funções que operam em tipos (Estruturas) específicos. 

![Metodos](
  https://raw.githubusercontent.com/licesoares/docArquitetura-Kubernetes/master/img/Metodos.png)
  
Fonte: Arquivo healthcheck.go do pacote Proxy Kubernetes/Proxy/HealthCheck.
- *Interfaces*: Interfaces em Go são tipos que declaram um conjunto de métodos, que assim como em outras linguagens, não possuem implementação. Objetos que implementam todos os métodos de uma interface, 'herdam' essa interface (de forma um pouco diferente, uma vez que Go não possui herança).

![interfaces](
  https://raw.githubusercontent.com/licesoares/docArquitetura-Kubernetes/master/img/interfaces.png)
  
Fonte: Arquivo config.go do pacote Proxy Kubernetes/Proxy/Config.

- *Encapsulamento*: Go encapsula coisas à nível de pacote. Nomes que começam com letra minúscula são visíveis apenas dentro do pacote.

![encapsulamento](
  https://raw.githubusercontent.com/licesoares/docArquitetura-Kubernetes/master/img/encapsulamento.png)
  
Fonte: Arquivo healthcheck.go do pacote Proxy Kubernetes/Proxy/HealthCheck.

<p align="justify">
Em bem menor escala, as linguagens Shell, Makefile , Protocol Buffer, YAML, HTML, Markdown e Python também são utilizadas na aplicação.
</p>

#### Vocabulário específico

- *Cluster*:<p align="justify"> Arquitetura de sistema capaz de combinar vários computadores para trabalharem em conjunto, sendo cada estação um nodo de uma rede formada pelo conjunto de computadores. No contexto de máquinas virtuais e containers, o nodo da rede pode ser cada container ou máquina virtual.</p>
- *Minions*: <p align="justify">É o nome dado para cada host do cluster.</p>
- *Kubelet*: <p align="justify">Agente que roda nos hosts do cluster.</p>
- *Pod*: <p align="justify">É a menor unidade dentro de um cluster. Nada mais é do que containers rodando dentro de seu cluster de Kubernetes. Pode ser um container rodando nginx, php, apache etc…</p>
- *Replication Controller*: <p align="justify">É o responsável por manter um número determinado de pods em execução. No RC é onde você diz quantos containers de nginx, php, apache você desejá que fiquem rodando; caso um caia, o RC cria outra instância automaticamente;</p>
- *Services*: <p align="justify">É o responsável por atrelar uma faixa de IP para um determinado RC. Para que cada vez que o RC crie uma nova instância de pod, o mesmo inicie com um IP determinado pelo service.</p>
- *Namespace*: <p align="justify">Com o namespace você pode dividir seu Cluster de Kubernetes em dois ambientes, Produção e Teste, podendo limitar os recursos computacionais para ambos.</p>
- *Docker*: <p align="justify">Plataforma Open Source escrita em Go que facilita a criação e administração de ambientes isolados (containers). O Docker possibilita o empacotamento de uma aplicação/ambiente criando uma imagem, e dessa forma, tornando essa aplicação/ambiente totalmente portável para qualquer outro host.</p>
- *Minikube*:<p align="justify"> Ferramenta que facilita a execução do Kubernetes localmente. O Minikube pode, por exemplo, rootear um cluster Kubernetes de um único nodo dentro de uma VM em um laptop. Ele também é capaz de executar uma imagem de container Docker localmente.</p>

#### Equipe de desenvolvimento

<p align="justify"> 
O Kubernetes é um sistema popular no GitHub, atualmente com 23.010 estrelas e 8.115 forks (11/05/2017), com 1.187 desenvolvedores ao redor do mundo. Para mostrar a evolução do desenvolvimento segue abaixo o gráfico de submissão de código de maio de 2015 até hoje:  
</p>


![grafic-commit](
  https://raw.githubusercontent.com/licesoares/docArquitetura-Kubernetes/master/img/grafic-commit.PNG)
   			  
Fonte:  https://github.com/kubernetes/kubernetes/graphs/commit-activity


<p align="justify"> 
Os principais contribuintes do sistema são Clayton Coleman, arquiteto e engenheiro de Software do Kubernetes, com 994 commits e o Brendan Burns, com 993 commits na aplicação. Outros vários desenvolvedores têm destaque na página com diversos commits e contribuições relevantes no código. 
</p><p align="justify"> 
Para guiar o desenvolvimento existem documentos sobre formas corretas de commits, bem como boas práticas de escrita de código, como pensar em nomes de variáveis e métodos, além de estruturas padrão de métodos, laços e etc.. Todo o desenvolvimento é passado por uma revisão de código antes de estar integrado a próxima release da ferramenta.
Apesar do Kubernetes tratar-se de um sistema de código aberto, o desenvolvimento de plugins ou outras ferramentas dessa natureza requer autorizações especiais.
</p>
                   
#### Evolução do sistema

<p align="justify">
Até hoje (21/05) foram lançadas mais de 240 releases, a última versão liberada foi a v1.6.4, no dia 19/05/2017. A versão v1.7 já está em modo alpha.4 de desenvolvimento. Para todas as versões existe a documentação de todas as modificações realizadas, bem como um link para o commit e revisão de código da correção/melhoria com uma descrição mais detalhada da alteração.
Segue abaixo um pouco sobre a evolução do sistema com algumas das principais versões já disponibilizadas:
</p>

- v1.2.0 – Lançado em 12 de março de 2016

<p align="justify">
Nesta versão foram implementadas melhorias significativas no sistema de escala, um aumento na escala de cluster em 400% representando 1000 nós com 30.000 pods por cluster. Além disso, a configuração passou a ser dinâmica, permitindo que a configuração dos aplicativos fosse armazenada como um objeto API Kubernetes e puxada dinamicamente na inicialização do container.</p>

<p align="justify">
A partir desta versão foi implementado também o Turnkey em modo Beta, que automatizou a implantação de atualizações do aplicativo, que agora são especificadas de forma declarativa. Esse app lida ainda com o controle de versão, permitindo vários lançamentos simultâneos, vinculando aos pods um status e mantendo a disponibilidade dos aplicativos.</p>

<p align="justify">
Os clusters do Kubernetes passaram a poder ocupar zonas dentro de um provedor de nuvem, o que significou a simplificação na forma de executar um contêiner em cada nó. </p>

<p align="justify">
A partir desta versão o Kubernetes pôde agendar serviços com documentação por log através de apenas um pod por nó.</p>

<p align="justify">
O Kubernetes ganhou também mais facilidade na integração em ambientes de rede personalizadas, suportando TLS para comunicação segura e roteamento de tráfego baseado em http.</p>

<p align="justify">
Um novo comando foi implementado para uma preparação de operaçoes como upgrades e ou manutenções do kernel, o comando “kubectl drain”.</p>

<p align="justify">
Foi implementada também uma interface mais amigável baseada em Material Design.</p>

![newgui](
  https://raw.githubusercontent.com/licesoares/docArquitetura-Kubernetes/master/img/newgui.png)

- v1.3.0 – Lançado em 1 de julho de 2016

<p align="justify">
Após diversas versões v1.2. e algumas versões alpha e beta da v1.3., a v1.3.0 foi lançada com alguns destaques. A partir desta versão o sistema ganhou autorização Alpha RBAC e todos os serviços de todos os clusters federados passaram a ser registrados na AWS e GCP. O Alpha PetSets passou a gerenciar aplicativos com status e a segurança foi reforçada. O Escalonador L7 LB e escalonadores de conexão de disco passaram a ser executados como master, evitando que nós precisem deste tipo de privilégio.</p>

<p align="justify">
O comando criado na versão anterior, “kubectl drain”, passou a poder apagar pods com armazenamento local. Uma exibição mais arrojada de erros foi implementada, em que o kubectl passou a exibir o número da linha em erro do JSON e a flag -t para indicar –type foi inserida.</p>

- v1.4.0 – Lançado em 26 de setembro de 2016

<p align="justify">
Nesta versão temas como UX foram abordados. A experiência do usuário passou a ser mais fácil, ficou mais simples obter um cluster e colocá-lo para rodar. Ficou mais fácil também entender um cluster, utilizando logs e padrões de API, e a capacidade de persistência do sistema foi aprimorada.</p>

<p align="justify">
Recursos de planejamento para escalonamento foram criados e o sistema ingressou nos clusters GCE e GKE de nível global https, com isso o suporte foi expandido para recursos federados de nuvem híbrida.</p>

<p align="justify">
No âmbito da segurança, houve um aumento da granularidade no nível do pod com políticas de imagens de contêiner, suporte a sysctl e API de revisão de acesso.</p>

- v1.5.0 – Lançado em 12 de dezembro de 2016

<p align="justify">
Dentre as atualizações mais significantes, esta versão trouxe novos comandos, suporte do Windows Server Container, implantação de cluster foi simplificada e o suporte a federação foi melhorado.</p>

- v.1.6.0 – Lançado em 28 de março de 2017

<p align="justify">
A partir desta versão, houve um crescimento ao suporte de nós para 5.000, utilizando etcd v3, que é habilitado por padrão. Uma versão beta da ferramenta bootstrap do cluster kubeandm também foi inserida e toda comunicação passou a ser sobre TLS.</p>

<p align="justify">
Um sistema de token de bootstrap passou a permitir gerenciamento de token e expiração. </p>

<p align="justify">
A interação com tempos de execução de contêineres agora é através da interface CRI, permitindo uma integração mais fácil dos tempos de execução com o kubelet. </p>

<p align="justify">
Novos recursos de programação entraram em modo beta, nesta versão é tornou-se possível usar vários agendadores e Nodes e Pods passaram a suportar afinidade e anti afinidade. Além disso, houve a implementação de um agendamento avançado para ser realizado com tolerâncias e a inserção de uma funcionalidade que permite que o usuário especifique por Pod por quanto tempo um Pod deve ficar vinculado a um nó quando existirem problemas à nível de nó.</p>


Referências utilizadas
--------------------

#### Frameworks

<p align="justify">
O Kubernetes possui uma API que visa facilitar a manipulação de objetos no sistema. Esses objetos são quaisquer unidades manipuláveis nos containers, como um nó, um Pod, um serviço, Namespace, etc. A API oferece uma linguagem declarativa e é extremamente poderosa, oferecendo abstração para o gerenciamento de domínios de objetos, controle de chamada e comportamento e concorrência de tarefa, além de validação das respostas recebidas nas chamadas feitas por objetos, classificando respostas com “Falha” ou “Inválida” em caso de erros. </p><p align="justify">
Além dessa API, o Kubernetes conta com uma API Server, que tem o objetivo de servir a API, sendo um servidor relativamente simples, com módulos bem definidos processando principalmente as operações de REST, Representational State Transfer. Essas operações visam  ignorar de implementação dos objetos e focar nos papéis dos objetos, nas restrições sobre sua interação com outros componentes e na sua interpretação de elementos de dados significantes. A API Server também possui o objetivo de garantir a sincronização dos componentes, inicialização assíncrona de recursos, consistência entre os objetos e atuar como um gateway para o Cluster. A API Server deve ser acessível para clientes fora do Cluster, ao contrário dos nós e containers, dessa forma, passando pela autenticação da API Server esses clientes podem acessar os nós e containers que não eram acessíveis.</p>

#### Ferramentas

<p align="justify">
O Kubernetes utiliza/pode utilizar diversas ferramentas para facilitar a utilização, manutenção e build do sistema. Abaixo seguem algumas indicadas pelo software: </p>

- *Godep*: Plataforma para estruturar o build fixando as dependências necessárias na compilação.
- *Aqua*: Ferramenta que auxilia na garantia da segurança dos containers no Kubernetes. Por meio dessa ferramenta é possível configurar facilmente segurança das imagens criadas, bem como quais e o número de usuários que podem acessar a imagem simultaneamente. Além disso, a ferramenta permite uma segmentação de rede que ‘particiona’ a segurança de diferentes aplicações em um mesmo cluster do Kubernetes, ou seja, caso várias aplicações rodem em um mesmo cluster e uma delas sofra um ataque, essa ferramenta impede que as aplicações vizinhas sejam infectadas.
- *Bitnami*: Ferramenta para auxiliar na compilação de blocos de um container, facilitando o building de blocos (aplicações) de um container e oferecendo modos de visualização gráfica de dados dos builds realizados.
- *Plugin RA CDE Kubernetes*: Este plugin auxilia na atualização automática de arquivos YAML utilizados no Kubernetes para especificações de configuração.
- *Canonical Distribution*: Ferramenta que possibilita a operação de clusters no Kubernets sob demanda, ou seja, geração de recurso para os containers de acordo com a necessidade do usuário.
- *Crunchy PostgreSQL Container Suite*: Conjunto de ferramentas para auxiliar na manutenção dos microserviços do PostgresSQL nos containers do Kubernets.
- *DataDog*: Ferramenta de monitoramento de serviços de infraestrutura, possibilitando alertas e análises de utilização de recursos.

<p align="justify">
Outras diversas ferramentas podem ser utilizadas, ligadas principalmente à gerenciamento de recursos, rede, build e segurança e estão disponíveis na página https://kubernetes.io/partners/. 
</p>

Arquitetura
--------------------

#### Visão de Processo

Segue abaixo a visão de Processo do Kubernetes e a descrição de cada componente.
 ![visao-processo](
  https://raw.githubusercontent.com/licesoares/docArquitetura-Kubernetes/master/img/visao-processo.PNG)

#### Componentes

<p align="justify">
Nó Master: Responsável por gerenciar o cluster do Kubernetes , sendo o ponto de entrada de todas as tarefas que são executadas. Sendo assim, o nó master cuida de orquestrar os nós de trabalho que estão sendo executados. Os principais componentes, são:
</p>

- *API Server*: Explicado no tópico Frameworks.
- *Etct (Cluster state store)*: <p align="justify">É um armazenamento de valor-chave , distribuído e consistente. É usado principalmente para configuração compartilhada de serviços. Ele fornece uma API REST para operações CRUD, bem como uma interface para registrar nós específicos, o que permite uma maneira confiável de notificar o restante do cluster sobre as alterações de configuração. Os dados armazenados pelo Kubernetes em etcd são os jobs agendado que são criados e implantados pelo pod/service, namespaces e informações de replicação, etc.</p>
- *Scheduler*: <p align="justify">O Scheduller gerencia a alocação de hosts e recursos para cada container. Após a criação de um Pod, por meio da API, o Scheduller verifica os recursos requisitados no Pod e o aloca à uma unidade do cluster. Sendo assim,a implantação de pods e serviços configurados nos nós acontece graças ao componente scheduler. O Scheduller tem as informações sobre os recursos disponíveis nos membros do cluster, bem como os necessários para que o serviço configurado seja executado e, portanto, possa decidir onde implantar um serviço específico.</p>
- *Controller Manager*: <p align="justify">Opcionalmente, você pode executar diferentes tipos de controladores dentro do nó master. O controlador usa apiserver para verificar o estado compartilhado do cluster e faz alterações corretivas para o estado atual para ser ficar no estado desejado. Um exemplo de controlador é de replicação, que cuida do número de pods do sistema. A replicação é configurada pelo usuário e essa é a responsabilidade do controlador de recriar um pod falhado ou remover um scheduler extra. Outros exemplos de controladores são o controlador de endpoints, o controlador de namespace e o controlador de service accounts. Sendo assim,a maioria das funções básicas à nível de cluster são executadas pelo Controller Manager. Ele executa funções relacionadas a coleta de lixo nos Pods, ciclo de vida de aplicações, escalonamento de recursos, roteamento, vinculação de serviços e provisionamento.</p>

<p align="justify">
Nó de trabalho: Os pods são executados neste nó onde contém todos os serviços necessários para gerenciar a rede entre os contêineres, comunicando com o nó mestre e atribuindo recursos aos contêineres. Os principais componentes são:</p>

- *Kubelet*:<p align="justify"> Kubelet obtém a configuração de um pod a partir do apiserver e garante que os containers estão em funcionamento. Este é o serviço do worker que é responsável pela comunicação com o nó master. Ele também se comunica com o etcd, para obter informações sobre serviços e escrever os detalhes sobre os recém-criados. Sendo assim , o kubelet é controlador da API dos pods e nós que controla toda a execução no container.</p>
- *Container Runtime*: <p align="justify">Cada nó executa um tempo de execução de container, ou seja, o Kubelet desconhece o tempo de execução do sistema recipiente. Isso ocorre para manter os limites dos containers claros, facilitando testes e ligações entre as aplicações.</p>
- *Kube Proxy*: <p align="justify">Solução para agrupamento de Pods com balanceamento de carga. Cada nó executa um kube-proxy que intercepta as chamadas de IP’s direcionando aos endereços corretos, equilibrando o tráfego entre clientes de um mesmo nó.</p>

#### Visão de desenvolvimento

<p align="justify">
O código do Kubernetes é extenso, mas é bem modularizado e cada arquivo de código, geralmente, não excede 300 linhas. Além disso, o código é bem comentado, tendo em toda função uma explicação sucinta do seu objetivo e comentários dentros das funções em operações mais complexas.</p>
<p align="justify">
Segue abaixo a visão de desenvolvimento do Kubernetes com todos os seus pacotes principais. Devido ao grande número de subpacotes existentes no código, eles não foram mapeados nesta representação. 
</p>

![visao-desenvolvimento](
  https://raw.githubusercontent.com/licesoares/docArquitetura-Kubernetes/master/img/visao-desenvolvimento.PNG)
  
- *API*: Pacote que contém o código da representação dos objetos Kubernetes em memória.
- *Capabilities*: <p align="justify">Código de gerenciamento de recursos à nível de sistema, este pacote provê diversas formas de configurações de privilégios, de forma que o usuário possa optar sob o nível/tipo de gerenciamento de recursos desejado no container.</p>
- *CloudProvider*: Fornece interfaces e implementações para provedores de serviços na nuvem, como balanceamento de carga, rotas e gerenciamento de hosts.
- *Controller*: <p align="justify">Código de controladores do sistema. No Kubernetes, um controlador é um loop de controle que observa o estado compartilhado do cluster através da APIServer e faz alterações tentando mover o estado atual para o estado desejado. Exemplos de controladores que acompanham Kubernetes hoje são o controlador de replicação, controlador de pontos de extremidade, controlador de namespace e controlador de contas de serviço.</p>
- *CredentialProvider*: Provê interfaces e implementações para esquema de autenticação de softwares de terceiros em um container.
- *FieldPath*: Fornece métodos para extrair atributos/campos de objetos dado um determinado caminho.
- *Generated*: Pacote para armazenamento de arquivos gerados automaticamente durante o build completo do sistema.
- *KubeApiServer*: <p align="justify">Pacote que armazena código comum da API Server, que não deve ser utilizado como código genérico da API. O módulo possui operações de validação e configuração de dados para os objetos api que incluem Pods, Services, ReplicationControllers e outros. Além disso, nessa parte do código ficam localizadas a implementação das operações de REST e o frontend do estado compartilhado do cluster através do qual todos os outros componentes interagem.</p>
- *KubeCtl*: Bibliotecas usadas para manipulação de ferramentas na linha de comando kubeclt.
- *KubeLet*: <p align="justify">Contém código responsável pelo gerenciamento de Pod à nível de Nó, que é executado em cada Nó de trabalho. O Kubelet é o principal "agente de nó" que é executado em cada nó. O kubelet funciona em termos de um PodSpec, que é um objeto YAML ou JSON que descreve um Pod. O kubelet tem um conjunto de PodSpecs que são fornecidos através de vários mecanismos (principalmente através da APIServer) e garante que os recipientes descritos nesses PodSpecs estão em execução e sem problemas com recursos. A implementação do kubelet não contempla o gerenciamento de contêineres que não foram criados pela Kubernetes.</p>
- *Master*: Este pacote é responsável por todo o código de configuração de execução do Nó Master, explicado na seção 3.1.
- *Probe*: Código de utilitários para verificação da utilização de recursos das aplicações no Nó.
- *Proxy*: Implementação do proxy de rede para comunicação transparente dos containers.
- *Registry*: Implementação do armazenamento e lógica do sistema da API Server.
- *Routes*: Pacote com uma coleção de rotas de tramitação http de pacotes.
- *Security*: Implementação de requisitos de segurança da API.
- *Util*: Implementação de métodos úteis que podem ser usados em qualquer outro pacote, este pacote, no entanto, não depende de nenhum pacote.
- *Version*: Pacote que contém informações da versão a ser gerada, informações gerais da última configuração de build para geração de nova versão.
- *Volume*: Armazena todo código referente a Volumes no Kubernetes, incluindo representações internas e código de montagem e desmontagem de volumes.

#### Visão Física

<p align="justify">
Como já foi explicado anteriormente,a ferramenta possui alguns conceitos específicos e sua arquitetura é elaborada para ser altamente escalável. Kubernetes possui uma unidade de controle chamada master server que executa vários serviços de uso exclusivo para o funcionamento do cluster. Toda a comunicação e configuração do cluster é realizada por meio do ETCD um armazenamento de chave-valor que salva o estado do cluster e compartilha entre os nós por meio de sua API HTTP/JSON. Cada minion possui um Docker em execução, além disso uma sub-rede privada dedicada à comunicação. Por meio da sub-rede temos rotas de tráfego para garantir o acesso a internet em todos os minions. 
</p>

![visao-fisica](
  https://raw.githubusercontent.com/licesoares/docArquitetura-Kubernetes/master/img/visao-fisica.PNG)
  

Referências
-----------

- https://kubernetes.io/
- https://github.com/kubernetes
- https://tour.golang.org
- https://infoslack.com/devops/introducao-ao-kubernetes
- http://fajlinux.com.br/devops/docker-cluster-com-o-kubernetes/
- http://www.tothenew.com/blog/understanding-kubernetes-architecture-and-setting-up-a-cluster-on-ubuntu/
- http://www.mundodocker.com.br/o-que-e-docker/

