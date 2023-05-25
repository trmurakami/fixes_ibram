# fixes_ibram

Instalar o librecat/catmandu no Ubuntu/Debian

    sudo apt-get update
    sudo apt-get install libcatmandu*-perl

Criar o diretório data

    mkdir data

Rodar o comando do librecat/catmandu

    catmandu convert MARC to MARC --fix fixes/fixes_ibram.txt < data/NOMEDOARQUIVODEORIGEM.mrc > data/NOMEDOARQUIVODEDESTINO.mrc

# Excluir todos os arquivos no Koha

    sudo su
    mysql -u root

    use koha_ibict
    SET FOREIGN_KEY_CHECKS=0;
    TRUNCATE items;
    TRUNCATE deleteditems;
    TRUNCATE biblioitems;
    TRUNCATE biblio;
    TRUNCATE deletedbiblioitems;
    TRUNCATE deletedbiblio;
    TRUNCATE biblio_metadata;
    TRUNCATE deletedbiblio_metadata;
    TRUNCATE auth_header;
    TRUNCATE sessions;
    TRUNCATE zebraqueue;

    SET FOREIGN_KEY_CHECKS=1;

    quit

# Importar registros no Koha

    cd /usr/share/koha/bin/migration_tools
    ./bulkmarcimport.pl -d -commit 1000 -file /var/www/html/fixes_ibram/data/result_20230525.mrc

# Reindexar o Zebra

    export PERL5LIB=/usr/share/koha/lib
    export KOHA_CONF=/etc/koha/sites/ibict/koha-conf.xml
    koha-rebuild-zebra -f -v ibict
