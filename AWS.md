## O que é cloud
- Modelos de Computacao
  - On Premise
  - Hybrid
  - Cloud (or as refered by the exam, Public)
- Vantagens
  - Despesas variaveis & Otimizacao de custos
  - Capacidade & Economia de escalas
  - Rapidez & Agilidade
- Infraestrutura global AWS: Regioes, Zonas de Disponibilidades e Locais de Borda
  - Conformidade com a governanca de dados e requisitos legais
  - Proximidade com clientes
  - Precificacao
  - Servicos disponiveis
- Interagir com servicos
  - Console de gerenciamento
  - AWS CLI
  - SDKs
- Abstraction
  - IaaS
  - PaaS
  - SaaS
- Infrastructure as Code
- Disaster Recovery
  - Recovery Point Objective (RPO)
    - tempo máximo aceitável desde o último ponto de recuperação de dados
  - Recovery Time Objective (RTO)
    - atraso máximo aceitável entre a interrupção do serviço e sua restauração
  - Estratégias
    - Backup and Restore
      - RPO e RTO alto
      - Mantem tudo em backup
      - Mais barato
    - Pilot Light
      - RPO mais baixo e RTO um pouco mais baixo
      - Mantem serviços core ativos (DB, por exemplo)
    - Warm Standby 
      - RTO muito mais baixo
      - Mantem um pedaço de serviços sempre ativos, apenas necessitando de redirecionamento
    - Multi site 
      - Reduz tendendo a zero o RTO e RPO
      - Processamento é executado simultaneamente em várias regiões
      - Mais caro

## Services

### Computing

#### EC2

O Amazon Elastic Compute Cloud (Amazon EC2) oferece uma capacidade de computação escalável sob demanda na Nuvem Amazon Web Services (AWS). O uso do Amazon EC2 reduz os custos de hardware para que você possa desenvolver e implantar aplicações com mais rapidez. É possível usar o Amazon EC2 para executar quantos servidores virtuais forem necessários, configurar a segurança e as redes e gerenciar o armazenamento. Você pode adicionar capacidade (aumentar a escala verticalmente) para lidar com tarefas de computação pesada, como processos mensais ou anuais ou picos no tráfego do site. Quando o uso diminui, você pode reduzir a capacidade (reduzir a escala verticalmente) de novo.


- Raw computing unit
- More control over processing
- Can be used for database
- Can be used for containers

##### Resources

O Amazon EC2 fornece os seguintes recursos de alto nível:

- Instâncias
- Imagens de máquina da Amazon (AMIs)
- Tipos de instância
- Pares de chaves
- Volumes de armazenamento de instâncias (temporarios)
- Volumes do Amazon EBS
- Regiões, zonas de disponibilidade, zonas locais, AWS Outposts e zonas do Wavelength
- Grupos de segurança
- Endereços IP elásticos (estáticos para computação em nuvem dinâmica. Tem cobrança adicional. Especifico para a conta. Associado a qualquer VPC por vez. Pode-se usar NAT para preservar o limite de 5 IPs por regiao)
- Tags
- Nuvens privadas virtuais (VPCs)

##### Instances

###### By Hardware

- Quando executa uma instância, o tipo de instância que você especifica determina o hardware do computador host usado para sua instância
- Cada tipo de instância oferece recursos de computação, memória e armazenamento diferentes, além de ser agrupado em famílias de instâncias de acordo com esses recursos

Convenção de nome:
1. Instance family
   - Instance generation
1. Processor family
1. Additional capability
1. Instance size

https://docs.aws.amazon.com/pt_br/AWSEC2/latest/UserGuide/instance-types.html

- **Uso geral**: M6a, M6g, M6gd, M6i, M6id, M6idn, M6in, M7a, M7g, M7gd, M7i, M7i-flex e T4g
- **Otimizadas para computação**: C6a, C6g, C6gd, C6gn, C6i, C6id, C6in, C7a, C7g, C7gd, C7gn, C7i, Hpc6a, Hpc7a, Hpc7g
- **Computação acelerada**: DL2q, G5g, Inf2, P5, Trn1, Trn1n
- **Otimizadas para memória**: Hpc6id, R6a, R6g, R6gd, R6i, R6id, R6idn, R6in, R7a, R7g, R7gd, R7i, R7iz, X2gd, X2idn, X2iedn
- **Otimizadas para armazenamento**: I4g, I4i, Im4gn, Is4gen

###### By Price

