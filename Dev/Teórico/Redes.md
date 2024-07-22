# Linha do tempo

## Década de 50

- Inicialmente os sistemas de computação eram `*únicos, centralizados e de grande porte.*`
- Operadas por pessoas `*muito especializadas`.*
- Usuário submetia um cartão com o `*job*` para o operador, e quando houvesse disponibilidade o cartão era submetido à máquina.
- Todo esse processo era feito em `*batch*` , ou seja, sem interação usuário - máquina.
- Resposta demorava muito.

## Década de 60

- Primeiros terminais interativos, acabando com o `*batch*`
- Surgiram sistemas de tempo compartilhado (`*time sharing*`) - vários terminais eram ligados à uma máquina `*mainframe*` que executava os serviços.
- sistemas multitarefa

## Década de 70

- Surge mini computadores com bom desempenho mas `*sem requisitos tão rígidos de temperatura e umidade.*`
- Base computacional espalhados com esses micro computadores, `*assim distribuindo esse processamento.*`
- Migração do `*mainframe para os microcomputadores.*`
- Periféricos caros - ou seja, sem impressora e afins.
- Problema de sincronia de informações dado à descentralização das informações. `*Necessidade de interligação dessas informações.*`

## Arquiteturas

Umas das arquiteturas propostas e muito utilizadas até mesmo nos dias de hoje é a `*Von Neumann*`. As Instruções são executadas sequencialmente. Tanto as instruções quanto os dados resultantes dela ficam na memória, o que faz com que a velocidade de acesso à ela seja mais baixo.

Para contornar as limitações da arquitetura `*Von neumann*`, foram propostas:

- Sistemas UCP - unidade central de processamento - com múltiplas unidades funcionais, possibilitando o paralelismo.
- Máquinas pipeline
- Array Processors

## Evolução

Evoluindo ainda mais o sistema, começam a ser utilizados `*sistemas multiprocessados fortemente acoplados` .* Ou seja, um sistema era composto por vários elementos de processamento que compartilhavam a memória.

Surge também `*sistemas fracamente acoplados`. `Computadores independentes que trabalham de forma coordenada.`* As primeiras redes de computadores.

## Vantagens x Desvantagens de multiprocessados

- Vantagens
    
    - Custo por desempenho
    - tempo de resposta melhor
    - modularidade
    - confiabilidade
- Desvantagens
    
    - Desenvolvimento mais complexo e mais caro
    - Decomposição de tarefas é complexo
    - depende de tecnologia de comunicação devida a alta demanda de tráfego de comunicação
    
    Uma máquina de arquitetura distribuída é composta por um conjunto de `*módulos autônomos de processamento interconectados*`. Necessita de um `*sistema operacional único para fazer seu gerenciamento.`*
    
    <aside> 💡 Não confundir `*máquina de arquitetura distribuída*` com `*redes de computadores.*` Enquanto o primeiro os módulos não são independentes, no segundo os módulos trabalham de forma autônoma e independente.
    
    </aside>
    
    As redes de computadores se tornam essenciais hoje em dia principalmente para extrair e correlacionar informações.
    
    ## Aplicações
    
- Realização de negócios eletrônicos
- Comércio eletrônico
- Aplicações pessoais: acessar internet
- **Servidor de arquivos**
    
    - Oferecer aos equipamentos conectados à rede um serviço de armazenamento de informações e compartilhamento de discos.
    - Garantir integridade de dados
    - Pode ser implementado das seguintes formas:
        - Sistema do usuário é alterado para que o sistema de arquivos seja visto como extensão do proprio sistema de arquivos.
        - Intermédio de utilitários: acessam arquivos do servidor, exemplos hoje em dia é o dropbox e google.
        - O usuário final acessa o servidor através de primitivas, via rede.
- `*Servidor de impressão*`
    
    - Oferece o serviços de impressão.
