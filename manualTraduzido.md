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

```{r, eval=FALSE}
# Precisamos do pacote knitr para definir opções de trechos de código
library(knitr)

# Seta opções do knitr para gerar código no relatório
# - Não imprime código
# - Salva os resultados para que os blocos de código não sejam executados novamente, a menos que o código mude (cache),
# _ou_ um bloco de código anterior relevante seja modificado (autodep), mas não o re-executa se o
# única coisa que mudou forem comentários (cache.comments)
# - Não obstrua a saída R com mensagens ou avisos (mensagem, aviso)
   # Isto _deixará_ mensagens de erro aparecendo no relatório gerado
opts_chunk$set(echo=FALSE,
               cache=TRUE, autodep=TRUE, cache.comments=FALSE,
               message=FALSE, warning=FALSE)
```

Assim definimos algumas opções adicionais além das que eu discuti, como não
re-executar um pedaço se apenas os comentários mudaram (`cache.comments =
FALSE`), e deixando de receber mensagens e avisos. (Eu só recomendaria
suprimir avisos se você tem a certeza de que seu código está ok.) Eu, normalmente,
também atribuiria a este ponto de configuração a opção `include = FALSE`.

Você pode sobrescrever estes padrões definindo opções para trechos específicos.

### Mais Opções

Veja em [http://yihui.name/knitr/options/] para obter uma listagem completa das opções possíveis.


# Matemática no R Markdown

Como esta é uma aula de Estatística, é importante que você seja capaz de escrever expressões matemáticas,
muitas vezes longas séries delas. O R Markdown oferece a sintaxe para
tornar fórmulas e derivações matemáticas complexas, e exibi-las _muito_ lindamente. Assim como o código,
a matemática pode ser inline ou como (**apresentações**). <- ???

O código de matemática inline é marcado com um par de dólares
(`$`), as $\pi r^2$ or $e^{i\pi}$.

```
O código de matemática inline é marcado com um par de dólares
(`$`), as $\pi r^2$ or $e^{i\pi}$.
```

??? --> Exibições matemáticas são marcadas com `\[` and `\]`, como em
\[
e^{i \pi} = -1
\]

```
??? --> Exibições matemáticas são marcadas com `\[` and `\]`, como em
\[
e^{i \pi} = -1
\]
```

Uma vez que seu texto está no modo matemático, o R Markdown faz o trabalho de
converter seu texto matemático para um programa diferente, chamado LaTeX[^latex].
Ele é o sistema mais comum para a composição de documentos matemáticos
em todas as ciências, e tem sido há décadas. Ele é extremamente poderoso,
estável, disponível basicamente em todos as plataformas e completamente gratuito. 
Mas isso também o torná-lo, em seu poder total, muito complicado. Felizmente, para nossos propósitos, 
é bastante simples. <-- ???


### Elementos do Modo Matemático

* A maioria das letras será renderizada em itálico (compare: a vs. `a` vs. $a$; apenas
o último está em modo matemático). O espaçamento entre as letras também segue as convenções da matemática, então não a trate como só outra maneira de obter itálico. (Compare _speed_, em itálico simples, com $speed$, no modo matemático.)
* Letras gregas podem ser acessadas com a barra na frente de seus nomes, como `\alpha` para $\alpha$. Fazer a primeira letra em maiúscula te dá a letra maiúscula, como em `\Gamma` para $\Gamma$ vs. `\gamma` para $\gamma$. (As maiúsculas alpha e beta são as mesmas que as Romanas A e B, portanto, não precisa de comando especial para elas.)
* Existem outros comandos "cortados" (ou "escapados") para outros símbolos matemáticos:
    + `\times` para $\times$
    + `\cdot` para $\cdot$
    + `\leq` e `\geq` para $\leq$ and $\geq$
    + `\subset` e `\subseteq` para $\subset$ and $\subseteq$
    + `\leftarrow`, `\rightarrow`, `\Leftarrow`, `\Rightarrow` para $\leftarrow$, $\rightarrow$, $\Leftarrow$, $\Rightarrow$
    + `\approx`, `\sim`, `\equiv` for $\approx$, $\sim$, $\equiv$
    + Veja, também, http://web.ift.uib.no/Teori/KURS/WRK/TeX/symALL.html para uma
lista completa dos símbolos.  (http://tug.ctan.org/info/symbols/comprehensive/symbols-a4.pdf lista de _todos_ os símbolos disponíveis no `LaTeX`, incluindo muitos caracteres especiais não-matemáticos)
* Subscritos vêm depois de um caractere underscore, `_`, e sobrescritos vêm depois de um circunflexo, `^`, como `\beta_1` para $\beta_1$ ou `a^2` para $a^2$.
* As chaves são usadas para criar agrupamentos que devem ser mantidos em conjunto, como, por exemplo, `a_{ij}` para $a_{ij}$ (vs. `a_ij` para $a_ij$).
* Se você precisa de algo em fonte normal (romana) no modo matemático, use `\mathrm`, como `t_{\mathrm{in}}^2` para $t_{\mathrm{in}}^2$.
* Se você quiser algo em uma fonte de estrutura de tópicos ("quadro-negro" ou "negrito") <- ??? use `\mathbb`, as `\mathbb{R}` para $\mathbb{R}$.
* Para texto negrito, use `\mathbf`, como
```
(\mathbf{x}^T\mathbf{x})^{-1}\mathbf{x}^T\mathbf{y}
```
para
\[
(\mathbf{x}^T\mathbf{x})^{-1}\mathbf{x}^T\mathbf{y}
\]
* Acentos nos caracteres funcionam como mudanças de fonte: `\vec{a}` gera
  $\vec{a}$, `\hat{a}` gera $\hat{a}$.  Alguns acentos, particularmente os "chapéus",
  funcionam melhor com espaços, como `\widehat{\mathrm{Var}}` produzindo
  $\widehat{\mathrm{Var}}$.
* Nomes de funções são, geralmente, escritos em fonte normal e espaçados de forma diferente: 
  $\log{x}$, não $log x$. O `LaTeX` e, por consequência, o `R Markdown` também, conhece muitas
  dessas funções e seus nomes iniciam com `\`.  Por exemplo:
  `\log`, `\sin`, `\cos`, `\exp`, `\min`, etc.  Siga estes nomes de funções
  com o argumento em chaves; isso ajuda o `LaTeX` a descobrir o que exatamente
  o argumento é, e mantê-lo agrupado com o nome da função quando
  está colocando o texto.  Então `\log{(x+1)}` é melhor que `\log (x+1)`.
* Frações podem ser criadas com `\frac`, como:
```
\frac{a+b}{b} = 1 + \frac{a}{b}
```
produz
\[
\frac{a+b}{b} = 1 + \frac{a}{b}
\]
* Somas podem ser escritas como:
```
\sum_{i=1}^{n}{x_i^2}
```
produzirá
\[
\sum_{i=1}^{n}{x_i^2}
\]
Os limites inferior e superior do somatório após a `\sum` são ambos opcionais.
Produtos e integrais funcionam de forma semelhante, apenas com `\prod` e `\int`:
\[
n! = \prod_{i=1}^{n}{i}
\]
\[
\log{b} - \log{a} = \int_{x=a}^{x=b}{\frac{1}{x} dx}
\]
`\sum`, `\prod` and `\int` se ajustam automaticamente ao tamanho da expressão a qual são somados, multiplicados ou integrados.
* "Delimitadores", como parênteses ou chaves, podem se redimensionar automaticamente para corresponder ao que eles têm ao redor.   Para fazer isso, você precisa usar `\left` e `\right`,
como
```
\left( \sum_{i=1}^{n}{i} \right)^2 = \left( \frac{n(n-1)}{2}\right)^2 = \frac{n^2(n-1)^2}{4}
```
será renderizado como
\[
\left( \sum_{i=1}^{n}{i} \right)^2 = \left( \frac{n(n-1)}{2}\right)^2 = \frac{n^2(n-1)^2}{4}
\]
   + Para usar chaves como delimitadores, anteceda-os com barras como `\{` e `\}` para $\{$ e $\}$.
* Múltiplas equações, com seus sinais iguais alinhados, podem ser criadas
usando `eqnarray`, da seguinte forma:
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
Observe que `&` envolve o que se passa no meio em cada linha e cada linha (exceto a última) é encerrada com `\\`. O lado esquerdo ou direito da equação pode estar em branco que o espaço será feito:
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

(Resumindamente `LaTeX`, `\begin{eqnarray}` entra automaticamente no modo matemático, mas o
R Markdown precisa de um empurrãozinho.)

### Traduzindo Matemática para `LaTeX`

O `LaTeX` é projetado para que cada parte de uma expressão matemática tenha uma
relação razoavelmente <-- direta ao que você escreve. Ainda assim, ele pode ser um
um pouco intimidador no início. O que muitas pessoas acham útil é começar com
alguma página com código matemático impresso ou manuscrito e depois traduzi-la,
linha por linha, no `LaTeX`, processando para ver se ele saiu
direito (e, caso contrário, entender onde consertar coisas). Se você precisa fazer expressões matemáticas para um
trabalho, pode ser uma boa ideia escrever as contas à mão e depois aproveitá-lo 
no `LaTeX`, se a aula o exige (como este), ou não.
Eventualmente, com a prática, a tradução se tornará fluida e automática.
Algumas pessoas inovam ainda a matemática escrevendo no `LaTeX`.

### `LaTeX` não verifica a correção

`LaTeX` não verifica se sua matemática está _certa_; ele apenas verifica se
descobre o que você está tentando dizer bem o suficiente para digitar e configurá-lo.
Assim, por exemplo, não tem nenhum problema com o seguinte:

\[
\begin{eqnarray}
(n+1)(n-1) & = & n^2\\
n^2 -1 & = & n^2\\
-1 & = & 0\\
1 & = & 0\\
-1 & = & 1
\end{eqnarray}
\]

(Existem programas de computador para matemática simbólica que, de fato,
verifique se sua operação matemática está correta, pelo menos se você estiver trabalhando na sub-área
de matemática a qual eles são projetados para lidar. Até onde eu sei, ninguém realmente
os combinou com `LaTeX`.)

### Um pouco mais de conteúdo avançado no modo matemátioc: Novos Comandos

Uma das coisas que você pode fazer no `LaTeX` é criar seus próprios comandos.
Isso é útil se você se encontrar escrevendo a mesma expressão complicada
repetidamente, ou, alternativamente, se você quiser ter certeza de que o mesmo
símbolo sempre será usado para a mesma ocasião. Por exemplo, em algumas áreas da 
estatística, o parâmetro genérico de um modelo é $\theta$, já em outros $\beta$, 
em outros $\psi$. Se você quiser, pode fazer algo como 
```
\[
\novocomando{\MeuParametro}{\theta}
\]
```
e então, em bits mais recentes de modo matemático <- ???, você pode escrever `\MeuParametro` e o `LaTeX` irá
traduzir isto para `\theta`. Se você decidir mais tarde que o seu parâmetro
seja `\beta`, ou mesmo `\mathrm{fred}`, basta alterar essa definição inicial
do novo comando, em vez de ter que usar cada `\theta`. <<<<---- ???

Novos comandos também podem receber um ou mais argumentos. Aqui está um comando útil
para escrever perspectivas <--- ???:
```
\[
\novocomando{\Expect}[1]{\mathbb{E}\left[ #1 \right]}
\]
```
E aqui está um comando para escrever covariâncias:
```
\[
\novocomando{\Cov}[2]{\mathrm{Cov}\left[ #1, #2\right]}
\]
```

Definir comandos como este não só te poupa de digitar muito, como torna mais fácil
gerir mudanças; também torna seu texto em modo matemático mais fácil para você e para os outros.
Isto é como usar nomes compreensíveis para variáveis e funções em seus programas (da mesma forma que é
preterívei criar funções em vez de codificar longas linhas de comandos.


Também é possível definir novos nomes às funções que funcionem como `\log`,
novos operadores matemáticos, diagramas de desenho, etc., etc., mas isso vai além do alcance dessas notas.

### Instalando `LaTeX`

Se você exportar seu documento R Markdown para HTML, não precisará instalar
`LaTeX` em seu computador. Isso acontece porque o HTML inclui instruções para
navegadores, que falam (por assim dizer) "Envie os bits de aparência engraçada com todos os
slashes para [mathjax.org](http://www.mathjax.org), e ele irá enviar você de volta
belas imagens de equações". O site realmente executa o `LaTeX`. <--- ???

Já se você quer produzir um PDF, aí, sim, você precisa ter o `LaTeX` instalado no seu
computador. A instalação depende da máquina. Para Macs, recomendo usar o pacote `MacTeX`, disponível em
https://tug.org/mactex/mactex-download.html. Para outros sistemas, veja os links de http://www.tug.org/begin.html.

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