- On-Demand
  - pagamento por segundos. Não há compromisso de longo prazo ao comprar Instâncias on-demand
  - você tem pleno controle sobre o ciclo de vida da instância: quando executar, interromper, hibernar, iniciar, reiniciar ou encerrá-la.
  - recomenda-se o uso de Instâncias on-demand para aplicações com workloads de curto prazo e irregulares que não podem ser interrompidas.
- Spot instances
  - are good for short term requirements as they can be very economical. However, you may find that the instance is terminated if the spot market price moves
  - Uma instância spot é uma instância que usa capacidade adicional do EC2 que está disponível por um valor mais baixo que o preço sob demanda
  - As Instâncias spot são uma opção econômica se houver flexibilidade quanto ao momento em que as aplicações serão executadas e se as aplicações poderão ser interrompidas
- Reserved instances
  - are good for long-term, static requirements as you must lock-in for 1 or 3 years in return for a decent discount
  - As instâncias reservadas não são instâncias físicas, mas um desconto na fatura aplicado na sua conta pelo uso de instâncias sob demanda
- Dedicated instances
  - Por padrão, as instâncias EC2 são executadas em hardware de locação compartilhada. As instâncias dedicadas são instâncias EC2 executadas em um hardware dedicado a um único cliente. As instâncias dedicadas que pertencem a diferentes Contas da AWS são isoladas fisicamente em nível de hardware, mesmo que essas contas estejam vinculadas a uma única conta pagante. No entanto, as instâncias dedicadas podem compartilhar o hardware com outras instâncias da mesma Conta da AWS que não sejam instâncias dedicadas.
- Dedicated host
  - Um Host dedicado também é um servidor físico que é dedicado para seu uso. Com um Host dedicado, você tem visibilidade e controle sobre como as instâncias são colocadas no servidor

##### Life Cycle

##### Auto Scaling

Automaticamente provisiona scale out (horizontal) de instancias EC2.

###### Auto Scaling Group

An Auto Scaling group contains a collection of EC2 instances that are treated as a logical grouping for the purposes of automatic scaling and management. An Auto Scaling group also lets you use Amazon EC2 Auto Scaling features such as health check replacements and scaling policies.

##### Amazon Machine Images

Os modelos pré-configurados para suas instâncias que empacotam os componentes de que você precisa para seu servidor (incluindo o sistema operacional e software adicional).

Uma Imagem de máquina da Amazon (AMI) é uma imagem compatível e mantida pela AWS, que fornece as informações necessárias para iniciar uma instância. Especifique uma AMI ao iniciar uma instância. Uma AMI inclui um ou mais snapshots do Amazon Elastic Block Store (Amazon EBS) ou, para AMIs com suporte de armazenamento de instâncias, um modelo para o volume raiz da instância (por exemplo, um sistema operacional, um servidor da aplicação e aplicações).

É possível criar ou utilizar uma imagem.

##### Storage Diagram

![](architecture_storage.png)

##### Network Diagram

![](ec2-basic-arch.png)

#### Outposts

O AWS Outposts é uma família de soluções totalmente gerenciadas que fornecem infraestrutura e serviços da AWS para praticamente qualquer local da borda ou on-premises. As soluções do Outposts permitem que os clientes estendam e executem serviços da AWS nativos on-premises e estão disponíveis em uma variedade de formatos.

Executa alguns produtos da AWS localmente e se conecta a uma ampla gama de serviços disponíveis na região local da AWS.
Possui Infraestrutura gerenciada.

Casos de uso
- Computação de baixa latência
- Migração e modernização
- Residência de dados
- Processamento local de dados

Options:
- Servers
- Racks

#### Containers
- Elastic Container Registry
  - Manage and store container images
- Elastic Container Service
- Elastic Kubernetes Service

#### Serverless
- Lambda
  - Event based functions (low-code)
- Fargate
  - Automatic managed containers, network and scalling
- Elastic Beanstalk
  - Fully managed deployment, provisioning, load balacing, auto scaling, monitoring and management of web code

#### Others

- Wavelength: Deploy computers in wavelenght zones (5G) for ultra low latency
- Batch: Trabalhos otimizados em lote, para Big Data, Execuções Repetidas (Finance Processing), ou ML, por exemplo
- Lightsail: ????

### Storage

#### Simple Storage Service (S3)

Usado para objetos, pode guardar static web sites, assets, disaster recovery e backups.
Its object oriented, different from EFS, that is highly hierarchical. It makes easier for
services like Athena to query objects due this feature.
Capacidade virtualmente ilimitada.

