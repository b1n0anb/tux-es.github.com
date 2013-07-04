---
layout: page
title: "Escrevendo posts para a comunidade"
comments: true
sharing: true
footer: true
---

O site Tux-ES utiliza o [Octopress](http://www.octopress.org) para gerenciar o conteúdo. Isso facilita a administração do site, pois conseguimos fazer um site bonito, bem estruturado e hospedado no gh-pages.

Preparando o ambiente para contribuição
----------------------------------------

O primeiro ponto a ser observado é que o Octopress é um sistema feito em Ruby, dessa forma, você precisa ter o Ruby 1.9.3 instalado em sua máquina de desenvolvimento. Para isso instale o [RVM](https://rvm.io/) e depois utilize-o para instalar o Ruby:

    $ curl -L https://get.rvm.io | bash -s stable --ruby
    $ rvm install 1.9.3
    $ rvm use 1.9.3
    $ rvm rubygems latest

Todo o site esta no repositório [tux-es.github.com](http://github.com/Tux-ES). Para escrever posts, você deve fazer um fork do repositório para o seu perfil do Github. Depois do fork feito, siga os passos abaixo:

    $ git clone git@github.com:SEU_USER/tux-es.github.com
    $ cd tux-es.github.com
    $ git checkout -b source --track origin/source
    $ sudo gem install bundler
    $ bundle install 

Agora vamos configurar o deploy _automágico_ das suas postagens para o seu repositório no Github. Basta digitar o comando abaixo e preencher as informações sobre o seu repositório:

    $ rake setup_github_pages

Ambiente configurado, vamos ao que interessa!

Escrevendo posts
-----------------

Para escrever posts no Octopress é muito simples, basta criar o post com o seguinte comando:

    $ rake new_post['O Título do seu post aqui']

Isso vai criar um arquivo em _source/_posts/YY-mm-dd-o-titulo-do-seu-post-aqui.markdown_ e é dentro dele que você vai colocar o conteúdo do seu post. Como você pode perceber, o nome do seu post é que vai ser usado para definir o slug da sua URL.

Ao abrir o arquivo do seu post, você verá o seguinte conteúdo:

    ---
    layout: post
    title: "O Título do seu post aqui"
    date: 2011-07-03 5:59
    comments: true
    external-url:
    categories:
    author:
    ---

Desses dados, é interessante comentar:

* __title:__ É onde vai ficar o título do seu post que será usado na tag _title_ da página
* __date:__ É a data e hora em que o post foi feito. Caso você não queira que isso apareça, basta remover
* __categories:__ A categoria em que se encaixa o post. Caso tenha mais de uma, basta passar uma lista [item1, item2, item3]
* __author:__ Nome do autor do post. Se não for passado ele pegará o autor padrão do arquivo de configuração.

E caso você esteja trabalhando em um rascunho, você pode inserir a opção __published: false__ que ele não será postado quando você gerar o conteúdo.

Para publicar o conteúdo do seu post no arquivo você deve usar a syntax markdown [Discount](http://tedwise.com/markdown/)

Pronto! Seu post esta feito, agora temos que publicá-lo!

Gerando o conteúdo e publicando no site
----------------------------------------

Na raiz do projeto, rode:

    $ rake generate

Isso irá gerar os seus posts no formato html e coloca-los na pasta _deploy. Logo em seguida:

    $ rake deploy

Isso irá enviar as mudanças para o seu repositório no Github, dentro do seu _branch master_

Agora, se você acessar o seu repositório _tux-ex.github.com_ irá ver que o branch master esta com as modificações que você acabou de enviar.

Para que esse conteúdo seja publicado de fato no site da Comunidade Tux-ES, faça um __Pull Request__ das suas modificações para o repositório oficial da comunidade.

Não se esqueça de commitar suas modificações no source!

    $ git add .
    $ git commit -m "Sua mensagem de commit"
    $ git push origin source

_That's all folks!_ _Let's Hack!_