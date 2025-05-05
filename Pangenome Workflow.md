# Mycetohabitans Pangenome Workflow

- **File and directory arrangement**
    
    ```
    .
    ├── 1.5_fix-fastas.sh
    ├── 1_process-gbk.sh
    ├── 2.5_import_functions.sh
    ├── 2_make-contig-db.sh
    ├── 4_genome-storage.sh
    ├── 5_make-pangenome-omggggggg.sh
    ├── ANI
    │   ├── fastANI_alignment_fraction.newick
    │   ├── fastANI_alignment_fraction.txt
    │   ├── fastANI_ani.newick
    │   ├── fastANI_ani.txt
    │   ├── fastANI_mapping_fragments.newick
    │   ├── fastANI_mapping_fragments.txt
    │   ├── fastANI_total_fragments.newick
    │   └── fastANI_total_fragments.txt
    ├── ANI.out
    ├── April21_WG-FREQUENCY.txt
    ├── April21_WG-PRESENCE-ABSENCE.txt
    ├── contigdbs
    │   ├── B10.db
    │   ├── B12.db
    │   ├── B13.db
    │   ├── B14.db
    │   ├── B1.db
    │   ├── B203.db
    │   ├── B23.db
    │   ├── B29.db
    │   ├── B2.db
    │   ├── B34.db
    │   ├── B3.db
    │   ├── B46.db
    │   ├── B47.db
    │   ├── B48.db
    │   ├── B49.db
    │   ├── B50.db
    │   ├── B514.db
    │   ├── B51.db
    │   ├── B52.db
    │   ├── B53.db
    │   ├── B55.db
    │   ├── B58.db
    │   ├── B5.db
    │   ├── B60.db
    │   ├── B62.db
    │   ├── B75.db
    │   ├── B82.db
    │   ├── B8.db
    │   └── filelist.txt
    ├── diamond-log-file.txt
    ├── fastas
    │   ├── B10.fa
    │   ├── B12.fa
    │   ├── B13.fa
    │   ├── B14.fa
    │   ├── B1.fa
    │   ├── B203.fa
    │   ├── B23.fa
    │   ├── B29.fa
    │   ├── B2.fa
    │   ├── B34.fa
    │   ├── B3.fa
    │   ├── B46.fa
    │   ├── B47.fa
    │   ├── B48.fa
    │   ├── B49.fa
    │   ├── B50.fa
    │   ├── B514.fa
    │   ├── B51.fa
    │   ├── B52.fa
    │   ├── B53.fa
    │   ├── B55.fa
    │   ├── B58.fa
    │   ├── B5.fa
    │   ├── B60.fa
    │   ├── B62.fa
    │   ├── B75.fa
    │   ├── B82.fa
    │   ├── B8.fa
    │   └── filelist.txt
    ├── fix_fastas.out
    ├── funcitonal_annotation.out
    ├── functions
    │   ├── B10.txt
    │   ├── B12.txt
    │   ├── B13.txt
    │   ├── B14.txt
    │   ├── B1.txt
    │   ├── B203.txt
    │   ├── B23.txt
    │   ├── B29.txt
    │   ├── B2.txt
    │   ├── B34.txt
    │   ├── B3.txt
    │   ├── B46.txt
    │   ├── B47.txt
    │   ├── B48.txt
    │   ├── B49.txt
    │   ├── B50.txt
    │   ├── B514.txt
    │   ├── B51.txt
    │   ├── B52.txt
    │   ├── B53.txt
    │   ├── B55.txt
    │   ├── B58.txt
    │   ├── B5.txt
    │   ├── B60.txt
    │   ├── B62.txt
    │   ├── B75.txt
    │   ├── B82.txt
    │   └── B8.txt
    ├── genbanks
    │   ├── B10.gb
    │   ├── B12.gb
    │   ├── B13.gb
    │   ├── B14.gb
    │   ├── B1.gb
    │   ├── B203.gb
    │   ├── B23.gb
    │   ├── B29.gb
    │   ├── B2.gb
    │   ├── B34.gb
    │   ├── B3.gb
    │   ├── B46.gb
    │   ├── B47.gb
    │   ├── B48.gb
    │   ├── B49.gb
    │   ├── B50.gb
    │   ├── B514.gb
    │   ├── B51.gb
    │   ├── B52.gb
    │   ├── B53.gb
    │   ├── B55.gb
    │   ├── B58.gb
    │   ├── B5.gb
    │   ├── B60.gb
    │   ├── B62.gb
    │   ├── B75.gb
    │   ├── B82.gb
    │   ├── B8.gb
    │   └── filelist.txt
    ├── genecalls
    │   ├── B10.txt
    │   ├── B12.txt
    │   ├── B13.txt
    │   ├── B14.txt
    │   ├── B1.txt
    │   ├── B203.txt
    │   ├── B23.txt
    │   ├── B29.txt
    │   ├── B2.txt
    │   ├── B34.txt
    │   ├── B3.txt
    │   ├── B46.txt
    │   ├── B47.txt
    │   ├── B48.txt
    │   ├── B49.txt
    │   ├── B50.txt
    │   ├── B514.txt
    │   ├── B51.txt
    │   ├── B52.txt
    │   ├── B53.txt
    │   ├── B55.txt
    │   ├── B58.txt
    │   ├── B5.txt
    │   ├── B60.txt
    │   ├── B62.txt
    │   ├── B75.txt
    │   ├── B82.txt
    │   └── B8.txt
    ├── genomesdbs
    │   ├── external-genomes.txt
    │   └── GENOMES.db
    ├── make_contig_dbs.out
    ├── makegenomedb.out
    ├── pangenome.out
    ├── process_genbanks.out
    ├── setups
    │   ├── kegg_setup
    │   │   ├── BRITE
    │   │   │   ├── ko00001
    │   │   │   ├── ko00194
    │   │   │   ├── ko00199
    │   │   │   ├── ko00535
    │   │   │   ├── ko00536
    │   │   │   ├── ko00537
    │   │   │   ├── ko01000
    │   │   │   ├── ko01001
    │   │   │   ├── ko01002
    │   │   │   ├── ko01003
    │   │   │   ├── ko01004
    │   │   │   ├── ko01005
    │   │   │   ├── ko01006
    │   │   │   ├── ko01007
    │   │   │   ├── ko01008
    │   │   │   ├── ko01009
    │   │   │   ├── ko01011
    │   │   │   ├── ko01504
    │   │   │   ├── ko02000
    │   │   │   ├── ko02022
    │   │   │   ├── ko02035
    │   │   │   ├── ko02042
    │   │   │   ├── ko02044
    │   │   │   ├── ko02048
    │   │   │   ├── ko03000
    │   │   │   ├── ko03009
    │   │   │   ├── ko03011
    │   │   │   ├── ko03012
    │   │   │   ├── ko03016
    │   │   │   ├── ko03019
    │   │   │   ├── ko03021
    │   │   │   ├── ko03029
    │   │   │   ├── ko03032
    │   │   │   ├── ko03036
    │   │   │   ├── ko03037
    │   │   │   ├── ko03041
    │   │   │   ├── ko03051
    │   │   │   ├── ko03100
    │   │   │   ├── ko03110
    │   │   │   ├── ko03200
    │   │   │   ├── ko03210
    │   │   │   ├── ko03310
    │   │   │   ├── ko03400
    │   │   │   ├── ko04030
    │   │   │   ├── ko04031
    │   │   │   ├── ko04040
    │   │   │   ├── ko04050
    │   │   │   ├── ko04052
    │   │   │   ├── ko04054
    │   │   │   ├── ko04090
    │   │   │   ├── ko04091
    │   │   │   ├── ko04121
    │   │   │   ├── ko04131
    │   │   │   ├── ko04147
    │   │   │   ├── ko04515
    │   │   │   ├── ko04812
    │   │   │   └── ko04990
    │   │   ├── hierarchies.json
    │   │   ├── HMMs
    │   │   │   ├── Kofam.hmm
    │   │   │   ├── Kofam.hmm.h3f
    │   │   │   ├── Kofam.hmm.h3i
    │   │   │   ├── Kofam.hmm.h3m
    │   │   │   └── Kofam.hmm.h3p
    │   │   ├── ko_list.txt
    │   │   ├── KO_REACTION_NETWORK
    │   │   │   ├── ko_data.tsv
    │   │   │   ├── ko_entries.tar.gz
    │   │   │   ├── ko_info.txt
    │   │   │   └── ko_list.txt
    │   │   ├── modules
    │   │   │   ├── M00001
    │   │   │   ├── M00002
    │   │   │   ├── M00003
    │   │   │   ├── M00004
    │   │   │   ├── M00005
    │   │   │   ├── M00006
    │   │   │   ├── M00007
    │   │   │   ├── M00008
    │   │   │   ├── M00009
    │   │   │   ├── M00010
    │   │   │   ├── M00011
    │   │   │   ├── M00012
    │   │   │   ├── M00013
    │   │   │   ├── M00014
    │   │   │   ├── M00015
    │   │   │   ├── M00016
    │   │   │   ├── M00017
    │   │   │   ├── M00018
    │   │   │   ├── M00019
    │   │   │   ├── M00020
    │   │   │   ├── M00021
    │   │   │   ├── M00022
    │   │   │   ├── M00023
    │   │   │   ├── M00024
    │   │   │   ├── M00025
    │   │   │   ├── M00026
    │   │   │   ├── M00027
    │   │   │   ├── M00028
    │   │   │   ├── M00029
    │   │   │   ├── M00030
    │   │   │   ├── M00031
    │   │   │   ├── M00032
    │   │   │   ├── M00033
    │   │   │   ├── M00034
    │   │   │   ├── M00035
    │   │   │   ├── M00036
    │   │   │   ├── M00037
    │   │   │   ├── M00038
    │   │   │   ├── M00039
    │   │   │   ├── M00040
    │   │   │   ├── M00042
    │   │   │   ├── M00043
    │   │   │   ├── M00044
    │   │   │   ├── M00045
    │   │   │   ├── M00046
    │   │   │   ├── M00047
    │   │   │   ├── M00048
    │   │   │   ├── M00049
    │   │   │   ├── M00050
    │   │   │   ├── M00051
    │   │   │   ├── M00052
    │   │   │   ├── M00053
    │   │   │   ├── M00055
    │   │   │   ├── M00056
    │   │   │   ├── M00057
    │   │   │   ├── M00058
    │   │   │   ├── M00059
    │   │   │   ├── M00060
    │   │   │   ├── M00061
    │   │   │   ├── M00063
    │   │   │   ├── M00064
    │   │   │   ├── M00065
    │   │   │   ├── M00066
    │   │   │   ├── M00067
    │   │   │   ├── M00068
    │   │   │   ├── M00069
    │   │   │   ├── M00070
    │   │   │   ├── M00071
    │   │   │   ├── M00072
    │   │   │   ├── M00073
    │   │   │   ├── M00074
    │   │   │   ├── M00075
    │   │   │   ├── M00076
    │   │   │   ├── M00077
    │   │   │   ├── M00078
    │   │   │   ├── M00079
    │   │   │   ├── M00081
    │   │   │   ├── M00082
    │   │   │   ├── M00083
    │   │   │   ├── M00085
    │   │   │   ├── M00086
    │   │   │   ├── M00087
    │   │   │   ├── M00088
    │   │   │   ├── M00089
    │   │   │   ├── M00090
    │   │   │   ├── M00091
    │   │   │   ├── M00092
    │   │   │   ├── M00093
    │   │   │   ├── M00094
    │   │   │   ├── M00095
    │   │   │   ├── M00096
    │   │   │   ├── M00097
    │   │   │   ├── M00098
    │   │   │   ├── M00099
    │   │   │   ├── M00100
    │   │   │   ├── M00101
    │   │   │   ├── M00102
    │   │   │   ├── M00103
    │   │   │   ├── M00104
    │   │   │   ├── M00106
    │   │   │   ├── M00107
    │   │   │   ├── M00108
    │   │   │   ├── M00109
    │   │   │   ├── M00110
    │   │   │   ├── M00112
    │   │   │   ├── M00113
    │   │   │   ├── M00114
    │   │   │   ├── M00115
    │   │   │   ├── M00116
    │   │   │   ├── M00117
    │   │   │   ├── M00118
    │   │   │   ├── M00119
    │   │   │   ├── M00120
    │   │   │   ├── M00121
    │   │   │   ├── M00122
    │   │   │   ├── M00123
    │   │   │   ├── M00124
    │   │   │   ├── M00125
    │   │   │   ├── M00126
    │   │   │   ├── M00127
    │   │   │   ├── M00128
    │   │   │   ├── M00129
    │   │   │   ├── M00130
    │   │   │   ├── M00131
    │   │   │   ├── M00132
    │   │   │   ├── M00133
    │   │   │   ├── M00134
    │   │   │   ├── M00135
    │   │   │   ├── M00136
    │   │   │   ├── M00137
    │   │   │   ├── M00138
    │   │   │   ├── M00140
    │   │   │   ├── M00141
    │   │   │   ├── M00142
    │   │   │   ├── M00143
    │   │   │   ├── M00144
    │   │   │   ├── M00145
    │   │   │   ├── M00146
    │   │   │   ├── M00147
    │   │   │   ├── M00148
    │   │   │   ├── M00149
    │   │   │   ├── M00150
    │   │   │   ├── M00151
    │   │   │   ├── M00152
    │   │   │   ├── M00153
    │   │   │   ├── M00154
    │   │   │   ├── M00155
    │   │   │   ├── M00156
    │   │   │   ├── M00157
    │   │   │   ├── M00158
    │   │   │   ├── M00159
    │   │   │   ├── M00160
    │   │   │   ├── M00161
    │   │   │   ├── M00162
    │   │   │   ├── M00163
    │   │   │   ├── M00165
    │   │   │   ├── M00166
    │   │   │   ├── M00167
    │   │   │   ├── M00168
    │   │   │   ├── M00169
    │   │   │   ├── M00170
    │   │   │   ├── M00171
    │   │   │   ├── M00172
    │   │   │   ├── M00173
    │   │   │   ├── M00174
    │   │   │   ├── M00175
    │   │   │   ├── M00176
    │   │   │   ├── M00307
    │   │   │   ├── M00308
    │   │   │   ├── M00309
    │   │   │   ├── M00338
    │   │   │   ├── M00344
    │   │   │   ├── M00345
    │   │   │   ├── M00346
    │   │   │   ├── M00356
    │   │   │   ├── M00357
    │   │   │   ├── M00358
    │   │   │   ├── M00363
    │   │   │   ├── M00364
    │   │   │   ├── M00365
    │   │   │   ├── M00366
    │   │   │   ├── M00367
    │   │   │   ├── M00368
    │   │   │   ├── M00369
    │   │   │   ├── M00370
    │   │   │   ├── M00371
    │   │   │   ├── M00372
    │   │   │   ├── M00373
    │   │   │   ├── M00374
    │   │   │   ├── M00375
    │   │   │   ├── M00376
    │   │   │   ├── M00377
    │   │   │   ├── M00378
    │   │   │   ├── M00415
    │   │   │   ├── M00416
    │   │   │   ├── M00417
    │   │   │   ├── M00418
    │   │   │   ├── M00419
    │   │   │   ├── M00422
    │   │   │   ├── M00432
    │   │   │   ├── M00433
    │   │   │   ├── M00525
    │   │   │   ├── M00526
    │   │   │   ├── M00527
    │   │   │   ├── M00528
    │   │   │   ├── M00529
    │   │   │   ├── M00530
    │   │   │   ├── M00531
    │   │   │   ├── M00532
    │   │   │   ├── M00533
    │   │   │   ├── M00534
    │   │   │   ├── M00535
    │   │   │   ├── M00537
    │   │   │   ├── M00538
    │   │   │   ├── M00539
    │   │   │   ├── M00540
    │   │   │   ├── M00541
    │   │   │   ├── M00542
    │   │   │   ├── M00543
    │   │   │   ├── M00544
    │   │   │   ├── M00545
    │   │   │   ├── M00546
    │   │   │   ├── M00547
    │   │   │   ├── M00548
    │   │   │   ├── M00549
    │   │   │   ├── M00550
    │   │   │   ├── M00551
    │   │   │   ├── M00552
    │   │   │   ├── M00554
    │   │   │   ├── M00555
    │   │   │   ├── M00563
    │   │   │   ├── M00564
    │   │   │   ├── M00565
    │   │   │   ├── M00567
    │   │   │   ├── M00568
    │   │   │   ├── M00569
    │   │   │   ├── M00570
    │   │   │   ├── M00572
    │   │   │   ├── M00573
    │   │   │   ├── M00574
    │   │   │   ├── M00575
    │   │   │   ├── M00576
    │   │   │   ├── M00577
    │   │   │   ├── M00579
    │   │   │   ├── M00580
    │   │   │   ├── M00595
    │   │   │   ├── M00596
    │   │   │   ├── M00597
    │   │   │   ├── M00598
    │   │   │   ├── M00608
    │   │   │   ├── M00609
    │   │   │   ├── M00611
    │   │   │   ├── M00612
    │   │   │   ├── M00613
    │   │   │   ├── M00614
    │   │   │   ├── M00615
    │   │   │   ├── M00616
    │   │   │   ├── M00617
    │   │   │   ├── M00618
    │   │   │   ├── M00620
    │   │   │   ├── M00621
    │   │   │   ├── M00622
    │   │   │   ├── M00623
    │   │   │   ├── M00624
    │   │   │   ├── M00625
    │   │   │   ├── M00627
    │   │   │   ├── M00630
    │   │   │   ├── M00631
    │   │   │   ├── M00632
    │   │   │   ├── M00633
    │   │   │   ├── M00636
    │   │   │   ├── M00637
    │   │   │   ├── M00638
    │   │   │   ├── M00639
    │   │   │   ├── M00641
    │   │   │   ├── M00642
    │   │   │   ├── M00643
    │   │   │   ├── M00649
    │   │   │   ├── M00651
    │   │   │   ├── M00652
    │   │   │   ├── M00660
    │   │   │   ├── M00661
    │   │   │   ├── M00664
    │   │   │   ├── M00672
    │   │   │   ├── M00673
    │   │   │   ├── M00674
    │   │   │   ├── M00675
    │   │   │   ├── M00696
    │   │   │   ├── M00697
    │   │   │   ├── M00698
    │   │   │   ├── M00700
    │   │   │   ├── M00702
    │   │   │   ├── M00704
    │   │   │   ├── M00705
    │   │   │   ├── M00714
    │   │   │   ├── M00718
    │   │   │   ├── M00725
    │   │   │   ├── M00726
    │   │   │   ├── M00730
    │   │   │   ├── M00736
    │   │   │   ├── M00740
    │   │   │   ├── M00741
    │   │   │   ├── M00744
    │   │   │   ├── M00745
    │   │   │   ├── M00746
    │   │   │   ├── M00761
    │   │   │   ├── M00763
    │   │   │   ├── M00769
    │   │   │   ├── M00773
    │   │   │   ├── M00774
    │   │   │   ├── M00775
    │   │   │   ├── M00776
    │   │   │   ├── M00777
    │   │   │   ├── M00778
    │   │   │   ├── M00779
    │   │   │   ├── M00780
    │   │   │   ├── M00781
    │   │   │   ├── M00782
    │   │   │   ├── M00783
    │   │   │   ├── M00784
    │   │   │   ├── M00785
    │   │   │   ├── M00786
    │   │   │   ├── M00787
    │   │   │   ├── M00788
    │   │   │   ├── M00789
    │   │   │   ├── M00790
    │   │   │   ├── M00793
    │   │   │   ├── M00794
    │   │   │   ├── M00795
    │   │   │   ├── M00796
    │   │   │   ├── M00797
    │   │   │   ├── M00798
    │   │   │   ├── M00799
    │   │   │   ├── M00800
    │   │   │   ├── M00801
    │   │   │   ├── M00802
    │   │   │   ├── M00803
    │   │   │   ├── M00804
    │   │   │   ├── M00805
    │   │   │   ├── M00808
    │   │   │   ├── M00810
    │   │   │   ├── M00811
    │   │   │   ├── M00814
    │   │   │   ├── M00815
    │   │   │   ├── M00819
    │   │   │   ├── M00823
    │   │   │   ├── M00824
    │   │   │   ├── M00825
    │   │   │   ├── M00826
    │   │   │   ├── M00827
    │   │   │   ├── M00828
    │   │   │   ├── M00829
    │   │   │   ├── M00830
    │   │   │   ├── M00831
    │   │   │   ├── M00832
    │   │   │   ├── M00833
    │   │   │   ├── M00834
    │   │   │   ├── M00835
    │   │   │   ├── M00836
    │   │   │   ├── M00837
    │   │   │   ├── M00838
    │   │   │   ├── M00840
    │   │   │   ├── M00841
    │   │   │   ├── M00842
    │   │   │   ├── M00843
    │   │   │   ├── M00844
    │   │   │   ├── M00845
    │   │   │   ├── M00846
    │   │   │   ├── M00847
    │   │   │   ├── M00848
    │   │   │   ├── M00849
    │   │   │   ├── M00850
    │   │   │   ├── M00851
    │   │   │   ├── M00852
    │   │   │   ├── M00853
    │   │   │   ├── M00854
    │   │   │   ├── M00855
    │   │   │   ├── M00856
    │   │   │   ├── M00857
    │   │   │   ├── M00859
    │   │   │   ├── M00860
    │   │   │   ├── M00861
    │   │   │   ├── M00862
    │   │   │   ├── M00866
    │   │   │   ├── M00867
    │   │   │   ├── M00868
    │   │   │   ├── M00872
    │   │   │   ├── M00873
    │   │   │   ├── M00874
    │   │   │   ├── M00875
    │   │   │   ├── M00876
    │   │   │   ├── M00877
    │   │   │   ├── M00878
    │   │   │   ├── M00879
    │   │   │   ├── M00880
    │   │   │   ├── M00881
    │   │   │   ├── M00882
    │   │   │   ├── M00883
    │   │   │   ├── M00884
    │   │   │   ├── M00889
    │   │   │   ├── M00890
    │   │   │   ├── M00891
    │   │   │   ├── M00892
    │   │   │   ├── M00893
    │   │   │   ├── M00894
    │   │   │   ├── M00895
    │   │   │   ├── M00896
    │   │   │   ├── M00897
    │   │   │   ├── M00898
    │   │   │   ├── M00899
    │   │   │   ├── M00900
    │   │   │   ├── M00901
    │   │   │   ├── M00902
    │   │   │   ├── M00903
    │   │   │   ├── M00904
    │   │   │   ├── M00905
    │   │   │   ├── M00906
    │   │   │   ├── M00909
    │   │   │   ├── M00910
    │   │   │   ├── M00911
    │   │   │   ├── M00912
    │   │   │   ├── M00913
    │   │   │   ├── M00914
    │   │   │   ├── M00915
    │   │   │   ├── M00916
    │   │   │   ├── M00917
    │   │   │   ├── M00918
    │   │   │   ├── M00919
    │   │   │   ├── M00921
    │   │   │   ├── M00922
    │   │   │   ├── M00923
    │   │   │   ├── M00924
    │   │   │   ├── M00925
    │   │   │   ├── M00926
    │   │   │   ├── M00927
    │   │   │   ├── M00928
    │   │   │   ├── M00929
    │   │   │   ├── M00930
    │   │   │   ├── M00931
    │   │   │   ├── M00932
    │   │   │   ├── M00933
    │   │   │   ├── M00934
    │   │   │   ├── M00935
    │   │   │   ├── M00936
    │   │   │   ├── M00937
    │   │   │   ├── M00938
    │   │   │   ├── M00939
    │   │   │   ├── M00940
    │   │   │   ├── M00941
    │   │   │   ├── M00942
    │   │   │   ├── M00943
    │   │   │   ├── M00944
    │   │   │   ├── M00945
    │   │   │   ├── M00946
    │   │   │   ├── M00947
    │   │   │   ├── M00948
    │   │   │   ├── M00949
    │   │   │   ├── M00950
    │   │   │   ├── M00951
    │   │   │   ├── M00952
    │   │   │   ├── M00953
    │   │   │   ├── M00956
    │   │   │   ├── M00957
    │   │   │   ├── M00958
    │   │   │   ├── M00959
    │   │   │   ├── M00960
    │   │   │   ├── M00961
    │   │   │   ├── M00962
    │   │   │   ├── M00963
    │   │   │   ├── M00964
    │   │   │   ├── M00965
    │   │   │   ├── M00966
    │   │   │   ├── M00967
    │   │   │   ├── M00968
    │   │   │   ├── M00969
    │   │   │   ├── M00970
    │   │   │   ├── M00971
    │   │   │   ├── M00972
    │   │   │   └── M00973
    │   │   ├── MODULES.db
    │   │   ├── modules.keg
    │   │   └── orphan_data
    │   │       └── 02_hmm_profiles_with_ko_fams_with_no_threshold.hmm
    │   └── scg_setup
    │       ├── ACCESSION_TO_TAXONOMY.txt.gz
    │       ├── SCG_SEARCH_DATABASES
    │       │   ├── Ribosomal_L13.dmnd
    │       │   ├── Ribosomal_L13.gz
    │       │   ├── Ribosomal_L16.dmnd
    │       │   ├── Ribosomal_L16.gz
    │       │   ├── Ribosomal_L17.dmnd
    │       │   ├── Ribosomal_L17.gz
    │       │   ├── Ribosomal_L1.dmnd
    │       │   ├── Ribosomal_L1.gz
    │       │   ├── Ribosomal_L20.dmnd
    │       │   ├── Ribosomal_L20.gz
    │       │   ├── Ribosomal_L21p.dmnd
    │       │   ├── Ribosomal_L21p.gz
    │       │   ├── Ribosomal_L22.dmnd
    │       │   ├── Ribosomal_L22.gz
    │       │   ├── ribosomal_L24.dmnd
    │       │   ├── ribosomal_L24.gz
    │       │   ├── Ribosomal_L27A.dmnd
    │       │   ├── Ribosomal_L27A.gz
    │       │   ├── Ribosomal_L2.dmnd
    │       │   ├── Ribosomal_L2.gz
    │       │   ├── Ribosomal_L3.dmnd
    │       │   ├── Ribosomal_L3.gz
    │       │   ├── Ribosomal_L4.dmnd
    │       │   ├── Ribosomal_L4.gz
    │       │   ├── Ribosomal_L6.dmnd
    │       │   ├── Ribosomal_L6.gz
    │       │   ├── Ribosomal_L9_C.dmnd
    │       │   ├── Ribosomal_L9_C.gz
    │       │   ├── Ribosomal_S11.dmnd
    │       │   ├── Ribosomal_S11.gz
    │       │   ├── Ribosomal_S20p.dmnd
    │       │   ├── Ribosomal_S20p.gz
    │       │   ├── Ribosomal_S2.dmnd
    │       │   ├── Ribosomal_S2.gz
    │       │   ├── Ribosomal_S3_C.dmnd
    │       │   ├── Ribosomal_S3_C.gz
    │       │   ├── Ribosomal_S6.dmnd
    │       │   ├── Ribosomal_S6.gz
    │       │   ├── Ribosomal_S7.dmnd
    │       │   ├── Ribosomal_S7.gz
    │       │   ├── Ribosomal_S8.dmnd
    │       │   ├── Ribosomal_S8.gz
    │       │   ├── Ribosomal_S9.dmnd
    │       │   └── Ribosomal_S9.gz
    │       └── VERSION
    └── wg
        ├── combined-aas.fa
        ├── combined-aas.fa.unique
        ├── combined-aas.fa.unique.dmnd
        ├── combined-aas.fa.unique.names
        ├── diamond-search-results.txt
        ├── diamond-search-results.txt.unique
        ├── log.txt
        ├── mcl-clusters.txt
        ├── mcl-input.txt
        └── wg-PAN.db
    ```
    
