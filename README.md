# Estudos Docker

## Resumo
Olá pessoal, tudo bem?
Meu nome é Iago Magalhães e estou criando este repositório para compartilhar, salvar e aprender sobre Docker.

## Introdução
<p>
    Apresentando uma visão mais geral do Docker, a própria documentação apresenta uma definição simples e direta.
</p>

    Docker é uma plataforma aberta para desenvolvimento, envio e execução de aplicativos. O Docker
    permite que você separe seus aplicativos de sua infraestrutura para que você possa entregar 
    software rapidamente. Com o Docker, você pode gerenciar sua infraestrutura da mesma 
    forma que gerencia seus aplicativos. Aproveitando as vantagens das metodologias do Docker
    para enviar, testar e implantar código rapidamente, você pode reduzir significativamente
    o atraso entre escrever código e executá-lo na produção.

<p>
    Esta plataforma utiliza container, mais o que é um container?
</p>

    De uma forma simplificada podemos pensar em um módulo que empacota dependências e aplicativos
    permitindo que estes sejam executados em diferentes ambientes. Nesse caso estamos descrevendo
    um pouco da teoria. Consequentemente, a imagem Docker contém todo o conjunto de ferramentas,
    bibliotecas e configurações necessárias para os aplicativos. - Juliana Mascarenhas

<p>
    Além disso, o seu uso no desenvolvimento de aplicações é incrível, no site Simplificando Redes, é possível encontrar um exemplo bem interessante e que resume e valida o uso do Docker.
</p>

    Vamos pegar um exemplo de um programador. Em seguida, vamos assumir que o programador está 
    fazendo uma aplicação em Python. Consequentemente, esse programador incluiu diversas bibliotecas 
    e preparou todo o ambiente para aquela aplicação. Agora, o programador pode gerar uma imagem Docker
    com todo o ambiente configurado. Dessa forma, se o programador desejar que outras pessoas tenham
    acesso a sua aplicação, pode simplesmente passar a imagem Docker correspondente.

<p>
    Container basicamente é a imagem do Docker em execução. Então, a partir do momento que você pega uma imagem Docker e executa, essa se transforma em um container.
</p>

<p>
    O container Docker trabalha de forma isolada e independente da infraestrutura. Dessa forma, esse isolamento do container proporciona resultados interessantes para atender a diferentes aplicações.
</p>

## Instalando Docker no Windows
<p>
    Nesse tópico, iremos instalar o Docker Desktop para Windows. Segundo a documentação oficial, temos 2 opções de instalação, sendo elas, a instalação interativa pelo instalador .exe e também pelo CLI. Primeiro veremos o passo a passo de instalação pelo modo interativo e depois através da linha de comando.
</p>

- Modo interativo de instalação <br>
    1. Baixe o instalador do Docker Desktop, disponível em: https://desktop.docker.com/win/main/amd64/Docker%20Desktop%20Installer.exe <br>
    2. Clique duas vezes em Docker Desktop Installer.exe para executar o instalador. <br>
    3. Quando solicitado, certifique-se de que a opção Usar WSL 2 em vez de Hyper-V na página de configuração esteja selecionada ou não, dependendo de sua escolha de back-end. (Se o seu sistema suportar apenas uma das duas opções, você não poderá selecionar qual back-end usar.) <br>
    4. Siga as instruções do assistente de instalação para autorizar o instalador e prosseguir com a instalação. <br>
    5. Quando a instalação for bem-sucedida, clique em Fechar para concluir o processo de instalação. <br>
    6. Se sua conta de administrador for diferente de sua conta de usuário, você deverá adicionar o usuário ao grupo docker-users . Execute o Gerenciamento do computador como administrador e navegue até Usuários e grupos locais > Grupos > docker-users . Clique com o botão direito do mouse para adicionar o usuário ao grupo. Saia e entre novamente para que as alterações entrem em vigor. <br>

- Modo CLI de instalação <br>
    1. Baixe o instalador do Docker Desktop, disponível em: https://desktop.docker.com/win/main/amd64/Docker%20Desktop%20Installer.exe <br>
    2. Abra o terminal do Windows <br>
    3. start /w "" "Docker Desktop Installer.exe" install <br>

## Manipulanção de containers
### Verificar as imagens Docker
<p>
    Inicialmente, vamos verificar as imagens que já temos.
</p>

    docker images

