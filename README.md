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
# Maximizando o desempenho de leitura/gravação do S3:
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
# Carregamento de várias partes do S3:
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
