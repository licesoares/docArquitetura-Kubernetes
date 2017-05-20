# Documentação Arquitetural do Sistema Kurbenetes
====================================

**Alunos:** Alice Soares, Luisa Helena, Maxmillian

**Professor:** Marco Túlio de Oliveira Valente

**Disciplina:** Engenharia de Software II

**Repositório Github:** https://github.com/kubernetes/kubernetes

Descrição do sistema
--------------------

#### Contexto
A utilização de máquinas virtuais atualmente é consolidada e auxilia no desenvolvimento de software em empresas e até para desenvolvedores individuais. Hoje existem diversas plataformas que permitem configurações dinâmicas de máquinas virtuais na nuvem que possibilitam a construção de ambientes de desenvolvimento escaláveis e padronizados a um valor acessível. No entanto, as aplicações que são executadas na máquina virtual compartilham os recursos de memória, disco rígido, bibliotecas, configurações e processos do Sistema Operacional hospedeiro, fazendo com que o teste de aplicações distintas precise considerar estes fatores. Os containers virtuais vêm resolver esta questão, eles promovem a virtualização a nível de sistema operacional encapsulando a aplicação e os recursos de memória, disco e rede requeridos por ela. Dessa forma, apesar de o Container e as máquinas virtuais trabalharem com virtualização e isolamento, os Containers criam ambientes isolados onde diferentes aplicações podem ser executadas simultaneamente.