### Executar um container em background 
<p>
    Essa forma de execução de container é interessante quando queremos usar um container sem realizar uma interatividade direta com o container.
</p>

    docker run –td --name 'nome do container' 'imagem'

### Verificar consumo de recursos de container Docker
<p>
    Para verificar como está o consumo de recursos de um ou mais containers Docker.
</p>

    docker stats
    
### Execução em um container Docker
<p>
    Para executar um comando que nos permite acessar o container que está sendo executado em background e executar um Shell nesse container. 
</p>

     docker exec -it 'nome do container' sh

<p>
    Agora, estamos dentro do shell do container e podemos verificar o conteúdo do container usando o comando ls.
</p>

    ls

### Como finalizar um container Docker em background?
<p>
    Para finalizar um container em background, precisamos sair do terminal usando o comando exit. E em seguida, executar o comando abaixo.
</p>

    docker stop 'meu_containter'

### Executar um comando em um container Docker
<p>
    Podemos executar o comando diretamente no container sem a necessidade de acessar o container.
    Para isso, podemos usar como exemplo a necessidade de executar o comando netstat dentro de um container sem a necessidade de acessar o terminal desse container.
</p>

    docker exec -it 'meu container' netstat -rn

### Salvar alterações em um container Docker
<p>
    O Docker tem uma função muito importante que permite salvar as alterações, como instalação de programas e configurações, que forma feitas em um container.
    Dessa forma, podemos gerar uma imagem do container Docker e garantir que nossas instalações e alterações estejam na imagem Docker. 
</p>

    docker exec -it 'meu container' sh

<p>
    Para salvar o container em uma imagem. 
</p>

    docker commit 'meu container' 'nome da imagem'

<p>
    Podemos verificar que agora temos uma nova imagem. Para isso vamos usar o comando abaixo.
</p>

    docker images

### Executando um container com a nossa imagem Docker
<p>
    Agora vamos executar um novo container que vai usar a imagem que criamos anteriormente.
    Dessa forma, poderemos verificar se as alterações que foram criadas na imagem estão dentro do novo container.
</p>

    docker run -it --name 'novo_container' 'nome da imagem'

## Conteinerizar um aplicativo
<p>
    Agora iremos criar um container para nossa aplicação seguindo a documentação do próprio Docker. No site oficial, o exemplo apresentado é utilizado com Node JS. Seguimos o passo a passo abaixo:
</p>

1. Crie a imagem do contêiner do aplicativo
<p>
    Para criar a imagem do contêiner , você precisará usar um arquivo Dockerfile. Um Dockerfile é simplesmente um arquivo baseado em texto sem extensão de arquivo que contém um script de instruções. O Docker usa esse script para criar uma imagem de contêiner.
</p>
1. No diretório da aplicação, crie um arquivo chamado Dockerfile. Você pode usar os seguintes comandos abaixo para criar um Dockerfile com base em seu sistema operacional.
No prompt de comando do Windows, execute os seguintes comandos listados abaixo.
Altere o diretório para o appdiretório. Substitua \path\to\apppelo caminho para o seu getting-started\appdiretório.
    
        cd \path\to\app
        
Crie um arquivo vazio chamado Dockerfile.
    
        type nul > Dockerfile

2. Usando um editor de texto ou editor de código, adicione o seguinte conteúdo ao Dockerfile:
        
        # syntax=docker/dockerfile:1
        FROM node:18-alpine
        WORKDIR /app
        COPY . .
        RUN yarn install --production
        CMD ["node", "src/index.js"]
        EXPOSE 3000
        
3. Crie a imagem do contêiner usando os seguintes comandos:
<p>
No terminal, altere o diretório para o getting-started/appdiretório. Substitua /path/to/apppelo caminho para o seu getting-started/appdiretório.
</p>

    cd /path/to/app

<p>
    Crie a imagem do contêiner.
</p>

    docker build -t getting-started

<p>
O docker buildcomando usa o Dockerfile para criar uma nova imagem de contêiner. Você deve ter notado que o Docker baixou muitas “camadas”. Isso ocorre porque você instruiu o construtor que deseja iniciar a partir da node:18-alpineimagem. Mas, como você não tinha isso em sua máquina, o Docker precisou baixar a imagem.

Depois que o Docker baixou a imagem, as instruções do Dockerfile foram copiadas em seu aplicativo e usadas yarnpara instalar as dependências de seu aplicativo. A CMDdiretiva especifica o comando padrão a ser executado ao iniciar um contêiner a partir desta imagem.