- **1_process-gbk.sh**
    
    ```bash
    #!/usr/bin/bash
    
    #SBATCH --partition=Orion
    #SBATCH --job-name=process-genbank
    #SBATCH --nodes=1
    #SBATCH --ntasks-per-node=14
    #SBATCH --cpus-per-task=2
    #SBATCH --time=1:00:00
    #SBATCH --output=process_genbanks.out
    
    #activate anvio-8
    module load anvio/8
    
    #go to file where the genomes are (change based on your file location)
    path=/path/to/directory #<--change this
    cd $path/genbanks
    ls *.gb > $path/genbanks/filelist.txt
    
    mkdir $path/fastas $path/genecalls $path/functions 
    
    for sample in `cat $path/genbanks/filelist.txt`
    do
    	anvi-script-process-genbank -i $path/genbanks/$sample \
    	--output-fasta $path/fastas/${sample:0:-3}.fa \ #retains all characters in filename until ".gb"
    	--output-gene-calls $path/genecalls/${sample:0:-3}.txt \ 
    	--output-functions $path/functions/${sample:0:-3}.txt \
    	--force-overwrite;
    done
    ```
    
- **1.5_fix-fastas.sh**
    
    ```bash
    #!/usr/bin/bash
    
    #SBATCH --partition=Orion
    #SBATCH --job-name=fixing_fastas
    #SBATCH --nodes=1
    #SBATCH --ntasks-per-node=14
    #SBATCH --cpus-per-task=2
    #SBATCH --time=1:00:00
    #SBATCH --output=fix_fastas.out
    
    module load anvio/8
    
    path=/path/to/dir #<-- change this
    cd $path
    
    cd $path/fastas
    ls *.fa > $path/fastas/filelist.txt
    
    #before anything, lets fix our fastas to only have nucleotides and not weird characters
    for file in `cat $path/fastas/filelist.txt`
    do
        anvi-script-reformat-fasta \
        --seq-type NT $path/fastas/$file \
        --overwrite-input \
      --prefix ${file:0:-3}
    done
    
    ```
    
