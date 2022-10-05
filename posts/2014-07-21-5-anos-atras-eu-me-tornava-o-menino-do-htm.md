---
title.pt: "CSS Modular com Mobile First-02"
title.en: "CSS Modular with Mobile First-02"
date: 2014-03-10 00:00:01
description.pt: "📚📚Mobile First vai muito além de código, é um pensamento que precisa existir desde o inicio do projeto. Mas nesse artigo vou abordar apenas codificação para tentar deixar o workflow mais agradável"
description.en: "📚📚Mobile First goes far beyond code, it's a thought that needs to exist from the beginning of the project. But in this article I will only cover coding to try to make the workflow more pleasant"
tags: ["css", "javascript", "php"]
---

02A importância de um CSS modularizado e o Atomic Design foi muito difundido nos últimos tempos, eu mesmo já escrevi um [artigo sobre o assunto](/blog/um-conto-sobre-componentizacao-e-quebra-de-paradigmas). Mas algo ainda me incomodava ao aplicar First Mobile em conjunto com CSS modular... os Media Queries.

## O uso tradicional

<iframe width="650" height="400" src="https://www.youtube.com/embed/L78ENSEHXLE" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

Imagino que a maneira na qual os Media Queries são mais utilizados é adicionando as condicionais no fim do CSS, algo como:

```css
@media (max-width: 767px) {
  ...
}
```

<iframe width="650" height="400" src="https://www.youtube.com/embed/9XaS93WMRQQ" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>


Um dos principais motivos para eu utilizar dessa forma, era nosso bom (só que não) e velho amigo IE8\. Ainda forneço suporte mínimo para esse navegador e como ele não aceita Media Queries, eu desenvolvia a versão mais "básica" para desktop, e ia "limpando" conforme a resolução.

Cheguei a pesquisar plugins que ajudariam a contornar esse problema, mas na época não encontrei nada que funcionasse ou me agradasse plenamente.

## Novos tempos

Mês passado iniciei um novo projeto, e adicionar Media Queries no final do CSS já não me deixava confortável mais.

A explicação é simples. Imaginem um componente, é de se esperar que toda a funcionalidade atrelada a ele esteja dentro do seu próprio 'include' (para quem usa pré-processadores). Mas a partir do momento que era necessário "ajustar" o funcionamento dele para outras resoluções no 'include' do media querie, as coisas ficavam esquisitas e eu me sentia desconfortável.

