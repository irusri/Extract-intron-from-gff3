###Extract intron feature gff3 from gene_exon gff3 file
========================
There are several ways to extract intron feature gff3 from gene_exon gff3 file. We can use GBrowse databases to dump intron based gff3 file as a first option.
######Option 1:
Load the gff3 file into MySQL:   
<code>
perl [bp_bulk_load.pl](https://github.com/bioperl/bioperl-live/blob/master/scripts/Bio-DB-GFF/bp_bulk_load_gff.pl) -u [uname]-p [pass] -d  [gbrowse_database] [input.gff3/input.fasta]  
</code>
Extract intron feature gff3:  
<code>
perl [make_intron_feature.pl](http://v22.popgenie.org/script/make_intron_feature.pl) -u [uname]-p [pass] -db [gbrowse_database] -o [output.gff3]
</code>

[Here](http://galaxy.popgenie.org:8080/u/chanaka/h/extract-intron) is the final result.

######Option 2:
This is an alternative solution without using GBrowse and MySQL.
First we need to download and install the latest version of [misopy](https://pypi.python.org/pypi/misopy) and [gffutils](https://github.com/seandavi/GFFutils).  
<code>
python [extract_intron_gff3_from_gff3.py](https://raw.github.com/irusri/Extract-intron-from-gff3/master/scripts/extract_intron_gff3_from_gff3.py) [input.gff3] [output.gff3]
</code>

Finally we need to filter and sort the output gff3 file  
<code>
awk '/intron/{print}' output.gff3 | sort -k 1,1 -k4,2n   > processed_intron.gff3
</code>

######Option 3:
If you don't like to type commands, you can use the [PlantGeIE Galaxy extract intron feature tool](http://galaxy.popgenie.org:8080/tool_runner?tool_id=extract_intron_gff3). Final result similar to [this](http://galaxy.popgenie.org:8080/u/chanaka/h/extract-intron-gff3)
