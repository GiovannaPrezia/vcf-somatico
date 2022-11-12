# 🧬Anotação de VCF somático utilizando VEP-esembl 105.0🧬
Script passo-a-passo para anotação de variantes de um arquivo VCF através da ferramenta _Ensembl Variant Effect Predictor_ (VEP). 
 
## Introdução
Um arquivo VCF (_Variant Call Format_) é um arquivo de dados usado a para armazenar variações de sequências de genes advindos de um DNA que passou pelo processo de sequenciamento de nova geração (NGS). Para o encontro dessas variantes existem diversas ferramentas que podem auxiliar em sua anotação e também associação das informações dessas variantes com bancos de dados afim de uma maior compreenção do que vem sendo estudado. 
Para o processamento desses dados, é possível seguir este tutorial com qualquer arquivo VCF que você possua, nós utilizamos como ferramenta suporte o Ensembl Variant Effect Predictor (VEP) para anotação. Mais sobre a ferramenta pode ser encontrado no GitHub da cientista de dados Keren Xu (https://github.com/XUKEREN/vcfannotatoR)

## Início de tudo
Para o desenvolvimento de uma pipeline é necessário que se utilize uma plataforma que suporte a leitura dos scripts. Neste tutorial foi escolhida a plataforma Google Colab (https://colab.research.google.com/). Através do link pode-se conhecer um pouco mais sobre como utilizar o Colab para a escrita e execução de scripts em Python.