Lembrei então que o [Bootstrap 3](http://getbootstrap.com) já estava trabalhando de uma maneira muito próxima da que eu considerava ideal, e fornecia com a ajuda de plugins, suporte para o IE8\. Então conheci o [Respond.js](https://github.com/scottjehl/Respond) e todos meus problemas com o IE8 se resolveram.

## Modern Workflow...

Não tem segredo. Simplesmente adiciono os Media Queries em sequencia da classe que desejo alterar. Caso use algum pré-processador, isso será ainda mais simples, porque você pode deixar tudo organizado. Usando o LESS como exemplo:

```css
.navbar {
  margin-top: 20px;
  @media (min-width: @screen-sm-min) {
    float: left;
    width: 25%;
  }
  @media (min-width: @screen-lg-min) {
    position: fixed;
    top: 40px; left: 20px;
  }
}
```
<iframe width="650" height="400" src="https://www.youtube.com/embed/yo3B_xHVEqM" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

![340x500](https://m.media-amazon.com/images/I/61ih6raIX9S._AC_SX569_.jpg)
![340x500](https://images.unsplash.com/photo-1649525926154-992ad78a537b?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=869&q=80)
![340x500](https://images.unsplash.com/photo-1649575207563-0314a0cd0398?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=580&q=80)
![340x500](https://images.unsplash.com/photo-1649578474199-59d8f6d4c03e?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=872&q=80)
![340x500](https://images.unsplash.com/photo-1649579035859-cf6c798b0bbf?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=870&q=80)
![340x500](https://images.unsplash.com/photo-1649510165975-dfb63de055a9?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=387&q=80)
Isso vai gerar:

```css
.navbar {
  margin-top: 20px;
}
@media (min-width: 768px) {
  .navbar {
    float: left;
    width: 25%;
  }
}
@media (min-width: 1200px) {
  .navbar {
    position: fixed;
    top: 40px;
    left: 20px;
  }
}
```

```php
protected function blockCodeContinue($Line, $Block)
    {
        if ($Line['indent'] >= 4)
        {
            if (isset($Block['interrupted']))
            {
                $Block['element']['element']['text'] .= str_repeat("\n", $Block['interrupted']);

                unset($Block['interrupted']);
            }

            $Block['element']['element']['text'] .= "\n";

            $text = substr($Line['body'], 4);

            $Block['element']['element']['text'] .= $text;

            return $Block;
        }
    }
```

```javascript 
var data;
var qnt;
var currentPage = 1;
var pageItems = 8;
function init(file) {
	var request = new XMLHttpRequest();
	request.open('GET', file, true);
	request.send(null);
	request.addEventListener("readystatechange", function() {
		if (this.readyState === 4) {
			data = JSON.parse(this.responseText);
			qnt = Object.keys(data['main']).length;
														
			var getPage = parseInt((window.location.href.match(/([^\/]*)\/*$/)[1]));
			if ((getPage < 1) || (getPage > Math.ceil(qnt/pageItems)) || !getPage) {
				setPage(currentPage);
				history.pushState({}, "", window.location.protocol + "//" + window.location.hostname + "/blog/");
			} else {
				setPage(getPage);
				currentPage = getPage;
			}
		}
	});
};
init('/main.json?z=' + Math.random());
```

Dessa forma conseguimos trabalhar com Mobile First de um jeito realmente interessante, e tudo flui muito naturalmente. Setamos primeiro as propriedades que são comuns para todas as resoluções e _progressivamente_ vamos adicionando as funcionalidades para resoluções maiores.

E além de tudo, os componentes vão ter todas as propriedades deles dentro do próprio 'include'. Caso queira adicionar ou remover determinado componente, não precisa se preocupar em alterar os Media Queries separados para ajustar o projeto.

## Plus: Os imprescindíveis automatizadores

E claro... nossos melhores amigos [Grunt](http://gruntjs.com) ou [Gulp](http://gulpjs.com) vão melhorar ainda mais esse processo.

Existe um pequeno problema quando usamos os Media Queries dessa maneira... código desnecessário. Vamos ter milhares de Media Queries repetidos espalhados pelo projeto.

A boa notícia é que tanto o Grunt quanto o Gulp tem um plugin que resolve esse problema (indicação do [Nícolas Rossett](https://www.facebook.com/nicolas.rossett)): [grunt-combine-media-queries](https://github.com/buildingblocks/grunt-combine-media-queries) ou [gulp-combine-media-queries](https://github.com/konitter/gulp-combine-media-queries).

Esse ótimo plugin vai pegar todos os Media Queries espalhados pelo CSS e juntar tudo no final conforme a resolução. Exatamente da maneira que você sempre fez.

## Conclusão

Quero deixar claro que essa é uma preferência pessoal de uso dos Media Queries, caso não se sinta confortável para trabalhar dessa forma, nada impede que continue usando da maneira tradicional, o importante é estar sempre seguro dentro do seu próprio workflow.

Abraços e até a próxima ;)

%%english-lang-block%%

The importance of modularized CSS and Atomic Design has been widespread in recent times, I myself have written an [article on the subject](/blog/a-tale-about-componentization-and-paradigm-breaking). But something still bothered me when applying First Mobile in conjunction with modular CSS... the Media Queries.

## The traditional usage

I imagine the way in which Media Queries are most used is by adding conditionals at the end of the CSS, something like:

%%code-block%%

One of the main reasons I used it this way was our good (but not) old friend IE8\. I still provide minimal support for this browser and as it doesn't support Media Queries, I developed the most "basic" desktop version, and "cleaned" it according to the resolution.

I even researched plugins that would help get around this problem, but at the time I didn't find anything that worked or fully pleased me.

## New Times


<iframe width="650" height="400" src="https://www.youtube.com/embed/L78ENSEHXLE" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

Last month I started a new project, and adding Media Queries at the end of the CSS didn't make me comfortable anymore.

The explanation is simple. Imagine a component, it is to be expected that all the functionality linked to it is inside its own 'include' (for those who use preprocessors). But from the moment it was necessary to "adjust" its functioning to other resolutions in the 'include' of the media querie, things got weird and I felt uncomfortable.

I then remembered that [Bootstrap 3](http://getbootstrap.com) was already working very close to what I considered ideal, and provided with the help of plugins, support for IE8\. Then I found [Respond.js](https://github.com/scottjehl/Respond) and all my problems with IE8 were solved.

## Modern Workflow...

There's no secret. I simply add the Media Queries in sequence of the class I want to change. If you use a preprocessor, this will be even simpler, because you can keep everything organized. Using LESS as an example:

%%code-block%%

<iframe width="650" height="400" src="https://www.youtube.com/embed/9XaS93WMRQQ" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
<iframe width="650" height="400" src="https://www.youtube.com/embed/yo3B_xHVEqM" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

![340x500](https://m.media-amazon.com/images/I/61ih6raIX9S._AC_SX569_.jpg)
![340x500](https://images.unsplash.com/photo-1649525926154-992ad78a537b?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=869&q=80)
![340x500](https://images.unsplash.com/photo-1649575207563-0314a0cd0398?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=580&q=80)
![340x500](https://images.unsplash.com/photo-1649578474199-59d8f6d4c03e?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=872&q=80)
![340x500](https://images.unsplash.com/photo-1649579035859-cf6c798b0bbf?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=870&q=80)
![340x500](https://images.unsplash.com/photo-1649510165975-dfb63de055a9?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=387&q=80)
This will generate:

%%code-block%%

%%code-block%%

%%code-block%%

That way we were able to work with Mobile First in a really interesting way, and everything flows very naturally. We first set the properties that are common for all resolutions and _progressively_ we add the features for higher resolutions.

And on top of that, the components will have all their properties inside the 'include' itself. If you want to add or remove a certain component, you don't have to worry about changing separate Media Queries to fit the project.

## Plus: The Essential Automators

And of course... our best friends [Grunt](http://gruntjs.com) or [Gulp](http://gulpjs.com) will improve this process even further.

There is a small problem when using Media Queries in this way... unnecessary code. We will have thousands of repeated Media Queries scattered throughout the project.

The good news is that both Grunt and Gulp have a plugin that solves this problem (indicated by [Nícolas Rossett](https://www.facebook.com/nicolas.rossett)): [grunt-combine-media-queries ](https://github.com/buildingblocks/grunt-combine-media-queries) or [gulp-combine-media-queries](https://github.com/konitter/gulp-combine-media-queries).

This great plugin will take all the Media Queries scattered around the CSS and put them together at the end according to the resolution. Exactly the way you always did.

## Conclusion

I want to make it clear that this is a personal preference for using Media Queries, if you don't feel comfortable working this way, nothing prevents you from continuing to use it in the traditional way, the important thing is to always be safe within your own workflow.

Hugs and see you soon ;)
