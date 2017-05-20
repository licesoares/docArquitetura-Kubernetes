# Documentação Arquitetural do Sistema Kubenetes


**Alunos:** Alice Soares, Luisa Helena, Maxmillian

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
A maior parte do sistema é escrita na linguagem “Go”, essa linguagem foi criada pela Google, e é de código livre desde 2009. A linguagem em questão tem sintaxe parecida com C e é uma linguagem do tipo Compilada, tem foco em eficiência e seu ponto forte é a programação concorrente. 
Em bem menor escala, as linguagens Shell, Makefile , Protocol Buffer, YAML, HTML, Markdown e Python também são utilizadas na aplicação.

#### Equipe de desenvolvimento
O Kubernetes é um sistema popular no GitHub, atualmente com 23.010 estrelas e 8.115 forks (11/05/2017), com 1.187 desenvolvedores ao redor do mundo. Para mostrar a evolução do desenvolvimento segue abaixo o gráfico de submissão de código de maio de 2015 até hoje:


#### Evolução do sistema
