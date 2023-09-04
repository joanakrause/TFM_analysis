# TFM_analysis. Adding short reads into a constrained tree


#### 1. Reverse complement R2 read obtained from Sanger sequencing using AliView
#### 2. Create a fasta file with 3-5 corallicolid 18S sequences (full length)
#### 3. Add our R1 and Reverse complemented R2 to this fasta
#### 4. Align sequences using MUSCLE
```
muscle -in corallicolid_seqs_myseq.fa -out coralicollid_seqs_myseq.aligned.fa
```
#### 5. Examine alignment in AliView and see where our R1 and R2 fall. See where they overlap and merge them to generate a longer sequence

#### 6. Use muscle to add new sequences to the alignment that was used to build the constrained tree

```
muscle -in corallicolid_seqs_myseq_merged.fa -out coralicollid_seqs_myseq_merged.aligned.fa
muscle -profile -in1 EukBank_Api_constrained_tree3.aligned.fa -in2 coralicolid_seqs_myseq_merged.fa -out EukBank_epa_apis_all.aligned.fa
```

#### 7. Run RAXML-EPA to add our sequence to the constrained tree
```
raxmlHPC -T 2 -m GTRCAT -f v -G 0.2 -n EPARUN -s EukBank_epa_apis_all.aligned.fa -t RAxML_bipartitions.EukBank_Api_constrained_3.tre
```
#### 8. Make the generated file readable for FigTree
```
sed 's/QUERY___//g' RAxML_labelledTree.EPARUN | sed 's/\[I[0-9]*\]//g' > RAxML_placement_tree_apis_Joana.tre
```
