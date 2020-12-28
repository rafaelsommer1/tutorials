Processamento de imagens por tensor de difusão
==============================================

Pré-Processamento
^^^^^^^^^^^^^^^^^

Formatos utilizados em difusão
""""""""""""""""""""""""""""""

Aqui abusaremos das bibliotecas do FSL e MrTrix
O primeiro ponto importante será o formato **.mif** que a biblioteca do MrTrix lança mão,
permitindo armazenar as grades de difusão junto com as imagens e facilitando a manipulação destes arquivos
Por exemplo,

Ao transformarmos um DICOM de difusão em nifti, com:

.. code::

    mrconvert dti_folder dti.nii.gz

Obteremos:

1. Arquivo de imagem **dti.nii.gz**
2. Matrix de vetores dos gradientes **file.bvec**
3. Vetor de bvalues **file.bval**

Enquanto podemos apenas realizar:

.. code::

    mrconvert dcm_folder dti.mif

Obtendo apenas um arquivo **dti.mif** com todas estas informações internamente
armazenadas

Finalmente, saiba que ao trabalhar com FSL utilizaremos majoritariamente
os arquivos niftis junto com as respectivas matrizes, e ao utilizarmos o MrTrix
podemos apenas usar um arquivo .mif

Correções de distorções
"""""""""""""""""""""""




Tractografia global e conectoma
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Co-registro de DWI e T1
"""""""""""""""""""""""


Modelagem tecidual
""""""""""""""""""



Freesurfer recon
""""""""""""""""

Converter labels do Freesurfer
""""""""""""""""""""""""""""""

.. code:: 

    labelconvert labelconvert $FREESURFER_HOME/subjects/subject/mri/aparc+aseg.mgz $FREESURFER_HOME/FreeSurferColorLUT.txt \
    /usr/local/anaconda3/share/mrtrix3/labelconvert/fs_default.txt subject_parcels.mif

