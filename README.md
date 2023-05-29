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

## Conteinerizar um aplicativo

## Compartilhe o aplicativo

## Usar Docker Compose

## Configurando banco de dados MySql usando Docker

## Referências
- https://docs.docker.com/get-started/overview/
- https://simplificandoredes.com/docker-instalacao/
- https://docs.docker.com/desktop/install/windows-install/
- https://jessicanathanyf.medium.com/configurando-um-banco-de-dados-no-mysql-usando-docker-5681bf8016dc
