```{bash}
# check for duplicates in fasta files, concatenate all fasta files into one 
# sed removes everything after space in defline
# awk  prevents redundant proteins
# grep removes created newline
zcat *_protein.faa.gz |\
    sed -e 's/^\(>[^[:space:]]*\).*/\1/' |\
    awk -v RS=">" '!a[$0]++ { print ">"$0; }' - |\
    grep -Ev '^\s*$|^>\s*$' |\
    gzip > one_faa.gz
```
https://askubuntu.com/a/1125418
