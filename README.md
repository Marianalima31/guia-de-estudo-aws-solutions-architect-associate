### guia-de-estudo-aws-solutions-architect-associate

Este guia de estudo ajudará você a passar no mais recente exame AWS Certified Solutions Architect - Associate. Idealmente, você deve consultar este guia enquanto trabalha com o seguinte material:

1.
2.

## Identity Access Management (IAM)

# IAM simplificado: 
o IAM oferece um hub de controle centralizado na AWS e se integra a todos os outros serviços da AWS. O IAM vem com a capacidade de compartilhar o acesso em vários níveis de permissão e oferece suporte à capacidade de usar a federação de identidade (o processo de delegação de autenticação a uma parte externa confiável, como Facebook ou Google) para acesso temporário ou limitado. O IAM vem com suporte MFA e permite que você configure uma política de rotação de senha personalizada em toda a organização. Também é compatível com PCI DSS, ou seja, padrão de segurança de dados da indústria de cartões de pagamento. (aprova os regulamentos de segurança de cartão de crédito exigidos pelo governo). 

# Entidades IAM: 

Usuários - qualquer usuário final individual, como funcionário, arquiteto de sistema, CTO, etc. 

Grupos - qualquer coleção de pessoas semelhantes com permissões compartilhadas, como administradores de sistema, funcionários de RH, equipes financeiras, etc. Cada usuário dentro de seu grupo especificado herdará as permissões definidas para o grupo. 

Roles - qualquer serviço de software que precisa receber permissões para fazer seu trabalho, por exemplo, AWS Lambda que precisa de permissões de gravação para S3 ou uma frota de instâncias do EC2 que precisam de permissões de leitura de um banco de dados RDS MySQL. 

Policies - os conjuntos de regras documentados que são aplicados para conceder ou limitar o acesso. Para que usuários, grupos ou funções definam permissões corretamente, eles usam políticas. As políticas são escritas em JSON e você pode usar políticas personalizadas para suas necessidades específicas ou usar as políticas padrão definidas pela AWS.

![image](https://github.com/Marianalima31/guia-de-estudo-aws-solutions-architect-associate/assets/77506074/34c301a6-a1f7-4392-8134-55e46d604a9d)

As políticas do IAM são separadas das outras entidades acima porque não são uma identidade do IAM. Em vez disso, eles são anexados às identidades do IAM para que a identidade do IAM em questão possa desempenhar sua função necessária.

# Detalhes da chave IAM:
O IAM é um serviço global da AWS que não é limitado por regiões. Qualquer usuário, grupo, função ou política é acessível globalmente.

A conta raiz com acesso administrativo completo é a conta usada para se inscrever na AWS. Portanto, o endereço de e-mail usado para criar a conta da AWS para uso provavelmente deve ser o endereço de e-mail oficial da empresa.

Novos usuários não têm permissões quando suas contas são criadas pela primeira vez. Essa é uma maneira segura de delegar acesso, pois as permissões devem ser concedidas intencionalmente.

Ao ingressar no ecossistema da AWS pela primeira vez, novos usuários recebem um ID de chave de acesso e um ID de chave de acesso secreta quando você concede a eles acesso programático. Eles são criados apenas uma vez especificamente para o novo usuário ingressar, portanto, se forem perdidos, basta gerar um novo ID de chave de acesso e um novo ID de chave de acesso secreta. As chaves de acesso são usadas apenas para AWS CLI e SDK, portanto, você não pode usá-las para acessar o console.

Ao criar sua conta da AWS, você pode ter um provedor de identidade existente interno para sua empresa que oferece Single Sign On (SSO). Se for esse o caso, é útil, eficiente e totalmente possível reutilizar suas identidades existentes na AWS. Para fazer isso, você permite que uma função do IAM seja assumida por um dos diretórios ativos. Isso ocorre porque o recurso IAM ID Federation permite que um serviço externo tenha a capacidade de assumir uma função IAM.

As funções do IAM podem ser atribuídas a um serviço, como uma instância do EC2, antes de seu primeiro uso/criação ou após seu uso/criação. Você pode alterar as permissões quantas vezes precisar. Tudo isso pode ser feito usando o console da AWS e as ferramentas de linha de comando da AWS.

Não é possível aninhar grupos do IAM. Usuários individuais do IAM podem pertencer a vários grupos, mas não é possível criar subgrupos para que um grupo IAM seja incorporado a outro grupo IAM.

Com as políticas do IAM, você pode adicionar facilmente tags que ajudam a definir quais recursos podem ser acessados por quem. Essas tags são usadas para controlar o acesso por meio de uma determinada política do IAM. Por exemplo, instâncias EC2 de produção e desenvolvimento podem ser marcadas como tal. Isso garantiria que as pessoas que deveriam acessar apenas as instâncias de desenvolvimento não pudessem acessar as instâncias de produção.

# Níveis de prioridade no IAM:
Explicit Deny/Negação explícita: Nega o acesso a um recurso específico e esta decisão não pode ser anulada.

Explicit Allow/Permitir explicitamente: permite o acesso a um determinado recurso desde que não haja uma Explicit Deny associada.

Default Deny (or Implicit Deny)/Negação padrão (ou negação implícita): as identidades do IAM começam sem acesso a recursos. Em vez disso, o acesso deve ser concedido.

# Ferramentas de segurança IAM:
IAM Access Advisor (nível de usuário)

O consultor de acesso mostra as permissões de serviço concedidas a um usuário e quando esses serviços foram acessados pela última vez.
Você pode usar essas informações para revisar suas políticas.
Relatório de credenciais IAM (nível de conta)

um relatório que lista todos os usuários da sua conta e o status de suas várias credenciais.

## Serviço de Armazenamento Simples (S3)
# S3 Simplificado:
O AWS S3 fornece armazenamento infinitamente escalável. Ele é usado para armazenamento e backup de dados, fins de recuperação de desastres, arquivos de dados, hospedagem de sites estáticos, hospedagem de mídia, entrega de atualizações de software e muito mais.

O S3 fornece aos desenvolvedores e equipes de TI armazenamento de objetos seguro, durável e altamente escalável. O armazenamento de objetos, em oposição ao armazenamento de blocos, é um termo geral que se refere a dados compostos de três coisas:

1.) os dados que você deseja armazenar

2.) uma quantidade expansível de metadados

3.) um identificador único para que os dados possam ser recuperados

Isso o torna um candidato perfeito para hospedar arquivos ou diretórios e um candidato ruim para hospedar bancos de dados ou sistemas operacionais. A tabela a seguir destaca as principais diferenças entre armazenamento de objeto e bloco:

![image](https://github.com/Marianalima31/guia-de-estudo-aws-solutions-architect-associate/assets/77506074/5e335ee4-750f-43bd-b3dd-bd17552b028b)


Os dados carregados no S3 são distribuídos em vários arquivos e instalações. Os arquivos carregados no S3 têm um limite superior de 5 TB por arquivo e o número de arquivos que podem ser carregados é virtualmente ilimitado. Os buckets do S3, que contêm todos os arquivos, são nomeados em um namespace universal, portanto, a exclusividade é necessária. Todos os uploads bem-sucedidos retornarão uma resposta HTTP 200.

# Detalhes da chave S3:
Objetos (arquivos ou diretórios regulares) são armazenados no S3 com uma chave, valor, ID de versão e metadados. Eles também podem conter torrents e sub-recursos para listas de controle de acesso que são basicamente permissões para o próprio objeto.

O modelo de consistência de dados para S3 garante acesso de leitura imediato para novos objetos após as solicitações PUT iniciais. Esses novos objetos são introduzidos na AWS pela primeira vez e, portanto, não precisam ser atualizados em nenhum lugar para que estejam disponíveis imediatamente.

O modelo de consistência de dados para S3 também garante acesso imediato de leitura para PUTS e DELETES de objetos já existentes, desde dezembro de 2020.

A Amazon garante durabilidade de 99,999999999% (ou 11 9s) para todas as classes de armazenamento S3, exceto sua classe de armazenamento de redundância reduzida.

O S3 vem com os seguintes recursos principais:

1.) armazenamento em camadas e variabilidade de preços

2.) gerenciamento do ciclo de vida para expirar o conteúdo mais antigo

3.) controle de versão para controle de versão

4.) criptografia para privacidade

5.) MFA exclui para evitar remoção acidental ou maliciosa de conteúdo

6.) listas de controle de acesso e políticas de bucket para proteger os dados

S3 cobra por:

1.) tamanho do armazenamento

2.) número de pedidos

3.) preços de gerenciamento de armazenamento (conhecidos como níveis)

4.) preços de transferência de dados (objetos saindo/entrando da AWS pela internet)

5.) aceleração de transferência (um aumento de velocidade opcional para mover objetos via Cloudfront)

6.) replicação entre regiões (mais HA do que o oferecido por padrão)

As políticas de bucket protegem os dados no nível do bucket, enquanto as listas de controle de acesso protegem os dados no nível de objeto mais granular.

Por padrão, todos os buckets recém-criados são privados.

O S3 pode ser configurado para criar logs de acesso que podem ser enviados para outro balde na conta atual ou até mesmo em uma conta separada. Isso facilita o monitoramento de quem acessa o que dentro do S3.

Existem 3 maneiras diferentes de compartilhar buckets S3 entre contas da AWS:

1.) Somente para acesso programático, use IAM & Bucket Policies para compartilhar buckets inteiros

2.) Somente para acesso programático, use ACLs e políticas de bucket para compartilhar objetos

3.) Para acesso por meio do console e do terminal, use as funções IAM entre contas

O S3 é um ótimo candidato para hospedagem de sites estáticos. Ao ativar a hospedagem de site estático para S3, você precisa de um arquivo index.html e um arquivo error.html. A hospedagem estática de sites cria um endpoint de site que pode ser acessado pela Internet.

Ao fazer upload de novos arquivos e ativar o controle de versão, eles não herdarão as propriedades da versão anterior.

# Classes de armazenamento S3:
S3 Standard - 99,99% de disponibilidade e 11 9s de durabilidade. Os dados desta classe são armazenados de forma redundante em vários dispositivos em várias instalações e são projetados para resistir à falha de 2 data centers simultâneos.

S3 Infrequently Accessed (IA) - Para dados que são necessários com menos frequência, mas quando necessário, os dados devem estar disponíveis rapidamente. A taxa de armazenamento é mais barata, mas você é cobrado pela recuperação.

S3 One Zone Infrequently Accessed (uma melhoria do RRS herdado / armazenamento de redundância reduzida) - para quando você deseja custos mais baixos de IA, mas não requer alta disponibilidade. Isso é ainda mais barato devido à falta de HA.

S3 Intelligent Tiering - Usa ML/AI integrado para determinar a classe de armazenamento mais econômica e, em seguida, move automaticamente seus dados para o nível apropriado. Ele faz isso sem sobrecarga operacional ou impacto no desempenho.

S3 Glacier - classe de armazenamento de baixo custo para arquivamento de dados. Essa classe é para fins de armazenamento puro, onde a recuperação não é necessária com frequência. Os tempos de recuperação variam de minutos a horas. Existem diferentes métodos de recuperação, dependendo de quão aceitáveis são os tempos de recuperação padrão para você:

Rápido: 1 a 5 minutos, mas esta opção é a mais cara.
Padrão: 3 - 5 horas para restaurar.
Volume: 5 - 12 horas. Essa opção tem o menor custo e é boa para um grande conjunto de dados.

A duração acelerada listada acima pode ser mais longa em raras situações de demanda excepcionalmente alta em toda a AWS. Se for absolutamente crítico ter acesso rápido aos dados do Glacier em todas as circunstâncias, você deve adquirir a capacidade provisionada. A capacidade provisionada garante que as recuperações aceleradas sempre funcionem dentro das restrições de tempo de 1 a 5 minutos. 

S3 Deep Glacier - O armazenamento S3 de menor custo, onde a recuperação pode levar 12 horas.