Por fim, a -tbandeira marca sua imagem. Pense nisso simplesmente como um nome legível para a imagem final. Como você nomeou a imagem getting-started, pode se referir a essa imagem ao executar um contêiner.

O .no final do docker buildcomando informa ao Docker que ele deve procurar Dockerfileno diretório atual.
</p>

2. Iniciar um contêiner de aplicativo
<p>
Agora que você tem uma imagem, pode executar o aplicativo em um contêiner . Para fazer isso, você usará o docker runcomando.
</p>

1. Inicie seu contêiner usando o docker runcomando e especifique o nome da imagem que você acabou de criar:
    
    docker run -dp 3000:3000 getting-started
    
<p>
    Você usa o -dsinalizador para executar o novo contêiner no modo “separado” (em segundo plano). Você também usa o -psinalizador para criar um mapeamento entre a porta 3000 do host e a porta 3000 do contêiner. Sem o mapeamento de porta, você não conseguiria acessar o aplicativo.
</p>

## Compartilhe o aplicativo
<p>
Agora que a imagem de uma aplicação foi criada é hora de compartilhar com a comunidade.
Para compartilhar imagens do Docker, você precisa usar um registro do Docker. O registro padrão é o Docker Hub e é de onde vieram todas as imagens que você usou.
</p>

1. Criar um repositório <br>
<p>
Para enviar uma imagem, primeiro você precisa criar um repositório no Docker Hub. <br>
</p>
    i. Inscreva-se ou entre no Docker Hub. <br>
    ii. Selecione o botão Criar repositório. <br>
    iii. Para o nome do repositório, use getting-started. Certifique-se de que a visibilidade é Public. <br>
    iv. Selecione o botão Criar. <br>
    
