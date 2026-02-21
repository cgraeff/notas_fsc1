# notas_fsc1
Notas de Física 1

Os arquivos nesse repositório são os códigos-fonte necessários para produzir
minhas notas de aula de Física 1 utilizando LaTeX. Se você deseja obter uma
cópia do PDF diretamente, no repositório existe uma cópia que é atualizada
regularmente, mas não em todas as revisões intermediárias.

## Licença
Os arquivos deste repositório são distribuidos de acordo com a licença Creative
Commons Atribuição-NãoComercial-CompartilhaIgual 4.0 Internacional
(http://creativecommons.org/licenses/by-nc-sa/4.0/deed.pt_BR).

## Obtenção de uma cópia, produção do PDF
Para obter uma cópia, você pode baixá-la em
`https://github.com/cgraeff/notas_fsc1` (tanto em versão PDF, quanto os arquivos
para gerar o PDF).

Para gerar o PDF, é necessária uma distribuição TeX. Versões existem para todos
os sistemas operacionais, porém nas instruções abaixo vou detalhar os passos
assumindo o sitema operacional GNU/Linux Fedora, pois ele é gratuito (e é o que
eu uso). Deve ser possível gerar o PDF em outros sistemas operacionais, mas não
tenho ideia de como fazer isso, ou de quanto trabalho isso vai dar.

### Como obter uma cópia dos arquivos
Para obter uma cópia mais facilmente, basta executar em um terminal o comando
```
git clone https://github.com/cgraeff/notas_fsc1.git
```

### Pacotes necessários para gerar o arquivo PDF
Uma série de pacotes que não fazem parte da instalação usual do TeXLive são
necessários para poder gerar o arquivo PDF. Em particular no Fedora tenho os
seguintes pacotes (nem todos são necessários para essas notas de aula):
```
texlive
texlive-beamertheme-metropolis
texlive-biblatex
texlive-braket
texlive-calrsfs
texlive-ccicons
texlive-collection-langgreek
texlive-collection-langportuguese
texlive-epstopdf
texlive-exam
texlive-exsheets
texlive-hardwrap
texlive-hyphenat
texlive-lgreek
texlive-lipsum
texlive-mathcomp
texlive-mdframed
texlive-numprint
texlive-revtex
texlive-revtex4
texlive-standalone
texlive-textgreek
texlive-tikz-3dplot
texlive-tikz-qtree
texlive-titlesec
texlive-tkz-euclide
texlive-tufte-latex
texlive-units
gnuplot-latex
biber
```

No Debian, são os seguintes pacotes:
```
texlive
texlive-latex-extra
texlive-lang-greek
texlive-lang-portuguese
texlive-latex-extra
biber
texlive-science
texlive-fonts-extra
gnuplot-data
```

### Como gerar o arquivo PDF
Para gerar o arquivo PDF, é necessário executar o comando `pdflatex` com a opção
`-shell-escape`:
```
pdflatex -shell-escape NotasFisica1.tex
```
A primeira execução será mais demorada, uma vez que é necessário gerar todas
as figuras. Ao modificar o texto de um capítulo, é interessante desabilitar
o processamento dos demais capítulos, caso contrário o processamento das figuras
pode ser muito demorado. (A modificação da ordem, ou a adição de figuras novas
pode levar ao reprocessamento de todas as figuras subsequentes, o que leva a uma
demora desnecessária ao processar todos os capítulos.)

Após executar o `pdflatex` uma vez, devemos gerar a bibliografia através do
comando `biber`:
```
biber main
```
seguido do comando `pdflatex -shell-escape NotasFisica1.tex` mais algumas vezes (até que
o próprio comando pare de pedir para ser executado novamente).

Para resolver problemas com pacotes de hifenização, pode ser útil remover os diretórios .texlive20??/ presentes no diretório do usuário e/ou executar os comandos
```
sudo fmtutil --all -sys
```
ou
```
fmtutil --all -user
```
ou os mesmos comandos com as opções `--missing --refresh` e `-sys` ou `-user`.

### Exluir arquivos desnecessários
Uma maneira simples de excluir os arquivos de log, figuras temporárias, etc, (arquivos ignorados segundo os filtros contidos no .gitignore) é
excluir todos os arquivos que não foram adicionados ao git através de
```
git clean -x
```
ou 
```
git clean -X
```
para excluir os arquivos ignorados e manter os criados manualmente e que ainda não foram "commited".

