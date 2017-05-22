# Documentação Arquitetural do Sistema Kubenetes

**Alunos:** Alice Soares, Luisa Cunha e Maxmillian Araújo

**Professor:** Marco Túlio de Oliveira Valente

**Disciplina:** Engenharia de Software II

**Repositório Github:** https://github.com/kubernetes/kubernetes

Descrição do sistema
--------------------

#### Contexto
A utilização de máquinas virtuais atualmente é consolidada e auxilia no desenvolvimento de software em empresas e até para desenvolvedores individuais. Hoje existem diversas plataformas que permitem configurações dinâmicas de máquinas virtuais na nuvem que possibilitam a construção de ambientes de desenvolvimento escaláveis e padronizados a um valor acessível. No entanto, as aplicações que são executadas na máquina virtual compartilham os recursos de memória, disco rígido, bibliotecas, configurações e processos do Sistema Operacional hospedeiro, fazendo com que o teste de aplicações distintas precise considerar estes fatores. Os containers virtuais vêm resolver esta questão, eles promovem a virtualização a nível de sistema operacional encapsulando a aplicação e os recursos de memória, disco e rede requeridos por ela. Dessa forma, apesar de o Container e as máquinas virtuais trabalharem com virtualização e isolamento, os Containers criam ambientes isolados onde diferentes aplicações podem ser executadas simultaneamente.

#### Objetivo
O Kubernetes além de prover o escalonamento e execução de containers de aplicações em clusters de máquinas físicas ou virtuais, oferece uma infraestrutura centrada em container que permite construir ambientes de desenvolvimento centrados em containers.

#### Kubenertes
O Kubernetes satisfaz diversas necessidades comuns de aplicações:
- *Co-alocação de processos auxiliares*: O Kubernetes trabalha com o conceito de Pod, que é a menor unidade de computação que pode ser criada e gerenciada. Um Pod é um grupo de um ou mais containers, o armazenamento compartilhado entre eles e as opções de como executar este grupo.

- *Montagem de sistemas de armazenamento para persistência de dados*: Um container sempre é iniciado no estado “limpo”, a consequência disso é que caso um container falhe e seja reiniciado (o que ocorre automaticamente) os arquivos são perdidos. Outro problema é que na execução simultânea de containers de uma mesma aplicação é possível que seja necessário compartilhar recursos. Para resolver estes problemas o Kubernetes possui uma abstração de Volume.
- *Proteção à informação sensível*: O Kubernetes chama de ‘Secret’ um objeto que contém algum tipo de informação sensível, como uma senha ou token. 
- *Checagem da aplicação*: São providas configurações diversas de Debug, Logging, Monitoramento, Tasks, Jobs, etc. de forma que o usuário consiga monitorar o funcionamento e execução dos containers.
- *Replicação de instâncias*: Duplicação de instâncias de Pods garantindo alta disponibilidade das aplicações.
- *Dimensionamento automático horizontal*: Ajusta automaticamente o número de Pods em um controlador de replicação coincidindo com a utilização média de CPU observada.
- *Sistema de nomes*: O Kubernetes oferece serviço de DNS para atribuir nomes de DNS’s a serviços das aplicações.
- *Balanceamento de carga*: Pods são criados e destruídos dinamicamente de forma a não sobrecarregar a máquina.
- *Atualização Contínua*: Provê atualização individual de Pod, de modo que não seja necessário desativar todo o serviço ao mesmo tempo.
- *Monitoramento de Recursos*: Verificação de utilização de recursos a nível de Pod ou clusters inteiros.
- *Logging* : O Kubernetes permite logs das aplicações recipientes.
- *Segurança* : Níveis de autorização e autenticação para acesso às aplicações.

Kubernetes é de código aberto, está disponível no GitHub no link https://github.com/kubernetes/kubernetes e possui extensa documentação que pode ser acessada no link https://kubernetes.io/. Essa disponibilidade e documentação permite que os usuários vejam como toda a programação funciona, bem como os incentiva a criar novas funcionalidades ou melhorias que os ajudem em seus cenários. O sistema não limita os tipos de aplicativos suportados, não fornece middleware, estrutura de processamento de dados, bases de dados ou sistemas de armazenamento em cluster, apesar disso, é capaz de executar todos estes aplicativos.

