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

## Configurando banco de dados MySql usando Docker

## Referências
- https://docs.docker.com/get-started/overview/
- https://simplificandoredes.com/docker-instalacao/
- https://docs.docker.com/desktop/install/windows-install/
- https://simplificandoredes.com/docker-manipulacao-de-containers/
- https://docs.docker.com/get-started/02_our_app/
- https://docs.docker.com/get-started/04_sharing_app/
- https://jessicanathanyf.medium.com/configurando-um-banco-de-dados-no-mysql-usando-docker-5681bf8016dc