- Composicao
   - Arquivo (Valor)
   - Identificador Exclusivo (Chave)
   - Metadados
- Cross region replication
- Transfer Acceleration: para bucket centralizado no mundo todo, ou que transfere altas quantidades
- Categorias de armazenamento
  - S3 Intelligent Tiering
    - para economia automatica de custos
  - S3 Standard
    - para dados acessados com frequencia
  - S3 Express One Zone
    - para dados acessados com mais frequencia
  - S3 Infrequent Access
    - para dados acessados com menos frequencia
- Backup, Arquivamentos e Recuperacao de Desastres
  - Glacier
    - para grande conjunto de dados
    - nao querer acesso imediato. 1 a 2 vezes por ano, de forma assincrona
  - Glacier Instant Retrieval
  - Glacier Deep Archive
    - retencao maior. De 7 a 10 anos
    - recuperacao em horas
- Storage lifecycle
  - Transition actions
  - Expiration (removal) actions

#### Elastic Block Store (EBS)

- In conjunction with EC2, it works as a hard drive. Data in EBS is stored in equally sized blocks.
- Can be used for snapshots, for example.
- It's very perfomatic, available and easialy backup and restoration
- Has low latency

#### Elastic File System

- In conjunction with EC2, it can be mounted for multiple instances. Its very scalable.

#### Storage Gateway

- Hybrid comuting storage integration
- Uses direct connect encrypted

#### Backup

- https://docs.aws.amazon.com/aws-backup/

### Network
- VPC and Subnets
  - Each VPC exists within a single region and cannot span multiple regions.
  - Within each VPC, you can create one or more subnets.
  - Each subnet is associated with a single Availability Zone and cannot span multiple Availability Zones.
  - Public subnet, Private subnet, VPN-only subnet, and Isolated subnet.
- Elastic Load Balancing
- Direct Connect
  - Conexao direta com a rede AWS
  - Menor gargalo e instabilidade
- Route 53 (DNS)
  - Global scope
- CloudFront
  - Low latency
  - Uses content delivery and edge locations strategy
  - Global scope
- API Gateway
- AWS Global Accelerator
  - otimiza o caminho para sua aplicação para manter a perda de pacotes, o jitter e a latência consistentemente baixos
  - Global scope
- Amazon VPN

### Data

#### Databases

#### SQL
- RDS
  - Relational Database
  - Scale Up: More resources
  - Scale Out: Read and Write Replicas
  - RDS Proxy (Manages the scalling)
- Aurora
  - Fully managed
  - apenas MySQL e PostgreSQL

#### NoSQL
- DynamoDB
- DocumentDB (json)
- ElastiCache (uses Redis... for caching)
- Neptune (graphs)

#### Data Warehouse

Big database of highly structured, current and historical, read-only data from multiple sources.
Uses ETL to get loaded.
Used for Business Intelligence

- Redshift

#### Datalake

Repository of raw data, historical and current, read-only, from multiple sources, in multiple formats.
Used to analyze data and gain insights. Or as a cheap option

- (S3)
- (Athena)


### Segurança e Conformidade

#### Identity and Access Management
The AWS account root user or an administrative user for the account can create IAM identities. An IAM identity provides access to an AWS account. An IAM user group is a collection of IAM users managed as a unit. An IAM identity represents a human user or programmatic workload, and can be authenticated and then authorized to perform actions in AWS. Each IAM identity can be associated with one or more policies. Policies determine what actions a user, role, or member of a user group can perform, on which AWS resources, and under what conditions.
  - Organizations and Accounts
  - Identities
    - Group (cannot be nested)
    - Users (can belong to multiple groups. not automatic)
    - Roles
      - can be assigned to multiple users
      - Uma função do IAM é uma identidade do IAM que você pode criar em sua conta que tem permissões específicas. Uma função do IAM é semelhante a um usuário do IAM no sentido de que é uma identidade da AWS com políticas de permissão que determinam o que a identidade pode e não pode fazer na AWS. No entanto, em vez de ser exclusivamente associada a uma pessoa, o propósito do perfil é ser assumido por qualquer pessoa que precisar dele. Além disso, um perfil não tem credenciais de longo prazo padrão associadas a ele, como senha ou chaves de acesso. Em vez disso, quando você assumir um perfil, ele fornecerá credenciais de segurança temporárias para sua sessão de perfil.
      - Você pode usar funções para delegar acesso a usuários, aplicativos ou serviços que normalmente não têm acesso aos seus recursos da AWS. Por exemplo, você pode conceder para os usuários na sua conta da AWS acesso a recursos que normalmente eles não têm ou conceder para os usuários em uma Conta da AWS acesso a recursos em outra conta
  - Policies
  - Global scope