- `*Compartilhamento de software*`
    
    - Um dos fatores mais problemáticos na manutenção de um sistema é a atualização das licenças de software.
    - Com a rede, pode se adquirir um número menor de licencas e elas serem compartilhadas através do servidor.
- `*Servidor de banco de dados*`
    
    - Consultar e gerar informações. A grande diferença de um sistema de arquivos para um banco de dados é a possibilidade de consultar informações mais complexas de uma forma mais performática.
    - Além disso, com o sistema de arquivos, para que as consultas ocorram todo os arquivos são enviados pela rede para que aconteca essa consulta, o que deixa a conexão muito mais lenta dessa rede.
    - Com o banco de dados, a consulta é enviada para um servidor do banco, que vai realizar essa consulta localmente no servidor e retornar apenas os dados necessários.
- `*Gerenciamento eletrônico de documentos*`
    
    - Tecnologia que provê um meio de gerar, controlar, armazenar e compartilhar informações existentes.
    - Sistemas GED permitem aos usuários acessar documentos de forma ágil e segura.
    - Mais organizado.
    
    # Modelo Cliente - Servidor
    
    Os dados são armazenados em computadores não operados chamados servidores. Os funcionários são clientes desse servidor onde acessam para capturar seus dados remotamente.
    
    Nosso modelo, há dois `*processos*` envolvidos: um no cliente e um no servidor.
    
    - O cliente envia uma mensagem pela rede ao processo servidor.
    - O processo cliente aguarda esse processo.
    - O processo servidor recebe a solicitação, executa o trabalho solicitado e envia de volta uma resposta.

<aside> 💡 Também é possível que um sistema possua simultaneamente processos clientes e processos servidores.

</aside>

# Resumo

- O que são redes de computadores:
    - Formada por um `*conjunto de módulos processadores capazes de trocar informações*` e compartilhar recursos, interligados por um sistema de comunicação.
- O que são sistemas de comunicação:
    - `*Arranjo*` topológico `*interligando os vários módulos através de enlaces físicos*` - meios de transmissão - `*e um conjunto protocolos.*`

# Tipo de rede

Dois tipos, de vários, se destacam:

- Escala
- Tecnologia de transmissão

# Sobre Tecnologia de transmissão

Há dois tipos de tecnologia de transmissão:

- Redes de Difusão - broadcasting
- Redes ponto a ponto

## Redes de Difusão - broadcasting

- Possuem apenas um único canal de comunicação, compartilhado com todos os hospedeiros.
- Mensagens enviadas por um dos hospedeiros são recebidas por todos os demais.

## Redes ponto a ponto

- Possui conexões a pares individuais de hospedeiros.
- Para ir da origem ao destino um pacote pode ter que visitar um ou mais hospedeiros intermediários.
- Algoritmos de roteamento desempenham um importante papel nas redes ponto a ponto.

# Sobre Escala

Podem ser classificadas:

- Redes locais (LAN)
    - Redes privadas contidas em um único edifício ou campus.
    - Muito utilizadas para conectar computadores pessoais ou estações de trabalho.
- Redes metropolitanas (MAN):
    - Versão ampliada da LAN.
    - Pode vir a abranger uma cidade inteira.
    - Podem ser publicas ou privadas,
    - Capaz de transportar dados, voz e video.
    - Prove interligação de redes.
- Redes geograficamente distribuídas
    - Abrange um país ou até mesmo um continente.
    - Maioria das WANs a sub-rede consiste em dois componentes:
        - Linha de Transmissão*
        - Elementos de comutação**
    - Conjunto de linhas e roteadores forma uma sub-rede

- O que fazem as linhas de transmissão?

Transportam os bits entre os equipamentos.

** O que são equipamentos de comutação?

Equipamentos que se conectam três ou mais linhas de transmissão.

Principais modelos:

- Interconexão de sistemas: como o bluetooth
- LANs sem fio: como os nossos wifis
- WANs sem fio