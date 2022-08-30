# Pangenome

Pangenome analysis


# Conectarse

~~~
ssh nombre@servidior
password
~~~
{: .language-bash}

Moverse a la carpeta

~~~
cd carpeta
~~~
{: .language-bash}


## Make blast

Concatenar archivos y correr BLAST.

~~~
cat Haydee/data/*.faa > all-genomes.faa
cd ../Blast/output-blast/
makeblastdb -in ../../data/all-genomes.faa -dbtype nucl -out ../blast/database/all-genomes
~~~
{: .language-bash}

~~~
cat: /home/betterlab/Haydee/data/all-genomes.faa: input file is output file

Adding sequences from FASTA; added 27811 sequences in 4.72535 seconds.
~~~
{: .output}


~~~
makeblastdb -in 2692915.4.faa -dbtype nucl -out ../blast/database/2692915.4
~~~
{: .language-bash}


~~~
blastn -db ../database/all-genomes -query ../../data/all-genomes.faa -outfmt "6 qseqid sseqid pident length mismatch gapopen qstart qend sstart send evalue bitscore"
~~~
{: .language-bash}

~~~
Argument "query". File is not accessible:  `../database/2692915.4'

~~~
{: .output}
