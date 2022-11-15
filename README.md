# ⚙ Anotação de VCF somático utilizando VEP-esembl 105.0 ⚙
Script passo-a-passo para anotação de variantes de um arquivo VCF através da ferramenta _Ensembl Variant Effect Predictor_ (VEP). 

Tópicos:
- [Introdução](##Introdução)
- [Criação de plataforma para execução dos scrips](##Plataforma-de-execução)
- [Primeiros Passos](##Primeiros-Passos)
- [Mão na Massa](##Mão-na-Massa)

## 📃 Introdução
Um arquivo VCF (_Variant Call Format_) é um arquivo de dados usado que contém informações de variações de sequências de genes advindos de um DNA que passou pelo processo de sequenciamento de nova geração (NGS). Para o encontro dessas variantes existem diversas ferramentas que podem auxiliar em sua anotação e também associação de suas informações à bancos de dados afim de uma maior compreenção do que se quer estudar/analisar. 
Para o processamento desses dados, é possível seguir este tutorial com qualquer arquivo VCF que você possua, nós utilizamos como ferramenta suporte o Ensembl Variant Effect Predictor (VEP) para anotação. Mais sobre a ferramenta pode ser encontrado no GitHub da cientista de dados Keren Xu (https://github.com/XUKEREN) no repositório vcfannotatoR https://github.com/XUKEREN/vcfannotatoR).

## 💻 Plataforma de execução 
Antes de mais nada, para o desenvolvimento de uma pipeline é necessário que se utilize uma plataforma que suporte a leitura dos scripts. Neste tutorial foi escolhida a plataforma Google Colab (https://colab.research.google.com/). Através do link pode-se conhecer um pouco mais sobre como utilizar o Colab para a escrita e execução de scripts em Python. 
- Link para rápida criação de um script no Colab --> https://colab.research.google.com/#create=true
- Nomeie o título do seu arquivo onde está escrito *Untitled.ipynb* e em seguida você já pode começar o script!

## 🚶‍♂️ Primeiros Passos

 _1. Preparo inicial_ - Importe seu drive no Colab para localização e gerenciamento dos dados escrevendo na barra de trabalho (Terminal):
```
from google.colab import drive
drive.mount('/content/drive')
```
 _2. Verificação do local_ - Para que o Colab saiba onde está trabalhando utilize o código pwd:
```
!pwd
  ```
 _3. Resultado_ - O terminal deve apresentar como resultado do último código como /content:

![image](https://user-images.githubusercontent.com/99352577/202039441-2901185f-55da-4114-a4f2-2868e3bfe1f3.png)

## 🔨 Mão na Massa
Agora vamos começar baixando os arquivos necessários! Entenda os processos:

 _1. Instalando modulo em pandas:_
```
import pandas as pd
import csv
```
 _2. Instalando pacotes para execução do VEP usando o código apt install:_

```
!sudo apt install unzip curl git libmodule-build-perl libdbi-perl libdbd-mysql-perl build-essential zlib1g-dev

```

 _3. Download do VEP utilizando o código wget:_
  
```
!wget -c https://github.com/Ensembl/ensembl-vep/archive/refs/tags/105.0.tar.gz
```
 _4. Descompactando os arquivos tar.gz:_
```
!tar -zxvf 105.0.tar.gz
```
 _5. Utilizar cd para entrar no diretório do VEP e INSTALL.pl para instalar:_
  
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


## 🧬Baixando o arquivo VCF
Agora vamos usar um VCF como exemplo. 

  _1.Baixe o arquivo *WP312.filtered.vcf.gz.* no Colab:_

![image](https://user-images.githubusercontent.com/99352577/202040401-5eb872d4-664c-4f62-8df3-7931dfb2a083.png)

  _2.Crie um diretório e transfira o arquivo para ele:_
```
%%bash
mkdir dados_vcf
````
  _3. Mova o arquivo VCF para o diretório criado, apenas para organização dos dados:_
````
!mv /content/WP312.filtered.vcf.gz /content/dados_vcf
````
  
## 📝Anotando as variantes com o VEP
Tudo alinhado, vamos as anotações!



