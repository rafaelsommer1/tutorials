Passos iniciais
===============

Softwares
^^^^^^^^^
| Os worflows mais importantes descritos nos documentos a seguir são baseados em funções de softwares externos que incluem principalmente:

- FMRIB Software Library (FSL) - https://fsl.fmrib.ox.ac.uk/fsl/fslwiki/FslInstallation
- MRtrix3 - https://www.mrtrix.org/download/
- Freesurfer - https://surfer.nmr.mgh.harvard.edu/fswiki/DownloadAndInstall
- R (fslr, oasis and myelinmap packages)

Todos sendo disponibilizados atualmente apenas para Linux e Mac


\* Para configuração dos pacotes de R checar no tópico de R

Para facilidadade de implementação, sugiro instalar os scripts desenvolvidos pelo grupo que
podem ser encontrados em: https://github.com/rafaelsommer1/neuroimage. Para instalá-los via terminal faça o seguinte:
 
.. code-block:: bash

  $ git clone https://github.com/rafaelsommer1/neuroimage.git
  $ cd neuroimage
  $ sudo echo "export SCRIPTS_RCS=`pwd`" >> ~/.bashrc
  $ sudo echo "export PATH=$PATH:`pwd`/bin" >> ~/.bashrc

Re-abra o terminal e teste:

.. code-block:: bash

  $ lesionMap
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
