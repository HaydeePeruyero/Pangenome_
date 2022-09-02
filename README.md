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

Concatenar archivos y correr BLAST con la opción de `prot` porque son Pangenomas.

~~~
cat Haydee/data/*.faa > all-genomes.faa
cd ~/Haydee/blast/output-blast/
makeblastdb -in ~/Haydee/data/all-genomes.faa -dbtype prot -out ~/Haydee/blast/database/all-genomes
~~~
{: .language-bash}

~~~
cat: /home/betterlab/Haydee/data/all-genomes.faa: input file is output file
Adding sequences from FASTA; added 27811 sequences in 4.72535 seconds.
~~~
{: .output}

~~~
#blastp blastp -query ~/Haydee/data/all-genomes.faa -db ~/Haydee/blast/all-genomes -outfmt "6" > all-genomes.blast
#Algunas de las posibles opciones: "6 qseqid sseqid pident length mismatch gapopen qstart qend sstart send evalue bitscore"
#Para dejar corriendo en la terminal
nohup blastp -query ~/Haydee/data/all-genomes.faa -db ~/Haydee/blast/all-genomes -outfmt "6" > all-genomes.blast &
~~~
{: .language-bash}

Copiar los archivos a local desde otra terminal.
~~~
scp servidor@servidor:/home/betterlab/Haydee/blast/all-genomes.blast .
~~~
{: .language-bash}

Default values for output:
~~~
-outfmt "6 qseqid sseqid pident length mismatch gapopen qstart qend sstart send evalue bitscore"
~~~
{: .language-bash}

  * qseqid: Query Seq-id
  * sseqid: Subject Seq-id
  * pident: Percentage of identical matches
  * length: Alignment length
  * mismatch Number of mismatches
  * gapopen: Number of gap openings
  * qstart: Start of alignment  in query
  * qend: End of alignment in query
  * sstart: Start of alignment in subject
  * send: End if alignment in subject
  * evalue: Expect value
  * bitscore: Bit score
  
Explore de dataset.

~~~
data <- read.delim("~/Pangenome/all-genomes.blast", header=FALSE)
head(data)
~~~
{: .language-bash}

~~~
                   V1                     V2      V3 V4 V5 V6 V7 V8 V9 V10      V11 V12
1 fig|2692915.4.peg.1    fig|2692915.4.peg.1 100.000 88  0  0  1 88  1  88 1.45e-62 183
2 fig|2692915.4.peg.1 fig|2692915.4.peg.7369  97.727 88  2  0  1 88  1  88 1.88e-61 180
3 fig|2692915.4.peg.1 fig|2692915.4.peg.3260  79.310 87 18  0  1 87  1  87 6.97e-47 153
4 fig|2692915.4.peg.1 fig|2692915.4.peg.1536  67.045 88 29  0  1 88  1  88 1.08e-41 132
5 fig|2692915.4.peg.1 fig|2692915.4.peg.1153  64.045 89 30  1  1 87  1  89 4.03e-39 132
6 fig|2692915.4.peg.1 fig|2692915.4.peg.5246 100.000 51  0  0  1 51  1  51 1.59e-33 108
~~~
{: .output}