#### Linguagem de programação utilizadas
A maior parte do sistema é escrita na linguagem “Go”, essa linguagem foi criada pela Google, e é de código livre desde 2009. A linguagem em questão tem o objetivo de acelerar o desenvolvimento e manutenção de programas complexos. Seguem algumas de suas características:
- *Programação concorrente/paralela nativa*: Não são usadas bibliotecas ou extensões para prover essas funcionalidades.
- *Desempenho*: Baseada na linguagem C, Go tem foco em desempenho sendo altamente otimizado.
- *Multiplataforma*: Linguagem possui suporte para Linux, Windows, MAC OS, FreeBSD e mobile.
- *Escalável*: Permite escalabilidade de forma quase transparente ao programador.
- *Compilado*: Linguagem do tipo Compilada que utiliza os compiladores gc e gccgo.
- *Garbage Collector nativo*: Incorporação de funcionalidade de linguagens de alto nível, de forma que o programador não precise se preocupar em limpar a memória utilizada.
- *Memory Safe*: Go possui gestão de memória e threads de forma transparente ao programador, fazendo a gestão automática evitanto problemas de alocação e invasão de memória.
- *Simples*: Com o foco em velocidade, vários recursos de linguagens de alto nível não estão presentes em Go, como Classes, Heranças, Overloads, Hierarquia de Tipos, Exceções e Ternários.

Apesar da linguagem Go não oferecer vários recursos considerados necessários para orientação a objetos, ela possui algumas características que a caracterizam nesse paradigma:
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

Em bem menor escala, as linguagens Shell, Makefile , Protocol Buffer, YAML, HTML, Markdown e Python também são utilizadas na aplicação.

#### Vocabulário específico

- *Cluster*: Arquitetura de sistema capaz de combinar vários computadores para trabalharem em conjunto, sendo cada estação um nodo de uma rede formada pelo conjunto de computadores. No contexto de máquinas virtuais e containers, o nodo da rede pode ser cada container ou máquina virtual.
- *Minions*: É o nome dado para cada host do cluster.
- *Kubelet*: Agente que roda nos hosts do cluster.
- *Pod*: É a menor unidade dentro de um cluster. Nada mais é do que containers rodando dentro de seu cluster de Kubernetes. Pode ser um container rodando nginx, php, apache etc…
- *Replication Controller*: É o responsável por manter um número determinado de pods em execução. No RC é onde você diz quantos containers de nginx, php, apache você desejá que fiquem rodando; caso um caia, o RC cria outra instância automaticamente;
- *Services*: É o responsável por atrelar uma faixa de IP para um determinado RC. Para que cada vez que o RC crie uma nova instância de pod, o mesmo inicie com um IP determinado pelo service.
- *Namespace*: Com o namespace você pode dividir seu Cluster de Kubernetes em dois ambientes, Produção e Teste, podendo limitar os recursos computacionais para ambos.
- *Docker*: Plataforma Open Source escrita em Go que facilita a criação e administração de ambientes isolados (containers). O Docker possibilita o empacotamento de uma aplicação/ambiente criando uma imagem, e dessa forma, tornando essa aplicação/ambiente totalmente portável para qualquer outro host.
- *Minikube*: Ferramenta que facilita a execução do Kubernetes localmente. O Minikube pode, por exemplo, rootear um cluster Kubernetes de um único nodo dentro de uma VM em um laptop. Ele também é capaz de executar uma imagem de container Docker localmente.

