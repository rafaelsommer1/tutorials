Processamento de imagens anatômicas
===================================

Objetivos
^^^^^^^^^

Este tópico se destina ao processamento de imagens anatomicas de pacientes com esclerose múltipla ou outras patologias desmielinizantes. Ao final do protocolo nosso objetivo é obter os seguintes dados:

- Mapa de lesões (probabilístico e binário)
- Mascaras de substância branca, substância cinzenta e LCR
- Volumetria normalizada de cérebro total, substância branca e substância cinzenta
- Volumetrias subcorticais normalizadas e absolutas
- Mapas corticais de volume, área e espessura com parcelações

Mapa de lesão
^^^^^^^^^^^^^
Inicialmente, costumo utilizar um script em R que realiza os seguintes procedimentos:

1. Extração de calota craniana
2. Normalização de sinal
3. Cálculo de mapas lesionais

Para chamar este script, necessitamos de pelo menos:

- Um T1 volumétrico
- Um Flair volumétrico
- Um T2

De dentro de uma pasta com os arquivos basta chamar:

.. code-block:: bash

    lesionMap t1.nii.gz t2.nii.gz flair.nii.gz

O processamento do script segue o seguinte algoritmo:

.. image:: imgs/lesion_seg.png

É importante a segmentação das lesões serem o primeiro passo, 
pois já realizamos o pré-processamento do T1 e o mapa de lesões será utilizado em análises posteriores, como volumetrias

O script de R que é chamado pelo comando **lesionMap** pode ser
visualizado em https://github.com/rafaelsommer1/neuroimage/blob/master/R/lesionMap.R,
caso seu mapa não fique adequado, é possível customizar os parâmetros do script