![](iam-terms-2.png)

#### ACLs & Security Groups
- ACLs: Firewall for VPC Subnets
  - Stateless: necessário especificar tanto uma regra de inbound como outbound para liberar uma porta específica.
- Security Group: instance-level firewall used for controlling access to AWS resources. Deny by nature.
  - Statefull: todo o tráfego liberado em um security group tem seu retorno previamente liberado, o que facilita a sua configuração

#### Authentication

- User and password
- MFA
- Access keys:  For API calls. Are a combination of an access key ID and a secret access key.
- Key pairs: are used for asymmetric or symmetric encrypting
- Server certificates: are SSL/TLS certificates that you can use to authenticate with AWS services

#### Access portal

- List of all AWS accounts
- Uses login, user and password authentication
- Can force MFA

#### Others

- AWS Security Hub:
  - Automatize verificações de segurança da AWS e centralize alertas de segurança
- Cognito
  - Gerenciamento de identidades de aplicacoes. Login, por exemplo
- AWS Artifact
  - Conformidade com regulamentos

##### Threat Detection
- AWS Inspector
  - Analise, com base em boas praticas, dos servicos
- AWS GuardDuty
  - Collects logs and uses ML to detect threats
- AWS Detective
  - Extends GuardDuty by automatically creating a graph model of your AWS environment for root cause analysis
- Amazon Macie
  - Descubra e proteja seus dados sigilosos em escala

##### Frontline
- AWS WAF
  - Firewall
  - Pode criar **regras de segurança** que controlam o tráfego de bots e **bloqueiam padrões de ataque comuns**, como injeção de SQL ou cross-site scripting (XSS).
  - Global scope
- AWS Shield
  - **DDoS**
  - Global scope

##### Keys and Certificates

- AWS Secrets Manager
  - gerenciar, recuperar e alternar credenciais de banco de dados, chaves de API e outros segredos ao longo de seus ciclos de vida.
- AWS Key Management Service (Chaves criptograficas)
- AWS CloudHSM (Manage Hardware Securit Module encryption keys)
  - Dispositivos Cloud de criptografia, com base em hardware que oferecem funções de gerar e armazenar chaves criptográficas simétricas e assimétricas em infraestruturas de chaves públicas
- AWS Certificate Manager
  - SSL and TLS
  - Global scope

### Outros

#### Migration

