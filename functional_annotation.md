# Functional annotation of transcripts and identified coding regions using Trinotate and TransDecoder

Now we have a bunch of transcript sequences and have identified some subset of them that appear to be biologically interesting in that they're differentially expressed between our two conditions - but we don't really know what they are or what biological functions they might represent.  We can explore their potential functions by functionally annotating them using our Trinotate software and analysis protocol.  To learn more about Trinotate, you can visit the [Trinotate website](http://trinotate.github.io/).

Let's make sure that we're back in our 'workspace' directory:

    % cd ~/workspace

    % pwd

.

    /home/training/workspace



Now, create a Trinotate/ directory and relocate to it. We'll use this as our Trinotate computation workspace.

    % mkdir Trinotate

    % cd Trinotate

Make a shortcut to your Trinity.fasta file in this Trinotate directory, for sake of convenience:

    %  ln -s ../Trinity.fasta

## Bioinformatics analyses to gather evidence for potential biological functions

Below, we're going to run a number of different tools to capture information about our transcript sequences.


### Identification of likely protein-coding regions in transcripts

[TransDecoder](http://transdecoder.github.io/) is a tool we built to identify likely coding regions within transcript sequences.  It identifies long open reading frames (ORFs) within transcripts and scores them according to their sequence composition.  Those ORFs that encode sequences with compositional properties (codon frequencies) consistent with coding transcripts are reported.

Running TransDecoder is a two-step process.  First run the TransDecoder step that identifies all long ORFs.

    % /usr/local/src/TransDecoder/TransDecoder.LongOrfs -t Trinity.fasta -m 800

>Note, we're setting '-m 800' here only to focus workshop activities on a small set of longest orfs that encode at least 800 amino acids in length.  If you were to run this on your own personal data, you would leave the default setting and not specify -m.

Now, run the step that predicts which ORFs are likely to be coding.

    % /usr/local/src/TransDecoder/TransDecoder.Predict -t Trinity.fasta 

You'll now find a number of output files containing 'transdecoder' in their name:

    %  ls -1 |grep transdecoder
.

    Trinity.fasta.transdecoder.bed
    Trinity.fasta.transdecoder.cds
    Trinity.fasta.transdecoder.gff3
    Trinity.fasta.transdecoder.pep    
    Trinity.fasta.transdecoder_dir/


The file we care about the most here is the 'Trinity.fasta.transdecoder.pep' file, which contains the protein sequences corresponding to the predicted coding regions within the transcripts.

Go ahead and take a look at this file:

    %   less Trinity.fasta.transdecoder.pep

.

    >TRINITY_DN1001_c0_g1::TRINITY_DN1001_c0_g1_i1::g.297::m.297 TRINITY_DN1001_c0_g1::TRINITY_DN1001_c0_g1_i1::g.297  ORF type:complete len:912 (+) TRINITY_DN1001_c0_g1_i1:93-2828(+)
    MKSDFKFSNLLGTVYRQGNVQFSHDGNMLLSPVGNRISVFDLVNNKSFTFAYEHRKNIAT
    FDVNKQGTLLLSVDTDGRAILVNFKTRNVLHHFNFKDKCYSVKFSPDGRYFALAVGRFLQ
    IWKTPDVSQDRQFAPFVRYRVHAGHFQDITSFTWSHDSRFLLTTSKDLTSRVWSINSEDK
    ELVATTLAGHRDYVLGAYFNSTQEKIYTISKDGAVFTWEYISKAQKEGLDEEDLEDEDLS
    KLSWRITKKNFFYANQAKVKCCTFHINSNLLIVGFSNGEFRLYEMPEFVMVQQLSMGQNP
    VNTVSVNNSGEWLAFGSSKLGQLLVYEWQSESYILKQQGHFDATNSLTYSPDGSRVVTAA
    EDGKIKVWDVASGFCLATFEEHTSAVTAVQFAKKGQVLFSASLDGTVRAWDLIRYRNFRV
    FTATERVQFTCLAVEPSGEVVSAGSTDSFDVFVWSVQTGQLLDTLSGHEGPVSCLAFSME
    NAVLASASWDKTIRIWSIFGRSQQVEPLEVFADILAITITPDGKHVAVSTLKGQLTIFDI
    ASGKQIGNIDCRKDIISGRFLQDRFTSKNSERSKYFTTINYSFDGKSIIAGGNNNSICLY
    DVPNEVLLKRFIVSRNMNLNGTLEFLNSSRMTEAGSLDLIDSSGEYSDLEDRIDGSLPGS
    HRGGDMSTRSSRPEIRVTSVQFSPTANAFAAASTEGLLIYSIDETLIFDPFDLDIDITPQ
    ATLEVLAEKDYLTALVMAFRLNEEYLINKVYENVPVTQINSVCNQLPVVYVSRLLTFIGN
    FATTSQHIEFNLLWLKALLIAHGSFMKQHEHMFSSATRAVRRFIGRIAEDVTFLSATNKY
    AYRFLTSTSGKGADSSEEEIQNISDSSSSDEDDVVMQSDDDEDGEWIGFQEKKQQLALSE
    DDSESEDELLQ*
    >TRINITY_DN1005_c0_g1::TRINITY_DN1005_c0_g1_i1::g.298::m.298 TRINITY_DN1005_c0_g1::TRINITY_DN1005_c0_g1_i1::g.298  ORF type:complete len:814 (+) TRINITY_DN1005_c0_g1_i1:165-2606(+)
    MVANSMNLADILKDEVSLERVKELKDQLLKEKSTIDYQLSKESNKNYEAVQESIKLLNIS
    QKDVIEVKDQLSKVKTLSDESKSSISRYDIIFDATRMYEKVDMTSEIYDKIVAFSDTVEQ
    VNRMLDTELAQDGLETGCPYLIQIHYLLTTIRNFQDQMTIMANVSTDDVQRTCQKLFSKV
    SGLVDKFDQLLESLIYDIVEMIRAENYSLVVRLFKIIDFEEREDLRIEAIRNIIKKKEIE
    AEKSTFKKLPSSKNIGRLELESNSKALEYPTDQGLYQEIINGTITTRVQSRGYKNLLYNK
    IKQSIQEMFIEVRKEYDGDKKFDVLNNLDWVFNELLVVKDYVSKYSPPYWNIFDKYYQFY
    YDELHILINELVDAEPETIIILDIIDFDKTFQNTLVKDFGFKRKETKTVIGDTQKETLFK
    DYLNLIVIKMTEWLGNLQKTEFKTFKDRSIPPQSDAENLLLLEGTKTCFQMFSQQVEVAA
    GSSQAKILVGVIEKFSELIENRLSNWISVVDEEVRRLMKYNELYDLDPNAIAPENEVPGG
    LLEYVIALANDQMRAADYAMAIGSKYGAMVTKAYEKEIQTNIDNILDRFADVSQVCISAL
    LTIIFDDLKKPYSEIFSKTWYKGSQAQQISDTISEYLEDIKVLMNPVLYGLFMERLIENT
    ILGYIGALKYEHSIKNKNNKFLESVKRDFEIFYKLFATYIGSSDETIEIVKEKFEVMDYF
    MDLCCEPIDSVMGIWDNFLQRYPDVPVVILEFVLKSRKDIDRSRRKKLVQRAIDLSLRPE
    HLAFISSEEYEPSYLSNFTIKSAKKSEDVGDDY*
    ...


There are a few items to take notice of in the above peptide file. The header lines includes the protein identifier composed of the original transcripts along with 'm.(number)'.  The 'type' attribute indicates whether the protein is 'complete', containing a start and a stop codon; '5prime_partial', meaning it's missing a start codon and presumably part of the N-terminus; '3prime_partial', meaning it's missing the stop codon and presumably part of the C-terminus; or 'internal', meaning it's both 5prime-partial and 3prime-partial. You'll also see an indicator (+) or (-) to indicate which strand the coding region is found on, along with the coordinates of the ORF in that transcript sequence.

This .pep file will be used for various sequence homology and other bioinformatics analyses below.


### Sequence homology searches

Earlier, we ran blastx against our mini SWISSPROT datbase to identify likely full-length transcripts.  Let's run blastx again to capture likely homolog information, and we'll lower our E-value threshold to 1e-5 to be less stringent than earlier.

    % blastx -db ~/shared_ro/dbs/sprot.mini.pep \
             -query Trinity.fasta -num_threads 2 \
             -max_target_seqs 1 -outfmt 6 -evalue 1e-5 \
              > swissprot.blastx.outfmt6

>Note, blastx might take ~10 minutes to complete for this assembly.  Also, you would normally search the full swissprot database. Here we're searching a small relevant subset of Swissprot just to speed up the search in this workshop setting.

Now, let's look for sequence homologies by just searching our predicted protein sequences rather than using the entire transcript as a target:

    % blastp -query Trinity.fasta.transdecoder.pep \
             -db ~/shared_ro/dbs/sprot.mini.pep -num_threads 2 \
             -max_target_seqs 1 -outfmt 6 -evalue 1e-5 \
              > swissprot.blastp.outfmt6

Using our predicted protein sequences, let's also run a HMMER search against the Pfam database, and identify conserved domains that might be indicative or suggestive of function:

    % hmmscan --cpu 2 --domtblout TrinotatePFAM.out \
              ~/shared_ro/dbs/Pfam-A.hmm \
              Trinity.fasta.transdecoder.pep > pfam.log

>Note, hmmscan might also take about 5 to 10 minutes to complete.

### Computational prediction of sequence features

The signalP and tmhmm software tools are very useful for predicting signal peptides (secretion signals) and transmembrane domains, respectively.

To predict signal peptides, run signalP like so:

    %  signalp -f short -n signalp.out Trinity.fasta.transdecoder.pep > sigP.log

Take a look at the output file:

    %  less signalp.out

.
 
    ##gff-version 2
    ##sequence-name source  feature start   end     score   N/A ?
    ## -----------------------------------------------------------
    TRINITY_DN31_c0_g1::TRINITY_DN31_c0_g1_i1::g.552::m.552 SignalP-4.1     SIGNAL  1       17      0.713   .       .       YES
    TRINITY_DN339_c0_g1::TRINITY_DN339_c0_g1_i1::g.63::m.63 SignalP-4.1     SIGNAL  1       19      0.874   .       .       YES

>How many of your proteins are predicted to encode signal peptides?


To predict transmembrane domain predictions, run tmhmm like so:

    %  tmhmm --short < Trinity.fasta.transdecoder.pep > tmhmm.out

Take a look at the output:

    % less tmhmm.out

.

    TRINITY_DN56_c0_g1_i1|m.126     len=303 ExpAA=126.72    First60=16.21   PredHel=6       Topology=o44-66i100-119o129-148i155-177o187-209i222-241o
    TRINITY_DN56_c0_g2_i1|m.127     len=262 ExpAA=126.02    First60=23.86   PredHel=6       Topology=o5-24i59-78o88-107i114-136o146-168i181-200o


Those entries that have results contain output like so 'Topology=o5-24i59-78o88-107i114-136o146-168i181-200o' are the predicted transmembrane proteins. The number of helices in the transmembrane domain is listed under PredHel=(number) and the topology indicates the region within the protein sequence that spans the membrane from (i) inside to (o) outside the cell.


