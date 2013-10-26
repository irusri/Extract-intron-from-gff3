###Extract intron feature gff3 from gene_exon gff3 file
========================
There are several ways to extract intron feature gff3 from gene_exon gff3 file. We can use GBrowse databases to dump intron based gff3 file as a first option.
######Option 1:
Load the gff3 file into MySQL:   
<pre>
perl [bp_bulk_load.pl](https://github.com/bioperl/bioperl-live/blob/master/scripts/Bio-DB-GFF/bp_bulk_load_gff.pl) -u [uname]-p [pass] -d  [gbrowse_database] [input.gff3/input.fasta]  
</pre>
Extract intron feature gff3:  
<pre>
perl [make_intron_feature.pl](http://v22.popgenie.org/script/make_intron_feature.pl) -u [uname]-p [pass] -db [gbrowse_database] -o [output.gff3]
</pre>

[Here](http://galaxy.popgenie.org:8080/u/chanaka/h/extract-intron) are the final results.

######Option 2:
This is an alternative solution without using GBrowse and MySQL.
First we need to download and install the latest version of [misopy](https://pypi.python.org/pypi/misopy) and [gffutils](https://github.com/seandavi/GFFutils).  
<pre>
python [extract_intron_gff3_from_gff3.py](https://raw.github.com/irusri/Extract-intron-from-gff3/master/scripts/extract_intron_gff3_from_gff3.py) [input.gff3] [output.gff3]
</pre>

Finally we need to filter and sort the output gff3 file  
<pre>
awk '/intron/{print}' output.gff3 | sort -k 1,1 -k4,2n   > processed_intron.gff3
</pre>

######Option 3:
If you don't like to type commands, you can use the [PlantGeIE Galaxy extract intron feature tool](http://galaxy.popgenie.org:8080/tool_runner?tool_id=extract_intron_gff3). Final results similar to [this](http://galaxy.popgenie.org:8080/u/chanaka/h/extract-intron-gff3).  
Before:  
<pre>
Chr01	phytozome8_0	gene	2906	6646	.	-	.	ID=Potri.001G000200;Name=Potri.001G000200  
Chr01	phytozome8_0	mRNA	2906	6646	.	-	.	ID=PAC:27045395;Name=Potri.001G000200.1;  
Chr01	phytozome8_0	exon	6501	6646	.	-	.	ID=PAC:27045395.exon.1;Parent=PAC:27045395;    
Chr01	phytozome8_0	CDS	6501	6644	.	-	0	ID=PAC:27045395.CDS.1;Parent=PAC:27045395;   
Chr01	phytozome8_0	five_prime_UTR	6645	6646	.	-	.	ID=PAC:27045395.five_prime_UTR.1; 
Chr01	phytozome8_0	exon	3506	3928	.	-	.	ID=PAC:27045395.exon.2;Parent=PAC:27045395;  
Chr01	phytozome8_0	CDS	3506	3928	.	-	0	ID=PAC:27045395.CDS.2;Parent=PAC:27045395;    
Chr01	phytozome8_0	exon	2906	3475	.	-	.	ID=PAC:27045395.exon.3;Parent=PAC:27045395;  
</pre>  
After:  
<pre>
Chr01	phytozome8_0	intron	3476	3505	.	.	.	ID=Potri.001G000200;Parent=PAC:27045395  
Chr01	phytozome8_0	intron	3929	6500	.	.	.	ID=Potri.001G000200;Parent=PAC:27045395  
</pre>