- AWS Application Discovery Service (gather information about on-premises data centers)
- AWS Application Migration Service (minimizes time-intensive, error-prone manual processes by automatically converting your source servers from physical, virtual, or cloud infrastructure to run natively on AWS)
- AWS Data Migration Service (migration from database to database)
- AWS Mainframe Modernization Service
- AWS Migration Hub (provides a single location to track the progress of application migrations across multiple AWS and partner solutions)
- AWS Snow Family (edge computing, edge storage, and data transfer devices. Non-data center environments, and in locations where there's lack of consistent network connectivity. For IoT in extreme conditions, for example)
  - [Snowcone](https://aws.amazon.com/snowcone/)
  - Snowball
  - Snowmobile
- AWS DataSync (migration from storage to storage)
- AWS Transfer Family (file transfer. SFTP)

#### Application Integration

- Amazon MQ (low latency publisher/subscriber agent)
- EventBridge
  - Bus: Roteador de eventos de uma fonte para um ou mais destinos (lambdas)
  - Pipes: Conexoes de uma fonte para um destino (Lambda)
- SNS (Publisher / Subscriber)
- SQS (Queue)
- SES (Email)
- Step Functions (serviço de orquestração de fluxo de trabalho que facilita a criação e a coordenação de aplicativos distribuídos e baseados em serviços. Ele permite criar fluxos de trabalho visualmente, definindo passos individuais como funções Lambda, tarefas de ECS, atividades de data pipeline, entre outros)

#### Gerenciamento
- CloudFormation
- AWS Organizations (permite criar novas contas da AWS sem custo adicional.Pode facilmente alocar recursos, agrupar contas e aplicar políticas de governança a contas ou grupos)
- CloudWatch (registro de servicos)
- CloudTrail (registro de eventos de utilizacao)
- Config (rastreia alterações em recursos, registra conformidade com políticas e cria snapshots do estado da infraestrutura ao longo do tempo)

#### Developer Tools
- Cloud9 (IDE)
- CodeGuru (Find most expensive lines of code)
- CodeCommit -> CodeBuild (and test) -> CodeDeploy
- CodePipeline

#### Analytics

- Amazon EMR (big data mapReduce)
- Managed Streaming for Apache Kafka (AWS MSK)
- Athena: Query S3 data using SQL
- QuickSight: Analise empresarial (Business Intelligence). Entenda os recursos por meio de linguagem natural, e paineis interativos
- Glue: Descubra, prepare e integre todos os seus dados em qualquer escala. Extract, Transform, Load (ETL)
- Kinesis: Processa e analisa de forma econômica os dados de streaming em qualquer escala como um serviço totalmente gerenciado. Consome dados em tempo real como vídeo, áudio, logs de aplicações, clickstreams de sites e dados de telemetria de IoT para machine learning (ML), análises e outras aplicações.
- CloudSearch: search solution for your website or application. Large collections of data such as web pages, document files, forum posts, or product information

#### Machine Learning
- Transcribe: Automatic speech recognition
- Lex: Build voice and text chatbots
- Comprehend: Processamento de linguagem natural
- Polly: Converte artigos em fala humana
- SageMaker: Build, train, and deploy machine learning (ML) models for any use case with fully managed infrastructure, tools, and workflows
- Amazon Textract: Extraia automaticamente texto impresso, manuscrito, elementos de layout e dados de qualquer documento

#### Front-end Web and Mobile
- Farm: Test Android, iOS and Web Apps on real devices in the AWS Cloud, in parallel

#### Business

- Amazon Connect
  - Ofereça um atendimento de classe superior ao cliente a um custo menor com uma central de atendimento na nuvem fácil de usar


## Marketplace

Discover, deploy and manage software that runs in AWS (used for data, for example)

### Services
- OpenSearch: Pesquise, Visualize e Analise ate petabytes de texto e dados nao estruturados
- Data Exchange: Encontre, Assine e Use dados de terceiros na nuvem

## Pricing

Three fundamental drivers of cost
   - Compute
     - by hour or second that started until it terminated, unless you have made a reservation
   - Storage
     - by GB
   - Outbound Data Transfer (between AWS and Internet, or between Regions)
     - the more data you transfer, the less you pay

How do you pay?
   - Usage, or Pay less using more
   - Save reserving

Services
   - Total Cost of Ownership calculator
   - Cost Explorer (Visualize, Understand and Manage costs)
   - AWS Pricing Calculator (Cost estimate with no commitment, and explore AWS services and pricing for your architecture needs)
   - AWS Budget (personalize as medidas de gastos, rastreie e seja notificado, defina e inicie cortes de gastos)

## Suporte

### Well Architected Tool
- [Pilares](https://docs.aws.amazon.com/pt_br/wellarchitected/latest/framework/the-pillars-of-the-framework.html): excelência operacional, segurança, confiabilidade, eficiência de performance, otimização de custos e sustentabilidade (CEOS ES)
- "Teste de Personalidade do Projeto"

### Trusted Advisor
- Economizar dinheiro, melhorar a perfomance e ajudar a corrigir falhar de seguranca
- Security, Performance, Service limits, Cost optimization, Fault tolerance (SCSPF)

### Cloud Adoption Framework

Fornece orientações de práticas recomendadas que ajudam a melhorar sua preparação para a nuvem
- Negócios, Pessoas, Governança, Plataforma, Segurança e Operações
- https://aws.amazon.com/pt/cloud-adoption-framework/

### Responsabilidade Compartilhada

- AWS: Infraestrutura de Serviços e Segurança Física
- Cliente: Criptografia, Proteção de Tráfego, Configuração de SOs, Redes e Firewalls, Plataformas, Apps, IAM e Dados

### Planos
- Developer, Business, Enterprise on Ramp, Enterprise

### Amazon IQ
- Permite que os clientes encontrem, colaborem com segurança e paguem especialistas terceirizados certificados pela AWS para trabalhos sob demanda em um projeto

### Health Dashboard

- Personal Health
- Service Health

## Leitura adicional

- https://medium.com/google-cloud/kubernetes-101-pods-nodes-containers-and-clusters-c1509e409e16
- https://kubernetes.io/docs/concepts/services-networking/service/
- https://medium.com/@prateekbansalind/demystifying-kubernetes-service-types-clusterip-nodeport-and-loadbalancer-88fb0c065ce9
