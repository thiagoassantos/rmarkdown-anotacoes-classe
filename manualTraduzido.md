---
title: "Usando R Markdown para anotações de aula"
author: "Thiago de Araújo, Steven Dutt Ross"
date: "2 de setembro de 2017"
output: html_document
---

* Overview
* *Mark Up*, Markdown
* Renderização e Edição
    * Renderização no R Studio
    * Renderização no R sem usar o R Studio
    * Renderização via linha de comando (Unix-type sistemas)
* Formatação Básica em R Markdown
    * Quebra de Parágrafos e quebra forçada de linhas.
    * Cabeçalhos
    * Itálico, Negrito
    * Citações
    * Tipo de Computador
    * Listas não-ordenadas
    * Listas numeradas
    * Título, Autor, Data, Formato de Saída, Tabela de Conteúdos
* Hiperlinks e Imagens
    * Hiperlinks
    * Imagens
    * Includindo Código
    * Trechos de Código e seus Resultados
    * Código incorporado <!-- MENCIONAR O INLINE -->
    * Visto, mas não ouvido
    * Nomeando pedaços de código
    * Alterando Tamanho de Imagens e Alinhamentos
    * Tabelas
    * Pedaços de Código em Cache (rodando somente com mudanças)
    * Configuração de Padrões para todos os pedações de código
    * Mais opções
* Matemática no R Markdown
    * Elementos da Matemática <!-- Elements of Math Mode -->
    * Matemática para ```LaTeX```
    * ```LaTeX``` não verifica corretude
    * Mais recursos avançados de Matemática: Novos Comandos
    * Instalando ```LaTeX```
* Juntando tudo: Escrevendo seu Relatório em R Markdown
* Troubleshooting/O que evitar <!-- TRADUZIR TROUBLESHOOTING -->
* Leitura adicional
    * Agradecimentos
    
# Visão Geral

