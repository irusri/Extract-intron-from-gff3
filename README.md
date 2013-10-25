##Extract-intron-from-gff3
========================

There several ways to extract intron gff3 file using gene gff3 file. We can use GBrowse databases to dump intron feature gff3 file. But we need load gff3 file into MySQL first.
Load the gff3 file into MySQL: 
<code>
perl [bp_bulk_load.pl](https://github.com/bioperl/bioperl-live/blob/master/scripts/Bio-DB-GFF/bp_bulk_load_gff.pl) -u [uname]-p [pass] -d  [gbrowse_database] [input.gff3/input.fasta]  
</code>
Extract the gff3:  
<code>
perl [make_intron_feature.pl](ftp://popgenie.org/popgenie/Populus_trichocarpa/v2.2_current/scripts/) -u [uname]-p [pass] -db [gbrowse_database] -o [output.gff3]
</code>

However we can extract intron feature gff3 file without using MySQL database:


