# 🧬Anotação de VCF somático utilizando VEP-esembl 105.0🧬
Script passo-a-passo para anotação de variantes de um arquivo VCF através da ferramenta _Ensembl Variant Effect Predictor_ (VEP). 

Tópicos:
- [Introdução](##Introdução)
- [Criação de plataforma para execução dos scrips](##Plataforma-de-execução)
- [Primeiros passos](##Preparo-do-ambiente)

## Introdução
Um arquivo VCF (_Variant Call Format_) é um arquivo de dados usado a para armazenar variações de sequências de genes advindos de um DNA que passou pelo processo de sequenciamento de nova geração (NGS). Para o encontro dessas variantes existem diversas ferramentas que podem auxiliar em sua anotação e também associação das informações dessas variantes com bancos de dados afim de uma maior compreenção do que vem sendo estudado. 
Para o processamento desses dados, é possível seguir este tutorial com qualquer arquivo VCF que você possua, nós utilizamos como ferramenta suporte o Ensembl Variant Effect Predictor (VEP) para anotação. Mais sobre a ferramenta pode ser encontrado no GitHub da cientista de dados Keren Xu (https://github.com/XUKEREN) no repositório vcfannotatoR https://github.com/XUKEREN/vcfannotatoR).

## Plataforma de execução 
Antes de mais nada, para o desenvolvimento de uma pipeline é necessário que se utilize uma plataforma que suporte a leitura dos scripts. Neste tutorial foi escolhida a plataforma Google Colab (https://colab.research.google.com/). Através do link pode-se conhecer um pouco mais sobre como utilizar o Colab para a escrita e execução de scripts em Python. 
- Link para rápida criação de um script no Colab --> https://colab.research.google.com/#create=true
- Nomeie o título do seu arquivo onde está escrito *Untitled2.ipynb* e em seguida você já pode começar o script!

## Preparo do Ambiente
  _1. Preparo inicial_ - Importe seu drive no Colab para localização e gerenciamento dos dados escrevendo na barra de trabalho (Terminal):
```
  from google.colab import drive
  drive.mount('/content/drive')
```
_2. Verificação do local_ - Para que o Colab saiba onde está trabalhando utilize o código pwd:
```
  !pwd
  ```
_3. Resultado_ - O terminal deve apresentar como resultado do último código como /content