R Markdown é uma maneira muito simples de escrever relatórios, além de rodar seu código em R automaticamente.
Ele também permite que você use linguagem matemática, hiperlinks, imagens e outras formatações básicas. O objetivo deste documento é explicar, com exemplos, como usar seus recursos mais essenciais. Não é uma referência abrangente. (Para isso, veja: http://rmarkdown.rstudio.com)

Este guia pressupõe que você conheça, ao menos, um pouco de R.

Este guia está em http://www.stat.cmu.edu/~cshalizi/rmarkdown/rmarkdown.Rmd. Por favor, veja a versão mais recente. Correções e sugestões são bem-vindas.



# Mark Up, Markdown

Provavelmente Você esteja acostumado a usar programas de processamento de texto, como o Microsoft Word, que empregam o princípio do "o que você vê é o que você obtém" (WYSIWYG): você deseja que algumas palavras sejam impressas em itálico e, com um clique, logo estão em itálico lá na tela. Você quer que outras palavras tenham uma fonte maior e diferente, então você apenas seleciona a fonte e seu tamanho, e assim por diante. Isso funciona bem o suficiente para <del>n00bs</del> leigos, mas não é uma base viável para um sistema de formatação de texto, porque depende de um programa específico: (a) saber o que você quer dizer e (b) implementá-lo bem. Durante várias décadas, os sistemas realmente sérios de escrita basearam-se em um princípio muito diferente, o da marcação de texto. A idéia essencial em uma **linguagem de marcação** é que ela trabalha em texto comum, além de sinais que indicam como alterar a formatação ou o significado do texto. Algumas linguagens de marcação, como o HTML (Hyper-Text Markup Language), utilizam uma sintaxe muito técnica; outras, como o chamado **Markdown**, são mais sutis. Por exemplo, as frases anteriores no Markdown se parecem com isto:

```
Durante várias décadas, os sistemas realmente sérios de escrita basearam-se em um princípio muito diferente, o da marcação de texto. A idéia essencial em uma **linguagem de marcação** é que ela trabalha em texto comum, além de sinais que indicam como alterar a formatação ou o significado do texto. Algumas linguagens de marcação, como o HTML (Hyper-Text Markup Language), utilizam uma sintaxe muito técnica; outras, como o chamado **Markdown**, são mais sutis.
```
Cada linguagem de marcação é *renderizada* em um formato que inclui uma bela formatação, imagens, matemática, códigos, etc., etc., especificadas pela marcação. No caso do HTML, o programa de renderização é chamado de "web browser" (navegador web). A maioria dos computadores que interpretam o Markdown sabe como convertê-lo para HTML (visualizando o documento Markdown no navegador), PDF (visualizand o documento num leitor de PDF, como Acrobat ou outros), ou o Word (finalmente na abominação de Redmond).

As vantagens das linguagens de marcação são muitas: elas tendem a ser mais portáteis, menos custosas a empresas de software e mais estáveis ao longo do tempo do que os programas de processamento de texto WYSIWYG. R Markdown é gratuito (você nunca pagará um dólar para usá-lo) e livre (a documentação está completamente aberta a todos). Mesmo que você prefira o Word, a pura estabilidade das linguagens de marcação as torna superiores para documentos científicos.

[**Markdown**](http://daringfireball.net/projects/markdown/basics) é uma linguagem de marcação simples inventada por John Gruber. Hoje, existem muitos programas que traduzem documentos escritos em Markdown para documentos em formato HTML, PDF ou mesmo Word (entre outros). 
[**R Markdown**](http://rmarkdown.rstudio.com), por sua vez, é uma extensão do Markdown para incorporar código em execução, em R, incluindo o resultado no documento. O presente guia mostra, por sua vez, três aspectos do R Markdown: como incluir formatação básica; como incluir o código R e sua saída; e como incluir código matemático.


# Renderizando e Editando

Para escrever em R Markdown, você precisará de um editor de texto: programa que permite ler
e escreva arquivos de texto simples. Você também precisará do R e do pacote `rmarkdown`
(bem como todos os pacotes que dependem dele).

* A maioria dos computadores vem com um editor de texto (TextEdit no Mac, Notepad em máquinas Windows, etc.).
* Há também muitos outros editores mais robustos; Eu uso [Emacs](http://www.gnu.org/software/emacs/emacs.html), mas admito que tem uma curva de aprendizado áspera.
* Você _pode_ usar o Word (ou qualquer outro processador de texto WYSIWYG), tomando cuidado apenas de salvar o seu documento em formato de texto simples. Entretanto, eu não recomendo isso.
* [R Studio](http://www.rstudio.com) vem com um editor de textos próprio, apropriado, e com muitas ferramentas para se trabalhar com documentos R Markdown.

Se esta é sua primeira vez usando um editor de texto para algo sério, eu recomendo usar o R Studio.

### Renderizando no R Studio

Supondo que você tenha o documento R Markdown aberto no editor de texto,
clique no botão "knit".

### Renderizando no R sem usar o R Studio

Use o comando `render` no pacote `rmarkdown`.

### Renderizando via linha de comando (sistemas tipo Unix)

Se você preferir renderizar via linha de comando, o script Perl [`rmarkdown.pl`] (http://www.stat.cmu.edu/~cshalizi/rmarkdown/rmarkdown.pl)
Poderá fazer todo o trabalho. O uso é `rmarkdown.pl nome_do_arquivo`, e
resulta na saída `nome_do_arquivo.html` ou` nome_do_arquivo.pdf`, conforme especificado no
próprio arquivo. (Ver abaixo.)

# Formatação Básica em R Markdown

Na maior parte do documento, texto é apenas texto. Uma vantagem do R Markdown é que a
você digita seu documento como você normalmente faz.

### Quebra de Parágrafos e Quebra Forçada de Linhas

Para inserir uma quebra entre os paragráfos, inclua uma linha comum em branco.

Para forçar uma quebra de linha, ponha _dois_ espaços  
em branco ao final da linha.

```
Para inserir uma quebra entre os paragráfos, inclua uma linha comum em branco.

Para forçar uma quebra de linha, ponha _dois_ espaços  
em branco ao final da linha.
```

### Cabeçalhos

O caractere `#` no início de uma linha significa que o resto da linha será interpretado
como um cabeçalho de seção. O número de `#`s no começo da linha indica, respectivamente,
o número da seção, sub-seção, sub-sub-seção, etc. do documento. Por exemplo, o `Formatação Básica em R Markdown` acima é precedido por um único `#` mas o `Cabeçalhos` do começo deste
parágrafo foi precedido por `###`. Não separe cabeçalhos por quebra de linhas.

### Itálico, Negrito

Para deixar um texto em _itálico_ ele deve ficar dentro de um _único conjunto de underscores_ ou
*asteriscos*. Para usar **negrito**, coloque o texto dentro de um __duplo conjunto de underscores__ 
ou **asteriscos**.

```
Para deixar um texto em _itálico_ ele deve ficar dentro de um _único conjunto de underscores_ ou
*asteriscos*. Para usar **negrito**, coloque o texto dentro de um __duplo conjunto de underscores__ 
ou **asteriscos**.
```

### Citações

Para citar um texto, o parágrafo deve ser iniciado por `>` (sinal maior que):

> In fact, all epistemological value of the theory of probability is based on this: that large-scale random phenomena in their collective action create strict, nonrandom regularity.  [Gnedenko and Kolmogorov, _Limit Distributions for Sums of Independent Random Variables_, p. 1]

```
> In fact, all epistemological value of the theory of probability is based on this: that large-scale random phenomena in their collective action create strict, nonrandom regularity.  [Gnedenko and Kolmogorov, _Limit Distributions for Sums of Independent Random Variables_, p. 1]
```

### Fonte de console

Para imprimir um texto com fonte de largura fixa (estilo cOOOdigo-fonte), deve-se iniciAAA-lo e termina-lo com
um sinal de crase, sem quebras de linha no texto. (Por exemplo, `R` vs. R.) 
Se você quiser exibir várias linhas como um prOOOprio texto, insira três crases no comeCCCO e ao final do texto:

```
O texto a ser impresso em uma fonte de largura fixa, inicia e termina com
um sinal de crase, sem quebras de linha no texto. (Por exemplo, `R` vs. R.)
```

### Lista de Marcadoress

* Esta EEE uma lista de marcadores (lista nAAAo ordenada) onde os itens sAAAo marcos com pontos (bullets).
* Cada item da lista deve comeCCCar com um `*` (asterisco) ou um UUUnico hIIIfen (`-`).
* Cada item deve estar em uma nova linha.
    + Para sub-bullets, idente as linhas (recue AAA direita) e as inicie com `+`.
    + Sub-sub-bullets nAAAo sAAAo realmente importantes em R Markdown.
    
### Listas Numeradas

1. As linhas que começam com um número (de 0--9), seguido de um texto, serão interpretadas como itens em uma lista enumerada.
2. O R Markdown lida com a numeração ao processar automaticamente.
2. Isso pode ser útil quando você perde a contagem ou não atualiza os números sozinho ao editar. (Consulte atentamente o arquivo .Rmd para este item.)
     a. VocEEE pode criar sub-listas de listas enumeradas com letras para cada sub-item.
     b. No entanto, são uma coisa frágil, o que é melhor você não forCCCar demais.

### Título, Autor, Data, Formato de saída, Índice

Você pode especificar conteUUUdos como título, autor e data no **cabeçalho** do seu
arquivo R Markdown (atributos em inglEEEs). Isso vai no início do arquivo, precedido e seguido por três hIIIfens. 
Assim, o início deste arquivo ficarAAA como:

```
---
title: Usando R Markdown para anotações de aula
author: CRS
date: Primeira versAAAo 7 janeiro de 2016, revisado em 22 agosto de 2016
---
```

Você também pode usar o cabeçalho para dizer ao R Markdown se deseja que ele seja processado para
HTML (padrão), PDF ou outro formato. Para que ele seja transformado em PDF, por exemplo, eu escrevi:

```
---
title: Usando R Markdown para anotações de aula
author: CRS
date: Primeira versAAAo 7 janeiro de 2016, revisado em 22 agosto de 2016
output: pdf_document
---
```
VocEEE pode adicionar uma tabela de conteúdos como uma opção para o tipo de saída.

```
---
title: Usando R Markdown para anotações de aula
author: CRS
date: Primeira versAAAo 7 janeiro de 2016, revisado em 22 agosto de 2016
output:
  html_document:
    toc: true
---
```

* Para criar PDFs, um programa chamado `LaTeX` (veja abaixo) deve ser instalado
no seu computador.
* Outros formatos de saída podem estar disponíveis. Veja `help (render)` no pacote `rmarkdown`.
* Existem muitas, muitas outras opções de formatação que podem ser dadas no
cabeçalho; consulte os principais arquivos de ajuda do R Markdown on-line.

# Hiperlinks e Imagens

### Hiperlinks

Os hiperlinks (links) sAAAo ancorados por URLs e fáceis de usar: basta digitar a URL, como, por exemplo,
http://www.stat.cmu.edu/~cshalizi/rmarkdown/rmarkdown.Rmd para obter a fonte do arquivo
deste documento. 

Os hiperlinks ancorados no texto têm a [âncora entre colchetes e o link
entre parênteses] (http://www.stat.cmu.edu/~cshalizi/rmarkdown/rmarkdown.Rmd).

```
Os hiperlinks ancorados no texto têm a [âncora entre colchetes e o link
entre parênteses] (http://www.stat.cmu.edu/~cshalizi/rmarkdown/rmarkdown.Rmd)
```

### Imagens

As imagens começam com um ponto de exclamação e depois vem o texto a ser usado
caso a imagem nAAAo possa ser carregada. Em seguida, o endereço do arquivo da imagem
(no mesmo diretório do seu documento) ou uma URL direto para ela (remotamente). Aqui estão dois
exemplos, um para uma imagem no diretório e outro para uma URL.

```
![Uma imagem local](cena-local.jpg)
![Uma imagem remota](http://apod.nasa.gov/apod/image/1302/ringshexagon_cassini_1016.jpg)
```
<!-- ###################### ERRO NA COMPILAÇÃO. ###########
![A local image](local-scene.jpg)
![A remote image](http://apod.nasa.gov/apod/image/1302/ringshexagon_cassini_1016.jpg)
-->

Não existe uma maneira de redimensionar imagens usando comandos prOOOprios Markdown. 
No R Markdown, no entanto, você pode usar o seguinte hack:

<pre><code>```{r, fig.retina=NULL, out.width=100, echo=FALSE}
knitr::include_graphics("http://apod.nasa.gov/apod/image/1302/ringshexagon_cassini_1016.jpg")
```</code></pre>

```{r, fig.retina=NULL, out.width=100, echo=FALSE}
knitr::include_graphics("http://apod.nasa.gov/apod/image/1302/ringshexagon_cassini_1016.jpg")
```
Esse cOOOdigo chama um comando R incluído no pacote `knitr`, com algumas opções sobre como o R é executado (descrito abaixo).

# Incluindo Código

O legal do R Markdown é que ele tambEEEm permite que você inclua seu código e o
executa automaticamente quando seu documento é processado e, de forma incomparável, inclui
os resultados desse código em seu documento. O código vem em duas variedades:
**chunks** (pedaços) de código ou código **inline**.

### Pedaços de código e seus resultados

Um **pedaço** de código é simplesmente um trecho de código isolado. Ele EEE precedido
por ` ``` {r} ` em uma linha e termina por uma linha que apenas diz ` ``` `.
O código entra no meio. Aqui, por exemplo, é algum código que
carrega um conjunto de dados de uma biblioteca e faz um gráfico de dispersão.

<pre><code>```{r}
library(MASS)
data(cats)
plot(Hwt ~ Bwt, data=cats, xlab="Body weight (kg)", ylab="Heart weight (g)")
```</code></pre>

```{r}
library(MASS)
data(cats)
plot(Hwt ~ Bwt, data=cats, xlab="Body weight (kg)", ylab="Heart weight (g)")
```
Primeiro, observe como o código está incluído, bem formatado, no documento.
Em segundo lugar, observe como a saída do código também é automaticamente incluída
no documento. Se o seu código produzir números ou texto, eles também podem ser
incluídos:

```{r}
with(cats, cor(Hwt, Bwt))
```

### Código Inline

A saída do seu código também pode ser muito bem incorporada no texto, usando o 
modo **inline**. Este é o código não iniciado em uma linha, mas começando com
` `r ` e terminando com ` ` `. Usar o código inline é como este documento
sabe que o conjunto de dados `cats` contém linhas `r nrow (cats)`
(` contém ` r nrow(gatos) ` linhas `), e que o peso médio dos corações das fêmeas
dos gatos é `r median(cats$Hwt[cats$Sex=="F"])` gramas (` `r median(cats$Hwt[cats$Sex=="F"])` `).

Observe que o código inline não exibe os comandos executados, apenas a saída deles.

### Visto mas não ouvido

Os pedaços de código (exceto código inline) podem ter um monte de **opções** que modificam
a forma como eles são executados e como eles aparecem no documento. Estas opções vão depois
o `r` inicial e antes do fechamento `}` que representa o início de um pedaço código. 
Uma das opções mais comuns desativa a impressão do código, porEEEm, deixa os resultados isolados:
 ` ```{r, echo=FALSE} `

Outra opção executa o código, mas não inclui nem o texto do código nem a saída.
 ` ```{r, include=FALSE} `
  
Isso pode parecer bobo, mas pode ser útil para pedaços de código que *configuram
como carregar arquivos de dados*, ou estimativas do modelo inicial, etc.


Outra opção imprime o código no documento mas não o executa:
 ` ```{r, eval=FALSE} `
Isso também é útil se você quiser comentar sobre o código (de modo que ele fique bem formatado).

### Nomeando pedaços de código

Você pode atribuir nomes aos pedaços de código logo após a abertura, como
` ``` {r, clevername} `. Esse nome é usado para as imagens (ou outros arquivos)
que são gerados quando o documento é processado.

### Alterando tamanhos de imagem e alinhamentos

Há muitas opções para ajustar a colocação das figuras que o
R produz. `fig.align` controla o **alinhamento** horizontal (esquerda, direita,
ou centro).

Ao produzir PDF, as opções `out.height` e` out.width` permitem que você especifique
a altura ou largura desejada da figura em polegadas, centímetros ou múltiplos
de comprimentos pré-definidos (do `LaTeX`). Então, por exemplo, ` ``` r,
out.height = "3in"} ` força a imagem a 3 polegadas de altura, enquanto que ` ```r,
out.width = "0.48 \\ textwidth"} ` força a largura da imagem a ser um pouco menos do que
metade da largura total do texto na página (de modo que duas dessas imagens
se encaixam lado a lado). As próximas figuras ilustram isso.


```{r, echo=FALSE, fig.width=3, fig.align="center"}
plot(Hwt ~ Bwt, data=cats, xlab="Body weight (kg)",
     ylab="Heart weight (g)", sub="Linear scale")
plot(Hwt ~ Bwt, data=cats, log="xy", xlab="Body weight (kg)",
     ylab="Heart weight (g)", sub="Logarithmic scale")
```



### Tabelas

A impressão padrão de matrizes, tabelas, etc., do R Markdown é, francamente,
feia. O pacote `knitr` contém um comando muito básico, `kable`, que irá
formatar uma matriz ou quadro de dados mais legalmente para exibição.

Compare:

```{r}
coefficients(summary(lm(Hwt ~ Bwt, data=cats)))
```

com

```{r}
library(knitr) # Only need this the first time!
kable(coefficients(summary(lm(Hwt ~ Bwt, data=cats))))
```

--- Pois é, os padrões do R imprimem um número louco de casas decimais, mas
este não é o momento de discutir dígitos significativos, ou a função `signif`.

### "Caching" de pedaços de código (re-executando somente com modificações)

Por padrão, o R Markdown executará de novo seu código toda vez que você renderizar o seu
documento. Se algum código do seu código for lento, isso pode aumentar ainda mais o tempo de renderizaCCCAAAO.
Você pode, no entanto, pedir ao R Markdown para monitorar se um pedaço de código foi modificado e apenas re-executar este pedaço. Isso é chamado **caching** do pedaço de código.

```{r, cache=TRUE}
lm(Hwt ~ Bwt, data=cats)
```
A questão é que um pedaço de código que não se alterou pode invocar
resultados de pedaços anteriores, trechos modificados, e então nós _precisarIIIamos re-executar os
pedaços desatualizados. Existem opções para informar manualmente o R Markdown que "este
trecho depende desse fragmento anterior", mas geralmente é mais fácil deixar ele mesmo cuidar disso, definindo a opção `autodep = TRUE`.

1. Se você carregar um pacote com os comandos `library()` ou `require()`, o R
   Markdown não é inteligente o suficiente para verificar se o pacote mudou
   (ou realmente foi instalado, se você sem ele instalado). Então isso não vai
   lanCCCar uma re-execução automática de um pedaço de código em cache.
2. Para forçar manualmente a re-execução de todos os pedaços de código, o mais fácil de fazer é
   excluir o diretório que o R Markdown cria (algo como 
   _filename_`_cache`) para armazenar o estado de todos os pedaços de código.
   
### Configuração de padrões para todos os pedaços de código

Você pode dizer para o R definir alguns padrões para se aplicar a todos os pedaços onde você não faz
especificamente sobrecarregá-los. Aqui estão os que eu geralmente uso:   

### Setting Defaults for All Chunks

You can tell R to set some defaults to apply to all chunks where you don't
specifically over-ride them.  Here are the ones I generally use:

```{r, eval=FALSE}
# Need the knitr package to set chunk options
library(knitr)

# Set knitr options for knitting code into the report:
# - Don't print out code (echo)
# - Save results so that code blocks aren't re-run unless code changes (cache),
# _or_ a relevant earlier code block changed (autodep), but don't re-run if the
# only thing that changed was the comments (cache.comments)
# - Don't clutter R output with messages or warnings (message, warning)
  # This _will_ leave error messages showing up in the knitted report
opts_chunk$set(echo=FALSE,
               cache=TRUE, autodep=TRUE, cache.comments=FALSE,
               message=FALSE, warning=FALSE)
```

This sets some additional options beyond the ones I've discussed, like not
re-running a chunk if only the comments have changed (`cache.comments =
FALSE`), and leaving out messages and warnings.  (I'd only recommend
suppressing warnings once you're sure your code is in good shape.)  I would
typically give this set-up chunk itself the option `include=FALSE`.

You can over-ride these defaults by setting options for individual chunks.

### More Options

See [http://yihui.name/knitr/options/] for a complete listing of possible chunk options.


# Math in R Markdown

Since this is a statistics class, you need to be able to write out mathematical
expressions, often long series of them.  R Markdown gives you the syntax to
render complex mathematical formulas and derivations, and have them displayed
_very_ nicely.  Like code, the math can either be inline or set off
(**displays**).

Inline math is marked off witha pair of dollar
signs (`$`), as $\pi r^2$ or $e^{i\pi}$.

```
Inline math is marked off witha pair of dollar
signs (`$`), as $\pi r^2$ or $e^{i\pi}$.
```

Mathematical displays are marked off with `\[` and `\]`, as in
\[
e^{i \pi} = -1
\]

```
Mathematical displays are marked off with `\[` and `\]`, as in
\[
e^{i \pi} = -1
\]
```

Once your text has entered math mode, R Markdown turns over the job of
converting your text into math to a different program, called LaTeX[^latex].
This is the most common system for typesetting mathematical documents
throughout the sciences, and has been for decades.  It is extremely powerful,
stable, available on basically every computer, and completely free.  It is
also, in its full power, pretty complicated.  Fortunately, the most useful
bits, for our purposes, are actually rather straightforward.

### Elements of Math Mode

* Most letters will be rendered in italics (compare: a vs. `a` vs. $a$; only
the last is in math mode).  The spacing between letters also follows the conventions for math, so don't treat it as just another way of getting italics.  (Compare _speed_, in simple italics, with $speed$, in math mode.)
* Greek letters can be accessed with the slash in front of their names, as `\alpha` for $\alpha$.  Making the first letter upper case gives the upper-case letter, as in `\Gamma` for $\Gamma$ vs. `\gamma` for $\gamma$.  (Upper-case alpha and beta are the same as Roman A and B, so no special commands for them.)
* There are other "slashed" (or "escaped") commands for other mathematical symbols:
    + `\times` for $\times$
    + `\cdot` for $\cdot$
    + `\leq` and `\geq` for $\leq$ and $\geq$
    + `\subset` and `\subseteq` for $\subset$ and $\subseteq$
    + `\leftarrow`, `\rightarrow`, `\Leftarrow`, `\Rightarrow` for $\leftarrow$, $\rightarrow$, $\Leftarrow$, $\Rightarrow$
    + `\approx`, `\sim`, `\equiv` for $\approx$, $\sim$, $\equiv$
    + See, e.g., http://web.ift.uib.no/Teori/KURS/WRK/TeX/symALL.html for a fuller
listing of available symbols.  (http://tug.ctan.org/info/symbols/comprehensive/symbols-a4.pdf lists _all_ symbols available in `LaTeX`, including many non-mathematical special chracters)
* Subscripts go after an underscore character, `_`, and superscripts go after a caret, `^`, as `\beta_1` for $\beta_1$ or `a^2` for $a^2$.
* Curly braces are used to create groupings that should be kept together, e.g., `a_{ij}` for $a_{ij}$ (vs. `a_ij` for $a_ij$).
* If you need something set in ordinary (Roman) type within math mode, use `\mathrm`, as `t_{\mathrm{in}}^2` for $t_{\mathrm{in}}^2$.
* If you'd like something set in an outline font ("blackboard bold"), use `\mathbb`, as `\mathbb{R}` for $\mathbb{R}$.
* For bold face, use `\mathbf`, as
```
(\mathbf{x}^T\mathbf{x})^{-1}\mathbf{x}^T\mathbf{y}
```
for
\[
(\mathbf{x}^T\mathbf{x})^{-1}\mathbf{x}^T\mathbf{y}
\]
* Accents on characters work rather like changes of font: `\vec{a}` produces
  $\vec{a}$, `\hat{a}` produces $\hat{a}$.  Some accents, particularly hats,
  work better if they space out, as with `\widehat{\mathrm{Var}}` producing
  $\widehat{\mathrm{Var}}$.
* Function names are typically written in romans, and spaced differently: thus
  $\log{x}$, not $log x$.  `LaTeX`, and therefore `R Markdown`, knows about a
  lot of such functions, and their names all begin with `\`.  For instance:
  `\log`, `\sin`, `\cos`, `\exp`, `\min`, etc.  Follow these function names
  with the argument in curly braces; this helps `LaTeX` figure out what exactly
  the argument is, and keep it grouped together with the function name when
  it's laying out the text.  Thus `\log{(x+1)}` is better than `\log (x+1)`.
* Fractions can be created with `\frac`, like so:
```
\frac{a+b}{b} = 1 + \frac{a}{b}
```
produces
\[
\frac{a+b}{b} = 1 + \frac{a}{b}
\]
* Sums can be written like so:
```
\sum_{i=1}^{n}{x_i^2}
```
will produce
\[
\sum_{i=1}^{n}{x_i^2}
\]
The lower and upper limits of summation after the `\sum` are both optional.
Products and integrals work similarly, only with `\prod` and `\int`:
\[
n! = \prod_{i=1}^{n}{i}
\]
\[
\log{b} - \log{a} = \int_{x=a}^{x=b}{\frac{1}{x} dx}
\]
`\sum`, `\prod` and `\int` all automatically adjust to the size of the expression being summed, producted or integrated.
* "Delimiters", like parentheses or braces, can automatically re-size to match what they're surrounding.  To do this, you need to use `\left` and `\right`,
as
```
\left( \sum_{i=1}^{n}{i} \right)^2 = \left( \frac{n(n-1)}{2}\right)^2 = \frac{n^2(n-1)^2}{4}
```
renders as
\[
\left( \sum_{i=1}^{n}{i} \right)^2 = \left( \frac{n(n-1)}{2}\right)^2 = \frac{n^2(n-1)^2}{4}
\]
   + To use curly braces as delimiters, precede them with slashes, as `\{` and `\}` for $\{$ and $\}$.
* Multiple equations, with their equals signs lined up, can be created
using `eqnarray`, as follows.
```
\[
\begin{eqnarray}
X & \sim & \mathrm{N}(0,1)\\
Y & \sim & \chi^2_{n-p}\\
R & \equiv & X/Y \sim t_{n-p}
\end{eqnarray}
\]
```

\[
\begin{eqnarray}
X & \sim & \mathrm{N}(0,1)\\
Y & \sim & \chi^2_{n-p}\\
R & \equiv & X/Y \sim t_{n-p}
\end{eqnarray}
\]
Notice that `&` surrounds what goes in the middle on each line, and each line (except the last) is terminated with `\\`.  The left or right hand side of the equation can be blank, and space will be made:
```
\[
\begin{eqnarray}
P(|X-\mu| > k) & = & P(|X-\mu|^2 > k^2)\\
& \leq & \frac{\mathbb{E}\left[|X-\mu|^2\right]}{k^2}\\
& \leq & \frac{\mathrm{Var}[X]}{k^2}
\end{eqnarray}
\]
```

\[
\begin{eqnarray}
P(|X-\mu| > k) & = & P(|X-\mu|^2 > k^2)\\
& \leq & \frac{\mathbb{E}\left[|X-\mu|^2\right]}{k^2}\\
& \leq & \frac{\mathrm{Var}[X]}{k^2}
\end{eqnarray}
\]

(In full `LaTeX`, `\begin{eqnarray}` automatically enters math mode, but
R Markdown needs the hint.)

### Translating Math into `LaTeX`

`LaTeX` is designed so that every part of a mathematical expression has a
reasonably straightforward counterpart in what you write.  Still, it can be a
bit intimidating at first.  What many people find useful to to start by taking
some page of printed or hand-written math and then deliberately translate that,
line by line, into `LaTeX`, and then rendering it to see whether it came out
right (and, if not, where to fix things).  If you need to do any math for an
assignment, it can be a good idea to write the math out by hand, and then turn
it into `LaTeX`, whether the class requires it (like this one) or not.
Eventually, with practice, the translation will become quite automatic, and
some people even do new math by writing out the `LaTeX`.

### `LaTeX` Does Not Check Correctness

`LaTeX` does not check whether your math is _right_; it just checks whether
it can figure out what you're trying to say well enough to type-set it.
Thus for instance it has no problem at all with the following:

\[
\begin{eqnarray}
(n+1)(n-1) & = & n^2\\
n^2 -1 & = & n^2\\
-1 & = & 0\\
1 & = & 0\\
-1 & = & 1
\end{eqnarray}
\]

(There _are_ computer programs for doing symbolic mathematics which, in effect,
do check whether your math is right, at least if you're working in the sub-area
of math they're designed to handle.  So far as I know, no one has ever really
combined them with `LaTeX`.)

### More Advanced Math-Mode Stuff: New Commands

One of the things you can do in `LaTeX` is create your own commands.
This is useful if you find yourself writing out the same complicated expression
repeatedly, or, alternatively, if you want to make sure that the same
symbol is always used for the same concept.  For instance, in some areas of
statistics, the generic parameter of a model is $\theta$, in others $\beta$,
in yet others $\psi$.  If you do something like this early on
```
\[
\newcommand{\MyParameter}{\theta}
\]
```
then in later bits of math mode you can write `\MyParameter`, and `LaTeX` will
translate this to `\theta`.  If you later decide that you want your parameter
to be `\beta`, or even `\mathrm{fred}`, you just change that initial definition
of the new command, rather than having to track down each `\theta`.

New commands can also take one or more arguments.  Here is a useful command
for writing expectations:
```
\[
\newcommand{\Expect}[1]{\mathbb{E}\left[ #1 \right]}
\]
```
And here is a command for writing covariances:
```
\[
\newcommand{\Cov}[2]{\mathrm{Cov}\left[ #1, #2\right]}
\]
```

Defining commands like this not only saves you typing, and makes it easier to
make changes; it also makes your math-mode text easier for you, or others, to
read even if it isn't rendered.  This is like using comprehensible
variable and function names in your programs, and for that matter like
using functions rather than long strings of commands in the first place.


It is also possible to define new function names which act like `\log`,
new mathematical operators, draw diagrams, etc., etc., but that goes way
beyond the scope of these notes.

### Installing `LaTeX`

If you render your R Markdown document to HTML, you do not need to install
`LaTeX` on your computer.  This is because the HTML includes instructions to
browsers, which say (as it were) "Send the funny-looking bits with all the
slashes to [mathjax.org](http://www.mathjax.org), and it will send you back
pretty pictures of equations".  The website actually runs the `LaTeX`.

If you want to produce PDF, you need to have `LaTeX` installed on your
computer.  How you actually do this depends on the precise kind of computer.
For Macs, I recommend using the `MacTeX` package, available from
https://tug.org/mactex/mactex-download.html.  For other systems, follow the
links from http://www.tug.org/begin.html.

# Putting It All Together: Writing Your Report in R Markdown

* You have installed the `rmarkdown` package and all its dependencies.
* You have installed `LaTeX`, if you're producing a PDF.
* You have installed and fired up your favorite text editor.
* You open it up to a new document.
    + You give it a title, an author, and a date.
* You use headers to divide it into appropriate, titled sections, and possibly sub-sections.
    + One common pattern: "Introduction", "Data and Research Questions", "Analysis", "Results", "Conclusion".
    + Another common pattern: "Problem 1", "Problem 2", ... , "Extra Credit".
* You write text.
* When you need it, you insert math into the text, or even whole mathematical
  displays.
* When you need it, you insert code into your document.
    + The code runs (as needed) when you render the document.
	+ Figures, tables, and other output are automatically inserted into the document, and track changes in your code.
* Every so often, try to render your document.
    + When you (think you) have finished a section is a good time to do so.
	+ Another good time is once you've made any non-trivial change to the code or the text.
* Either your document rendered successfully or it didn't.
    + If it did, and you like the results, congratulate yourself and cheerfully go on to your next task.
	+ If it rendered but you don't like the results, think about why and try to fix it.
	+ If it didn't render, R will tell you where it gave up, so try to debug from around there.

# Troubleshooting/Stuff to Avoid

- Do not call `View` or `help` in your document; these are interactive commands which don't work well in scripts.
- "It worked in the console but it wouldn't knit": You have almost certainly done something somewhat different _before_ the code chunk that's giving you trouble.  Clear your workspace in the console and re-run.
    + R Studio keeps _two_ environments or workspaces which it uses to evaluate R expressions, look up function or variable names, etc.  One is the "usual" global environment of the console, which builds cumulatively from the start of your session.  (Unless you deliberately manipulate it; don't do that unless you know what you're doing.)  Every time you knit, however, it re-runs your code in clean workspace, as though you had just started R from scratch.  This means knitted code does what you say it should, and _only_ that.  If your code knits, it should work on any computer; getting something to run in the console which you can't reproduce is just dumb luck.
- "It works when I source it, but it won't knit": This is basically the same problem as "it worked in the console".
- Avoid `attach` in both the console and in your file; using it is a recipe for creating hard-to-find errors.  You can still shorten expressions using `with` instead.
- You need LaTeX to create PDFs.  If you are having trouble doing so, try switching the output format to HTML.
    + Do try to fix your LaTeX installation later, when you don't have such time pressure; it's really useful.
	+ LaTeX will complain if you try to print out truly enormous things.  Errors about "out of stack", or "pandoc 43", are often caused by this. Don't print out enormous things.  (Suppressing warnings and other messages may help.)
- When you need to load data files or source someone else's code, use full URLs, rather than creating local copies and loading them from your disk.


# Further Reading

For more on R Markdown, see http://rmarkdown.rstudio.com, particularly the
more detailed help pages (rather than the first-guides).

For `LaTeX`, the classic reference is the book by Leslie Lamport, _LaTeX: A
Document Preparation System_ (2nd ed., Reading, Mass.: Addison-Wesley, 1994).
This is not, admittedly, the easiest read in the world.
[_LaTeX_](https://en.wikibooks.org/wiki/LaTeX), from Wikibooks, is more
accessible, and free online in easy bite-sized chunks.

R Markdown is based on the `knitr` package, developed by Yihui Xie, for
integrated R with `LaTeX`; see http://yihui.name/knitr/, and, for
full documentation, Xie's book _Dynamic Documents with R and knitr_ (2nd
edition, Boca Raton, Florida; CRC Press, 2016).

For an thorough, entertaining, and completely correct explanation of why "The
word processor is a stupid and grossly inefficient tool for preparing text for
communication with others", see http://ricardo.ecn.wfu.edu/~cottrell/wp.html.

[^latex]: In the 1970s, the great computer scientist Donald Knuth wrote a
mark-up language, and a rendering program for that language, called `TeX`
(pronounced "tech"), for writing complex mathematical documents.  In the 1980s,
the computer scientist Leslie Lamport extended `TeX` in ways that made it
rather more user-friendly, and called the result `LaTeX` (pronounced
"la-tech").

### Acknowledgments

Thanks to Prof. [Howard
Seltman](http://www.stat.cmu.edu/~hseltman/AboutMe.html) for suggestions; to
Dr. [Uma Ravat](http://www.math.uiuc.edu/~umaravat/) for showing me the trick
for re-sizing images; and to an old post by Prof. [Jenny
Bryan](http://www.stat.ubc.ca/~jenny/) on [how to include verbatim R
chunks](http://rmarkdown.rstudio.com/articles_verbatim.html).
