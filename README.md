## SEQLIM
Multiple Sequence Alignment Editing

# Description
SEQLIM is a python script for manipulating biological sequences. It enables concatenating and formatting Multiple Sequence Alignments.
 
# Installation

* Install Python 2.7 or higher, Python installers are available at https://www.python.org/.
* Download seqlim.py somewhere in your `PATH`, and test it.
```
$ seqlim.py -h
```
* Or move to a folder where seqlim.py is in and use `python` command.
```
$ python seqlim.py -h
```

# Examples

* Suppose that there are two files in FASTA format at `./test/fasta`.
 
 
`Locus1.fasta`

    >Escheri1
    CCUGGCGGCCGUAGCGCGGUGGUCCCACCUGACCCCAUGCCGAACUCAGAAGUGAAAC
    >Enteroc1
    UGUGGUGGCGAUAGCGAGAAGGAUACACCUGUUCCCAUGCCGAACACAGAAGUUAAGC
 
 
`Locus2.fasta`

    >Escheri2
    UAGCGCCGAUGGUAGUGUGGGGUCUCCCCAUGCGAGAGUAGGGAACU--GCCAGGC
    >Enteroc2
    UAGCGCCGAUUGUAGUGAAGGGUUUCCCUUUGUGAGAGUAGG--ACGUCGCCACGC
 

* Concatenate these files horizontally.

```
$ seqlim.py cath ./test/fasta
>Escheri1
CCUGGCGGCCGUAGCGCGGUGGUCCCACCUGACCCCAUGCCGAACUCAGAAGUGAAACUA
GCGCCGAUGGUAGUGUGGGGUCUCCCCAUGCGAGAGUAGGGAACU--GCCAGGC
>Enteroc1
UGUGGUGGCGAUAGCGAGAAGGAUACACCUGUUCCCAUGCCGAACACAGAAGUUAAGCUA
GCGCCGAUUGUAGUGAAGGGUUUCCCUUUGUGAGAGUAGG--ACGUCGCCACGC
``` 

* Concatenate these files vertically.

```
$ seqlim.py catv ./test/fasta
>Escheri1
CCUGGCGGCCGUAGCGCGGUGGUCCCACCUGACCCCAUGCCGAACUCAGAAGUGAAAC
>Enteroc1
UGUGGUGGCGAUAGCGAGAAGGAUACACCUGUUCCCAUGCCGAACACAGAAGUUAAGC
>Escheri2
UAGCGCCGAUGGUAGUGUGGGGUCUCCCCAUGCGAGAGUAGGGAACU--GCCAGGC
>Enteroc2
UAGCGCCGAUUGUAGUGAAGGGUUUCCCUUUGUGAGAGUAGG--ACGUCGCCACGC
``` 

* Set alternative input sequence format after `-infmt`. SEQLIM accepts `phylip`, `phy`, or `ph` for PHYLIP format; `nexus`, `nex`, or `nxs` for NEXUS format.

```
$ seqlim.py -infmt phylip cath ./test/phylip
>Escheri1
CCUGGCGGCCGUAGCGCGGUGGUCCCACCUGACCCCAUGCCGAACUCAGAAGUGAAAC
>Enteroc1
UGUGGUGGCGAUAGCGAGAAGGAUACACCUGUUCCCAUGCCGAACACAGAAGUUAAGC
>Escheri2
UAGCGCCGAUGGUAGUGUGGGGUCUCCCCAUGCGAGAGUAGGGAACU--GCCAGGC
>Enteroc2
UAGCGCCGAUUGUAGUGAAGGGUUUCCCUUUGUGAGAGUAGG--ACGUCGCCACGC
``` 
 
* Set output format after `-outfmt`.
``` 
$ seqlim.py -outfmt phylip cath ./test/fasta
 2 114
Escheri1     CCUGGCGGCC GUAGCGCGGU GGUCCCACCU GACCCCAUGC CGAACUCAGA AGUGAAACUA
Enteroc1     UGUGGUGGCG AUAGCGAGAA GGAUACACCU GUUCCCAUGC CGAACACAGA AGUUAAGCUA

             GCGCCGAUGG UAGUGUGGGG UCUCCCCAUG CGAGAGUAGG GAACU--GCC AGGC
             GCGCCGAUUG UAGUGAAGGG UUUCCCUUUG UGAGAGUAGG --ACGUCGCC ACGC
```
 
* The line and block lengths of sequences can be adjusted using `-line\_length` and `-block\_length`, respectively.
```
$ python seqlim.py -outfmt phylip -line_length 50 -block_length 5 cath ./test/fasta
 2 114
Escheri1     CCUGG CGGCC GUAGC GCGGU GGUCC CACCU GACCC CAUGC CGAAC UCAGA
Enteroc1     UGUGG UGGCG AUAGC GAGAA GGAUA CACCU GUUCC CAUGC CGAAC ACAGA

             AGUGA AACUA GCGCC GAUGG UAGUG UGGGG UCUCC CCAUG CGAGA GUAGG
             AGUUA AGCUA GCGCC GAUUG UAGUG AAGGG UUUCC CUUUG UGAGA GUAGG

             GAACU --GCC AGGC
             --ACG UCGCC ACGC
```

* Save an output.
``` 
$ seqlim.py -o ./test/temp/concatenated.fasta cath ./test/fasta
```
 
* Just convert a sequence format to another.
```
$ seqlim.py -outfmt phylip -o ./test/temp/converted.phylip cnvt ./test/fasta/locus1.fasta
``` 
 
* Convert all sequence files in `./test/fasta` to another format (PHYLIP) and save them in `./test/phylip`.
```
$ seqlim.py -o ./test/phylip -outfmt phylip cnvt ./test/fasta
``` 
 
