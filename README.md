# ⚙ Anotação de VCF somático utilizando VEP-esembl 105.0 ⚙
Script passo-a-passo para anotação de variantes de um arquivo VCF através da ferramenta _Ensembl Variant Effect Predictor_ (VEP). 

Tópicos:
- [Introdução](#-introdução)
- [Criação de plataforma para execução dos scrips](#-plataforma-de-execução)
- [Primeiros Passos](#%EF%B8%8F-primeiros-passos)
- [Mão na Massa](#-mão-na-massa)
- [Baixando arquivos para execução](#baixando-o-arquivo-vcf)
- [Anotando as variantes com o VEP](#anotando-as-variantes-com-o-vep)
- [Analisando o resultado com o pandas](#analisando-o-resultado-com-o-pandas)


## 📃 Introdução
Um arquivo VCF (_Variant Call Format_) é um arquivo de dados usado que contém informações de variações de sequências de genes advindos de um DNA que passou pelo processo de sequenciamento de nova geração (NGS). Para o encontro dessas variantes existem diversas ferramentas que podem auxiliar em sua anotação e também associação de suas informações à bancos de dados afim de uma maior compreenção do que se quer estudar/analisar. 
Para o processamento desses dados, é possível seguir este tutorial com qualquer arquivo VCF que você possua, nós utilizamos como ferramenta suporte o Ensembl Variant Effect Predictor (VEP) para anotação. 
- Mais sobre a ferramenta pode ser encontrado através dos links:
  - https://www.ensembl.org/info/docs/tools/vep/index.html 
  - https://github.com/Ensembl/ensembl-vep
- Também através do GitHub da cientista de dados Keren Xu (https://github.com/XUKEREN) no repositório vcfannotatoR https://github.com/XUKEREN/vcfannotatoR).

## 💻 Plataforma de execução 
Antes de mais nada, para o desenvolvimento de uma pipeline é necessário que se utilize uma plataforma que suporte a leitura dos scripts. Neste tutorial foi escolhida a plataforma Google Colab (https://colab.research.google.com/). Através do link pode-se conhecer um pouco mais sobre como utilizar o Colab para a escrita e execução de scripts em Python, útil para a execução deste tutorial. 
- Link para rápida criação de um script no Colab --> https://colab.research.google.com/#create=true
- Nomeie o título do seu arquivo onde está escrito *Untitled.ipynb* e em seguida você já pode começar o script!.

## 🚶‍♂️ Primeiros Passos

 _1. Preparo inicial_ - Importe seu drive no Colab para localização e gerenciamento dos dados escrevendo na barra de trabalho (Terminal):
```
from google.colab import drive
drive.mount('/content/drive')
```
 _2. Verificação do local_ - Para que o Colab saiba onde está trabalhando utilize o código `pwd`:
```
!pwd
  ```
 _3. Resultado_ - O terminal deve apresentar como resultado do último código como `/content`:

![image](https://user-images.githubusercontent.com/99352577/202039441-2901185f-55da-4114-a4f2-2868e3bfe1f3.png)

## 🔨 Mão na Massa
Agora vamos começar baixando os arquivos necessários! Entenda os processos:

 _1. Instalando modulo em pandas:_
```
import pandas as pd
import csv
```
 _2. Instalando pacotes para execução do VEP usando o código `apt install`:_

```
!sudo apt install unzip curl git libmodule-build-perl libdbi-perl libdbd-mysql-perl build-essential zlib1g-dev

```

 _3. Download do VEP utilizando o código `wget`:_
  
```
!wget -c https://github.com/Ensembl/ensembl-vep/archive/refs/tags/105.0.tar.gz
```
 _4. Descompactando os arquivos `tar.gz`:_
```
!tar -zxvf 105.0.tar.gz
```
 _5. Utilizar cd para entrar no diretório do VEP e `INSTALL.pl` para instalar:_
  
```
!cd ensembl-vep-105.0
./INSTALL.pl --NO_UPDATE
```

- *Você pode colar todos os comandos a partir do passo 2 em uma mesma célula e executar! (Recomendado instalar o módulo pandas separadamente)*

```
%%bash
sudo apt install unzip curl git libmodule-build-perl libdbi-perl libdbd-mysql-perl build-essential zlib1g-dev
wget -c https://github.com/Ensembl/ensembl-vep/archive/refs/tags/105.0.tar.gz
tar -zxvf 105.0.tar.gz
cd ensembl-vep-105.0
./INSTALL.pl --NO_UPDATE 
```

- *Para verificar se tudo deu certo digite:*

```
%%bash
cd ensembl-vep-105.0
./vep
```
- *Seu resultado deve ter esse cabeçalho:*

![image](https://user-images.githubusercontent.com/99352577/202039139-9f90f685-98a5-4be0-922e-b00a4e951630.png)

O Colab salva seus arquivos em seu próprio disco, a partir desse momento ele deve estar se apresentando dessa maneira:

![image](https://user-images.githubusercontent.com/99352577/202040299-e9732c77-6e8e-4421-b2a6-10f9793929b0.png)


## 🧬Baixando arquivos para execução
Para o teste de execução do tutorial disponibilizamos um VCF. É necessário fazer o download deste arquivo presente aqui no git:

- Arquivo em VCF para teste

  _1.Vamos começar fazendo o download do arquivo `WP312.filtered.vcf.gz.` no Colab:_

![image](https://user-images.githubusercontent.com/99352577/202040401-5eb872d4-664c-4f62-8df3-7931dfb2a083.png)

  _2.Crie um diretório com o comando `mkdir` e transfira o arquivo para ele:_
```
%%bash
mkdir dados_vcf
````
  _3. Mova o arquivo VCF para o diretório criado utilizando o comando `mv`, apenas para organização dos dados:_
````
!mv /content/WP312.filtered.vcf.gz /content/dados_vcf
````

- Arquivo FASTA da referência

 _4. Também vai ser necessário fazer o download de um arquivo de sequência contendo a referência da espécie de estudo, no caso vamos baixar a ref hg19 humana usando o comando `wget`:
 	obs: Desta vez pode ser um processo mais demorado (cerca de 10m) tendo em vista que o arquivo possui 2,9 GB;_
````
!wget -c https://data.broadinstitute.org/snowman/hg19/Homo_sapiens_assembly19.fasta
```` 

  _5.Crie um diretório para a referência:_
```
%%bash
mkdir referencia_fasta
````

  _3. Mova o arquivo VCF para o diretório criado utilizando o comando `mv`, apenas para organização dos dados:_
````
!mv /content/Homo_sapiens_assembly19.fasta  /content/referencia_fasta
````

## 📝Anotando as variantes com o VEP
Tudo alinhado, vamos as anotações! Primeiramente, vamos entender os comandos que utilizaremos:
Através do link (https://rest.ensembl.org/#VEP) é possível entender os comandos e seus `outputs/saídas`.
No nosso script:
 - `fork` : quantos núcleos o Colab vai usar para executar o programa;
 - `i` : de `input`, é o local onde o programa resgata o arquivo para iniciar a execução;
 - `o` : de `output`, como o arquivo será salvo no final;
 - `dir_cache` : é o cache do diretório do arquivo;
 - `fasta` : resgata o arquivo em `fasta` da referência (baixada anteriormente);
 - `offline` : possibilidade de execução offline;
 - `refseq` : código que busca a referência;
A partir de `--pick` você seleciona aquilo que deseja identificar em seus dados, na tabela das variantes que será gerado a partir do seu VCF. Através dos links inclusos na [Introdução](#-introdução), sobre o programa VEP, você consegue identificar filtros que pode adicionar para a sua análise. 

- Comando exemplo para execução: 

````
%%bash
./ensembl-vep-105.0/vep \
  --fork 4 \
  -i /content/dados_vcf/WP312.filtered.vcf.gz \
  -o /content/dados_vcf/WP312.output-vep.vcf.tsv \
  --dir_cache /content \
  --fasta /content/referencia_fasta/Homo_sapiens_assembly19.fasta  \
  --cache --offline --assembly GRCh37 --refseq  \
	--pick --pick_allele --force_overwrite --tab --symbol --check_existing --variant_class --everything --filter_common \
  --fields "Uploaded_variation,Location,Allele,Existing_variation,HGVSc,HGVSp,SYMBOL,Consequence,IND,ZYG,Amino_acids,CLIN_SIG,PolyPhen,SIFT,VARIANT_CLASS,FREQS" \
  --individual all
  
````
## 🐼Analisando o resultado com o pandas
Agora utilizaremos o pandas (biblioteca de software criada para a linguagem Python para manipulação e análise de dados) que nos permitira visualizar os dados gerados pelo VEP:

 _- Mova o arquivo VCF para o diretório criado utilizando o comando `mv`, apenas para organização dos dados:_
````
tabela = pd.read_csv('/content/dados_vcf/WP312.output-vep.vcf.tsv', sep='\t', skiprows=38)
df = pd.DataFrame(tabela)
df
````

O seu resultado deve ser uma tabela assim:
![image](https://user-images.githubusercontent.com/99352577/202541504-3d507785-6709-49e5-95d9-f95b02576580.png)


