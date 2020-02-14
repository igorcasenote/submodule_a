# Primeiros **Passos**

Seja bem-vindo à Azion!

Aqui você encontrará informações sobre os primeiros passos necessários para configurar sua conta. Sempre que necessário, consulte a documentação detalhada dos produtos da Azion no menu lateral.

> 1. [Ative sua conta](#ative-sua-conta)
> 2. [Crie um novo Edge Application](#crie-um-novo-edge-application)
> 3. [Crie um novo Domain associado ao seu Edge Application](#crie-um-novo-domain-associado-ao-seu-edge-application)
> 4. [Altere o DNS de sua aplicação para o Domain criado](#altere-o-domain-de-sua-aplicacao-para-o-domain-criado)

---

## Ative sua conta

Ao se cadastrar na Azion você receberá um email para ativação de sua conta. 
Nesse email você encontrará as instruções para confirmar seu endereço eletrônico e gerar sua senha. Seu endereço eletrônico será utilizado como usuário de acesso ao painel de controle web da Azion, o [Real-Time Manager](https://manager.azion.com/), onde você poderá gerenciar as configurações de sua conta e produtos.

Caso você não receba o email, por favor verifique sua pasta Spam.
O email deverá ser enviado com os seguintes cabeçalhos.

> From: noreply@azion.com
> 
> Subject: Please Verify Your Azion Account

---

## Crie um novo Edge Application

Após a ativação de sua conta, você deve criar seu primeiro edge application. Para criar uma nova configuração, execute os passos que seguem:

1. Acesse o [Real-Time Manager](https://manager.azion.com/) com o seu email e senha.
2. Preencha os campos solicitados e salve seu primeiro _edge application_.

Você precisa informar os campos que seguem.

#### Name for Application

Atribua um nome sugestivo para seu edge application. Este nome será utilizado para identificar sua configuração. Você pode utilizar o próprio domínio de sua aplicação web como nome.

_Ex.: www.azion.com_

#### Main Settings

Nesta seção são definidos os principais campos relacionados a entrega de suas aplicações.

| Campo | Descrição | 
|:--------|:-------:|
| **Delivery Protocol** | Escolha o protocolo de entrega suportado por sua aplicação web: * _HTTP_ caso sua aplicação suporte apenas o protocolo HTTP. * _HTTP_ & _HTTPS_ caso sua aplicacão suporte ambos protocolos HTTP e HTTPS. Para utilizar HTTPS, você precisará de um [Digital Certificates]({% tl documentation_products_edge_applications_digital_certificates %}) | 

#### Origins

Em Origins são definidos os dados de sua a origem. Para entender mais sobre como funciona o Edge Applications, para que serve a origem ou como realizar configurações mais avançadas de origem, consulte a documentação técnica do produto.

| Campo | Descrição | 
|:--------|:-------:|
| **Origin Type** | Escolha o tipo de origem: _Single Origin:_ se a Azion deve se conectar a uma origem externa para buscar os dados que não estiverem em cache. _Cloud Storage:_ se a Azion deve se conectar ao Azion Cloud Storage para buscar objetos armazenados por você.  _Media Packager:_ se a Azion deve se conectar ao Azion Media Packager para entregar via HLS suas mídias (audio e video) armazenadas na Azion. Os campos que seguem se referem a origem do tipo Single Origin.|   
| **Address** | Defina o endereço de origem de sua aplicação, no formato FQDN (Full Qualified Domain Name), por exemplo origem.azion.com, ou endereço IP.Por padrão a Azion se conectará em sua origem pela porta 80, para HTTP, ou 443, para HTTPS. Se desejar configurar uma porta diferente de conexão com sua origem, você pode utilizar a notação host:port nesse campo, por exemplo origem.azion.com:8080. Consulte o campo abaixo para entender opções de conexão com sua origem.Você não pode configurar como origem o mesmo domínio de entrega de seu conteúdo. A origem deve possuir um endereço próprio. |
| **Origin Protocol Policy** | Na arquitetura de proxy reverso adotada pela Azion, seus usuários se conectam ao Intelligent Edge por HTTP ou HTTPS e você escolhe como deseja que a Azion se conecte em sua origem: **Preserve HTTP/HTTPS protocol:** irá manter o mesmo protocolo de conexão (HTTP ou HTTPS) e porta utilizados por seu usuário ao acessar seu conteúdo na Azion para se conectar em sua origem. **Enforce HTTP:** a conexão entre os Edge Servers da Azion e sua origem será por HTTP, independente do protocolo de conexão (HTTP ou HTTPS) e porta utilizados por seu usuário para acessar seu conteúdo na Azion. Com essa opção, você pode customizar uma porta para sua origem no campo Address diferente da porta default (80 para HTTP) se desejar. **Enforce HTTPS:** a conexão entre os Edge Servers da Azion e sua origem será por HTTPS, independente do protocolo de conexão (HTTP ou HTTPS) e porta utilizados por seu usuário para acessar seu conteúdo na Azion. Com essa opção, você pode customizar uma porta para sua origem no campo Address diferente da porta default (443 para HTTPS) se desejar. |
| **Host Header** | O cabeçalho Host é utilizado por sua origem para identificar o _virtualhost_ e localizar seu conteúdo ou aplicação. Ao configurar uma origem no Real-Time Manager, você pode customizar a valor que deve ser enviado pela Azion no cabeçalho Host.Utilize o valor _${host}_, no campo Host Header, caso sua origem esteja configurada para responder o _virtualhost_ pelo mesmo domínio que é utilizado por seus usuários para acessar seu conteúdo na Azion. Dessa forma, você estará instruindo os edge serveres a repassarem para sua origem o mesmo cabeçalho Host que for recebido de seus visitantes. Se necessário, você pode preencher um valor customizado de Host Header para ser enviado para sua origem. Por exemplo, _origin.domain.com_. Você deve customizar o Host Header se sua origem estiver configurada para responder um _virtualhost_ em um domínio diferente do que é utilizado por seus usuários. | 

#### Cache Settings

Nesta seção serão definidas as opções de cache para seu conteúdo. Há dois tipos de cache:

* **Browser Cache** é o cache de seu conteúdo armazenado no browser de seus usuários. Você pode definir tempo de vida (_time-to-live_, TTL) para cada conteúdo, mas terá pouca autonomia para forçar a expiração do conteúdo antes do tempo definido como TTL, caso haja necessidade de alterar o conteúdo antes do tempo.
* **CDN Cache** é o cache de seu conteúdo nos Edge Servers da Azion. Além de poder definir o TTL para cada tipo de conteúdo, você poderá executar, em tempo real, a operação de [Purge]({% tl documentation_products_edge_applications_real_time_purge %}) do conteúdo, sempre que houver necessidade de eliminar os dados armazenados no cache.

| Campo | Descrição | 
|:--------|:-------:|
| **Browser Cache Settings** |Utilize a opção _Honor Origin Cache Headers_ se desejar que a Azion envie para seus usuários os mesmos cabeçalhos de controle de cache recebidos de sua origem. Você também pode customizar o controle de Browser Cache selecionando a opção _Override Cache Settings_. Nesse caso, você deverá definir um **Maximum TTL**, que é o tempo de vida (em segundos) máximo que o conteúdo poderá ficar em cache no browser de seus usuários. |
| **CDN Cache Settings** | Utilize a opção _Honor Origin Cache Headers_ se desejar que a Azion respeite os cabeçalhos de controle de cache recebidos de sua origem, para gestão do cache nos Edge Servers da Azion. Você também pode customizar o controle de CDN Cache selecionando a opção _Override Cache Settings_. Nesse caso, você deverá definir um **Maximum TTL**, que é o tempo de vida (em segundos) máximo que o conteúdo poderá ficar em cache nos Edge Servers da Azion. Você poderá, a qualquer momento, executar a Purge do conteúdo em tempo real. |

Não se esqueca de salvar sua configuração clicando no botão **Save**.


 > Se desejar, você pode editar seu edge application recém criado para opções mais avançadas.


---

## Crie um novo Domain associado ao seu Edge Application

Após a criação de seu primeiro edge application, você deve associar um ou mais domínios para acesso de seus usuários:

1. Acesse o [Real-Time Manager](https://manager.azion.com/) com o seu email e senha.
2. Clique no menu > Edge Services > Domains.
3. Clique no botão Add Domain.
4. Preencha os campos solicitados e salve sua configuração.

Você precisa informar os campos que seguem.

**Add Name Configuration**

Atribua um nome sugestivo para seu edge application. Este nome será utilizado para identificar sua configuração. Você pode utilizar o próprio domínio de sua aplicação web como nome.

_Ex.: www.azion.com_

**Settings**

Nesta seção são definidos os principais campos relacionados a entrega de suas aplicações.

| Campo | Descrição | 
|:--------|:-------:|
| **Digital Certificate** | Se você tiver selecionado _HTTP & HTTPS_ durante a criação de seu edge application, deverá selecionar o certificado SSL que será utilizado para criptografar o seu tráfego HTTPS. A Azion disponibiliza o certificado _Azion (SAN)_ que pode ser utilizado para os domínios abaixo de _azioncdn.net_. Você também poderá realizar o upload de seu Custom Certificate a qualquer momento. Consulte a [documentação técnica]({% tl documentation_products_edge_applications_digital_certificates %}#custom-certificate) sobre como proceder. |
| **CNAMEs** | Configure a lista de domínios (CNAMEs) de entrega do seu conteúdo ou aplicação. Se necessário, você pode utilizar Wildcard Domain (_*.yourdomain.com_). _Ex.: www.azion.com_ |
| **CNAME Access Only** | Por default, todas as configurações de Content Delivery recebem automaticamente um nome de domínio abaixo de _azioncdn.net_. Ao marcar esta opção, você estará configurando o Content Delivery para entregar seu conteúdo ou aplicações apenas pelos domínios listados no campo CNAME. |               
| **Edge Application** | Nesse campo você seleciona o edge application que deseja associar a este domínio de entrega. |           

---

## Altere o DNS de sua aplicação para o Domain criado

Após associar um Domain ao seu Edge Application, você irá visualizar a listagem de configurações existentes em sua conta.

Para cada configuração criada é atribuído automaticamente um **Domain Name** abaixo do domínio _*.ha.azioncdn.net_.

Você precisará desse domínio para homologar o funcionamento de sua nova configuração. Para colocar sua configuração em produção, você terá que realizar o apontamento do domínio de seu conteúdo para o Domain Name atribuído à sua configuração, através de um registro do tipo CNAME em seu servidor de DNS.


> Você deve homologar atentamente seu conteúdo e aplicação web antes de realizar o apontamento de DNS para o Domain Name da Azion.


---

Para continuar aprendendo sobre os produtos da Azion, consulte o menu de navegação na lateral esquerda e na cabeceira, ou realize uma busca utilizando as palavras-chave na página inicial do [Azion for Developers]({% tl documentation %}).

---

Não encontrou o que procurava? [Abra um ticket.](https://tickets.azion.com/)