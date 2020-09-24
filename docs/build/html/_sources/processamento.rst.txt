Neuroimagem
===========

Softwares
^^^^^^^^^
| Os worflows mais importantes descritos nos documentos a seguir são baseados em funções de softwares externos que incluem principalmente:

- FMRIB Software Library (FSL) - https://fsl.fmrib.ox.ac.uk/fsl/fslwiki/FslInstallation
- MRtrix3 - https://www.mrtrix.org/download/
- Freesurfer - https://surfer.nmr.mgh.harvard.edu/fswiki/DownloadAndInstall
- R (fslr, oasis and myelinmap packages)

Todos sendo disponibilizados atualmente apenas para Linux e Mac


\* Para configuração dos pacotes de R checar no tópico de R

Para facilidadade de implementação, sugiro instalar os scripts desenvolvidos pelo grupo que podem ser encontrados em: https://github.com/rafaelsommer1/neuroimage. Para instalá-los basta:
 
.. code-block:: bash

  git clone https://github.com/rafaelsommer1/neuroimage.git
  cd neuroimage
  sudo echo "export SCRIPTS_RCS=`pwd`" >> ~/.bashrc
  sudo echo "export PATH=$PATH:`pwd`/bin" >> ~/.bashrc

Re-abra o terminal e teste:

.. code-block:: bash

  lesionMap
  >> Usage: lesionMap <t1> <t2> <flair>
  >> Call this script from the top of the files folder

Se houver este resultado, os scripts estão instalados, em caso de erro entrar em contato com rafaelcasommer@gmail.com

DICOM para Nifti
^^^^^^^^^^^^^^^^

Arquivos adquiridos na ressonância ficam disponibilizados em formato DICOM o que pode ser bastante util para armazenamento de informações de identificação, metadados, etc... Porém não são simples de analisar e não compartilhaveis, visto que possuem informações sigilosas dos pacientes. Portanto, grande parte dos softwares de neuroimagem trabalham com imagens de formato Nifti.

A documentação do formato pode ser encontrada em: https://nifti.nimh.nih.gov/

É importante então convertermos nossas imagens de dicom para nifti. Eu costumo utilizar o programa do mrtrix **mrconvert** para tal. Geralmente basta:

.. code-block:: bash

  mrconvert dicom_folder file.nii.gz

Sendo nifti_file o nome do arquivo desejado

Após, costumo sempre orientar as imagens conforme o FSL, visto que a conversão muitas vezes pode levar a alterações de orientação. Basta:

.. code-block:: bash

    fslreorient2std file.nii.gz file.nii.gz


Processamento de imagens anatômicas
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Este tópico se destina ao processamento de imagens anatomicas de pacientes com esclerose múltipla ou outras patologias desmielinizantes. Ao final do protocolo nosso objetivo é obter os seguintes dados:

- Mapa de lesões (probabilístico e binário)
- Mascaras de substância branca, substância cinzenta e LCR
- Volumetria normalizada de cérebro total, substância branca e substância cinzenta
- Volumetrias subcorticais normalizadas e absolutas
- Mapas corticais de volume, área e espessura com parcelações

Mapa de lesão
"""""""""""""""""""""""""""
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

O processamento do script segue:

.. image:: imgs/lesion_seg.png