#### Equipe de desenvolvimento
O Kubernetes é um sistema popular no GitHub, atualmente com 23.010 estrelas e 8.115 forks (11/05/2017), com 1.187 desenvolvedores ao redor do mundo. Para mostrar a evolução do desenvolvimento segue abaixo o gráfico de submissão de código de maio de 2015 até hoje:  
  ![grafic-commit](
  https://raw.githubusercontent.com/licesoares/docArquitetura-Kubernetes/master/img/grafic-commit.PNG)
   			  
Fonte:  https://github.com/kubernetes/kubernetes/graphs/commit-activity

Os principais contribuintes do sistema são Clayton Coleman, arquiteto e engenheiro de Software do Kubernetes, com 994 commits e o Brendan Burns, com 993 commits na aplicação. Outros vários desenvolvedores têm destaque na página com diversos commits e contribuições relevantes no código. 
Para guiar o desenvolvimento existem documentos sobre formas corretas de commits, bem como boas práticas de escrita de código, como pensar em nomes de variáveis e métodos, além de estruturas padrão de métodos, laços e etc.. Todo o desenvolvimento é passado por uma revisão de código antes de estar integrado a próxima release da ferramenta.
Apesar do Kubernetes tratar-se de um sistema de código aberto, o desenvolvimento de plugins ou outras ferramentas dessa natureza requer autorizações especiais.

                   
#### Evolução do sistema
Até hoje (21/05) foram lançadas mais de 240 releases, a última versão liberada foi a v1.6.4, no dia 19/05/2017. A versão v1.7 já está em modo alpha.4 de desenvolvimento. Para todas as versões existe a documentação de todas as modificações realizadas, bem como um link para o commit e revisão de código da correção/melhoria com uma descrição mais detalhada da alteração.

Segue abaixo um pouco sobre a evolução do sistema com algumas das principais versões já disponibilizadas:

- v1.2.0 – Lançado em 12 de março de 2016

Foram inseridas diversas melhorias no sistema desde a versão V1.1.1. Um suporte ao Ubuntu foi adicionado e algumas características experimentais foram implantadas. As mudanças mais significativas estão no aumento da escala de cluster, que reduziram a sobrecarga do sistema em 4 vezes, e a implantação do turnkey, API para automatizar a atualização permitindo lançamentos simultâneos e visualização de status. Além disso, o gerenciamento de clusters também foi automatizado.

- v1.3.0 – Lançado em 1 de julho de 2016

A versão V1.3.0 foi lançada como V1.3.0-alpha.1 até V1.3.0-alpha.5, em seguida V1.3.0-beta.1 até V1.3.0-beta.3, todas com atualizações de funcionalidades e correções de erros. Dentre as implantações nesta versão estão os registros dos clusters federados em nuvem AWS e GCP e atualizações de segurança e autenticação.

- v1.4.0 – Lançado em 26 de setembro de 2016

Com esta versão houveram melhorias na experiência do usuário que simplificaram como obter e entender um cluster. Foi implantado suporte a aplicações e os recursos de persistência foram aprimorados. Em Federação de cluster aconteceu a entrada global multi-cluster htttp através do GCE e GKE Clusters. A segurança foi aumentada com api de revisão de acesso e políticas de imagem de container.

- v1.5.0 – Lançado em 12 de dezembro de 2016

Dentre as atualizações mais significantes, esta versão trouxe novos comandos, suporte do Windows Server Container, implantação de cluster foi simplificada e o suporte a federação foi melhorado.

- v.1.6.0 – Lançado em 28 de março de 2017

Kubernetes agora suporta até 5.000 nós via etcd v3, que é habilitado por padrão. O controle de acesso baseado em funções (rbac) foi graduado para beta e define funções de padrão seguro para o plano de controle, o nó e os componentes do controlador. A ferramenta bootstrap do cluster kubeadm se graduou para beta. Esta versão foi lançada com um problema que faz com o que a aplicação pare que foi corrigida na versão v.1.6.1. Toda a comunicação está agora sobre tls. Plugins de autorização podem ser instalados pelo kubeadm, incluindo o novo padrão de rbac. O sistema de token bootstrap agora permite gerenciamento de token e expiração. A interação com os tempos de execução do recipiente é agora através da interface cri, permitindo uma integração mais fácil dos tempos de execução com o kubelet. Docker permanece o tempo de execução padrão via docker-cri. Tornou-se possível utilizar vários escalonadores e os recursos de armazenamento foram atualizados.


Referências utilizadas
--------------------

#### Frameworks
O Kubernetes possui uma API que visa facilitar a manipulação de objetos no sistema. Esses objetos são quaisquer unidade manipuláveis nos containers, como um nó, um Pod, um serviço, Namespace, etc. A API oferece uma linguagem declarativa e é extremamente poderosa, oferecendo abstração para o gerenciamento de domínios de objetos, controle de chamada e comportamento e concorrência de tarefa, além de validação das respostas recebidas nas chamadas feitas por objetos, classificando respostas com “Falha” ou “Inválida” em caso de erros. 
Além dessa API, o Kubernetes conta com uma API Server, que tem o objetivo de servir a API, sendo um servidor relativamente simples, com módulos bem definidos processando principalmente as operações de REST, Representational State Transfer. Essas operações visam  ignorar de implementação dos objetos e focar nos papéis dos objetos, nas restrições sobre sua interação com outros componentes e na sua interpretação de elementos de dados significantes. A API Server também possui o objetivo de garantir a sincronização dos componentes, inicialização assíncrona de recursos, consistência entre os objetos e atuar como um gateway para o Cluster. A API Server deve ser acessível para clientes fora do Cluster, ao contrário dos nós e containers, dessa forma, passando pela autenticação da API Server esses clientes podem acessar os nós e containers que não eram acessíveis.

#### Ferramentas
O Kubernetes utiliza/pode utilizar diversas ferramentas para facilitar a utilização, manutenção e build do sistema. Abaixo seguem algumas indicadas pelo software: 
- *Godep*: Plataforma para estruturar o build fixando as dependências necessárias na compilação.
- *Aqua*: Ferramenta que auxilia na garantia da segurança dos containers no Kubernetes. Por meio dessa ferramenta é possível configurar facilmente segurança das imagens criadas, bem como quais e o número de usuários que podem acessar a imagem simultaneamente. Além disso, a ferramenta permite uma segmentação de rede que ‘particiona’ a segurança de diferentes aplicações em um mesmo cluster do Kubernetes, ou seja, caso várias aplicações rodem em um mesmo cluster e uma delas sofra um ataque, essa ferramenta impede que as aplicações vizinhas sejam infectadas.
- *Bitnami*: Ferramenta para auxiliar na compilação de blocos de um container, facilitando o building de blocos (aplicações) de um container e oferecendo modos de visualização gráfica de dados dos builds realizados.
- *Plugin RA CDE Kubernetes*: Este plugin auxilia na atualização automática de arquivos YAML utilizados no Kubernetes para especificações de configuração.
- *Canonical Distribution*: Ferramenta que possibilita a operação de clusters no Kubernets sob demanda, ou seja, geração de recurso para os containers de acordo com a necessidade do usuário.
- *Crunchy PostgreSQL Container Suite*: Conjunto de ferramentas para auxiliar na manutenção dos microserviços do PostgresSQL nos containers do Kubernets.
- *DataDog*: Ferramenta de monitoramento de serviços de infraestrutura, possibilitando alertas e análises de utilização de recursos.

Outras diversas ferramentas podem ser utilizadas, ligadas principalmente à gerenciamento de recursos, rede, build e segurança e estão disponíveis na página https://kubernetes.io/partners/. 


Arquitetura
--------------------

#### Visão de Processo

Segue abaixo a visão de Processo do Kubernetes e a descrição de cada componente.
 ![visao-processo](
  https://raw.githubusercontent.com/licesoares/docArquitetura-Kubernetes/master/img/visao-processo.PNG)

#### Componentes
Nó Master: Responsável por gerenciar o cluster do Kubernetes , sendo o ponto de entrada de todas as tarefas que são executadas. Sendo assim, o nó master cuida de orquestrar os nós de trabalho que estão sendo executados. Os principais componentes, são:
- *API Server*: Explicado no tópico Frameworks.
- *Etct (Cluster state store)*: É um armazenamento de valor-chave , distribuído e consistente. É usado principalmente para configuração compartilhada de serviços. Ele fornece uma API REST para operações CRUD, bem como uma interface para registrar nós específicos, o que permite uma maneira confiável de notificar o restante do cluster sobre as alterações de configuração. Os dados armazenados pelo Kubernetes em etcd são os jobs agendado que são criados e implantados pelo pod/service, namespaces e informações de replicação, etc.
- *Scheduler*: O Scheduller gerencia a alocação de hosts e recursos para cada container. Após a criação de um Pod, por meio da API, o Scheduller verifica os recursos requisitados no Pod e o aloca à uma unidade do cluster. Sendo assim,a implantação de pods e serviços configurados nos nós acontece graças ao componente scheduler. O Scheduller tem as informações sobre os recursos disponíveis nos membros do cluster, bem como os necessários para que o serviço configurado seja executado e, portanto, possa decidir onde implantar um serviço específico.
- *Controller Manager*: Opcionalmente, você pode executar diferentes tipos de controladores dentro do nó master. O controlador usa apiserver para verificar o estado compartilhado do cluster e faz alterações corretivas para o estado atual para ser ficar no estado desejado. Um exemplo de controlador é de replicação, que cuida do número de pods do sistema. A replicação é configurada pelo usuário e essa é a responsabilidade do controlador de recriar um pod falhado ou remover um scheduler extra. Outros exemplos de controladores são o controlador de endpoints, o controlador de namespace e o controlador de service accounts. Sendo assim,a maioria das funções básicas à nível de cluster são executadas pelo Controller Manager. Ele executa funções relacionadas a coleta de lixo nos Pods, ciclo de vida de aplicações, escalonamento de recursos, roteamento, vinculação de serviços e provisionamento.

Nó de trabalho: Os pods são executados neste nó onde contém todos os serviços necessários para gerenciar a rede entre os contêineres, comunicando com o nó mestre e atribuindo recursos aos contêineres. Os principais componentes são:
- *Kubelet*: Kubelet obtém a configuração de um pod a partir do apiserver e garante que os containers estão em funcionamento. Este é o serviço do worker que é responsável pela comunicação com o nó master. Ele também se comunica com o etcd, para obter informações sobre serviços e escrever os detalhes sobre os recém-criados. Sendo assim , o kubelet é controlador da API dos pods e nós que controla toda a execução no container.
- *Container Runtime*: Cada nó executa um tempo de execução de container, ou seja, o Kubelet desconhece o tempo de execução do sistema recipiente. Isso ocorre para manter os limites dos containers claros, facilitando testes e ligações entre as aplicações.
- *Kube Proxy*: Solução para agrupamento de Pods com balanceamento de carga. Cada nó executa um kube-proxy que intercepta as chamadas de IP’s direcionando aos endereços corretos, equilibrando o tráfego entre clientes de um mesmo nó.

#### Visão de desenvolvimento
Segue abaixo a visão de desenvolvimento do Kubernetes com todos os seus pacotes principais. Devido ao grande número de subpacotes existentes no código, eles não foram mapeadas nesta representação. 

![visao-desenvolvimento](
  https://raw.githubusercontent.com/licesoares/docArquitetura-Kubernetes/master/img/visao-desenvolvimento.PNG)
  
- *API*: Pacote que contém o código da representação dos objetos Kubernetes em memória.
- *Capabilities*: Código de gerenciamento de recursos à nível de sistema.
- *CloudProvider*: Fornece interfaces e implementações para provedores de serviços na nuvem.
- *Controller*: Código de controladores do sistema.
- *CredentialProvider*: Provê interfaces e implementações para esquema de autenticação de softwares de terceiros em um container.
- *FiedPath*: Fornece métodos para extrair atributos/campos de objetos dado um determinado caminho.
- *Generated*: Pacote para armazenamento de arquivos gerados automaticamente durante o build completo do sistema.
- *KubeApiServer*: Pacote que armazena código comum da API Server, que não deve ser utilizado como código genérico da API.
- *KubeCtl*: Bibliotecas usadas para manipulação de ferramentas na linha de comando kubeclt.
- *KubeLet*: Contém código responsável pelo gerenciamento de Pod à nível de Nó, que é executado em cada Nó de trabalho.
- *Master*: Este pacote é responsável por todo o código de configuração de execução do Nó Master, explicado na seção 3.1.
- *Probe*: Código de utilitários para verificação da utilização de recursos das aplicações no Nó.
- *Proxy*: Implementação do proxy de rede para comunicação transparente dos containers.
- *Registry*: Implementação do armazenamento e lógica do sistema da API Server.
- *Routes*: Pacote com uma coleção de rotas de tramitação http de pacotes.
- *Security*: Implementação de requisitos de segurança da api.
- *Util*: Implementação de métodos úteis que podem ser usados em qualquer outro pacote, este pacote, no entanto, não depende de nenhum pacote.
- *Version*: Pacote que contém informações da versão a ser gerada, informações gerais da última configuração de build para geração de nova versão.
- *Volume*: Armazena todo código referente a Volumes no Kubernetes, incluindo representações internas e código de montagem e desmontagem de volumes.

#### Visão Física
Como já foi explicado anteriormente,a ferramenta possui alguns conceitos específicos e sua arquitetura é elaborada para ser altamente escalável. Kubernetes possui uma unidade de controle chamada master server que executa vários serviços de uso exclusivo para o funcionamento do cluster. Toda a comunicação e configuração do cluster é realizada por meio do ETCD um armazenamento de chave-valor que salva o estado do cluster e compartilha entre os nós por meio de sua API HTTP/JSON. Cada minion possui um Docker em execução, além disso uma sub-rede privada dedicada à comunicação. Por meio da sub-rede temos rotas de tráfego para garantir o acesso a internet em todos os minions. 

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