![image](https://github.com/IagoMagalhaes23/Estudos-Docker/assets/65053026/479b029e-9f0b-40f8-8f34-a0369c4dcb04) <br>

2. Enviar a imagem <br>
    i. Na linha de comando, tente executar o comando push que você vê no Docker Hub. Observe que seu comando estará usando seu namespace, não “docker”. <br>
    
        docker push docker/getting-started
        The push refers to repository [docker.io/docker/getting-started]
        An image does not exist locally with the tag: docker/getting-started
    
<p>
Por que falhou? O comando push estava procurando por uma imagem chamada docker/getting-started, mas não encontrou nenhuma. Se você executar docker image ls, também não verá nenhum. <br>
</p>
<p>
Para corrigir isso, você precisa “marcar” sua imagem existente que você criou para dar outro nome a ela. <br>
</p>
    ii. Faça login no Docker Hub usando o comando docker login -u YOUR-USER-NAME. <br>
    iii. Use o docker tagcomando para dar getting-startedum novo nome à imagem. Certifique-se de trocar YOUR-USER-NAMEcom seu Docker ID. <br>
    
    docker tag getting-started YOUR-USER-NAME/getting-started
    
   iv. Agora tente seu comando push novamente. Se você estiver copiando o valor do Docker Hub, poderá descartar a tagnameparte, pois não adicionou uma tag ao nome da imagem. Se você não especificar uma tag, o Docker usará uma tag chamada latest. <br>
    
    docker push YOUR-USER-NAME/getting-started
    
3. Execute a imagem em uma nova instância <br>
<p>
Agora que sua imagem foi criada e enviada para um registro, tente executar seu aplicativo em uma nova instância que nunca viu essa imagem de contêiner. Para fazer isso, você usará o Play with Docker. <br>
</p>
i. Abra seu navegador para jogar com o Docker . <br>
ii. Selecione Login e, em seguida, selecione janela de encaixe na lista suspensa. <br>
iii. Conecte-se com sua conta do Docker Hub. <br>
iv. Depois de fazer login, selecione a opção ADICIONAR NOVA INSTÂNCIA na barra lateral esquerda. Se você não vê-lo, deixe seu navegador um pouco mais largo. Após alguns segundos, uma janela de terminal é aberta em seu navegador. <br>

![image](https://github.com/IagoMagalhaes23/Estudos-Docker/assets/65053026/62a22eb3-ffa3-4b04-91e8-e162ea149ed4) <br>

v. No terminal, inicie seu aplicativo recém-enviado. <br>
     docker run -dp 3000:3000 YOUR-USER-NAME/getting-started
Você deve ver a imagem ser puxada para baixo e, eventualmente, inicializada. <br>
vi. Selecione o emblema 3000 quando aparecer e você verá o aplicativo com suas modificações. Se o emblema 3000 não aparecer, você pode selecionar o botão Open Port e digitar 3000. <br>

## Usar Docker Compose

### Usar Docker Compose
<p>
O Docker Compose é uma ferramenta desenvolvida para ajudar a definir e compartilhar aplicativos com vários contêineres. Com o Compose, podemos criar um arquivo YAML para definir os serviços e, com um único comando, podemos girar ou desmontar tudo.
</p>
<p>
A grande vantagem de usar o Compose é que você pode definir sua pilha de aplicativos em um arquivo, mantê-lo na raiz do repositório do seu projeto (agora com controle de versão) e permitir facilmente que outra pessoa contribua com seu projeto. Alguém só precisaria clonar seu repositório e iniciar o aplicativo de composição. Na verdade, você pode ver alguns projetos no GitHub/GitLab fazendo exatamente isso agora.
</p>

### Instale o Docker Compose
<p>
Se você instalou o Docker Desktop para Windows, Mac ou Linux, você já tem o Docker Compose! As instâncias do Play-with-Docker também têm o Docker Compose instalado.
</p>
<p>
As instalações autônomas do Docker Engine exigem que o Docker Compose seja instalado como um pacote separado, consulte Instalar o plug-in do Compose .
</p>
<p>
Após a instalação, você poderá executar o seguinte e ver as informações da versão.
</p>

    docker compose version

### Crie o arquivo Compose
1. Na raiz da '/getting-started/apppasta', crie um arquivo chamado 'docker-compose.yml'.
2. No arquivo de composição, começaremos definindo a lista de serviços (ou contêineres) que desejamos executar como parte de nosso aplicativo.
    
       services:

<p>
E agora, começaremos a migrar um serviço por vez para o arquivo de composição.
</p>

### Defina o serviço do app
<p>
Para lembrar, esse era o comando que estávamos usando para definir nosso contêiner de aplicativo.
</p>

      docker run -dp 3000:3000 \
      -w /app -v "$(pwd):/app" \
      --network todo-app \
      -e MYSQL_HOST=mysql \
      -e MYSQL_USER=root \
      -e MYSQL_PASSWORD=secret \
      -e MYSQL_DB=todos \
      node:18-alpine \
      sh -c "yarn install && yarn run dev"

1. Primeiro, vamos definir a entrada de serviço e a imagem do container. Podemos escolher qualquer nome para o serviço. O nome se tornará automaticamente um alias de rede, o que será útil ao definir nosso serviço MySQL.
        
        services:
          app:
            image: node:18-alpine

2. Normalmente, você verá o commandfechamento da imagedefinição, embora não haja nenhum requisito no pedido. Então, vamos em frente e mover isso para o nosso arquivo.

        services:
          app:
            image: node:18-alpine
            command: sh -c "yarn install && yarn run dev"

3. Vamos migrar a -p 3000:3000parte do comando definindo o portspara o serviço. Usaremos a sintaxe curta aqui, mas também há uma sintaxe longa mais detalhada disponível.

        services:
          app:
            image: node:18-alpine
            command: sh -c "yarn install && yarn run dev"
            ports:
              - 3000:3000

4. Em seguida, migraremos o diretório de trabalho ( -w /app) e o mapeamento de volume ( -v "$(pwd):/app") usando as definições working_dire . volumesVolumes também tem uma sintaxe curta e longa.
Uma vantagem das definições de volume do Docker Compose é que podemos usar caminhos relativos do diretório atual.

        services:
          app:
            image: node:18-alpine
            command: sh -c "yarn install && yarn run dev"
            ports:
              - 3000:3000
            working_dir: /app
            volumes:
              - ./:/app

5. Por fim, precisamos migrar as definições de variáveis de ambiente usando a 'environment' chave.

        services:
          app:
            image: node:18-alpine
            command: sh -c "yarn install && yarn run dev"
            ports:
              - 3000:3000
            working_dir: /app
            volumes:
              - ./:/app
            environment:
              MYSQL_HOST: mysql
              MYSQL_USER: root
              MYSQL_PASSWORD: secret
              MYSQL_DB: todos

#### Defina o serviço MySQL
<p>
Agora, é hora de definir o serviço MySQL. O comando que usamos para esse container foi o seguinte:
</p>

      docker run -d \
      --network todo-app --network-alias mysql \
      -v todo-mysql-data:/var/lib/mysql \
      -e MYSQL_ROOT_PASSWORD=secret \
      -e MYSQL_DATABASE=todos \
      mysql:8.0

1. Vamos primeiro definir o novo serviço e nomeá-lo mysqlpara que ele obtenha automaticamente o alias de rede. Iremos em frente e especificaremos a imagem a ser usada também.

        services:
          app:
            # The app service definition
          mysql:
            image: mysql:8.0

2. Em seguida, definiremos o mapeamento de volume. Quando executamos o contêiner com docker run, o volume nomeado foi criado automaticamente. No entanto, isso não acontece ao executar com o Compose. Precisamos definir o volume na volumes:seção de nível superior e especificar o ponto de montagem na configuração do serviço. Simplesmente fornecendo apenas o nome do volume, as opções padrão são usadas. Há muito mais opções disponíveis embora.

        services:
          app:
            # The app service definition
          mysql:
            image: mysql:8.0
            volumes:
              - todo-mysql-data:/var/lib/mysql

        volumes:
          todo-mysql-data:

3. Por fim, precisamos apenas especificar as variáveis ​​de ambiente.

        services:
          app:
            # The app service definition
          mysql:
            image: mysql:8.0
            volumes:
              - todo-mysql-data:/var/lib/mysql
            environment:
              MYSQL_ROOT_PASSWORD: secret
              MYSQL_DATABASE: todos

        volumes:
          todo-mysql-data:

<p>
Neste ponto, nosso complete docker-compose.ymldeve ficar assim:
</p>

    services:
      app:
        image: node:18-alpine
        command: sh -c "yarn install && yarn run dev"
        ports:
          - 3000:3000
        working_dir: /app
        volumes:
          - ./:/app
        environment:
          MYSQL_HOST: mysql
          MYSQL_USER: root
          MYSQL_PASSWORD: secret
          MYSQL_DB: todos

      mysql:
        image: mysql:8.0
        volumes:
          - todo-mysql-data:/var/lib/mysql
        environment:
          MYSQL_ROOT_PASSWORD: secret
          MYSQL_DATABASE: todos

    volumes:
      todo-mysql-data:

### Execute a pilha de aplicativos
<p>
Agora que temos nosso docker-compose.ymlarquivo, podemos iniciá-lo!
</p>

1. Certifique-se de que nenhuma outra cópia do app/db esteja sendo executada primeiro ( 'docker ps' e 'docker rm -f <ids>').

2. Inicie a pilha de aplicativos usando o docker compose upcomando. Adicionaremos o -dsinalizador para executar tudo em segundo plano.
    
        docker compose up -d

<p>
Quando executamos isso, devemos ver uma saída como esta:
</p>

         Creating network "app_default" with the default driver
         Creating volume "app_todo-mysql-data" with default driver
         Creating app_app_1   ... done
         Creating app_mysql_1 ... done

<p>
Você notará que o volume foi criado, assim como uma rede! Por padrão, o Docker Compose cria automaticamente uma rede especificamente para a pilha de aplicativos (é por isso que não definimos uma no arquivo de composição).
</p>

3. Vamos ver os logs usando o docker compose logs -fcomando. Você verá os logs de cada um dos serviços intercalados em um único fluxo. Isso é incrivelmente útil quando você deseja observar problemas relacionados ao tempo. O -f sinalizador “segue” o log, portanto, fornecerá uma saída ao vivo à medida que for gerado.
<p>
Se você já executou o comando, verá uma saída semelhante a esta:
</p>

         mysql_1  | 2019-10-03T03:07:16.083639Z 0 [Note] mysqld: ready for connections.
         mysql_1  | Version: '8.0.31'  socket: '/var/run/mysqld/mysqld.sock'  port: 3306  MySQL Community Server (GPL)
         app_1    | Connected to mysql db at host mysql
         app_1    | Listening on port 3000

<p>
O nome do serviço é exibido no início da linha (geralmente colorido) para ajudar a distinguir as mensagens. Se você deseja visualizar os logs de um serviço específico, pode adicionar o nome do serviço ao final do comando logs (por exemplo, docker compose logs -f app).
</p>

4. Neste ponto, você deve conseguir abrir seu aplicativo e vê-lo em execução. E ei! Estamos reduzidos a um único comando!

### Veja a pilha de aplicativos no Docker Dashboard
<p>
Se olharmos para o Docker Dashboard, veremos que existe um grupo chamado app . Este é o “nome do projeto” do Docker Compose e usado para agrupar os contêineres. Por padrão, o nome do projeto é simplesmente o nome do diretório no qual ele docker-compose.ymlestá localizado.
</p>
    
![image](https://github.com/IagoMagalhaes23/Estudos-Docker/assets/65053026/c0d9f9a2-3283-435f-b78d-ffd4f8460e61)

<p>
Se você clicar na seta de divulgação ao lado de app , verá os dois contêineres que definimos no arquivo de composição. Os nomes também são um pouco mais descritivos, pois seguem o padrão de <service-name>-<replica-number>. Portanto, é muito fácil ver rapidamente qual contêiner é nosso aplicativo e qual é o banco de dados mysql.
</p>
    
![image](https://github.com/IagoMagalhaes23/Estudos-Docker/assets/65053026/233215ca-818b-46dc-b299-72984bddf518)

### Derrube tudo
<p>
Quando estiver pronto para destruir tudo, basta executar 'docker compose down' ou ir para a lixeira no Docker Dashboard para o aplicativo inteiro. Os contêineres irão parar e a rede será removida.
</p>

    **Aviso**

    Removendo Volumes

    Por padrão, os volumes nomeados em seu arquivo de composição NÃO são removidos ao executar docker compose down. Se você deseja remover os volumes, precisará adicionar o --volumessinalizador.

    O Docker Dashboard não remove volumes quando você exclui a pilha de aplicativos.

<p>
Depois de demolido, você pode mudar para outro projeto, corra docker compose upe esteja pronto para contribuir com esse projeto! Realmente não fica muito mais simples do que isso!
</p>

## Configurando banco de dados MySql usando Docker
<p>
    Agora iremos congigurar um banco de dados MySql utilizando o docker.
</p>

- 1º Passo: Baixando a imagem MySQL
    <p>
        Vamos baixar a última imagem do MySQL no Docker hub
    </p>
        
        docker pull mysql/mysql-server
    
- 2º Passo: Executando container
    <p>
    Vamos executar um container a partir da imagem que acabamos de baixar. De início, não iremos configurar a configuração de ambiente, e vamos executar o MySQL com usuário padrão e sem senha. Antes de executar o comando, crie um diretório chamado de mysql . Digite o comando abaixo no seu terminal.
    </p>

    <p>
    Obs: crie a penas o diretório C:/mysql por padrão, o MySQL precisa ter as pastas /var/lib/mysql que é neste diretório que o MySQL irá salvar os dados do banco.
    </p>
    
        docker ryn -e MYSQL_ALLOW_EMPTY_PASSWORD=sim -v C:/mysql/var/lib/mysql mysql
    
- 3º Passo: Obtendo o IP do container
    <p>
    Para descobrir o IP do container digite docker container ls para verificar os containers que estão sendo executados e copie o ID do container mysql. Feito isso, digite o comando:
    </p>

        docker container inpect ID_CONTAINER.

    <p>
    Esse comando irá trazer todas as informações do container, e no final da tela você irá localizar o IPAddress do container.
    </p>
- 4º Passo: Acessando o banco através do container
    <p>
    Para acessar o banco MySQL através do container, precisamos entrar em dentro do container, e para isso, precisaremos digitar o comando abaixo:
    </p>
    
        docker exec -it ID_CONTAINER
    
    <p>
    Agora  é possível criar outros bancos, utilizando o comando 'create database seu_banco;'
    Utilize o comando 'use seu-banco;' para que acesse seu banco e consiga executar scripts para criar as tabelas e inserir os dados.
    </p>
## Referências
- https://docs.docker.com/get-started/overview/
- https://simplificandoredes.com/docker-instalacao/
- https://docs.docker.com/desktop/install/windows-install/
- https://simplificandoredes.com/docker-manipulacao-de-containers/
- https://docs.docker.com/get-started/02_our_app/
- https://docs.docker.com/get-started/04_sharing_app/
- https://docs.docker.com/get-started/08_using_compose/
- https://jessicanathanyf.medium.com/configurando-um-banco-de-dados-no-mysql-usando-docker-5681bf8016dc
