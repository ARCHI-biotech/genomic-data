use strict;
use warnings;
use Bio::Tools::Vcf;

my $vcf_file = 'CEU POPULATION.vcf';

my $vcf_parser = Bio::Tools::Vcf->new(-file => $vcf_file);

while (my $vcf_record = $vcf_parser->next()) 
{
    my $chrom = $vcf_record->chrom();
    my $pos   = $vcf_record->pos();
    my $ref   = $vcf_record->ref();  # Reference allele (e.g., 'A')
    my $alt   = $vcf_record->alt();  # Alternate allele (e.g., 'T')
    my $qual  = $vcf_record->qual();
    my $allele = ($alt) ? '1' : '0';  # If ALT exists: '1', else '0' (REF)
    print join("\t", $chrom, $pos, $ref, $alt, $allele, $qual), "\n";
}

$vcf_parser->close();
