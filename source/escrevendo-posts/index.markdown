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

Todo o site esta no repositório [tux-es.github.com](http://github.com/Tux-ES). Para escrever posts, você deve:

1. Fazer um fork do repositório para o seu perfil do Github
2. Criar seu post
3. Subir seu post em uma branch separada
4. Fazer o pull request

Nós criamos um pequeno passo a passo que pode lhe ajudar, então vamos lá, o primeiro passo é fazer o fork, depois de feito execute:

    $ git clone git@github.com:SEU_USER/tux-es.github.com
    $ cd tux-es.github.com
    $ git remote add upstream git@github.com:Tux-ES/tux-es.github.com.git
    $ git fetch --all
    $ git checkout source && git rebase upstream/source # Em teoria esse procedimento não deve gerar qualquer conflito :)
    $ gem install bundler
    $ bundle install

Ambiente configurado, vamos ao que interessa!

Escrevendo posts
-----------------

Antes de escrever um post é importante criar uma branch para essa nova publicação, isso facilita na hora que formos aprovar seu pull request.

Então faça:

    $ git checkout source # apenas se não estiver na branch de nome source
    $ git rebase upstream/source
    $ git checkout meu-novo-post # Use aqui o nome que desejar

Para escrever posts no Octopress é muito simples, basta criar o post com o seguinte comando:

    $ rake new_post['O Título do seu post aqui']

Isso vai criar um arquivo em `source/_posts/YY-mm-dd-o-titulo-do-seu-post-aqui.markdown`, é dentro dele que você vai colocar o conteúdo do seu post. Como você pode perceber, o nome do seu post é que vai ser usado para definir o slug da sua URL.

Outro detalhe sobre é sobre o formato do arquivo. Os arquivos *devem* ser escritos em Markdown, entretanto o Octopress também permite o uso de HTML junto ao Markdown. Mas pedimos que só utilize HTML em último caso, com Markdown o código fica mais limpo e bonito.

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

E caso você esteja trabalhando em um rascunho, você pode inserir a opção `published: false` que ele não será postado quando você gerar o conteúdo.

Como já mencionamos, para escrever o conteúdo do seu post no arquivo você deve usar a syntax markdown [Discount](http://tedwise.com/markdown/)

Pronto! Seu post esta feito. Para ter uma visualização de como está ficando você pode rodar o comando `rake preview` na raiz do projeto e acessar pelo seu navegador pela url `http://localhost:4000/`.

Fazendo o Pull Request
----------------------

Este processo já é coberto pela documentação do GitHub, portanto a sugestão é que [visite o link descritivo desse processo](https://help.github.com/articles/fork-a-repo).

Assim que o pull request for feito nós receberemos uma notificação e entraremos em contato ;).

_That's all folks!_ _Let's Hack!_
