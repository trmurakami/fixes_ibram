# fixes_ibram

Instalar o librecat/catmandu no Ubuntu/Debian

    sudo apt-get update
    sudo apt-get install libcatmandu*-perl

Criar o diretório data

    mkdir data

Rodar o comando do librecat/catmandu

    catmandu convert MARC to MARC --fix fixes/fixes_ibram.txt < data/NOMEDOARQUIVODEORIGEM.mrc > data/NOMEDOARQUIVODEDESTINO.mrc