- **2_make-contig-db.sh**
    
    ```bash
    #!/usr/bin/bash
    
    #SBATCH --partition=Orion
    #SBATCH --job-name=anvi-gen-contigs-database
    #SBATCH --nodes=1
    #SBATCH --ntasks-per-node=14
    #SBATCH --cpus-per-task=1
    #SBATCH --time=1:00:00
    #SBATCH --output=make_contig_dbs.out
    
    module load anvio/8
    path=/path/to/die #<-- change this
    cd $path
    
    mkdir contigdbs
    
    for file in `cat $path/fastas/filelist.txt`
    do
        anvi-gen-contigs-database \
        -f $path/fastas/$file \
        -n ${file:0:-3} \
        -o $path/contigdbs/${file:0:-3}.db \
        --external-gene-calls $path/genecalls/${file:0:-3}.txt \
        --force-overwrite 
    done
    ```
    
- **2.5_import_functions.sh**
    
    ```bash
    #!/usr/bin/bash
    
    #SBATCH --partition=Orion
    #SBATCH --job-name=anvio_kegg_stuff
    #SBATCH --nodes=1
    #SBATCH --ntasks-per-node=28
    #SBATCH --cpus-per-task=2
    #SBATCH --time=23:00:00
    #SBATCH --output=funcitonal_annotation.out
    
    module load anvio/8
    path=/path/to/dir #<-- change this
    cd $path
    
    cd $path/contigdbs
    ls *.db > filelist.txt
    
    cd $path
    
    #setting up functional directories
    anvi-setup-scg-taxonomy --scgs-taxonomy-data-dir $path/setups/scg_setup --reset
    anvi-setup-kegg-data --kegg-data-dir $path/setups/kegg_setup
    anvi-setup-modelseed-database --dir $path/setups/modelseed_setup
    
    for file in `cat $path/contigdbs/filelist.txt`
    do
        anvi-run-hmms -c $path/contigdbs/$file --num-threads 4
        anvi-run-scg-taxonomy -c $path/contigdbs/$file --scgs-taxonomy-data-dir $path/setups/scg_setup --num-threads 4
        anvi-scan-trnas -c $path/contigdbs/$file --num-threads 4
        anvi-import-functions --contigs-db $path/contigdbs/$file -i $path/functions/${file:0:-3}.txt 
        anvi-run-kegg-kofams --contigs-db $path/contigdbs/$file --kegg-data-dir $path/serups/kegg_setup --num-threads 5
        anvi-reaction-network -c $path/contigdbs/$file --ko-dir $path/setups/kegg_setup --modelseed-dir $path/setups/modelseed_setup
    
    done
    ```
    
