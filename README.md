
Description of the workflow which was used in the manuscript “Wolbachia in Antarctic terrestrial invertebrates: absent or undiscovered?”


# Step 1
# Data download
fastq-dump --split-files <SRR_id.fastq>

# Compress obtained files
gzip <SRR_id.fastq>

# Check integrity of compressed file
gzip -v -t <SRR_id.fastq.gz>

# Step 2
# Profile each sample with mOTU3 profiler 

motus profile -f <SRR_id_1.fastq.gz> -r <SRR_id_2.fastq.gz> -o <SRR_id_3mg_RelativeAbundance.tab> -u -q -g 3 -t 10 -n <SRR_id_3mg_id>  -M SRR_id.3mg_relAbund

# Step 3
# Profile samples with Kraken2

kraken2 --db ~/databases/kraken2_modified/db_05_2024_standart --threads 40 --report <SRR_id._kraken2_profile.txt> --use-names --classified-out ${ff%_1.fastq.gz}_Classified_concat.fastq.gz --minimum-base-quality 20 --gzip-compressed <SRR_id.fastq.gz>

#




