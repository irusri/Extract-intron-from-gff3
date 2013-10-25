###Extract intron feature gff3 from gene gff3 file
========================
There several ways to extract intron gff3 file using gene gff3 file. We can use GBrowse databases to dump intron feature gff3 file. But we need load gff3 file into MySQL first.
######Option 1:
Load the gff3 file into MySQL:   
<code>
perl [bp_bulk_load.pl](https://github.com/bioperl/bioperl-live/blob/master/scripts/Bio-DB-GFF/bp_bulk_load_gff.pl) -u [uname]-p [pass] -d  [gbrowse_database] [input.gff3/input.fasta]  
</code>
Extract the gff3:  
<code>
perl [make_intron_feature.pl](http://popgenie.org/script/make_intron_feature.pl) -u [uname]-p [pass] -db [gbrowse_database] -o [output.gff3]
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
awk '/intron/{print}' output.gff3 > filtered.gff3
</code>