![image](https://github.com/Marianalima31/guia-de-estudo-aws-solutions-architect-associate/assets/77506074/ac6b1509-4af8-4117-bca5-0c679ad87efa)


# Criptografia S3:
Os dados do S3 podem ser criptografados tanto em trânsito quanto em repouso.

Criptografia em trânsito: quando o tráfego que passa entre um endpoint e outro é indecifrável. Qualquer um que espionar entre o servidor A e o servidor B não conseguirá entender as informações que passam. A criptografia em trânsito para S3 é sempre obtida por SSL/TLS.

Criptografia em repouso: quando os dados imóveis armazenados no S3 são criptografados. Se alguém invadir um servidor, ainda não poderá acessar informações criptografadas nesse servidor. A criptografia em repouso pode ser feita no lado do servidor ou no lado do cliente. O lado do servidor é quando o S3 criptografa seus dados conforme eles são gravados no disco e os descriptografa quando você os acessa. O lado do cliente é quando você criptografa pessoalmente o objeto por conta própria e, em seguida, carrega-o no S3 posteriormente.

Você pode criptografar no lado do servidor suportado pela AWS das seguintes maneiras:

Chaves gerenciadas S3 / SSE - S3 (S3 de criptografia do lado do servidor) - quando a Amazon gerencia as chaves de criptografia e descriptografia para você automaticamente. Nesse cenário, você concede um pouco de controle à Amazon em troca de facilidade de uso.
AWS Key Management Service/SSE - KMS - quando a Amazon e você gerenciam as chaves de criptografia e descriptografia juntos.
Criptografia do lado do servidor com chaves fornecidas pelo cliente / SSE - C - quando dou à Amazon minhas próprias chaves que gerencio. Nesse cenário, você concede facilidade de uso em troca de mais controle.
# Versão S3:
Quando o controle de versão está ativado, o S3 armazena todas as versões de um objeto, incluindo todas as gravações e até exclusões.
É um ótimo recurso para fazer backup de conteúdo implicitamente e para reversões fáceis em caso de erro humano.
Pode ser pensado como análogo ao Git.
Depois que o controle de versão é habilitado em um bucket, ele não pode ser desabilitado - apenas suspenso.
O controle de versão se integra com regras de ciclo de vida para que você possa definir regras para expirar ou migrar dados com base em sua versão.
O controle de versão também possui capacidade de exclusão de MFA para fornecer uma camada adicional de segurança.
# Gerenciamento do ciclo de vida S3:
Automatiza a movimentação de objetos entre os diferentes níveis de armazenamento.
Pode ser usado em conjunto com controle de versão.
As regras de ciclo de vida podem ser aplicadas às versões atual e anterior de um objeto.
# Replicação entre regiões S3:
Podemos fazer 2 tipos de replicações - Cross Region Replication (CRR) e Same Region Replication (SRR). O controle de versão do bucket S3 deve ser ativado nos buckets S3 de origem e destino. A replicação ocorre de forma assíncrona e os 2 buckets podem pertencer a 2 contas diferentes da AWS.
- A replicação entre regiões só funciona se o controle de versão estiver ativado.
- Quando a replicação entre regiões está habilitada, nenhum dado pré-existente é transferido. Somente novos uploads no bucket original são replicados. Todas as atualizações subsequentes são replicadas.
- Ao replicar o conteúdo de um depósito para outro, você pode realmente alterar a propriedade do conteúdo, se desejar. Você também pode alterar a camada de armazenamento do novo depósito com o conteúdo replicado.
- Quando os arquivos são excluídos no depósito original (por meio de um marcador de exclusão, pois o controle de versão impede exclusões verdadeiras), essas exclusões não são replicadas.

Depois que a replicação é habilitada, apenas novos objetos são replicados. Podemos replicar objetos existentes do S3 usando a replicação em lote.
Podemos ativar ou desativar a replicação de marcadores de exclusão. (Exclusões permanentes usando id de versão não podem ser replicadas).
Por padrão, a replicação está habilitada para todos os objetos no bucket S3 de origem, mas podemos usar alguns filtros e habilitar a replicação para objetos específicos nesse bucket.
A replicação de bucket não pode ser encadeada.
# Aceleração de transferência S3:
A aceleração de transferência usa a rede do CloudFront enviando ou recebendo dados em pontos de presença CDN (chamados pontos de presença) em vez de uploads ou downloads mais lentos na origem.
Isso é feito carregando em um URL distinto para o ponto de presença em vez do próprio bucket. Isso é transferido pelo backbone da rede da AWS em uma velocidade muito mais rápida.
Você pode testar a velocidade de aceleração de transferência diretamente em comparação com uploads regulares.
# S3 Notificações de Eventos:
O recurso de notificação do Amazon S3 permite receber e enviar notificações quando determinados eventos ocorrem em seu bucket. Para habilitar as notificações, você deve primeiro configurar os eventos que deseja que o Amazon S3 publique (novo objeto adicionado, objeto antigo excluído etc.) e os destinos para onde deseja que o Amazon S3 envie as notificações de eventos. O Amazon S3 oferece suporte aos seguintes destinos onde pode publicar eventos:

Amazon Simple Notification Service (Amazon SNS) - Um serviço da web que coordena e gerencia a entrega ou envio de mensagens para endpoints ou clientes assinantes.
Amazon Simple Queue Service (Amazon SQS) - O SQS oferece filas hospedadas confiáveis e escaláveis para armazenar mensagens enquanto elas trafegam entre computadores.
AWS Lambda - AWS Lambda é um serviço de computação onde você pode carregar seu código e o serviço pode executar o código em seu nome usando a infraestrutura da AWS. Você empacota e carrega seu código personalizado no AWS Lambda ao criar uma função do Lambda. O evento S3 que aciona a função Lambda também pode servir como entrada do código.

# S3 e ElasticSearch:
Se você estiver usando o S3 para armazenar arquivos de log, o ElasticSearch fornece recursos de pesquisa completos para logs e pode ser usado para pesquisar dados armazenados em um bucket do S3.
Você pode integrar seu domínio ElasticSearch com S3 e Lambda. Nessa configuração, todos os novos logs recebidos pelo S3 acionarão uma notificação de evento para o Lambda, que por sua vez executará o código do aplicativo nos novos dados de log. Depois que seu código terminar de processar, os dados serão transmitidos para seu domínio ElasticSearch e estarão disponíveis para observação.
# Maximizing S3 Read/Write Performance/ Maximizando o desempenho de leitura/gravação do S3:
Se a taxa de solicitação para leitura e gravação de objetos no S3 for extremamente alta, você poderá usar a nomenclatura sequencial baseada em data para seus prefixos para melhorar o desempenho. Versões anteriores do AWS Docs também sugeriam o uso de chaves hash ou strings aleatórias para prefixar o nome do objeto. Nesses casos, as partições usadas para armazenar os objetos serão melhor distribuídas e, portanto, permitirão um melhor desempenho de leitura/gravação de seus objetos.
Se seus dados do S3 estiverem recebendo um grande número de solicitações GET de usuários, você deve considerar o uso do Amazon CloudFront para otimização de desempenho. Ao integrar o CloudFront com o S3, você pode distribuir conteúdo por meio do cache do CloudFront para seus usuários para menor latência e maior taxa de transferência de dados. Isso também tem a vantagem adicional de enviar menos solicitações diretas ao S3, o que reduzirá os custos. Por exemplo, suponha que você tenha alguns objetos muito populares. O CloudFront busca esses objetos do S3 e os armazena em cache. O CloudFront pode atender solicitações futuras para os objetos de seu cache, reduzindo o número total de solicitações GET enviadas ao Amazon S3.
Mais informações sobre como garantir alto desempenho no S3
# Registro de acesso ao servidor S3:
O registro de acesso ao servidor fornece registros detalhados para as solicitações feitas a um depósito. Os logs de acesso ao servidor são úteis para muitos aplicativos. Por exemplo, informações de log de acesso podem ser úteis em auditorias de segurança e acesso. Também pode ajudá-lo a aprender sobre sua base de clientes e entender melhor sua fatura do Amazon S3.
Por padrão, o registro está desabilitado. Quando o log está habilitado, os logs são salvos em um bucket na mesma região da AWS que o bucket de origem.
Cada registro de log de acesso fornece detalhes sobre uma única solicitação de acesso, como solicitante, nome do bloco, hora da solicitação, ação da solicitação, status da resposta e um código de erro, se relevante.
# Funciona da seguinte forma:
O S3 coleta periodicamente registros de log de acesso do bucket que você deseja monitorar
O S3 então consolida esses registros em arquivos de log
O S3 finalmente carrega os arquivos de log para seu bucket de monitoramento secundário como objetos de log
# S3 Multipart Upload / Carregamento de várias partes do S3:
O upload de várias partes permite fazer upload de um único objeto como um conjunto de partes. Cada parte é uma parte contígua dos dados do objeto. Você pode carregar essas partes do objeto de forma independente e em qualquer ordem.
Uploads em várias partes são recomendados para arquivos com mais de 100 MB e é a única maneira de fazer upload de arquivos com mais de 5 GB. Ele atinge a funcionalidade carregando seus dados em paralelo para aumentar a eficiência.
Se a transmissão de qualquer parte falhar, você pode retransmitir essa parte sem afetar outras partes. Após o upload de todas as partes do seu objeto, o Amazon S3 monta essas partes e cria o objeto.
Possíveis razões pelas quais você gostaria de usar o multipart upload:
O multipart upload oferece a capacidade de iniciar um upload antes que você saiba o tamanho final do objeto.
O upload de várias partes oferece uma taxa de transferência aprimorada.
O multipart upload oferece a capacidade de pausar e retomar uploads de objetos.
O multipart upload oferece recuperação rápida de problemas de rede.
Você pode usar um AWS SDK para fazer upload de um objeto em partes. Como alternativa, você pode executar a mesma ação por meio da AWS CLI.
Você também pode paralelizar downloads do S3 usando buscas de intervalo de bytes. Se houver uma falha durante o download, a falha será localizada apenas no intervalo de bytes específico e não em todo o objeto.
# URLs pré-assinados S3:
Todos os objetos S3 são privados por padrão, no entanto, o proprietário do objeto de um depósito privado com objetos privados pode, opcionalmente, compartilhar esses objetos sem ter que alterar as permissões do depósito para serem públicas.

Isso é feito criando um URL pré-assinado. Usando suas próprias credenciais de segurança, você pode conceder permissão por tempo limitado para baixar ou visualizar seus objetos privados do S3.

Ao criar um URL pré-assinado para seu objeto S3, você deve fazer o seguinte:

Forneça suas credenciais de segurança.
Especifique um balde.
Especifique uma chave de objeto.
Especifique o método HTTP (GET para baixar o objeto).
Especifique a data e hora de expiração.
As URLs pré-assinadas são válidas apenas pela duração especificada e qualquer pessoa que receba a URL pré-assinada dentro dessa duração pode acessar o objeto.

O diagrama a seguir destaca como os URLs pré-assinados funcionam:

![image](https://github.com/Marianalima31/guia-de-estudo-aws-solutions-architect-associate/assets/77506074/4bb61716-c2b3-412c-b44a-d656aacc7b9d)


# S3 Selecione:
O S3 Select é um recurso do Amazon S3 projetado para extrair apenas os dados necessários de um objeto, o que pode melhorar drasticamente o desempenho e reduzir o custo de aplicativos que precisam acessar dados no S3.
A maioria dos aplicativos precisa recuperar o objeto inteiro e, em seguida, filtrar apenas os dados necessários para análise posterior. O S3 Select permite que os aplicativos descarreguem o trabalho pesado de filtrar e acessar dados dentro de objetos para o serviço Amazon S3.
Por exemplo, vamos imaginar que você é um desenvolvedor em um grande varejista e precisa analisar os dados de vendas semanais de uma única loja, mas os dados de todas as 200 lojas são salvos em um novo CSV editado por GZIP todos os dias.
Sem o S3 Select, você precisaria baixar, descompactar e processar todo o CSV para obter os dados necessários.
Com o S3 Select, você pode usar uma expressão SQL simples para retornar apenas os dados da loja de seu interesse, em vez de recuperar o objeto inteiro.

# Buckets e Objetos
O Amazon S3 armazena dados em buckets (semelhantes aos diretórios de nível superior). O nome de um bucket S3 da AWS deve ser globalmente exclusivo em todas as regiões e todas as contas da AWS . Os buckets S3 têm escopo de região. Dentro de um bucket do S3, os arquivos são armazenados como objetos. S3 não tem o conceito de diretórios. Cada objeto em um bucket do S3 tem uma chave no formato s3://bucket_name/unique_value que representa o caminho completo desse objeto. A chave deve ser exclusiva para cada objeto no nível do bucket.

Um objeto S3 consiste em -

o conteúdo que precisamos carregar (pode ter tamanho máximo de 5 TB). Ao fazer upload de conteúdo com mais de 5 GB de tamanho para um bucket do S3, devemos usar o upload de várias partes.
alguns metadados - lista de pares de chave/valor de texto definidos pelo usuário ou pelo próprio S3.
até 10 tags - pares chave/valor unicode úteis no caso de segurança e ciclo de vida do objeto.
ID da versão se o controle de versão do bucket do S3 estiver ativado.

# Segurança S3
O controle de acesso a buckets e objetos do AWS S3 para usuários/funções do IAM na mesma conta da AWS pode ser feito usando as políticas do IAM da AWS. A AWS também nos fornece políticas baseadas em recursos -

S3 Bucket Policies - Regras amplas do bucket que podem ser atribuídas a usuários do IAM na conta atual da AWS ou até mesmo a outras contas da AWS.

As políticas de bucket do S3 são usadas em casos como - conceder acesso público ao bucket do S3, forçar objetos do S3 a serem criptografados no upload ou conceder acesso a outras contas da AWS.

Listas de controle de acesso a objetos (ACLs) - Políticas de nível de objeto granular.

💡As políticas de nível de bucket também podem ser configuradas usando Bucket ACLs, mas é recomendável usar S3 Bucket Policies.
O recurso de ACLs de balde ou objeto pode ser desativado, se você desejar.

A AWS também fornece uma configuração chamada Block Public Access . Se você ativar isso para um bucket do S3, independentemente de qualquer política de bucket do S3 existente que conceda acesso público ao bucket do S3, esse bucket do S3 nunca será exposto à Internet pública. Você também pode ativar Bloquear acesso público no nível da conta da AWS.

A criptografia em repouso está disponível para objetos S3.
Ao reduzir o volume de dados que precisam ser carregados e processados por seus aplicativos, o S3 Select pode melhorar o desempenho da maioria dos aplicativos que acessam com frequência os dados do S3 em até 400% porque você está lidando com significativamente menos dados.
Você também pode usar o S3 Select para Glacier.


# CloudFront
CloudFront Simplified:

O serviço AWS CDN é chamado CloudFront. Ele fornece conteúdo e ativos armazenados em cache para aumentar o desempenho global do seu aplicativo. Os principais componentes do CloudFront são os pontos de presença (endpoints de cache), a origem (fonte original da verdade a ser armazenada em cache, como uma instância EC2, um bucket S3, um Elastic Load Balancer ou uma configuração do Route 53) e a distribuição (o arranjo de localizações de borda a partir da origem ou basicamente da própria rede). 

# CloudFront e AWS Global Accelerator
CloudFront é uma rede de entrega de conteúdo (CDN) fornecida pela AWS. Ele melhora o desempenho de leitura armazenando conteúdo em cache em locais de borda e, assim, proporcionando uma melhor experiência do usuário, reduzindo a latência do aplicativo.

O CloudFront possui 216 pontos de presença em todo o mundo. Ele suporta vários tipos de origens - buckets S3, origens personalizadas (qualquer endpoint HTTP - como uma instância EC2, ALB, site S3 etc.)

💡 Você pode limitar o acesso de um bucket S3 apenas ao CloudFront usando a Política de acesso de origem (OAC) + as políticas de bucket S3 necessárias, fazendo com que os objetos S3 ainda sejam acessíveis globalmente. 💡 CloudFront com S3 deve ser usado para conteúdo estático que deve estar disponível em qualquer lugar. A replicação entre regiões S3 deve ser usada para conteúdo dinâmico que precisa estar disponível apenas em algumas regiões e com baixa latência.
O CloudFront fornece o recurso de restrição geográfica que permite restringir o acesso ao seu conteúdo com base na localização geográfica do visualizador. Você pode criar uma lista de permissões/lista de bloqueio para essa finalidade. O CloudFront usa um terceiro banco de dados para detectar o país do usuário usando o IP do usuário.

O custo de saída varia entre os pontos de presença. Isso é o CloudFront nos oferece 3 classes de preços -

Classe de preço 100 – Somente pontos de presença com custos de saída mais baratos são usados.
Classe de Preço 200 - Esta classe é mais cara que a anterior e abrange mais regiões que a primeira. Se a baixa latência for importante, considere usar esta classe.
Classe de Preço Todas - Esta classe é a mais cara e abrange todas as regiões. Se o conteúdo for muito importante e precisar estar disponível em qualquer lugar, esta é a faixa de preço recomendada.

# Detalhes principais do CloudFront:
+ Quando o conteúdo é armazenado em cache, isso é feito por um determinado limite de tempo chamado Time To Live, ou TTL, que é sempre em segundos
+ Se necessário, o CloudFront pode servir sites inteiros, incluindo conteúdo dinâmico, estático, de streaming e interativo.
+ As solicitações são sempre roteadas e armazenadas em cache no ponto de presença mais próximo do usuário, propagando assim os nós CDN e garantindo o melhor desempenho para solicitações futuras.
+ Existem dois tipos diferentes de distribuições:
  + Distribuição na Web: sites, itens normais em cache, etc.
  + RTMP: streaming de conteúdo, adobe, etc.
+ Os pontos de presença não são apenas somente leitura. Eles podem ser gravados, o que retornará o valor da gravação à origem.
+ O conteúdo armazenado em cache pode ser invalidado manualmente ou apagado além do TTL, mas isso acarreta um custo.
+ Você pode invalidar a distribuição de determinados objetos ou diretórios inteiros para que o conteúdo seja sempre carregado diretamente da origem. A invalidação do conteúdo também é útil durante a depuração se o conteúdo extraído da origem parecer correto, mas extrair esse mesmo conteúdo de um ponto de presença parecer incorreto.
+ Você pode configurar um failover para a origem criando um grupo de origem com duas origens dentro. Uma origem atuará como primária e a outra como secundária. O CloudFront alternará automaticamente entre os dois quando a origem primária falhar.
+ O Amazon CloudFront entrega seu conteúdo de cada ponto de presença e oferece um recurso SSL personalizado com IP dedicado. SNI Custom SSL funciona com a maioria dos navegadores modernos.
+ Se você executar cargas de trabalho compatíveis com PCI ou HIPAA e precisar registrar dados de uso, poderá fazer o seguinte:
  + Habilite os logs de acesso do CloudFront.
  + Capture solicitações enviadas para a API do CloudFront.
+ Uma Origin Access Identity (OAI) é usada para compartilhar conteúdo privado por meio do CloudFront. O OAI é um usuário virtual que será usado para conceder permissão à distribuição do CloudFront para buscar um objeto privado de sua origem (por exemplo, bucket S3).
  
# URLs assinados e cookies assinados do CloudFront:
+URLs assinados e cookies assinados do CloudFront fornecem a mesma funcionalidade básica: eles permitem que você controle quem pode acessar seu conteúdo. Esses recursos existem porque muitas empresas que distribuem conteúdo pela Internet desejam restringir o acesso a documentos, dados comerciais, fluxos de mídia ou conteúdo destinado a usuários selecionados. Por exemplo, os usuários que pagaram uma taxa deveriam poder acessar conteúdo privado que os usuários do nível gratuito não deveriam.
+ Se você quiser fornecer conteúdo privado por meio do CloudFront e estiver tentando decidir se deseja usar URLs assinados ou cookies assinados, considere o seguinte:
  + Use URLs assinados nos seguintes casos:
    + Você deseja usar uma distribuição RTMP. Cookies assinados não são compatíveis com distribuições RTMP.
    + Você deseja restringir o acesso a arquivos individuais, por exemplo, um download de instalação do seu aplicativo.
    + Seus usuários estão usando um cliente (por exemplo, um cliente HTTP personalizado) que não oferece suporte a cookies.
  + Use cookies assinados para os seguintes casos:
    + Você deseja fornecer acesso a vários arquivos restritos. Por exemplo, todos os arquivos de um vídeo em formato HLS ou todos os arquivos da área de usuários pagos de um site.
    + Você não deseja alterar seus URLs atuais.
   
#Snowball
Snowball simplificado:
Snowball é um disco físico gigante usado para migrar grandes quantidades de dados para a AWS. É uma solução de transporte de dados em escala de peta bytes. Usar um disco grande como o Snowball ajuda a contornar problemas comuns de transferência de dados em grande escala, como altos custos de rede, longos tempos de transferência e preocupações de segurança. As bolas de neve são extremamente seguras por design e, quando a transferência de dados é concluída, seus dados são apagados.

Detalhes principais do Snowball:
Snowball é uma escolha forte para um trabalho de transferência de dados se você precisar de uma transferência de dados rápida e segura que varia de terabytes a muitos petabytes para a AWS.
O Snowball também pode ser a escolha certa se você não quiser fazer atualizações caras em sua infraestrutura de rede existente, se enfrentar frequentemente grandes acúmulos de dados, se estiver localizado em um ambiente fisicamente isolado ou se estiver em um ambiente área onde conexões de internet de alta velocidade não estão disponíveis ou têm um custo proibitivo.
Como regra geral, se levar mais de uma semana para carregar seus dados na AWS usando a capacidade disponível de sua conexão de Internet existente, considere usar o Snowball.
Por exemplo, se você tiver uma conexão de 100 Mb que possa dedicar exclusivamente à transferência de seus dados e precisar transferir 100 TB de dados no total, levará mais de 100 dias para que a transferência seja concluída nessa conexão. Você pode fazer a mesma transferência em cerca de uma semana usando vários Snowballs.
Aqui está uma referência de quando o Snowball deve ser considerado com base no número de dias que seriam necessários para fazer a mesma transferência através de uma conexão com a Internet:

![image](https://github.com/Marianalima31/guia-de-estudo-aws-solutions-architect-associate/assets/77506074/f569c26f-da0e-40aa-aa21-4c44338b6fe7)


Snowball Edge e Snowmobile:
Snowball Edge é um tipo específico de Snowball que vem com recursos de computação e armazenamento por meio do AWS Lambda e tipos específicos de instância do EC2. Isso significa que você pode executar código em sua bola de neve enquanto seus dados estão a caminho de um data center da Amazon. Isso permite o suporte de cargas de trabalho locais em locais remotos ou off-line e, como resultado, o Snowball Edge não precisa se limitar a um serviço de transferência de dados. Um caso de uso interessante é com aviões comerciais. Às vezes, os aviões voam com bordas de bola de neve a bordo para que possam armazenar grandes quantidades de dados de voo e calcular as funções necessárias para os próprios sistemas do avião. O Snowball Edges também pode ser agrupado localmente para um desempenho ainda melhor.
Snowmobile é uma solução de transferência de dados em escala de exabytes. É uma solução de transporte de dados para 100 petabytes de dados e está contida em um contêiner de 45 pés transportado por um semi-caminhão. Essa transferência massiva faz sentido se você deseja mover todo o seu data center com anos de dados para a nuvem.

# Gateway de armazenamento
Gateway de armazenamento simplificado:
Storage Gateway é um serviço que conecta ambientes locais com armazenamento baseado em nuvem para integrar de forma contínua e segura um aplicativo local com um back-end de armazenamento em nuvem. O Storage Gateway vem em três sabores: File Gateway, Volume Gateway e Tape Gateway.

Detalhes principais do gateway de armazenamento:
+ O serviço Storage Gateway pode ser um dispositivo físico ou uma imagem de VM baixada em um host em um data center local. Ele atua como uma ponte para enviar ou receber dados da AWS.
+O Storage Gateway pode ser baseado no hipervisor ESXi da VMWare para máquinas Linux e no hipervisor Hyper-V da Microsoft para máquinas Windows.
+Os três tipos de gateways de armazenamento estão abaixo:
  + File Gateway - Opera via NFS ou SMB e é usado para armazenar arquivos no S3 em um ponto de montagem do sistema de arquivos de rede na máquina virtual fornecida. Simplificando, você pode pensar em um File Gateway como uma montagem de sistema de arquivos no S3.
  + Volume Gateway - Opera via iSCSI e é usado para armazenar cópias de unidades de disco rígido ou unidades de disco rígido virtuais no S3. Isso pode ser alcançado por meio de volumes armazenados ou volumes em cache . Simplificando, você pode pensar no Volume Gateway como uma forma de armazenar unidades de disco rígido virtuais na nuvem.
  + Tape Gateway - Opera como uma biblioteca de fitas virtual
+ As informações relevantes do arquivo que passam pelo Storage Gateway, como propriedade do arquivo, permissões, carimbos de data/hora etc., são armazenadas como metadados para os objetos aos quais pertencem. Depois que esses detalhes do arquivo forem armazenados no S3, eles poderão ser gerenciados nativamente. Isso significa que todos os recursos do S3, como controle de versão, gerenciamento de ciclo de vida, políticas de bucket, replicação entre regiões, etc., podem ser aplicados como parte do Storage Gateway.
+ A interface dos aplicativos com a AWS por meio do Volume Gateway é feita por meio do protocolo de bloco iSCSI. Os dados gravados nesses volumes podem ter backup assíncrono no AWS Elastic Block Store (EBS) como instantâneos pontuais do conteúdo dos volumes. Esses tipos de instantâneos atuam como backups incrementais que capturam apenas o estado alterado, semelhante a uma solicitação pull no Git. Além disso, todos os instantâneos são compactados para reduzir os custos de armazenamento.
+ O Tape Gateway oferece uma maneira durável e econômica de arquivar e replicar dados no S3 e, ao mesmo tempo, eliminar fitas (armazenamento de dados tradicional). A Virtual Tape Library, ou VTL, aproveita a infraestrutura de backup baseada em fita existente para armazenar dados em cartuchos de fita virtuais criados no Tape Gateway. É uma ótima maneira de modernizar e mover backups para a nuvem.

Volumes armazenados versus volumes em cache:
+ Volumes armazenados do Volume Gateway permitem armazenar dados localmente no local e fazer backup dos dados na AWS como uma fonte de dados secundária. Os volumes armazenados permitem acesso de baixa latência a conjuntos de dados inteiros, ao mesmo tempo que fornecem alta disponibilidade em uma solução de nuvem híbrida. Além disso, você pode montar volumes armazenados na infraestrutura de aplicativos como unidades iSCSI para que, quando os dados forem gravados nesses volumes, os dados sejam gravados no hardware local e tenham backup assíncrono como instantâneos no AWS EBS ou S3.

    + No diagrama a seguir de uma arquitetura de volume armazenado, os dados são fornecidos ao usuário pela rede de área de armazenamento, armazenamento conectado à rede ou armazenamento conectado diretamente em seu data center. O S3 existe apenas como um backup seguro e confiável.
![image](https://github.com/Marianalima31/guia-de-estudo-aws-solutions-architect-associate/assets/77506074/c92365b2-736d-4e8d-8fa5-385d89c8733d)


+Os volumes em cache do Volume Gateway diferem porque não armazenam todo o conjunto de dados localmente como os volumes armazenados. Em vez disso, a AWS é usada como fonte de dados primária e o hardware local é usado como camada de cache. Apenas os componentes usados ​​com mais frequência são retidos na infraestrutura local, enquanto os dados restantes são fornecidos pela AWS. Isso minimiza a necessidade de dimensionar a infraestrutura local, mantendo ao mesmo tempo o acesso de baixa latência aos dados mais referenciados.

  + No diagrama a seguir de uma arquitetura de volume em cache, os dados acessados ​​com mais frequência são fornecidos ao usuário pela rede de área de armazenamento, armazenamento conectado à rede ou armazenamento conectado diretamente em seu data center. S3 atende o restante dos dados da AWS.
![image](https://github.com/Marianalima31/guia-de-estudo-aws-solutions-architect-associate/assets/77506074/d47861ce-c7fb-4712-90de-b54aac9be30b)

# Nuvem de computação elástica (EC2)
EC2 simplificado:
O EC2 ativa instâncias de servidor redimensionáveis ​​que podem ser ampliadas e reduzidas rapidamente. Uma instância é um servidor virtual na nuvem. Com o Amazon EC2, você pode instalar e configurar o sistema operacional e os aplicativos executados na sua instância. Sua configuração na inicialização é uma cópia ativa da Amazon Machine Image (AMI) que você especifica ao executar a instância. O EC2 tem um prazo extremamente reduzido para provisionar e inicializar novas instâncias e o EC2 garante que você pague conforme usa, pague pelo que usa, pague menos quando usar mais e pague ainda menos quando reservar capacidade. Quando sua instância EC2 está em execução, você é cobrado pela CPU, memória, armazenamento e rede. Quando ele é interrompido, você será cobrado apenas pelo armazenamento do EBS.

Detalhes principais do EC2:
+ Você pode executar diferentes tipos de instâncias a partir de uma única AMI. Um tipo de instância determina essencialmente o hardware do computador host usado para sua instância. Cada tipo de instância oferece diferentes recursos de computação e memória. Você deve selecionar um tipo de instância com base na quantidade de memória e capacidade de computação necessária para o aplicativo ou software que planeja executar na instância.
+ Você pode executar várias instâncias de uma AMI, conforme mostrado na figura a seguir:
![image](https://github.com/Marianalima31/guia-de-estudo-aws-solutions-architect-associate/assets/77506074/9b4a87ab-fef3-48c4-a24a-b3e73ca0fed4)

+ Você tem a opção de usar locação dedicada com sua instância. Isso significa que dentro de um data center da AWS, você tem acesso exclusivo ao hardware físico. Naturalmente, essa opção tem um custo alto, mas faz sentido se você trabalha com tecnologia que possui uma política de licenciamento rígida.
Com o EC2 VM Import, você pode importar VMs existentes para a AWS, desde que esses hosts usem os formatos de virtualização VMware ESX, VMware Workstation, Microsoft Hyper-V ou Citrix Xen.
+ Quando você inicia uma nova instância do EC2, o EC2 tenta colocar a instância de forma que todas as suas VMs fiquem espalhadas por diferentes hardwares para limitar a falha em um único local. Você pode usar grupos de posicionamento para influenciar o posicionamento de um grupo de instâncias interdependentes que atendem às necessidades da sua carga de trabalho. Há uma explicação sobre grupos de canais em uma seção abaixo.
+ Ao executar uma instância no Amazon EC2, você tem a opção de transmitir dados do usuário para a instância quando ela for iniciada. Esses dados do usuário podem ser usados ​​para executar tarefas ou scripts comuns de configuração automatizada. Por exemplo, você pode passar um script bash que garanta que o htop esteja instalado no novo host EC2 e esteja sempre ativo.
+ Por padrão, o endereço IP público de uma instância EC2 é liberado quando a instância é interrompida, mesmo que esteja interrompida temporariamente. Portanto, é melhor referir-se a uma instância pelo seu nome de host DNS externo. Se você precisar de um endereço IP público persistente que possa ser associado à mesma instância, use um endereço IP elástico que seja basicamente um endereço IP estático.
+ Se você tiver requisitos para autogerenciar um banco de dados SQL, o EC2 pode ser uma alternativa sólida ao RDS. Para garantir alta disponibilidade, lembre-se de ter pelo menos uma outra instância do EC2 em uma zona de disponibilidade separada para que, mesmo se uma instância de banco de dados falhar, as outras ainda estarão disponíveis.
+ Uma imagem dourada é simplesmente uma AMI que você personalizou totalmente de acordo com sua preferência, com todos os detalhes de software/dados/configuração necessários definidos e prontos para uso uma vez. Essa AMI pessoal pode então ser a fonte a partir da qual você inicia novas instâncias.
+ As verificações de status da instância verificam a integridade do servidor EC2 em execução, a verificação de status dos sistemas monitora a integridade do hipervisor subjacente. Se você notar um problema de status do sistema, basta parar a instância e iniciá-la novamente (sem necessidade de reinicializar), pois a VM será reiniciada em um novo hipervisor.

Preço da instância EC2:

+ Instâncias sob demanda são baseadas em uma taxa fixa por hora ou segundo. Como o nome indica, você pode iniciar uma instância sob demanda sempre que precisar e interrompê-la quando não precisar mais dela. Não há exigência de um compromisso de longo prazo.
+ As instâncias reservadas garantem que você mantenha o uso exclusivo de uma instância em termos de contrato de 1 ou 3 anos. O compromisso de longo prazo oferece descontos significativamente reduzidos na tarifa horária.
+ As instâncias spot aproveitam o excesso de capacidade da Amazon e funcionam de maneira interessante. Para usá-los, você deve fazer uma oferta financeira para ter acesso. Como as instâncias spot só estão disponíveis quando a Amazon tem capacidade excedente, essa opção só faz sentido se seu aplicativo tiver horários de início e término flexíveis. Você não será cobrado se sua instância for interrompida devido a uma alteração de preço (por exemplo, alguém acabou de oferecer um preço mais alto pelo acesso) e, consequentemente, sua carga de trabalho não for concluída. No entanto, se você mesmo encerrar a instância, será cobrado por qualquer hora de execução da instância. As instâncias spot normalmente são usadas em trabalhos de processamento em lote.
  
Reservado Padrão vs. Reservado Conversível vs. Reservado Programado:

+ Instâncias reservadas padrão têm reservas inflexíveis com desconto de 75% nas instâncias sob demanda. As Instâncias Reservadas Padrão não podem ser movidas entre regiões. Você pode escolher se uma instância reservada se aplica a uma zona de disponibilidade específica ou a uma região inteira, mas não pode alterar a região.
+ Instâncias reservadas conversíveis são instâncias com desconto de 54% em relação às instâncias sob demanda, mas você também pode modificar o tipo de instância a qualquer momento. Por exemplo, você suspeita que depois de alguns meses sua VM talvez precise mudar de uso geral para otimização de memória, mas ainda não tem certeza. Portanto, se você acha que no futuro poderá precisar alterar o tipo de VM ou atualizar a capacidade das VMs, escolha Instâncias reservadas conversíveis. Porém, não há downgrade do tipo de instância com esta opção.
+ As Instâncias Reservadas Agendadas são reservadas de acordo com um cronograma especificado que você define. Por exemplo, você poderá usar Instâncias reservadas agendadas se executar software educacional que só precisa estar disponível durante o horário escolar. Esta opção permite combinar melhor a capacidade necessária com uma programação recorrente para que você possa economizar dinheiro.
  
Ciclo de vida da instância EC2:
A tabela a seguir destaca os vários estados de instância em que uma VM pode estar em um determinado momento.

| Estado da instância  |                          Descrição	                         | Cobrança | 
| -------------------- | ----------------------------------------------------------- | ------------------------------------------------|
| pending              | A instância se prepara para entrar no running estado. Uma   | Não faturado
|                      |  instância entra no estado pendente quando é executada      | 
|                      |  pela primeira vez ou quando é iniciada após estar          |
|                      |  no stoppedestado.                                          |
|                      |                                                             |
| running              | A instância está em execução e pronta para uso.	           | Faturado
|                      |                                                             |
| stopping	           | A instância está se preparando para ser interrompida ou     | Não cobrado se estiver se preparando para parar.
|                      | colocada em hibernação.                                     | Faturado se estiver se preparando para hibernar
|                      |                                                             |
| stopped	             | A instância está encerrada e não pode ser usada. A          | Não faturado
|                      | instância pode ser iniciada a qualquer momento.             |
|                      |                                                             |
| shutting-down	       | A instância está se preparando para ser encerrada.          |  Não faturado
|                      |                                                             |
| terminated	         | A instância foi excluída permanentemente e não pode         |  Não faturado
|                      | ser iniciada.	                                             |



# Segurança EC2:
Ao implantar uma instância do Amazon EC2, você é responsável pelo gerenciamento do sistema operacional convidado (incluindo atualizações e patches de segurança), qualquer software aplicativo ou utilitário instalado nas instâncias e pela configuração do firewall fornecido pela AWS (chamado de grupo de segurança ) em cada instância.
Com o EC2, a proteção contra encerramento da instância fica desabilitada por padrão. Isso significa que você não tem uma proteção contra o encerramento acidental de sua instância. Você deve ativar esse recurso se quiser uma proteção extra.
O Amazon EC2 usa criptografia de chave pública para criptografar e descriptografar informações de login. A criptografia de chave pública usa uma chave pública para criptografar um dado, como uma senha, e o destinatário usa sua chave privada para descriptografar os dados. As chaves pública e privada são conhecidas como par de chaves.
Você pode criptografar o volume do dispositivo raiz, onde você instala o sistema operacional subjacente. Você pode fazer isso durante a criação da instância ou com ferramentas de terceiros, como o bit locker. É claro que volumes EBS adicionais ou secundários também são criptografáveis.
Por padrão, uma instância do EC2 com um volume raiz do AWS Elastic Block Store (EBS) anexado será excluída junto quando a instância for encerrada. No entanto, qualquer volume EBS adicional ou secundário que também esteja anexado à mesma instância será preservado. Isso ocorre porque o volume raiz do EBS é para instalações de sistema operacional e outras configurações de baixo nível. Esta regra pode ser modificada, mas geralmente é mais fácil inicializar uma nova instância com um novo volume de dispositivo raiz do que usar um antigo.
Grupos de colocação EC2:
Os grupos de posicionamento equilibram a compensação entre tolerância ao risco e desempenho da rede quando se trata da sua frota de instâncias do EC2. Quanto mais você se preocupa com o risco, mais isoladas você deseja que suas instâncias fiquem umas das outras. Quanto mais você se preocupa com o desempenho, mais unidas você deseja que suas instâncias sejam umas com as outras.

Existem três tipos diferentes de grupos de posicionamento EC2:

1.) Grupos de posicionamento agrupados

Clustered Placement Grouping ocorre quando você coloca todas as suas instâncias do EC2 em uma única zona de disponibilidade. Isso é recomendado para aplicativos que precisam da menor latência possível e do maior rendimento de rede.
Somente determinadas instâncias podem ser iniciadas neste grupo (otimizadas para computação, otimizadas para GPU, otimizadas para armazenamento e otimizadas para memória).
2.) Grupos de canais de distribuição

Spread Placement Grouping é quando você coloca cada instância individual do EC2 em cima de seu próprio hardware distinto para que a falha seja isolada.
Suas VMs ficam em racks separados, com entradas de rede separadas e requisitos de energia separados. Os grupos de colocação espalhados são recomendados para aplicativos que possuem um pequeno número de instâncias críticas que devem ser mantidas separadas umas das outras.
3.) Grupos de posicionamento particionados

O agrupamento de posicionamentos particionados é semelhante ao agrupamento de posicionamentos espalhados, mas difere porque você pode ter várias instâncias do EC2 em uma única partição. Em vez disso, a falha é isolada em uma partição (digamos, 3 ou 4 instâncias em vez de 1), mas você aproveita os benefícios da proximidade para melhorar o desempenho da rede.
Com esse grupo de posicionamento, você tem várias instâncias vivendo juntas no mesmo hardware dentro de diferentes zonas de disponibilidade em uma ou mais regiões.
Se desejar um equilíbrio entre tolerância ao risco e desempenho da rede, use Partitioned Placement Groups.
Cada nome de grupo de posicionamento em sua AWS deve ser exclusivo

Você pode mover uma instância existente para um grupo de posicionamento, desde que ela esteja parada. Você pode mover a instância por meio da CLI ou de um SDK da AWS, mas não pelo console. Você também pode tirar um snapshot da instância existente, convertê-la em uma AMI e iniciá-la no grupo de posicionamento onde deseja que ela esteja.

Armazenamento de blocos elásticos (EBS)
EBS simplificado:
Um volume do Amazon EBS é um dispositivo de armazenamento durável em nível de bloco que você pode anexar a uma única instância do EC2. Você pode pensar no EBS como um disco rígido virtual baseado em nuvem. Você pode usar volumes do EBS como armazenamento primário para dados que exigem atualizações frequentes, como a unidade do sistema para uma instância ou o armazenamento para um aplicativo de banco de dados. Você também pode usá-los para aplicativos com alto rendimento que executam varreduras contínuas de disco.

Detalhes principais do EBS:
Os volumes do EBS persistem independentemente da vida útil de uma instância do EC2.
Cada volume do EBS é replicado automaticamente em sua zona de disponibilidade para proteção contra falhas de componentes e recuperação de desastres (semelhante ao Standard S3).
Existem cinco tipos diferentes de armazenamento EBS:
Uso Geral (SSD)
IOPS provisionadas (SSD, desenvolvidas para velocidade)
Unidade de disco rígido com rendimento otimizado (magnética, construída para cargas de dados maiores)
Unidade de disco rígido fria (magnética, desenvolvida para cargas de trabalho acessadas com menos frequência)
Magnético
Os volumes EBS oferecem SLA de 99,999%.
Onde quer que esteja sua instância EC2, seu volume estará na mesma zona de disponibilidade
Um volume EBS só pode ser anexado a uma instância EC2 por vez.
Depois de criar um volume, você poderá anexá-lo a qualquer instância do EC2 na mesma zona de disponibilidade.
O Amazon EBS oferece a capacidade de criar snapshots (backups) de qualquer volume do EBS e gravar uma cópia dos dados do volume no S3, onde são armazenados de forma redundante em várias zonas de disponibilidade.
Um instantâneo do EBS reflete o conteúdo do volume durante um instante concreto no tempo.
Uma imagem (AMI) é a mesma coisa, mas inclui um sistema operacional e um carregador de boot para que possa ser usada para inicializar uma instância.
As AMIs também podem ser consideradas servidores pré-preparados e inicializáveis. AMIs são sempre usadas ao executar uma instância.
Ao provisionar uma instância do EC2, uma AMI é, na verdade, a primeira coisa que você deve especificar. Você pode escolher uma AMI pré-fabricada ou escolher a sua própria, criada a partir de um snapshot do EBS.
Você também pode usar os seguintes critérios para ajudar a escolher sua AMI:
Sistema operacional
Arquitetura (32 bits ou 64 bits)
Região
Permissões de lançamento
Armazenamento de dispositivo raiz (mais na seção relevante abaixo)
Você pode copiar AMIs para regiões totalmente novas.
Ao copiar AMIs para novas regiões, a Amazon não copiará permissões de execução, tags definidas pelo usuário ou permissões de bucket do Amazon S3 da AMI de origem para a nova AMI. Você deve garantir que esses detalhes estejam definidos corretamente para as instâncias na nova região.
Você pode alterar os volumes do EBS dinamicamente, incluindo o tamanho e o tipo de armazenamento
SSD versus HDD:
Os volumes apoiados por SSD são criados para cargas de trabalho transacionais que envolvem operações frequentes de leitura/gravação, onde o atributo de desempenho dominante é IOPS. Regra geral : sua carga de trabalho será pesada em IOPS? Planeje para SSD.
Os volumes suportados por HDD são criados para grandes cargas de trabalho de streaming em que a taxa de transferência (medida em MiB/s) é uma medida de desempenho melhor do que IOPS. Regra prática : sua carga de trabalho terá alto rendimento? Planeje o HDD.
hdd_vs_ssd

Instantâneos do EBS:
Os snapshots do EBS são cópias pontuais de volumes. Você pode pensar em instantâneos como fotografias do estado atual do disco e do estado de tudo dentro dele.
Um instantâneo é restrito à região onde foi criado.
Os instantâneos capturam apenas o estado de alteração desde quando o último instantâneo foi obtido. Isto é o que é registrado em cada novo instantâneo, não o estado inteiro do servidor.
Por causa disso, pode levar algum tempo para que seu primeiro snapshot seja criado. Isso ocorre porque a mudança de estado do primeiro instantâneo é todo o novo volume. Só depois o delta será capturado porque haverá algo anterior para comparar.
Os snapshots do EBS ocorrem de forma assíncrona, o que significa que um volume pode ser usado normalmente enquanto um snapshot está ocorrendo.
Ao criar um instantâneo para um dispositivo raiz futuro, considera-se uma prática recomendada interromper a instância em execução onde o dispositivo original está antes de tirar o instantâneo.
A maneira mais fácil de mover uma instância e um volume do EC2 para outra zona de disponibilidade é tirar um snapshot.
Ao criar uma imagem a partir de um instantâneo, se você quiser implantar um tipo de volume diferente para a nova imagem (por exemplo, SSD de uso geral -> HDD otimizado para taxa de transferência), certifique-se de que a virtualização da nova imagem seja assistida por hardware.
Um breve resumo para criar cópias de instâncias EC2: Instância antiga -> Instantâneo -> Imagem (AMI) -> Nova instância
Você não pode excluir um snapshot de um volume EBS usado como dispositivo raiz de uma AMI registrada. Se o snapshot original fosse excluído, a AMI não conseguiria usá-lo como base para criar novas instâncias. Por esse motivo, a AWS protege você contra a exclusão acidental do instantâneo do EBS, pois isso pode ser crítico para seus sistemas. Para excluir um instantâneo do EBS anexado a uma AMI registrada, primeiro remova a AMI e, em seguida, o instantâneo poderá ser excluído.
Armazenamento de dispositivo raiz EBS:
Todos os volumes raiz da AMI (onde o sistema operacional do EC2 está instalado) são de dois tipos: apoiados por EBS ou apoiados por armazenamento de instância
Ao excluir uma instância do EC2 que estava usando um volume raiz baseado no Instance Store, seu volume raiz também será excluído. Quaisquer volumes adicionais ou secundários persistirão.
Se você usar um volume raiz apoiado por EBS, o volume raiz não será encerrado com sua instância EC2 quando a instância for colocada offline. Os volumes apoiados pelo EBS não são dispositivos de armazenamento temporário como os volumes apoiados pelo Instance Store.
Os volumes apoiados pelo EBS são iniciados a partir de um snapshot do AWS EBS, como o nome indica
Os volumes apoiados pelo armazenamento de instâncias são iniciados a partir de um modelo armazenado AWS S3. Eles são efêmeros, então tome cuidado ao encerrar uma instância!
Os armazenamentos de instâncias secundárias para um dispositivo raiz com suporte de armazenamento de instâncias devem ser instalados durante o provisionamento original do servidor. Você não pode adicionar mais após o fato. No entanto, você pode adicionar volumes EBS à mesma instância após a criação do servidor.
Com essas desvantagens dos volumes do Instance Store, por que escolher um? Porque eles têm uma taxa de IOPS muito alta. Portanto, embora um armazenamento de instâncias não possa fornecer persistência de dados, ele pode fornecer IOPS muito mais altas em comparação com armazenamento conectado à rede, como o EBS.
Além disso, os armazenamentos de instâncias são ideais para armazenamento temporário de informações que mudam frequentemente, como buffers, caches, dados temporários e outros conteúdos temporários, ou para dados que são replicados em uma frota de instâncias, como um pool de servidores web com balanceamento de carga. .
Quando usar um em vez do outro?
Use o EBS para dados de banco de dados, logs críticos e configurações de aplicativos.
Use o armazenamento de instâncias para dados em processo, logs não críticos e estado transitório do aplicativo.
Use o S3 para dados compartilhados entre sistemas, como conjuntos de dados de entrada e resultados processados, ou para dados estáticos necessários para cada novo sistema quando lançado.
Criptografia EBS:
A criptografia EBS oferece uma solução de criptografia simples para recursos EBS que não exige que você crie, mantenha e proteja sua própria infraestrutura de gerenciamento de chaves.
Ele usa chaves mestras do cliente (CMK) do AWS Key Management Service (AWS KMS) ao criar volumes e snapshots criptografados.
Você pode criptografar o dispositivo raiz e os volumes secundários de uma instância do EC2. Quando você cria um volume EBS criptografado e o anexa a um tipo de instância compatível, os seguintes tipos de dados são criptografados:
Dados em repouso dentro do volume
Todos os dados transferidos entre o volume e a instância
Todos os instantâneos criados a partir do volume
Todos os volumes criados a partir desses instantâneos
O EBS criptografa seu volume com uma chave de dados usando o algoritmo AES-256.
Instantâneos de volumes criptografados também são criptografados naturalmente. Os volumes restaurados de snapshots criptografados também são criptografados. Você só pode compartilhar instantâneos não criptografados.
A maneira antiga de criptografar um dispositivo raiz era criar um instantâneo de uma instância EC2 provisionada. Ao fazer uma cópia desse instantâneo, você ativou a criptografia durante a criação da cópia. Por fim, depois que a cópia foi criptografada, você criou uma AMI a partir da cópia criptografada e passou a ter uma instância EC2 com criptografia no dispositivo raiz. Devido à complexidade disso, agora você pode simplesmente criptografar dispositivos raiz como parte das opções de provisionamento do EC2.
Interfaces de Rede Elástica (ENI)
ENI simplificado:
Uma interface de rede elástica é um componente de rede que representa uma placa de rede virtual. Ao provisionar uma nova instância, uma ENI será anexada automaticamente e você poderá criar e configurar interfaces de rede adicionais, se desejar. Ao mover uma interface de rede de uma instância para outra, o tráfego de rede é redirecionado para a nova instância.

Detalhes principais da ENI:
ENI é usado principalmente para soluções de rede de baixo orçamento e alta disponibilidade
No entanto, se você suspeitar que precisa de alto rendimento de rede, poderá usar o Enhanced Networking ENI.
Rede aprimorada A ENI usa virtualização de E/S de raiz única para fornecer recursos de rede de alto desempenho em tipos de instância compatíveis. O SR-IOV fornece maior E/S e menor rendimento e garante maior largura de banda, maior desempenho de pacotes por segundo (PPS) e latências entre instâncias consistentemente mais baixas. O SR-IOV faz isso dedicando a interface a uma única instância e ignorando efetivamente partes do hipervisor, o que permite melhor desempenho.
Adicionar mais ENIs não necessariamente acelerará o rendimento da sua rede, mas o Enhanced Networking ENI sim.
Não há custo extra para usar o Enhanced Networking ENI e o melhor desempenho de rede que ele oferece. A única desvantagem é que o Enhanced Networking ENI não está disponível em todas as famílias e tipos de instâncias do EC2.
Você pode anexar uma interface de rede a uma instância do EC2 das seguintes maneiras:
Quando está em execução (anexação a quente)
Quando está parado (anexação quente)
Quando a instância está sendo executada (anexação a frio).
Se uma instância do EC2 falhar com o ENI configurado corretamente, você (ou, mais provavelmente, o código em execução em seu nome) poderá anexar a interface de rede a uma instância de espera ativa. Como as interfaces ENI mantêm seus próprios endereços IP privados, endereços IP elásticos e endereços MAC, o tráfego de rede começará a fluir para a instância em espera assim que você conectar a interface de rede à instância de substituição. Os usuários experimentarão uma breve perda de conectividade entre o momento em que a instância falha e o momento em que a interface de rede é anexada à instância em espera, mas nenhuma alteração na tabela de rotas da VPC ou no servidor DNS é necessária.
Para instâncias que trabalham com Machine Learning e High Performance Computing, utilize EFA (Elastic Fabric Adaptor). Os EFAs aceleram o trabalho exigido nos casos de uso acima. O EFA fornece latência mais baixa e mais consistente e maior rendimento do que o transporte TCP tradicionalmente usado em sistemas de computação de alto desempenho baseados em nuvem.
O EFA também pode usar OS-bypass (somente no Linux) que permitirá que aplicativos de ML e HPC interajam diretamente com o Elastic Fabric Adapter, em vez de serem normalmente roteados para ele por meio do sistema operacional. Isso proporciona um enorme aumento de desempenho.
Você pode ativar um log de fluxo de VPC em sua interface de rede para capturar informações sobre o tráfego IP que entra e sai de uma interface de rede.
Grupos de segurança
Grupos de segurança simplificados:
Grupos de segurança são usados ​​para controlar o acesso (SSH, HTTP, RDP, etc.) com EC2. Eles atuam como um firewall virtual para suas instâncias controlarem o tráfego de entrada e saída. Ao executar uma instância em uma VPC, você pode atribuir até cinco grupos de segurança à instância, e os grupos de segurança atuam no nível da instância, não no nível da sub-rede.

Detalhes principais dos grupos de segurança:
Os grupos de segurança controlam o tráfego de entrada e saída para suas instâncias (eles atuam como um firewall para instâncias EC2), enquanto os NACLs controlam o tráfego de entrada e saída para suas sub-redes (eles atuam como um firewall para sub-redes). Os grupos de segurança geralmente controlam a lista de portas que podem ser usadas pelas instâncias do EC2 e os NACLs controlam qual rede ou lista de endereços IP pode se conectar a toda a sua VPC.
Cada vez que você faz uma alteração em um grupo de segurança, essa alteração ocorre imediatamente
Sempre que você cria uma regra de entrada, uma regra de saída é criada imediatamente. Isso ocorre porque os grupos de segurança têm estado . Isso significa que quando você cria uma regra de entrada para um grupo de segurança, uma regra de saída correspondente é criada para corresponder a ela. Isto contrasta com os NACLs que não têm estado e requerem intervenção manual para criar regras de entrada e de saída.
As regras do Grupo de Segurança são baseadas em ALLOWs e não existe o conceito de DENY quando se trata de Grupos de Segurança. Isso significa que você não pode negar explicitamente ou colocar portas específicas na lista negra por meio de grupos de segurança; você só pode negá-las implicitamente, excluindo-as da sua lista ALLOWs
Devido ao detalhe acima, tudo está bloqueado por padrão. Você deve entrar e permitir intencionalmente o acesso a determinadas portas.
Os grupos de segurança são específicos de uma única VPC, portanto não é possível compartilhar um grupo de segurança entre várias VPCs. No entanto, você pode copiar um grupo de segurança para criar um novo grupo de segurança com as mesmas regras em outra VPC para a mesma conta da AWS.
Os Grupos de Segurança são regionais e podem abranger AZs, mas não podem ser inter-regionais.
Existem regras de saída se você precisar conectar seu servidor a um serviço diferente, como um endpoint de API ou um backend de banco de dados. Você precisa habilitar a regra ALLOW para a porta correta para que o tráfego possa sair do EC2 e entrar no outro serviço AWS.
Você pode anexar vários grupos de segurança a uma instância do EC2 e pode ter várias instâncias do EC2 sob a égide de um grupo de segurança
Você pode especificar a origem do seu grupo de segurança (basicamente quem tem permissão para ignorar o firewall virtual) como um único endereço IP /32 , um intervalo de IP ou até mesmo um grupo de segurança separado.
Você não pode bloquear endereços IP específicos com grupos de segurança (em vez disso, use NACLs)
Você pode aumentar o limite do seu grupo de segurança enviando uma solicitação à AWS
Firewall de aplicativos da Web (WAF)
WAF simplificado:
AWS WAF é um aplicativo da web que permite permitir ou bloquear solicitações HTTP(s) vinculadas ao CloudFront, API Gateway, Application Load Balancers, EC2 e outros pontos de entrada da Camada 7 em seu ambiente AWS. O AWS WAF oferece controle sobre como o tráfego chega às suas aplicações, permitindo criar regras de segurança que bloqueiam padrões de ataque comuns, como injeção de SQL ou scripts entre sites, e regras que filtram padrões de tráfego específicos que você pode definir. O conjunto de regras padrão do WAF aborda questões como os 10 principais riscos de segurança do OWASP e é atualizado regularmente sempre que novas vulnerabilidades são descobertas.

Detalhes principais do WAF:
Conforme mencionado acima, o WAF opera como um firewall da Camada 7. Isso concede a capacidade de monitorar condições granulares baseadas na Web, como parâmetros de string de consulta de URL. Esse nível de detalhe ajuda a detectar crimes e problemas honestos com as solicitações repassadas ao seu ambiente AWS.
Com o WAF, você pode definir condições como quais endereços IP têm permissão para fazer quais tipos de solicitações ou acessar que tipo de conteúdo.
Com base nessas condições, o endpoint correspondente permitirá a solicitação servindo o conteúdo solicitado ou retornará um status HTTP 403 Proibido.
No nível mais simples, o AWS WAF permite escolher um dos seguintes comportamentos:
Permitir todas as solicitações, exceto aquelas especificadas : isso é útil quando você deseja que o CloudFront ou um Application Load Balancer forneça conteúdo para um site público, mas também deseja bloquear solicitações de invasores.
Bloquear todas as solicitações, exceto aquelas que você especificar : isso é útil quando você deseja fornecer conteúdo para um site restrito cujos usuários são facilmente identificáveis ​​por propriedades em solicitações da Web, como os endereços IP usados ​​para navegar no site.
Conte as solicitações que correspondem às propriedades especificadas : quando você deseja permitir ou bloquear solicitações com base em novas propriedades em solicitações da web, primeiro você pode configurar o AWS WAF para contar as solicitações que correspondem a essas propriedades sem permitir ou bloquear essas solicitações. Isso permite que você confirme que não configurou acidentalmente o AWS WAF para bloquear todo o tráfego do seu site. Quando tiver certeza de que especificou as propriedades corretas, você poderá alterar o comportamento para permitir ou bloquear solicitações.
Capacidades de proteção WAF:
As diferentes características de solicitação que podem ser utilizadas para limitar o acesso:
O endereço IP de onde uma solicitação se origina
O país de origem de uma solicitação
Os valores encontrados nos cabeçalhos da solicitação
Quaisquer strings que aparecem na solicitação (sejam strings específicas ou strings que correspondam a um padrão regex)
A duração da solicitação
Qualquer presença de código SQL (provavelmente uma tentativa de injeção de SQL)
Qualquer presença de um script (provavelmente uma tentativa de script entre sites)
Você também pode usar NACLs para bloquear endereços IP maliciosos, evitar injeções de SQL/XSS e bloquear solicitações de países específicos. No entanto, é uma boa prática praticar a defesa em profundidade.
Negar ou bloquear usuários mal-intencionados no nível do WAF tem a vantagem adicional de proteger seu ecossistema AWS em sua fronteira mais externa.
CloudWatch
CloudWatch simplificado:
Amazon CloudWatch é um serviço de monitoramento e observabilidade. Ele fornece dados e insights acionáveis ​​para monitorar seus aplicativos, responder a alterações de desempenho em todo o sistema, otimizar a utilização de recursos e obter uma visão unificada da integridade operacional.

Detalhes principais do CloudWatch:
O CloudWatch coleta dados operacionais e de monitoramento na forma de logs, métricas e eventos.
Você pode usar o CloudWatch para detectar comportamentos anômalos em seus ambientes, definir alarmes, visualizar logs e métricas lado a lado, executar ações automatizadas, solucionar problemas e descobrir insights para manter seus aplicativos funcionando perfeitamente.
Dentro do domínio de computação, o CloudWatch pode informar sobre a integridade de instâncias EC2, grupos de escalonamento automático, Elastic Load Balancers e verificações de integridade do Route53. Nos domínios de armazenamento e entrega de conteúdo, o CloudWatch pode informar sobre a integridade dos volumes EBS, gateways de armazenamento e CloudFront.
Com relação ao EC2, o CloudWatch só pode monitorar métricas no nível do host, como CPU, rede, disco e verificações de status, para obter insights como a integridade do hipervisor subjacente.
CloudWatch NÃO é CloudTrail, por isso é importante saber que somente o CloudTrail pode monitorar o acesso à AWS por motivos de segurança e auditoria. CloudWatch tem tudo a ver com desempenho. CloudTrail tem tudo a ver com auditoria.
O CloudWatch com EC2 monitorará eventos a cada 5 minutos por padrão, mas você poderá ter intervalos de 1 minuto se usar o monitoramento detalhado.
Captura de tela 17/06/2020 às 20h16 23h

Você pode personalizar seus painéis do CloudWatch para obter insights.
Existe um agente CloudWatch multiplataforma que pode ser instalado em instâncias baseadas em Linux e Windows. Esse agente permite selecionar as métricas a serem coletadas, incluindo métricas de sub-recursos, como núcleo por CPU. Você pode usar esse agente único para coletar métricas do sistema e arquivos de log de instâncias do Amazon EC2 e servidores locais.
As seguintes métricas não são coletadas de instâncias do EC2 por meio do CloudWatch:
Utilização de memória
Utilização de troca de disco
Utilização do espaço em disco
Utilização de arquivo de página
Coleta de registros
Se precisar das informações acima, você pode recuperá-las por meio do agente oficial do CloudWatch ou pode criar uma métrica personalizada e enviar os dados por conta própria por meio de um script personalizado.
O principal objetivo do CloudWatch:
Colete métricas
Coletar registros
Coletar eventos
Criar alarmes
Crie painéis
Registros do CloudWatch:
Você pode usar o Amazon CloudWatch Logs para monitorar, armazenar e acessar arquivos de log de instâncias do Amazon EC2, AWS CloudTrail, Amazon Route 53 e outras fontes. Você pode então recuperar os dados de log associados do CloudWatch Logs.
Ele ajuda a centralizar os logs de todos os sistemas, aplicativos e serviços da AWS que você usa, em um único serviço altamente escalonável.
Você pode criar grupos de logs para unir unidades lógicas do CloudWatch Logs.
Você pode transmitir arquivos de log personalizados para obter mais informações.
Eventos CloudWatch:
O Amazon CloudWatch Events oferece um fluxo quase em tempo real de eventos do sistema que descrevem alterações nos recursos da AWS.
Você pode usar eventos para acionar lambdas, por exemplo, enquanto usa alarmes para informar que algo deu errado.
Alarmes CloudWatch:
Os alarmes do CloudWatch enviam notificações ou fazem alterações automaticamente nos recursos que você está monitorando com base nas regras definidas por você.
Por exemplo, você pode criar alarmes personalizados do CloudWatch que acionarão notificações como a ultrapassagem de um limite de faturamento definido.
Os alarmes do CloudWatch têm dois estados de okoualarm
Métricas do CloudWatch:
As métricas do CloudWatch representam um conjunto de pontos de dados ordenados por tempo.
Basicamente, são variáveis ​​que você pode monitorar ao longo do tempo para ajudar a saber se está tudo bem, por exemplo, utilização horária da CPU.
O CloudWatch Metrics permite rastrear métricas de alta resolução em intervalos de menos de um minuto até por segundo.
Painéis CloudWatch:
Os painéis do CloudWatch são páginas iniciais personalizáveis ​​no console do CloudWatch que você pode usar para monitorar seus recursos em uma única visualização
Esses painéis se integram ao CloudWatch Metrics e ao CloudWatch Alarms para criar visualizações personalizadas de métricas e alarmes para seus recursos da AWS.
CloudTrail
CloudTrail simplificado:
AWS CloudTrail é um serviço que permite governança, conformidade, auditoria operacional e auditoria de risco de sua conta AWS. Com ele, você pode registrar, monitorar continuamente e reter atividades de conta relacionadas a ações em sua infraestrutura AWS. O CloudTrail fornece histórico de eventos da atividade da sua conta da AWS, incluindo ações realizadas por meio do AWS Management Console, AWS SDKs, ferramentas de linha de comando, chamadas de API e outros serviços da AWS. É um serviço regional, mas você pode configurar o CloudTrail para coletar trilhas em todas as regiões.

Detalhes principais do CloudTrail:
O CloudTrail Events registra chamadas ou atividades de API.
O CloudTrail Events armazena os últimos 90 dias de eventos em seu histórico de eventos. Isso está habilitado por padrão e não tem custo adicional.
Esse histórico de eventos simplifica a análise de segurança, o rastreamento de alterações de recursos e a solução de problemas.
Existem dois tipos de eventos que podem ser registrados no CloudTrail: eventos de gerenciamento e eventos de dados.
Os eventos de gerenciamento fornecem informações sobre operações de gerenciamento executadas em recursos da sua conta da AWS.
Pense nos eventos de gerenciamento como coisas normalmente feitas por pessoas quando estão na AWS. Exemplos:
um login de usuário
uma política mudou
uma configuração de segurança recém-criada
uma exclusão de regra de registro
Os eventos de dados fornecem informações sobre as operações de recursos executadas em um recurso.
Pense nos eventos de dados como coisas normalmente feitas pelo software ao atingir vários endpoints da AWS. Exemplos:
Atividade da API em nível de objeto S3
Atividade de execução de função Lambda
Por padrão, o CloudTrail registra eventos de gerenciamento, mas não eventos de dados.
Por padrão, os arquivos de log do CloudTrail Events são criptografados usando criptografia no lado do servidor (SSE) do Amazon S3. Você também pode optar por criptografar seus arquivos de log com uma chave do AWS Key Management Service (AWS KMS). Como esses logs são armazenados no S3, você pode definir regras de ciclo de vida do Amazon S3 para arquivar ou excluir arquivos de log automaticamente. Se desejar notificações sobre entrega e validação de arquivos de log, você poderá configurar notificações do Amazon SNS.
Sistema de arquivos elástico (EFS)
EFS simplificado:
O EFS fornece um sistema de arquivos NFS elástico simples e totalmente gerenciado para uso na AWS. O EFS aumenta ou diminui a capacidade de armazenamento do sistema de arquivos de forma automática e instantânea à medida que você adiciona ou remove arquivos, sem interromper seu aplicativo.

Detalhes da chave EFS:
No EFS, a capacidade de armazenamento é elástica (aumenta e diminui automaticamente) e seu tamanho muda com base na adição ou remoção de arquivos.
Embora o EBS monte um volume EBS em uma instância, você pode anexar um volume EFS em várias instâncias do EC2.
As instâncias EC2 se comunicam com o sistema de arquivos remoto usando o protocolo NFSv4. Isso torna necessário abrir a porta NFS para nosso grupo de segurança (regras de firewall EC2) para permitir o tráfego de entrada nessa porta.
Dentro de um volume EFS, o estado do ponto de acesso NFS informará quais instâncias estão disponíveis para montagem
Com o EFS, você paga apenas pelo armazenamento que usa, portanto, paga conforme o uso. Não é necessário pré-provisionamento.
O EFS pode escalar até petabytes e suportar milhares de conexões NFS simultâneas.
Os dados são armazenados em várias AZs em uma região e o EFS garante consistência de leitura após gravação.
É melhor para armazenamento de arquivos acessado por uma frota de servidores, em vez de apenas um servidor.
Amazon FSx para Windows
Amazon FSx para Windows simplificado:
O Amazon FSx for Windows File Server fornece um sistema de arquivos Microsoft nativo totalmente gerenciado.

Detalhes principais do Amazon FSx para Windows:
Com o FSx for Windows, você pode mover facilmente seus aplicativos baseados em Windows que exigem armazenamento de arquivos na AWS.
Ele é construído no Windows Server e existe apenas para aplicativos baseados em Microsoft, portanto, se você precisar de armazenamento de arquivos baseado em SMB, escolha FSx.
O FSx para Windows também permite a conectividade entre servidores locais e a AWS, para que esses mesmos servidores locais também possam usar o Amazon FSx.
Você pode usar o Microsoft Active Directory para autenticar no sistema de arquivos.
O Amazon FSx for Windows oferece vários níveis de segurança e conformidade para ajudar a garantir que seus dados estejam protegidos. O Amazon FSx criptografa automaticamente seus dados em repouso e em trânsito.
Você pode acessar o Amazon FSx for Windows a partir de vários recursos de computação, não apenas do EC2.
Você pode implantar o Amazon FSx for Windows em uma única AZ ou em uma configuração Multi-AZ.
Você pode usar SSD ou HDD como dispositivo de armazenamento, dependendo de suas necessidades.
FSx para Windows oferece suporte a backups automatizados diários e administradores também fazem backups quando necessário.
FSx para Windows remove conteúdo duplicado e compacta conteúdo comum
Por padrão, todos os dados são criptografados em repouso.
Amazon FSx para Lustre
Amazon FSx para Lustre simplificado:
O Amazon FSx for Lustre torna fácil e econômico iniciar e executar o sistema de arquivos Lustre de código aberto para aplicações de computação de alto desempenho. Com o FSx for Lustre, você pode iniciar e executar um sistema de arquivos capaz de processar grandes conjuntos de dados com até centenas de gigabytes por segundo de taxa de transferência, milhões de IOPS e latências inferiores a milissegundos.

Detalhes da chave do Amazon FSx for Lustre:
O FSx for Lustre é compatível com as AMIs baseadas em Linux mais populares, incluindo Amazon Linux, Amazon Linux 2, Red Hat Enterprise Linux (RHEL), CentOS, SUSE Linux e Ubuntu.
Como o sistema de arquivos Lustre foi projetado para cargas de trabalho de computação de alto desempenho que normalmente são executadas em clusters de computação, escolha EFS para sistema de arquivos Linux normal se seus requisitos não corresponderem a este caso de uso.
O FSx Lustre tem a capacidade de armazenar e recuperar dados diretamente no S3 por conta própria.
Serviço de banco de dados relacional (RDS)
RDS simplificado:
RDS é um serviço gerenciado que facilita a configuração, operação e dimensionamento de um banco de dados relacional na AWS. Ele fornece capacidade econômica e redimensionável, ao mesmo tempo que automatiza ou terceiriza tarefas administrativas demoradas, como provisionamento de hardware, configuração de banco de dados, aplicação de patches e backups.

Detalhes da chave RDS:
RDS vem em seis sabores diferentes:
servidor SQL
Oráculo
Servidor MySQL
PostgreSQL
Maria DB
aurora
Pense no RDS como o mecanismo de banco de dados no qual vários bancos de dados ficam sobrepostos.
O RDS tem dois recursos principais durante a expansão:
Leia a replicação para melhorar o desempenho
Multi-AZ para alta disponibilidade
No mundo dos bancos de dados, o Online Transaction Processing (OLTP) difere do Online Analytical Processing (OLAP) em termos do tipo de consulta que você faria. O OLTP fornece dados para a lógica de negócios que, em última análise, compõe o funcionamento central da sua plataforma ou aplicativo. OLAP visa obter insights sobre os dados que você armazenou para tomar melhores decisões estratégicas como empresa.
O RDS é executado em máquinas virtuais, mas você não tem acesso a essas máquinas. Você não pode usar SSH em uma instância RDS, portanto, não pode corrigir o sistema operacional. Isso significa que a AWS é responsável pela segurança e manutenção do RDS. Você pode provisionar uma instância do EC2 como banco de dados se precisar ou quiser gerenciar o servidor subjacente por conta própria, mas não com um mecanismo RDS.
Só porque você não pode acessar a VM diretamente, isso não significa que o RDS não tenha servidor. No entanto, existe o Aurora serverless (explicado abaixo), que atende a um propósito de nicho.
As filas SQS podem ser usadas para armazenar gravações pendentes no banco de dados se seu aplicativo estiver sofrendo com uma alta carga de gravação. Essas gravações poderão então ser adicionadas ao banco de dados quando o banco de dados estiver pronto para processá-las. Adicionar mais IOPS também ajudará, mas por si só não eliminará totalmente a chance de perda de gravações. Uma fila, entretanto, garante que as gravações no banco de dados não sejam perdidas.
RDS Multi-AZ:
A recuperação de desastres na AWS sempre busca garantir que cópias de reserva dos recursos sejam mantidas em uma área geográfica separada. Dessa forma, se um desastre (desastre natural, conflito político, etc.) ocorrer onde estão seus recursos originais, as cópias não serão afetadas.
Quando você provisiona uma instância de banco de dados Multi-AZ, o Amazon RDS cria automaticamente uma instância de banco de dados primária e replica de forma síncrona os dados para uma instância de espera em uma zona de disponibilidade (AZ) diferente. Cada AZ funciona em sua própria infraestrutura fisicamente distinta e independente e é projetada para ser altamente confiável.
Com uma configuração Multi-AZ, o EC2 se conecta ao seu armazenamento de dados RDS usando um endereço DNS mascarado como uma string de conexão. Se o banco de dados primário falhar, o Multi-AZ será inteligente o suficiente para detectar essa falha e atualizar automaticamente o endereço DNS para apontar para o secundário. Nenhuma intervenção manual é necessária e a AWS se encarrega de trocar o endereço IP no DNS.
Multi-AZ é compatível com todos os tipos de banco de dados, exceto aurora. Isso ocorre porque o Aurora é completamente tolerante a falhas por si só.
O recurso Multi-AZ permite alta disponibilidade em zonas de disponibilidade e não em regiões.
Durante um failover, o antigo primário recuperado torna-se o novo secundário e o secundário promovido torna-se primário. Depois que o banco de dados original for recuperado, um processo de sincronização será iniciado, onde os dois bancos de dados se espelharão uma vez para sincronizar os novos dados que o antigo primário com falha pode ter perdido.
Você pode forçar um failover para uma configuração Multi-AZ reiniciando a instância primária
Com uma configuração Multi-AZ RDS, os backups são feitos no modo de espera.
Réplicas de leitura RDS:
A replicação de leitura é usada exclusivamente para melhoria de desempenho.
Com uma configuração de réplica de leitura, o EC2 se conecta ao backend RDS usando um endereço DNS e cada gravação recebida pelo banco de dados mestre também é passada para um banco de dados secundário para que se torne uma cópia perfeita do mestre. Isso tem o efeito geral de reduzir o número de transações no mestre porque os bancos de dados secundários podem ser consultados em busca dos mesmos dados.
No entanto, se o banco de dados mestre falhar, não haverá failover automático. Você teria que criar manualmente uma nova cadeia de conexão para sincronizar com uma das réplicas de leitura para que ela se tornasse uma mestre por conta própria. Então você teria que atualizar suas instâncias do EC2 para apontar para a réplica de leitura. Você pode ter até cinco cópias do seu banco de dados mestre com replicação de leitura.
Você pode promover réplicas de leitura como seu próprio banco de dados de produção, se necessário.
As réplicas de leitura são suportadas para todos os seis tipos de banco de dados no RDS.
Cada réplica de leitura terá seu próprio endpoint DNS.
Os backups automatizados devem ser habilitados para usar réplicas de leitura.
Você pode ter réplicas de leitura com o Multi-AZ ativado ou ter a réplica de leitura em uma região totalmente separada. Você pode até ter réplicas de leitura de réplicas de leitura, mas tome cuidado com a latência ou o atraso de replicação. A ressalva para réplicas de leitura é que elas estão sujeitas a pequenos atrasos de replicação. Isso ocorre porque algumas das transações mais recentes podem estar faltando, pois não são atualizadas tão rapidamente quanto as primárias. Os designers de aplicativos precisam considerar quais consultas têm tolerância a dados ligeiramente desatualizados. Essas consultas devem ser executadas na réplica de leitura, enquanto aquelas que exigem dados totalmente atualizados devem ser executadas no nó primário.
Backups RDS:
Quando se trata de RDS, existem dois tipos de backups:
backups automatizados
instantâneos de banco de dados
Backups automatizadospermitem que você recupere seu banco de dados a qualquer momento dentro de um período de retenção (entre um e 35 dias). Os backups automatizados tirarão um instantâneo diário completo e também armazenarão logs de transações ao longo do dia. Quando você executa uma recuperação de banco de dados, o RDS primeiro escolhe o backup diário mais recente e aplica os logs de transações relevantes daquele dia. Dentro do período de retenção definido, isso lhe dá a capacidade de fazer uma recuperação pontual até o segundo exato. Os backups automatizados estão habilitados por padrão. Os dados de backup são armazenados livremente até o tamanho do seu banco de dados real (portanto, para cada GB salvo no RDS, a mesma quantidade será armazenada livremente no S3 até o limite de GB do banco de dados). Os backups são feitos dentro de uma janela definida, portanto a latência pode aumentar à medida que a E/S de armazenamento é suspensa para que seja feito backup dos dados.
Os instantâneos de banco de dados são feitos manualmente pelo administrador. Uma diferença importante dos backups automatizados é que eles são retidos mesmo depois que a instância original do RDS é encerrada. Com backups automatizados, os dados de backup no S3 são apagados junto com o mecanismo RDS. É por isso que você será questionado se deseja tirar um instantâneo final do seu banco de dados quando for excluí-lo.
Quando você restaura um banco de dados por meio de backups automatizados ou instantâneos de banco de dados, o resultado é o provisionamento de uma instância RDS totalmente nova com seu próprio endpoint de banco de dados para ser alcançada.
Segurança RDS:
Você pode autenticar sua instância de banco de dados usando a autenticação de banco de dados IAM. A autenticação de banco de dados IAM funciona com MySQL e PostgreSQL. Com esse método de autenticação, você não precisa usar uma senha ao se conectar a uma instância de banco de dados. Em vez disso, você usa um token de autenticação.
Um token de autenticação é uma string exclusiva que o Amazon RDS gera mediante solicitação. Os tokens de autenticação têm vida útil de 15 minutos. Você não precisa armazenar credenciais de usuário no banco de dados porque a autenticação é gerenciada externamente usando o IAM.
A autenticação do banco de dados IAM oferece os seguintes benefícios:
O tráfego de rede de e para o banco de dados é criptografado usando Secure Sockets Layer (SSL).
Você pode usar o IAM para gerenciar centralmente o acesso aos recursos do banco de dados, em vez de gerenciar o acesso individualmente em cada instância de banco de dados.
Para aplicações executadas no Amazon EC2, você pode usar credenciais de perfil específicas da sua instância do EC2 para acessar seu banco de dados em vez de uma senha, para maior segurança
A criptografia em repouso é compatível com todos os seis tipos de DB para RDS. A criptografia é feita usando o serviço AWS KMS. Depois que a instância do RDS tiver a criptografia habilitada, os dados no banco de dados serão criptografados, assim como todos os backups (automatizados ou instantâneos) e réplicas de leitura.
Depois que os dados são criptografados, o Amazon RDS trata da autenticação do acesso e da descriptografia dos dados de forma transparente, com impacto mínimo no desempenho. Você não precisa modificar seus aplicativos clientes de banco de dados para usar criptografia.
A criptografia do Amazon RDS está disponível atualmente para todos os mecanismos de banco de dados e tipos de armazenamento. No entanto, você precisa garantir que o tipo de instância subjacente ofereça suporte à criptografia de banco de dados.
Você só pode habilitar a criptografia para uma instância de banco de dados do Amazon RDS ao criá-la, e não depois que a instância de banco de dados for criada e as instâncias de banco de dados criptografadas não puderem ser modificadas para desabilitar a criptografia.
Monitoramento aprimorado RDS:
O RDS vem com um recurso de monitoramento aprimorado. O Amazon RDS fornece métricas em tempo real para o sistema operacional (SO) em que sua instância de banco de dados é executada. Você pode visualizar as métricas da sua instância de banco de dados usando o console ou consumir a saída JSON do Enhanced Monitoring do CloudWatch Logs em um sistema de monitoramento de sua escolha.
Por padrão, as métricas do Enhanced Monitoring são armazenadas no CloudWatch Logs por 30 dias. Para modificar a quantidade de tempo que as métricas são armazenadas no CloudWatch Logs, altere a retenção do grupo de logs RDS OS Metrics no console do CloudWatch.
Observe que existem diferenças importantes entre o CloudWatch e as métricas de monitoramento aprimorado. O CloudWatch reúne métricas sobre a utilização da CPU do hipervisor para uma instância de banco de dados, e o Enhanced Monitoring reúne suas métricas de um agente na instância. Como resultado, você poderá encontrar diferenças entre as medidas, porque a camada do hipervisor executa uma pequena quantidade de trabalho que pode ser captada e interpretada como parte da métrica.
aurora
Aurora simplificada:
Aurora é o principal banco de dados da AWS conhecido por combinar o desempenho e a disponibilidade de bancos de dados corporativos tradicionais com a simplicidade e a economia de bancos de dados de código aberto. É um RDBMS compatível com MySQL/PostgreSQL que fornece segurança, disponibilidade e confiabilidade de bancos de dados comerciais por 1/10 do custo dos concorrentes. É muito mais eficaz como banco de dados AWS devido aos multiplicadores de desempenho de 5x e 3x para MySQL e PostgreSQL, respectivamente.

Detalhes principais da Aurora:
Em caso de falha na infraestrutura, o Aurora executa um failover automático para uma réplica própria.
O Amazon Aurora normalmente envolve um cluster de instâncias de banco de dados em vez de uma única instância. Cada conexão é tratada por uma instância de banco de dados específica. Ao se conectar a um cluster do Aurora, o nome do host e a porta especificados apontam para um manipulador intermediário chamado endpoint. Aurora usa o mecanismo de endpoint para abstrair essas conexões. Assim, você não precisa codificar todos os nomes de host ou escrever sua própria lógica para balanceamento de carga e redirecionamento de conexões quando algumas instâncias de banco de dados não estiverem disponíveis.
Por padrão, há 2 cópias em no mínimo 3 zonas de disponibilidade para um total de 6 cópias de todos os seus dados do Aurora. Isso possibilita lidar com a perda potencial de até 2 cópias dos seus dados sem afetar a disponibilidade de gravação e até 3 cópias dos seus dados sem afetar a disponibilidade de leitura.
O armazenamento Aurora é autocorretivo e os blocos de dados e discos são continuamente verificados em busca de erros. Se algum for encontrado, esses erros serão reparados automaticamente.
A replicação do Aurora difere das réplicas RDS no sentido de que é possível que as réplicas do Aurora sejam tanto um modo de espera como parte de uma configuração multi-AZ quanto um destino para tráfego de leitura. No RDS, o modo de espera multi-AZ não pode ser configurado para ser um terminal de leitura e somente réplicas de leitura podem servir essa função.
Com a replicação do Aurora, você pode ter até quinze cópias. Se você deseja MySQL ou PostgreSQL downstream enquanto replica cópias, então você pode ter apenas 5 ou 1.
O failover automatizado só é possível com a replicação de leitura do Aurora
Para obter mais informações sobre as diferenças entre a replicação RDS e a replicação Aurora, consulte o seguinte:
Captura de tela 18/06/2020 às 15h02 39h

Os backups automatizados estão sempre habilitados nas instâncias do Aurora e os backups não afetam o desempenho do banco de dados. Você também pode tirar instantâneos que também não afetam o desempenho. Seus snapshots podem ser compartilhados entre contas da AWS.
Uma tática comum para migrar bancos de dados RDS para RDs Aurora é criar uma réplica de leitura de um banco de dados RDS MariaDB/MySQL como um banco de dados Aurora. Em seguida, basta promover o banco de dados Aurora em uma instância de produção e excluir o antigo banco de dados MariaDB/MySQL.
O Aurora começa com 10 GB e é dimensionado de 10 GB até 128 TB por meio de escalonamento automático de armazenamento. O poder de computação do Aurora chega a 32vCPUs e 244 GB de memória
Aurora sem servidor:
Aurora Serverless é uma configuração simples, sob demanda e de escalonamento automático para as edições do Aurora compatíveis com MySQL/PostgreSQl. Com o Aurora Serverless, sua instância aumenta ou diminui automaticamente e é ativada ou desativada com base no uso do aplicativo. Os casos de uso desse serviço são cargas de trabalho pouco frequentes, intermitentes e imprevisíveis.
Isso também torna possível mais barato porque você só paga por chamada
Com o Aurora Serverless, basta criar um endpoint de banco de dados, especificar opcionalmente o intervalo de capacidade de banco de dados desejado e conectar seus aplicativos.
Ele elimina a complexidade do gerenciamento de instâncias e capacidade de banco de dados. O banco de dados será iniciado, encerrado e dimensionado automaticamente para atender às necessidades do seu aplicativo. Ele dimensionará perfeitamente a capacidade de computação e memória conforme necessário, sem interrupção das conexões do cliente.
Endpoints do cluster Aurora:
Usando endpoints de cluster, você mapeia cada conexão para a instância ou grupo de instâncias apropriado com base no seu caso de uso.
Você pode se conectar a endpoints de cluster associados a diferentes funções ou trabalhos em seu banco de dados Aurora. Isso ocorre porque diferentes instâncias ou grupos de instâncias executam funções diferentes.
Por exemplo, para executar instruções DDL você pode conectar-se à instância primária. Para realizar consultas, você pode conectar-se ao endpoint do leitor, com o Aurora executando automaticamente o balanceamento de carga entre todas as réplicas do Aurora atrás do endpoint do leitor. Para diagnóstico ou ajuste, você pode conectar-se a um endpoint diferente para examinar detalhes.
Como a entrada para sua instância de banco de dados permanece a mesma após um failover, seu aplicativo pode retomar a operação do banco de dados sem a necessidade de intervenção administrativa manual para qualquer um dos seus endpoints.
Terminais do leitor Aurora:
Os endpoints do Aurora Reader são um subconjunto da ideia acima de endpoints de cluster. Use o endpoint do leitor para operações de leitura, como consultas. Ao processar essas instruções nas réplicas somente leitura do Aurora, esse endpoint reduz a sobrecarga na instância primária.
Existem até 15 réplicas de leitura do Aurora como um endpoint de leitor para ajudar a lidar com o tráfego de consulta somente leitura.
Também ajuda o cluster a dimensionar a capacidade de lidar com consultas SELECT simultâneas, proporcionalmente ao número de réplicas do Aurora no cluster. Cada cluster de banco de dados Aurora tem um endpoint de leitor.
Se o cluster contiver uma ou mais réplicas do Aurora, o endpoint do leitor fará o balanceamento de carga de cada solicitação de conexão entre as réplicas do Aurora. Nesse caso, você só poderá executar instruções somente leitura, como SELECT, nessa sessão. Se o cluster contiver apenas uma instância primária e nenhuma réplica do Aurora, o endpoint do leitor se conectará diretamente à instância primária. Nesse caso, você pode realizar operações de gravação por meio do endpoint.
DynamoDB
DynamoDB simplificado:
O Amazon DynamoDB é um banco de dados de valores-chave e documentos que oferece desempenho de milissegundos de um dígito em qualquer escala. É um banco de dados não SQL totalmente gerenciado, multirregional, multimestre e durável. Ele vem com segurança integrada, backup e restauração e cache na memória para aplicativos em escala de Internet.

Detalhes da chave do DynamoDB:
Os principais componentes do DynamoDB são:
uma coleção que serve como mesa fundacional
um documento que é equivalente a uma linha em um banco de dados SQL
pares de valores-chave que são os campos dentro do documento ou linha
A conveniência dos bancos de dados não relacionais é que cada linha pode parecer totalmente diferente com base no seu caso de uso. Não precisa haver uniformidade. Por exemplo, se você precisar de uma nova coluna para uma entrada específica, também não precisará garantir que essa coluna exista para as outras entradas.
O DynamoDB oferece suporte a modelos baseados em documentos e valores-chave. É uma ótima opção para dispositivos móveis, web, jogos, tecnologia de publicidade, IoT, etc.
O DynamoDB é armazenado via SSD e é por isso que é tão rápido.
Está espalhado por 3 data centers geograficamente distintos.
O modelo de consistência padrão é Leituras Eventualmente Consistentes, mas também há Leituras Fortemente Consistentes.
A diferença entre os dois modelos de consistência é a regra de um segundo. Com leituras consistentes eventuais, todas as cópias de dados geralmente são idênticas dentro de um segundo após uma operação de gravação. Uma leitura repetida após um curto período de tempo deverá retornar os dados atualizados. No entanto, se você precisar ler dados atualizados em menos de um segundo e isso precisar ser uma garantia, leituras fortemente consistentes serão sua melhor aposta.
Se você enfrentar um cenário que exige que o esquema ou a estrutura dos seus dados mude com frequência, será necessário escolher um banco de dados que forneça uma maneira não rígida e flexível de adicionar ou remover novos tipos de dados. Este é um exemplo clássico de escolha entre um banco de dados relacional e um banco de dados não relacional (NoSQL). Neste cenário, escolha DynamoDB.
Um sistema de banco de dados relacional não é bem dimensionado pelos seguintes motivos:
Ele normaliza os dados e os armazena em várias tabelas que exigem várias consultas para gravar no disco.
Geralmente incorre nos custos de desempenho de um sistema de transação compatível com ACID.
Ele usa junções caras para remontar as visualizações necessárias dos resultados da consulta.
A alta cardinalidade é boa para o desempenho de E/S do DynamoDB. Quanto mais distintos forem os valores da chave de partição, melhor. Faz com que as solicitações enviadas sejam espalhadas pelo espaço particionado.
O DynamoDB utiliza processamento paralelo para obter desempenho previsível. Você pode visualizar cada partição ou nó como um servidor de banco de dados independente de tamanho fixo, com cada partição ou nó responsável por um bloco definido de dados. Na terminologia SQL, esse conceito é conhecido como fragmentação, mas é claro que o DynamoDB não é um banco de dados baseado em SQL. Com o DynamoDB, os dados são armazenados em unidades de estado sólido (SSD).
Acelerador DynamoDB (DAX):
O Amazon DynamoDB Accelerator (DAX) é um cache na memória totalmente gerenciado e altamente disponível que pode reduzir os tempos de resposta do Amazon DynamoDB de milissegundos para microssegundos, mesmo com milhões de solicitações por segundo.
Com o DAX, seus aplicativos permanecem rápidos e responsivos, mesmo quando volumes de solicitações sem precedentes surgem em seu caminho. Não há necessidade de ajuste.
O DAX permite expandir sob demanda para um cluster de dez nós, proporcionando milhões de solicitações por segundo.
O DAX faz mais do que apenas aumentar o desempenho de leitura ao gravar no cache. Isso também melhora o desempenho de gravação.
Assim como o DynamoDB, o DAX é totalmente gerenciado. Você não precisa mais se preocupar com tarefas de gerenciamento, como provisionamento de hardware ou software, instalação e configuração, aplicação de patches de software, operação de um cluster de cache distribuído confiável ou replicação de dados em várias instâncias à medida que você escala.
Isso significa que não há necessidade de os desenvolvedores gerenciarem a lógica de cache. O DAX é totalmente compatível com chamadas de API existentes do DynamoDB.
O DAX permite provisionar um cluster DAX para várias tabelas do DynamoDB, vários clusters DAX para uma única tabela do DynamoDB ou algo intermediário, proporcionando flexibilidade máxima.
O DAX foi projetado para HA, portanto, no caso de falha de uma AZ, ele fará failover para uma de suas réplicas em outra AZ. Isso também é gerenciado automaticamente.
Fluxos do DynamoDB:
Um stream do DynamoDB é um fluxo ordenado de informações sobre alterações em itens em uma tabela do Amazon DynamoDB. Quando você habilita um stream em uma tabela, o DynamoDB captura informações sobre cada modificação nos itens de dados da tabela.
O Amazon DynamoDB é integrado ao AWS Lambda para que você possa criar gatilhos – trechos de código que respondem automaticamente a eventos no DynamoDB Streams.
Imediatamente após a modificação de um item na tabela, um novo registro aparece no fluxo da tabela. O AWS Lambda pesquisa o stream e invoca sua função Lambda de forma síncrona ao detectar novos registros de stream. A função Lambda pode executar qualquer ação especificada, como enviar uma notificação ou iniciar um fluxo de trabalho.
Com gatilhos, você pode criar aplicativos que reagem a modificações de dados em tabelas do DynamoDB.
Sempre que um aplicativo cria, atualiza ou exclui itens da tabela, o DynamoDB Streams grava um registro de stream com os atributos de chave primária dos itens que foram modificados. Um registro de fluxo contém informações sobre uma modificação de dados em um único item em uma tabela do DynamoDB. Você pode configurar o fluxo para que os registros do fluxo capturem informações adicionais, como as imagens "antes" e "depois" dos itens modificados.
Tabelas globais do DynamoDB
Global Tables é uma solução de replicação multirregional e multimestre para desempenho local rápido de aplicativos distribuídos globalmente.
O Global Tables replica suas tabelas do Amazon DynamoDB automaticamente nas regiões da AWS de sua escolha.
Ele é baseado em fluxos do DynamoDB e é redundante em várias regiões para recuperação de dados ou para fins de alta disponibilidade. O failover de aplicativos é tão simples quanto redirecionar as chamadas do DynamoDB do seu aplicativo para outra região da AWS.
O Global Tables elimina o difícil trabalho de replicação de dados entre regiões e resolução de conflitos de atualização, permitindo que você se concentre na lógica de negócios do seu aplicativo. Você não precisa reescrever seus aplicativos para usar tabelas globais.
A latência de replicação com Tabelas Globais normalmente é inferior a um segundo.
Desvio para o vermelho
Redshift simplificado:
O Amazon Redshift é um serviço de data warehouse totalmente gerenciado em escala de petabytes na nuvem. O serviço Amazon Redshift gerencia todo o trabalho de configuração, operação e escalabilidade de um data warehouse. Essas tarefas incluem provisionamento de capacidade, monitoramento e backup do cluster e aplicação de patches e atualizações ao mecanismo Amazon Redshift.

Detalhes principais do Redshift:
Um cluster do Amazon Redshift é um conjunto de nós que consiste em um nó líder e um ou mais nós de computação. O tipo e o número de nós de cálculo necessários dependem do tamanho dos seus dados, do número de consultas que você executará e do desempenho de execução de consultas necessário.
O Redshift é usado para business intelligence e extrai conjuntos de dados muito grandes e complexos para realizar consultas complexas a fim de coletar insights dos dados.
Ele se ajusta ao caso de uso de Processamento Analítico Online (OLAP). Redshift é uma tecnologia poderosa para descoberta de dados, incluindo recursos para visualização quase ilimitada de relatórios, cálculos analíticos complexos e planejamento preditivo de cenários “e se” (orçamento, previsão, etc.).
Dependendo de suas necessidades de armazenamento de dados, você pode começar com um cluster pequeno de nó único e expandir facilmente para um cluster maior de vários nós conforme seus requisitos mudam. Você pode adicionar ou remover nós de computação do cluster sem qualquer interrupção do serviço.
Se você pretende manter seu cluster em execução por um ano ou mais, poderá economizar dinheiro reservando nós de computação por um período de um ou três anos.
Instantâneos são backups pontuais de um cluster. Esses backups são habilitados por padrão com um período de retenção de 1 dia. O período máximo de retenção é de 35 dias.
O Redshift também pode replicar seus snapshots de forma assíncrona para uma região diferente, se desejar.
Um cluster Redshift altamente disponível exigiria 3 cópias dos seus dados. Uma cópia estaria ativa no Redshift e as outras ficariam em espera no S3.
O Redshift pode ter até 128 nós de computação em um cluster de vários nós. O nó líder sempre gerencia as conexões do cliente e retransmite as consultas aos nós de computação que armazenam os dados reais e executam as consultas.
O Redshift é capaz de alcançar eficiência, apesar das muitas partes em sua arquitetura, por meio do uso de compactação colunar de armazenamentos de dados que contêm dados semelhantes. Além disso, o Redshift não requer índices ou visualizações materializadas, o que significa que pode ser relativamente menor em tamanho comparado a um banco de dados OLTP contendo a mesma quantidade de informações. Finalmente, ao carregar dados em uma tabela Redshift, o Redshift irá automaticamente fazer uma amostragem dos dados e escolher o esquema de compactação mais apropriado.
O Redshift também vem com Massive Parallel Processing (MPP) para aproveitar todos os nós do seu cluster de vários nós. Isso é feito distribuindo uniformemente os dados e a carga de consultas em todos os nós. Por causa disso, a expansão ainda mantém um ótimo desempenho.
O Redshift é criptografado em trânsito usando SSL e criptografado em repouso usando AES-256. Por padrão, o Redshift gerenciará todas as chaves, mas você também pode fazer isso por meio do AWS CloudHSM ou AWS KMS.
O Redshift é cobrado por:
Horas do nó de computação (total de horas que seus nós não líderes gastaram consultando dados)
Cópias de segurança
Transferência de dados dentro de uma VPC (mas não fora dela)
Redshift não é multi-AZ, se você quiser multi-AZ, precisará criar um cluster separado ingerindo a mesma entrada. Você também pode restaurar manualmente os snapshots para uma nova AZ em caso de interrupção.
Quando você provisiona um cluster do Amazon Redshift, ele é bloqueado por padrão para que ninguém tenha acesso a ele. Para conceder acesso de entrada a outros usuários a um cluster do Amazon Redshift, associe o cluster a um grupo de segurança.
O Amazon Redshift oferece armazenamento gratuito para snapshots igual à capacidade de armazenamento do cluster até que você exclua o cluster. Depois de atingir o limite de armazenamento gratuito de snapshots, você será cobrado por qualquer armazenamento adicional à taxa normal. Por isso, você deve avaliar quantos dias precisa para manter os snapshots automatizados e configurar seu período de retenção adequadamente, e excluir quaisquer snapshots manuais que não sejam mais necessários.
Independentemente de você ativar ou não os snapshots automatizados, você poderá tirar um snapshot manual sempre que desejar. O Amazon Redshift nunca excluirá automaticamente um snapshot manual. Os snapshots manuais são retidos mesmo depois de você excluir o cluster do Redshift. Como os snapshots manuais acumulam cobranças de armazenamento, é importante excluí-los manualmente se não precisar mais deles
Espectro de desvio para o vermelho:
O Amazon Redshift Spectrum é usado para executar consultas em exabytes de dados não estruturados no Amazon S3, sem necessidade de carregamento ou ETL.
As consultas do Redshift Spectrum empregam paralelismo massivo para serem executadas muito rapidamente em grandes conjuntos de dados. Grande parte do processamento ocorre na camada Redshift Spectrum, e a maior parte dos dados permanece no Amazon S3.
As consultas do Redshift Spectrum usam muito menos capacidade de processamento do seu cluster do que outras consultas.
O cluster e os arquivos de dados no Amazon S3 devem estar na mesma região da AWS.
As tabelas externas do S3 são somente leitura. Você não pode executar operações de inserção, atualização ou exclusão em tabelas externas.
Roteamento VPC aprimorado do Redshift:
Ao usar o Amazon Redshift Enhanced VPC Routing, o Redshift força todo o tráfego (como tráfego COPY e UNLOAD) entre o cluster e os repositórios de dados por meio da Amazon VPC.
Se o roteamento de VPC aprimorado não estiver habilitado, o Amazon Redshift roteará o tráfego pela Internet, incluindo o tráfego para outros serviços na rede da AWS.
Ao usar o roteamento de VPC aprimorado, você pode usar recursos padrão de VPC, como grupos de segurança de VPC, listas de controle de acesso de rede (ACLs), endpoints de VPC, políticas de endpoint de VPC, gateways de Internet e servidores de sistema de nomes de domínio (DNS).
ElastiCache
ElastiCache simplificado:
O serviço ElastiCache facilita a implantação, a operação e o dimensionamento de um cache na memória na nuvem. Ele ajuda você a aumentar o desempenho de seus bancos de dados existentes, recuperando dados de armazenamentos de dados na memória de alto rendimento e baixa latência.

Detalhes principais do ElastiCache:
O serviço é ótimo para melhorar o desempenho de aplicações web, permitindo que você receba informações localmente, em vez de depender apenas de bancos de dados relativamente distantes.

O Amazon ElastiCache oferece Redis e Memcached totalmente gerenciados para as aplicações mais exigentes que exigem tempos de resposta inferiores a um milissegundo.

Para dados que não mudam com frequência e são frequentemente solicitados, faz muito sentido armazenar esses dados em cache, em vez de consultá-los no banco de dados.

Configurações comuns que melhoram o desempenho do banco de dados incluem a introdução de réplicas de leitura de um banco de dados primário e a inserção de uma camada de cache na arquitetura de armazenamento.

Memcached é para fins de cache simples com escalabilidade horizontal e desempenho multithread, mas se você precisar de mais complexidade para seu ambiente de cache, escolha Redis.

Uma comparação adicional entre MemcacheD e Redis para ElastiCache:Captura de tela 18/06/2020 às 8h18h34

Outra vantagem de usar o ElastiCache é que, ao armazenar em cache os resultados da consulta, você paga o preço da consulta ao banco de dados apenas uma vez, sem precisar executar novamente a consulta, a menos que os dados sejam alterados.

O Amazon ElastiCache pode ser ampliado, expandido e ampliado para atender às demandas flutuantes dos aplicativos. O escalonamento de gravação e memória é compatível com fragmentação. As réplicas fornecem escalonamento de leitura.

Rota53
Rota53 simplificada:
O Amazon Route 53 é um serviço de sistema de nomes de domínio (DNS) altamente disponível e escalável. Você pode usar o Route 53 para executar três funções principais em qualquer combinação: registro de domínio, roteamento DNS e verificação de integridade.

Detalhes principais do Route53:
O DNS é usado para mapear nomes de domínio legíveis por humanos em um endereço de protocolo da Internet, de forma semelhante à forma como as listas telefônicas mapeiam nomes de empresas com números de telefone.
A AWS tem seu próprio registrador de domínio.
Quando você compra um nome de domínio, cada endereço DNS começa com um registro SOA (Início de Autoridade). O registro SOA armazena informações sobre o nome do servidor que iniciou a transferência de propriedade, o administrador que agora usará o domínio, os metadados atuais disponíveis e o número padrão de segundos ou TTL.
Os registros NS, ou registros de servidor de nomes, são usados ​​pelos hosts de domínio de nível superior (.org, .com, .uk, etc.) para direcionar o tráfego para os servidores de conteúdo. Os servidores DNS de conteúdo contêm os registros DNS oficiais.
Os navegadores conversam com os domínios de nível superior sempre que são consultados e encontram nomes de domínio que não reconhecem.
Os navegadores solicitarão os registros DNS autorizados associados ao domínio.
Como o domínio de nível superior contém registros NS, o TLD pode, por sua vez, consultar os servidores de nomes em busca de seu próprio SOA.
Dentro do SOA estarão as informações solicitadas.
Depois que essas informações forem coletadas, elas serão devolvidas ao navegador original que as solicitou.
Em resumo: Navegador -> TLD -> NS -> SOA -> registro DNS. O pipeline é revertido quando o registro DNS correto é encontrado.
Servidores de nomes autorizados armazenam informações de registro DNS, geralmente um provedor de hospedagem DNS ou registrador de domínio como GoDaddy, que oferece registro e hospedagem DNS.
Existem vários registros DNS para Route53. Aqui estão alguns dos mais comuns:
Registros A : são o tipo fundamental de registro DNS. O “A” nos registros A significa “endereço”. Esses registros são usados ​​por um computador para emparelhar diretamente um nome de domínio com um endereço IP. IPv4 e IPv6 são suportados com "AAAA" referente à versão IPv6. A: URL -> IPv4 e AAAA: URL -> IPv6 .
Registros CName : também chamados de Nome Canônico. Esses registros são usados ​​para resolver um nome de domínio para outro nome de domínio. Por exemplo, o domínio da versão móvel de um site pode ser um CName do domínio da versão do navegador desse mesmo site, em vez de um endereço IP separado. Isso permitiria que os usuários móveis que visitassem o site recebessem a versão móvel. CNAME: URL -> URL .
Registros de alias : esses registros são usados ​​para mapear seus domínios para recursos da AWS, como balanceadores de carga, endpoints CDN e buckets S3. Os registros de alias funcionam de maneira semelhante aos CNames, no sentido de que você mapeia um domínio para outro. A principal diferença é que, ao apontar seu registro Alias ​​para um serviço em vez de um nome de domínio, você tem a capacidade de alterar livremente seus nomes de domínio, se necessário, e não precisa se preocupar com quais registros podem ser mapeados para ele. Os registros de alias oferecem funcionalidade dinâmica. Alias: URL -> Recurso AWS .
Registros PTR : Esses registros são o oposto de um registro A. Os registros PTR mapeiam um IP para um domínio e são usados ​​em pesquisas reversas de DNS como forma de obter o nome de domínio de um endereço IP. PTR: IPv4 -> URL .
Uma outra grande diferença entre os registros CNames e Alias ​​é que um CName não pode ser usado para o nome de domínio simples (o registro ápice em toda a sua configuração DNS/o registro primário a ser usado). CNames devem sempre ser registros secundários que podem ser mapeados para outro registro secundário ou para o registro apex. O primário deve ser sempre do tipo Alias ​​ou A Record para funcionar.
Devido à natureza dinâmica dos registros Alias, eles são frequentemente recomendados para a maioria dos casos de uso e devem ser usados ​​sempre que possível.
TTL é o comprimento que um registro DNS é armazenado em cache nos servidores de resolução ou no próprio cache dos usuários, para que um mapeamento mais recente do IP para o domínio possa ser recuperado. O Time To Live é medido em segundos e quanto menor o TTL, mais rápidas as alterações de DNS se propagam pela Internet. A maioria dos provedores, por exemplo, possui um TTL que dura 48 horas.
Você pode criar verificações de integridade para enviar uma notificação simples se surgir algum problema com a configuração do DNS.
Além disso, as verificações de integridade do Route53 podem ser usadas para qualquer endpoint da AWS que possa ser acessado pela Internet. Isso o torna uma opção ideal para monitorar a integridade de seus endpoints AWS.
Políticas de roteamento Route53:
Ao criar um registro, você escolhe uma política de roteamento, que determina como o Amazon Route 53 responde às consultas DNS. As políticas de roteamento disponíveis são:
Roteamento Simples
Roteamento Ponderado
Roteamento baseado em latência
Roteamento de failover
Roteamento de geolocalização
Roteamento de proximidade geográfica
Roteamento de resposta multivalor
O Roteamento Simples é usado quando você precisa apenas de um único registro em seu DNS com um ou mais endereços IP atrás do registro, caso queira equilibrar a carga. Se você especificar vários valores em uma política de roteamento simples, o Route53 retornará um IP aleatório entre as opções disponíveis.
O roteamento ponderado é usado quando você deseja dividir seu tráfego com base nos pesos atribuídos. Por exemplo, se você deseja que 80% do seu tráfego vá para uma AZ e o restante para outra, use o Roteamento Ponderado. Esta política é muito útil para testar alterações de recursos e, devido às características de divisão de tráfego, pode funcionar como um meio de realizar implantações azul-verde. Ao criar o Roteamento Ponderado, você precisa especificar um novo registro para cada endereço IP. Você não pode agrupar os vários IPs em um registro como no Simple Routing.
O Roteamento Baseado em Latência , como o nome indica, baseia-se na configuração do roteamento com base no que seria a menor latência para um determinado usuário. Para usar o roteamento baseado em latência, você deve criar um registro de recurso de latência definido na mesma região que o recurso EC2 ou ELB correspondente que recebe o tráfego. Quando o Route53 recebe uma consulta para o seu site, ele seleciona o conjunto de registros que fornece ao usuário a velocidade mais rápida. Ao criar o roteamento baseado em latência, você precisa especificar um novo registro para cada IP.
O roteamento de failover é usado quando você deseja configurar um failover ativo-passivo. O Route53 monitorará a integridade do seu primário para que ele possa fazer failover quando necessário. Você também pode configurar manualmente verificações de integridade para monitorar todos os endpoints se desejar regras mais detalhadas.
O roteamento de geolocalização permite escolher para onde o tráfego será enviado com base na localização geográfica de seus usuários.
O roteamento de proximidade geográfica permite que você escolha para onde o tráfego será enviado com base na localização geográfica de seus usuários e seus recursos. Você pode optar por rotear mais ou menos tráfego com base em um peso especificado, conhecido como tendência. Esta tendência expande ou diminui a disponibilidade de uma região geográfica, o que facilita a transferência do tráfego de recursos de um local para recursos de outro. Para usar esse método de roteamento, você deve ativar o fluxo de tráfego Route53. Se você deseja controlar o tráfego global, use o roteamento de proximidade geográfica. Se você deseja que o tráfego permaneça em uma região local, use o roteamento por geolocalização.
O Roteamento Multivalor é praticamente igual ao Roteamento Simples, mas o Roteamento Multivalor permite que você faça verificações de integridade em cada conjunto de registros. Isso garante que apenas um IP íntegro será retornado aleatoriamente, em vez de qualquer IP.
Balanceadores de carga elásticos (ELB)
ELB simplificado:
O Elastic Load Balancing distribui automaticamente o tráfego de entrada de aplicativos entre vários destinos, como instâncias do Amazon EC2, contêineres Docker, endereços IP e funções Lambda. Ele pode lidar com a carga variável do tráfego do seu aplicativo em uma única zona de disponibilidade ou em várias zonas de disponibilidade. O Elastic Load Balancing oferece três tipos de balanceadores de carga, todos com alta disponibilidade, escalabilidade automática e segurança robusta necessária para tornar seus aplicativos tolerantes a falhas.

Detalhes principais do ELB:
Os balanceadores de carga podem ser voltados para a Internet ou internos do aplicativo.
Para rotear o tráfego de domínio para um balanceador de carga ELB, use o Amazon Route 53 para criar um registro Alias ​​que aponte para seu balanceador de carga. Um registro Alias ​​é preferível a um CName, mas ambos podem funcionar.
ELBs não possuem endereços IPv4 predefinidos; você deve resolvê-los com DNS. Seu balanceador de carga nunca terá seu próprio IP por padrão, mas você pode criar um IP estático para um balanceador de carga de rede porque os LBs de rede são para fins de alto desempenho.
As instâncias por trás do ELB são relatadas como InServiceou OutOfService. Quando uma instância EC2 atrás de um ELB falha em uma verificação de integridade, o ELB para de enviar tráfego para essa instância.
Uma configuração de pilha dupla para um balanceador de carga significa balanceamento de carga em IPv4 e IPv6
Na AWS, existem três tipos de LBs:
LBs de aplicativos
LBs de rede
LB clássicos.
Os LBs de aplicativos são mais adequados para tráfego HTTP(S) e equilibram a carga na camada 7 OSI. Eles são inteligentes o suficiente para reconhecer aplicativos e os Application Load Balancers também suportam roteamento baseado em caminho, roteamento baseado em host e suporte para aplicativos em contêineres. Por exemplo, se você alterar o idioma do seu navegador para francês, um Application LB terá visibilidade dos metadados que recebe do seu navegador, que contêm detalhes sobre o idioma que você usa. Para otimizar sua experiência de navegação, ele irá encaminhá-lo para os servidores de língua francesa no backend atrás do LB. Você também pode criar roteamento avançado de solicitações, movendo o tráfego para servidores específicos com base em regras definidas por você para casos específicos.
Os LBs de rede são mais adequados para tráfego TCP onde o desempenho é necessário e equilibram a carga na camada 4. Eles são capazes de gerenciar milhões de solicitações por segundo, mantendo uma latência extremamente baixa.
LBs clássicos são o produto ELB legado e se equilibram em HTTP(S) ou TCP, mas não em ambos. Mesmo sendo os LBs mais antigos, eles ainda suportam recursos como sessões fixas e cabeçalhos X-Forwarded-For.
Se você precisar de gerenciamento flexível de aplicativos e encerramento de TLS, deverá usar o Application Load Balancer. Se o desempenho extremo e um IP estático forem necessários para seu aplicativo, você deverá usar o Network Load Balancer. Se o seu aplicativo for criado na rede EC2 Classic, você deverá usar o Classic Load Balancer.
O ciclo de vida de uma solicitação para visualizar um site atrás de um ELB:
O navegador solicita o endereço IP do balanceador de carga do DNS.
DNS fornece o IP.
Com o IP em mãos, seu navegador faz uma solicitação HTTP para uma página HTML do Load Balancer.
Os dispositivos de perímetro da AWS verificam sua solicitação antes de passá-la para o LB.
O LB encontra um servidor web ativo para transmitir a solicitação HTTP.
O servidor web retorna o arquivo HTML solicitado.
O navegador recebe o arquivo HTML solicitado e renderiza a representação gráfica dele na tela.
Os balanceadores de carga são um serviço regional. Eles não equilibram a carga entre diferentes regiões. Você deve provisionar um novo ELB em cada região em que você opera.
Se seu aplicativo parar de responder, você receberá um erro 504 ao acessar seu balanceador de carga. Isso significa que o aplicativo está com problemas e o erro pode ter chegado ao balanceador de carga a partir dos serviços por trás dele. Isso não significa necessariamente que haja um problema com o próprio LB.
Recursos avançados do ELB:
Para ativar a resolução DNS IPv6, é necessário criar um segundo registro de recurso DNS para que o registro ALIAS AAAA seja resolvido para o balanceador de carga junto com o registro IPv4.
O cabeçalho X-Forwarded-For, por meio do protocolo Proxy, é simplesmente a ideia para os balanceadores de carga encaminharem o endereço IP do solicitante junto com a solicitação real de informações dos servidores por trás dos LBs. Normalmente, os servidores atrás dos LBs apenas veem que o IP que envia o tráfego pertence ao Load Balancer. Eles geralmente não têm ideia da verdadeira origem da solicitação, pois só sabem sobre o computador (o LB) que lhes pede para fazer alguma coisa. Mas às vezes podemos querer rotear o IP original para os servidores back-end para casos de uso específicos e ignorar o endereço IP do LB. O cabeçalho X-Forwarded-For torna isso possível.
Sticky Sessions vinculam um determinado usuário a uma instância específica durante sua permanência no aplicativo ou site. Isso significa que todas as suas interações com o aplicativo serão direcionadas sempre para o mesmo host. Se você precisar de disco local para que seu aplicativo funcione, sessões fixas são ótimas, pois os usuários têm acesso consistente garantido ao mesmo armazenamento efêmero em uma instância específica. A desvantagem das sessões fixas é que, se feitas de maneira inadequada, podem anular o propósito do balanceamento de carga. Todo o tráfego poderia, hipoteticamente, ser vinculado à mesma instância, em vez de ser distribuído uniformemente.
Os padrões de caminho criam um ouvinte com regras para encaminhar solicitações com base no caminho da URL definido nessas solicitações do usuário. Este método, conhecido como roteamento baseado em caminho, garante que o tráfego possa ser direcionado especificamente para vários serviços de back-end. Por exemplo, com Path Patterns você pode encaminhar solicitações gerais para um grupo de destino e solicitações para renderizar imagens para outro grupo de destino. Portanto, o URL “ www.example.com/” será encaminhado para um servidor que é usado para conteúdo geral, enquanto “ www.example.com/photos” será encaminhado para outro servidor que renderiza imagens.
Balanceamento de carga entre zonas ELB:
O balanceamento de carga entre zonas garante uma distribuição uniforme entre AZs, em vez de apenas dentro de uma única AZ.
Se o balanceamento de carga entre zonas estiver desabilitado, cada nó do balanceador de carga distribuirá solicitações uniformemente entre as instâncias registradas apenas em sua zona de disponibilidade.
O balanceamento de carga entre zonas reduz a necessidade de manter números equivalentes de instâncias em cada zona de disponibilidade habilitada e melhora a capacidade do seu aplicativo de lidar com a perda de uma ou mais instâncias.
No entanto, ainda é recomendável manter números aproximadamente equivalentes de instâncias em cada zona de disponibilidade habilitada para maior tolerância a falhas.
Para ambientes onde os clientes armazenam pesquisas de DNS em cache, as solicitações recebidas podem favorecer uma das zonas de disponibilidade. Usando o balanceamento de carga entre zonas, esse desequilíbrio na carga da solicitação é distribuído por todas as instâncias disponíveis na região.
Segurança ELB:
ELB suporta terminação SSL/TLS e HTTPS. A terminação no balanceador de carga é desejada porque a descriptografia consome muitos recursos e CPU. Colocar a carga de descriptografia no balanceador de carga permite que as instâncias do EC2 gastem seu poder de processamento em tarefas de aplicação, o que ajuda a melhorar o desempenho geral.
Elastic Load Balancers (junto com CloudFront) oferecem suporte ao Perfect Forward Secrecy. Este é um recurso que fornece salvaguardas adicionais contra a espionagem de dados criptografados em trânsito através do uso de uma chave de sessão aleatória exclusiva. Isso é feito garantindo que a parte em uso de um sistema de criptografia altere automática e frequentemente as chaves que usa para criptografar e descriptografar informações. Portanto, se esta chave mais recente for comprometida, ela exporá apenas uma pequena parte dos dados recentes do usuário.
Os balanceadores de carga clássicos não oferecem suporte à indicação de nome de servidor (SNI). O SNI permite que o servidor (o LB, neste caso) hospede com segurança vários certificados TLS para vários sites, todos sob um único endereço IP (o registro Alias ​​ou registro CName, neste caso). Para permitir o SNI, você deve usar um Application Load Balancer ou usá-lo com uma distribuição web do CloudFront.
Dimensionamento automático
Escalonamento automático simplificado:
O AWS Auto Scaling permite criar planos de escalabilidade que automatizam a forma como grupos de diferentes recursos respondem às mudanças na demanda. Você pode otimizar a disponibilidade, os custos ou o equilíbrio de ambos. O AWS Auto Scaling cria automaticamente todas as políticas de escalabilidade e define metas para você com base em sua preferência.

Detalhes principais do escalonamento automático:
O Auto Scaling é um grande benefício das economias de escala da nuvem, portanto, se você tiver necessidade de escalonamento, pense automaticamente em usar o serviço Auto Scaling.
O Auto Scaling tem três componentes:
Grupos : estes são componentes lógicos. Um grupo de servidores web de instâncias EC2, um grupo de banco de dados de instâncias RDS, etc.
Modelos de configuração : os grupos usam um modelo para configurar e iniciar novas instâncias para melhor atender às necessidades de escalabilidade. Você pode especificar informações para as novas instâncias, como a AMI a ser usada, o tipo de instância, grupos de segurança, dispositivos de bloco a serem associados às instâncias e muito mais.
Opções de escalabilidade : as opções de escalabilidade fornecem várias maneiras de escalar seus grupos do Auto Scaling. Você pode basear o gatilho de escalabilidade na ocorrência de uma condição especificada ou em um agendamento.
A imagem a seguir destaca o estado de um grupo de Auto Scaling. Os quadrados laranja representam instâncias ativas. Os quadrados pontilhados representam instâncias potenciais que podem e serão geradas sempre que necessário. O número mínimo, o número máximo e a capacidade desejada de instâncias são totalmente configuráveis.
Captura de tela 19/06/2020 às 16h44 18h

Ao usar o Auto Scaling, seus aplicativos obtêm os seguintes benefícios:
Melhor tolerância a falhas : o Auto Scaling pode detectar quando uma instância não está íntegra, encerrá-la e iniciar uma instância para substituí-la. Você também pode configurar o Auto Scaling para usar diversas zonas de disponibilidade. Se uma zona de disponibilidade ficar indisponível, o Auto Scaling poderá executar instâncias em outra para compensar.
Melhor disponibilidade : o Auto Scaling pode ajudá-lo a garantir que seu aplicativo sempre tenha a quantidade certa de capacidade para lidar com as demandas de tráfego atuais.
Quando se trata de dimensionar seus grupos de instâncias, o serviço Auto Scaling é flexível e pode ser feito de várias maneiras:
O Auto Scaling pode ser dimensionado com base na demanda colocada em suas instâncias. Esta opção automatiza o processo de escalonamento especificando determinados limites que, quando atingidos, acionarão o escalonamento. Esta é a implementação mais popular do Auto Scaling.
O Auto Scaling pode garantir o número atual de instâncias em todos os momentos. Esta opção sempre manterá o número de servidores que você deseja executar, mesmo quando eles falharem.
O Auto Scaling só pode ser dimensionado com intervenção manual. Se você deseja controlar todo o dimensionamento sozinho, esta opção faz sentido.
O Auto Scaling pode ser dimensionado com base em uma programação. Se você puder prever picos de tráfego com segurança, essa opção fará sentido.
Auto Scaling baseado em escalonamento preditivo. Essa opção permite que o AWS AI/ML aprenda mais sobre seu ambiente para prever o melhor momento de escalabilidade para melhorias de desempenho e economia de custos.
Ao manter a instância em execução atual, o Auto Scaling realizará verificações de integridade ocasionais nas instâncias em execução para garantir que todas estejam íntegras. Quando o serviço detecta que uma instância não está íntegra, ele encerra essa instância e, em seguida, coloca uma nova online.
Ao projetar HA para seu Auto Scaling, use diversas AZs e diversas regiões sempre que possível.
O Auto Scaling permite suspender e depois retomar um ou mais processos do Auto Scaling em seu grupo de Auto Scaling. Isso pode ser muito útil quando você deseja investigar um problema em seu aplicativo sem acionar o processo de Auto Scaling ao fazer alterações.
Você pode especificar sua configuração de inicialização com vários grupos do Auto Scaling. No entanto, você só pode especificar uma configuração de execução para um grupo do Auto Scaling por vez.
Você não pode modificar uma configuração de inicialização depois de criá-la. Se quiser alterar a configuração de execução de um grupo do Auto Scaling, você deverá criar uma nova configuração de execução e atualizar seu grupo do Auto Scaling para herdar essa nova configuração de execução.
Política de rescisão padrão do Auto Scaling:
A política de encerramento padrão para um grupo de Auto Scaling é encerrar automaticamente uma instância interrompida, portanto, a menos que você tenha configurado de outra forma, a interrupção de uma instância resultará em encerramento, independentemente de você querer que isso aconteça ou não. Uma nova instância será criada em seu lugar.
A política de encerramento padrão poupará instâncias informadas caso alguns servidores estejam executando sistemas ou aplicativos críticos. Esses servidores críticos são protegidos contra “scale in”, que é apenas o processo de exclusão de instâncias consideradas supérfluas aos requisitos.
A política de encerramento padrão foi projetada para ajudar a garantir que sua arquitetura de rede abranja as zonas de disponibilidade de maneira uniforme. Com a política de encerramento padrão, o comportamento do grupo do Auto Scaling é o seguinte:
Se houver instâncias em várias zonas de disponibilidade, uma instância da zona de disponibilidade com o maior número de instâncias será encerrada. Se houver mais de uma zona de disponibilidade com o mesmo número máximo de instâncias, ele escolherá a zona de disponibilidade onde as instâncias usam a configuração de inicialização mais antiga.
Em seguida, ele determinará quais instâncias desprotegidas na zona de disponibilidade selecionada usam a configuração de inicialização mais antiga. Se houver uma dessas instâncias, ela será encerrada.
Se houver várias instâncias para encerrar, ele determinará quais instâncias desprotegidas estão mais próximas da próxima hora de cobrança. (Isso ajuda você a maximizar o uso de suas instâncias do EC2 e a gerenciar os custos de uso do Amazon EC2.) Se houver algumas instâncias que atendam a esses critérios, elas serão encerradas.
Este fluxograma pode fornecer mais clareza sobre como a política padrão do Auto Scaling decide quais instâncias excluir:
Captura de tela 19/06/2020 às 17h19 14h

Período de espera do escalonamento automático:
O período de espera é uma configuração configurável para seu grupo de Auto Scaling que ajuda a garantir que ele não inicie ou encerre instâncias adicionais antes que a atividade de escalabilidade anterior entre em vigor.
Depois que o Grupo de Auto Scaling for dimensionado usando uma política, ele aguardará a conclusão do período de espera antes de retomar outras atividades de escalabilidade, se necessário.
O período de espera padrão é de 300 segundos, mas pode ser modificado.
Nuvem privada virtual (VPC)
VPC simplificado:
A VPC permite provisionar uma seção logicamente isolada da nuvem AWS, onde você pode iniciar serviços e sistemas em uma rede virtual definida por você. Ao ter a opção de selecionar quais recursos da AWS são públicos e quais não são, o VPC oferece um controle muito mais granular sobre a segurança.

Detalhes da chave VPC:
Você pode pensar no VPC como seu próprio data center virtual na nuvem. Você tem controle total da sua própria rede; incluindo a faixa de IP, a criação de sub-redes (sub-redes), a configuração das tabelas de rotas e os gateways de rede utilizados.
Você pode então iniciar instâncias do EC2 em uma sub-rede de sua escolha, selecionar os IPs que estarão disponíveis para as instâncias, atribuir grupos de segurança para elas e criar listas de controle de acesso à rede (NACLs) para as próprias sub-redes como proteção adicional.
Essa personalização oferece muito mais controle para especificar e personalizar a configuração da sua infraestrutura. Por exemplo, você pode ter uma sub-rede pública para seus servidores web receberem tráfego HTTP e, em seguida, uma sub-rede privada diferente para seu servidor de banco de dados onde o acesso à Internet é proibido.
Você usa sub-redes para utilizar com eficiência redes que possuem um grande número de hosts
VPCs vêm com defesa profunda por design. Desde a sub-rede (NACLs) até o servidor individual (grupo de segurança) e mais abaixo até o próprio aplicativo (práticas de codificação segura), você pode configurar vários níveis de proteção contra usuários e programas mal-intencionados.
A VPC padrão para seu ambiente AWS permite que todas as sub-redes tenham uma rota para a Internet, o que significa que todas as sub-redes na VPC padrão podem ser acessadas pela Internet. A configuração padrão permite implantar instâncias imediatamente e cada instância do EC2 terá um endereço IP público e privado.
Há uma VPC padrão por região. No entanto, você pode ter quantas VPCs personalizadas desejar e todas são privadas por padrão.
Ao criar uma VPC personalizada, novas sub-redes não são criadas por padrão. Você deve criá-los separadamente. O mesmo se aplica a um gateway de Internet. Se quiser que sua VPC tenha acesso à Internet, você também precisa criar o gateway para que a rede possa ser acessada publicamente por todo o mundo.
Por causa disso, quando você cria um IGW, ele estará inicialmente em estado desanexado. Você precisará atribuí-lo manualmente à VPC personalizada.
No entanto, depois de criar uma VPC personalizada, o seguinte será criado por padrão:
uma tabela de rotas
um NACL
um grupo de segurança
Captura de tela 19/06/2020 às 18h26min37h

Esses componentes, que serão explicados com mais detalhes caso ainda não sejam conhecidos, na verdade correspondem ao fluxo de tráfego de como os dados chegarão às suas instâncias. Quer o tráfego venha de fora ou de dentro da VPC, ele deve primeiro passar pela tabela de rotas por meio do roteador para saber onde está o destino desejado. Depois que isso for conhecido, o tráfego passará pela segurança em nível de sub-rede, conforme descrito pela NACL. Se a NACL considerar o tráfego válido, ele passará para a segurança em nível de instância conforme descrito pelo grupo de segurança. Se o tráfego não tiver sido eliminado neste momento, só então alcançará a instância pretendida.
O VPC Wizard é uma ferramenta automatizada útil para criar VPCs personalizadas.
Você pode ter sua VPC em hardware dedicado para que a rede seja exclusiva no nível físico, mas esta opção é extremamente cara. Felizmente, se uma VPC estiver em hospedagem dedicada, ela sempre poderá ser alterada de volta para a hospedagem padrão. Isso pode ser feito por meio da AWS CLI, SDK ou API. No entanto, os hosts existentes no hardware dedicado devem primeiro estar em stoppedestado.
Ao criar uma VPC, você deve atribuir a ela um bloco CIDR IPv4. Este bloco CIDR é um intervalo de endereços IPv4 privados que serão herdados pelas suas instâncias quando você as criar.
O intervalo de IP de uma VPC padrão é sempre /16 .
Ao criar intervalos de IP para suas sub-redes, o bloco CIDR /16 é o maior intervalo de IPs que pode ser usado. Isso ocorre porque as sub-redes devem ter tantos IPs ou menos IPs que a VPC à qual pertencem. Um bloco CIDR /28 é o menor intervalo de IP disponível para sub-redes.
Com CIDR em geral, /32 denota um único endereço IP e /0 refere-se a toda a rede. Quanto mais alto você subir no CIDR, mais estreito será o intervalo de IP.
As informações acima sobre IPs referem-se a endereços IP públicos e privados.
Endereços IP privados não podem ser acessados ​​pela Internet e, em vez disso, são usados ​​para comunicação entre as instâncias em sua VPC. Ao executar uma instância em uma VPC, um endereço IP privado do intervalo de endereços IPv4 da sub-rede é atribuído à interface de rede padrão (eth0) da instância.
Isso significa que todas as instâncias dentro de uma VPC possuem um IP privado, mas apenas aquelas selecionadas para se comunicar com o mundo externo possuem um IP público.
Quando você inicia uma instância em uma sub-rede que tem acesso público por meio de um gateway de Internet, são criados um endereço IP público e um endereço IP privado. Em vez disso, o endereço IP público é atribuído à interface de rede primária (eth0) criada para a instância. Externamente, o endereço IP público é mapeado para o endereço IP privado através da tradução de endereços de rede (NAT).
Opcionalmente, você pode associar um bloco CIDR IPv6 à VPC e às sub-redes e atribuir endereços IPv6 desse bloco aos recursos da VPC.
As VPCs são específicas da região e você pode ter até cinco VPCs por região.
Por padrão, a AWS está configurada para ter uma sub-rede em cada AZ das regiões onde sua aplicação está.
Em uma arquitetura VPC ideal e segura, você inicia os servidores web ou balanceadores de carga elásticos na sub-rede pública e os servidores de banco de dados na sub-rede privada.
Aqui está um exemplo de um aplicativo hipotético atrás de uma configuração típica de VPC:
Captura de tela 21/06/2020 às 18h20 21h

Os grupos de segurança podem abranger sub-redes, mas não abrangem VPCs. O ICMP garante que as instâncias de um grupo de segurança possam executar ping em outras instâncias de um grupo de segurança diferente. É compatível com IPv4 e IPv6.
Sub-redes VPC:
Se uma rede tiver um grande número de hosts sem subdivisões agrupadas logicamente, gerenciar muitos hosts poderá ser uma tarefa tediosa. Portanto, você usa sub-redes para dividir uma rede e facilitar o gerenciamento.
Ao criar uma sub-rede, certifique-se de especificar em qual VPC deseja colocá-la. Você pode atribuir intervalos IPv4 e IPv6 às suas sub-redes.
Os principais benefícios das sub-redes:
Eles melhoram o fluxo de tráfego e, portanto, a velocidade e o desempenho de toda a rede. Um gateway de Internet (IGW) recebendo um pacote e verificando em qual das 5 sub-redes o pacote deve ser entregue é muito mais rápido do que verificar 100 instâncias individualmente. E se o destino de um pacote estiver na sub-rede de onde ele se origina, o tráfego permanecerá dentro da sub-rede e não sobrecarregará o restante da VPC.
As sub-redes funcionam como grupos lógicos nos quais colocar suas entidades. Torna muito mais fácil configurar recursos semelhantes como um grupo, em vez de para cada instância individual.
A Amazon sempre reserva cinco endereços IP em uma sub-rede. Os primeiros quatro endereços IP e o último endereço IP de cada bloco CIDR de sub-rede estarão sempre indisponíveis para uso.
Listas de controle de acesso à rede:
Listas de controle de acesso à rede (ou NACLs) são como grupos de segurança, mas para sub-redes e não para instâncias. A principal diferença entre grupos de segurança e NACLs é que os grupos de segurança são stateful , o que significa que você pode executar regras de permissão e negação que podem ser divergentes, dependendo se o tráfego é de entrada ou de saída, para essa regra.
A tabela a seguir destaca as diferenças entre NACLs e sub-redes.
NACL	Grupo de segurança
Opera no nível da sub-rede	Opera no nível da instância
Suporta regras de permissão e regras de negação	Suporta apenas regras permitidas
Não tem estado: o tráfego de retorno deve ser explicitamente permitido pelas regras	Tem estado: o tráfego de retorno é permitido automaticamente, independentemente de quaisquer regras
Processamos as regras em ordem, começando pela regra de número mais baixo, ao decidir se permitiremos o tráfego	Avaliamos todas as regras antes de decidir se permitiremos o tráfego
Aplica-se automaticamente a todas as instâncias nas sub-redes às quais está associado (portanto, fornece uma camada adicional de defesa se as regras do grupo de segurança forem muito permissivas)	Aplica-se a uma instância somente se alguém especificar o grupo de segurança ao iniciar a instância ou associar o grupo de segurança à instância posteriormente
Como os NACLs não têm estado, você também deve garantir que as regras de saída existam juntamente com as regras de entrada para que a entrada e a saída possam fluir sem problemas.

O NACL padrão que acompanha uma nova VPC tem uma regra padrão para permitir todas as entradas e saídas. Isso significa que ele existe, mas não faz nada, pois todo o tráfego passa por ele livremente.

No entanto, quando você cria uma nova NACL (em vez de usar o padrão que vem com a VPC), as regras padrão negarão todas as entradas e saídas.

Se você criar uma nova NACL, deverá associar quaisquer sub-redes desejadas a ela manualmente para que elas possam herdar o conjunto de regras da NACL. Se você não atribuir explicitamente uma sub-rede a uma NACL, a AWS a associará à sua NACL padrão.

Os NACLs são avaliados antes dos grupos de segurança e você bloqueia IPs maliciosos com NACLs, não com grupos de segurança.

Uma sub-rede só pode seguir as regras listadas por uma NACL por vez. Entretanto, uma NACL pode descrever as regras para qualquer número de sub-redes. As regras entrarão em vigor imediatamente.

As regras de Network ACL são avaliadas pelo número da regra, do menor para o maior, e executadas imediatamente quando uma regra de permissão/negação correspondente é encontrada. Por causa disso, o pedido é importante com seus números de regra.

Quanto menor o número de uma regra na lista, maior será a antiguidade dessa regra. Liste suas regras de acordo.

Se você estiver usando o gateway NAT junto com seu NACL, deverá garantir a disponibilidade do intervalo de portas efêmeras do gateway NAT dentro das regras de seu NACL. Como o tráfego do gateway NAT pode aparecer em qualquer uma das portas do intervalo durante sua conexão, você deve garantir que todas as portas possíveis sejam contabilizadas e abertas.

A NACL pode ter um pequeno impacto sobre como as instâncias do EC2 em uma sub-rede privada se comunicarão com qualquer serviço, incluindo VPC Endpoints.

Instâncias NAT versus gateways NAT:
Anexar um gateway de Internet a uma VPC permite que instâncias com IPs públicos acessem diretamente a Internet. O NAT faz algo semelhante, porém é para instâncias que não possuem IP público. Serve como uma etapa intermediária que permite que instâncias privadas primeiro mascarem seu próprio IP privado como o IP público do NAT antes de acessar a Internet.
Você gostaria que suas instâncias privadas acessassem a Internet para que pudessem ter atualizações normais de software. O NAT impede qualquer início de conexão pela Internet.
Instâncias NAT são instâncias EC2 individuais que desempenham a função de fornecer às sub-redes privadas um meio de acessar a Internet com segurança.
Por serem instâncias individuais, a alta disponibilidade não é um recurso integrado e pode se tornar um ponto de estrangulamento em sua VPC. Eles não são tolerantes a falhas e servem como um ponto único de falha. Embora seja possível usar grupos de escalonamento automático, scripts para automatizar failover, etc. para evitar gargalos, é muito melhor usar o gateway NAT como alternativa para uma solução escalonável.
NAT Gateway é um serviço gerenciado composto por várias instâncias vinculadas entre si em uma zona de disponibilidade para obter alta disponibilidade por padrão.
Para obter mais HA e uma arquitetura independente de zona, crie um gateway NAT para cada zona de disponibilidade e configure seu roteamento para garantir que os recursos usem o gateway NAT em sua zona de disponibilidade correspondente.
As instâncias NAT estão obsoletas, mas ainda podem ser utilizadas. Os gateways NAT são o meio preferido para obter a tradução de endereços de rede.
Não há necessidade de corrigir gateways NAT, pois o serviço é gerenciado pela AWS. Você precisa corrigir instâncias NAT porque elas são apenas instâncias individuais do EC2.
Como a comunicação sempre deve ser iniciada a partir de suas instâncias privadas, você precisa de uma regra de roteamento para rotear o tráfego de uma sub-rede privada para seu gateway NAT.
Sua instância/gateway NAT terá que residir em uma sub-rede pública, pois sua sub-rede pública é a sub-rede configurada para ter acesso à Internet.
Ao criar instâncias NAT, é importante lembrar que as instâncias EC2 possuem verificações de origem/destino por padrão. O que essas verificações fazem é garantir que qualquer tráfego encontrado seja gerado pela instância ou seja o destinatário pretendido desse tráfego. Caso contrário, o tráfego será descartado porque a instância do EC2 não é a origem nem o destino.
Portanto, como as instâncias NAT atuam como uma espécie de proxy, você deve desabilitar as verificações de origem/destino ao refletir sobre uma instância NAT.
Hostes Bastiões:
Bastion Hosts são computadores para fins especiais projetados e configurados para resistir a ataques. Este servidor geralmente executa um único programa e é despojado além dessa finalidade para reduzir vetores de ataque.
O objetivo dos Bastion Hosts é acessar remotamente as instâncias por trás da sub-rede privada para fins de administração do sistema, sem expor o host por meio de um gateway de Internet.
A melhor maneira de implementar um Bastion Host é criar uma pequena instância EC2 que tenha apenas uma regra de grupo de segurança para um único endereço IP. Isso garante segurança máxima.
É perfeitamente aceitável usar uma instância pequena em vez de uma grande porque a instância só será usada como um servidor de salto que conecta diferentes servidores entre si.
Se você estiver acessando RDP ou SSH nas instâncias de sua sub-rede privada, use um Bastion Host. Se você for fornecer tráfego de Internet para as instâncias da sua sub-rede privada, use um NAT.
Semelhante aos gateways NAT e às instâncias NAT, os Bastion Hosts vivem em uma sub-rede pública.
Existem AMIs Bastion Host pré-preparadas.
Tabelas de rotas:
As tabelas de rotas são usadas para garantir que as sub-redes possam se comunicar entre si e que o tráfego saiba para onde ir.
Cada sub-rede criada é automaticamente associada à tabela de rotas principal da VPC.
Você pode ter várias tabelas de rotas. Se não desejar que sua nova sub-rede seja associada à tabela de rotas padrão, você deverá especificar que deseja associá-la a uma tabela de rotas diferente.
Devido a esse comportamento padrão, há uma possível preocupação de segurança a ser observada: se a tabela de rotas padrão for pública, as novas sub-redes associadas a ela também serão públicas.
A prática recomendada é garantir que a tabela de rotas padrão à qual as novas sub-redes estão associadas seja privada.
Isso significa que você garante que não haja rota para a Internet para a tabela de rotas padrão. Em seguida, você pode criar uma tabela de rotas personalizada que seja pública. Novas sub-redes automaticamente não terão rota para a Internet. Se quiser que uma nova sub-rede seja acessível publicamente, basta associá-la à tabela de rotas personalizada.
As tabelas de rotas podem ser configuradas para acessar endpoints (serviços públicos acessados ​​de forma privada) e não apenas a internet.
Portal da Internet:
Se o gateway da Internet não estiver conectado à VPC, que é o pré-requisito para que as instâncias sejam acessadas pela Internet, naturalmente as instâncias da sua VPC não estarão acessíveis.
Se você deseja que todo o seu VPC permaneça privado (e não apenas algumas sub-redes), não anexe um IGW.
Quando um endereço IP público é atribuído a uma instância EC2, ele é efetivamente registrado pelo Internet Gateway como um endpoint público válido. Porém, cada instância conhece apenas seu IP privado e não seu IP público. Somente o IGW conhece os IPs públicos que pertencem às instâncias.
Quando uma instância EC2 inicia uma conexão com a Internet pública, a solicitação é enviada usando o IP público como origem, mesmo que a instância não saiba nada sobre isso. Isso funciona porque o IGW realiza sua própria tradução de NAT, onde os IPs privados são mapeados para IPs públicos e vice-versa para o tráfego que entra e sai da VPC.
Assim, quando o tráfego da Internet é destinado ao endpoint IP público de uma instância, o IGW o recebe e encaminha o tráfego para a instância EC2 usando seu IP privado interno.
Você só pode ter um IGW por VPC.
Resumo : O IGW conecta seu VPC à Internet .
Redes Privadas Virtuais (VPNs):
As VPCs também podem servir como ponte entre o data center corporativo e a nuvem AWS. Com uma rede privada virtual (VPN) VPC, sua VPC se torna uma extensão do seu ambiente local.
Naturalmente, as instâncias executadas em sua VPC não podem se comunicar com seus próprios servidores locais. Você pode permitir o acesso primeiro:
anexando um gateway privado virtual ao VPC
criando uma tabela de rotas personalizada para a conexão
atualizando as regras do seu grupo de segurança para permitir o tráfego da conexão
criando a própria conexão VPN gerenciada.
Para ativar a conexão VPN, você também deve definir um recurso de gateway do cliente na AWS, que fornece informações da AWS sobre o dispositivo de gateway do cliente. E você deve configurar um endereço IP roteável pela Internet da interface externa do gateway do cliente.
Um gateway do cliente é um dispositivo físico ou aplicativo de software no lado local da conexão VPN.
Embora o termo “conexão VPN” seja um conceito geral, uma conexão VPN para AWS sempre se refere à conexão entre sua VPC e sua própria rede. A AWS oferece suporte a conexões VPN de segurança de protocolo da Internet (IPsec).
O diagrama a seguir ilustra uma única conexão VPN.
Captura de tela 21/06/2020 às 18h13 17h

A VPC acima possui um gateway privado virtual conectado (observação: não é um gateway de Internet) e há uma rede remota que inclui um gateway do cliente que você deve configurar para ativar a conexão VPN. Você configura o roteamento para que qualquer tráfego da VPC vinculado à sua rede seja roteado para o gateway privado virtual.
Resumo : As VPNs conectam seu local ao VPC pela Internet.
AWS DirectConnect:
Direct Connect é um serviço da AWS que estabelece uma conexão de rede dedicada entre suas instalações e a AWS. Você pode criar essa conectividade privada para reduzir custos de rede, aumentar a largura de banda e fornecer uma experiência de rede mais consistente em comparação com conexões regulares baseadas na Internet.
O caso de uso do Direct Connect são cargas de trabalho de alto rendimento ou se você precisar de uma conexão estável ou confiável
A VPN se conecta ao seu local pela Internet e o DirectConnect se conecta ao seu local por meio de um túnel privado.
As etapas para configurar uma conexão AWS DirectConnect:
Crie uma interface virtual no console DirectConnect. Esta é uma interface virtual pública.
Vá para o console VPC e depois para conexões VPN. Crie um gateway de cliente local.
Crie um gateway privado virtual e anexe-o ao ambiente VPC desejado.
Selecione conexões VPN e crie uma nova conexão VPN. Selecione o gateway do cliente e o gateway privado virtual.
Assim que a conexão VPN estiver disponível, configure a VPN no gateway do cliente ou no próprio firewall local
O fluxo de dados para a AWS via DirectConnect se parece com o seguinte: Roteador local -> linha dedicada -> sua própria gaiola / DMZ -> linha de conexão cruzada -> Roteador AWS Direct Connect -> Backbone AWS -> Nuvem AWS
Resumo : o DirectConnect conecta seu local ao VPC por meio de um túnel não público.
Pontos finais de VPC:
Os VPC Endpoints garantem que você possa conectar sua VPC a serviços da AWS compatíveis sem precisar de um gateway de Internet, dispositivo NAT, conexão VPN ou AWS Direct Connect. O tráfego entre sua VPC e outros serviços da AWS permanece dentro do ecossistema Amazon e esses endpoints são dispositivos virtuais com alta disponibilidade e sem restrições de largura de banda.
Eles funcionam basicamente anexando uma ENI a uma instância EC2 que pode se comunicar facilmente com uma ampla gama de serviços AWS.
Os endpoints de gateway dependem da criação de entradas em uma tabela de rotas e de apontá-las para endpoints privados usados ​​para S3 ou DynamoDB. Os endpoints de gateway são principalmente apenas um alvo que você define.
Os endpoints de interface usam o AWS PrivateLink e possuem um endereço IP privado, portanto, são sua própria entidade e não apenas um destino em uma tabela de rotas. Por causa disso, custam US$ 0,01/hora. Os Gateway Endpoints são gratuitos, pois são apenas uma nova rota a ser definida.
O Interface Endpoint provisiona uma interface Elastic Network ou ENI (pense em placa de rede) em sua VPC. Eles servem como entrada e saída para o tráfego de entrada e saída de outro serviço AWS compatível. Ele usa um registro DNS para direcionar seu tráfego para o endereço IP privado da interface. O Gateway Endpoint usa o prefixo de rota em sua tabela de rotas para direcionar o tráfego destinado ao S3 ou DynamoDB para o Gateway Endpoint (pense em 0.0.0.0/0 -> igw).
Para proteger seu endpoint de interface, use grupos de segurança. Mas para proteger o Gateway Endpoint, use políticas de VPC Endpoint.
Resumo : VPC Endpoints conectam seu VPC aos serviços da AWS por meio de um túnel não público.
AWS PrivateLink:
O AWS PrivateLink simplifica a segurança dos dados compartilhados com aplicativos baseados em nuvem, eliminando a exposição dos dados à Internet pública. O AWS PrivateLink fornece conectividade privada entre diferentes VPCs, serviços da AWS e aplicativos locais, com segurança na rede Amazon.
É semelhante ao serviço AWS Direct Connect, pois estabelece conexões privadas com a nuvem AWS, exceto que o Direct Connect vincula ambientes locais à AWS. O PrivateLink, por outro lado, protege o tráfego de ambientes VPC que já estão na AWS.
Isso é útil porque diferentes serviços da AWS geralmente se comunicam entre si pela Internet. Se você não quiser esse comportamento e, em vez disso, quiser que os serviços da AWS se comuniquem apenas dentro da rede da AWS, use o AWS PrivateLink. Ao não atravessar a Internet, o PrivateLink reduz a exposição a vetores de ameaças, como força bruta e ataques distribuídos de negação de serviço.
O PrivateLink permite que você publique um "endpoint" ao qual outras pessoas possam se conectar a partir de sua própria VPC. É semelhante a um VPC Endpoint normal, mas em vez de se conectar a um serviço AWS, as pessoas podem se conectar ao seu endpoint.
Além disso, você desejaria usar conectividade IP privada e grupos de segurança para que seus serviços funcionassem como se estivessem hospedados diretamente em sua rede privada.
Lembre-se de que o AWS PrivateLink se aplica a aplicativos/serviços que se comunicam entre si na rede AWS. Para que as VPCs se comuniquem entre si na rede AWS, use o peering de VPC.
Resumo: O AWS PrivateLink conecta seus serviços da AWS a outros serviços da AWS por meio de um túnel não público.
Pareamento de VPC:
O peering de VPC permite conectar um VPC a outro por meio de uma rota de rede direta usando os IPs privados pertencentes a ambos. Com o peering de VPC, as instâncias em VPCs diferentes se comportam como se estivessem na mesma rede.
Você pode criar uma conexão de peering de VPC entre suas próprias VPCs, independentemente de estarem na mesma região ou não, e com uma VPC em uma conta da AWS totalmente diferente.
O peering de VPC geralmente é feito de forma que haja um VPC central que faz peering com outros. Somente a VPC central pode se comunicar com as outras VPCs.
Você não pode fazer peering transitivo para VPCs não centrais. VPCs não centrais não podem passar pela VPC central para chegar a outra VPC não central. Você deve configurar um novo portal entre nós não centrais se precisar que eles se comuniquem entre si.
O diagrama a seguir destaca a ideia acima. A VPC B está livre para se comunicar com a VPC A com peering de VPC habilitado entre ambas. No entanto, a VPC B não pode continuar a conversa com a VPC C. Somente a VPC A pode se comunicar com a VPC C.
Captura de tela 19/06/2020 às 18h12 14h

Vale a pena saber quais configurações de peering de VPC não são suportadas:
Sobreposição de blocos CIDR
Peering transitivo
Roteamento de ponta a ponta por meio de um gateway ou dispositivo de conexão (conexão VPN, gateway de Internet, conexão AWS Direct Connect, etc.)
Você pode fazer peering entre regiões, mas não pode ter uma sub-rede estendida por diversas zonas de disponibilidade. No entanto, você pode ter várias sub-redes na mesma zona de disponibilidade.
Resumo : O peering de VPC conecta sua VPC a outra VPC por meio de um túnel não público.
Registros de fluxo de VPC:
Logs de fluxo de VPC é um recurso que captura as informações de IP de todo o tráfego que entra e sai de sua VPC. Os dados do log de fluxo são enviados para um bucket S3 ou CloudWatch onde você pode visualizar, recuperar e manipular esses dados.

Você pode capturar o fluxo de tráfego em vários estágios de sua viagem:

Tráfego fluindo para dentro e fora da VPC (como no IGW)
Tráfego fluindo para dentro e fora da sub-rede
Tráfego que entra e sai da interface de rede da instância EC2 (eth0, eth1, etc.)
Os registros de fluxo VPS capturam metadados de pacotes e não conteúdos de pacotes. Coisas como:

O IP de origem
O IP de destino
O tamanho do pacote
Qualquer coisa que possa ser observada de fora do pacote.
Seus logs de fluxo podem ser configurados para registrar tráfego válido, tráfego inválido ou ambos

Você pode ter logs de fluxo provenientes de uma VPC diferente da VPC onde estão seus logs de fluxo. No entanto, a outra VPC deve ser emparelhada por meio de peering de VPC e em sua conta por meio do AWS Organizations.

Você pode personalizar seus registros marcando-os.

Depois de criar um log de fluxo, você não poderá alterar sua configuração. Você deve fazer um novo.

Nem todo o tráfego IP é monitorado nos registros de fluxo de VPC. Veja a seguir uma lista de coisas que são ignoradas pelos logs de fluxo:

Solicitações de consulta para metadados de instância
Tráfego DHCP
Solicitações de consulta ao servidor DNS da AWS
Acelerador global da AWS:
O AWS Global Accelerator acelera a conectividade para melhorar o desempenho e a disponibilidade para os usuários. O Global Accelerator fica no topo do backbone da AWS e direciona o tráfego para endpoints ideais em todo o mundo. Por padrão, o Global Accelerator fornece dois endereços IP estáticos que você pode usar.

O Global Accelerator ajuda a reduzir o número de saltos para chegar aos recursos da AWS. Seus usuários só precisam chegar a um ponto de presença e, uma vez lá, tudo permanecerá interno à rede global da AWS. Normalmente, são necessárias muitas redes para chegar ao aplicativo por completo e os caminhos de e para o aplicativo podem variar. A cada salto, há risco envolvido na segurança ou na falha.

Captura de tela 21/06/2020 às 17h50 às 14h

Em resumo, o Global Accelerator é um pipeline rápido/confiável entre o usuário e o aplicativo.
É como fazer uma viagem (tráfego na web) e parar para pedir informações em partes possivelmente inseguras da cidade (várias redes são visitadas, o que pode aumentar os riscos de segurança), em vez de ter um GPS (acelerador global) que o leva diretamente para onde você deseja ir (ponto final) sem ter que fazer paradas desnecessárias.
Pode ser confundido com o Cloudfront, mas o CloudFront é um cache para conteúdo proveniente de um servidor de origem distante.
Embora o CloudFront simplesmente armazene em cache o conteúdo estático no local AWS Point Of Presence (POP) mais próximo, o acelerador global usará o mesmo Amazon POP para aceitar solicitações iniciais e encaminhá-las diretamente para os serviços.
O roteamento baseado em latência do Route53 também pode parecer semelhante ao Global Accelerator, mas o Route 53 serve simplesmente para ajudar a escolher qual região o usuário usará. Route53 não tem nada a ver com fornecer um caminho de rede rápido.
O Global Accelerator também fornece failover regional rápido.
Serviço de fila simples (SQS)
SQS simplificado:
SQS é um serviço baseado na web que dá acesso a uma fila de mensagens que pode ser usada para armazenar mensagens enquanto espera que outro serviço as processe. Ajuda no desacoplamento de sistemas e no dimensionamento horizontal de recursos AWS.

Detalhes principais do SQS:
O objetivo por trás do SQS é dissociar o trabalho entre sistemas. Dessa forma, os serviços downstream em um sistema podem executar o trabalho quando estiverem prontos, e não quando os serviços upstream os alimentam com dados.
Em um ambiente hipotético da AWS em execução sem SQS, o Aplicativo A passaria os dados do Aplicativo B , independentemente de o Aplicativo B estar pronto para receber as informações. No entanto, com o SQS, há uma etapa intermediária onde os dados são armazenados temporariamente em um buffer. Ele espera até que o Aplicativo B extraia os dados armazenados temporariamente. O SQS não é um serviço baseado em push, portanto é necessário que o SQS trabalhe em conjunto com outro serviço que o consulte em busca de informações.
Existem dois tipos de filas SQS; padrão e FIFO . As filas padrão podem ser recebidas fora de ordem com base no tamanho da mensagem ou em qualquer outra forma que as filas SQS decidam otimizar. As filas FIFO garantem que a ordem das mensagens que entram na fila é a mesma que a ordem das mensagens que saem dela.
As filas SQS padrão garantem que uma mensagem seja entregue pelo menos uma vez e por isso, ocasionalmente é possível que uma mensagem seja entregue mais de uma vez devido à arquitetura assíncrona e altamente distribuída. Com filas padrão, você tem um número quase ilimitado de transações por segundo.
As filas FIFO SQS garantem processamento exatamente uma vez e são limitadas a 300 transações por segundo.
As mensagens na fila podem ser mantidas lá de um minuto a 14 dias e o período de retenção padrão é de 4 dias.
Os tempos limite de visibilidade no SQS são o mecanismo no qual as mensagens marcadas para entrega da fila recebem um prazo para serem totalmente recebidas por um leitor. Isso é feito tornando-os temporariamente invisíveis para outros leitores. Se a mensagem não for totalmente processada dentro do prazo, a mensagem ficará visível novamente. Esta é outra maneira pela qual as mensagens podem ser duplicadas. Se quiser reduzir a chance de duplicação, aumente o tempo limite de visibilidade.
O tempo limite máximo de visibilidade é de 12 horas.
Lembre-se sempre de que as mensagens na fila SQS continuarão a existir mesmo depois que a instância do EC2 as tiver processado, até que você exclua essa mensagem. Você deve garantir a exclusão da mensagem após o processamento para evitar que a mensagem seja recebida e processada novamente quando o tempo limite de visibilidade expirar.
Uma fila SQS pode conter um número ilimitado de mensagens.
Você não pode definir uma prioridade para itens individuais na fila SQS. Se a prioridade das mensagens for importante, crie duas filas SQS separadas. As filas SQS para a mensagem prioritária podem ser pesquisadas primeiro pelas instâncias EC2 e, uma vez concluídas, as mensagens da segunda fila podem ser processadas em seguida.
Pesquisa SQS:
A votação é o meio pelo qual você consulta mensagens ou trabalho no SQS. O Amazon SQS fornece sondagens curtas e longas para receber mensagens de uma fila. Por padrão, as filas usam sondagem curta.
Sondagem longa SQS : esta técnica de sondagem só retornará da fila quando uma mensagem estiver lá, independentemente de a fila estar cheia ou vazia no momento. Dessa forma, o leitor precisa aguardar o tempo limite definido ou até que uma mensagem finalmente chegue. A sondagem longa do SQS não retorna uma resposta até que uma mensagem chegue na fila, reduzindo o custo geral ao longo do tempo.
SQS short-polling : Esta técnica de polling retornará imediatamente com uma mensagem que já está armazenada na fila ou de mãos vazias.
O ReceiveMessageWaitTimeSeconds é o atributo da fila que determina se você está usando a sondagem Curta ou Longa. Por padrão, seu valor é zero, o que significa que está usando sondagem curta. Se for definido com um valor maior que zero, então é uma pesquisa longa.
Cada vez que você pesquisa a fila, você incorre em uma cobrança. Portanto, é importante decidir cuidadosamente sobre uma estratégia de pesquisa que se adapte ao seu caso de uso.
Serviço de fluxo de trabalho simples (SWF)
SWF simplificado:
SWF é um serviço web que facilita a coordenação do trabalho em componentes de aplicativos distribuídos. O SWF tem uma variedade de casos de uso, incluindo processamento de mídia, back-end de aplicativos da web, fluxos de trabalho de processos de negócios e pipelines analíticos.

Detalhes da chave SWF:
SWF é uma forma de coordenar tarefas entre aplicativos e pessoas. É um serviço que combina fluxos de trabalho digitais e humanos.
Um exemplo de fluxo de trabalho orientado a humanos é o processo no qual os funcionários do armazém da Amazon encontram e enviam seu item como parte de seu pedido da Amazon.
O SWF fornece uma API orientada a tarefas e garante que uma tarefa seja atribuída apenas uma vez e nunca seja duplicada. Usando novamente os trabalhadores do armazém da Amazon como exemplo, isso faria sentido. A Amazon não gostaria de enviar a você o mesmo item duas vezes, pois perderia dinheiro.
O pipeline SWF é composto por três aplicativos de trabalho diferentes que ajudam a concluir um trabalho:
Atores SWF são trabalhadores que acionam o início de um fluxo de trabalho.
Os SWF Deciders são trabalhadores que controlam o fluxo do fluxo de trabalho depois de iniciado.
Os Trabalhadores de Atividade SWF são os trabalhadores que realmente executam a tarefa até a conclusão.
Com o SWF, as execuções do fluxo de trabalho podem durar até um ano, em comparação com o período máximo de retenção de 14 dias do SQS.
Serviço de Notificação Simples (SNS)
SNS simplificado:
Simple Notification Service é um serviço de mensagens baseado em push que fornece um método altamente escalonável, flexível e econômico para publicar mensagens personalizadas para assinantes que desejam ser informados sobre um determinado tópico.

Detalhes da chave SNS:
O SNS é usado principalmente para enviar alarmes ou alertas.
O SNS fornece tópicos para mensagens de alto rendimento, baseadas em push e muitos para muitos.
Usando tópicos do Amazon SNS, seus sistemas editores podem distribuir mensagens para um grande número de endpoints de assinantes para processamento paralelo, incluindo filas do Amazon SQS, funções do AWS Lambda e webhooks HTTP/S. Além disso, o SNS pode ser usado para distribuir notificações aos usuários finais usando push móvel, SMS e e-mail.
Você pode enviar essas notificações push para dispositivos Apple, Google, Fire OS e Windows.
O SNS permite agrupar vários destinatários usando tópicos. Um tópico é um ponto de acesso que permite que os destinatários se inscrevam dinamicamente para obter cópias idênticas da mesma notificação.
Um tópico pode oferecer suporte a entregas para vários tipos de endpoint. Quando você publica em um tópico, o SNS formata adequadamente cópias dessa mensagem para enviar a qualquer tipo de dispositivo.
Para evitar a perda de mensagens, as mensagens são armazenadas de forma redundante em várias AZs.
Não há pesquisas longas ou curtas envolvidas no SNS devido ao envio instantâneo de mensagens
O SNS possui entrega flexível de mensagens em vários protocolos de transporte e possui uma API simples.
Kinesis
Kinesis simplificado:
O Amazon Kinesis facilita a coleta, o processamento e a análise de dados de streaming em tempo real para que você possa obter insights oportunos e reagir rapidamente a novas informações. Com o Amazon Kinesis, você pode ingerir dados em tempo real, como vídeo, áudio, logs de aplicativos, fluxos de cliques de sites e dados de telemetria de IoT para machine learning, análises e outros aplicativos. O Amazon Kinesis permite processar e analisar dados à medida que eles chegam e responder instantaneamente, em vez de ter que esperar até que todos os dados sejam coletados para que o processamento possa começar.

Detalhes principais do Kinesis:
O Amazon Kinesis facilita o carregamento e a análise de grandes volumes de dados que entram na AWS.

Kinesis é usado para processar fluxos de dados em tempo real (dados gerados continuamente) de dispositivos que enviam dados constantemente para a AWS para que esses dados possam ser coletados e analisados.

É um serviço totalmente gerenciado que é dimensionado automaticamente para corresponder ao rendimento dos seus dados e não requer administração contínua. Ele também pode agrupar, compactar e criptografar os dados antes de carregá-los, minimizando a quantidade de armazenamento usada no destino e aumentando a segurança.

Existem três tipos diferentes de Kinesis:

Fluxos Kinesis

O Kinesis Streams funciona onde os produtores de dados transmitem seus dados para o Kinesis Streams, que pode reter os dados de um dia até 7 dias. Uma vez dentro do Kinesis Streams, os dados ficam contidos em fragmentos.
O Kinesis Streams pode capturar e armazenar continuamente terabytes de dados por hora de centenas de milhares de fontes, como fluxos de cliques de sites, transações financeiras, feeds de mídia social, registros de TI e eventos de rastreamento de localização. Por exemplo: solicitações de compra de uma grande loja online como Amazon, preços de ações, conteúdo Netflix, conteúdo Twitch, dados de jogos online, posicionamento e direções do Uber, etc.
Mangueira de incêndio Kinesis

O Amazon Kinesis Firehose é a maneira mais fácil de carregar dados de streaming em armazenamentos de dados e ferramentas de análise. Quando os dados são transmitidos para o Kinesis Firehose, não há armazenamento persistente para mantê-los. Os dados devem ser analisados ​​à medida que chegam, por isso é opcional ter funções Lambda dentro do Kinesis Firehose. Depois de processados, você envia os dados para outro lugar.
O Kinesis Firehose pode capturar, transformar e carregar dados de streaming no Amazon S3, Amazon Redshift, Amazon Elasticsearch Service e Splunk, permitindo análises quase em tempo real com ferramentas e painéis de business intelligence existentes que você já usa atualmente.
Kinesis Analytics

O Kinesis Analytics funciona com o Kinesis Streams e o Kinesis Firehose e pode analisar dados dinamicamente. Os dados no Kinesis Analytics também são enviados para outro lugar assim que o processamento for concluído. Ele analisa seus dados dentro do próprio serviço Kinesis.
As chaves de partição são usadas com o Kinesis para que você possa organizar os dados por fragmento. Dessa forma, a entrada de um dispositivo específico pode receber uma chave que limitará seu destino a um fragmento específico.

As chaves de partição são úteis se você quiser manter a ordem em seu fragmento.

Os consumidores, ou as instâncias do EC2 que leem o Kinesis Streams, podem entrar nos fragmentos para analisar o que há neles. Depois de concluir a análise ou análise dos dados, os consumidores podem transferi-los para vários locais para armazenamento, como um banco de dados ou S3.

A capacidade total de um stream do Kinesis é a soma dos dados em seus fragmentos constituintes.

Você sempre pode aumentar a capacidade de gravação atribuída à sua tabela de fragmentos.

lambda
Lambda simplificado:
O AWS Lambda permite executar código sem provisionar ou gerenciar servidores. Você paga apenas pelo tempo de computação consumido. Com o Lambda, você pode executar código para praticamente qualquer tipo de aplicativo ou serviço de back-end – tudo sem administração. Você carrega seu código e o Lambda cuida de tudo o que é necessário para executar e dimensionar seu código com alta disponibilidade. Você pode configurar seu código para ser acionado automaticamente a partir de outros serviços da AWS ou ser chamado diretamente de qualquer aplicativo web ou móvel.

Detalhes da chave Lambda:
Lambda é um serviço de computação onde você carrega seu código como uma função e a AWS fornece os detalhes necessários abaixo da função para que ela seja executada com sucesso.
AWS Lambda é a camada de abstração definitiva. Você só se preocupa com o código, a AWS faz todo o resto.
Lambda oferece suporte a Go, Python, C#, PowerShell, Node.js e Java
Cada função Lambda é mapeada para uma solicitação. O Lambda é dimensionado horizontalmente automaticamente.
O preço do Lambda depende do número de solicitações e o primeiro milhão é gratuito. Cada milhão depois disso custa US$ 0,20.
O preço do Lambda também depende do tempo de execução do seu código, arredondado para os 100 MB mais próximos, e da quantidade de memória que seu código aloca.
Lambda funciona globalmente.
As funções Lambda podem acionar outras funções Lambda.
Você pode usar o Lambda como um serviço orientado a eventos que é executado com base nas mudanças no seu ecossistema AWS.
Você também pode usar o Lambda como manipulador em resposta a eventos HTTP por meio de chamadas de API pelo AWS SDK ou API Gateway.
Captura de tela 30/06/2020 às 9h19h33

Ao criar ou atualizar funções do Lambda que usam variáveis ​​de ambiente, o AWS Lambda as criptografa usando o AWS Key Management Service. Quando sua função Lambda é invocada, esses valores são descriptografados e disponibilizados para o código Lambda.

Na primeira vez que você cria ou atualiza funções do Lambda que usam variáveis ​​de ambiente em uma região, uma chave de serviço padrão é criada automaticamente no AWS KMS. Esta chave é usada para criptografar variáveis ​​de ambiente. No entanto, se desejar usar auxiliares de criptografia e KMS para criptografar variáveis ​​de ambiente após a criação da função Lambda, você deverá criar sua própria chave AWS KMS e escolhê-la em vez da chave padrão.

Para permitir que sua função Lambda acesse recursos dentro de uma VPC privada, você deve fornecer informações adicionais de configuração específicas da VPC que incluam IDs de sub-rede da VPC e IDs de grupos de segurança. O AWS Lambda usa essas informações para configurar interfaces de rede elásticas (ENIs) que permitem que sua função se conecte com segurança a outros recursos em uma VPC privada.

O AWS X-Ray permite depurar sua função Lambda em caso de comportamento inesperado.

Lambda@Edge:
Você pode usar o Lambda@Edge para permitir que suas funções do Lambda personalizem o conteúdo que o CloudFront entrega.
Ele adiciona capacidade de computação aos pontos de presença do CloudFront e permite executar as funções em locais da AWS mais próximos dos visualizadores do seu aplicativo. As funções são executadas em resposta a eventos do CloudFront, sem provisionamento ou gerenciamento de servidores. Você pode usar funções do Lambda para alterar solicitações e respostas do CloudFront nos seguintes pontos:
Depois que o CloudFront recebe uma solicitação de um visualizador (solicitação do visualizador)
Antes do CloudFront encaminhar a solicitação para a origem (solicitação de origem)
Depois que o CloudFront receber a resposta da origem (resposta de origem)
Antes do CloudFront encaminhar a resposta ao visualizador (resposta do visualizador)
Captura de tela 30/06/2020 às 9h27h48

Você usaria o Lambda@Edge para simplificar e reduzir a infraestrutura de origem.
Gateway de API
Gateway de API simplificado:
O API Gateway é um serviço totalmente gerenciado para desenvolvedores que facilita a criação, publicação, gerenciamento e proteção de APIs inteiras. Com alguns cliques no AWS Management Console, você pode criar uma API que atua como uma “porta de entrada” para aplicativos acessarem dados, lógica de negócios ou funcionalidade de seus serviços de back-end, como cargas de trabalho em execução no código EC2). no AWS Lambda ou em qualquer aplicativo da web.

Detalhes da chave do gateway de API:
O Amazon API Gateway lida com todas as tarefas envolvidas na aceitação e processamento de centenas de milhares de chamadas de API simultâneas, incluindo gerenciamento de tráfego, autorização e controle de acesso, monitoramento e gerenciamento de versão de API.
O Amazon API Gateway não possui taxas mínimas ou custos iniciais. Você paga apenas pelas chamadas de API recebidas e pela quantidade de dados transferidos.
O API Gateway faz o seguinte para suas APIs:
Expõe endpoints HTTP(S) para funcionalidade RESTful
Usa funcionalidade sem servidor para conectar-se ao Lambda e DynamoDB
Pode enviar cada endpoint da API para um destino diferente
Funciona de forma barata e eficiente
Escala facilmente e sem esforço
Pode limitar solicitações para evitar ataques
Rastreie e controle o uso por meio de uma chave API
Pode ser controlado por versão
Pode ser conectado ao CloudWatch para monitoramento e observabilidade
Como o API Gateway pode funcionar com o AWS Lambda, você pode executar APIs e códigos sem precisar manter servidores.
O Amazon API Gateway fornece limitação em vários níveis, inclusive global e por chamada de serviço.
Em software, um processo de estrangulamento, ou controlador de estrangulamento, como às vezes é chamado, é um processo responsável por regular a taxa na qual o processamento do aplicativo é conduzido, seja de forma estática ou dinâmica.
Os limites de limitação podem ser definidos para taxas e rajadas padrão. Por exemplo, os proprietários de APIs podem definir um limite de taxa de 1.000 solicitações por segundo para um método específico em suas APIs REST e também configurar o Amazon API Gateway para lidar com uma explosão de 2.000 solicitações por segundo durante alguns segundos.
O Amazon API Gateway rastreia o número de solicitações por segundo. Qualquer solicitação acima do limite receberá uma resposta HTTP 429. Os SDKs do cliente gerados pelo Amazon API Gateway tentam novamente chamadas automaticamente quando recebem essa resposta.
Você pode adicionar cache às chamadas de API provisionando um cache do Amazon API Gateway e especificando seu tamanho em gigabytes. O cache é provisionado para um estágio específico de suas APIs. Isso melhora o desempenho e reduz o tráfego enviado ao seu back-end. As configurações de cache permitem controlar a maneira como a chave de cache é criada e o tempo de vida (TTL) dos dados armazenados para cada método. O Amazon API Gateway também expõe APIs de gerenciamento que ajudam a invalidar o cache de cada estágio.
Você pode ativar o cache da API para melhorar a latência e reduzir a E/S do seu endpoint.
Ao armazenar em cache para um estágio de API específico (versão controlada por versão), você armazena em cache as respostas para um TTL específico em segundos.
O API Gateway oferece suporte ao AWS Certificate Manager e pode usar certificados TLS/SSL gratuitos.
Com o API Gateway, existem dois tipos de chamadas de API:
Chamadas para a API do API Gateway para criar, modificar, excluir ou implantar APIs REST. Eles são registrados no CloudTrail.
Chamadas de API configuradas pelos desenvolvedores para fornecer funcionalidades personalizadas: elas não são registradas no CloudTrail.
Compartilhamento de recursos entre origens:
Na computação, a política de mesma origem é um conceito importante onde um navegador permite que scripts contidos em uma página acessem dados de outra página, mas somente se ambas as páginas tiverem a mesma origem.
Esse comportamento é imposto pelos navegadores, mas é ignorado por ferramentas como cURL e PostMan.
O compartilhamento de recursos de origem cruzada (CORS) é uma maneira pela qual o servidor na origem pode relaxar a política de mesma origem. O CORS permite que o compartilhamento de recursos restritos, como fontes, seja solicitado de outro domínio fora do domínio original de onde o primeiro recurso foi compartilhado.
O CORS define uma maneira de os aplicativos Web clientes carregados em um domínio interagirem com recursos em um domínio diferente. Com o suporte ao CORS, você pode criar aplicações web avançadas do lado do cliente com o Amazon S3 e permitir seletivamente o acesso de origem cruzada aos recursos do Amazon S3.
Se você encontrar um erro mencionando que uma política de origem não pode ser lida no recurso remoto, será necessário ativar o CORS no API Gateway.
O CORS é aplicado no lado do cliente (navegador da web).
Um exemplo comum desse problema é se você estiver usando um site com Javascript/AJAX para vários domínios no API Gateway. Você precisaria garantir que o CORS esteja habilitado.
O CORS não evita ataques XSS, mas protege contra ataques CSRF. O que ele faz é controlar quem pode usar os dados servidos pelo seu endpoint. Portanto, se você tiver um site meteorológico com retornos de chamada para uma API que verifica a previsão, poderá impedir alguém de escrever um site que atenda chamadas JavaScript em sua API quando navegar para seu site.
Quando alguém tentar fazer chamadas maliciosas, seu navegador lerá os cabeçalhos do CORS e não permitirá que a solicitação ocorra, protegendo você do ataque.
CloudFormação
CloudFormation simplificado:
CloudFormation é uma ferramenta automatizada para provisionar ambientes inteiros baseados em nuvem. É semelhante ao Terraform, onde você codifica as instruções sobre o que deseja ter dentro da configuração do seu aplicativo (X muitos servidores web do tipo Y com um banco de dados do tipo Z no backend, etc). Torna muito mais fácil apenas descrever o que você deseja na marcação e fazer com que a AWS faça o trabalho real de provisionamento envolvido.

Detalhes principais do CloudFormation:
O principal caso de uso do CloudFormation é para configurações avançadas e ambientes de produção, pois é complexo e possui muitos recursos robustos.
Os modelos CloudFormation podem ser usados ​​para criar, atualizar e excluir infraestrutura.
Os modelos são escritos em YAML ou JSON
Uma configuração completa do CloudFormation é chamada de pilha.
Depois que um modelo for criado, a AWS criará a pilha correspondente. Esta é a representação viva e ativa do referido modelo. Um modelo pode criar um número infinito de pilhas.
O campo Recursos é o único campo obrigatório ao criar um modelo CloudFormation
Os gatilhos de reversão permitem monitorar a criação da pilha à medida que ela é construída. Se ocorrer um erro, você poderá acionar uma reversão, como o nome indica.
O AWS Quick Starts é composto por muitas pilhas CloudFormation de alta qualidade projetadas por engenheiros da AWS.
Um modelo de exemplo que geraria uma instância EC2:
Captura de tela 01/07/2020 às 8h44min52s

Para quaisquer recursos lógicos na pilha, o CloudFormation criará recursos físicos correspondentes em sua conta AWS. É função do CloudFormation manter os recursos lógicos e físicos sincronizados.
Um modelo pode ser atualizado e usado para atualizar a mesma pilha.
ElasticBeanstalk
ElasticBeanstalk simplificado:
ElasticBeanstalk é outra maneira de criar scripts para seu processo de provisionamento, implantando aplicativos existentes na nuvem. ElasticBeanstalk é voltado para desenvolvedores que sabem muito pouco sobre nuvem e desejam a maneira mais simples de implantar seu código.

Detalhes principais do ElasticBeanstalk:
Basta fazer upload da sua aplicação e o ElasticBeanstalk cuidará da infraestrutura subjacente.
O ElasticBeanstalk tem provisionamento de capacidade, o que significa que você pode usá-lo com escalonamento automático desde o início. O ElasticBeanstalk aplica atualizações ao seu aplicativo tendo uma duplicata pronta com a versão já atualizada. Esta duplicata é então trocada pelo original. Isso é feito como medida preventiva caso seu aplicativo atualizado falhe. Se o aplicativo falhar, o ElasticBeanstalk voltará para a cópia original com a versão mais antiga e não haverá tempo de inatividade para os usuários que estão usando seu aplicativo.
Você pode usar o ElasticBeanstalk até mesmo para hospedar o Docker, já que o Elastic Beanstalk oferece suporte à implantação de aplicações web a partir de contêineres. Com os contêineres Docker, você pode definir seu próprio ambiente de execução, sua própria plataforma, linguagem de programação e quaisquer dependências de aplicativos (como gerenciadores de pacotes ou ferramentas) que não são suportadas por outras plataformas. O ElasticBeanstalk facilita a implantação do Docker, pois os contêineres do Docker já são independentes e incluem todas as informações de configuração e software necessários para execução.
Organizações AWS
Organizações AWS simplificadas:
AWS Organizations é um serviço de gerenciamento de contas que permite consolidar várias contas da AWS em uma organização que você cria e gerencia centralmente.

Detalhes principais das organizações da AWS:
As práticas recomendadas são usar a conta raiz para gerenciar a cobrança apenas com contas separadas usadas para implantar recursos.
O objetivo do AWS Organizations é implantar permissões para contas separadas abaixo da conta raiz e fazer com que essas políticas sejam implementadas. O AWS Organizations ajuda você a controlar centralmente seu ambiente à medida que você aumenta e dimensiona suas cargas de trabalho na AWS.
Você pode usar unidades organizacionais (OUs) para agrupar contas semelhantes e administrá-las como uma única unidade. Isso simplifica muito o gerenciamento de suas contas.
Você pode anexar um controle baseado em política a uma UO e todas as contas dentro da UO herdarão automaticamente a política. Portanto, se todos os desenvolvedores da sua empresa tiverem sua própria conta AWS de sandbox, eles poderão ser tratados como uma única unidade e restringidos pelas mesmas políticas.
Com o AWS Organizations, podemos ativar ou desativar serviços usando políticas de controle de serviços (SCPs) amplamente em unidades organizacionais ou, mais especificamente, em contas individuais
Use SCPs com AWS Organizations para estabelecer controles de acesso para que todos os principais do IAM (usuários e funções) os cumpram. Com SCPs, você pode especificar Conditions , Resources e NotAction para negar acesso a contas na sua organização ou unidade organizacional. Por exemplo, você pode usar SCPs para restringir o acesso a regiões específicas da AWS ou impedir a exclusão de recursos comuns, como uma função do IAM usada para seus administradores centrais.
Diversos
A seção a seguir inclui serviços, recursos e técnicas que podem aparecer no exame. Eles também são extremamente úteis para um engenheiro que usa AWS. Se os seguintes itens aparecerem no exame, eles não serão testados detalhadamente. Você apenas terá que saber qual é o significado por trás do nome. É uma ótima ideia aprender cada item a fundo para o benefício de sua carreira, mas não é necessário para o exame.

O que é o Amazon Cognito?
Antes de discutir o Amazon Cognito, primeiro é importante entender o que é Web Identity Federation. A Web Identity Federation permite que você conceda aos seus usuários acesso aos recursos da AWS após eles terem sido autenticados com sucesso em um provedor de identidade baseado na Web, como Facebook, Google, Amazon, etc. Após um login bem-sucedido nesses serviços, o usuário recebe um código de autenticação de o provedor de identidade que pode ser usado para obter credenciais temporárias da AWS.
Amazon Cognito é o serviço da Amazon que fornece Web Identity Federation. Você não precisa escrever o código que instrui os usuários a fazer login no Facebook ou no Google em seu aplicativo. O Cognito já faz isso para você imediatamente.
Uma vez autenticado em um provedor de identidade (por exemplo, o Facebook), o provedor fornece um token de autenticação. Esse token de autenticação é então fornecido ao Cognito, que responde com acesso limitado ao seu ambiente AWS. Você determina o quão limitado gostaria que esse acesso fosse na função do IAM.
O trabalho do Cognito é intermediar entre seu aplicativo e autenticadores legítimos.
Os grupos de usuários Cognito são diretórios de usuários usados ​​para inscrição e funcionalidade de login em seu aplicativo. A autenticação bem-sucedida gera um token web JSON. Lembre-se de que os grupos de usuários sejam baseados em usuários. Ele lida com registro, recuperação e autenticação.
Cognito Identity Pools são usados ​​para permitir aos usuários acesso temporário a serviços diretos da AWS, como S3 ou DynamoDB. Na verdade, os pools de identidade entram e concedem a você a função do IAM.
A autenticação baseada em SAML pode ser usada para permitir login no AWS Management Console para usuários não IAM.
Em particular, você pode usar o Microsoft Active Directory, que também implementa Security Assertion Markup Language (SAML).
Você pode usar o Amazon Cognito para fornecer credenciais temporárias e com privilégios limitados ao seu aplicativo para que os usuários possam acessar os recursos da AWS.
Os pools de identidades do Amazon Cognito oferecem suporte a identidades autenticadas e não autenticadas.
Você pode recuperar um identificador exclusivo do Amazon Cognito (ID de identidade) para seu usuário final imediatamente se estiver permitindo usuários não autenticados ou depois de definir os tokens de login no provedor de credenciais se estiver autenticando usuários.
Quando você precisar adicionar autenticação facilmente ao seu aplicativo móvel e de desktop, pense no Amazon Cognito.
O que é o AWS Resource Access Manager?
O AWS Resource Access Manager (RAM) é um serviço que permite compartilhar recursos da AWS de maneira fácil e segura com qualquer conta da AWS ou dentro da sua organização da AWS. Você pode compartilhar AWS Transit Gateways, sub-redes, configurações do AWS License Manager e recursos de regras do Amazon Route 53 Resolver com RAM.
Muitas organizações usam várias contas para criar isolamento administrativo ou de cobrança e para limitar o impacto de erros como parte do serviço AWS Organizations.
A RAM elimina a necessidade de criar recursos duplicados em diversas contas, reduzindo a sobrecarga operacional do gerenciamento desses recursos em cada conta que você possui.
Você pode criar recursos centralmente em um ambiente com várias contas e usar RAM para compartilhar esses recursos entre contas em três etapas simples: criar um compartilhamento de recursos, especificar recursos e especificar contas.
RAM está disponível sem custo adicional.
O que é Atenas?
Athena é um serviço de consulta interativo que permite interagir e consultar dados do S3 usando comandos SQL padrão. Isso é benéfico para consultas programáticas para o desenvolvedor médio. Não tem servidor, não requer provisionamento e você paga por consulta e por TB verificado. Você basicamente transforma o S3 em um banco de dados com suporte SQL usando Athena.
Exemplos de casos de uso:
Logs de consulta despejados em buckets S3 como alternativa ou complemento à pilha ELK
Definir consultas para executar relatórios de negócios com base nos dados que entram regularmente no S3
Executar consultas em dados de fluxo de cliques para obter mais informações sobre o comportamento do cliente
O que é AWS Macie?
Para entender o Macie, é importante entender PII ou informações de identificação pessoal:
Dados pessoais utilizados para estabelecer a identidade de um indivíduo que podem ser explorados
Exemplos: número do Seguro Social, número de telefone, endereço residencial, endereço de e-mail, data de nascimento, número do passaporte, etc.
O Amazon Macie é um serviço de segurança baseado em ML que ajuda a evitar a perda de dados descobrindo, classificando e protegendo automaticamente dados confidenciais armazenados no Amazon S3. O Amazon Macie usa aprendizado de máquina para reconhecer dados confidenciais, como informações de identificação pessoal (PII) ou propriedade intelectual, atribui um valor comercial e fornece visibilidade sobre onde esses dados estão armazenados e como estão sendo usados ​​na sua organização.
Você pode ser informado sobre detecções por meio de painéis, alertas ou relatórios do Macie.
Macie também pode analisar logs do CloudTrail para ver quem pode ter interagido com dados confidenciais.
O Macie monitora continuamente a atividade de acesso a dados em busca de anomalias e fornece alertas quando detecta risco de acesso não autorizado ou vazamento inadvertido de dados.
Macie tem a capacidade de detectar permissões de acesso global definidas inadvertidamente em dados confidenciais, detectar o upload de chaves de API dentro do código-fonte e verificar se os dados confidenciais do cliente estão sendo armazenados e acessados ​​de uma maneira que atenda aos seus padrões de conformidade.
O que é AWS KMS?
O AWS Key Management Service (AWS KMS) é um serviço gerenciado que facilita a criação e o controle das chaves de criptografia usadas para criptografar seus dados. As chaves mestras criadas no AWS KMS são protegidas por módulos criptográficos validados pelo FIPS 140-2.
O AWS KMS é integrado à maioria dos outros serviços da AWS que criptografam seus dados com chaves de criptografia gerenciadas por você. O AWS KMS também está integrado ao AWS CloudTrail para fornecer logs de uso de chaves de criptografia para ajudar a atender às suas necessidades de auditoria, regulamentação e conformidade.
Você pode configurar seu aplicativo para usar a API KMS para criptografar todos os dados antes de salvá-los no disco.
O que é o AWS Secrets Manager?
AWS Secrets Manager é um serviço da AWS que facilita o gerenciamento de segredos.
Os segredos podem ser credenciais de banco de dados, senhas, chaves de API de terceiros e até mesmo texto arbitrário. É possível armazenar e controlar o acesso a esses segredos centralmente usando o console do Secrets Manager, a interface de linha de comando (CLI) do Secrets Manager ou a API e SDKs do Secrets Manager.
No passado, quando você criava um aplicativo personalizado que recuperava informações de um banco de dados, normalmente era necessário incorporar as credenciais (o segredo) para acessar o banco de dados diretamente no aplicativo. Quando chegou a hora de alternar as credenciais, foi necessário fazer muito mais do que apenas criar novas credenciais. Você teve que investir tempo para atualizar o aplicativo para usar as novas credenciais. Então você teve que distribuir o aplicativo atualizado. Se você tivesse vários aplicativos que compartilhavam credenciais e perdesse a atualização de um deles, o aplicativo seria interrompido.
Devido a esse risco, muitos clientes optaram por não alternar regularmente suas credenciais, o que efetivamente substitui um risco por outro (funcionalidade versus segurança).
O Secrets Manager permite substituir credenciais embutidas em seu código (incluindo senhas) por uma chamada de API para o Secrets Manager para recuperar o segredo programaticamente.
Isso ajuda a garantir que o segredo não possa ser comprometido por alguém que examine seu código, porque o segredo simplesmente não existe.
Além disso, é possível configurar o Secrets Manager para alternar automaticamente o segredo para você de acordo com uma programação especificada. Isso permite substituir segredos de longo prazo por segredos de curto prazo, o que ajuda a reduzir significativamente o risco de comprometimento.
O que é AWS STS?
AWS Security Token Service (AWS STS) é o serviço que você pode usar para criar e fornecer a usuários confiáveis ​​credenciais de segurança temporárias que podem controlar o acesso aos seus recursos da AWS.
As credenciais de segurança temporárias funcionam de forma quase idêntica às credenciais de chave de acesso de longo prazo que os usuários do IAM podem usar.
As credenciais de segurança temporárias são de curto prazo, como o nome indica. Eles podem ser configurados para durar de alguns minutos a várias horas. Depois que as credenciais expiram, a AWS não as reconhece mais nem permite qualquer tipo de acesso a partir de solicitações de API feitas com elas.
O que é OpsWorks?
AWS OpsWorks é um serviço de gerenciamento de configuração que fornece instâncias gerenciadas de Chef e Puppet. Chef e Puppet são plataformas de automação que permitem usar código para automatizar as configurações de seus servidores.
O OpsWorks permite usar o Chef e o Puppet para automatizar o modo como os servidores são configurados, implantados e gerenciados em instâncias do Amazon EC2 ou ambientes de computação locais.
OpsWorks tem três ofertas: AWS Opsworks for Chef Automate, AWS OpsWorks for Puppet Enterprise e AWS OpsWorks Stacks.
O AWS OpsWorks Stacks permite gerenciar aplicações e servidores na AWS e no local. Com o OpsWorks Stacks, você pode modelar seu aplicativo como uma pilha contendo diferentes camadas, como balanceamento de carga, banco de dados e servidor de aplicativos.
O OpsWorks Stacks é complexo o suficiente para implantar e configurar instâncias do Amazon EC2 em cada camada ou conectar-se a outros recursos, como bancos de dados do Amazon RDS.
O que é o Transcodificador Elástico?
Um transcodificador de mídia na nuvem. Basicamente, é um serviço que converte arquivos de mídia do formato original para o formato de mídia especificado, seja para telefones, tablets, PCs, etc.
Devido ao suporte integrado para diferentes tipos de mídia, você pode confiar que a qualidade resultante será boa.
Com o Elastic Transcoder, você paga por minuto do trabalho de transcodificação e pela resolução do trabalho concluído.
O que é o AWS Directory Service?
O AWS Directory Service oferece várias maneiras de usar o Amazon Cloud Directory e o Microsoft Active Directory (AD) com outros serviços da AWS.
Os diretórios armazenam informações sobre usuários, grupos e dispositivos, e os administradores os utilizam para gerenciar o acesso a informações e recursos.
O AWS Directory Service oferece diversas opções de diretório para clientes que desejam usar aplicativos existentes com reconhecimento do Microsoft AD ou do Lightweight Directory Access Protocol (LDAP) na nuvem. Ele também oferece as mesmas opções para desenvolvedores que precisam de um diretório para gerenciar usuários, grupos, dispositivos e acesso.
O que é IoT Core?
O AWS IoT Core é um serviço de nuvem gerenciado que permite que dispositivos conectados interajam de maneira fácil e segura com aplicativos em nuvem e outros dispositivos.
O AWS IoT Core fornece comunicação e processamento de dados seguros em diferentes tipos de dispositivos e locais conectados para que você possa criar facilmente aplicativos de IoT.
O que é AWS WorkSpaces?
O Amazon WorkSpaces é uma solução de desktop como serviço (DaaS) gerenciada e segura. Você pode usar o Amazon WorkSpaces para provisionar desktops Windows ou Linux em apenas alguns minutos e escalar rapidamente para fornecer milhares de desktops a funcionários em todo o mundo.
O Amazon WorkSpaces ajuda a eliminar a complexidade no gerenciamento de inventário de hardware, versões e patches de sistema operacional e infraestrutura de desktop virtual (VDI), o que ajuda a simplificar sua estratégia de entrega de desktops.
Com o Amazon WorkSpaces, seus usuários obtêm um desktop rápido e responsivo de sua escolha, que podem acessar em qualquer lugar, a qualquer hora e em qualquer dispositivo compatível.
O que é AWS Fargate?
AWS Fargate é um mecanismo de computação sem servidor para contêineres.
O tipo de inicialização Fargate permite executar aplicativos em contêineres sem a necessidade de provisionar e gerenciar a infraestrutura de back-end. Basta registrar sua definição de tarefa e o Fargate iniciará o contêiner para você.
Funciona com Amazon Elastic Container Service (ECS) e Amazon Elastic Kubernetes Service (EKS).
O Fargate facilita o foco na criação de seus aplicativos. Ele elimina a necessidade de provisionar e gerenciar servidores, permite especificar e pagar por recursos por aplicativo e melhora a segurança por meio do isolamento de aplicativos por design.
O que é o Amazon Elastic Container Service?
O Amazon Elastic Container Service (Amazon ECS) é um serviço de orquestração de contêineres totalmente gerenciado.
O Amazon ECS elimina a necessidade de instalar, operar e dimensionar sua própria infraestrutura de gerenciamento de cluster. Com chamadas de API simples, você pode iniciar e interromper aplicativos habilitados para contêiner, consultar o estado completo do seu cluster e acessar muitos recursos familiares, como grupos de segurança, Elastic Load Balancing, volumes EBS e funções IAM.
Você pode usar o Amazon ECS para programar o posicionamento de contêineres no cluster com base nas necessidades de recursos e nos requisitos de disponibilidade. Você também pode integrar seu próprio agendador ou agendadores de terceiros para atender aos requisitos específicos do negócio ou do aplicativo.
Você pode optar por executar clusters ECS usando AWS Fargate, que é computação sem servidor para contêineres. O Fargate elimina a necessidade de provisionar e gerenciar servidores, permite especificar e pagar por recursos por aplicativo e melhora a segurança por meio do isolamento de aplicativos desde o design.
O que é o serviço Amazon Elastic Kubernetes?
O Amazon Elastic Kubernetes Service (Amazon EKS) é um serviço Kubernetes totalmente gerenciado. O EKS executa Kubernetes upstream e é certificado em conformidade com Kubernetes para que você possa aproveitar todos os benefícios das ferramentas de código aberto da comunidade. Você também pode migrar facilmente qualquer aplicativo Kubernetes padrão para EKS sem precisar refatorar seu código.
Kubernetes é um software de código aberto que permite implantar e gerenciar aplicativos em contêineres em escala. O Kubernetes agrupa contêineres em agrupamentos lógicos para gerenciamento e descoberta e, em seguida, os lança em clusters de instâncias do EC2. Usando o Kubernetes, você pode executar aplicativos em contêineres, incluindo microsserviços, trabalhadores de processamento em lote e plataformas como serviço (PaaS) usando o mesmo conjunto de ferramentas no local e na nuvem.
O Amazon EKS provisiona e dimensiona o plano de controle do Kubernetes, incluindo os servidores de API e a camada de persistência de back-end, em várias zonas de disponibilidade da AWS para alta disponibilidade e tolerância a falhas. O Amazon EKS detecta e substitui automaticamente nós do plano de controle não íntegros e fornece patches para o plano de controle.
Sem o Amazon EKS, você mesmo precisa executar o plano de controle do Kubernetes e o cluster de nós de trabalho. Com o Amazon EKS, você provisiona seus nós de trabalho usando um único comando no console, CLI ou API do EKS, e a AWS cuida do provisionamento, da escalabilidade e do gerenciamento do plano de controle do Kubernetes em uma configuração altamente disponível e segura. Isso elimina uma carga operacional significativa para executar o Kubernetes e permite que você se concentre na construção de aplicativos em vez de gerenciar a infraestrutura da AWS.
Você pode executar o EKS usando o AWS Fargate, que é uma computação sem servidor para contêineres. O Fargate elimina a necessidade de provisionar e gerenciar servidores, permite especificar e pagar por recursos por aplicativo e melhora a segurança por meio do isolamento de aplicativos desde o design.
O Amazon EKS está integrado a vários serviços da AWS para fornecer escalabilidade e segurança para seus aplicativos. Esses serviços incluem Elastic Load Balancing para distribuição de carga, IAM para autenticação, Amazon VPC para isolamento e AWS CloudTrail para registro em log.
O que significa luz piloto?
O termo piloto light é frequentemente usado para descrever um cenário de recuperação de desastres no qual uma versão mínima de um ambiente está sempre em execução na nuvem.
A ideia da luz piloto é uma analogia que vem do aquecedor a gás. Em um aquecedor a gás, uma pequena chama que está sempre acesa e pode acender rapidamente toda a fornalha para aquecer uma casa. Este cenário é semelhante a um cenário de backup e restauração.
Por exemplo, com a AWS você pode manter uma luz piloto configurando e executando os elementos principais mais críticos do seu sistema na AWS. Quando chegar o momento da recuperação, você poderá provisionar rapidamente um ambiente de produção em grande escala em torno do núcleo crítico que sempre esteve em execução.
O que são implantações Azul-Verde?
Um dos desafios da automação de implantações é a passagem do estágio final de testes para a produção ao vivo. Geralmente, você precisa fazer isso rapidamente para minimizar o tempo de inatividade.
A abordagem de implantação Azul-Verde faz isso garantindo que você tenha dois ambientes de produção, tão idênticos quanto possível. A qualquer momento um deles, digamos o azul, por exemplo, está ativo. Ao preparar uma nova versão do seu software, você realiza o estágio final de testes no ambiente verde. Assim que o software estiver funcionando no ambiente verde, você troca o roteador para que todas as solicitações recebidas vão para o ambiente verde - o azul agora está ocioso.
A implantação azul-verde também oferece uma maneira rápida de reverter - se algo der errado, você mudará o roteador de volta para o ambiente azul.
CloudFormation e CodeDeploy (versão do Jenkins da AWS) oferecem suporte a essa técnica de implantação.
O que é o Amazon Data Lifecycle Manager?
Você pode usar o Amazon Data Lifecycle Manager (Amazon DLM) para automatizar a criação, retenção e exclusão de snapshots obtidos para fazer backup de volumes do Amazon EBS.
Automatizar o gerenciamento de snapshots ajuda você a:
Proteja dados valiosos aplicando um agendamento regular de backup.
Retenha backups conforme exigido pelos auditores ou pela conformidade interna.
Reduza os custos de armazenamento excluindo backups desatualizados.
Usar o Amazon DLM significa que você não precisa mais se lembrar de tirar snapshots do EBS, reduzindo assim a carga cognitiva dos engenheiros.
O que é autorização de origem de rota?
Você pode trazer parte ou todo o seu intervalo de endereços IPv4 públicos da sua rede local para sua conta da AWS. Você continua sendo o proprietário do intervalo de endereços, mas a AWS o anuncia na Internet. Depois de trazer o intervalo de endereços para a AWS, ele aparecerá na sua conta como um pool de endereços.
Você pode então criar um endereço Elastic IP a partir do seu pool de endereços e usá-lo com seus recursos da AWS, como instâncias EC2, gateways NAT e Network Load Balancers. Isso também é chamado de "Traga seus próprios endereços IP (BYOIP)".
Para garantir que somente você possa trazer seu intervalo de endereços para sua conta da AWS, você deve autorizar a Amazon a anunciar o intervalo de endereços e fornecer prova de que você é o proprietário do intervalo de endereços.
O benefício do ROA é que você pode migrar aplicativos pré-existentes para a AWS sem exigir que seus parceiros e clientes alterem suas listas de permissões de endereços IP.
O que é o Amazon MQ?
O Amazon MQ é um serviço de agente de mensagens gerenciado que facilita a configuração e a operação de agentes de mensagens na nuvem.
O serviço é usado ao migrar serviços e aplicativos locais para a nuvem, e é assim que ele difere do Amazon SQS.
O Amazon MQ oferece suporte a agentes com durabilidade otimizada e apoiados pelo Amazon EFS para oferecer suporte à alta disponibilidade e durabilidade de mensagens, e a agentes com otimização de taxa de transferência apoiados pelo Amazon EBS para oferecer suporte a aplicações de alto volume que exigem baixa latência e alta taxa de transferência.
Você pode migrar facilmente de qualquer agente de mensagens para o Amazon MQ porque não precisa reescrever nenhum código de mensagens em seus aplicativos.
O Amazon MQ é adequado para profissionais de TI corporativos, desenvolvedores e arquitetos que gerenciam eles próprios um agente de mensagens – seja no local ou na nuvem – e desejam migrar para um serviço de nuvem totalmente gerenciado sem reescrever o código de mensagens em seus aplicativos.
O que é AWSConfig?
AWS Config é um serviço que permite avaliar, auditar e avaliar as configurações dos seus recursos da AWS. O Config monitora e registra continuamente as configurações de recursos da AWS e permite automatizar a avaliação das configurações registradas em relação às configurações desejadas.
Com o Config, você pode revisar alterações nas configurações e relacionamentos entre recursos da AWS, mergulhar em históricos detalhados de configuração de recursos e determinar sua conformidade geral em relação às configurações especificadas em suas diretrizes internas. Isso permite simplificar a auditoria de conformidade, a análise de segurança, o gerenciamento de alterações e a solução de problemas operacionais.
O AWS Config permite que você faça o seguinte: ·
Avalie as configurações de recursos da AWS para obter as configurações desejadas. ·
Obtenha um instantâneo das configurações atuais dos recursos suportados associados à sua conta da AWS. ·
Recupere configurações de um ou mais recursos existentes em sua conta. ·
Recuperar configurações históricas de um ou mais recursos. ·
Receba uma notificação sempre que um recurso for criado, modificado ou excluído.
Visualize relacionamentos entre recursos. Por exemplo, talvez você queira localizar todos os recursos que usam um grupo de segurança específico.
   
# Invalidação de cache
O CloudFront armazena automaticamente o conteúdo em cache em seus pontos de presença para melhorar o desempenho de leitura. Porém, se o conteúdo for atualizado com frequência, será necessário invalidar o conteúdo armazenado em cache para que os usuários possam acessar a versão atualizada. Existem duas maneiras de invalidar conteúdo no CloudFront:

+ Invalidação de objeto individual - Este método permite invalidar um arquivo específico do cache do CloudFront.
+ Invalidação por caminho(by path) - Este método permite invalidar vários arquivos que correspondam a um determinado padrão. Isso pode ser feito especificando um padrão de caminho que corresponda aos arquivos que você deseja invalidar.
É importante observar que a invalidação do conteúdo armazenado em cache no CloudFront pode levar algum tempo e resultar em um aumento temporário na latência. Além disso, há custos associados à invalidação do conteúdo em cache, por isso é importante considerar cuidadosamente quando e com que frequência realizar invalidações.

# Acelerador Global AWS
💡 **Anycast IP** é uma metodologia de endereçamento e roteamento de rede em que um único endereço IP é compartilhado por vários servidores ou dispositivos. Quando um cliente envia uma solicitação para um IP Anycast, a rede roteia a solicitação para o servidor ou dispositivo mais próximo que está anunciando o endereço IP, com base no protocolo de roteamento.
Suponha que implantamos nosso aplicativo na Índia. No entanto, os usuários da América e da Europa podem enfrentar problemas de latência ao acessar nosso aplicativo devido ao tráfego de rede ter que atravessar a Internet pública antes de chegar à Índia. Para reduzir esta latência, decidimos implantar instâncias adicionais da aplicação na América do Norte, na América do Sul e na Europa. O objetivo é redirecionar os usuários com base em sua localização, de modo que, se um usuário estiver na América do Norte, ele será direcionado para a instância de aplicativo íntegro mais próxima naquela região. Para alcançar esse roteamento inteligente, utilizamos o AWS Global Accelerator.

Quando um usuário faz uma solicitação, seu tráfego é direcionado para o ponto de presença da AWS mais próximo usando o roteamento Anycast IP. A partir daí, o AWS Global Accelerator roteia de forma inteligente o tráfego para a instância de aplicação íntegra mais próxima, levando em consideração fatores como integridade da rede, integridade da aplicação e proximidade do usuário.

![image](https://github.com/Marianalima31/guia-de-estudo-aws-solutions-architect-associate/assets/77506074/7ec045dc-324b-41ea-a03d-7ff58f04f85c)

