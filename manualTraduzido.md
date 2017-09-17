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
    
# Visão geral

Usar R Markdown é uma maneira muito simples de escrever relatórios, além de rodar seu código R neles automaticamente.
Ele também te permite usar notação matemática, hiperlinks, imagens e entre outras formatações básicas. O objetivo deste guia é explicar, com exemplos, como usar os recursos mais essenciais do R Markdown. Não é uma referência abrangente (para isso, veja: http://rmarkdown.rstudio.com)

Este guia pressupõe que você conheça, ao menos, um pouco de R.

O guia original está em http://www.stat.cmu.edu/~cshalizi/rmarkdown/rmarkdown.Rmd. Por favor, consulte a versão mais recente. Correções e sugestões são bem-vindas.



# *Mark up*, Markdown

Provavelmente você já esteja acostumado a usar programas de processamento de texto, como o Microsoft Word, que empregam o princípio do "what you see is what you get" - WYSIWYG (que pode ser traduzido como "o que se vê é o que se obtém"): você deseja que algumas palavras sejam impressas em itálico e, com um clique, logo estão em itálico lá na tela. Quer que outras palavras tenham uma fonte maior e diferente, então você apenas seleciona o tipo de fonte e seu tamanho e assim por diante. Isso funciona bem o suficiente para <del>n00bs</del> leigos, mas não é uma forma viável para um sistema de formatação de texto, porque aí se depende de um programa específico que: (a) saiba o que você quer dizer; e, (b): implemente-o muito bem. Durante várias décadas, os sistemas realmente sérios de escrita basearam-se em um princípio muito diferente: o da marcação de texto. A ideia essencial em uma **linguagem de marcação** é que ela funciona em texto comum, além de sinais que indicam como alterar a formatação ou o significado do texto. Algumas linguagens de marcação, como o HTML (Hyper-Text Markup Language), utilizam uma sintaxe muito técnica; outras, como o **Markdown**, são mais sutis. Por exemplo, as frases anteriores no Markdown são literalmente escritas assim:

```
Durante várias décadas, os sistemas realmente sérios de escrita basearam-se em um princípio muito diferente: o da marcação de texto. A ideia essencial em uma **linguagem de marcação** é que ela funciona em texto comum, além de sinais que indicam como alterar a formatação ou o significado do texto. Algumas linguagens de marcação, como o HTML (Hyper-Text Markup Language), utilizam uma sintaxe muito técnica; outras, como o **Markdown**, são mais sutis.
```
Cada linguagem de marcação é *processada* em um formato que lhe inclui uma bela formatação, imagens, notação matemática, códigos, etc., etc., especificadas pela marcação. No caso do HTML, seu programa de renderização (processamento) é chamado de "web browser" (navegador web). A maioria dos computadores que interpretam o Markdown podem convertê-lo para: HTML (visualizando o documento Markdown no navegador), PDF (visualizando o documento num leitor de PDF, como Acrobat ou outros) ou o Word (finalmente, a abominação de Redmond<sup>[1](#nota1)</sup>).

As vantagens das linguagens de marcação são muitas: elas tendem a ser mais portáteis, sem gastos com licença e mais estáveis ao longo do tempo do que os programas de processamento de texto WYSIWYG. R Markdown é gratuito (você nunca pagará para usá-lo) e livre (a documentação está completamente aberta a todos). Mesmo que você prefira o Word, a pura estabilidade dessas linguagens as torna superiores a documentos científicos.

O [**Markdown**](http://daringfireball.net/projects/markdown/basics) é uma linguagem de marcação simples criada por John Gruber. Hoje, existem muitos programas que traduzem documentos escritos em Markdown para documentos em formato HTML, PDF ou mesmo Word (entre outros formatos).<br> 
[**R Markdown**](http://rmarkdown.rstudio.com), por sua vez, é uma extensão do Markdown para incorporar código em execução (em R), incluindo o resultado no documento. O presente guia mostra três aspectos do R Markdown: como incluir formatação básica; como incluir o código R e sua saída; e, como incluir notação matemática.


# Renderizando e editando

Para escrever em R Markdown, você precisará de um editor de texto: um programa que permite ler
e escrever arquivos de texto simples. Você também precisará do R instalado e de seu pacote `rmarkdown`
(bem como todos os pacotes que dependam dele).

* A maioria dos computadores vem com um editor de texto (TextEdit no Mac, Notepad em máquinas Windows, etc.).
* Há também muitos outros editores mais robustos. Eu uso [Emacs](http://www.gnu.org/software/emacs/emacs.html), mas admito que ele tem uma curva de aprendizado áspera.
* Você _pode_ usar o Word (ou qualquer outro processador de texto WYSIWYG), tomando cuidado apenas de salvar o seu documento em formato de texto simples. Entretanto, eu não recomendo isso.
* O [R Studio](http://www.rstudio.com) vem com um editor de textos próprio, apropriado, e com muitas ferramentas para se trabalhar com documentos R Markdown.

Se é sua primeira vez usando um editor de texto para algo sério, eu recomendo usar o R Studio.

### Renderizando no R Studio

Supondo que você tenha o documento R Markdown aberto no editor de texto,
clique no botão "knit".

### Renderizando no R sem usar o R Studio

Use o comando `render` do pacote `rmarkdown`.

### Renderizando via linha de comando (tipo sistemas UNIX)

Se você preferir renderizar via linha de comando, o script Perl [`rmarkdown.pl`](http://www.stat.cmu.edu/~cshalizi/rmarkdown/rmarkdown.pl)
poderá fazer todo o trabalho. Para usá-lo, há o seguinte comando `rmarkdown.pl nome_do_arquivo`, e
resultará na saída `nome_do_arquivo.html` ou `nome_do_arquivo.pdf`, conforme especificado no
próprio arquivo. (ver abaixo.)

# Formatação básica em R Markdown

Na maior parte do documento, texto é apenas texto. Uma vantagem do R Markdown é que a
você digita seu documento como você normalmente faz.

### Quebra de parágrafos e quebra forçada de linhas

Para inserir uma quebra de linha entre os paragráfos, deixe uma linha em branco entre eles.

Para forçar uma quebra de linha, ponha _dois_ espaços  
em branco ao final da linha.

```
Para inserir uma quebra de linha entre os paragráfos, deixe uma linha em branco entre eles.

Para forçar uma quebra de linha, ponha _dois_ espaços  
em branco ao final da linha.
```

### Cabeçalhos

O caractere `#` no início de uma linha significa que o resto da linha será interpretado
como um cabeçalho de seção. O número de `#`s no começo da linha indica, respectivamente,
o número da seção, sub-seção, sub-sub-seção, etc. do documento. Por exemplo, o `Formatação Básica em R Markdown` acima é precedido por um único `#`, mas o `Cabeçalhos` do começo deste
parágrafo foi precedido por `###`. Não separe cabeçalhos por quebra de linhas.

### Itálico, negrito

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

### Fonte em estilo console

Para imprimir um texto com fonte de largura fixa (estilo de código-fonte), deve-se iniciá-lo e terminá-lo com
um sinal de crase, sem quebras de linha no texto. (Por exemplo, `R` vs. R.) 
Se você quiser exibir várias linhas como um texto, insira três crases no começo e ao final do texto:

```
O texto a ser impresso em uma fonte de largura fixa, inicia e termina com
um sinal de crase, sem quebras de linha no texto. (Por exemplo, `R` vs. R.)
```

### Lista de marcadores

* Esta é uma lista de marcadores (lista não-ordenada) onde os itens são marcados com pontos (bullets).
* Cada item da lista deve começar com um `*` (asterisco) ou um único hífen (`-`).
* Cada item deve estar em uma nova linha.
    + Para sub-itens, idente as linhas (recue à direita) e as inicie com `+`.
    + Sub-sub-itens não são realmente importantes em R Markdown.
    
### Listas numeradas

1. As linhas que começam com um número (de 0--9), seguido de um texto, são interpretadas como itens em uma lista enumerada.
2. O R Markdown lida com a numeração ao processar automaticamente.
2. Isso pode ser útil quando você perde a contagem ou não atualiza os números sozinho ao editar (consulte atentamente o arquivo .Rmd para este item.)
     a. Você pode criar sub-listas de listas enumeradas com letras para cada sub-item. <---
     b. No entanto, elas são uma coisa "frágil", o que é melhor você não forçar demais.

### Título, autor, data, formato de saída, índice

Você pode especificar conteúdos como título, autor e data no **cabeçalho** do seu
arquivo R Markdown (atributos em inglês). Isso vai no início do arquivo, precedido e seguido por três hífens. 
Assim, o início deste arquivo ficará como:

```
---
title: Usando R Markdown para anotações de aula
author: CRS
date: Primeira versão: 7 janeiro de 2016, revisado em 22 agosto de 2016
---
```

Você também pode usar o cabeçalho para dizer ao R Markdown que ele seja processado para
HTML (padrão), PDF ou algum outro formato. Para que ele seja transformado em PDF, por exemplo, eu escrevi:

```
---
title: Usando R Markdown para anotações de aula
author: CRS
date: Primeira versão 7 janeiro de 2016, revisado em 22 agosto de 2016
output: pdf_document
---
```
Você pode adicionar uma tabela de conteúdos como uma opção para o tipo de saída.

```
---
title: Usando R Markdown para anotações de aula
author: CRS
date: Primeira versão 7 janeiro de 2016, revisado em 22 agosto de 2016
output:
  html_document:
    toc: true
---
```

* Para criar PDFs, um programa chamado `LaTeX` (veja abaixo) deve ser instalado no seu computador.
* Outros formatos de saída devem estar disponíveis. Veja `help (render)` no pacote `rmarkdown`.
* Existem muitas, muitas outras opções de formatação que podem ser dadas no
cabeçalho; consulte os principais arquivos de ajuda do R Markdown on-line.

# Hiperlinks e imagens

### Hiperlinks

Os hiperlinks (links) são ancorados (referenciados) por URLs e fáceis de usar: por exemplo, basta digitar a URL
http://www.stat.cmu.edu/~cshalizi/rmarkdown/rmarkdown.Rmd para obter a fonte do arquivo
deste documento. 

Hiperlinks referenciados no texto têm a [âncora entre colchetes e o link
entre parênteses](http://www.stat.cmu.edu/~cshalizi/rmarkdown/rmarkdown.Rmd).

```
Hiperlinks referenciados no texto têm a [âncora entre colchetes e o link
entre parênteses](http://www.stat.cmu.edu/~cshalizi/rmarkdown/rmarkdown.Rmd).
```

### Imagens

As imagens começam com um ponto de exclamação e, depois, vem o texto a ser usado
caso a imagem não possa ser carregada. Em seguida, o endereço do arquivo da imagem
(no mesmo diretório do seu documento) ou uma URL direto para ela (remotamente). Aqui estão dois
exemplos, um para uma imagem no diretório e outro para uma URL externa.

```
![Uma imagem local](cena-local.jpg)
![Uma imagem remota](http://apod.nasa.gov/apod/image/1302/ringshexagon_cassini_1016.jpg)
```
<!-- ###################### ERRO NA COMPILAÇÃO. ###########
![A local image](local-scene.jpg)
![A remote image](http://apod.nasa.gov/apod/image/1302/ringshexagon_cassini_1016.jpg)
-->

Não existe uma maneira de redimensionar imagens usando comandos próprios Markdown. 
No entanto, você pode usar o seguinte hack:

<pre><code>```{r, fig.retina=NULL, out.width=100, echo=FALSE}
knitr::include_graphics("http://apod.nasa.gov/apod/image/1302/ringshexagon_cassini_1016.jpg")
```</code></pre>

```{r, fig.retina=NULL, out.width=100, echo=FALSE}
knitr::include_graphics("http://apod.nasa.gov/apod/image/1302/ringshexagon_cassini_1016.jpg")
```
Esse código chama um comando R incluído no pacote `knitr`, com algumas opções sobre como o R será executado (descrito abaixo).

# Incluindo código

O legal do R Markdown é que ele também permite a você incluir seu código e o
executar automaticamente quando o documento for processado. E, de forma incomparável, inclui
os resultados desse código em seu documento. O código vem em duas variedades:
**chunks** (pedaços) de código ou código **inline**.

### Pedaços de código e seus resultados

Um **pedaço** de código é simplesmente um trecho isolado de código. Ele é precedido
por ` ``` {r} ` em uma linha e termina outra linha que diz ` ``` `.
O código fica no meio. Aqui, por exemplo, é um código que
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

### Código inline

A saída do seu código também pode ser muito bem incorporada no texto, usando o 
modo **inline**. Este código não é iniciado em uma linha, mas começa com
` `r ` e terminando com ` ` `. Usar o código inline é como este documento <-----
sabe que o conjunto de dados `cats` contém linhas `r nrow (cats)`
(` contém ` r nrow(gatos) ` linhas `), e que o peso médio dos corações das fêmeas
dos gatos é `r median(cats$Hwt[cats$Sex=="F"])` gramas (` `r median(cats$Hwt[cats$Sex=="F"])` `).

Observe que o código inline não exibe os comandos executados, apenas a saída deles.

### Visto, mas não ouvido

Os pedaços de código (exceto código inline) têm um monte de **opções** que modificam
a forma como eles são executados e como eles aparecem no documento. Estas opções podem vir depois
do `r` inicial e antes do fechamento `}`, que representa o início de um pedaço código. 
Uma das opções mais comuns desativa a impressão do código, porém, deixa os resultados isolados:
 ` ```{r, echo=FALSE} `

Outra opção executa o código, mas não inclui nem o texto do código nem a saída.
 ` ```{r, include=FALSE} `
  
Isso pode parecer bobo, mas pode ser útil para pedaços de código que configuram (setam) algo,
como carregar arquivos de dados ou estimativas de modelo inicial etc.


Outra opção imprime o código no documento, mas não o executa:
 ` ```{r, eval=FALSE} `
Isso também é útil se você quiser comentar sobre o código (de modo que ele fique bem formatado).

### Nomeando pedaços de código

Você pode atribuir nomes aos pedaços de código logo após a abertura, como
` ``` {r, clevername} `. Esse nome é usado para as imagens (ou outros arquivos)
que são gerados quando o documento é processado.

### Alterando tamanhos de imagem e alinhamentos

Há muitas opções para se ajustar as figuras que o
R produz. `fig.align` controla o **alinhamento** horizontal (esquerda, direita,
ou centro).

Ao produzir PDF, as opções `out.height` e` out.width` permitem que você especifique
a altura ou largura desejada da figura em polegadas, centímetros ou múltiplos
de comprimentos pré-definidos (`LaTeX`). Então, por exemplo, ` ``` r,
out.height = "3in"} ` força a imagem a 3 polegadas de altura, enquanto que ` ```r,
out.width = "0.48 \\ textwidth"} ` força a largura da imagem a ser um pouco menor do que
metade da largura total do texto na página (de modo que duas dessas imagens
se encaixam lado a lado). As próximas figuras ilustram isso.


```{r, echo=FALSE, fig.width=3, fig.align="center"}
plot(Hwt ~ Bwt, data=cats, xlab="Body weight (kg)",
     ylab="Heart weight (g)", sub="Linear scale")
plot(Hwt ~ Bwt, data=cats, log="xy", xlab="Body weight (kg)",
     ylab="Heart weight (g)", sub="Logarithmic scale")
```



### Tabelas

A impressão padrão de matrizes, tabelas e relacionados do R Markdown, sinceramente, é
feia. O pacote `knitr` contém um comando muito básico, `kable`, que irá
formatar uma matriz ou quadro de dados mais legalmente para exibição.

Compare:

```{r}
coefficients(summary(lm(Hwt ~ Bwt, data=cats)))
```

com

```{r}
library(knitr) # Só precisa disso uma vez!
kable(coefficients(summary(lm(Hwt ~ Bwt, data=cats))))
```

--- Pois é, os padrões do R fazem imprimir um número louco de casas decimais, mas
este não é o momento de discutir dígitos significativos, ou a função `signif`. <---

### "Caching" de pedaços de código (re-executando somente com modificações)

Por padrão, o R Markdown executa seu código de novo toda vez que você renderiza o
documento. Se algum trecho do seu código for lento, isso pode aumentar ainda mais o tempo de renderização.
Você pode, no entanto, pedir ao R Markdown para monitorar se um pedaço de código foi modificado e apenas re-executar este pedaço. Isso é chamado **caching** de pedaço de código.

```{r, cache=TRUE}
lm(Hwt ~ Bwt, data=cats)
```
A questão é que um pedaço de código que não se alterou pode invocar
resultados de pedaços anteriores, trechos modificados e logo nós precisaríamos re-executar os
pedaços desatualizados. Existem opções para informar manualmente ao R Markdown que "este
trecho depende de um fragmento anterior", mas geralmente é mais fácil deixar ele mesmo cuidar disso, definindo a opção `autodep=TRUE`.

1. Se você carregar um pacote com os comandos `library()` ou `require()`, o R
   Markdown não será inteligente o suficiente para verificar se o pacote mudou
   (ou realmente foi instalado, se você não o tiver instalado). Então, isso não vai
   lançar uma re-execução automática de um pedaço de código em cache.
2. Para forçar manualmente a re-execução de todos os pedaços de código, o mais fácil a se fazer é
   excluir o diretório que o R Markdown cria (algo como 
   _nome_do_arquivo_`_cache`) para armazenar o estado de todos os pedaços de código.
   
### Configuração de padrões para todos os pedaços de código

Você pode dizer para o R aplicar alguns padrões a todos os pedaços. Aqui estão os que eu geralmente uso:   

```{r, eval=FALSE}
# Precisamos do pacote knitr para definir opções de trechos de código
library(knitr)

# Opções do knitr para gerar código no relatório
# - Não imprime código
# - Salva os resultados de modo que os blocos de código não sejam novamente executados, a menos que o código mude (ele fica no cache),
# _ou_ um bloco relevante de código anterior seja modificado (autodep), mas não o re-executa se a
# única coisa que mudou forem comentários (cache.comments)
# - Não obstrua a saída do R com mensagens ou avisos (mensagem, aviso)
   # Isto _deixará_ mensagens de erro aparecendo no relatório gerado
opts_chunk$set(echo=FALSE,
               cache=TRUE, autodep=TRUE, cache.comments=FALSE,
               message=FALSE, warning=FALSE)
```

Assim, temos algumas opções adicionais além das que eu discuti, como não
re-executar um pedaço somente se os comentários foram mudados (`cache.comments =
FALSE`), deixando de receber mensagens e avisos. (Eu só recomendaria
suprimir avisos se você tiver certeza de que seu código está ok.) Eu, normalmente,
também usaria a opção `include = FALSE` a este ponto de configuração.

Você pode sobrescrever estes padrões definindo opções para trechos específicos.

### Mais Opções

Veja em [http://yihui.name/knitr/options/], para obter uma listagem completa das opções possíveis.


# Matemática no R Markdown

Como esta é uma aula de Estatística, é importante que você seja capaz de escrever expressões matemáticas,
muitas vezes longas séries delas. O R Markdown oferece a sintaxe para
exibir fórmulas e derivações matemáticas complexas, e exibi-las _muito_ lindamente. Assim como o código,
a notação matemática pode ser disposta inline ou como **exibições** (destacadas).

O código de matemática inline é marcado com um par de cifrões
(`$`), como em $\pi r^2$ ou $e^{i\pi}$.

```
O código de matemática inline é marcado com um par de cifrões
(`$`), como em $\pi r^2$ ou $e^{i\pi}$.
```

Já as expressões matemáticas são marcadas entre `\[` e `\]`, como em
\[
e^{i \pi} = -1
\]

```
Exibições matemáticas são marcadas com `\[` e `\]`, como em
\[
e^{i \pi} = -1
\]
```

Uma vez que seu texto está em modo matemático, o R Markdown faz o trabalho de
converter o trecho matemático para um programa diferente, chamado LaTeX[^latex].
Este é o sistema mais comum de composição de documentos matemáticos
nas ciências e tem sido usado há décadas. Ele é extremamente poderoso,
estável, disponível basicamente a todas as plataformas e completamente gratuito. 
Mas ele também pode se tornar, em seu poder total, um tanto complicado. Felizmente, para nossos propósitos, 
é bem simples.


### Elementos do modo matemático

* A maioria das letras será renderizada em itálico (compare: a vs. `a` vs. $a$; apenas
o último está em modo matemático). A composição das letras também segue as convenções da matemática, então, por exemplo, não as trate como só outra maneira de obter itálico. (Compare _velocidade_, em itálico simples, com $velocidade$, em notação matemática.)
* Letras gregas podem ser acessadas com a barra na frente de seus nomes, como `\alpha` para $\alpha$. Fazer a primeira letra em maiúscula te dá a letra maiúscula, como em `\Gamma` para $\Gamma$ vs. `\gamma` para $\gamma$. (As maiúsculas alpha e beta são as mesmas que as latinas A e B, portanto, não se precisa de comando especial para elas.)
* Existem outros para símbolos matemáticos de operações (em inglês):
    + `\times` para $\times$
    + `\cdot` para $\cdot$
    + `\leq` e `\geq` para $\leq$ and $\geq$
    + `\subset` e `\subseteq` para $\subset$ and $\subseteq$
    + `\leftarrow`, `\rightarrow`, `\Leftarrow`, `\Rightarrow` para $\leftarrow$, $\rightarrow$, $\Leftarrow$, $\Rightarrow$
    + `\approx`, `\sim`, `\equiv` for $\approx$, $\sim$, $\equiv$
    + Veja, também, http://web.ift.uib.no/Teori/KURS/WRK/TeX/symALL.html para uma
lista completa dos símbolos.  (http://tug.ctan.org/info/symbols/comprehensive/symbols-a4.pdf lista de _todos_ os símbolos disponíveis no `LaTeX`, incluindo muitos caracteres especiais não-matemáticos).
* Subscritos vêm depois de um caractere underscore, `_`, e sobrescritos vêm depois de um circunflexo, `^`, como `\beta_1` para $\beta_1$ ou `a^2` para $a^2$.
* As chaves são usadas para criar agrupamentos que devem ser mantidos em conjunto, como, por exemplo, `a_{ij}` para $a_{ij}$ (vs. `a_ij` para $a_ij$).
* Se você precisa de fonte normal (romana) no modo matemático, use `\mathrm`, como `t_{\mathrm{in}}^2` para $t_{\mathrm{in}}^2$.
* Se você quiser uma fonte estilo "quadro-negro" ou "cursiva" (ex.: conjuntos numéricos), use `\mathbb`, como `\mathbb{R}` para $\mathbb{R}$.
* Para texto em negrito, use `\mathbf`, como
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
* Nomes de funções são escritos, geralmente, em fonte normal mas espaçados de forma diferente: 
  ou seja, $\log{x}$, não $log x$. O `LaTeX` e, por consequência, o `R Markdown` também, tem muitas
  dessas funções e seus nomes iniciam com `\`.  Por exemplo:
  `\log`, `\sin`, `\cos`, `\exp`, `\min`, etc.  Use estas funções
  com o argumento entre chaves; isso permite ao `LaTeX` descobrir qual
  argumento usar e mantê-lo agrupado com o nome da função.  Então `\log{(x+1)}` é melhor que `\log (x+1)`.
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
que produzirá produzirá
\[
\sum_{i=1}^{n}{x_i^2}
\]
Os limites inferior e superior do somatório, após a `\sum`, são ambos opcionais.
Produtos e integrais funcionam de forma semelhante, com `\prod` e `\int`:
\[
n! = \prod_{i=1}^{n}{i}
\]
\[
\log{b} - \log{a} = \int_{x=a}^{x=b}{\frac{1}{x} dx}
\]
`\sum`, `\prod` and `\int` se ajustam automaticamente ao tamanho da expressão a qual são somados, multiplicados ou integrados.
* "Delimitadores", como parênteses ou chaves, podem se redimensionar automaticamente para se adaptar ao que eles têm em volta.   Para fazer isso, você precisa usar `\left` e `\right`,
como
```
\left( \sum_{i=1}^{n}{i} \right)^2 = \left( \frac{n(n-1)}{2}\right)^2 = \frac{n^2(n-1)^2}{4}
```
e será renderizado assim
\[
\left( \sum_{i=1}^{n}{i} \right)^2 = \left( \frac{n(n-1)}{2}\right)^2 = \frac{n^2(n-1)^2}{4}
\]
   + Para usar chaves como delimitadores, anteceda-as com barras como `\{` e `\}` para $\{$ e $\}$.
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
Observe que `&` envolve o meio de cada linha e cada uma delas (exceto a última) é encerrada com `\\`. Os lados esquerdo ou direito da equação podem estar em branco e o espaço será gerado:
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

(No `LaTeX`, o comando `\begin{eqnarray}` entra automaticamente no modo matemático, mas no
R Markdown precisa-se de um empurrãozinho.)

### Traduzindo matemática para o `LaTeX`

O `LaTeX` é projetado para que cada parte de uma expressão matemática tenha uma
relação próxima ao que você escreve. Ainda assim, de início, ele pode ser um
um pouco intimidador. O que muitos acham interessante é começar 
alguma página com código matemático impresso ou manuscrito e depois traduzi-la,
linha a linha, no `LaTeX`, processando para ver se ele saiu
direito (e, caso contrário, entender onde consertar). Se você precisa fazer expressões matemáticas para um
trabalho, pode ser uma boa ideia escrever as contas à mão e depois aproveitá-lo 
no `LaTeX`, se a aula o exige (como esta), ou não.
Eventualmente, com a prática, a tradução se tornará fluida e automática.
Algumas pessoas inovam ainda a matemática escrevendo no `LaTeX`.

### `LaTeX` não verifica a corretude

`LaTeX` não verifica se sua notação matemática está _certa_; ele apenas tenta
descobrir o que você está tentando dizer, bem o suficiente para re-digitar e melhorá-lo.
Assim, por exemplo, não há nenhum problema com o seguinte código:

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
verificam se sua operação matemática está correta. Pelo menos se você estiver trabalhando na subárea da Matemática,
a qual eles são projetados para lidar. Até onde eu sei, ninguém realmente os combinou com `LaTeX`.)

### Um pouco mais de conteúdo avançado no modo matemático: Novos Comandos

Uma das coisas que você pode fazer no `LaTeX` é criar seus próprios comandos (atalhos).
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
e então no modo matemático você pode escrever `\MeuParametro` e o `LaTeX` irá
traduzir isto para `\theta`. Se você decidir mais tarde que o seu parâmetro
vire `\beta`, ou mesmo `\mathrm{fred}`, basta alterar essa definição inicial
do novo comando, em vez de ter que usar cada `\theta` outra vez.

Novos comandos também podem receber um ou mais argumentos. Aqui está um comando útil
para probabilidade:
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
gerir mudanças; também torna seu texto mais fácil para você e para os outros.
Isto é como usar nomes compreensíveis para variáveis e funções em seus programas (da mesma forma que é
preterívei criar funções em vez de codificar longas linhas de comandos).


Também é possível definir novos nomes às funções que funcionem como `\log`,
novos operadores matemáticos, diagramas de desenho, etc., etc., mas isso vai além do proposto nessas notas.

### Instalando `LaTeX`

Se você exportar seu documento R Markdown para HTML, não precisará instalar
`LaTeX` em seu computador. Sim, porque o HTML inclui instruções para
navegadores, que então falam (por assim dizer) "Envie esses textos de aparência engraçada para 
[mathjax.org](http://www.mathjax.org), e ele te enviará de volta
belas imagens de equações". O site realmente executa o `LaTeX`.

Já se você quer produzir um PDF, aí, sim, você precisa ter o `LaTeX` instalado no seu
computador. A instalação depende da máquina. Para Macs, recomendo usar o pacote `MacTeX`, disponível em
https://tug.org/mactex/mactex-download.html. Para outros sistemas, veja os links de http://www.tug.org/begin.html.

# Juntando tudo: redigindo seu relatório em R Markdown

Você:
* instala o pacote `rmarkdown` e todas as suas dependências.
* instala o `LaTeX`, se precisa produzir um PDF.
* instala e configurou seu editor de texto favorito.
* cria um novo documento.
    + atribui-lhe um título, um autor e uma data.
* usa cabeçalhos para dividi-lo em seções específicas, seções entituladas e, possivelmente, sub-seções.
    + Segue im padrão comum: "Introdução", "Dados e Questões de Pesquisa", "Análise", "Resultados", "Conclusão".
    + Outro padrão comum: "Problema 1", "Problema 2", ..., "Créditos extra".
* Você escreve texto.
* Quando precisar, pode inserir notação matemática no texto ou mesmo elaboradas apresentações do tipo.
* Se precisar também, poderá inserir código em seu documento.
    + O código é executado (conforme necessário) quando você processa o documento.
    + Figuras, tabelas e outros resultados são inseridos automaticamente no documento e acompanham as alterações em seu código.
* De vez em quando, tente renderizar seu documento.
    + Quando (pensar que você) termina uma seção, aproveite para já criar outra.
    + Outra boa opção é se você fez alterações não triviais no código ou no texto.
* Seu documento foi processado com sucesso ou não.
    + Se o fez, e você gostou dos resultados, comemore alegremente e vá para sua próxima tarefa.
    + Se processou mas você não gostou dos resultados, pense sobre e tente corrigi-lo.
    + Se não processou, o R lhe dirá onde ele parou e, então, tente depurar de lá.

# Solução de problemas/coisas a se evitar

* Não ligue para `View` ou `help` no seu documento; estes são comandos interativos que não funcionam bem em scripts.
* "Funcionou no console do R, mas não gerou o documento": Quase certamente, você fez alguma coisa diferente *antes* do pedaço do código que está dando problema. Limpe seu espaço de trabalho no console e re-execute.
    + O R Studio mantém dois ambientes, ou espaços de trabalho, que ele usa para avaliar as expressões do R, a função de busca ou os nomes das variáveis, etc. Um deles é o ambiente global "usual" do console, que é compilado cumulativamente desde o início da sessão (a menos que você manipule deliberadamente, não faça isso a menos que você saiba o que está fazendo.) Toda vez que você usar o knit, no entanto, ele re-executa seu código no espaço de trabalho limpo, como se você tivesse começado R do zero. Isso significa que o código no knit faz o que você diz, e apenas isso. Se o seu código foi renderizado no knit, ele deve funcionar em qualquer computador; Fazer algo para rodar no console e que você não pode reproduzir é tentar a sorte.
* "Funciona quando eu rodo (abre a aplicação), mas não gera o documento": basicamente é o mesmo problema do "funcionou no console...". <-----
* Evite `attach` no console e no seu arquivo; Usá-lo é uma receita para criar erros difíceis de encontrar. Você ainda pode encurtar expressões usando `with`em vez disso.
* Você precisa do LaTeX para criar PDFs. Se você está tendo problemas ao fazer isso, tente mudar o formato de saída para HTML.
    + Tente corrigir a instalação do LaTeX mais tarde, quando você não tiver pressão de tempo; isto é realmente útil.
    + O LaTeX irá reclamar se você tentar imprimir coisas realmente enormes. Erros sobre "out of stack" ("fora da pilha"), ou "pandoc 43", são muitas vezes causados por isso. Não imprima coisas enormes. (Supressão de avisos e outras mensagens podem ajudar.)
* Quando você precisa carregar arquivos de dados ou usar o código de outra pessoa, use URLs absolutas, ao invés de criar cópias locais e carregá-las em seu disco.

# Leitura adicional

Para mais informações sobre o R Markdown, consulte http://rmarkdown.rstudio.com, em particular as páginas de ajuda mais detalhadas (em vez dos primeiros guias).

Para o `LaTeX`, a referência clássica é o livro de Leslie Lamport, *LaTeX: A Document Preparation System* (2ª edição, Reading, Mass .: Addison-Wesley, 1994). Esta não é, reconhecidamente, a leitura mais fácil do mundo. LaTeX, de Wikibooks, é mais acessível, online e gratuito.

O R Markdown baseia-se no pacote `knitr`, desenvolvido por Yihui Xie, para integração do R com `LaTeX`; veja http://yihui.name/knitr/ e, para obter a documentação completa, o livro de Xie *Dynamic Documents with R and knitr* (2ª edição, Boca Raton, Flórida, CRC Press, 2016).

Para uma explicação completa, divertida e completamente correta de porque "O processador de texto é uma ferramenta estúpida e grosseiramente ineficiente de se preparar texto para comunicação com os outros", veja http://ricardo.ecn.wfu.edu/~cottrell/wp. html.

[^latex]: na década de 1970, o grande cientista da computação Donald Knuth escreveu uma linguagem de marcação e o programa de renderização dessa linguagem, chamado `TeX` (pronuncia-se como "tec"), para escrever documentos matemáticos complexos. Na década de 1980, a cientista de computação Leslie Lamport aperfeiçoou o `TeX` de modo que ele se tornara bem mais fácil de usar e passou a se chamar LaTeX (pronunciando-se "la-tec").

# Agradecimentos

Ao [Prof. Howard Seltman](http://www.stat.cmu.edu/~hseltman/AboutMe.html) por sugestões; à [Drª. Uma Ravat](http://www.math.uiuc.edu/~umaravat/) por me mostrar o truque para re-dimensionar imagens; e a uma antiga postagem da [Profª. Jenny Bryan](http://www.stat.ubc.ca/~jenny/) sobre como incluir trechos literais de R.

## Notas da tradução
1. Alusão à <a name="nota1" href="https://en.wikipedia.org/wiki/Microsoft_Redmond_campus">Microsoft</a>