- **4_genome-storage.sh**
    
    ```bash
    #!/usr/bin/bash
    
    module load anvio/8
    
    path=/path/to/dir #<-- change this
    cd $path
    mkdir genomesdbs
    
    anvi-script-gen-genomes-file --input-dir $path/contigdbs -o $path/genomesdbs/external-genomes.txt
    
    anvi-gen-genomes-storage -e $path/genomesdbs/external-genomes.txt -o $path/genomesdbs/GENOMES.db --gene-caller NCBI_PGAP
    ```
    
- **5_make-pangenome-omggg.sh**
    
    ```bash
    #!/usr/bin/bash
    
    #SBATCH --partition=Orion
    #SBATCH --job-name=pangenome
    #SBATCH --nodes=1
    #SBATCH --ntasks-per-node=14
    #SBATCH --cpus-per-task=1
    #SBATCH --time=1:00:00
    #SBATCH --output=ANI.out
    
    module load anvio/8
    path=/path/to/dir #<-- change this
    cd $path
    
    #command to generate pangenome
    anvi-pan-genome -g $path/genomesdbs/GENOMES.db \
    --project-name projectname \ #<-- change this
    --num-threads 4 --force-overwrite
    
    #command to calculate ANI
    anvi-compute-genome-similarity --external-genomes \
    $path/genomesdbs/external-genomes.txt --program fastANI --output-dir $path/ANI \
    --num-threads 4 \
    --pan-db $path/projectname/projectname-PAN.db #<-- change according to project name
    
    #command to display pangenome. I typically copypaste it and run it on teh terminal everytime i need to view the pangenome. you should be present in $path for this to run
    anvi-display-pan -p projectname/projectname-PAN.db  \ #<-- change this
    -g genomesdbs/GENOMES.db
    ```