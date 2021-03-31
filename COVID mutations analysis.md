# COVID mutations analysis

## Summary
We analyzed the variants within  patients (intra-host diversity) in combination with the variants in the *covid* population. Thus, we had *two* levels of variability. Within and between patients. The goal of the analysis was to understand the within-patient variability. The following sub-questions were tackled: (i) can we trust the within patient variability; (ii) How should the frequency of the within-patient variability be modeled; (iii) Can we infer selective forces by combining the within-patient and between-patient variability?

Briefly, the results show that  the within-patients frequencies are noisy and characterized by large variance. Also, at least, low frequency variants cannot be trusted and they may often be artifacts. Finally, by combining the within-patient and between-patient variability we may infer mutations that may be under selection forces even though they are - still - in low frequency. 

## Methods
### Data

**Greek samples**: NGS samples from the Greek cohort were obtained by following the **paragon** protocol. The primer set comprises the following locations. 

```text
	chrom	left_start	left_end	right_start	right_end
NC_045512.2	8	34	111	140
NC_045512.2	70	94	192	212
NC_045512.2	159	183	285	308
NC_045512.2	256	279	380	404
NC_045512.2	336	353	458	482
NC_045512.2	411	434	535	557
NC_045512.2	503	527	623	647
NC_045512.2	591	612	711	737
NC_045512.2	677	703	804	824
NC_045512.2	777	799	891	914
NC_045512.2	860	884	985	1008
NC_045512.2	958	980	1074	1107
NC_045512.2	1042	1068	1164	1186
NC_045512.2	1131	1158	1258	1280
NC_045512.2	1229	1254	1347	1378
NC_045512.2	1312	1336	1434	1458
NC_045512.2	1408	1430	1515	1538
NC_045512.2	1487	1510	1607	1635
NC_045512.2	1564	1589	1685	1712
NC_045512.2	1648	1681	1765	1797
NC_045512.2	1728	1752	1851	1875
NC_045512.2	1823	1847	1945	1972
NC_045512.2	1887	1912	2010	2036
NC_045512.2	1974	2003	2088	2110
NC_045512.2	2044	2073	2163	2193
NC_045512.2	2126	2151	2249	2272
NC_045512.2	2217	2243	2336	2366
NC_045512.2	2299	2332	2422	2448
NC_045512.2	2383	2406	2501	2525
NC_045512.2	2468	2496	2593	2615
NC_045512.2	2562	2588	2685	2711
NC_045512.2	2651	2673	2771	2800
NC_045512.2	2736	2762	2861	2884
NC_045512.2	2820	2848	2934	2957
NC_045512.2	2900	2928	3023	3049
NC_045512.2	2988	3015	3111	3136
NC_045512.2	3080	3106	3200	3229
NC_045512.2	3170	3194	3290	3317
NC_045512.2	3255	3286	3373	3404
NC_045512.2	3334	3367	3457	3480
NC_045512.2	3419	3445	3578	3602
NC_045512.2	3541	3566	3661	3689
NC_045512.2	3629	3657	3754	3778
NC_045512.2	3726	3749	3849	3875
NC_045512.2	3808	3837	3926	3956
NC_045512.2	3890	3921	4006	4039
NC_045512.2	3974	4000	4091	4118
NC_045512.2	4061	4085	4187	4209
NC_045512.2	4145	4171	4265	4290
NC_045512.2	4225	4254	4345	4374
NC_045512.2	4311	4340	4436	4460
NC_045512.2	4406	4430	4532	4560
NC_045512.2	4486	4512	4611	4633
NC_045512.2	4561	4591	4683	4709
NC_045512.2	4644	4667	4766	4791
NC_045512.2	4730	4762	4846	4879
NC_045512.2	4812	4842	4934	4961
NC_045512.2	4904	4930	5063	5093
NC_045512.2	4994	5015	5157	5183
NC_045512.2	5104	5137	5228	5253
NC_045512.2	5196	5223	5316	5345
NC_045512.2	5286	5311	5407	5435
NC_045512.2	5381	5403	5505	5529
NC_045512.2	5474	5501	5593	5623
NC_045512.2	5548	5574	5674	5697
NC_045512.2	5628	5657	5754	5785
NC_045512.2	5719	5745	5840	5866
NC_045512.2	5809	5833	5931	5957
NC_045512.2	5883	5912	6008	6032
NC_045512.2	5977	6004	6099	6125
NC_045512.2	6062	6095	6185	6211
NC_045512.2	6158	6181	6282	6306
NC_045512.2	6249	6274	6369	6392
NC_045512.2	6330	6358	6452	6479
NC_045512.2	6419	6446	6542	6568
NC_045512.2	6503	6536	6629	6651
NC_045512.2	6592	6625	6709	6741
NC_045512.2	6674	6705	6791	6822
NC_045512.2	6752	6785	6874	6901
NC_045512.2	6839	6863	6959	6988
NC_045512.2	6917	6950	7041	7066
NC_045512.2	7007	7035	7126	7156
NC_045512.2	7098	7122	7216	7240
NC_045512.2	7167	7200	7290	7312
NC_045512.2	7253	7286	7398	7427
NC_045512.2	7358	7390	7507	7532
NC_045512.2	7473	7503	7597	7622
NC_045512.2	7562	7591	7678	7706
NC_045512.2	7643	7673	7762	7790
NC_045512.2	7730	7758	7849	7878
NC_045512.2	7805	7838	7929	7953
NC_045512.2	7888	7921	8009	8033
NC_045512.2	7958	7988	8081	8107
NC_045512.2	8042	8075	8157	8180
NC_045512.2	8126	8152	8248	8274
NC_045512.2	8212	8242	8333	8355
NC_045512.2	8287	8316	8406	8435
NC_045512.2	8375	8400	8496	8524
NC_045512.2	8456	8485	8575	8605
NC_045512.2	8539	8569	8658	8688
NC_045512.2	8616	8649	8738	8764
NC_045512.2	8711	8734	8834	8860
NC_045512.2	8798	8825	8919	8945
NC_045512.2	8890	8915	9006	9035
NC_045512.2	8976	9000	9097	9120
NC_045512.2	9050	9079	9174	9199
NC_045512.2	9139	9169	9259	9287
NC_045512.2	9231	9254	9347	9380
NC_045512.2	9314	9341	9436	9462
NC_045512.2	9404	9431	9516	9544
NC_045512.2	9481	9511	9641	9665
NC_045512.2	9597	9630	9744	9771
NC_045512.2	9709	9735	9835	9858
NC_045512.2	9802	9831	9926	9951
NC_045512.2	9865	9898	10016	10038
NC_045512.2	9987	10012	10108	10135
NC_045512.2	10080	10104	10191	10220
NC_045512.2	10153	10178	10274	10300
NC_045512.2	10244	10270	10368	10393
NC_045512.2	10334	10362	10454	10483
NC_045512.2	10423	10447	10548	10572
NC_045512.2	10518	10543	10635	10661
NC_045512.2	10602	10624	10723	10751
NC_045512.2	10687	10714	10809	10833
NC_045512.2	10776	10800	10892	10922
NC_045512.2	10855	10888	10978	11004
NC_045512.2	10943	10969	11028	11058
NC_045512.2	11004	11028	11125	11150
NC_045512.2	11093	11119	11218	11242
NC_045512.2	11190	11214	11311	11337
NC_045512.2	11270	11300	11392	11417
NC_045512.2	11357	11382	11477	11504
NC_045512.2	11438	11463	11555	11583
NC_045512.2	11526	11551	11650	11675
NC_045512.2	11605	11638	11731	11754
NC_045512.2	11693	11726	11816	11842
NC_045512.2	11785	11810	11908	11934
NC_045512.2	11877	11903	12000	12026
NC_045512.2	11966	11994	12090	12115
NC_045512.2	12042	12069	12165	12190
NC_045512.2	12137	12161	12262	12286
NC_045512.2	12226	12251	12348	12374
NC_045512.2	12305	12328	12428	12454
NC_045512.2	12395	12421	12556	12581
NC_045512.2	12522	12551	12646	12670
NC_045512.2	12610	12638	12737	12759
NC_045512.2	12685	12710	12809	12833
NC_045512.2	12776	12801	12900	12924
NC_045512.2	12864	12893	12984	13009
NC_045512.2	12923	12956	13075	13097
NC_045512.2	13045	13071	13155	13178
NC_045512.2	13126	13151	13254	13275
NC_045512.2	13204	13230	13325	13347
NC_045512.2	13281	13314	13406	13427
NC_045512.2	13353	13380	13479	13499
NC_045512.2	13442	13466	13562	13590
NC_045512.2	13529	13554	13648	13678
NC_045512.2	13612	13644	13728	13761
NC_045512.2	13672	13705	13820	13846
NC_045512.2	13788	13815	13905	13937
NC_045512.2	13870	13901	13989	14019
NC_045512.2	13959	13982	14080	14107
NC_045512.2	14043	14073	14166	14190
NC_045512.2	14124	14153	14243	14273
NC_045512.2	14212	14237	14336	14361
NC_045512.2	14309	14332	14428	14457
NC_045512.2	14397	14420	14511	14544
NC_045512.2	14481	14507	14607	14630
NC_045512.2	14581	14603	14705	14730
NC_045512.2	14668	14695	14783	14810
NC_045512.2	14748	14776	14872	14897
NC_045512.2	14838	14868	14952	14980
NC_045512.2	14917	14941	15036	15066
NC_045512.2	15006	15031	15130	15162
NC_045512.2	15086	15107	15209	15234
NC_045512.2	15181	15205	15305	15327
NC_045512.2	15277	15300	15399	15426
NC_045512.2	15374	15394	15493	15519
NC_045512.2	15463	15486	15624	15655
NC_045512.2	15587	15613	15709	15731
NC_045512.2	15678	15704	15786	15819
NC_045512.2	15756	15780	15875	15903
NC_045512.2	15846	15871	15963	15995
NC_045512.2	15929	15955	16052	16077
NC_045512.2	16014	16039	16131	16160
NC_045512.2	16088	16121	16212	16235
NC_045512.2	16181	16207	16302	16330
NC_045512.2	16272	16297	16397	16420
NC_045512.2	16367	16392	16481	16507
NC_045512.2	16442	16472	16560	16582
NC_045512.2	16528	16556	16650	16677
NC_045512.2	16611	16637	16737	16760
NC_045512.2	16706	16731	16830	16855
NC_045512.2	16791	16824	16909	16935
NC_045512.2	16869	16899	16991	17018
NC_045512.2	16935	16958	17061	17084
NC_045512.2	17028	17057	17144	17170
NC_045512.2	17110	17134	17230	17252
NC_045512.2	17181	17211	17303	17329
NC_045512.2	17265	17298	17393	17414
NC_045512.2	17359	17389	17470	17493
NC_045512.2	17422	17443	17569	17592
NC_045512.2	17537	17559	17663	17686
NC_045512.2	17625	17654	17747	17772
NC_045512.2	17716	17739	17835	17860
NC_045512.2	17805	17831	17930	17954
NC_045512.2	17888	17915	18014	18037
NC_045512.2	17968	17999	18091	18113
NC_045512.2	18052	18081	18174	18201
NC_045512.2	18137	18165	18257	18279
NC_045512.2	18220	18252	18342	18368
NC_045512.2	18296	18316	18433	18460
NC_045512.2	18397	18426	18557	18585
NC_045512.2	18483	18509	18654	18678
NC_045512.2	18601	18627	18714	18741
NC_045512.2	18687	18710	18809	18835
NC_045512.2	18780	18805	18899	18922
NC_045512.2	18856	18881	18976	19005
NC_045512.2	18946	18971	19066	19094
NC_045512.2	19035	19062	19158	19184
NC_045512.2	19103	19136	19253	19277
NC_045512.2	19219	19249	19335	19368
NC_045512.2	19300	19326	19449	19471
NC_045512.2	19400	19426	19522	19549
NC_045512.2	19489	19518	19611	19637
NC_045512.2	19576	19607	19692	19725
NC_045512.2	19651	19676	19777	19800
NC_045512.2	19738	19771	19860	19885
NC_045512.2	19813	19840	19938	19962
NC_045512.2	19889	19918	20005	20033
NC_045512.2	19957	19978	20102	20131
NC_045512.2	20072	20095	20188	20221
NC_045512.2	20161	20184	20278	20308
NC_045512.2	20238	20271	20358	20386
NC_045512.2	20322	20354	20441	20470
NC_045512.2	20404	20437	20546	20578
NC_045512.2	20492	20525	20633	20666
NC_045512.2	20603	20629	20724	20752
NC_045512.2	20691	20720	20808	20840
NC_045512.2	20774	20803	20897	20921
NC_045512.2	20860	20887	20985	21009
NC_045512.2	20953	20980	21072	21102
NC_045512.2	21032	21064	21153	21179
NC_045512.2	21119	21145	21244	21268
NC_045512.2	21196	21221	21337	21370
NC_045512.2	21305	21331	21425	21454
NC_045512.2	21387	21420	21505	21536
NC_045512.2	21467	21500	21587	21616
NC_045512.2	21549	21579	21672	21697
NC_045512.2	21636	21660	21761	21785
NC_045512.2	21728	21757	21848	21877
NC_045512.2	21814	21844	21930	21963
NC_045512.2	21899	21926	22019	22048
NC_045512.2	21985	22013	22104	22134
NC_045512.2	22067	22095	22191	22215
NC_045512.2	22154	22187	22271	22302
NC_045512.2	22235	22264	22358	22382
NC_045512.2	22320	22342	22466	22493
NC_045512.2	22437	22459	22554	22579
NC_045512.2	22520	22548	22639	22664
NC_045512.2	22605	22630	22726	22754
NC_045512.2	22691	22722	22839	22865
NC_045512.2	22801	22824	22917	22950
NC_045512.2	22879	22908	23044	23068
NC_045512.2	22989	23012	23133	23162
NC_045512.2	23087	23120	23208	23236
NC_045512.2	23173	23203	23294	23319
NC_045512.2	23261	23285	23381	23405
NC_045512.2	23347	23376	23455	23478
NC_045512.2	23424	23451	23538	23563
NC_045512.2	23494	23516	23619	23643
NC_045512.2	23577	23607	23697	23726
NC_045512.2	23662	23692	23786	23810
NC_045512.2	23754	23780	23878	23903
NC_045512.2	23846	23874	23962	23995
NC_045512.2	23929	23957	24047	24072
NC_045512.2	24000	24030	24125	24147
NC_045512.2	24088	24114	24201	24224
NC_045512.2	24173	24197	24295	24321
NC_045512.2	24262	24291	24386	24410
NC_045512.2	24356	24382	24464	24489
NC_045512.2	24429	24453	24547	24570
NC_045512.2	24503	24527	24625	24652
NC_045512.2	24587	24615	24704	24728
NC_045512.2	24673	24700	24799	24822
NC_045512.2	24770	24795	24891	24919
NC_045512.2	24862	24887	24983	25009
NC_045512.2	24946	24975	25067	25091
NC_045512.2	25034	25063	25157	25183
NC_045512.2	25123	25151	25246	25271
NC_045512.2	25213	25239	25325	25349
NC_045512.2	25284	25306	25405	25433
NC_045512.2	25364	25397	25492	25513
NC_045512.2	25455	25480	25579	25603
NC_045512.2	25539	25562	25656	25680
NC_045512.2	25624	25647	25739	25772
NC_045512.2	25701	25732	25842	25875
NC_045512.2	25808	25838	25930	25954
NC_045512.2	25885	25913	26007	26034
NC_045512.2	25972	26000	26096	26121
NC_045512.2	26062	26087	26182	26203
NC_045512.2	26146	26172	26266	26294
NC_045512.2	26228	26257	26353	26373
NC_045512.2	26324	26347	26446	26473
NC_045512.2	26404	26434	26529	26553
NC_045512.2	26493	26524	26618	26642
NC_045512.2	26579	26608	26700	26725
NC_045512.2	26666	26696	26791	26813
NC_045512.2	26764	26787	26866	26890
NC_045512.2	26807	26833	26958	26980
NC_045512.2	26917	26942	27040	27066
NC_045512.2	27009	27033	27122	27151
NC_045512.2	27095	27116	27213	27243
NC_045512.2	27181	27209	27321	27354
NC_045512.2	27281	27314	27414	27437
NC_045512.2	27370	27397	27484	27509
NC_045512.2	27450	27475	27615	27638
NC_045512.2	27572	27596	27733	27761
NC_045512.2	27695	27719	27811	27844
NC_045512.2	27779	27807	27895	27928
NC_045512.2	27864	27890	27990	28012
NC_045512.2	27960	27984	28079	28102
NC_045512.2	28045	28075	28169	28194
NC_045512.2	28134	28165	28251	28282
NC_045512.2	28222	28246	28336	28360
NC_045512.2	28286	28307	28410	28435
NC_045512.2	28376	28395	28500	28525
NC_045512.2	28462	28485	28583	28610
NC_045512.2	28556	28577	28691	28715
NC_045512.2	28645	28669	28766	28789
NC_045512.2	28729	28751	28847	28872
NC_045512.2	28820	28843	28947	28969
NC_045512.2	28884	28906	29000	29024
NC_045512.2	28963	28987	29074	29098
NC_045512.2	29036	29058	29151	29177
NC_045512.2	29107	29132	29227	29246
NC_045512.2	29203	29221	29326	29352
NC_045512.2	29290	29320	29415	29438
NC_045512.2	29368	29394	29489	29512
NC_045512.2	29459	29482	29574	29603
NC_045512.2	29547	29570	29666	29696
NC_045512.2	29626	29655	29751	29774
NC_045512.2	29708	29731	29844	29875

```

  Primer-sets are important because in the analysis the part of the short reads that corresponds to the primer locations were soft-clipped. Thus, they didn't participate in the SNP calling analysis. 

### Data Location

All analysis is located in the folder `/home/pavlos/covid_analysis_pavlos`. The directory is actually hosted in the msc-server (ip: 139.91.75.56, directory:/home/pavlos/covid). This directory is mapped to `rantaplan`, in the folder `covid_analysis_pavlos`, and in `zoya`, in the folder `/home/pavlos/covid_analysis_pavlos`. 

The *signal-pipeline* has been performed within the directory `covid-19-signal`. There, we can see the following directories:

*  `resources`: contains different files necessary for the analysis such as the primer sets. We have put there the **paragon** primer sets. By default, the directory contains (in the folder 'primer_schemes') the artic_v3 and the liverpool primer scheme. 

* Note: in our primer scheme (the paragon), described in the file `SARSCoV2.paragon.bed`, I have substracted 1bp from the beginning of the left end of the left primer. This is because the primer masking was not performed correctly during the `ivar` process. 

* `data`: The data directory contains mainly fasta and gff3 files necessary for the analysis. The `ls` command, returns the following files:

  ```{text}
  pavlos@curie:~/covid/covid-19-signal/data$ ls
  composite_human_viral_reference.fna      composite_human_viral_reference.fna.sa  MN908947.3.gbk
  composite_human_viral_reference.fna.amb  GRC38_no_alt_analysis_set.fna           MN908947.3.gff3
  composite_human_viral_reference.fna.ann  Kraken2                                 NexteraPE-PE.fa
  composite_human_viral_reference.fna.bwt  MN908947.3.fasta
  composite_human_viral_reference.fna.pac  MN908947.3.fasta.fai
  ```

* `/home/pavlos/covid/covid-19-signal/tal_results_dir`: contains all the results. The results are organized in folders, one per sample, for the signal pipeline. Furthermore, we have created some additional folders, the `pair_alignments`, the `snp_consistency` and the `depth` and `consensus` which contain some specific analysis as we  will describe later in the text. 

* `/home/pavlos/covid/scripts`: Here we have saved the scripts, mainly R and perl, for the analyses. The `ls` command gives the following output:

  ```{text}
  ## usage: ./align_sequences.pl - | -sam <INPUT FILE> -goodAl <OUTPUT FILE> -alignments <OUTPUT FILE> -stats <OUTPUT FILE> -misal <OUTPUT FILE>
  ## performs needleman-wunsch pairwise alignment. It is used to discover whether pair-reads match together or they are characterized by mismatches or indels. A strange thing in the data is that despite paired reads should start/end at the same location, they often don't do so. Probably because larger fragments were obtained in the first place. Also there are several mismatches. 
  
  align_sequences.pl
  ---------------------------------------------------------------------------------------
  ## Given some positions on the genome, this script just goes into the mpileup file to count what nucleotides were found at certain positions. It is used to study whether certain variants found to be polymorphic within individuals from Greece, are also polymorphic in other locations (especially those that the variants do not segregate in the population (e.g. Brazil))
  
  analyze_mpileup.R
  ---------------------------------------------------------------------------------------
  ## It reads the gisaid alignment and a list of interesting positions (in our case, these are the polymorphic positions in our samples from the Talianidis lab). Then, given the positions it maps the positions back to the reference genome *in the alignment* to find the new positions in the aligment (maybe these are different due to the '-' character') and it reports:
  - per continent
  - per country 
  The states that are found in these genomic locations. 
  This script was used to find out whether the within-individuals polymorphic positions are also polymorphic in different populations around the globe
  
  continents_info_gisaid.R
  ---------------------------------------------------------------------------------------
  ## To script to exei grapsei h Maria
  ## TODO ... description
  double_covered_regions.r
  ---------------------------------------------------------------------------------------
  ## scripts from the UCSC to convert fa to Tab and VCF format respectively
  faToTab
  faToVcf
  ---------------------------------------------------------------------------------------
  ## Creates a bed file with amplicons instead of primers
  ./get_amplicons_from_primers.pl -in <PRIMER FILE>
  As input, it uses the bed file for the primers (paragon file). The output looks like that:
  NC_045512.2     29482   29574   340     nCoV-2019_2     +
  NC_045512.2     29570   29666   341     nCoV-2019_1     +
  NC_045512.2     29655   29751   342     nCoV-2019_2     +
  NC_045512.2     29731   29844   343     nCoV-2019_1     +
  
  get_amplicons_from_primers.pl
  ---------------------------------------------------------------------------------------
  ## Creates a bed file with amplicons instead of primers
  ./get_amplicons_from_primers.pl -in <PRIMER FILE>
  As input, it uses the bed file for the primers (paragon file). The output looks like that:
  NC_045512.2     29482   29574   340     nCoV-2019_2     +
  NC_045512.2     29570   29666   341     nCoV-2019_1     +
  NC_045512.2     29655   29751   342     nCoV-2019_2     +
  NC_045512.2     29731   29844   343     nCoV-2019_1     +
  
  get_amplicons_from_primers.pl
  ---------------------------------------------------------------------------------------
  ## A: keep snp positions from ivar.tsv                                          
  # saved at: '/home/maria/covid_analysis_pavlos/gisaid/our_SNPpos.txt'
  #B: make matrix of snps from all samples:
  #PINAKAS ME ROWS=POSITIONS, COLS=SAMPLES kai VALUES=ALT_FREQ
  #C: same pinakas as B, containing a column for the gisaid samples as well
  # all (onoma)                                                                                                                       
  our_snpPOS.r
  ---------------------------------------------------------------------------------------
  ## it plots the coverage and the number of primers per position. Primers may overlap so in some regions, there are two amplicons that are present and therefore the coverage is greater. 
  
  plot_depth.R
  ---------------------------------------------------------------------------------------
  ## it plots the coverage and the number of primers per position. Primers may overlap so in some regions, there are two amplicons that are present and therefore the coverage is greater. 
  
  plot.R
  ---------------------------------------------------------------------------------------
  ## TODO
  ##  It prints the number of mismatches and gaps of the paired end reads.
  plot_stats_tsvs.R
  ---------------------------------------------------------------------------------------
  ## TODO
  
  plot_tsvs.R
  ---------------------------------------------------------------------------------------
  ## TODO check if this is correct
  Prints out the number of mismatches and gaps from the paired end reads.
  
  posListScore2.pl
  ---------------------------------------------------------------------------------------
  ## samme as posListScore2.pl
  
  posListScore3.pl
  ---------------------------------------------------------------------------------------
  ## samme as posListScore2.pl
  
  posListScore.pl
  ---------------------------------------------------------------------------------------
  ## converts the tab format from paragon to bed format
  ./primTabtoBed.pl -in <FILE>\n\n
  
  primTabtoBed.pl
  ---------------------------------------------------------------------------------------
  # PERIGRAFI:                                                                             # kaloume to IVAR gia ta BAMS tou kathe amplicon                                         # kanoume merge ta BAMS apo ta diadoxika amplicon kai kaloume to IVAR                     ## First run the script split_all_bams.r (it's in the scripts folder) to split the bams of each sample                              
  ## into separate bam files, one for each amplicon                                         ## go to the ~/covid_analysis_pavlos/covid-19-signal/tal_results_dir/snp_consistency and type 'Rscript split_all_bams.r'            
  ## then each folder will contain SAM files                                               ## activate the conda environment                                                         ## ACTIVATE CONDA OUTSIDE THE SCRIPT                                                     ## conda activate /home/maria/SNAKE_COVID/conda/5258de7f                                 ## 1. go to the ~/covid_analysis_pavlos/covid-19-signal/tal_results_dir/snp_consistency directory  
  
  runIvarForSample.sh
  ---------------------------------------------------------------------------------------
  ## It runs ivar after producing the mpileup file
  runIvar.sh
  ---------------------------------------------------------------------------------------
  ## # Xwrizoume ta BAM arxeia kathe deigmatos                                             # se mini SAMs pou to kathe ena periexei ta reads pou proerxontai apo ena amplicon       #input: */core/*_viral_reference.mapping.primertrimmed.sorted.bam                         #output dir: covid_analysis_pavlos/covid-19-signal/tal_results_dir/snp_consistency       ### NOTE: edw exw kalesei to consistencyCheck.pl (9/2/2021)                               ### to opoio metaonomastike kai egine store sto: scripts/splitBAM_to_amplicons.pl   
  
  split_all_bams.r
  ---------------------------------------------------------------------------------------
  ## "It checks the amplicon overlap regions to study whether amlplicons from different primers give consistent results\n./s\
  amtools view -h BAM | consistencyCheck.pl -bed <FILE WITH PRIMERS INFO *> -snp <SNP FILE>\n\n\t* CHROM LEFT_PRIMER_START RIGHT_PRIM\
  ER_END\n\n"
  
  splitBAM_to_amplicons.pl
  ---------------------------------------------------------------------------------------
  ## prints out the p-values for the test: The variants in the current position do not depend on the major state on the next positon, based on the HyperGeometric distribution
  
  transition_prob3.R
  ---------------------------------------------------------------------------------------
  ## it finds out whether there is a bias on the type of mutations (2nd more frequent base per site) given the state in the next position. This version is for the gisaid data
  
  transition_prob_gisaid.R
  ---------------------------------------------------------------------------------------
  ## TODO
  variant_consistency_statistics.R
  
  ```

  

* `/home/pavlos/covid_analysis_pavlos/gisaid`: contains gisaid data and some subsets of it (brazilian samples). The version of the gisaid data is the 0312 (March 12th, 2021)


### The signal pipeline
The signal pipeline is described nicely on the log files generated when the signal pipeline was executed.  I add here the whole file located at:
`/home/pavlos/covid_analysis_pavlos/covid-19-signal/.snakemake/log`. 
```{text}
Building DAG of jobs...
Using shell: /usr/bin/bash
Provided cores: 8
Rules claiming more threads will be scaled down.
Job counts:
	count	jobs
	1	all
	1	copy_config_sample_log
	9	coverage_depth
	9	generate_coverage_plot
	9	get_host_removed_reads
	9	get_mapping_reads
	18	link_raw_data
	9	raw_reads_composite_reference_bwa_map
	9	run_bed_primer_trim
	9	run_fastqc_on_mapped_reads
	9	run_filtering_of_residual_adapters
	9	run_ivar_consensus
	9	run_ivar_variants
	9	run_kraken2
	9	run_quast
	9	run_raw_fastqc
	9	run_trimgalore
	9	viral_reference_bwa_build
	9	viral_reference_bwa_map
	164
Select jobs to execute...

[Thu Jan 28 19:49:33 2021]
rule link_raw_data:
    input: /home/maria/covid_analysis_pavlos/dec_10/fastq/NGS0990_R2.fastq.gz
    output: NGS0990/raw_fastq/NGS0990_R2.fastq.gz
    jobid: 2
    wildcards: sn=NGS0990, r=2
    priority: 4

echo 2; mkdir -p NGS0990/raw_fastq/; cp /home/maria/covid_analysis_pavlos/dec_10/fastq/NGS0990_R2.fastq.gz NGS0990/raw_fastq/NGS0990_R2.fastq.gz;

[Thu Jan 28 19:49:33 2021]
rule link_raw_data:
    input: /home/maria/covid_analysis_pavlos/dec_10/fastq/NGS1044_R2.fastq.gz
    output: NGS1044/raw_fastq/NGS1044_R2.fastq.gz
    jobid: 16
    wildcards: sn=NGS1044, r=2
    priority: 4

echo 2; mkdir -p NGS1044/raw_fastq/; cp /home/maria/covid_analysis_pavlos/dec_10/fastq/NGS1044_R2.fastq.gz NGS1044/raw_fastq/NGS1044_R2.fastq.gz;

[Thu Jan 28 19:49:33 2021]
rule link_raw_data:
    input: /home/maria/covid_analysis_pavlos/dec_10/fastq/NGS1045_R2.fastq.gz
    output: NGS1045/raw_fastq/NGS1045_R2.fastq.gz
    jobid: 18
    wildcards: sn=NGS1045, r=2
    priority: 4

echo 2; mkdir -p NGS1045/raw_fastq/; cp /home/maria/covid_analysis_pavlos/dec_10/fastq/NGS1045_R2.fastq.gz NGS1045/raw_fastq/NGS1045_R2.fastq.gz;

[Thu Jan 28 19:49:33 2021]
rule link_raw_data:
    input: /home/maria/covid_analysis_pavlos/dec_10/fastq/NGS1040_R2.fastq.gz
    output: NGS1040/raw_fastq/NGS1040_R2.fastq.gz
    jobid: 8
    wildcards: sn=NGS1040, r=2
    priority: 4

echo 2; mkdir -p NGS1040/raw_fastq/; cp /home/maria/covid_analysis_pavlos/dec_10/fastq/NGS1040_R2.fastq.gz NGS1040/raw_fastq/NGS1040_R2.fastq.gz;

[Thu Jan 28 19:49:33 2021]
rule link_raw_data:
    input: /home/maria/covid_analysis_pavlos/dec_10/fastq/NGS1042_R2.fastq.gz
    output: NGS1042/raw_fastq/NGS1042_R2.fastq.gz
    jobid: 12
    wildcards: sn=NGS1042, r=2
    priority: 4

echo 2; mkdir -p NGS1042/raw_fastq/; cp /home/maria/covid_analysis_pavlos/dec_10/fastq/NGS1042_R2.fastq.gz NGS1042/raw_fastq/NGS1042_R2.fastq.gz;

[Thu Jan 28 19:49:33 2021]
rule link_raw_data:
    input: /home/maria/covid_analysis_pavlos/dec_10/fastq/NGS1001_R2.fastq.gz
    output: NGS1001/raw_fastq/NGS1001_R2.fastq.gz
    jobid: 6
    wildcards: sn=NGS1001, r=2
    priority: 4

echo 2; mkdir -p NGS1001/raw_fastq/; cp /home/maria/covid_analysis_pavlos/dec_10/fastq/NGS1001_R2.fastq.gz NGS1001/raw_fastq/NGS1001_R2.fastq.gz;

[Thu Jan 28 19:49:34 2021]
rule link_raw_data:
    input: /home/maria/covid_analysis_pavlos/dec_10/fastq/NGS1041_R1.fastq.gz
    output: NGS1041/raw_fastq/NGS1041_R1.fastq.gz
    jobid: 9
    wildcards: sn=NGS1041, r=1
    priority: 4

echo 1; mkdir -p NGS1041/raw_fastq/; cp /home/maria/covid_analysis_pavlos/dec_10/fastq/NGS1041_R1.fastq.gz NGS1041/raw_fastq/NGS1041_R1.fastq.gz;

[Thu Jan 28 19:49:34 2021]
rule link_raw_data:
    input: /home/maria/covid_analysis_pavlos/dec_10/fastq/NGS1000_R1.fastq.gz
    output: NGS1000/raw_fastq/NGS1000_R1.fastq.gz
    jobid: 3
    wildcards: sn=NGS1000, r=1
    priority: 4

echo 1; mkdir -p NGS1000/raw_fastq/; cp /home/maria/covid_analysis_pavlos/dec_10/fastq/NGS1000_R1.fastq.gz NGS1000/raw_fastq/NGS1000_R1.fastq.gz;
[Thu Jan 28 19:49:36 2021]
Finished job 2.
1 of 164 steps (0.61%) done
Select jobs to execute...

[Thu Jan 28 19:49:36 2021]
rule link_raw_data:
    input: /home/maria/covid_analysis_pavlos/dec_10/fastq/NGS1000_R2.fastq.gz
    output: NGS1000/raw_fastq/NGS1000_R2.fastq.gz
    jobid: 4
    wildcards: sn=NGS1000, r=2
    priority: 4

echo 2; mkdir -p NGS1000/raw_fastq/; cp /home/maria/covid_analysis_pavlos/dec_10/fastq/NGS1000_R2.fastq.gz NGS1000/raw_fastq/NGS1000_R2.fastq.gz;
[Thu Jan 28 19:49:38 2021]
Finished job 6.
2 of 164 steps (1%) done
Select jobs to execute...

[Thu Jan 28 19:49:39 2021]
rule link_raw_data:
    input: /home/maria/covid_analysis_pavlos/dec_10/fastq/NGS1043_R2.fastq.gz
    output: NGS1043/raw_fastq/NGS1043_R2.fastq.gz
    jobid: 14
    wildcards: sn=NGS1043, r=2
    priority: 4

echo 2; mkdir -p NGS1043/raw_fastq/; cp /home/maria/covid_analysis_pavlos/dec_10/fastq/NGS1043_R2.fastq.gz NGS1043/raw_fastq/NGS1043_R2.fastq.gz;
[Thu Jan 28 19:49:43 2021]
Finished job 3.
3 of 164 steps (2%) done
Select jobs to execute...

[Thu Jan 28 19:49:43 2021]
rule link_raw_data:
    input: /home/maria/covid_analysis_pavlos/dec_10/fastq/NGS1001_R1.fastq.gz
    output: NGS1001/raw_fastq/NGS1001_R1.fastq.gz
    jobid: 5
    wildcards: sn=NGS1001, r=1
    priority: 4

echo 1; mkdir -p NGS1001/raw_fastq/; cp /home/maria/covid_analysis_pavlos/dec_10/fastq/NGS1001_R1.fastq.gz NGS1001/raw_fastq/NGS1001_R1.fastq.gz;
[Thu Jan 28 19:49:44 2021]
Finished job 4.
4 of 164 steps (2%) done
Select jobs to execute...

[Thu Jan 28 19:49:44 2021]
rule link_raw_data:
    input: /home/maria/covid_analysis_pavlos/dec_10/fastq/NGS1041_R2.fastq.gz
    output: NGS1041/raw_fastq/NGS1041_R2.fastq.gz
    jobid: 10
    wildcards: sn=NGS1041, r=2
    priority: 4

echo 2; mkdir -p NGS1041/raw_fastq/; cp /home/maria/covid_analysis_pavlos/dec_10/fastq/NGS1041_R2.fastq.gz NGS1041/raw_fastq/NGS1041_R2.fastq.gz;
[Thu Jan 28 19:49:45 2021]
Finished job 14.
5 of 164 steps (3%) done
Select jobs to execute...

[Thu Jan 28 19:49:45 2021]
rule link_raw_data:
    input: /home/maria/covid_analysis_pavlos/dec_10/fastq/NGS1040_R1.fastq.gz
    output: NGS1040/raw_fastq/NGS1040_R1.fastq.gz
    jobid: 7
    wildcards: sn=NGS1040, r=1
    priority: 4

echo 1; mkdir -p NGS1040/raw_fastq/; cp /home/maria/covid_analysis_pavlos/dec_10/fastq/NGS1040_R1.fastq.gz NGS1040/raw_fastq/NGS1040_R1.fastq.gz;
[Thu Jan 28 19:49:49 2021]
Finished job 5.
6 of 164 steps (4%) done
Select jobs to execute...

[Thu Jan 28 19:49:49 2021]
rule link_raw_data:
    input: /home/maria/covid_analysis_pavlos/dec_10/fastq/NGS1045_R1.fastq.gz
    output: NGS1045/raw_fastq/NGS1045_R1.fastq.gz
    jobid: 17
    wildcards: sn=NGS1045, r=1
    priority: 4

echo 1; mkdir -p NGS1045/raw_fastq/; cp /home/maria/covid_analysis_pavlos/dec_10/fastq/NGS1045_R1.fastq.gz NGS1045/raw_fastq/NGS1045_R1.fastq.gz;
[Thu Jan 28 19:49:50 2021]
Finished job 9.
7 of 164 steps (4%) done
Select jobs to execute...

[Thu Jan 28 19:49:50 2021]
rule link_raw_data:
    input: /home/maria/covid_analysis_pavlos/dec_10/fastq/NGS1044_R1.fastq.gz
    output: NGS1044/raw_fastq/NGS1044_R1.fastq.gz
    jobid: 15
    wildcards: sn=NGS1044, r=1
    priority: 4

echo 1; mkdir -p NGS1044/raw_fastq/; cp /home/maria/covid_analysis_pavlos/dec_10/fastq/NGS1044_R1.fastq.gz NGS1044/raw_fastq/NGS1044_R1.fastq.gz;
[Thu Jan 28 19:50:02 2021]
Finished job 10.
8 of 164 steps (5%) done
Select jobs to execute...

[Thu Jan 28 19:50:02 2021]
rule link_raw_data:
    input: /home/maria/covid_analysis_pavlos/dec_10/fastq/NGS0990_R1.fastq.gz
    output: NGS0990/raw_fastq/NGS0990_R1.fastq.gz
    jobid: 1
    wildcards: sn=NGS0990, r=1
    priority: 4

echo 1; mkdir -p NGS0990/raw_fastq/; cp /home/maria/covid_analysis_pavlos/dec_10/fastq/NGS0990_R1.fastq.gz NGS0990/raw_fastq/NGS0990_R1.fastq.gz;
[Thu Jan 28 19:50:07 2021]
Finished job 16.
9 of 164 steps (5%) done
Select jobs to execute...
[Thu Jan 28 19:50:07 2021]
Finished job 1.
10 of 164 steps (6%) done

[Thu Jan 28 19:50:08 2021]
rule link_raw_data:
    input: /home/maria/covid_analysis_pavlos/dec_10/fastq/NGS1043_R1.fastq.gz
    output: NGS1043/raw_fastq/NGS1043_R1.fastq.gz
    jobid: 13
    wildcards: sn=NGS1043, r=1
    priority: 4

echo 1; mkdir -p NGS1043/raw_fastq/; cp /home/maria/covid_analysis_pavlos/dec_10/fastq/NGS1043_R1.fastq.gz NGS1043/raw_fastq/NGS1043_R1.fastq.gz;
Select jobs to execute...

[Thu Jan 28 19:50:08 2021]
rule link_raw_data:
    input: /home/maria/covid_analysis_pavlos/dec_10/fastq/NGS1042_R1.fastq.gz
    output: NGS1042/raw_fastq/NGS1042_R1.fastq.gz
    jobid: 11
    wildcards: sn=NGS1042, r=1
    priority: 4

echo 1; mkdir -p NGS1042/raw_fastq/; cp /home/maria/covid_analysis_pavlos/dec_10/fastq/NGS1042_R1.fastq.gz NGS1042/raw_fastq/NGS1042_R1.fastq.gz;
[Thu Jan 28 19:50:14 2021]
Finished job 13.
11 of 164 steps (7%) done
Select jobs to execute...

[Thu Jan 28 19:50:14 2021]
rule run_raw_fastqc:
    input: NGS1041/raw_fastq/NGS1041_R1.fastq.gz, NGS1041/raw_fastq/NGS1041_R2.fastq.gz
    output: NGS1041/raw_fastq/NGS1041_R1_fastqc.html, NGS1041/raw_fastq/NGS1041_R2_fastqc.html
    log: NGS1041/raw_fastq/NGS1041_fastqc.log
    jobid: 59
    benchmark: NGS1041/benchmarks/NGS1041_raw_fastqc.benchmark.tsv
    wildcards: sn=NGS1041


        fastqc -o NGS1041/raw_fastq NGS1041/raw_fastq/NGS1041_R1.fastq.gz NGS1041/raw_fastq/NGS1041_R2.fastq.gz 2> NGS1041/raw_fastq/NGS1041_fastqc.log
        
Activating conda environment: /home/maria/SNAKE_COVID/conda/b95377fd
[Thu Jan 28 19:50:26 2021]
Finished job 15.
12 of 164 steps (7%) done
[Thu Jan 28 19:50:26 2021]
Finished job 12.
13 of 164 steps (8%) done
Select jobs to execute...
[Thu Jan 28 19:50:27 2021]
Finished job 18.
14 of 164 steps (9%) done

[Thu Jan 28 19:50:27 2021]
rule run_raw_fastqc:
    input: NGS1043/raw_fastq/NGS1043_R1.fastq.gz, NGS1043/raw_fastq/NGS1043_R2.fastq.gz
    output: NGS1043/raw_fastq/NGS1043_R1_fastqc.html, NGS1043/raw_fastq/NGS1043_R2_fastqc.html
    log: NGS1043/raw_fastq/NGS1043_fastqc.log
    jobid: 61
    benchmark: NGS1043/benchmarks/NGS1043_raw_fastqc.benchmark.tsv
    wildcards: sn=NGS1043


        fastqc -o NGS1043/raw_fastq NGS1043/raw_fastq/NGS1043_R1.fastq.gz NGS1043/raw_fastq/NGS1043_R2.fastq.gz 2> NGS1043/raw_fastq/NGS1043_fastqc.log
        

[Thu Jan 28 19:50:27 2021]
rule viral_reference_bwa_build:
    input: /home/maria/covid_analysis_pavlos/covid-19-signal/data/MN908947.3.fasta
    output: NGS0990/core/viral_reference.bwt
    log: NGS0990/core/NGS0990_viral_reference_bwa-build.log
    jobid: 68
    benchmark: NGS0990/benchmarks/NGS0990_reference_bwa_build.benchmark.tsv
    wildcards: sn=NGS0990

bwa index -p NGS0990/core/viral_reference /home/maria/covid_analysis_pavlos/covid-19-signal/data/MN908947.3.fasta >NGS0990/core/NGS0990_viral_reference_bwa-build.log 2>&1

[Thu Jan 28 19:50:27 2021]
rule viral_reference_bwa_build:
    input: /home/maria/covid_analysis_pavlos/covid-19-signal/data/MN908947.3.fasta
    output: NGS1040/core/viral_reference.bwt
    log: NGS1040/core/NGS1040_viral_reference_bwa-build.log
    jobid: 83
    benchmark: NGS1040/benchmarks/NGS1040_reference_bwa_build.benchmark.tsv
    wildcards: sn=NGS1040

bwa index -p NGS1040/core/viral_reference /home/maria/covid_analysis_pavlos/covid-19-signal/data/MN908947.3.fasta >NGS1040/core/NGS1040_viral_reference_bwa-build.log 2>&1
Select jobs to execute...
Select jobs to execute...
Activating conda environment: /home/maria/SNAKE_COVID/conda/b95377fd
Activating conda environment: /home/maria/SNAKE_COVID/conda/3850436d
Activating conda environment: /home/maria/SNAKE_COVID/conda/3850436d
[Thu Jan 28 19:50:33 2021]
Finished job 8.
15 of 164 steps (9%) done
Select jobs to execute...

[Thu Jan 28 19:50:33 2021]
rule run_raw_fastqc:
    input: NGS1044/raw_fastq/NGS1044_R1.fastq.gz, NGS1044/raw_fastq/NGS1044_R2.fastq.gz
    output: NGS1044/raw_fastq/NGS1044_R1_fastqc.html, NGS1044/raw_fastq/NGS1044_R2_fastqc.html
    log: NGS1044/raw_fastq/NGS1044_fastqc.log
    jobid: 62
    benchmark: NGS1044/benchmarks/NGS1044_raw_fastqc.benchmark.tsv
    wildcards: sn=NGS1044


        fastqc -o NGS1044/raw_fastq NGS1044/raw_fastq/NGS1044_R1.fastq.gz NGS1044/raw_fastq/NGS1044_R2.fastq.gz 2> NGS1044/raw_fastq/NGS1044_fastqc.log
        
[Thu Jan 28 19:50:35 2021]
Finished job 17.
16 of 164 steps (10%) done
[Thu Jan 28 19:50:35 2021]
Finished job 68.
17 of 164 steps (10%) done
Select jobs to execute...
[Thu Jan 28 19:50:35 2021]
Finished job 83.
18 of 164 steps (11%) done

[Thu Jan 28 19:50:35 2021]
rule viral_reference_bwa_build:
    input: /home/maria/covid_analysis_pavlos/covid-19-signal/data/MN908947.3.fasta
    output: NGS1042/core/viral_reference.bwt
    log: NGS1042/core/NGS1042_viral_reference_bwa-build.log
    jobid: 93
    benchmark: NGS1042/benchmarks/NGS1042_reference_bwa_build.benchmark.tsv
    wildcards: sn=NGS1042

bwa index -p NGS1042/core/viral_reference /home/maria/covid_analysis_pavlos/covid-19-signal/data/MN908947.3.fasta >NGS1042/core/NGS1042_viral_reference_bwa-build.log 2>&1

[Thu Jan 28 19:50:35 2021]
rule viral_reference_bwa_build:
    input: /home/maria/covid_analysis_pavlos/covid-19-signal/data/MN908947.3.fasta
    output: NGS1001/core/viral_reference.bwt
    log: NGS1001/core/NGS1001_viral_reference_bwa-build.log
    jobid: 78
    benchmark: NGS1001/benchmarks/NGS1001_reference_bwa_build.benchmark.tsv
    wildcards: sn=NGS1001

bwa index -p NGS1001/core/viral_reference /home/maria/covid_analysis_pavlos/covid-19-signal/data/MN908947.3.fasta >NGS1001/core/NGS1001_viral_reference_bwa-build.log 2>&1

[Thu Jan 28 19:50:36 2021]
rule run_raw_fastqc:
    input: NGS0990/raw_fastq/NGS0990_R1.fastq.gz, NGS0990/raw_fastq/NGS0990_R2.fastq.gz
    output: NGS0990/raw_fastq/NGS0990_R1_fastqc.html, NGS0990/raw_fastq/NGS0990_R2_fastqc.html
    log: NGS0990/raw_fastq/NGS0990_fastqc.log
    jobid: 55
    benchmark: NGS0990/benchmarks/NGS0990_raw_fastqc.benchmark.tsv
    wildcards: sn=NGS0990


        fastqc -o NGS0990/raw_fastq NGS0990/raw_fastq/NGS0990_R1.fastq.gz NGS0990/raw_fastq/NGS0990_R2.fastq.gz 2> NGS0990/raw_fastq/NGS0990_fastqc.log
        
Select jobs to execute...
Select jobs to execute...
Activating conda environment: /home/maria/SNAKE_COVID/conda/b95377fd
Activating conda environment: /home/maria/SNAKE_COVID/conda/3850436d
Activating conda environment: /home/maria/SNAKE_COVID/conda/3850436d
[Thu Jan 28 19:50:38 2021]
Finished job 7.
19 of 164 steps (12%) done
Select jobs to execute...

[Thu Jan 28 19:50:38 2021]
rule viral_reference_bwa_build:
    input: /home/maria/covid_analysis_pavlos/covid-19-signal/data/MN908947.3.fasta
    output: NGS1044/core/viral_reference.bwt
    log: NGS1044/core/NGS1044_viral_reference_bwa-build.log
    jobid: 103
    benchmark: NGS1044/benchmarks/NGS1044_reference_bwa_build.benchmark.tsv
    wildcards: sn=NGS1044

bwa index -p NGS1044/core/viral_reference /home/maria/covid_analysis_pavlos/covid-19-signal/data/MN908947.3.fasta >NGS1044/core/NGS1044_viral_reference_bwa-build.log 2>&1
Activating conda environment: /home/maria/SNAKE_COVID/conda/b95377fd
[Thu Jan 28 19:50:39 2021]
Finished job 11.
20 of 164 steps (12%) done
Select jobs to execute...

[Thu Jan 28 19:50:39 2021]
rule run_raw_fastqc:
    input: NGS1040/raw_fastq/NGS1040_R1.fastq.gz, NGS1040/raw_fastq/NGS1040_R2.fastq.gz
    output: NGS1040/raw_fastq/NGS1040_R1_fastqc.html, NGS1040/raw_fastq/NGS1040_R2_fastqc.html
    log: NGS1040/raw_fastq/NGS1040_fastqc.log
    jobid: 58
    benchmark: NGS1040/benchmarks/NGS1040_raw_fastqc.benchmark.tsv
    wildcards: sn=NGS1040


        fastqc -o NGS1040/raw_fastq NGS1040/raw_fastq/NGS1040_R1.fastq.gz NGS1040/raw_fastq/NGS1040_R2.fastq.gz 2> NGS1040/raw_fastq/NGS1040_fastqc.log
        
[Thu Jan 28 19:50:39 2021]
Finished job 93.
21 of 164 steps (13%) done
[Thu Jan 28 19:50:39 2021]
Finished job 78.
22 of 164 steps (13%) done
Select jobs to execute...

[Thu Jan 28 19:50:39 2021]
rule run_raw_fastqc:
    input: NGS1001/raw_fastq/NGS1001_R1.fastq.gz, NGS1001/raw_fastq/NGS1001_R2.fastq.gz
    output: NGS1001/raw_fastq/NGS1001_R1_fastqc.html, NGS1001/raw_fastq/NGS1001_R2_fastqc.html
    log: NGS1001/raw_fastq/NGS1001_fastqc.log
    jobid: 57
    benchmark: NGS1001/benchmarks/NGS1001_raw_fastqc.benchmark.tsv
    wildcards: sn=NGS1001


        fastqc -o NGS1001/raw_fastq NGS1001/raw_fastq/NGS1001_R1.fastq.gz NGS1001/raw_fastq/NGS1001_R2.fastq.gz 2> NGS1001/raw_fastq/NGS1001_fastqc.log
        

[Thu Jan 28 19:50:39 2021]
rule run_raw_fastqc:
    input: NGS1000/raw_fastq/NGS1000_R1.fastq.gz, NGS1000/raw_fastq/NGS1000_R2.fastq.gz
    output: NGS1000/raw_fastq/NGS1000_R1_fastqc.html, NGS1000/raw_fastq/NGS1000_R2_fastqc.html
    log: NGS1000/raw_fastq/NGS1000_fastqc.log
    jobid: 56
    benchmark: NGS1000/benchmarks/NGS1000_raw_fastqc.benchmark.tsv
    wildcards: sn=NGS1000


        fastqc -o NGS1000/raw_fastq NGS1000/raw_fastq/NGS1000_R1.fastq.gz NGS1000/raw_fastq/NGS1000_R2.fastq.gz 2> NGS1000/raw_fastq/NGS1000_fastqc.log
        
Select jobs to execute...
Activating conda environment: /home/maria/SNAKE_COVID/conda/3850436d
[Thu Jan 28 19:50:42 2021]
Finished job 103.
23 of 164 steps (14%) done
Select jobs to execute...

[Thu Jan 28 19:50:42 2021]
rule viral_reference_bwa_build:
    input: /home/maria/covid_analysis_pavlos/covid-19-signal/data/MN908947.3.fasta
    output: NGS1045/core/viral_reference.bwt
    log: NGS1045/core/NGS1045_viral_reference_bwa-build.log
    jobid: 108
    benchmark: NGS1045/benchmarks/NGS1045_reference_bwa_build.benchmark.tsv
    wildcards: sn=NGS1045

bwa index -p NGS1045/core/viral_reference /home/maria/covid_analysis_pavlos/covid-19-signal/data/MN908947.3.fasta >NGS1045/core/NGS1045_viral_reference_bwa-build.log 2>&1
Activating conda environment: /home/maria/SNAKE_COVID/conda/b95377fd
Activating conda environment: /home/maria/SNAKE_COVID/conda/b95377fd
Activating conda environment: /home/maria/SNAKE_COVID/conda/b95377fd
Activating conda environment: /home/maria/SNAKE_COVID/conda/3850436d
[Thu Jan 28 19:50:46 2021]
Finished job 108.
24 of 164 steps (15%) done
Select jobs to execute...

[Thu Jan 28 19:50:46 2021]
rule run_raw_fastqc:
    input: NGS1042/raw_fastq/NGS1042_R1.fastq.gz, NGS1042/raw_fastq/NGS1042_R2.fastq.gz
    output: NGS1042/raw_fastq/NGS1042_R1_fastqc.html, NGS1042/raw_fastq/NGS1042_R2_fastqc.html
    log: NGS1042/raw_fastq/NGS1042_fastqc.log
    jobid: 60
    benchmark: NGS1042/benchmarks/NGS1042_raw_fastqc.benchmark.tsv
    wildcards: sn=NGS1042


        fastqc -o NGS1042/raw_fastq NGS1042/raw_fastq/NGS1042_R1.fastq.gz NGS1042/raw_fastq/NGS1042_R2.fastq.gz 2> NGS1042/raw_fastq/NGS1042_fastqc.log
        
Activating conda environment: /home/maria/SNAKE_COVID/conda/b95377fd
[Thu Jan 28 19:50:51 2021]
Finished job 61.
25 of 164 steps (15%) done
Select jobs to execute...

[Thu Jan 28 19:50:51 2021]
rule viral_reference_bwa_build:
    input: /home/maria/covid_analysis_pavlos/covid-19-signal/data/MN908947.3.fasta
    output: NGS1000/core/viral_reference.bwt
    log: NGS1000/core/NGS1000_viral_reference_bwa-build.log
    jobid: 73
    benchmark: NGS1000/benchmarks/NGS1000_reference_bwa_build.benchmark.tsv
    wildcards: sn=NGS1000

bwa index -p NGS1000/core/viral_reference /home/maria/covid_analysis_pavlos/covid-19-signal/data/MN908947.3.fasta >NGS1000/core/NGS1000_viral_reference_bwa-build.log 2>&1
Activating conda environment: /home/maria/SNAKE_COVID/conda/3850436d
[Thu Jan 28 19:50:55 2021]
Finished job 73.
26 of 164 steps (16%) done
Select jobs to execute...

[Thu Jan 28 19:50:55 2021]
rule viral_reference_bwa_build:
    input: /home/maria/covid_analysis_pavlos/covid-19-signal/data/MN908947.3.fasta
    output: NGS1041/core/viral_reference.bwt
    log: NGS1041/core/NGS1041_viral_reference_bwa-build.log
    jobid: 88
    benchmark: NGS1041/benchmarks/NGS1041_reference_bwa_build.benchmark.tsv
    wildcards: sn=NGS1041

bwa index -p NGS1041/core/viral_reference /home/maria/covid_analysis_pavlos/covid-19-signal/data/MN908947.3.fasta >NGS1041/core/NGS1041_viral_reference_bwa-build.log 2>&1
[Thu Jan 28 19:50:57 2021]
Finished job 55.
27 of 164 steps (16%) done
Select jobs to execute...

[Thu Jan 28 19:50:57 2021]
rule run_raw_fastqc:
    input: NGS1045/raw_fastq/NGS1045_R1.fastq.gz, NGS1045/raw_fastq/NGS1045_R2.fastq.gz
    output: NGS1045/raw_fastq/NGS1045_R1_fastqc.html, NGS1045/raw_fastq/NGS1045_R2_fastqc.html
    log: NGS1045/raw_fastq/NGS1045_fastqc.log
    jobid: 63
    benchmark: NGS1045/benchmarks/NGS1045_raw_fastqc.benchmark.tsv
    wildcards: sn=NGS1045


        fastqc -o NGS1045/raw_fastq NGS1045/raw_fastq/NGS1045_R1.fastq.gz NGS1045/raw_fastq/NGS1045_R2.fastq.gz 2> NGS1045/raw_fastq/NGS1045_fastqc.log
        
Activating conda environment: /home/maria/SNAKE_COVID/conda/3850436d
[Thu Jan 28 19:50:58 2021]
Finished job 88.
28 of 164 steps (17%) done
Select jobs to execute...

[Thu Jan 28 19:50:58 2021]
rule copy_config_sample_log:
    input: /home/maria/covid_analysis_pavlos/covid-19-signal/config.yaml, /home/maria/covid_analysis_pavlos/covid-19-signal/tal_table.csv
    output: config.yaml, tal_table.csv
    jobid: 164


        cp /home/maria/covid_analysis_pavlos/covid-19-signal/config.yaml config.yaml
        cp /home/maria/covid_analysis_pavlos/covid-19-signal/tal_table.csv tal_table.csv
        
[Thu Jan 28 19:50:58 2021]
Finished job 164.
29 of 164 steps (18%) done
Select jobs to execute...

[Thu Jan 28 19:50:58 2021]
rule viral_reference_bwa_build:
    input: /home/maria/covid_analysis_pavlos/covid-19-signal/data/MN908947.3.fasta
    output: NGS1043/core/viral_reference.bwt
    log: NGS1043/core/NGS1043_viral_reference_bwa-build.log
    jobid: 98
    benchmark: NGS1043/benchmarks/NGS1043_reference_bwa_build.benchmark.tsv
    wildcards: sn=NGS1043

bwa index -p NGS1043/core/viral_reference /home/maria/covid_analysis_pavlos/covid-19-signal/data/MN908947.3.fasta >NGS1043/core/NGS1043_viral_reference_bwa-build.log 2>&1
Activating conda environment: /home/maria/SNAKE_COVID/conda/b95377fd
Activating conda environment: /home/maria/SNAKE_COVID/conda/3850436d
[Thu Jan 28 19:51:01 2021]
Finished job 98.
30 of 164 steps (18%) done
Select jobs to execute...
Failed to solve scheduling problem with ILP solver. Falling back to greedy solver.Run Snakemake with --verbose to see the full solver output for debugging the problem.
[Thu Jan 28 19:51:03 2021]
Finished job 57.
31 of 164 steps (19%) done
Select jobs to execute...
Failed to solve scheduling problem with ILP solver. Falling back to greedy solver.Run Snakemake with --verbose to see the full solver output for debugging the problem.
[Thu Jan 28 19:51:04 2021]
Finished job 56.
32 of 164 steps (20%) done
Select jobs to execute...
Failed to solve scheduling problem with ILP solver. Falling back to greedy solver.Run Snakemake with --verbose to see the full solver output for debugging the problem.
[Thu Jan 28 19:51:09 2021]
Finished job 59.
33 of 164 steps (20%) done
Select jobs to execute...

[Thu Jan 28 19:51:10 2021]
rule raw_reads_composite_reference_bwa_map:
    input: NGS1000/raw_fastq/NGS1000_R1.fastq.gz, NGS1000/raw_fastq/NGS1000_R2.fastq.gz
    output: NGS1000/host_removal/NGS1000_viral_and_nonmapping_reads.bam
    log: NGS1000/host_removal/NGS1000_human_read_mapping.log
    jobid: 22
    benchmark: NGS1000/benchmarks/NGS1000_composite_reference_bwa_map.benchmark.tsv
    wildcards: sn=NGS1000
    threads: 4

(conda info --envs; bwa mem -t 4 /home/maria/covid_analysis_pavlos/covid-19-signal/data/composite_human_viral_reference.fna NGS1000/raw_fastq/NGS1000_R1.fastq.gz NGS1000/raw_fastq/NGS1000_R2.fastq.gz | /home/maria/covid_analysis_pavlos/covid-19-signal/scripts/filter_non_human_reads.py -c MN908947.3 > NGS1000/host_removal/NGS1000_viral_and_nonmapping_reads.bam) 2> NGS1000/host_removal/NGS1000_human_read_mapping.log
Activating conda environment: /home/maria/SNAKE_COVID/conda/3850436d
[Thu Jan 28 19:52:02 2021]
Finished job 62.
34 of 164 steps (21%) done
Select jobs to execute...
Failed to solve scheduling problem with ILP solver. Falling back to greedy solver.Run Snakemake with --verbose to see the full solver output for debugging the problem.
[Thu Jan 28 19:52:52 2021]
Finished job 60.
35 of 164 steps (21%) done
Select jobs to execute...
Failed to solve scheduling problem with ILP solver. Falling back to greedy solver.Run Snakemake with --verbose to see the full solver output for debugging the problem.
[Thu Jan 28 19:53:11 2021]
Finished job 63.
36 of 164 steps (22%) done
Select jobs to execute...
Failed to solve scheduling problem with ILP solver. Falling back to greedy solver.Run Snakemake with --verbose to see the full solver output for debugging the problem.
[Thu Jan 28 19:53:20 2021]
Finished job 58.
37 of 164 steps (23%) done
Select jobs to execute...

[Thu Jan 28 19:53:20 2021]
rule raw_reads_composite_reference_bwa_map:
    input: NGS1045/raw_fastq/NGS1045_R1.fastq.gz, NGS1045/raw_fastq/NGS1045_R2.fastq.gz
    output: NGS1045/host_removal/NGS1045_viral_and_nonmapping_reads.bam
    log: NGS1045/host_removal/NGS1045_human_read_mapping.log
    jobid: 36
    benchmark: NGS1045/benchmarks/NGS1045_composite_reference_bwa_map.benchmark.tsv
    wildcards: sn=NGS1045
    threads: 4

(conda info --envs; bwa mem -t 4 /home/maria/covid_analysis_pavlos/covid-19-signal/data/composite_human_viral_reference.fna NGS1045/raw_fastq/NGS1045_R1.fastq.gz NGS1045/raw_fastq/NGS1045_R2.fastq.gz | /home/maria/covid_analysis_pavlos/covid-19-signal/scripts/filter_non_human_reads.py -c MN908947.3 > NGS1045/host_removal/NGS1045_viral_and_nonmapping_reads.bam) 2> NGS1045/host_removal/NGS1045_human_read_mapping.log
Activating conda environment: /home/maria/SNAKE_COVID/conda/3850436d
[Thu Jan 28 19:55:52 2021]
Finished job 22.
38 of 164 steps (23%) done
Select jobs to execute...

[Thu Jan 28 19:55:52 2021]
rule raw_reads_composite_reference_bwa_map:
    input: NGS1040/raw_fastq/NGS1040_R1.fastq.gz, NGS1040/raw_fastq/NGS1040_R2.fastq.gz
    output: NGS1040/host_removal/NGS1040_viral_and_nonmapping_reads.bam
    log: NGS1040/host_removal/NGS1040_human_read_mapping.log
    jobid: 26
    benchmark: NGS1040/benchmarks/NGS1040_composite_reference_bwa_map.benchmark.tsv
    wildcards: sn=NGS1040
    threads: 4

(conda info --envs; bwa mem -t 4 /home/maria/covid_analysis_pavlos/covid-19-signal/data/composite_human_viral_reference.fna NGS1040/raw_fastq/NGS1040_R1.fastq.gz NGS1040/raw_fastq/NGS1040_R2.fastq.gz | /home/maria/covid_analysis_pavlos/covid-19-signal/scripts/filter_non_human_reads.py -c MN908947.3 > NGS1040/host_removal/NGS1040_viral_and_nonmapping_reads.bam) 2> NGS1040/host_removal/NGS1040_human_read_mapping.log
Activating conda environment: /home/maria/SNAKE_COVID/conda/3850436d
[Thu Jan 28 20:06:02 2021]
Finished job 36.
39 of 164 steps (24%) done
Select jobs to execute...

[Thu Jan 28 20:06:02 2021]
rule raw_reads_composite_reference_bwa_map:
    input: NGS1044/raw_fastq/NGS1044_R1.fastq.gz, NGS1044/raw_fastq/NGS1044_R2.fastq.gz
    output: NGS1044/host_removal/NGS1044_viral_and_nonmapping_reads.bam
    log: NGS1044/host_removal/NGS1044_human_read_mapping.log
    jobid: 34
    benchmark: NGS1044/benchmarks/NGS1044_composite_reference_bwa_map.benchmark.tsv
    wildcards: sn=NGS1044
    threads: 4

(conda info --envs; bwa mem -t 4 /home/maria/covid_analysis_pavlos/covid-19-signal/data/composite_human_viral_reference.fna NGS1044/raw_fastq/NGS1044_R1.fastq.gz NGS1044/raw_fastq/NGS1044_R2.fastq.gz | /home/maria/covid_analysis_pavlos/covid-19-signal/scripts/filter_non_human_reads.py -c MN908947.3 > NGS1044/host_removal/NGS1044_viral_and_nonmapping_reads.bam) 2> NGS1044/host_removal/NGS1044_human_read_mapping.log
Activating conda environment: /home/maria/SNAKE_COVID/conda/3850436d
[Thu Jan 28 20:12:01 2021]
Finished job 26.
40 of 164 steps (24%) done
Select jobs to execute...

[Thu Jan 28 20:12:01 2021]
rule get_host_removed_reads:
    input: NGS1045/host_removal/NGS1045_viral_and_nonmapping_reads.bam
    output: NGS1045/host_removal/NGS1045_R1.fastq.gz, NGS1045/host_removal/NGS1045_R2.fastq.gz, NGS1045/host_removal/NGS1045_singletons.fastq.gz, NGS1045/host_removal/NGS1045_viral_and_nonmapping_reads_filtered_sorted.bam
    log: NGS1045/host_removal/NGS1045_samtools_fastq.log
    jobid: 35
    benchmark: NGS1045/benchmarks/NGS1045_get_host_removed_reads.benchmark.tsv
    wildcards: sn=NGS1045
    threads: 2


        samtools view -b NGS1045/host_removal/NGS1045_viral_and_nonmapping_reads.bam | samtools sort -n -@2 > NGS1045/host_removal/NGS1045_viral_and_nonmapping_reads_filtered_sorted.bam 2> NGS1045/host_removal/NGS1045_samtools_fastq.log
        samtools fastq -1 NGS1045/host_removal/NGS1045_R1.fastq.gz -2 NGS1045/host_removal/NGS1045_R2.fastq.gz -s NGS1045/host_removal/NGS1045_singletons.fastq.gz NGS1045/host_removal/NGS1045_viral_and_nonmapping_reads_filtered_sorted.bam 2>> NGS1045/host_removal/NGS1045_samtools_fastq.log 
        

[Thu Jan 28 20:12:01 2021]
rule get_host_removed_reads:
    input: NGS1000/host_removal/NGS1000_viral_and_nonmapping_reads.bam
    output: NGS1000/host_removal/NGS1000_R1.fastq.gz, NGS1000/host_removal/NGS1000_R2.fastq.gz, NGS1000/host_removal/NGS1000_singletons.fastq.gz, NGS1000/host_removal/NGS1000_viral_and_nonmapping_reads_filtered_sorted.bam
    log: NGS1000/host_removal/NGS1000_samtools_fastq.log
    jobid: 21
    benchmark: NGS1000/benchmarks/NGS1000_get_host_removed_reads.benchmark.tsv
    wildcards: sn=NGS1000
    threads: 2


        samtools view -b NGS1000/host_removal/NGS1000_viral_and_nonmapping_reads.bam | samtools sort -n -@2 > NGS1000/host_removal/NGS1000_viral_and_nonmapping_reads_filtered_sorted.bam 2> NGS1000/host_removal/NGS1000_samtools_fastq.log
        samtools fastq -1 NGS1000/host_removal/NGS1000_R1.fastq.gz -2 NGS1000/host_removal/NGS1000_R2.fastq.gz -s NGS1000/host_removal/NGS1000_singletons.fastq.gz NGS1000/host_removal/NGS1000_viral_and_nonmapping_reads_filtered_sorted.bam 2>> NGS1000/host_removal/NGS1000_samtools_fastq.log 
        
Activating conda environment: /home/maria/SNAKE_COVID/conda/3850436d
Activating conda environment: /home/maria/SNAKE_COVID/conda/3850436d
[Thu Jan 28 20:12:59 2021]
Finished job 21.
41 of 164 steps (25%) done
Select jobs to execute...

[Thu Jan 28 20:12:59 2021]
rule run_trimgalore:
    input: NGS1000/host_removal/NGS1000_R1.fastq.gz, NGS1000/host_removal/NGS1000_R2.fastq.gz
    output: NGS1000/adapter_trimmed/NGS1000_R1_val_1.fq.gz, NGS1000/adapter_trimmed/NGS1000_R2_val_2.fq.gz, NGS1000/adapter_trimmed/NGS1000_R1_val_1_fastqc.html, NGS1000/adapter_trimmed/NGS1000_R2_val_2_fastqc.html
    log: NGS1000/adapter_trimmed/NGS1000_trim_galore.log
    jobid: 38
    benchmark: NGS1000/benchmarks/NGS1000_trimgalore.benchmark.tsv
    wildcards: sn=NGS1000
    priority: 2
    threads: 2

trim_galore --quality 20 --length 20  -o NGS1000/adapter_trimmed --cores 2 --fastqc --paired NGS1000/host_removal/NGS1000_R1.fastq.gz NGS1000/host_removal/NGS1000_R2.fastq.gz 2> NGS1000/adapter_trimmed/NGS1000_trim_galore.log
Activating conda environment: /home/maria/SNAKE_COVID/conda/b95377fd
[Thu Jan 28 20:13:55 2021]
Finished job 38.
42 of 164 steps (26%) done
Select jobs to execute...

[Thu Jan 28 20:13:55 2021]
rule run_filtering_of_residual_adapters:
    input: NGS1000/adapter_trimmed/NGS1000_R1_val_1.fq.gz, NGS1000/adapter_trimmed/NGS1000_R2_val_2.fq.gz
    output: NGS1000/adapter_trimmed/NGS1000_R1_val_1_posttrim_filter.fq.gz, NGS1000/adapter_trimmed/NGS1000_R2_val_2_posttrim_filter.fq.gz
    jobid: 47
    wildcards: sn=NGS1000
    priority: 2
    threads: 2


	python3.6 /home/maria/covid_analysis_pavlos/covid-19-signal/scripts/filter_residual_adapters.py --input_R1 NGS1000/adapter_trimmed/NGS1000_R1_val_1.fq.gz --input_R2 NGS1000/adapter_trimmed/NGS1000_R2_val_2.fq.gz
	
Activating conda environment: /home/maria/SNAKE_COVID/conda/3850436d
[Thu Jan 28 20:17:07 2021]
Finished job 47.
43 of 164 steps (26%) done
Select jobs to execute...

[Thu Jan 28 20:17:07 2021]
rule get_host_removed_reads:
    input: NGS1040/host_removal/NGS1040_viral_and_nonmapping_reads.bam
    output: NGS1040/host_removal/NGS1040_R1.fastq.gz, NGS1040/host_removal/NGS1040_R2.fastq.gz, NGS1040/host_removal/NGS1040_singletons.fastq.gz, NGS1040/host_removal/NGS1040_viral_and_nonmapping_reads_filtered_sorted.bam
    log: NGS1040/host_removal/NGS1040_samtools_fastq.log
    jobid: 25
    benchmark: NGS1040/benchmarks/NGS1040_get_host_removed_reads.benchmark.tsv
    wildcards: sn=NGS1040
    threads: 2


        samtools view -b NGS1040/host_removal/NGS1040_viral_and_nonmapping_reads.bam | samtools sort -n -@2 > NGS1040/host_removal/NGS1040_viral_and_nonmapping_reads_filtered_sorted.bam 2> NGS1040/host_removal/NGS1040_samtools_fastq.log
        samtools fastq -1 NGS1040/host_removal/NGS1040_R1.fastq.gz -2 NGS1040/host_removal/NGS1040_R2.fastq.gz -s NGS1040/host_removal/NGS1040_singletons.fastq.gz NGS1040/host_removal/NGS1040_viral_and_nonmapping_reads_filtered_sorted.bam 2>> NGS1040/host_removal/NGS1040_samtools_fastq.log 
        
Activating conda environment: /home/maria/SNAKE_COVID/conda/3850436d
[Thu Jan 28 20:18:56 2021]
Finished job 34.
44 of 164 steps (27%) done
Select jobs to execute...

[Thu Jan 28 20:18:56 2021]
rule viral_reference_bwa_map:
    input: NGS1000/adapter_trimmed/NGS1000_R1_val_1_posttrim_filter.fq.gz, NGS1000/adapter_trimmed/NGS1000_R2_val_2_posttrim_filter.fq.gz, NGS1000/core/viral_reference.bwt
    output: NGS1000/core/NGS1000_viral_reference.bam
    log: NGS1000/core/NGS1000_viral_reference_bwa.log
    jobid: 72
    benchmark: NGS1000/benchmarks/NGS1000_viral_reference_bwa_map.benchmark.tsv
    wildcards: sn=NGS1000
    threads: 2

(bwa mem -t 2 NGS1000/core/viral_reference NGS1000/adapter_trimmed/NGS1000_R1_val_1_posttrim_filter.fq.gz NGS1000/adapter_trimmed/NGS1000_R2_val_2_posttrim_filter.fq.gz | samtools view -bS | samtools sort -@2 -o NGS1000/core/NGS1000_viral_reference.bam) 2> NGS1000/core/NGS1000_viral_reference_bwa.log

[Thu Jan 28 20:18:56 2021]
rule get_host_removed_reads:
    input: NGS1044/host_removal/NGS1044_viral_and_nonmapping_reads.bam
    output: NGS1044/host_removal/NGS1044_R1.fastq.gz, NGS1044/host_removal/NGS1044_R2.fastq.gz, NGS1044/host_removal/NGS1044_singletons.fastq.gz, NGS1044/host_removal/NGS1044_viral_and_nonmapping_reads_filtered_sorted.bam
    log: NGS1044/host_removal/NGS1044_samtools_fastq.log
    jobid: 33
    benchmark: NGS1044/benchmarks/NGS1044_get_host_removed_reads.benchmark.tsv
    wildcards: sn=NGS1044
    threads: 2


        samtools view -b NGS1044/host_removal/NGS1044_viral_and_nonmapping_reads.bam | samtools sort -n -@2 > NGS1044/host_removal/NGS1044_viral_and_nonmapping_reads_filtered_sorted.bam 2> NGS1044/host_removal/NGS1044_samtools_fastq.log
        samtools fastq -1 NGS1044/host_removal/NGS1044_R1.fastq.gz -2 NGS1044/host_removal/NGS1044_R2.fastq.gz -s NGS1044/host_removal/NGS1044_singletons.fastq.gz NGS1044/host_removal/NGS1044_viral_and_nonmapping_reads_filtered_sorted.bam 2>> NGS1044/host_removal/NGS1044_samtools_fastq.log 
        
Activating conda environment: /home/maria/SNAKE_COVID/conda/3850436d
Activating conda environment: /home/maria/SNAKE_COVID/conda/3850436d
[Thu Jan 28 20:19:37 2021]
Finished job 72.
45 of 164 steps (27%) done
Select jobs to execute...

[Thu Jan 28 20:19:37 2021]
rule run_kraken2:
    input: NGS1000/adapter_trimmed/NGS1000_R1_val_1_posttrim_filter.fq.gz, NGS1000/adapter_trimmed/NGS1000_R2_val_2_posttrim_filter.fq.gz
    output: NGS1000/kraken2/NGS1000_kraken2.out
    log: NGS1000/kraken2/NGS1000_kraken2.log
    jobid: 147
    benchmark: NGS1000/benchmarks/NGS1000_run_kraken2.benchmark.tsv
    wildcards: sn=NGS1000

cd NGS1000/kraken2 && kraken2 --db /home/maria/covid_analysis_pavlos/covid-19-signal/data/Kraken2/db --threads 1 --quick --unclassified-out "NGS1000_kraken2_unclassified_reads#" --classified-out "NGS1000_kraken2_classified_reads#" --output NGS1000_kraken2.out --paired --gzip-compressed ../../NGS1000/adapter_trimmed/NGS1000_R1_val_1_posttrim_filter.fq.gz ../../NGS1000/adapter_trimmed/NGS1000_R2_val_2_posttrim_filter.fq.gz --report NGS1000_kraken2.report 2>../../NGS1000/kraken2/NGS1000_kraken2.log

[Thu Jan 28 20:19:37 2021]
rule run_bed_primer_trim:
    input: NGS1000/core/NGS1000_viral_reference.bam
    output: NGS1000/core/NGS1000_viral_reference.mapping.primertrimmed.sorted.bam, NGS1000/core/NGS1000_viral_reference.mapping.primertrimmed.bam, NGS1000/core/NGS1000_viral_reference.mapping.bam
    log: NGS1000/core/NGS1000_ivar_trim.log
    jobid: 71
    benchmark: NGS1000/benchmarks/NGS1000_bed_primer_trim.benchmark.tsv
    wildcards: sn=NGS1000

samtools view -F4 -o NGS1000/core/NGS1000_viral_reference.mapping.bam NGS1000/core/NGS1000_viral_reference.bam; samtools index NGS1000/core/NGS1000_viral_reference.mapping.bam; ivar trim -e -i NGS1000/core/NGS1000_viral_reference.mapping.bam -b /home/maria/covid_analysis_pavlos/covid-19-signal/resources/SARSCoV2.paragon.bed -m 20 -q 20 -p NGS1000/core/NGS1000_viral_reference.mapping.primertrimmed 2> NGS1000/core/NGS1000_ivar_trim.log; samtools sort -o NGS1000/core/NGS1000_viral_reference.mapping.primertrimmed.sorted.bam NGS1000/core/NGS1000_viral_reference.mapping.primertrimmed.bam
Activating conda environment: /home/maria/SNAKE_COVID/conda/b95377fd
Activating conda environment: /home/maria/SNAKE_COVID/conda/5258de7f
[Thu Jan 28 20:19:58 2021]
Finished job 147.
46 of 164 steps (28%) done
Select jobs to execute...
Failed to solve scheduling problem with ILP solver. Falling back to greedy solver.Run Snakemake with --verbose to see the full solver output for debugging the problem.
[Thu Jan 28 20:22:06 2021]
Finished job 71.
47 of 164 steps (29%) done
Select jobs to execute...

[Thu Jan 28 20:22:06 2021]
rule get_mapping_reads:
    input: NGS1000/core/NGS1000_viral_reference.mapping.primertrimmed.bam
    output: NGS1000/mapped_clean_reads/NGS1000_R1.fastq.gz, NGS1000/mapped_clean_reads/NGS1000_R2.fastq.gz, NGS1000/mapped_clean_reads/NGS1000_singletons.fastq.gz, NGS1000/mapped_clean_reads/NGS1000_sorted_clean.bam
    log: NGS1000/mapped_clean_reads/NGS1000_samtools_fastq.log
    jobid: 70
    benchmark: NGS1000/benchmarks/NGS1000_get_mapping_reads.benchmark.tsv
    wildcards: sn=NGS1000
    priority: 2


        samtools sort -n NGS1000/core/NGS1000_viral_reference.mapping.primertrimmed.bam -o NGS1000/mapped_clean_reads/NGS1000_sorted_clean.bam 2> NGS1000/mapped_clean_reads/NGS1000_samtools_fastq.log
        samtools fastq -1 NGS1000/mapped_clean_reads/NGS1000_R1.fastq.gz -2 NGS1000/mapped_clean_reads/NGS1000_R2.fastq.gz -s NGS1000/mapped_clean_reads/NGS1000_singletons.fastq.gz NGS1000/mapped_clean_reads/NGS1000_sorted_clean.bam 2>> NGS1000/mapped_clean_reads/NGS1000_samtools_fastq.log 
        

[Thu Jan 28 20:22:06 2021]
rule run_ivar_consensus:
    input: NGS1000/core/NGS1000_viral_reference.mapping.primertrimmed.sorted.bam
    output: NGS1000/core/NGS1000.consensus.fa
    log: NGS1000/core/NGS1000_ivar_consensus.log
    jobid: 110
    benchmark: NGS1000/benchmarks/NGS1000_ivar_consensus.benchmark.tsv
    wildcards: sn=NGS1000

(samtools mpileup -aa -A -d 100000 -Q0 NGS1000/core/NGS1000_viral_reference.mapping.primertrimmed.sorted.bam | ivar consensus -t 0.75 -m 10 -n N -p NGS1000/core/NGS1000.consensus) 2>NGS1000/core/NGS1000_ivar_consensus.log
Activating conda environment: /home/maria/SNAKE_COVID/conda/3850436d
Activating conda environment: /home/maria/SNAKE_COVID/conda/5258de7f
[Thu Jan 28 20:22:19 2021]
Finished job 110.
48 of 164 steps (29%) done
Select jobs to execute...

[Thu Jan 28 20:22:19 2021]
rule run_quast:
    input: NGS1000/core/NGS1000.consensus.fa
    output: NGS1000/quast/NGS1000_quast_report.html
    log: NGS1000/quast/NGS1000_quast.log
    jobid: 156
    benchmark: NGS1000/benchmarks/NGS1000_run_quast.benchmark.tsv
    wildcards: sn=NGS1000

quast NGS1000/core/NGS1000.consensus.fa -r /home/maria/covid_analysis_pavlos/covid-19-signal/data/MN908947.3.fasta -g /home/maria/covid_analysis_pavlos/covid-19-signal/data/MN908947.3.gff3 --output-dir NGS1000/quast --threads 1 >NGS1000/quast/NGS1000_quast.log && for f in NGS1000/quast/report.*; do mv $f ${f/report/NGS1000_quast_report}; done
Activating conda environment: /home/maria/SNAKE_COVID/conda/2d0610a0
[Thu Jan 28 20:22:24 2021]
Finished job 156.
49 of 164 steps (30%) done
Select jobs to execute...

[Thu Jan 28 20:22:24 2021]
rule coverage_depth:
    input: NGS1000/core/NGS1000_viral_reference.mapping.primertrimmed.sorted.bam
    output: NGS1000/coverage/NGS1000_depth.txt
    jobid: 129
    benchmark: NGS1000/benchmarks/NGS1000_coverage_depth.benchmark.tsv
    wildcards: sn=NGS1000

bedtools genomecov -d -ibam NGS1000/core/NGS1000_viral_reference.mapping.primertrimmed.sorted.bam >NGS1000/coverage/NGS1000_depth.txt
Activating conda environment: /home/maria/SNAKE_COVID/conda/3850436d
[Thu Jan 28 20:22:33 2021]
Finished job 129.
50 of 164 steps (30%) done
Select jobs to execute...

[Thu Jan 28 20:22:33 2021]
rule generate_coverage_plot:
    input: NGS1000/coverage/NGS1000_depth.txt
    output: NGS1000/coverage/NGS1000_coverage_plot.png
    jobid: 138
    wildcards: sn=NGS1000

/home/maria/covid_analysis_pavlos/covid-19-signal/scripts/generate_coverage_plot.py NGS1000/coverage/NGS1000_depth.txt NGS1000/coverage/NGS1000_coverage_plot.png
Activating conda environment: /home/maria/SNAKE_COVID/conda/4bc6b9de
[Thu Jan 28 20:22:37 2021]
Finished job 70.
51 of 164 steps (31%) done
Select jobs to execute...

[Thu Jan 28 20:22:37 2021]
rule run_fastqc_on_mapped_reads:
    input: NGS1000/mapped_clean_reads/NGS1000_R1.fastq.gz, NGS1000/mapped_clean_reads/NGS1000_R2.fastq.gz
    output: NGS1000/mapped_clean_reads/NGS1000_R1_fastqc.html, NGS1000/mapped_clean_reads/NGS1000_R2_fastqc.html
    log: NGS1000/mapped_clean_reads/NGS1000_fastqc.log
    jobid: 69
    benchmark: NGS1000/benchmarks/NGS1000_clean_fastqc.benchmark.tsv
    wildcards: sn=NGS1000


        fastqc -o NGS1000/mapped_clean_reads NGS1000/mapped_clean_reads/NGS1000_R1.fastq.gz NGS1000/mapped_clean_reads/NGS1000_R2.fastq.gz 2> NGS1000/mapped_clean_reads/NGS1000_fastqc.log
        
Activating conda environment: /home/maria/SNAKE_COVID/conda/b95377fd
[Thu Jan 28 20:22:42 2021]
Finished job 138.
52 of 164 steps (32%) done
Select jobs to execute...

[Thu Jan 28 20:22:42 2021]
rule run_ivar_variants:
    input: /home/maria/covid_analysis_pavlos/covid-19-signal/data/MN908947.3.fasta, /home/maria/covid_analysis_pavlos/covid-19-signal/data/MN908947.3.fasta.fai, NGS1000/core/NGS1000_viral_reference.mapping.primertrimmed.sorted.bam, /home/maria/covid_analysis_pavlos/covid-19-signal/data/MN908947.3.gff3
    output: NGS1000/core/NGS1000_ivar_variants.tsv
    log: NGS1000/core/NGS1000_ivar_variants.log
    jobid: 120
    benchmark: NGS1000/benchmarks/NGS1000_ivar_variants.benchmark.tsv
    wildcards: sn=NGS1000

(samtools mpileup -aa -A -d 0 --reference /home/maria/covid_analysis_pavlos/covid-19-signal/data/MN908947.3.fasta -B -Q 0 NGS1000/core/NGS1000_viral_reference.mapping.primertrimmed.sorted.bam | ivar variants -r /home/maria/covid_analysis_pavlos/covid-19-signal/data/MN908947.3.fasta -m 10 -p NGS1000/core/NGS1000_ivar_variants -q 20 -t 0.25 -g /home/maria/covid_analysis_pavlos/covid-19-signal/data/MN908947.3.gff3) 2> NGS1000/core/NGS1000_ivar_variants.log
Activating conda environment: /home/maria/SNAKE_COVID/conda/5258de7f
[Thu Jan 28 20:22:54 2021]
Finished job 69.
53 of 164 steps (32%) done
Select jobs to execute...
Failed to solve scheduling problem with ILP solver. Falling back to greedy solver.Run Snakemake with --verbose to see the full solver output for debugging the problem.
[Thu Jan 28 20:23:03 2021]
Finished job 120.
54 of 164 steps (33%) done
Select jobs to execute...
Failed to solve scheduling problem with ILP solver. Falling back to greedy solver.Run Snakemake with --verbose to see the full solver output for debugging the problem.
[Thu Jan 28 20:23:18 2021]
Finished job 35.
55 of 164 steps (34%) done
Select jobs to execute...

[Thu Jan 28 20:23:18 2021]
rule run_trimgalore:
    input: NGS1045/host_removal/NGS1045_R1.fastq.gz, NGS1045/host_removal/NGS1045_R2.fastq.gz
    output: NGS1045/adapter_trimmed/NGS1045_R1_val_1.fq.gz, NGS1045/adapter_trimmed/NGS1045_R2_val_2.fq.gz, NGS1045/adapter_trimmed/NGS1045_R1_val_1_fastqc.html, NGS1045/adapter_trimmed/NGS1045_R2_val_2_fastqc.html
    log: NGS1045/adapter_trimmed/NGS1045_trim_galore.log
    jobid: 45
    benchmark: NGS1045/benchmarks/NGS1045_trimgalore.benchmark.tsv
    wildcards: sn=NGS1045
    priority: 2
    threads: 2

trim_galore --quality 20 --length 20  -o NGS1045/adapter_trimmed --cores 2 --fastqc --paired NGS1045/host_removal/NGS1045_R1.fastq.gz NGS1045/host_removal/NGS1045_R2.fastq.gz 2> NGS1045/adapter_trimmed/NGS1045_trim_galore.log
Activating conda environment: /home/maria/SNAKE_COVID/conda/b95377fd
[Thu Jan 28 20:25:19 2021]
Finished job 33.
56 of 164 steps (34%) done
Select jobs to execute...

[Thu Jan 28 20:25:19 2021]
rule run_trimgalore:
    input: NGS1044/host_removal/NGS1044_R1.fastq.gz, NGS1044/host_removal/NGS1044_R2.fastq.gz
    output: NGS1044/adapter_trimmed/NGS1044_R1_val_1.fq.gz, NGS1044/adapter_trimmed/NGS1044_R2_val_2.fq.gz, NGS1044/adapter_trimmed/NGS1044_R1_val_1_fastqc.html, NGS1044/adapter_trimmed/NGS1044_R2_val_2_fastqc.html
    log: NGS1044/adapter_trimmed/NGS1044_trim_galore.log
    jobid: 44
    benchmark: NGS1044/benchmarks/NGS1044_trimgalore.benchmark.tsv
    wildcards: sn=NGS1044
    priority: 2
    threads: 2

trim_galore --quality 20 --length 20  -o NGS1044/adapter_trimmed --cores 2 --fastqc --paired NGS1044/host_removal/NGS1044_R1.fastq.gz NGS1044/host_removal/NGS1044_R2.fastq.gz 2> NGS1044/adapter_trimmed/NGS1044_trim_galore.log
Activating conda environment: /home/maria/SNAKE_COVID/conda/b95377fd
[Thu Jan 28 20:30:39 2021]
Finished job 44.
57 of 164 steps (35%) done
Select jobs to execute...

[Thu Jan 28 20:30:39 2021]
rule run_filtering_of_residual_adapters:
    input: NGS1044/adapter_trimmed/NGS1044_R1_val_1.fq.gz, NGS1044/adapter_trimmed/NGS1044_R2_val_2.fq.gz
    output: NGS1044/adapter_trimmed/NGS1044_R1_val_1_posttrim_filter.fq.gz, NGS1044/adapter_trimmed/NGS1044_R2_val_2_posttrim_filter.fq.gz
    jobid: 53
    wildcards: sn=NGS1044
    priority: 2
    threads: 2


	python3.6 /home/maria/covid_analysis_pavlos/covid-19-signal/scripts/filter_residual_adapters.py --input_R1 NGS1044/adapter_trimmed/NGS1044_R1_val_1.fq.gz --input_R2 NGS1044/adapter_trimmed/NGS1044_R2_val_2.fq.gz
	
Activating conda environment: /home/maria/SNAKE_COVID/conda/3850436d
[Thu Jan 28 20:31:03 2021]
Finished job 25.
58 of 164 steps (35%) done
Select jobs to execute...

[Thu Jan 28 20:31:03 2021]
rule run_trimgalore:
    input: NGS1040/host_removal/NGS1040_R1.fastq.gz, NGS1040/host_removal/NGS1040_R2.fastq.gz
    output: NGS1040/adapter_trimmed/NGS1040_R1_val_1.fq.gz, NGS1040/adapter_trimmed/NGS1040_R2_val_2.fq.gz, NGS1040/adapter_trimmed/NGS1040_R1_val_1_fastqc.html, NGS1040/adapter_trimmed/NGS1040_R2_val_2_fastqc.html
    log: NGS1040/adapter_trimmed/NGS1040_trim_galore.log
    jobid: 40
    benchmark: NGS1040/benchmarks/NGS1040_trimgalore.benchmark.tsv
    wildcards: sn=NGS1040
    priority: 2
    threads: 2

trim_galore --quality 20 --length 20  -o NGS1040/adapter_trimmed --cores 2 --fastqc --paired NGS1040/host_removal/NGS1040_R1.fastq.gz NGS1040/host_removal/NGS1040_R2.fastq.gz 2> NGS1040/adapter_trimmed/NGS1040_trim_galore.log
Activating conda environment: /home/maria/SNAKE_COVID/conda/b95377fd
[Thu Jan 28 20:32:44 2021]
Finished job 45.
59 of 164 steps (36%) done
Select jobs to execute...

[Thu Jan 28 20:32:44 2021]
rule run_filtering_of_residual_adapters:
    input: NGS1045/adapter_trimmed/NGS1045_R1_val_1.fq.gz, NGS1045/adapter_trimmed/NGS1045_R2_val_2.fq.gz
    output: NGS1045/adapter_trimmed/NGS1045_R1_val_1_posttrim_filter.fq.gz, NGS1045/adapter_trimmed/NGS1045_R2_val_2_posttrim_filter.fq.gz
    jobid: 54
    wildcards: sn=NGS1045
    priority: 2
    threads: 2


	python3.6 /home/maria/covid_analysis_pavlos/covid-19-signal/scripts/filter_residual_adapters.py --input_R1 NGS1045/adapter_trimmed/NGS1045_R1_val_1.fq.gz --input_R2 NGS1045/adapter_trimmed/NGS1045_R2_val_2.fq.gz
	
Activating conda environment: /home/maria/SNAKE_COVID/conda/3850436d
[Thu Jan 28 20:40:49 2021]
Finished job 40.
60 of 164 steps (37%) done
Select jobs to execute...

[Thu Jan 28 20:40:49 2021]
rule run_filtering_of_residual_adapters:
    input: NGS1040/adapter_trimmed/NGS1040_R1_val_1.fq.gz, NGS1040/adapter_trimmed/NGS1040_R2_val_2.fq.gz
    output: NGS1040/adapter_trimmed/NGS1040_R1_val_1_posttrim_filter.fq.gz, NGS1040/adapter_trimmed/NGS1040_R2_val_2_posttrim_filter.fq.gz
    jobid: 49
    wildcards: sn=NGS1040
    priority: 2
    threads: 2


	python3.6 /home/maria/covid_analysis_pavlos/covid-19-signal/scripts/filter_residual_adapters.py --input_R1 NGS1040/adapter_trimmed/NGS1040_R1_val_1.fq.gz --input_R2 NGS1040/adapter_trimmed/NGS1040_R2_val_2.fq.gz
	
Activating conda environment: /home/maria/SNAKE_COVID/conda/3850436d
[Thu Jan 28 20:51:23 2021]
Finished job 53.
61 of 164 steps (37%) done
Select jobs to execute...

[Thu Jan 28 20:51:23 2021]
rule raw_reads_composite_reference_bwa_map:
    input: NGS1001/raw_fastq/NGS1001_R1.fastq.gz, NGS1001/raw_fastq/NGS1001_R2.fastq.gz
    output: NGS1001/host_removal/NGS1001_viral_and_nonmapping_reads.bam
    log: NGS1001/host_removal/NGS1001_human_read_mapping.log
    jobid: 24
    benchmark: NGS1001/benchmarks/NGS1001_composite_reference_bwa_map.benchmark.tsv
    wildcards: sn=NGS1001
    threads: 4

(conda info --envs; bwa mem -t 4 /home/maria/covid_analysis_pavlos/covid-19-signal/data/composite_human_viral_reference.fna NGS1001/raw_fastq/NGS1001_R1.fastq.gz NGS1001/raw_fastq/NGS1001_R2.fastq.gz | /home/maria/covid_analysis_pavlos/covid-19-signal/scripts/filter_non_human_reads.py -c MN908947.3 > NGS1001/host_removal/NGS1001_viral_and_nonmapping_reads.bam) 2> NGS1001/host_removal/NGS1001_human_read_mapping.log
Activating conda environment: /home/maria/SNAKE_COVID/conda/3850436d
[Thu Jan 28 20:54:32 2021]
Finished job 24.
62 of 164 steps (38%) done
Select jobs to execute...

[Thu Jan 28 20:54:32 2021]
rule raw_reads_composite_reference_bwa_map:
    input: NGS1041/raw_fastq/NGS1041_R1.fastq.gz, NGS1041/raw_fastq/NGS1041_R2.fastq.gz
    output: NGS1041/host_removal/NGS1041_viral_and_nonmapping_reads.bam
    log: NGS1041/host_removal/NGS1041_human_read_mapping.log
    jobid: 28
    benchmark: NGS1041/benchmarks/NGS1041_composite_reference_bwa_map.benchmark.tsv
    wildcards: sn=NGS1041
    threads: 4

(conda info --envs; bwa mem -t 4 /home/maria/covid_analysis_pavlos/covid-19-signal/data/composite_human_viral_reference.fna NGS1041/raw_fastq/NGS1041_R1.fastq.gz NGS1041/raw_fastq/NGS1041_R2.fastq.gz | /home/maria/covid_analysis_pavlos/covid-19-signal/scripts/filter_non_human_reads.py -c MN908947.3 > NGS1041/host_removal/NGS1041_viral_and_nonmapping_reads.bam) 2> NGS1041/host_removal/NGS1041_human_read_mapping.log
Activating conda environment: /home/maria/SNAKE_COVID/conda/3850436d
[Thu Jan 28 21:04:59 2021]
Finished job 28.
63 of 164 steps (38%) done
Select jobs to execute...

[Thu Jan 28 21:04:59 2021]
rule viral_reference_bwa_map:
    input: NGS1044/adapter_trimmed/NGS1044_R1_val_1_posttrim_filter.fq.gz, NGS1044/adapter_trimmed/NGS1044_R2_val_2_posttrim_filter.fq.gz, NGS1044/core/viral_reference.bwt
    output: NGS1044/core/NGS1044_viral_reference.bam
    log: NGS1044/core/NGS1044_viral_reference_bwa.log
    jobid: 102
    benchmark: NGS1044/benchmarks/NGS1044_viral_reference_bwa_map.benchmark.tsv
    wildcards: sn=NGS1044
    threads: 2

(bwa mem -t 2 NGS1044/core/viral_reference NGS1044/adapter_trimmed/NGS1044_R1_val_1_posttrim_filter.fq.gz NGS1044/adapter_trimmed/NGS1044_R2_val_2_posttrim_filter.fq.gz | samtools view -bS | samtools sort -@2 -o NGS1044/core/NGS1044_viral_reference.bam) 2> NGS1044/core/NGS1044_viral_reference_bwa.log

[Thu Jan 28 21:04:59 2021]
rule get_host_removed_reads:
    input: NGS1001/host_removal/NGS1001_viral_and_nonmapping_reads.bam
    output: NGS1001/host_removal/NGS1001_R1.fastq.gz, NGS1001/host_removal/NGS1001_R2.fastq.gz, NGS1001/host_removal/NGS1001_singletons.fastq.gz, NGS1001/host_removal/NGS1001_viral_and_nonmapping_reads_filtered_sorted.bam
    log: NGS1001/host_removal/NGS1001_samtools_fastq.log
    jobid: 23
    benchmark: NGS1001/benchmarks/NGS1001_get_host_removed_reads.benchmark.tsv
    wildcards: sn=NGS1001
    threads: 2


        samtools view -b NGS1001/host_removal/NGS1001_viral_and_nonmapping_reads.bam | samtools sort -n -@2 > NGS1001/host_removal/NGS1001_viral_and_nonmapping_reads_filtered_sorted.bam 2> NGS1001/host_removal/NGS1001_samtools_fastq.log
        samtools fastq -1 NGS1001/host_removal/NGS1001_R1.fastq.gz -2 NGS1001/host_removal/NGS1001_R2.fastq.gz -s NGS1001/host_removal/NGS1001_singletons.fastq.gz NGS1001/host_removal/NGS1001_viral_and_nonmapping_reads_filtered_sorted.bam 2>> NGS1001/host_removal/NGS1001_samtools_fastq.log 
        
Activating conda environment: /home/maria/SNAKE_COVID/conda/3850436d
Activating conda environment: /home/maria/SNAKE_COVID/conda/3850436d
[Thu Jan 28 21:05:51 2021]
Finished job 23.
64 of 164 steps (39%) done
Select jobs to execute...

[Thu Jan 28 21:05:51 2021]
rule run_trimgalore:
    input: NGS1001/host_removal/NGS1001_R1.fastq.gz, NGS1001/host_removal/NGS1001_R2.fastq.gz
    output: NGS1001/adapter_trimmed/NGS1001_R1_val_1.fq.gz, NGS1001/adapter_trimmed/NGS1001_R2_val_2.fq.gz, NGS1001/adapter_trimmed/NGS1001_R1_val_1_fastqc.html, NGS1001/adapter_trimmed/NGS1001_R2_val_2_fastqc.html
    log: NGS1001/adapter_trimmed/NGS1001_trim_galore.log
    jobid: 39
    benchmark: NGS1001/benchmarks/NGS1001_trimgalore.benchmark.tsv
    wildcards: sn=NGS1001
    priority: 2
    threads: 2

trim_galore --quality 20 --length 20  -o NGS1001/adapter_trimmed --cores 2 --fastqc --paired NGS1001/host_removal/NGS1001_R1.fastq.gz NGS1001/host_removal/NGS1001_R2.fastq.gz 2> NGS1001/adapter_trimmed/NGS1001_trim_galore.log
Activating conda environment: /home/maria/SNAKE_COVID/conda/b95377fd
[Thu Jan 28 21:06:43 2021]
Finished job 39.
65 of 164 steps (40%) done
Select jobs to execute...

[Thu Jan 28 21:06:43 2021]
rule run_filtering_of_residual_adapters:
    input: NGS1001/adapter_trimmed/NGS1001_R1_val_1.fq.gz, NGS1001/adapter_trimmed/NGS1001_R2_val_2.fq.gz
    output: NGS1001/adapter_trimmed/NGS1001_R1_val_1_posttrim_filter.fq.gz, NGS1001/adapter_trimmed/NGS1001_R2_val_2_posttrim_filter.fq.gz
    jobid: 48
    wildcards: sn=NGS1001
    priority: 2
    threads: 2


	python3.6 /home/maria/covid_analysis_pavlos/covid-19-signal/scripts/filter_residual_adapters.py --input_R1 NGS1001/adapter_trimmed/NGS1001_R1_val_1.fq.gz --input_R2 NGS1001/adapter_trimmed/NGS1001_R2_val_2.fq.gz
	
Activating conda environment: /home/maria/SNAKE_COVID/conda/3850436d
[Thu Jan 28 21:09:11 2021]
Finished job 102.
66 of 164 steps (40%) done
Select jobs to execute...

[Thu Jan 28 21:09:11 2021]
rule get_host_removed_reads:
    input: NGS1041/host_removal/NGS1041_viral_and_nonmapping_reads.bam
    output: NGS1041/host_removal/NGS1041_R1.fastq.gz, NGS1041/host_removal/NGS1041_R2.fastq.gz, NGS1041/host_removal/NGS1041_singletons.fastq.gz, NGS1041/host_removal/NGS1041_viral_and_nonmapping_reads_filtered_sorted.bam
    log: NGS1041/host_removal/NGS1041_samtools_fastq.log
    jobid: 27
    benchmark: NGS1041/benchmarks/NGS1041_get_host_removed_reads.benchmark.tsv
    wildcards: sn=NGS1041
    threads: 2


        samtools view -b NGS1041/host_removal/NGS1041_viral_and_nonmapping_reads.bam | samtools sort -n -@2 > NGS1041/host_removal/NGS1041_viral_and_nonmapping_reads_filtered_sorted.bam 2> NGS1041/host_removal/NGS1041_samtools_fastq.log
        samtools fastq -1 NGS1041/host_removal/NGS1041_R1.fastq.gz -2 NGS1041/host_removal/NGS1041_R2.fastq.gz -s NGS1041/host_removal/NGS1041_singletons.fastq.gz NGS1041/host_removal/NGS1041_viral_and_nonmapping_reads_filtered_sorted.bam 2>> NGS1041/host_removal/NGS1041_samtools_fastq.log 
        
Activating conda environment: /home/maria/SNAKE_COVID/conda/3850436d
[Thu Jan 28 21:09:45 2021]
Finished job 48.
67 of 164 steps (41%) done
Select jobs to execute...

[Thu Jan 28 21:09:45 2021]
rule run_kraken2:
    input: NGS1001/adapter_trimmed/NGS1001_R1_val_1_posttrim_filter.fq.gz, NGS1001/adapter_trimmed/NGS1001_R2_val_2_posttrim_filter.fq.gz
    output: NGS1001/kraken2/NGS1001_kraken2.out
    log: NGS1001/kraken2/NGS1001_kraken2.log
    jobid: 148
    benchmark: NGS1001/benchmarks/NGS1001_run_kraken2.benchmark.tsv
    wildcards: sn=NGS1001

cd NGS1001/kraken2 && kraken2 --db /home/maria/covid_analysis_pavlos/covid-19-signal/data/Kraken2/db --threads 1 --quick --unclassified-out "NGS1001_kraken2_unclassified_reads#" --classified-out "NGS1001_kraken2_classified_reads#" --output NGS1001_kraken2.out --paired --gzip-compressed ../../NGS1001/adapter_trimmed/NGS1001_R1_val_1_posttrim_filter.fq.gz ../../NGS1001/adapter_trimmed/NGS1001_R2_val_2_posttrim_filter.fq.gz --report NGS1001_kraken2.report 2>../../NGS1001/kraken2/NGS1001_kraken2.log

[Thu Jan 28 21:09:45 2021]
rule run_kraken2:
    input: NGS1044/adapter_trimmed/NGS1044_R1_val_1_posttrim_filter.fq.gz, NGS1044/adapter_trimmed/NGS1044_R2_val_2_posttrim_filter.fq.gz
    output: NGS1044/kraken2/NGS1044_kraken2.out
    log: NGS1044/kraken2/NGS1044_kraken2.log
    jobid: 153
    benchmark: NGS1044/benchmarks/NGS1044_run_kraken2.benchmark.tsv
    wildcards: sn=NGS1044

cd NGS1044/kraken2 && kraken2 --db /home/maria/covid_analysis_pavlos/covid-19-signal/data/Kraken2/db --threads 1 --quick --unclassified-out "NGS1044_kraken2_unclassified_reads#" --classified-out "NGS1044_kraken2_classified_reads#" --output NGS1044_kraken2.out --paired --gzip-compressed ../../NGS1044/adapter_trimmed/NGS1044_R1_val_1_posttrim_filter.fq.gz ../../NGS1044/adapter_trimmed/NGS1044_R2_val_2_posttrim_filter.fq.gz --report NGS1044_kraken2.report 2>../../NGS1044/kraken2/NGS1044_kraken2.log
Activating conda environment: /home/maria/SNAKE_COVID/conda/b95377fd
Activating conda environment: /home/maria/SNAKE_COVID/conda/b95377fd
[Thu Jan 28 21:10:06 2021]
Finished job 148.
68 of 164 steps (41%) done
Select jobs to execute...

[Thu Jan 28 21:10:06 2021]
rule run_bed_primer_trim:
    input: NGS1044/core/NGS1044_viral_reference.bam
    output: NGS1044/core/NGS1044_viral_reference.mapping.primertrimmed.sorted.bam, NGS1044/core/NGS1044_viral_reference.mapping.primertrimmed.bam, NGS1044/core/NGS1044_viral_reference.mapping.bam
    log: NGS1044/core/NGS1044_ivar_trim.log
    jobid: 101
    benchmark: NGS1044/benchmarks/NGS1044_bed_primer_trim.benchmark.tsv
    wildcards: sn=NGS1044

samtools view -F4 -o NGS1044/core/NGS1044_viral_reference.mapping.bam NGS1044/core/NGS1044_viral_reference.bam; samtools index NGS1044/core/NGS1044_viral_reference.mapping.bam; ivar trim -e -i NGS1044/core/NGS1044_viral_reference.mapping.bam -b /home/maria/covid_analysis_pavlos/covid-19-signal/resources/SARSCoV2.paragon.bed -m 20 -q 20 -p NGS1044/core/NGS1044_viral_reference.mapping.primertrimmed 2> NGS1044/core/NGS1044_ivar_trim.log; samtools sort -o NGS1044/core/NGS1044_viral_reference.mapping.primertrimmed.sorted.bam NGS1044/core/NGS1044_viral_reference.mapping.primertrimmed.bam
Activating conda environment: /home/maria/SNAKE_COVID/conda/5258de7f
[Thu Jan 28 21:11:07 2021]
Finished job 27.
69 of 164 steps (42%) done
Select jobs to execute...

[Thu Jan 28 21:11:07 2021]
rule run_trimgalore:
    input: NGS1041/host_removal/NGS1041_R1.fastq.gz, NGS1041/host_removal/NGS1041_R2.fastq.gz
    output: NGS1041/adapter_trimmed/NGS1041_R1_val_1.fq.gz, NGS1041/adapter_trimmed/NGS1041_R2_val_2.fq.gz, NGS1041/adapter_trimmed/NGS1041_R1_val_1_fastqc.html, NGS1041/adapter_trimmed/NGS1041_R2_val_2_fastqc.html
    log: NGS1041/adapter_trimmed/NGS1041_trim_galore.log
    jobid: 41
    benchmark: NGS1041/benchmarks/NGS1041_trimgalore.benchmark.tsv
    wildcards: sn=NGS1041
    priority: 2
    threads: 2

trim_galore --quality 20 --length 20  -o NGS1041/adapter_trimmed --cores 2 --fastqc --paired NGS1041/host_removal/NGS1041_R1.fastq.gz NGS1041/host_removal/NGS1041_R2.fastq.gz 2> NGS1041/adapter_trimmed/NGS1041_trim_galore.log
Activating conda environment: /home/maria/SNAKE_COVID/conda/b95377fd
[Thu Jan 28 21:11:52 2021]
Finished job 153.
70 of 164 steps (43%) done
Select jobs to execute...
Failed to solve scheduling problem with ILP solver. Falling back to greedy solver.Run Snakemake with --verbose to see the full solver output for debugging the problem.
[Thu Jan 28 21:12:25 2021]
Finished job 41.
71 of 164 steps (43%) done
Select jobs to execute...

[Thu Jan 28 21:12:25 2021]
rule run_filtering_of_residual_adapters:
    input: NGS1041/adapter_trimmed/NGS1041_R1_val_1.fq.gz, NGS1041/adapter_trimmed/NGS1041_R2_val_2.fq.gz
    output: NGS1041/adapter_trimmed/NGS1041_R1_val_1_posttrim_filter.fq.gz, NGS1041/adapter_trimmed/NGS1041_R2_val_2_posttrim_filter.fq.gz
    jobid: 50
    wildcards: sn=NGS1041
    priority: 2
    threads: 2


	python3.6 /home/maria/covid_analysis_pavlos/covid-19-signal/scripts/filter_residual_adapters.py --input_R1 NGS1041/adapter_trimmed/NGS1041_R1_val_1.fq.gz --input_R2 NGS1041/adapter_trimmed/NGS1041_R2_val_2.fq.gz
	
Activating conda environment: /home/maria/SNAKE_COVID/conda/3850436d
[Thu Jan 28 21:14:10 2021]
Finished job 54.
72 of 164 steps (44%) done
Select jobs to execute...

[Thu Jan 28 21:14:10 2021]
rule viral_reference_bwa_map:
    input: NGS1001/adapter_trimmed/NGS1001_R1_val_1_posttrim_filter.fq.gz, NGS1001/adapter_trimmed/NGS1001_R2_val_2_posttrim_filter.fq.gz, NGS1001/core/viral_reference.bwt
    output: NGS1001/core/NGS1001_viral_reference.bam
    log: NGS1001/core/NGS1001_viral_reference_bwa.log
    jobid: 77
    benchmark: NGS1001/benchmarks/NGS1001_viral_reference_bwa_map.benchmark.tsv
    wildcards: sn=NGS1001
    threads: 2

(bwa mem -t 2 NGS1001/core/viral_reference NGS1001/adapter_trimmed/NGS1001_R1_val_1_posttrim_filter.fq.gz NGS1001/adapter_trimmed/NGS1001_R2_val_2_posttrim_filter.fq.gz | samtools view -bS | samtools sort -@2 -o NGS1001/core/NGS1001_viral_reference.bam) 2> NGS1001/core/NGS1001_viral_reference_bwa.log

[Thu Jan 28 21:14:10 2021]
rule run_kraken2:
    input: NGS1045/adapter_trimmed/NGS1045_R1_val_1_posttrim_filter.fq.gz, NGS1045/adapter_trimmed/NGS1045_R2_val_2_posttrim_filter.fq.gz
    output: NGS1045/kraken2/NGS1045_kraken2.out
    log: NGS1045/kraken2/NGS1045_kraken2.log
    jobid: 154
    benchmark: NGS1045/benchmarks/NGS1045_run_kraken2.benchmark.tsv
    wildcards: sn=NGS1045

cd NGS1045/kraken2 && kraken2 --db /home/maria/covid_analysis_pavlos/covid-19-signal/data/Kraken2/db --threads 1 --quick --unclassified-out "NGS1045_kraken2_unclassified_reads#" --classified-out "NGS1045_kraken2_classified_reads#" --output NGS1045_kraken2.out --paired --gzip-compressed ../../NGS1045/adapter_trimmed/NGS1045_R1_val_1_posttrim_filter.fq.gz ../../NGS1045/adapter_trimmed/NGS1045_R2_val_2_posttrim_filter.fq.gz --report NGS1045_kraken2.report 2>../../NGS1045/kraken2/NGS1045_kraken2.log
Activating conda environment: /home/maria/SNAKE_COVID/conda/b95377fd
Activating conda environment: /home/maria/SNAKE_COVID/conda/3850436d
[Thu Jan 28 21:14:48 2021]
Finished job 77.
73 of 164 steps (45%) done
Select jobs to execute...

[Thu Jan 28 21:14:48 2021]
rule viral_reference_bwa_map:
    input: NGS1045/adapter_trimmed/NGS1045_R1_val_1_posttrim_filter.fq.gz, NGS1045/adapter_trimmed/NGS1045_R2_val_2_posttrim_filter.fq.gz, NGS1045/core/viral_reference.bwt
    output: NGS1045/core/NGS1045_viral_reference.bam
    log: NGS1045/core/NGS1045_viral_reference_bwa.log
    jobid: 107
    benchmark: NGS1045/benchmarks/NGS1045_viral_reference_bwa_map.benchmark.tsv
    wildcards: sn=NGS1045
    threads: 2

(bwa mem -t 2 NGS1045/core/viral_reference NGS1045/adapter_trimmed/NGS1045_R1_val_1_posttrim_filter.fq.gz NGS1045/adapter_trimmed/NGS1045_R2_val_2_posttrim_filter.fq.gz | samtools view -bS | samtools sort -@2 -o NGS1045/core/NGS1045_viral_reference.bam) 2> NGS1045/core/NGS1045_viral_reference_bwa.log
Activating conda environment: /home/maria/SNAKE_COVID/conda/3850436d
[Thu Jan 28 21:17:44 2021]
Finished job 50.
74 of 164 steps (45%) done
Select jobs to execute...

[Thu Jan 28 21:17:44 2021]
rule run_bed_primer_trim:
    input: NGS1001/core/NGS1001_viral_reference.bam
    output: NGS1001/core/NGS1001_viral_reference.mapping.primertrimmed.sorted.bam, NGS1001/core/NGS1001_viral_reference.mapping.primertrimmed.bam, NGS1001/core/NGS1001_viral_reference.mapping.bam
    log: NGS1001/core/NGS1001_ivar_trim.log
    jobid: 76
    benchmark: NGS1001/benchmarks/NGS1001_bed_primer_trim.benchmark.tsv
    wildcards: sn=NGS1001

samtools view -F4 -o NGS1001/core/NGS1001_viral_reference.mapping.bam NGS1001/core/NGS1001_viral_reference.bam; samtools index NGS1001/core/NGS1001_viral_reference.mapping.bam; ivar trim -e -i NGS1001/core/NGS1001_viral_reference.mapping.bam -b /home/maria/covid_analysis_pavlos/covid-19-signal/resources/SARSCoV2.paragon.bed -m 20 -q 20 -p NGS1001/core/NGS1001_viral_reference.mapping.primertrimmed 2> NGS1001/core/NGS1001_ivar_trim.log; samtools sort -o NGS1001/core/NGS1001_viral_reference.mapping.primertrimmed.sorted.bam NGS1001/core/NGS1001_viral_reference.mapping.primertrimmed.bam

[Thu Jan 28 21:17:44 2021]
rule run_kraken2:
    input: NGS1041/adapter_trimmed/NGS1041_R1_val_1_posttrim_filter.fq.gz, NGS1041/adapter_trimmed/NGS1041_R2_val_2_posttrim_filter.fq.gz
    output: NGS1041/kraken2/NGS1041_kraken2.out
    log: NGS1041/kraken2/NGS1041_kraken2.log
    jobid: 150
    benchmark: NGS1041/benchmarks/NGS1041_run_kraken2.benchmark.tsv
    wildcards: sn=NGS1041

cd NGS1041/kraken2 && kraken2 --db /home/maria/covid_analysis_pavlos/covid-19-signal/data/Kraken2/db --threads 1 --quick --unclassified-out "NGS1041_kraken2_unclassified_reads#" --classified-out "NGS1041_kraken2_classified_reads#" --output NGS1041_kraken2.out --paired --gzip-compressed ../../NGS1041/adapter_trimmed/NGS1041_R1_val_1_posttrim_filter.fq.gz ../../NGS1041/adapter_trimmed/NGS1041_R2_val_2_posttrim_filter.fq.gz --report NGS1041_kraken2.report 2>../../NGS1041/kraken2/NGS1041_kraken2.log
Activating conda environment: /home/maria/SNAKE_COVID/conda/5258de7f
Activating conda environment: /home/maria/SNAKE_COVID/conda/b95377fd
[Thu Jan 28 21:18:20 2021]
Finished job 154.
75 of 164 steps (46%) done
Select jobs to execute...
Failed to solve scheduling problem with ILP solver. Falling back to greedy solver.Run Snakemake with --verbose to see the full solver output for debugging the problem.
[Thu Jan 28 21:18:21 2021]
Finished job 150.
76 of 164 steps (46%) done
Select jobs to execute...

[Thu Jan 28 21:18:21 2021]
rule viral_reference_bwa_map:
    input: NGS1041/adapter_trimmed/NGS1041_R1_val_1_posttrim_filter.fq.gz, NGS1041/adapter_trimmed/NGS1041_R2_val_2_posttrim_filter.fq.gz, NGS1041/core/viral_reference.bwt
    output: NGS1041/core/NGS1041_viral_reference.bam
    log: NGS1041/core/NGS1041_viral_reference_bwa.log
    jobid: 87
    benchmark: NGS1041/benchmarks/NGS1041_viral_reference_bwa_map.benchmark.tsv
    wildcards: sn=NGS1041
    threads: 2

(bwa mem -t 2 NGS1041/core/viral_reference NGS1041/adapter_trimmed/NGS1041_R1_val_1_posttrim_filter.fq.gz NGS1041/adapter_trimmed/NGS1041_R2_val_2_posttrim_filter.fq.gz | samtools view -bS | samtools sort -@2 -o NGS1041/core/NGS1041_viral_reference.bam) 2> NGS1041/core/NGS1041_viral_reference_bwa.log
Activating conda environment: /home/maria/SNAKE_COVID/conda/3850436d
[Thu Jan 28 21:19:34 2021]
Finished job 87.
77 of 164 steps (47%) done
Select jobs to execute...

[Thu Jan 28 21:19:34 2021]
rule run_bed_primer_trim:
    input: NGS1041/core/NGS1041_viral_reference.bam
    output: NGS1041/core/NGS1041_viral_reference.mapping.primertrimmed.sorted.bam, NGS1041/core/NGS1041_viral_reference.mapping.primertrimmed.bam, NGS1041/core/NGS1041_viral_reference.mapping.bam
    log: NGS1041/core/NGS1041_ivar_trim.log
    jobid: 86
    benchmark: NGS1041/benchmarks/NGS1041_bed_primer_trim.benchmark.tsv
    wildcards: sn=NGS1041

samtools view -F4 -o NGS1041/core/NGS1041_viral_reference.mapping.bam NGS1041/core/NGS1041_viral_reference.bam; samtools index NGS1041/core/NGS1041_viral_reference.mapping.bam; ivar trim -e -i NGS1041/core/NGS1041_viral_reference.mapping.bam -b /home/maria/covid_analysis_pavlos/covid-19-signal/resources/SARSCoV2.paragon.bed -m 20 -q 20 -p NGS1041/core/NGS1041_viral_reference.mapping.primertrimmed 2> NGS1041/core/NGS1041_ivar_trim.log; samtools sort -o NGS1041/core/NGS1041_viral_reference.mapping.primertrimmed.sorted.bam NGS1041/core/NGS1041_viral_reference.mapping.primertrimmed.bam
Activating conda environment: /home/maria/SNAKE_COVID/conda/5258de7f
[Thu Jan 28 21:20:44 2021]
Finished job 76.
78 of 164 steps (48%) done
Select jobs to execute...

[Thu Jan 28 21:20:44 2021]
rule run_ivar_variants:
    input: /home/maria/covid_analysis_pavlos/covid-19-signal/data/MN908947.3.fasta, /home/maria/covid_analysis_pavlos/covid-19-signal/data/MN908947.3.fasta.fai, NGS1001/core/NGS1001_viral_reference.mapping.primertrimmed.sorted.bam, /home/maria/covid_analysis_pavlos/covid-19-signal/data/MN908947.3.gff3
    output: NGS1001/core/NGS1001_ivar_variants.tsv
    log: NGS1001/core/NGS1001_ivar_variants.log
    jobid: 121
    benchmark: NGS1001/benchmarks/NGS1001_ivar_variants.benchmark.tsv
    wildcards: sn=NGS1001

(samtools mpileup -aa -A -d 0 --reference /home/maria/covid_analysis_pavlos/covid-19-signal/data/MN908947.3.fasta -B -Q 0 NGS1001/core/NGS1001_viral_reference.mapping.primertrimmed.sorted.bam | ivar variants -r /home/maria/covid_analysis_pavlos/covid-19-signal/data/MN908947.3.fasta -m 10 -p NGS1001/core/NGS1001_ivar_variants -q 20 -t 0.25 -g /home/maria/covid_analysis_pavlos/covid-19-signal/data/MN908947.3.gff3) 2> NGS1001/core/NGS1001_ivar_variants.log

[Thu Jan 28 21:20:44 2021]
rule get_mapping_reads:
    input: NGS1001/core/NGS1001_viral_reference.mapping.primertrimmed.bam
    output: NGS1001/mapped_clean_reads/NGS1001_R1.fastq.gz, NGS1001/mapped_clean_reads/NGS1001_R2.fastq.gz, NGS1001/mapped_clean_reads/NGS1001_singletons.fastq.gz, NGS1001/mapped_clean_reads/NGS1001_sorted_clean.bam
    log: NGS1001/mapped_clean_reads/NGS1001_samtools_fastq.log
    jobid: 75
    benchmark: NGS1001/benchmarks/NGS1001_get_mapping_reads.benchmark.tsv
    wildcards: sn=NGS1001
    priority: 2


        samtools sort -n NGS1001/core/NGS1001_viral_reference.mapping.primertrimmed.bam -o NGS1001/mapped_clean_reads/NGS1001_sorted_clean.bam 2> NGS1001/mapped_clean_reads/NGS1001_samtools_fastq.log
        samtools fastq -1 NGS1001/mapped_clean_reads/NGS1001_R1.fastq.gz -2 NGS1001/mapped_clean_reads/NGS1001_R2.fastq.gz -s NGS1001/mapped_clean_reads/NGS1001_singletons.fastq.gz NGS1001/mapped_clean_reads/NGS1001_sorted_clean.bam 2>> NGS1001/mapped_clean_reads/NGS1001_samtools_fastq.log 
        
Activating conda environment: /home/maria/SNAKE_COVID/conda/5258de7f
Activating conda environment: /home/maria/SNAKE_COVID/conda/3850436d
[Thu Jan 28 21:21:03 2021]
Finished job 121.
79 of 164 steps (48%) done
Select jobs to execute...

[Thu Jan 28 21:21:03 2021]
rule run_ivar_consensus:
    input: NGS1001/core/NGS1001_viral_reference.mapping.primertrimmed.sorted.bam
    output: NGS1001/core/NGS1001.consensus.fa
    log: NGS1001/core/NGS1001_ivar_consensus.log
    jobid: 111
    benchmark: NGS1001/benchmarks/NGS1001_ivar_consensus.benchmark.tsv
    wildcards: sn=NGS1001

(samtools mpileup -aa -A -d 100000 -Q0 NGS1001/core/NGS1001_viral_reference.mapping.primertrimmed.sorted.bam | ivar consensus -t 0.75 -m 10 -n N -p NGS1001/core/NGS1001.consensus) 2>NGS1001/core/NGS1001_ivar_consensus.log
Activating conda environment: /home/maria/SNAKE_COVID/conda/5258de7f
[Thu Jan 28 21:21:20 2021]
Finished job 111.
80 of 164 steps (49%) done
Select jobs to execute...

[Thu Jan 28 21:21:20 2021]
rule run_quast:
    input: NGS1001/core/NGS1001.consensus.fa
    output: NGS1001/quast/NGS1001_quast_report.html
    log: NGS1001/quast/NGS1001_quast.log
    jobid: 157
    benchmark: NGS1001/benchmarks/NGS1001_run_quast.benchmark.tsv
    wildcards: sn=NGS1001

quast NGS1001/core/NGS1001.consensus.fa -r /home/maria/covid_analysis_pavlos/covid-19-signal/data/MN908947.3.fasta -g /home/maria/covid_analysis_pavlos/covid-19-signal/data/MN908947.3.gff3 --output-dir NGS1001/quast --threads 1 >NGS1001/quast/NGS1001_quast.log && for f in NGS1001/quast/report.*; do mv $f ${f/report/NGS1001_quast_report}; done
[Thu Jan 28 21:21:22 2021]
Finished job 75.
81 of 164 steps (49%) done
Select jobs to execute...

[Thu Jan 28 21:21:22 2021]
rule run_fastqc_on_mapped_reads:
    input: NGS1001/mapped_clean_reads/NGS1001_R1.fastq.gz, NGS1001/mapped_clean_reads/NGS1001_R2.fastq.gz
    output: NGS1001/mapped_clean_reads/NGS1001_R1_fastqc.html, NGS1001/mapped_clean_reads/NGS1001_R2_fastqc.html
    log: NGS1001/mapped_clean_reads/NGS1001_fastqc.log
    jobid: 74
    benchmark: NGS1001/benchmarks/NGS1001_clean_fastqc.benchmark.tsv
    wildcards: sn=NGS1001


        fastqc -o NGS1001/mapped_clean_reads NGS1001/mapped_clean_reads/NGS1001_R1.fastq.gz NGS1001/mapped_clean_reads/NGS1001_R2.fastq.gz 2> NGS1001/mapped_clean_reads/NGS1001_fastqc.log
        
Activating conda environment: /home/maria/SNAKE_COVID/conda/2d0610a0
Activating conda environment: /home/maria/SNAKE_COVID/conda/b95377fd
[Thu Jan 28 21:21:26 2021]
Finished job 157.
82 of 164 steps (50%) done
Select jobs to execute...

[Thu Jan 28 21:21:26 2021]
rule coverage_depth:
    input: NGS1001/core/NGS1001_viral_reference.mapping.primertrimmed.sorted.bam
    output: NGS1001/coverage/NGS1001_depth.txt
    jobid: 130
    benchmark: NGS1001/benchmarks/NGS1001_coverage_depth.benchmark.tsv
    wildcards: sn=NGS1001

bedtools genomecov -d -ibam NGS1001/core/NGS1001_viral_reference.mapping.primertrimmed.sorted.bam >NGS1001/coverage/NGS1001_depth.txt
Activating conda environment: /home/maria/SNAKE_COVID/conda/3850436d
[Thu Jan 28 21:21:36 2021]
Finished job 130.
83 of 164 steps (51%) done
Select jobs to execute...

[Thu Jan 28 21:21:36 2021]
rule generate_coverage_plot:
    input: NGS1001/coverage/NGS1001_depth.txt
    output: NGS1001/coverage/NGS1001_coverage_plot.png
    jobid: 139
    wildcards: sn=NGS1001

/home/maria/covid_analysis_pavlos/covid-19-signal/scripts/generate_coverage_plot.py NGS1001/coverage/NGS1001_depth.txt NGS1001/coverage/NGS1001_coverage_plot.png
Activating conda environment: /home/maria/SNAKE_COVID/conda/4bc6b9de
[Thu Jan 28 21:21:39 2021]
Error in rule generate_coverage_plot:
    jobid: 139
    output: NGS1001/coverage/NGS1001_coverage_plot.png
    conda-env: /home/maria/SNAKE_COVID/conda/4bc6b9de
    shell:
        /home/maria/covid_analysis_pavlos/covid-19-signal/scripts/generate_coverage_plot.py NGS1001/coverage/NGS1001_depth.txt NGS1001/coverage/NGS1001_coverage_plot.png
        (one of the commands exited with non-zero exit code; note that snakemake uses bash strict mode!)

Job failed, going on with independent jobs.
Select jobs to execute...
Failed to solve scheduling problem with ILP solver. Falling back to greedy solver.Run Snakemake with --verbose to see the full solver output for debugging the problem.
[Thu Jan 28 21:21:40 2021]
Finished job 74.
84 of 164 steps (51%) done
Select jobs to execute...
Failed to solve scheduling problem with ILP solver. Falling back to greedy solver.Run Snakemake with --verbose to see the full solver output for debugging the problem.
[Thu Jan 28 21:23:04 2021]
Finished job 107.
85 of 164 steps (52%) done
Select jobs to execute...

[Thu Jan 28 21:23:04 2021]
rule raw_reads_composite_reference_bwa_map:
    input: NGS1043/raw_fastq/NGS1043_R1.fastq.gz, NGS1043/raw_fastq/NGS1043_R2.fastq.gz
    output: NGS1043/host_removal/NGS1043_viral_and_nonmapping_reads.bam
    log: NGS1043/host_removal/NGS1043_human_read_mapping.log
    jobid: 32
    benchmark: NGS1043/benchmarks/NGS1043_composite_reference_bwa_map.benchmark.tsv
    wildcards: sn=NGS1043
    threads: 4

(conda info --envs; bwa mem -t 4 /home/maria/covid_analysis_pavlos/covid-19-signal/data/composite_human_viral_reference.fna NGS1043/raw_fastq/NGS1043_R1.fastq.gz NGS1043/raw_fastq/NGS1043_R2.fastq.gz | /home/maria/covid_analysis_pavlos/covid-19-signal/scripts/filter_non_human_reads.py -c MN908947.3 > NGS1043/host_removal/NGS1043_viral_and_nonmapping_reads.bam) 2> NGS1043/host_removal/NGS1043_human_read_mapping.log
Activating conda environment: /home/maria/SNAKE_COVID/conda/3850436d
[Thu Jan 28 21:24:30 2021]
Finished job 86.
86 of 164 steps (52%) done
Select jobs to execute...

[Thu Jan 28 21:24:30 2021]
rule get_mapping_reads:
    input: NGS1041/core/NGS1041_viral_reference.mapping.primertrimmed.bam
    output: NGS1041/mapped_clean_reads/NGS1041_R1.fastq.gz, NGS1041/mapped_clean_reads/NGS1041_R2.fastq.gz, NGS1041/mapped_clean_reads/NGS1041_singletons.fastq.gz, NGS1041/mapped_clean_reads/NGS1041_sorted_clean.bam
    log: NGS1041/mapped_clean_reads/NGS1041_samtools_fastq.log
    jobid: 85
    benchmark: NGS1041/benchmarks/NGS1041_get_mapping_reads.benchmark.tsv
    wildcards: sn=NGS1041
    priority: 2


        samtools sort -n NGS1041/core/NGS1041_viral_reference.mapping.primertrimmed.bam -o NGS1041/mapped_clean_reads/NGS1041_sorted_clean.bam 2> NGS1041/mapped_clean_reads/NGS1041_samtools_fastq.log
        samtools fastq -1 NGS1041/mapped_clean_reads/NGS1041_R1.fastq.gz -2 NGS1041/mapped_clean_reads/NGS1041_R2.fastq.gz -s NGS1041/mapped_clean_reads/NGS1041_singletons.fastq.gz NGS1041/mapped_clean_reads/NGS1041_sorted_clean.bam 2>> NGS1041/mapped_clean_reads/NGS1041_samtools_fastq.log 
        
Activating conda environment: /home/maria/SNAKE_COVID/conda/3850436d
[Thu Jan 28 21:25:23 2021]
Finished job 85.
87 of 164 steps (53%) done
Select jobs to execute...

[Thu Jan 28 21:25:23 2021]
rule coverage_depth:
    input: NGS1041/core/NGS1041_viral_reference.mapping.primertrimmed.sorted.bam
    output: NGS1041/coverage/NGS1041_depth.txt
    jobid: 132
    benchmark: NGS1041/benchmarks/NGS1041_coverage_depth.benchmark.tsv
    wildcards: sn=NGS1041

bedtools genomecov -d -ibam NGS1041/core/NGS1041_viral_reference.mapping.primertrimmed.sorted.bam >NGS1041/coverage/NGS1041_depth.txt
Activating conda environment: /home/maria/SNAKE_COVID/conda/3850436d
[Thu Jan 28 21:25:36 2021]
Finished job 132.
88 of 164 steps (54%) done
Select jobs to execute...

[Thu Jan 28 21:25:36 2021]
rule generate_coverage_plot:
    input: NGS1041/coverage/NGS1041_depth.txt
    output: NGS1041/coverage/NGS1041_coverage_plot.png
    jobid: 141
    wildcards: sn=NGS1041

/home/maria/covid_analysis_pavlos/covid-19-signal/scripts/generate_coverage_plot.py NGS1041/coverage/NGS1041_depth.txt NGS1041/coverage/NGS1041_coverage_plot.png
Activating conda environment: /home/maria/SNAKE_COVID/conda/4bc6b9de
[Thu Jan 28 21:25:37 2021]
Error in rule generate_coverage_plot:
    jobid: 141
    output: NGS1041/coverage/NGS1041_coverage_plot.png
    conda-env: /home/maria/SNAKE_COVID/conda/4bc6b9de
    shell:
        /home/maria/covid_analysis_pavlos/covid-19-signal/scripts/generate_coverage_plot.py NGS1041/coverage/NGS1041_depth.txt NGS1041/coverage/NGS1041_coverage_plot.png
        (one of the commands exited with non-zero exit code; note that snakemake uses bash strict mode!)

Job failed, going on with independent jobs.
Select jobs to execute...

[Thu Jan 28 21:25:37 2021]
rule run_fastqc_on_mapped_reads:
    input: NGS1041/mapped_clean_reads/NGS1041_R1.fastq.gz, NGS1041/mapped_clean_reads/NGS1041_R2.fastq.gz
    output: NGS1041/mapped_clean_reads/NGS1041_R1_fastqc.html, NGS1041/mapped_clean_reads/NGS1041_R2_fastqc.html
    log: NGS1041/mapped_clean_reads/NGS1041_fastqc.log
    jobid: 84
    benchmark: NGS1041/benchmarks/NGS1041_clean_fastqc.benchmark.tsv
    wildcards: sn=NGS1041


        fastqc -o NGS1041/mapped_clean_reads NGS1041/mapped_clean_reads/NGS1041_R1.fastq.gz NGS1041/mapped_clean_reads/NGS1041_R2.fastq.gz 2> NGS1041/mapped_clean_reads/NGS1041_fastqc.log
        
Activating conda environment: /home/maria/SNAKE_COVID/conda/b95377fd
[Thu Jan 28 21:25:58 2021]
Finished job 84.
89 of 164 steps (54%) done
Select jobs to execute...

[Thu Jan 28 21:25:58 2021]
rule run_ivar_consensus:
    input: NGS1041/core/NGS1041_viral_reference.mapping.primertrimmed.sorted.bam
    output: NGS1041/core/NGS1041.consensus.fa
    log: NGS1041/core/NGS1041_ivar_consensus.log
    jobid: 113
    benchmark: NGS1041/benchmarks/NGS1041_ivar_consensus.benchmark.tsv
    wildcards: sn=NGS1041

(samtools mpileup -aa -A -d 100000 -Q0 NGS1041/core/NGS1041_viral_reference.mapping.primertrimmed.sorted.bam | ivar consensus -t 0.75 -m 10 -n N -p NGS1041/core/NGS1041.consensus) 2>NGS1041/core/NGS1041_ivar_consensus.log
Activating conda environment: /home/maria/SNAKE_COVID/conda/5258de7f
[Thu Jan 28 21:26:24 2021]
Finished job 113.
90 of 164 steps (55%) done
Select jobs to execute...

[Thu Jan 28 21:26:24 2021]
rule run_ivar_variants:
    input: /home/maria/covid_analysis_pavlos/covid-19-signal/data/MN908947.3.fasta, /home/maria/covid_analysis_pavlos/covid-19-signal/data/MN908947.3.fasta.fai, NGS1041/core/NGS1041_viral_reference.mapping.primertrimmed.sorted.bam, /home/maria/covid_analysis_pavlos/covid-19-signal/data/MN908947.3.gff3
    output: NGS1041/core/NGS1041_ivar_variants.tsv
    log: NGS1041/core/NGS1041_ivar_variants.log
    jobid: 123
    benchmark: NGS1041/benchmarks/NGS1041_ivar_variants.benchmark.tsv
    wildcards: sn=NGS1041

(samtools mpileup -aa -A -d 0 --reference /home/maria/covid_analysis_pavlos/covid-19-signal/data/MN908947.3.fasta -B -Q 0 NGS1041/core/NGS1041_viral_reference.mapping.primertrimmed.sorted.bam | ivar variants -r /home/maria/covid_analysis_pavlos/covid-19-signal/data/MN908947.3.fasta -m 10 -p NGS1041/core/NGS1041_ivar_variants -q 20 -t 0.25 -g /home/maria/covid_analysis_pavlos/covid-19-signal/data/MN908947.3.gff3) 2> NGS1041/core/NGS1041_ivar_variants.log
Activating conda environment: /home/maria/SNAKE_COVID/conda/5258de7f
[Thu Jan 28 21:26:51 2021]
Finished job 123.
91 of 164 steps (55%) done
Select jobs to execute...

[Thu Jan 28 21:26:51 2021]
rule run_quast:
    input: NGS1041/core/NGS1041.consensus.fa
    output: NGS1041/quast/NGS1041_quast_report.html
    log: NGS1041/quast/NGS1041_quast.log
    jobid: 159
    benchmark: NGS1041/benchmarks/NGS1041_run_quast.benchmark.tsv
    wildcards: sn=NGS1041

quast NGS1041/core/NGS1041.consensus.fa -r /home/maria/covid_analysis_pavlos/covid-19-signal/data/MN908947.3.fasta -g /home/maria/covid_analysis_pavlos/covid-19-signal/data/MN908947.3.gff3 --output-dir NGS1041/quast --threads 1 >NGS1041/quast/NGS1041_quast.log && for f in NGS1041/quast/report.*; do mv $f ${f/report/NGS1041_quast_report}; done
Activating conda environment: /home/maria/SNAKE_COVID/conda/2d0610a0
[Thu Jan 28 21:26:57 2021]
Finished job 159.
92 of 164 steps (56%) done
Select jobs to execute...

[Thu Jan 28 21:26:57 2021]
rule run_bed_primer_trim:
    input: NGS1045/core/NGS1045_viral_reference.bam
    output: NGS1045/core/NGS1045_viral_reference.mapping.primertrimmed.sorted.bam, NGS1045/core/NGS1045_viral_reference.mapping.primertrimmed.bam, NGS1045/core/NGS1045_viral_reference.mapping.bam
    log: NGS1045/core/NGS1045_ivar_trim.log
    jobid: 106
    benchmark: NGS1045/benchmarks/NGS1045_bed_primer_trim.benchmark.tsv
    wildcards: sn=NGS1045

samtools view -F4 -o NGS1045/core/NGS1045_viral_reference.mapping.bam NGS1045/core/NGS1045_viral_reference.bam; samtools index NGS1045/core/NGS1045_viral_reference.mapping.bam; ivar trim -e -i NGS1045/core/NGS1045_viral_reference.mapping.bam -b /home/maria/covid_analysis_pavlos/covid-19-signal/resources/SARSCoV2.paragon.bed -m 20 -q 20 -p NGS1045/core/NGS1045_viral_reference.mapping.primertrimmed 2> NGS1045/core/NGS1045_ivar_trim.log; samtools sort -o NGS1045/core/NGS1045_viral_reference.mapping.primertrimmed.sorted.bam NGS1045/core/NGS1045_viral_reference.mapping.primertrimmed.bam
Activating conda environment: /home/maria/SNAKE_COVID/conda/5258de7f
[Thu Jan 28 21:29:11 2021]
Finished job 101.
93 of 164 steps (57%) done
Select jobs to execute...

[Thu Jan 28 21:29:12 2021]
rule get_mapping_reads:
    input: NGS1044/core/NGS1044_viral_reference.mapping.primertrimmed.bam
    output: NGS1044/mapped_clean_reads/NGS1044_R1.fastq.gz, NGS1044/mapped_clean_reads/NGS1044_R2.fastq.gz, NGS1044/mapped_clean_reads/NGS1044_singletons.fastq.gz, NGS1044/mapped_clean_reads/NGS1044_sorted_clean.bam
    log: NGS1044/mapped_clean_reads/NGS1044_samtools_fastq.log
    jobid: 100
    benchmark: NGS1044/benchmarks/NGS1044_get_mapping_reads.benchmark.tsv
    wildcards: sn=NGS1044
    priority: 2


        samtools sort -n NGS1044/core/NGS1044_viral_reference.mapping.primertrimmed.bam -o NGS1044/mapped_clean_reads/NGS1044_sorted_clean.bam 2> NGS1044/mapped_clean_reads/NGS1044_samtools_fastq.log
        samtools fastq -1 NGS1044/mapped_clean_reads/NGS1044_R1.fastq.gz -2 NGS1044/mapped_clean_reads/NGS1044_R2.fastq.gz -s NGS1044/mapped_clean_reads/NGS1044_singletons.fastq.gz NGS1044/mapped_clean_reads/NGS1044_sorted_clean.bam 2>> NGS1044/mapped_clean_reads/NGS1044_samtools_fastq.log 
        
Activating conda environment: /home/maria/SNAKE_COVID/conda/3850436d
[Thu Jan 28 21:29:39 2021]
Finished job 32.
94 of 164 steps (57%) done
Select jobs to execute...

[Thu Jan 28 21:29:39 2021]
rule get_host_removed_reads:
    input: NGS1043/host_removal/NGS1043_viral_and_nonmapping_reads.bam
    output: NGS1043/host_removal/NGS1043_R1.fastq.gz, NGS1043/host_removal/NGS1043_R2.fastq.gz, NGS1043/host_removal/NGS1043_singletons.fastq.gz, NGS1043/host_removal/NGS1043_viral_and_nonmapping_reads_filtered_sorted.bam
    log: NGS1043/host_removal/NGS1043_samtools_fastq.log
    jobid: 31
    benchmark: NGS1043/benchmarks/NGS1043_get_host_removed_reads.benchmark.tsv
    wildcards: sn=NGS1043
    threads: 2


        samtools view -b NGS1043/host_removal/NGS1043_viral_and_nonmapping_reads.bam | samtools sort -n -@2 > NGS1043/host_removal/NGS1043_viral_and_nonmapping_reads_filtered_sorted.bam 2> NGS1043/host_removal/NGS1043_samtools_fastq.log
        samtools fastq -1 NGS1043/host_removal/NGS1043_R1.fastq.gz -2 NGS1043/host_removal/NGS1043_R2.fastq.gz -s NGS1043/host_removal/NGS1043_singletons.fastq.gz NGS1043/host_removal/NGS1043_viral_and_nonmapping_reads_filtered_sorted.bam 2>> NGS1043/host_removal/NGS1043_samtools_fastq.log 
        

[Thu Jan 28 21:29:39 2021]
rule coverage_depth:
    input: NGS1044/core/NGS1044_viral_reference.mapping.primertrimmed.sorted.bam
    output: NGS1044/coverage/NGS1044_depth.txt
    jobid: 135
    benchmark: NGS1044/benchmarks/NGS1044_coverage_depth.benchmark.tsv
    wildcards: sn=NGS1044

bedtools genomecov -d -ibam NGS1044/core/NGS1044_viral_reference.mapping.primertrimmed.sorted.bam >NGS1044/coverage/NGS1044_depth.txt

[Thu Jan 28 21:29:39 2021]
rule run_ivar_variants:
    input: /home/maria/covid_analysis_pavlos/covid-19-signal/data/MN908947.3.fasta, /home/maria/covid_analysis_pavlos/covid-19-signal/data/MN908947.3.fasta.fai, NGS1044/core/NGS1044_viral_reference.mapping.primertrimmed.sorted.bam, /home/maria/covid_analysis_pavlos/covid-19-signal/data/MN908947.3.gff3
    output: NGS1044/core/NGS1044_ivar_variants.tsv
    log: NGS1044/core/NGS1044_ivar_variants.log
    jobid: 126
    benchmark: NGS1044/benchmarks/NGS1044_ivar_variants.benchmark.tsv
    wildcards: sn=NGS1044

(samtools mpileup -aa -A -d 0 --reference /home/maria/covid_analysis_pavlos/covid-19-signal/data/MN908947.3.fasta -B -Q 0 NGS1044/core/NGS1044_viral_reference.mapping.primertrimmed.sorted.bam | ivar variants -r /home/maria/covid_analysis_pavlos/covid-19-signal/data/MN908947.3.fasta -m 10 -p NGS1044/core/NGS1044_ivar_variants -q 20 -t 0.25 -g /home/maria/covid_analysis_pavlos/covid-19-signal/data/MN908947.3.gff3) 2> NGS1044/core/NGS1044_ivar_variants.log
Activating conda environment: /home/maria/SNAKE_COVID/conda/3850436d
Activating conda environment: /home/maria/SNAKE_COVID/conda/5258de7f
Activating conda environment: /home/maria/SNAKE_COVID/conda/3850436d
[Thu Jan 28 21:30:26 2021]
Finished job 135.
95 of 164 steps (58%) done
Select jobs to execute...

[Thu Jan 28 21:30:26 2021]
rule generate_coverage_plot:
    input: NGS1044/coverage/NGS1044_depth.txt
    output: NGS1044/coverage/NGS1044_coverage_plot.png
    jobid: 144
    wildcards: sn=NGS1044

/home/maria/covid_analysis_pavlos/covid-19-signal/scripts/generate_coverage_plot.py NGS1044/coverage/NGS1044_depth.txt NGS1044/coverage/NGS1044_coverage_plot.png
Activating conda environment: /home/maria/SNAKE_COVID/conda/4bc6b9de
[Thu Jan 28 21:30:29 2021]
Error in rule generate_coverage_plot:
    jobid: 144
    output: NGS1044/coverage/NGS1044_coverage_plot.png
    conda-env: /home/maria/SNAKE_COVID/conda/4bc6b9de
    shell:
        /home/maria/covid_analysis_pavlos/covid-19-signal/scripts/generate_coverage_plot.py NGS1044/coverage/NGS1044_depth.txt NGS1044/coverage/NGS1044_coverage_plot.png
        (one of the commands exited with non-zero exit code; note that snakemake uses bash strict mode!)

Job failed, going on with independent jobs.
Select jobs to execute...

[Thu Jan 28 21:30:29 2021]
rule run_ivar_consensus:
    input: NGS1044/core/NGS1044_viral_reference.mapping.primertrimmed.sorted.bam
    output: NGS1044/core/NGS1044.consensus.fa
    log: NGS1044/core/NGS1044_ivar_consensus.log
    jobid: 116
    benchmark: NGS1044/benchmarks/NGS1044_ivar_consensus.benchmark.tsv
    wildcards: sn=NGS1044

(samtools mpileup -aa -A -d 100000 -Q0 NGS1044/core/NGS1044_viral_reference.mapping.primertrimmed.sorted.bam | ivar consensus -t 0.75 -m 10 -n N -p NGS1044/core/NGS1044.consensus) 2>NGS1044/core/NGS1044_ivar_consensus.log
Activating conda environment: /home/maria/SNAKE_COVID/conda/5258de7f
[Thu Jan 28 21:30:34 2021]
Finished job 31.
96 of 164 steps (59%) done
Select jobs to execute...

[Thu Jan 28 21:30:34 2021]
rule run_trimgalore:
    input: NGS1043/host_removal/NGS1043_R1.fastq.gz, NGS1043/host_removal/NGS1043_R2.fastq.gz
    output: NGS1043/adapter_trimmed/NGS1043_R1_val_1.fq.gz, NGS1043/adapter_trimmed/NGS1043_R2_val_2.fq.gz, NGS1043/adapter_trimmed/NGS1043_R1_val_1_fastqc.html, NGS1043/adapter_trimmed/NGS1043_R2_val_2_fastqc.html
    log: NGS1043/adapter_trimmed/NGS1043_trim_galore.log
    jobid: 43
    benchmark: NGS1043/benchmarks/NGS1043_trimgalore.benchmark.tsv
    wildcards: sn=NGS1043
    priority: 2
    threads: 2

trim_galore --quality 20 --length 20  -o NGS1043/adapter_trimmed --cores 2 --fastqc --paired NGS1043/host_removal/NGS1043_R1.fastq.gz NGS1043/host_removal/NGS1043_R2.fastq.gz 2> NGS1043/adapter_trimmed/NGS1043_trim_galore.log
Activating conda environment: /home/maria/SNAKE_COVID/conda/b95377fd
[Thu Jan 28 21:30:50 2021]
Finished job 49.
97 of 164 steps (59%) done
Select jobs to execute...

[Thu Jan 28 21:30:50 2021]
rule viral_reference_bwa_map:
    input: NGS1040/adapter_trimmed/NGS1040_R1_val_1_posttrim_filter.fq.gz, NGS1040/adapter_trimmed/NGS1040_R2_val_2_posttrim_filter.fq.gz, NGS1040/core/viral_reference.bwt
    output: NGS1040/core/NGS1040_viral_reference.bam
    log: NGS1040/core/NGS1040_viral_reference_bwa.log
    jobid: 82
    benchmark: NGS1040/benchmarks/NGS1040_viral_reference_bwa_map.benchmark.tsv
    wildcards: sn=NGS1040
    threads: 2

(bwa mem -t 2 NGS1040/core/viral_reference NGS1040/adapter_trimmed/NGS1040_R1_val_1_posttrim_filter.fq.gz NGS1040/adapter_trimmed/NGS1040_R2_val_2_posttrim_filter.fq.gz | samtools view -bS | samtools sort -@2 -o NGS1040/core/NGS1040_viral_reference.bam) 2> NGS1040/core/NGS1040_viral_reference_bwa.log
Activating conda environment: /home/maria/SNAKE_COVID/conda/3850436d
[Thu Jan 28 21:31:15 2021]
Finished job 43.
98 of 164 steps (60%) done
Select jobs to execute...

[Thu Jan 28 21:31:15 2021]
rule run_filtering_of_residual_adapters:
    input: NGS1043/adapter_trimmed/NGS1043_R1_val_1.fq.gz, NGS1043/adapter_trimmed/NGS1043_R2_val_2.fq.gz
    output: NGS1043/adapter_trimmed/NGS1043_R1_val_1_posttrim_filter.fq.gz, NGS1043/adapter_trimmed/NGS1043_R2_val_2_posttrim_filter.fq.gz
    jobid: 52
    wildcards: sn=NGS1043
    priority: 2
    threads: 2


	python3.6 /home/maria/covid_analysis_pavlos/covid-19-signal/scripts/filter_residual_adapters.py --input_R1 NGS1043/adapter_trimmed/NGS1043_R1_val_1.fq.gz --input_R2 NGS1043/adapter_trimmed/NGS1043_R2_val_2.fq.gz
	
Activating conda environment: /home/maria/SNAKE_COVID/conda/3850436d
[Thu Jan 28 21:33:16 2021]
Finished job 126.
99 of 164 steps (60%) done
Select jobs to execute...

[Thu Jan 28 21:33:16 2021]
rule run_kraken2:
    input: NGS1040/adapter_trimmed/NGS1040_R1_val_1_posttrim_filter.fq.gz, NGS1040/adapter_trimmed/NGS1040_R2_val_2_posttrim_filter.fq.gz
    output: NGS1040/kraken2/NGS1040_kraken2.out
    log: NGS1040/kraken2/NGS1040_kraken2.log
    jobid: 149
    benchmark: NGS1040/benchmarks/NGS1040_run_kraken2.benchmark.tsv
    wildcards: sn=NGS1040

cd NGS1040/kraken2 && kraken2 --db /home/maria/covid_analysis_pavlos/covid-19-signal/data/Kraken2/db --threads 1 --quick --unclassified-out "NGS1040_kraken2_unclassified_reads#" --classified-out "NGS1040_kraken2_classified_reads#" --output NGS1040_kraken2.out --paired --gzip-compressed ../../NGS1040/adapter_trimmed/NGS1040_R1_val_1_posttrim_filter.fq.gz ../../NGS1040/adapter_trimmed/NGS1040_R2_val_2_posttrim_filter.fq.gz --report NGS1040_kraken2.report 2>../../NGS1040/kraken2/NGS1040_kraken2.log
[Thu Jan 28 21:33:18 2021]
Finished job 52.
100 of 164 steps (61%) done
Select jobs to execute...

[Thu Jan 28 21:33:19 2021]
rule viral_reference_bwa_map:
    input: NGS1043/adapter_trimmed/NGS1043_R1_val_1_posttrim_filter.fq.gz, NGS1043/adapter_trimmed/NGS1043_R2_val_2_posttrim_filter.fq.gz, NGS1043/core/viral_reference.bwt
    output: NGS1043/core/NGS1043_viral_reference.bam
    log: NGS1043/core/NGS1043_viral_reference_bwa.log
    jobid: 97
    benchmark: NGS1043/benchmarks/NGS1043_viral_reference_bwa_map.benchmark.tsv
    wildcards: sn=NGS1043
    threads: 2

(bwa mem -t 2 NGS1043/core/viral_reference NGS1043/adapter_trimmed/NGS1043_R1_val_1_posttrim_filter.fq.gz NGS1043/adapter_trimmed/NGS1043_R2_val_2_posttrim_filter.fq.gz | samtools view -bS | samtools sort -@2 -o NGS1043/core/NGS1043_viral_reference.bam) 2> NGS1043/core/NGS1043_viral_reference_bwa.log
Activating conda environment: /home/maria/SNAKE_COVID/conda/b95377fd
Activating conda environment: /home/maria/SNAKE_COVID/conda/3850436d
[Thu Jan 28 21:33:31 2021]
Finished job 100.
101 of 164 steps (62%) done
Select jobs to execute...

[Thu Jan 28 21:33:31 2021]
rule run_kraken2:
    input: NGS1043/adapter_trimmed/NGS1043_R1_val_1_posttrim_filter.fq.gz, NGS1043/adapter_trimmed/NGS1043_R2_val_2_posttrim_filter.fq.gz
    output: NGS1043/kraken2/NGS1043_kraken2.out
    log: NGS1043/kraken2/NGS1043_kraken2.log
    jobid: 152
    benchmark: NGS1043/benchmarks/NGS1043_run_kraken2.benchmark.tsv
    wildcards: sn=NGS1043

cd NGS1043/kraken2 && kraken2 --db /home/maria/covid_analysis_pavlos/covid-19-signal/data/Kraken2/db --threads 1 --quick --unclassified-out "NGS1043_kraken2_unclassified_reads#" --classified-out "NGS1043_kraken2_classified_reads#" --output NGS1043_kraken2.out --paired --gzip-compressed ../../NGS1043/adapter_trimmed/NGS1043_R1_val_1_posttrim_filter.fq.gz ../../NGS1043/adapter_trimmed/NGS1043_R2_val_2_posttrim_filter.fq.gz --report NGS1043_kraken2.report 2>../../NGS1043/kraken2/NGS1043_kraken2.log
Activating conda environment: /home/maria/SNAKE_COVID/conda/b95377fd
[Thu Jan 28 21:33:47 2021]
Finished job 152.
102 of 164 steps (62%) done
Select jobs to execute...

[Thu Jan 28 21:33:47 2021]
rule run_fastqc_on_mapped_reads:
    input: NGS1044/mapped_clean_reads/NGS1044_R1.fastq.gz, NGS1044/mapped_clean_reads/NGS1044_R2.fastq.gz
    output: NGS1044/mapped_clean_reads/NGS1044_R1_fastqc.html, NGS1044/mapped_clean_reads/NGS1044_R2_fastqc.html
    log: NGS1044/mapped_clean_reads/NGS1044_fastqc.log
    jobid: 99
    benchmark: NGS1044/benchmarks/NGS1044_clean_fastqc.benchmark.tsv
    wildcards: sn=NGS1044


        fastqc -o NGS1044/mapped_clean_reads NGS1044/mapped_clean_reads/NGS1044_R1.fastq.gz NGS1044/mapped_clean_reads/NGS1044_R2.fastq.gz 2> NGS1044/mapped_clean_reads/NGS1044_fastqc.log
        
Activating conda environment: /home/maria/SNAKE_COVID/conda/b95377fd
[Thu Jan 28 21:33:53 2021]
Finished job 97.
103 of 164 steps (63%) done
Select jobs to execute...

[Thu Jan 28 21:33:53 2021]
rule run_bed_primer_trim:
    input: NGS1043/core/NGS1043_viral_reference.bam
    output: NGS1043/core/NGS1043_viral_reference.mapping.primertrimmed.sorted.bam, NGS1043/core/NGS1043_viral_reference.mapping.primertrimmed.bam, NGS1043/core/NGS1043_viral_reference.mapping.bam
    log: NGS1043/core/NGS1043_ivar_trim.log
    jobid: 96
    benchmark: NGS1043/benchmarks/NGS1043_bed_primer_trim.benchmark.tsv
    wildcards: sn=NGS1043

samtools view -F4 -o NGS1043/core/NGS1043_viral_reference.mapping.bam NGS1043/core/NGS1043_viral_reference.bam; samtools index NGS1043/core/NGS1043_viral_reference.mapping.bam; ivar trim -e -i NGS1043/core/NGS1043_viral_reference.mapping.bam -b /home/maria/covid_analysis_pavlos/covid-19-signal/resources/SARSCoV2.paragon.bed -m 20 -q 20 -p NGS1043/core/NGS1043_viral_reference.mapping.primertrimmed 2> NGS1043/core/NGS1043_ivar_trim.log; samtools sort -o NGS1043/core/NGS1043_viral_reference.mapping.primertrimmed.sorted.bam NGS1043/core/NGS1043_viral_reference.mapping.primertrimmed.bam
Activating conda environment: /home/maria/SNAKE_COVID/conda/5258de7f
[Thu Jan 28 21:34:05 2021]
Finished job 116.
104 of 164 steps (63%) done
Select jobs to execute...

[Thu Jan 28 21:34:05 2021]
rule run_quast:
    input: NGS1044/core/NGS1044.consensus.fa
    output: NGS1044/quast/NGS1044_quast_report.html
    log: NGS1044/quast/NGS1044_quast.log
    jobid: 162
    benchmark: NGS1044/benchmarks/NGS1044_run_quast.benchmark.tsv
    wildcards: sn=NGS1044

quast NGS1044/core/NGS1044.consensus.fa -r /home/maria/covid_analysis_pavlos/covid-19-signal/data/MN908947.3.fasta -g /home/maria/covid_analysis_pavlos/covid-19-signal/data/MN908947.3.gff3 --output-dir NGS1044/quast --threads 1 >NGS1044/quast/NGS1044_quast.log && for f in NGS1044/quast/report.*; do mv $f ${f/report/NGS1044_quast_report}; done
Activating conda environment: /home/maria/SNAKE_COVID/conda/2d0610a0
[Thu Jan 28 21:34:11 2021]
Finished job 162.
105 of 164 steps (64%) done
Select jobs to execute...
Failed to solve scheduling problem with ILP solver. Falling back to greedy solver.Run Snakemake with --verbose to see the full solver output for debugging the problem.
[Thu Jan 28 21:35:06 2021]
Finished job 99.
106 of 164 steps (65%) done
Select jobs to execute...
Failed to solve scheduling problem with ILP solver. Falling back to greedy solver.Run Snakemake with --verbose to see the full solver output for debugging the problem.
[Thu Jan 28 21:36:21 2021]
Finished job 96.
107 of 164 steps (65%) done
Select jobs to execute...

[Thu Jan 28 21:36:21 2021]
rule coverage_depth:
    input: NGS1043/core/NGS1043_viral_reference.mapping.primertrimmed.sorted.bam
    output: NGS1043/coverage/NGS1043_depth.txt
    jobid: 134
    benchmark: NGS1043/benchmarks/NGS1043_coverage_depth.benchmark.tsv
    wildcards: sn=NGS1043

bedtools genomecov -d -ibam NGS1043/core/NGS1043_viral_reference.mapping.primertrimmed.sorted.bam >NGS1043/coverage/NGS1043_depth.txt

[Thu Jan 28 21:36:21 2021]
rule run_ivar_consensus:
    input: NGS1043/core/NGS1043_viral_reference.mapping.primertrimmed.sorted.bam
    output: NGS1043/core/NGS1043.consensus.fa
    log: NGS1043/core/NGS1043_ivar_consensus.log
    jobid: 115
    benchmark: NGS1043/benchmarks/NGS1043_ivar_consensus.benchmark.tsv
    wildcards: sn=NGS1043

(samtools mpileup -aa -A -d 100000 -Q0 NGS1043/core/NGS1043_viral_reference.mapping.primertrimmed.sorted.bam | ivar consensus -t 0.75 -m 10 -n N -p NGS1043/core/NGS1043.consensus) 2>NGS1043/core/NGS1043_ivar_consensus.log

[Thu Jan 28 21:36:21 2021]
rule get_mapping_reads:
    input: NGS1043/core/NGS1043_viral_reference.mapping.primertrimmed.bam
    output: NGS1043/mapped_clean_reads/NGS1043_R1.fastq.gz, NGS1043/mapped_clean_reads/NGS1043_R2.fastq.gz, NGS1043/mapped_clean_reads/NGS1043_singletons.fastq.gz, NGS1043/mapped_clean_reads/NGS1043_sorted_clean.bam
    log: NGS1043/mapped_clean_reads/NGS1043_samtools_fastq.log
    jobid: 95
    benchmark: NGS1043/benchmarks/NGS1043_get_mapping_reads.benchmark.tsv
    wildcards: sn=NGS1043
    priority: 2


        samtools sort -n NGS1043/core/NGS1043_viral_reference.mapping.primertrimmed.bam -o NGS1043/mapped_clean_reads/NGS1043_sorted_clean.bam 2> NGS1043/mapped_clean_reads/NGS1043_samtools_fastq.log
        samtools fastq -1 NGS1043/mapped_clean_reads/NGS1043_R1.fastq.gz -2 NGS1043/mapped_clean_reads/NGS1043_R2.fastq.gz -s NGS1043/mapped_clean_reads/NGS1043_singletons.fastq.gz NGS1043/mapped_clean_reads/NGS1043_sorted_clean.bam 2>> NGS1043/mapped_clean_reads/NGS1043_samtools_fastq.log 
        

[Thu Jan 28 21:36:21 2021]
rule run_ivar_variants:
    input: /home/maria/covid_analysis_pavlos/covid-19-signal/data/MN908947.3.fasta, /home/maria/covid_analysis_pavlos/covid-19-signal/data/MN908947.3.fasta.fai, NGS1043/core/NGS1043_viral_reference.mapping.primertrimmed.sorted.bam, /home/maria/covid_analysis_pavlos/covid-19-signal/data/MN908947.3.gff3
    output: NGS1043/core/NGS1043_ivar_variants.tsv
    log: NGS1043/core/NGS1043_ivar_variants.log
    jobid: 125
    benchmark: NGS1043/benchmarks/NGS1043_ivar_variants.benchmark.tsv
    wildcards: sn=NGS1043

(samtools mpileup -aa -A -d 0 --reference /home/maria/covid_analysis_pavlos/covid-19-signal/data/MN908947.3.fasta -B -Q 0 NGS1043/core/NGS1043_viral_reference.mapping.primertrimmed.sorted.bam | ivar variants -r /home/maria/covid_analysis_pavlos/covid-19-signal/data/MN908947.3.fasta -m 10 -p NGS1043/core/NGS1043_ivar_variants -q 20 -t 0.25 -g /home/maria/covid_analysis_pavlos/covid-19-signal/data/MN908947.3.gff3) 2> NGS1043/core/NGS1043_ivar_variants.log
Activating conda environment: /home/maria/SNAKE_COVID/conda/5258de7f
Activating conda environment: /home/maria/SNAKE_COVID/conda/3850436d
Activating conda environment: /home/maria/SNAKE_COVID/conda/5258de7f
Activating conda environment: /home/maria/SNAKE_COVID/conda/3850436d
[Thu Jan 28 21:36:28 2021]
Finished job 134.
108 of 164 steps (66%) done
Select jobs to execute...

[Thu Jan 28 21:36:28 2021]
rule generate_coverage_plot:
    input: NGS1043/coverage/NGS1043_depth.txt
    output: NGS1043/coverage/NGS1043_coverage_plot.png
    jobid: 143
    wildcards: sn=NGS1043

/home/maria/covid_analysis_pavlos/covid-19-signal/scripts/generate_coverage_plot.py NGS1043/coverage/NGS1043_depth.txt NGS1043/coverage/NGS1043_coverage_plot.png
[Thu Jan 28 21:36:30 2021]
Finished job 115.
109 of 164 steps (66%) done
Select jobs to execute...

[Thu Jan 28 21:36:30 2021]
rule run_quast:
    input: NGS1043/core/NGS1043.consensus.fa
    output: NGS1043/quast/NGS1043_quast_report.html
    log: NGS1043/quast/NGS1043_quast.log
    jobid: 161
    benchmark: NGS1043/benchmarks/NGS1043_run_quast.benchmark.tsv
    wildcards: sn=NGS1043

quast NGS1043/core/NGS1043.consensus.fa -r /home/maria/covid_analysis_pavlos/covid-19-signal/data/MN908947.3.fasta -g /home/maria/covid_analysis_pavlos/covid-19-signal/data/MN908947.3.gff3 --output-dir NGS1043/quast --threads 1 >NGS1043/quast/NGS1043_quast.log && for f in NGS1043/quast/report.*; do mv $f ${f/report/NGS1043_quast_report}; done
Activating conda environment: /home/maria/SNAKE_COVID/conda/4bc6b9de
[Thu Jan 28 21:36:31 2021]
Error in rule generate_coverage_plot:
    jobid: 143
    output: NGS1043/coverage/NGS1043_coverage_plot.png
    conda-env: /home/maria/SNAKE_COVID/conda/4bc6b9de
    shell:
        /home/maria/covid_analysis_pavlos/covid-19-signal/scripts/generate_coverage_plot.py NGS1043/coverage/NGS1043_depth.txt NGS1043/coverage/NGS1043_coverage_plot.png
        (one of the commands exited with non-zero exit code; note that snakemake uses bash strict mode!)

Job failed, going on with independent jobs.
Select jobs to execute...
Failed to solve scheduling problem with ILP solver. Falling back to greedy solver.Run Snakemake with --verbose to see the full solver output for debugging the problem.
Activating conda environment: /home/maria/SNAKE_COVID/conda/2d0610a0
[Thu Jan 28 21:36:34 2021]
Finished job 125.
110 of 164 steps (67%) done
Select jobs to execute...
Failed to solve scheduling problem with ILP solver. Falling back to greedy solver.Run Snakemake with --verbose to see the full solver output for debugging the problem.
[Thu Jan 28 21:36:37 2021]
Finished job 161.
111 of 164 steps (68%) done
Select jobs to execute...
Failed to solve scheduling problem with ILP solver. Falling back to greedy solver.Run Snakemake with --verbose to see the full solver output for debugging the problem.
[Thu Jan 28 21:36:41 2021]
Finished job 95.
112 of 164 steps (68%) done
Select jobs to execute...

[Thu Jan 28 21:36:41 2021]
rule raw_reads_composite_reference_bwa_map:
    input: NGS0990/raw_fastq/NGS0990_R1.fastq.gz, NGS0990/raw_fastq/NGS0990_R2.fastq.gz
    output: NGS0990/host_removal/NGS0990_viral_and_nonmapping_reads.bam
    log: NGS0990/host_removal/NGS0990_human_read_mapping.log
    jobid: 20
    benchmark: NGS0990/benchmarks/NGS0990_composite_reference_bwa_map.benchmark.tsv
    wildcards: sn=NGS0990
    threads: 4

(conda info --envs; bwa mem -t 4 /home/maria/covid_analysis_pavlos/covid-19-signal/data/composite_human_viral_reference.fna NGS0990/raw_fastq/NGS0990_R1.fastq.gz NGS0990/raw_fastq/NGS0990_R2.fastq.gz | /home/maria/covid_analysis_pavlos/covid-19-signal/scripts/filter_non_human_reads.py -c MN908947.3 > NGS0990/host_removal/NGS0990_viral_and_nonmapping_reads.bam) 2> NGS0990/host_removal/NGS0990_human_read_mapping.log
Activating conda environment: /home/maria/SNAKE_COVID/conda/3850436d
[Thu Jan 28 21:37:47 2021]
Finished job 149.
113 of 164 steps (69%) done
Select jobs to execute...

[Thu Jan 28 21:37:47 2021]
rule run_fastqc_on_mapped_reads:
    input: NGS1043/mapped_clean_reads/NGS1043_R1.fastq.gz, NGS1043/mapped_clean_reads/NGS1043_R2.fastq.gz
    output: NGS1043/mapped_clean_reads/NGS1043_R1_fastqc.html, NGS1043/mapped_clean_reads/NGS1043_R2_fastqc.html
    log: NGS1043/mapped_clean_reads/NGS1043_fastqc.log
    jobid: 94
    benchmark: NGS1043/benchmarks/NGS1043_clean_fastqc.benchmark.tsv
    wildcards: sn=NGS1043


        fastqc -o NGS1043/mapped_clean_reads NGS1043/mapped_clean_reads/NGS1043_R1.fastq.gz NGS1043/mapped_clean_reads/NGS1043_R2.fastq.gz 2> NGS1043/mapped_clean_reads/NGS1043_fastqc.log
        
Activating conda environment: /home/maria/SNAKE_COVID/conda/b95377fd
[Thu Jan 28 21:38:00 2021]
Finished job 94.
114 of 164 steps (70%) done
Select jobs to execute...
Failed to solve scheduling problem with ILP solver. Falling back to greedy solver.Run Snakemake with --verbose to see the full solver output for debugging the problem.
[Thu Jan 28 21:38:51 2021]
Finished job 20.
115 of 164 steps (70%) done
Select jobs to execute...

[Thu Jan 28 21:38:51 2021]
rule raw_reads_composite_reference_bwa_map:
    input: NGS1042/raw_fastq/NGS1042_R1.fastq.gz, NGS1042/raw_fastq/NGS1042_R2.fastq.gz
    output: NGS1042/host_removal/NGS1042_viral_and_nonmapping_reads.bam
    log: NGS1042/host_removal/NGS1042_human_read_mapping.log
    jobid: 30
    benchmark: NGS1042/benchmarks/NGS1042_composite_reference_bwa_map.benchmark.tsv
    wildcards: sn=NGS1042
    threads: 4

(conda info --envs; bwa mem -t 4 /home/maria/covid_analysis_pavlos/covid-19-signal/data/composite_human_viral_reference.fna NGS1042/raw_fastq/NGS1042_R1.fastq.gz NGS1042/raw_fastq/NGS1042_R2.fastq.gz | /home/maria/covid_analysis_pavlos/covid-19-signal/scripts/filter_non_human_reads.py -c MN908947.3 > NGS1042/host_removal/NGS1042_viral_and_nonmapping_reads.bam) 2> NGS1042/host_removal/NGS1042_human_read_mapping.log
Activating conda environment: /home/maria/SNAKE_COVID/conda/3850436d
[Thu Jan 28 21:40:29 2021]
Finished job 82.
116 of 164 steps (71%) done
Select jobs to execute...

[Thu Jan 28 21:40:29 2021]
rule run_bed_primer_trim:
    input: NGS1040/core/NGS1040_viral_reference.bam
    output: NGS1040/core/NGS1040_viral_reference.mapping.primertrimmed.sorted.bam, NGS1040/core/NGS1040_viral_reference.mapping.primertrimmed.bam, NGS1040/core/NGS1040_viral_reference.mapping.bam
    log: NGS1040/core/NGS1040_ivar_trim.log
    jobid: 81
    benchmark: NGS1040/benchmarks/NGS1040_bed_primer_trim.benchmark.tsv
    wildcards: sn=NGS1040

samtools view -F4 -o NGS1040/core/NGS1040_viral_reference.mapping.bam NGS1040/core/NGS1040_viral_reference.bam; samtools index NGS1040/core/NGS1040_viral_reference.mapping.bam; ivar trim -e -i NGS1040/core/NGS1040_viral_reference.mapping.bam -b /home/maria/covid_analysis_pavlos/covid-19-signal/resources/SARSCoV2.paragon.bed -m 20 -q 20 -p NGS1040/core/NGS1040_viral_reference.mapping.primertrimmed 2> NGS1040/core/NGS1040_ivar_trim.log; samtools sort -o NGS1040/core/NGS1040_viral_reference.mapping.primertrimmed.sorted.bam NGS1040/core/NGS1040_viral_reference.mapping.primertrimmed.bam

[Thu Jan 28 21:40:29 2021]
rule get_host_removed_reads:
    input: NGS0990/host_removal/NGS0990_viral_and_nonmapping_reads.bam
    output: NGS0990/host_removal/NGS0990_R1.fastq.gz, NGS0990/host_removal/NGS0990_R2.fastq.gz, NGS0990/host_removal/NGS0990_singletons.fastq.gz, NGS0990/host_removal/NGS0990_viral_and_nonmapping_reads_filtered_sorted.bam
    log: NGS0990/host_removal/NGS0990_samtools_fastq.log
    jobid: 19
    benchmark: NGS0990/benchmarks/NGS0990_get_host_removed_reads.benchmark.tsv
    wildcards: sn=NGS0990
    threads: 2


        samtools view -b NGS0990/host_removal/NGS0990_viral_and_nonmapping_reads.bam | samtools sort -n -@2 > NGS0990/host_removal/NGS0990_viral_and_nonmapping_reads_filtered_sorted.bam 2> NGS0990/host_removal/NGS0990_samtools_fastq.log
        samtools fastq -1 NGS0990/host_removal/NGS0990_R1.fastq.gz -2 NGS0990/host_removal/NGS0990_R2.fastq.gz -s NGS0990/host_removal/NGS0990_singletons.fastq.gz NGS0990/host_removal/NGS0990_viral_and_nonmapping_reads_filtered_sorted.bam 2>> NGS0990/host_removal/NGS0990_samtools_fastq.log 
        
Activating conda environment: /home/maria/SNAKE_COVID/conda/5258de7f
Activating conda environment: /home/maria/SNAKE_COVID/conda/3850436d
[Thu Jan 28 21:41:29 2021]
Finished job 19.
117 of 164 steps (71%) done
Select jobs to execute...

[Thu Jan 28 21:41:29 2021]
rule run_trimgalore:
    input: NGS0990/host_removal/NGS0990_R1.fastq.gz, NGS0990/host_removal/NGS0990_R2.fastq.gz
    output: NGS0990/adapter_trimmed/NGS0990_R1_val_1.fq.gz, NGS0990/adapter_trimmed/NGS0990_R2_val_2.fq.gz, NGS0990/adapter_trimmed/NGS0990_R1_val_1_fastqc.html, NGS0990/adapter_trimmed/NGS0990_R2_val_2_fastqc.html
    log: NGS0990/adapter_trimmed/NGS0990_trim_galore.log
    jobid: 37
    benchmark: NGS0990/benchmarks/NGS0990_trimgalore.benchmark.tsv
    wildcards: sn=NGS0990
    priority: 2
    threads: 2

trim_galore --quality 20 --length 20  -o NGS0990/adapter_trimmed --cores 2 --fastqc --paired NGS0990/host_removal/NGS0990_R1.fastq.gz NGS0990/host_removal/NGS0990_R2.fastq.gz 2> NGS0990/adapter_trimmed/NGS0990_trim_galore.log
Activating conda environment: /home/maria/SNAKE_COVID/conda/b95377fd
[Thu Jan 28 21:42:31 2021]
Finished job 37.
118 of 164 steps (72%) done
Select jobs to execute...

[Thu Jan 28 21:42:31 2021]
rule run_filtering_of_residual_adapters:
    input: NGS0990/adapter_trimmed/NGS0990_R1_val_1.fq.gz, NGS0990/adapter_trimmed/NGS0990_R2_val_2.fq.gz
    output: NGS0990/adapter_trimmed/NGS0990_R1_val_1_posttrim_filter.fq.gz, NGS0990/adapter_trimmed/NGS0990_R2_val_2_posttrim_filter.fq.gz
    jobid: 46
    wildcards: sn=NGS0990
    priority: 2
    threads: 2


	python3.6 /home/maria/covid_analysis_pavlos/covid-19-signal/scripts/filter_residual_adapters.py --input_R1 NGS0990/adapter_trimmed/NGS0990_R1_val_1.fq.gz --input_R2 NGS0990/adapter_trimmed/NGS0990_R2_val_2.fq.gz
	
Activating conda environment: /home/maria/SNAKE_COVID/conda/3850436d
[Thu Jan 28 21:46:11 2021]
Finished job 46.
119 of 164 steps (73%) done
Select jobs to execute...

[Thu Jan 28 21:46:11 2021]
rule viral_reference_bwa_map:
    input: NGS0990/adapter_trimmed/NGS0990_R1_val_1_posttrim_filter.fq.gz, NGS0990/adapter_trimmed/NGS0990_R2_val_2_posttrim_filter.fq.gz, NGS0990/core/viral_reference.bwt
    output: NGS0990/core/NGS0990_viral_reference.bam
    log: NGS0990/core/NGS0990_viral_reference_bwa.log
    jobid: 67
    benchmark: NGS0990/benchmarks/NGS0990_viral_reference_bwa_map.benchmark.tsv
    wildcards: sn=NGS0990
    threads: 2

(bwa mem -t 2 NGS0990/core/viral_reference NGS0990/adapter_trimmed/NGS0990_R1_val_1_posttrim_filter.fq.gz NGS0990/adapter_trimmed/NGS0990_R2_val_2_posttrim_filter.fq.gz | samtools view -bS | samtools sort -@2 -o NGS0990/core/NGS0990_viral_reference.bam) 2> NGS0990/core/NGS0990_viral_reference_bwa.log
Activating conda environment: /home/maria/SNAKE_COVID/conda/3850436d
[Thu Jan 28 21:46:57 2021]
Finished job 67.
120 of 164 steps (73%) done
Select jobs to execute...

[Thu Jan 28 21:46:57 2021]
rule run_kraken2:
    input: NGS0990/adapter_trimmed/NGS0990_R1_val_1_posttrim_filter.fq.gz, NGS0990/adapter_trimmed/NGS0990_R2_val_2_posttrim_filter.fq.gz
    output: NGS0990/kraken2/NGS0990_kraken2.out
    log: NGS0990/kraken2/NGS0990_kraken2.log
    jobid: 146
    benchmark: NGS0990/benchmarks/NGS0990_run_kraken2.benchmark.tsv
    wildcards: sn=NGS0990

cd NGS0990/kraken2 && kraken2 --db /home/maria/covid_analysis_pavlos/covid-19-signal/data/Kraken2/db --threads 1 --quick --unclassified-out "NGS0990_kraken2_unclassified_reads#" --classified-out "NGS0990_kraken2_classified_reads#" --output NGS0990_kraken2.out --paired --gzip-compressed ../../NGS0990/adapter_trimmed/NGS0990_R1_val_1_posttrim_filter.fq.gz ../../NGS0990/adapter_trimmed/NGS0990_R2_val_2_posttrim_filter.fq.gz --report NGS0990_kraken2.report 2>../../NGS0990/kraken2/NGS0990_kraken2.log

[Thu Jan 28 21:46:57 2021]
rule run_bed_primer_trim:
    input: NGS0990/core/NGS0990_viral_reference.bam
    output: NGS0990/core/NGS0990_viral_reference.mapping.primertrimmed.sorted.bam, NGS0990/core/NGS0990_viral_reference.mapping.primertrimmed.bam, NGS0990/core/NGS0990_viral_reference.mapping.bam
    log: NGS0990/core/NGS0990_ivar_trim.log
    jobid: 66
    benchmark: NGS0990/benchmarks/NGS0990_bed_primer_trim.benchmark.tsv
    wildcards: sn=NGS0990

samtools view -F4 -o NGS0990/core/NGS0990_viral_reference.mapping.bam NGS0990/core/NGS0990_viral_reference.bam; samtools index NGS0990/core/NGS0990_viral_reference.mapping.bam; ivar trim -e -i NGS0990/core/NGS0990_viral_reference.mapping.bam -b /home/maria/covid_analysis_pavlos/covid-19-signal/resources/SARSCoV2.paragon.bed -m 20 -q 20 -p NGS0990/core/NGS0990_viral_reference.mapping.primertrimmed 2> NGS0990/core/NGS0990_ivar_trim.log; samtools sort -o NGS0990/core/NGS0990_viral_reference.mapping.primertrimmed.sorted.bam NGS0990/core/NGS0990_viral_reference.mapping.primertrimmed.bam
Activating conda environment: /home/maria/SNAKE_COVID/conda/b95377fd
Activating conda environment: /home/maria/SNAKE_COVID/conda/5258de7f
[Thu Jan 28 21:47:21 2021]
Finished job 146.
121 of 164 steps (74%) done
[Thu Jan 28 21:48:28 2021]
Finished job 30.
122 of 164 steps (74%) done
Select jobs to execute...

[Thu Jan 28 21:48:28 2021]
rule get_host_removed_reads:
    input: NGS1042/host_removal/NGS1042_viral_and_nonmapping_reads.bam
    output: NGS1042/host_removal/NGS1042_R1.fastq.gz, NGS1042/host_removal/NGS1042_R2.fastq.gz, NGS1042/host_removal/NGS1042_singletons.fastq.gz, NGS1042/host_removal/NGS1042_viral_and_nonmapping_reads_filtered_sorted.bam
    log: NGS1042/host_removal/NGS1042_samtools_fastq.log
    jobid: 29
    benchmark: NGS1042/benchmarks/NGS1042_get_host_removed_reads.benchmark.tsv
    wildcards: sn=NGS1042
    threads: 2


        samtools view -b NGS1042/host_removal/NGS1042_viral_and_nonmapping_reads.bam | samtools sort -n -@2 > NGS1042/host_removal/NGS1042_viral_and_nonmapping_reads_filtered_sorted.bam 2> NGS1042/host_removal/NGS1042_samtools_fastq.log
        samtools fastq -1 NGS1042/host_removal/NGS1042_R1.fastq.gz -2 NGS1042/host_removal/NGS1042_R2.fastq.gz -s NGS1042/host_removal/NGS1042_singletons.fastq.gz NGS1042/host_removal/NGS1042_viral_and_nonmapping_reads_filtered_sorted.bam 2>> NGS1042/host_removal/NGS1042_samtools_fastq.log 
        
Activating conda environment: /home/maria/SNAKE_COVID/conda/3850436d
[Thu Jan 28 21:49:38 2021]
Finished job 66.
123 of 164 steps (75%) done
Select jobs to execute...

[Thu Jan 28 21:49:38 2021]
rule get_mapping_reads:
    input: NGS0990/core/NGS0990_viral_reference.mapping.primertrimmed.bam
    output: NGS0990/mapped_clean_reads/NGS0990_R1.fastq.gz, NGS0990/mapped_clean_reads/NGS0990_R2.fastq.gz, NGS0990/mapped_clean_reads/NGS0990_singletons.fastq.gz, NGS0990/mapped_clean_reads/NGS0990_sorted_clean.bam
    log: NGS0990/mapped_clean_reads/NGS0990_samtools_fastq.log
    jobid: 65
    benchmark: NGS0990/benchmarks/NGS0990_get_mapping_reads.benchmark.tsv
    wildcards: sn=NGS0990
    priority: 2


        samtools sort -n NGS0990/core/NGS0990_viral_reference.mapping.primertrimmed.bam -o NGS0990/mapped_clean_reads/NGS0990_sorted_clean.bam 2> NGS0990/mapped_clean_reads/NGS0990_samtools_fastq.log
        samtools fastq -1 NGS0990/mapped_clean_reads/NGS0990_R1.fastq.gz -2 NGS0990/mapped_clean_reads/NGS0990_R2.fastq.gz -s NGS0990/mapped_clean_reads/NGS0990_singletons.fastq.gz NGS0990/mapped_clean_reads/NGS0990_sorted_clean.bam 2>> NGS0990/mapped_clean_reads/NGS0990_samtools_fastq.log 
        

[Thu Jan 28 21:49:38 2021]
rule run_ivar_variants:
    input: /home/maria/covid_analysis_pavlos/covid-19-signal/data/MN908947.3.fasta, /home/maria/covid_analysis_pavlos/covid-19-signal/data/MN908947.3.fasta.fai, NGS0990/core/NGS0990_viral_reference.mapping.primertrimmed.sorted.bam, /home/maria/covid_analysis_pavlos/covid-19-signal/data/MN908947.3.gff3
    output: NGS0990/core/NGS0990_ivar_variants.tsv
    log: NGS0990/core/NGS0990_ivar_variants.log
    jobid: 118
    benchmark: NGS0990/benchmarks/NGS0990_ivar_variants.benchmark.tsv
    wildcards: sn=NGS0990

(samtools mpileup -aa -A -d 0 --reference /home/maria/covid_analysis_pavlos/covid-19-signal/data/MN908947.3.fasta -B -Q 0 NGS0990/core/NGS0990_viral_reference.mapping.primertrimmed.sorted.bam | ivar variants -r /home/maria/covid_analysis_pavlos/covid-19-signal/data/MN908947.3.fasta -m 10 -p NGS0990/core/NGS0990_ivar_variants -q 20 -t 0.25 -g /home/maria/covid_analysis_pavlos/covid-19-signal/data/MN908947.3.gff3) 2> NGS0990/core/NGS0990_ivar_variants.log

[Thu Jan 28 21:49:38 2021]
rule run_ivar_consensus:
    input: NGS0990/core/NGS0990_viral_reference.mapping.primertrimmed.sorted.bam
    output: NGS0990/core/NGS0990.consensus.fa
    log: NGS0990/core/NGS0990_ivar_consensus.log
    jobid: 109
    benchmark: NGS0990/benchmarks/NGS0990_ivar_consensus.benchmark.tsv
    wildcards: sn=NGS0990

(samtools mpileup -aa -A -d 100000 -Q0 NGS0990/core/NGS0990_viral_reference.mapping.primertrimmed.sorted.bam | ivar consensus -t 0.75 -m 10 -n N -p NGS0990/core/NGS0990.consensus) 2>NGS0990/core/NGS0990_ivar_consensus.log

[Thu Jan 28 21:49:38 2021]
rule coverage_depth:
    input: NGS0990/core/NGS0990_viral_reference.mapping.primertrimmed.sorted.bam
    output: NGS0990/coverage/NGS0990_depth.txt
    jobid: 128
    benchmark: NGS0990/benchmarks/NGS0990_coverage_depth.benchmark.tsv
    wildcards: sn=NGS0990

bedtools genomecov -d -ibam NGS0990/core/NGS0990_viral_reference.mapping.primertrimmed.sorted.bam >NGS0990/coverage/NGS0990_depth.txt
Activating conda environment: /home/maria/SNAKE_COVID/conda/3850436d
Activating conda environment: /home/maria/SNAKE_COVID/conda/3850436d
Activating conda environment: /home/maria/SNAKE_COVID/conda/5258de7f
Activating conda environment: /home/maria/SNAKE_COVID/conda/5258de7f
[Thu Jan 28 21:49:50 2021]
Finished job 128.
124 of 164 steps (76%) done
Select jobs to execute...

[Thu Jan 28 21:49:50 2021]
rule generate_coverage_plot:
    input: NGS0990/coverage/NGS0990_depth.txt
    output: NGS0990/coverage/NGS0990_coverage_plot.png
    jobid: 137
    wildcards: sn=NGS0990

/home/maria/covid_analysis_pavlos/covid-19-signal/scripts/generate_coverage_plot.py NGS0990/coverage/NGS0990_depth.txt NGS0990/coverage/NGS0990_coverage_plot.png
Activating conda environment: /home/maria/SNAKE_COVID/conda/4bc6b9de
[Thu Jan 28 21:49:53 2021]
Error in rule generate_coverage_plot:
    jobid: 137
    output: NGS0990/coverage/NGS0990_coverage_plot.png
    conda-env: /home/maria/SNAKE_COVID/conda/4bc6b9de
    shell:
        /home/maria/covid_analysis_pavlos/covid-19-signal/scripts/generate_coverage_plot.py NGS0990/coverage/NGS0990_depth.txt NGS0990/coverage/NGS0990_coverage_plot.png
        (one of the commands exited with non-zero exit code; note that snakemake uses bash strict mode!)

Job failed, going on with independent jobs.
[Thu Jan 28 21:50:00 2021]
Finished job 109.
125 of 164 steps (76%) done
Select jobs to execute...

[Thu Jan 28 21:50:00 2021]
rule run_quast:
    input: NGS0990/core/NGS0990.consensus.fa
    output: NGS0990/quast/NGS0990_quast_report.html
    log: NGS0990/quast/NGS0990_quast.log
    jobid: 155
    benchmark: NGS0990/benchmarks/NGS0990_run_quast.benchmark.tsv
    wildcards: sn=NGS0990

quast NGS0990/core/NGS0990.consensus.fa -r /home/maria/covid_analysis_pavlos/covid-19-signal/data/MN908947.3.fasta -g /home/maria/covid_analysis_pavlos/covid-19-signal/data/MN908947.3.gff3 --output-dir NGS0990/quast --threads 1 >NGS0990/quast/NGS0990_quast.log && for f in NGS0990/quast/report.*; do mv $f ${f/report/NGS0990_quast_report}; done
[Thu Jan 28 21:50:01 2021]
Finished job 118.
126 of 164 steps (77%) done
Activating conda environment: /home/maria/SNAKE_COVID/conda/2d0610a0
[Thu Jan 28 21:50:05 2021]
Finished job 155.
127 of 164 steps (77%) done
[Thu Jan 28 21:50:17 2021]
Finished job 65.
128 of 164 steps (78%) done
Select jobs to execute...

[Thu Jan 28 21:50:17 2021]
rule run_fastqc_on_mapped_reads:
    input: NGS0990/mapped_clean_reads/NGS0990_R1.fastq.gz, NGS0990/mapped_clean_reads/NGS0990_R2.fastq.gz
    output: NGS0990/mapped_clean_reads/NGS0990_R1_fastqc.html, NGS0990/mapped_clean_reads/NGS0990_R2_fastqc.html
    log: NGS0990/mapped_clean_reads/NGS0990_fastqc.log
    jobid: 64
    benchmark: NGS0990/benchmarks/NGS0990_clean_fastqc.benchmark.tsv
    wildcards: sn=NGS0990


        fastqc -o NGS0990/mapped_clean_reads NGS0990/mapped_clean_reads/NGS0990_R1.fastq.gz NGS0990/mapped_clean_reads/NGS0990_R2.fastq.gz 2> NGS0990/mapped_clean_reads/NGS0990_fastqc.log
        
Activating conda environment: /home/maria/SNAKE_COVID/conda/b95377fd
[Thu Jan 28 21:50:31 2021]
Finished job 64.
129 of 164 steps (79%) done
[Thu Jan 28 21:58:00 2021]
Finished job 29.
130 of 164 steps (79%) done
Select jobs to execute...

[Thu Jan 28 21:58:00 2021]
rule run_trimgalore:
    input: NGS1042/host_removal/NGS1042_R1.fastq.gz, NGS1042/host_removal/NGS1042_R2.fastq.gz
    output: NGS1042/adapter_trimmed/NGS1042_R1_val_1.fq.gz, NGS1042/adapter_trimmed/NGS1042_R2_val_2.fq.gz, NGS1042/adapter_trimmed/NGS1042_R1_val_1_fastqc.html, NGS1042/adapter_trimmed/NGS1042_R2_val_2_fastqc.html
    log: NGS1042/adapter_trimmed/NGS1042_trim_galore.log
    jobid: 42
    benchmark: NGS1042/benchmarks/NGS1042_trimgalore.benchmark.tsv
    wildcards: sn=NGS1042
    priority: 2
    threads: 2

trim_galore --quality 20 --length 20  -o NGS1042/adapter_trimmed --cores 2 --fastqc --paired NGS1042/host_removal/NGS1042_R1.fastq.gz NGS1042/host_removal/NGS1042_R2.fastq.gz 2> NGS1042/adapter_trimmed/NGS1042_trim_galore.log
Activating conda environment: /home/maria/SNAKE_COVID/conda/b95377fd
[Thu Jan 28 22:01:18 2021]
Finished job 106.
131 of 164 steps (80%) done
Select jobs to execute...

[Thu Jan 28 22:01:18 2021]
rule run_ivar_consensus:
    input: NGS1045/core/NGS1045_viral_reference.mapping.primertrimmed.sorted.bam
    output: NGS1045/core/NGS1045.consensus.fa
    log: NGS1045/core/NGS1045_ivar_consensus.log
    jobid: 117
    benchmark: NGS1045/benchmarks/NGS1045_ivar_consensus.benchmark.tsv
    wildcards: sn=NGS1045

(samtools mpileup -aa -A -d 100000 -Q0 NGS1045/core/NGS1045_viral_reference.mapping.primertrimmed.sorted.bam | ivar consensus -t 0.75 -m 10 -n N -p NGS1045/core/NGS1045.consensus) 2>NGS1045/core/NGS1045_ivar_consensus.log

[Thu Jan 28 22:01:18 2021]
rule coverage_depth:
    input: NGS1045/core/NGS1045_viral_reference.mapping.primertrimmed.sorted.bam
    output: NGS1045/coverage/NGS1045_depth.txt
    jobid: 136
    benchmark: NGS1045/benchmarks/NGS1045_coverage_depth.benchmark.tsv
    wildcards: sn=NGS1045

bedtools genomecov -d -ibam NGS1045/core/NGS1045_viral_reference.mapping.primertrimmed.sorted.bam >NGS1045/coverage/NGS1045_depth.txt

[Thu Jan 28 22:01:18 2021]
rule get_mapping_reads:
    input: NGS1045/core/NGS1045_viral_reference.mapping.primertrimmed.bam
    output: NGS1045/mapped_clean_reads/NGS1045_R1.fastq.gz, NGS1045/mapped_clean_reads/NGS1045_R2.fastq.gz, NGS1045/mapped_clean_reads/NGS1045_singletons.fastq.gz, NGS1045/mapped_clean_reads/NGS1045_sorted_clean.bam
    log: NGS1045/mapped_clean_reads/NGS1045_samtools_fastq.log
    jobid: 105
    benchmark: NGS1045/benchmarks/NGS1045_get_mapping_reads.benchmark.tsv
    wildcards: sn=NGS1045
    priority: 2


        samtools sort -n NGS1045/core/NGS1045_viral_reference.mapping.primertrimmed.bam -o NGS1045/mapped_clean_reads/NGS1045_sorted_clean.bam 2> NGS1045/mapped_clean_reads/NGS1045_samtools_fastq.log
        samtools fastq -1 NGS1045/mapped_clean_reads/NGS1045_R1.fastq.gz -2 NGS1045/mapped_clean_reads/NGS1045_R2.fastq.gz -s NGS1045/mapped_clean_reads/NGS1045_singletons.fastq.gz NGS1045/mapped_clean_reads/NGS1045_sorted_clean.bam 2>> NGS1045/mapped_clean_reads/NGS1045_samtools_fastq.log 
        

[Thu Jan 28 22:01:18 2021]
rule run_ivar_variants:
    input: /home/maria/covid_analysis_pavlos/covid-19-signal/data/MN908947.3.fasta, /home/maria/covid_analysis_pavlos/covid-19-signal/data/MN908947.3.fasta.fai, NGS1045/core/NGS1045_viral_reference.mapping.primertrimmed.sorted.bam, /home/maria/covid_analysis_pavlos/covid-19-signal/data/MN908947.3.gff3
    output: NGS1045/core/NGS1045_ivar_variants.tsv
    log: NGS1045/core/NGS1045_ivar_variants.log
    jobid: 127
    benchmark: NGS1045/benchmarks/NGS1045_ivar_variants.benchmark.tsv
    wildcards: sn=NGS1045

(samtools mpileup -aa -A -d 0 --reference /home/maria/covid_analysis_pavlos/covid-19-signal/data/MN908947.3.fasta -B -Q 0 NGS1045/core/NGS1045_viral_reference.mapping.primertrimmed.sorted.bam | ivar variants -r /home/maria/covid_analysis_pavlos/covid-19-signal/data/MN908947.3.fasta -m 10 -p NGS1045/core/NGS1045_ivar_variants -q 20 -t 0.25 -g /home/maria/covid_analysis_pavlos/covid-19-signal/data/MN908947.3.gff3) 2> NGS1045/core/NGS1045_ivar_variants.log
Activating conda environment: /home/maria/SNAKE_COVID/conda/3850436d
Activating conda environment: /home/maria/SNAKE_COVID/conda/5258de7f
Activating conda environment: /home/maria/SNAKE_COVID/conda/3850436d
Activating conda environment: /home/maria/SNAKE_COVID/conda/5258de7f
[Thu Jan 28 22:03:05 2021]
Finished job 136.
132 of 164 steps (80%) done
Select jobs to execute...

[Thu Jan 28 22:03:05 2021]
rule generate_coverage_plot:
    input: NGS1045/coverage/NGS1045_depth.txt
    output: NGS1045/coverage/NGS1045_coverage_plot.png
    jobid: 145
    wildcards: sn=NGS1045

/home/maria/covid_analysis_pavlos/covid-19-signal/scripts/generate_coverage_plot.py NGS1045/coverage/NGS1045_depth.txt NGS1045/coverage/NGS1045_coverage_plot.png
Activating conda environment: /home/maria/SNAKE_COVID/conda/4bc6b9de
[Thu Jan 28 22:03:08 2021]
Error in rule generate_coverage_plot:
    jobid: 145
    output: NGS1045/coverage/NGS1045_coverage_plot.png
    conda-env: /home/maria/SNAKE_COVID/conda/4bc6b9de
    shell:
        /home/maria/covid_analysis_pavlos/covid-19-signal/scripts/generate_coverage_plot.py NGS1045/coverage/NGS1045_depth.txt NGS1045/coverage/NGS1045_coverage_plot.png
        (one of the commands exited with non-zero exit code; note that snakemake uses bash strict mode!)

Job failed, going on with independent jobs.
[Thu Jan 28 22:06:57 2021]
Finished job 42.
133 of 164 steps (81%) done
Select jobs to execute...

[Thu Jan 28 22:06:57 2021]
rule run_filtering_of_residual_adapters:
    input: NGS1042/adapter_trimmed/NGS1042_R1_val_1.fq.gz, NGS1042/adapter_trimmed/NGS1042_R2_val_2.fq.gz
    output: NGS1042/adapter_trimmed/NGS1042_R1_val_1_posttrim_filter.fq.gz, NGS1042/adapter_trimmed/NGS1042_R2_val_2_posttrim_filter.fq.gz
    jobid: 51
    wildcards: sn=NGS1042
    priority: 2
    threads: 2


	python3.6 /home/maria/covid_analysis_pavlos/covid-19-signal/scripts/filter_residual_adapters.py --input_R1 NGS1042/adapter_trimmed/NGS1042_R1_val_1.fq.gz --input_R2 NGS1042/adapter_trimmed/NGS1042_R2_val_2.fq.gz
	
Activating conda environment: /home/maria/SNAKE_COVID/conda/3850436d
[Thu Jan 28 22:07:03 2021]
Finished job 117.
134 of 164 steps (82%) done
Select jobs to execute...

[Thu Jan 28 22:07:03 2021]
rule run_quast:
    input: NGS1045/core/NGS1045.consensus.fa
    output: NGS1045/quast/NGS1045_quast_report.html
    log: NGS1045/quast/NGS1045_quast.log
    jobid: 163
    benchmark: NGS1045/benchmarks/NGS1045_run_quast.benchmark.tsv
    wildcards: sn=NGS1045

quast NGS1045/core/NGS1045.consensus.fa -r /home/maria/covid_analysis_pavlos/covid-19-signal/data/MN908947.3.fasta -g /home/maria/covid_analysis_pavlos/covid-19-signal/data/MN908947.3.gff3 --output-dir NGS1045/quast --threads 1 >NGS1045/quast/NGS1045_quast.log && for f in NGS1045/quast/report.*; do mv $f ${f/report/NGS1045_quast_report}; done
Activating conda environment: /home/maria/SNAKE_COVID/conda/2d0610a0
[Thu Jan 28 22:07:09 2021]
Finished job 163.
135 of 164 steps (82%) done
[Thu Jan 28 22:08:38 2021]
Finished job 127.
136 of 164 steps (83%) done
[Thu Jan 28 22:08:53 2021]
Finished job 105.
137 of 164 steps (84%) done
Select jobs to execute...

[Thu Jan 28 22:08:53 2021]
rule run_fastqc_on_mapped_reads:
    input: NGS1045/mapped_clean_reads/NGS1045_R1.fastq.gz, NGS1045/mapped_clean_reads/NGS1045_R2.fastq.gz
    output: NGS1045/mapped_clean_reads/NGS1045_R1_fastqc.html, NGS1045/mapped_clean_reads/NGS1045_R2_fastqc.html
    log: NGS1045/mapped_clean_reads/NGS1045_fastqc.log
    jobid: 104
    benchmark: NGS1045/benchmarks/NGS1045_clean_fastqc.benchmark.tsv
    wildcards: sn=NGS1045


        fastqc -o NGS1045/mapped_clean_reads NGS1045/mapped_clean_reads/NGS1045_R1.fastq.gz NGS1045/mapped_clean_reads/NGS1045_R2.fastq.gz 2> NGS1045/mapped_clean_reads/NGS1045_fastqc.log
        
Activating conda environment: /home/maria/SNAKE_COVID/conda/b95377fd
[Thu Jan 28 22:10:34 2021]
Finished job 104.
138 of 164 steps (84%) done
[Thu Jan 28 22:16:37 2021]
Finished job 81.
139 of 164 steps (85%) done
Select jobs to execute...

[Thu Jan 28 22:16:37 2021]
rule coverage_depth:
    input: NGS1040/core/NGS1040_viral_reference.mapping.primertrimmed.sorted.bam
    output: NGS1040/coverage/NGS1040_depth.txt
    jobid: 131
    benchmark: NGS1040/benchmarks/NGS1040_coverage_depth.benchmark.tsv
    wildcards: sn=NGS1040

bedtools genomecov -d -ibam NGS1040/core/NGS1040_viral_reference.mapping.primertrimmed.sorted.bam >NGS1040/coverage/NGS1040_depth.txt

[Thu Jan 28 22:16:37 2021]
rule run_ivar_variants:
    input: /home/maria/covid_analysis_pavlos/covid-19-signal/data/MN908947.3.fasta, /home/maria/covid_analysis_pavlos/covid-19-signal/data/MN908947.3.fasta.fai, NGS1040/core/NGS1040_viral_reference.mapping.primertrimmed.sorted.bam, /home/maria/covid_analysis_pavlos/covid-19-signal/data/MN908947.3.gff3
    output: NGS1040/core/NGS1040_ivar_variants.tsv
    log: NGS1040/core/NGS1040_ivar_variants.log
    jobid: 122
    benchmark: NGS1040/benchmarks/NGS1040_ivar_variants.benchmark.tsv
    wildcards: sn=NGS1040

(samtools mpileup -aa -A -d 0 --reference /home/maria/covid_analysis_pavlos/covid-19-signal/data/MN908947.3.fasta -B -Q 0 NGS1040/core/NGS1040_viral_reference.mapping.primertrimmed.sorted.bam | ivar variants -r /home/maria/covid_analysis_pavlos/covid-19-signal/data/MN908947.3.fasta -m 10 -p NGS1040/core/NGS1040_ivar_variants -q 20 -t 0.25 -g /home/maria/covid_analysis_pavlos/covid-19-signal/data/MN908947.3.gff3) 2> NGS1040/core/NGS1040_ivar_variants.log

[Thu Jan 28 22:16:37 2021]
rule get_mapping_reads:
    input: NGS1040/core/NGS1040_viral_reference.mapping.primertrimmed.bam
    output: NGS1040/mapped_clean_reads/NGS1040_R1.fastq.gz, NGS1040/mapped_clean_reads/NGS1040_R2.fastq.gz, NGS1040/mapped_clean_reads/NGS1040_singletons.fastq.gz, NGS1040/mapped_clean_reads/NGS1040_sorted_clean.bam
    log: NGS1040/mapped_clean_reads/NGS1040_samtools_fastq.log
    jobid: 80
    benchmark: NGS1040/benchmarks/NGS1040_get_mapping_reads.benchmark.tsv
    wildcards: sn=NGS1040
    priority: 2


        samtools sort -n NGS1040/core/NGS1040_viral_reference.mapping.primertrimmed.bam -o NGS1040/mapped_clean_reads/NGS1040_sorted_clean.bam 2> NGS1040/mapped_clean_reads/NGS1040_samtools_fastq.log
        samtools fastq -1 NGS1040/mapped_clean_reads/NGS1040_R1.fastq.gz -2 NGS1040/mapped_clean_reads/NGS1040_R2.fastq.gz -s NGS1040/mapped_clean_reads/NGS1040_singletons.fastq.gz NGS1040/mapped_clean_reads/NGS1040_sorted_clean.bam 2>> NGS1040/mapped_clean_reads/NGS1040_samtools_fastq.log 
        

[Thu Jan 28 22:16:37 2021]
rule run_ivar_consensus:
    input: NGS1040/core/NGS1040_viral_reference.mapping.primertrimmed.sorted.bam
    output: NGS1040/core/NGS1040.consensus.fa
    log: NGS1040/core/NGS1040_ivar_consensus.log
    jobid: 112
    benchmark: NGS1040/benchmarks/NGS1040_ivar_consensus.benchmark.tsv
    wildcards: sn=NGS1040

(samtools mpileup -aa -A -d 100000 -Q0 NGS1040/core/NGS1040_viral_reference.mapping.primertrimmed.sorted.bam | ivar consensus -t 0.75 -m 10 -n N -p NGS1040/core/NGS1040.consensus) 2>NGS1040/core/NGS1040_ivar_consensus.log
Activating conda environment: /home/maria/SNAKE_COVID/conda/5258de7f
Activating conda environment: /home/maria/SNAKE_COVID/conda/3850436d
Activating conda environment: /home/maria/SNAKE_COVID/conda/3850436d
Activating conda environment: /home/maria/SNAKE_COVID/conda/5258de7f
[Thu Jan 28 22:18:09 2021]
Finished job 131.
140 of 164 steps (85%) done
Select jobs to execute...

[Thu Jan 28 22:18:09 2021]
rule generate_coverage_plot:
    input: NGS1040/coverage/NGS1040_depth.txt
    output: NGS1040/coverage/NGS1040_coverage_plot.png
    jobid: 140
    wildcards: sn=NGS1040

/home/maria/covid_analysis_pavlos/covid-19-signal/scripts/generate_coverage_plot.py NGS1040/coverage/NGS1040_depth.txt NGS1040/coverage/NGS1040_coverage_plot.png
Activating conda environment: /home/maria/SNAKE_COVID/conda/4bc6b9de
[Thu Jan 28 22:18:12 2021]
Error in rule generate_coverage_plot:
    jobid: 140
    output: NGS1040/coverage/NGS1040_coverage_plot.png
    conda-env: /home/maria/SNAKE_COVID/conda/4bc6b9de
    shell:
        /home/maria/covid_analysis_pavlos/covid-19-signal/scripts/generate_coverage_plot.py NGS1040/coverage/NGS1040_depth.txt NGS1040/coverage/NGS1040_coverage_plot.png
        (one of the commands exited with non-zero exit code; note that snakemake uses bash strict mode!)

Job failed, going on with independent jobs.
[Thu Jan 28 22:22:03 2021]
Finished job 112.
141 of 164 steps (86%) done
Select jobs to execute...

[Thu Jan 28 22:22:03 2021]
rule run_quast:
    input: NGS1040/core/NGS1040.consensus.fa
    output: NGS1040/quast/NGS1040_quast_report.html
    log: NGS1040/quast/NGS1040_quast.log
    jobid: 158
    benchmark: NGS1040/benchmarks/NGS1040_run_quast.benchmark.tsv
    wildcards: sn=NGS1040

quast NGS1040/core/NGS1040.consensus.fa -r /home/maria/covid_analysis_pavlos/covid-19-signal/data/MN908947.3.fasta -g /home/maria/covid_analysis_pavlos/covid-19-signal/data/MN908947.3.gff3 --output-dir NGS1040/quast --threads 1 >NGS1040/quast/NGS1040_quast.log && for f in NGS1040/quast/report.*; do mv $f ${f/report/NGS1040_quast_report}; done
Activating conda environment: /home/maria/SNAKE_COVID/conda/2d0610a0
[Thu Jan 28 22:22:08 2021]
Finished job 158.
142 of 164 steps (87%) done
[Thu Jan 28 22:23:31 2021]
Finished job 122.
143 of 164 steps (87%) done
[Thu Jan 28 22:24:08 2021]
Finished job 80.
144 of 164 steps (88%) done
Select jobs to execute...

[Thu Jan 28 22:24:08 2021]
rule run_fastqc_on_mapped_reads:
    input: NGS1040/mapped_clean_reads/NGS1040_R1.fastq.gz, NGS1040/mapped_clean_reads/NGS1040_R2.fastq.gz
    output: NGS1040/mapped_clean_reads/NGS1040_R1_fastqc.html, NGS1040/mapped_clean_reads/NGS1040_R2_fastqc.html
    log: NGS1040/mapped_clean_reads/NGS1040_fastqc.log
    jobid: 79
    benchmark: NGS1040/benchmarks/NGS1040_clean_fastqc.benchmark.tsv
    wildcards: sn=NGS1040


        fastqc -o NGS1040/mapped_clean_reads NGS1040/mapped_clean_reads/NGS1040_R1.fastq.gz NGS1040/mapped_clean_reads/NGS1040_R2.fastq.gz 2> NGS1040/mapped_clean_reads/NGS1040_fastqc.log
        
Activating conda environment: /home/maria/SNAKE_COVID/conda/b95377fd
[Thu Jan 28 22:26:04 2021]
Finished job 79.
145 of 164 steps (88%) done
[Thu Jan 28 22:43:29 2021]
Finished job 51.
146 of 164 steps (89%) done
Select jobs to execute...

[Thu Jan 28 22:43:29 2021]
rule viral_reference_bwa_map:
    input: NGS1042/adapter_trimmed/NGS1042_R1_val_1_posttrim_filter.fq.gz, NGS1042/adapter_trimmed/NGS1042_R2_val_2_posttrim_filter.fq.gz, NGS1042/core/viral_reference.bwt
    output: NGS1042/core/NGS1042_viral_reference.bam
    log: NGS1042/core/NGS1042_viral_reference_bwa.log
    jobid: 92
    benchmark: NGS1042/benchmarks/NGS1042_viral_reference_bwa_map.benchmark.tsv
    wildcards: sn=NGS1042
    threads: 2

(bwa mem -t 2 NGS1042/core/viral_reference NGS1042/adapter_trimmed/NGS1042_R1_val_1_posttrim_filter.fq.gz NGS1042/adapter_trimmed/NGS1042_R2_val_2_posttrim_filter.fq.gz | samtools view -bS | samtools sort -@2 -o NGS1042/core/NGS1042_viral_reference.bam) 2> NGS1042/core/NGS1042_viral_reference_bwa.log

[Thu Jan 28 22:43:29 2021]
rule run_kraken2:
    input: NGS1042/adapter_trimmed/NGS1042_R1_val_1_posttrim_filter.fq.gz, NGS1042/adapter_trimmed/NGS1042_R2_val_2_posttrim_filter.fq.gz
    output: NGS1042/kraken2/NGS1042_kraken2.out
    log: NGS1042/kraken2/NGS1042_kraken2.log
    jobid: 151
    benchmark: NGS1042/benchmarks/NGS1042_run_kraken2.benchmark.tsv
    wildcards: sn=NGS1042

cd NGS1042/kraken2 && kraken2 --db /home/maria/covid_analysis_pavlos/covid-19-signal/data/Kraken2/db --threads 1 --quick --unclassified-out "NGS1042_kraken2_unclassified_reads#" --classified-out "NGS1042_kraken2_classified_reads#" --output NGS1042_kraken2.out --paired --gzip-compressed ../../NGS1042/adapter_trimmed/NGS1042_R1_val_1_posttrim_filter.fq.gz ../../NGS1042/adapter_trimmed/NGS1042_R2_val_2_posttrim_filter.fq.gz --report NGS1042_kraken2.report 2>../../NGS1042/kraken2/NGS1042_kraken2.log
Activating conda environment: /home/maria/SNAKE_COVID/conda/3850436d
Activating conda environment: /home/maria/SNAKE_COVID/conda/b95377fd
[Thu Jan 28 22:46:45 2021]
Finished job 151.
147 of 164 steps (90%) done
[Thu Jan 28 22:49:47 2021]
Finished job 92.
148 of 164 steps (90%) done
Select jobs to execute...

[Thu Jan 28 22:49:47 2021]
rule run_bed_primer_trim:
    input: NGS1042/core/NGS1042_viral_reference.bam
    output: NGS1042/core/NGS1042_viral_reference.mapping.primertrimmed.sorted.bam, NGS1042/core/NGS1042_viral_reference.mapping.primertrimmed.bam, NGS1042/core/NGS1042_viral_reference.mapping.bam
    log: NGS1042/core/NGS1042_ivar_trim.log
    jobid: 91
    benchmark: NGS1042/benchmarks/NGS1042_bed_primer_trim.benchmark.tsv
    wildcards: sn=NGS1042

samtools view -F4 -o NGS1042/core/NGS1042_viral_reference.mapping.bam NGS1042/core/NGS1042_viral_reference.bam; samtools index NGS1042/core/NGS1042_viral_reference.mapping.bam; ivar trim -e -i NGS1042/core/NGS1042_viral_reference.mapping.bam -b /home/maria/covid_analysis_pavlos/covid-19-signal/resources/SARSCoV2.paragon.bed -m 20 -q 20 -p NGS1042/core/NGS1042_viral_reference.mapping.primertrimmed 2> NGS1042/core/NGS1042_ivar_trim.log; samtools sort -o NGS1042/core/NGS1042_viral_reference.mapping.primertrimmed.sorted.bam NGS1042/core/NGS1042_viral_reference.mapping.primertrimmed.bam
Activating conda environment: /home/maria/SNAKE_COVID/conda/5258de7f
[Thu Jan 28 23:14:30 2021]
Finished job 91.
149 of 164 steps (91%) done
Select jobs to execute...

[Thu Jan 28 23:14:30 2021]
rule coverage_depth:
    input: NGS1042/core/NGS1042_viral_reference.mapping.primertrimmed.sorted.bam
    output: NGS1042/coverage/NGS1042_depth.txt
    jobid: 133
    benchmark: NGS1042/benchmarks/NGS1042_coverage_depth.benchmark.tsv
    wildcards: sn=NGS1042

bedtools genomecov -d -ibam NGS1042/core/NGS1042_viral_reference.mapping.primertrimmed.sorted.bam >NGS1042/coverage/NGS1042_depth.txt

[Thu Jan 28 23:14:30 2021]
rule get_mapping_reads:
    input: NGS1042/core/NGS1042_viral_reference.mapping.primertrimmed.bam
    output: NGS1042/mapped_clean_reads/NGS1042_R1.fastq.gz, NGS1042/mapped_clean_reads/NGS1042_R2.fastq.gz, NGS1042/mapped_clean_reads/NGS1042_singletons.fastq.gz, NGS1042/mapped_clean_reads/NGS1042_sorted_clean.bam
    log: NGS1042/mapped_clean_reads/NGS1042_samtools_fastq.log
    jobid: 90
    benchmark: NGS1042/benchmarks/NGS1042_get_mapping_reads.benchmark.tsv
    wildcards: sn=NGS1042
    priority: 2


        samtools sort -n NGS1042/core/NGS1042_viral_reference.mapping.primertrimmed.bam -o NGS1042/mapped_clean_reads/NGS1042_sorted_clean.bam 2> NGS1042/mapped_clean_reads/NGS1042_samtools_fastq.log
        samtools fastq -1 NGS1042/mapped_clean_reads/NGS1042_R1.fastq.gz -2 NGS1042/mapped_clean_reads/NGS1042_R2.fastq.gz -s NGS1042/mapped_clean_reads/NGS1042_singletons.fastq.gz NGS1042/mapped_clean_reads/NGS1042_sorted_clean.bam 2>> NGS1042/mapped_clean_reads/NGS1042_samtools_fastq.log 
        

[Thu Jan 28 23:14:30 2021]
rule run_ivar_variants:
    input: /home/maria/covid_analysis_pavlos/covid-19-signal/data/MN908947.3.fasta, /home/maria/covid_analysis_pavlos/covid-19-signal/data/MN908947.3.fasta.fai, NGS1042/core/NGS1042_viral_reference.mapping.primertrimmed.sorted.bam, /home/maria/covid_analysis_pavlos/covid-19-signal/data/MN908947.3.gff3
    output: NGS1042/core/NGS1042_ivar_variants.tsv
    log: NGS1042/core/NGS1042_ivar_variants.log
    jobid: 124
    benchmark: NGS1042/benchmarks/NGS1042_ivar_variants.benchmark.tsv
    wildcards: sn=NGS1042

(samtools mpileup -aa -A -d 0 --reference /home/maria/covid_analysis_pavlos/covid-19-signal/data/MN908947.3.fasta -B -Q 0 NGS1042/core/NGS1042_viral_reference.mapping.primertrimmed.sorted.bam | ivar variants -r /home/maria/covid_analysis_pavlos/covid-19-signal/data/MN908947.3.fasta -m 10 -p NGS1042/core/NGS1042_ivar_variants -q 20 -t 0.25 -g /home/maria/covid_analysis_pavlos/covid-19-signal/data/MN908947.3.gff3) 2> NGS1042/core/NGS1042_ivar_variants.log

[Thu Jan 28 23:14:30 2021]
rule run_ivar_consensus:
    input: NGS1042/core/NGS1042_viral_reference.mapping.primertrimmed.sorted.bam
    output: NGS1042/core/NGS1042.consensus.fa
    log: NGS1042/core/NGS1042_ivar_consensus.log
    jobid: 114
    benchmark: NGS1042/benchmarks/NGS1042_ivar_consensus.benchmark.tsv
    wildcards: sn=NGS1042

(samtools mpileup -aa -A -d 100000 -Q0 NGS1042/core/NGS1042_viral_reference.mapping.primertrimmed.sorted.bam | ivar consensus -t 0.75 -m 10 -n N -p NGS1042/core/NGS1042.consensus) 2>NGS1042/core/NGS1042_ivar_consensus.log
Activating conda environment: /home/maria/SNAKE_COVID/conda/3850436d
Activating conda environment: /home/maria/SNAKE_COVID/conda/3850436d
Activating conda environment: /home/maria/SNAKE_COVID/conda/5258de7f
Activating conda environment: /home/maria/SNAKE_COVID/conda/5258de7f
[Thu Jan 28 23:15:38 2021]
Finished job 133.
150 of 164 steps (91%) done
Select jobs to execute...

[Thu Jan 28 23:15:38 2021]
rule generate_coverage_plot:
    input: NGS1042/coverage/NGS1042_depth.txt
    output: NGS1042/coverage/NGS1042_coverage_plot.png
    jobid: 142
    wildcards: sn=NGS1042

/home/maria/covid_analysis_pavlos/covid-19-signal/scripts/generate_coverage_plot.py NGS1042/coverage/NGS1042_depth.txt NGS1042/coverage/NGS1042_coverage_plot.png
Activating conda environment: /home/maria/SNAKE_COVID/conda/4bc6b9de
[Thu Jan 28 23:15:46 2021]
Finished job 142.
151 of 164 steps (92%) done
[Thu Jan 28 23:19:16 2021]
Finished job 114.
152 of 164 steps (93%) done
Select jobs to execute...

[Thu Jan 28 23:19:16 2021]
rule run_quast:
    input: NGS1042/core/NGS1042.consensus.fa
    output: NGS1042/quast/NGS1042_quast_report.html
    log: NGS1042/quast/NGS1042_quast.log
    jobid: 160
    benchmark: NGS1042/benchmarks/NGS1042_run_quast.benchmark.tsv
    wildcards: sn=NGS1042

quast NGS1042/core/NGS1042.consensus.fa -r /home/maria/covid_analysis_pavlos/covid-19-signal/data/MN908947.3.fasta -g /home/maria/covid_analysis_pavlos/covid-19-signal/data/MN908947.3.gff3 --output-dir NGS1042/quast --threads 1 >NGS1042/quast/NGS1042_quast.log && for f in NGS1042/quast/report.*; do mv $f ${f/report/NGS1042_quast_report}; done
Activating conda environment: /home/maria/SNAKE_COVID/conda/2d0610a0
[Thu Jan 28 23:19:21 2021]
Finished job 160.
153 of 164 steps (93%) done
[Thu Jan 28 23:20:07 2021]
Finished job 124.
154 of 164 steps (94%) done
[Thu Jan 28 23:20:30 2021]
Finished job 90.
155 of 164 steps (95%) done
Select jobs to execute...

[Thu Jan 28 23:20:30 2021]
rule run_fastqc_on_mapped_reads:
    input: NGS1042/mapped_clean_reads/NGS1042_R1.fastq.gz, NGS1042/mapped_clean_reads/NGS1042_R2.fastq.gz
    output: NGS1042/mapped_clean_reads/NGS1042_R1_fastqc.html, NGS1042/mapped_clean_reads/NGS1042_R2_fastqc.html
    log: NGS1042/mapped_clean_reads/NGS1042_fastqc.log
    jobid: 89
    benchmark: NGS1042/benchmarks/NGS1042_clean_fastqc.benchmark.tsv
    wildcards: sn=NGS1042


        fastqc -o NGS1042/mapped_clean_reads NGS1042/mapped_clean_reads/NGS1042_R1.fastq.gz NGS1042/mapped_clean_reads/NGS1042_R2.fastq.gz 2> NGS1042/mapped_clean_reads/NGS1042_fastqc.log
        
Activating conda environment: /home/maria/SNAKE_COVID/conda/b95377fd
[Thu Jan 28 23:22:00 2021]
Finished job 89.
156 of 164 steps (95%) done
Exiting because a job execution failed. Look above for error message
Complete log: /home/maria/covid_analysis_pavlos/covid-19-signal/.snakemake/log/2021-01-28T194932.692546.snakemake.log

```

   

#### Within patients variability

The within-patient-variability was estimated by the typical process of mapping short-read to the reference genome and following the **SIGNAL** pipeline.  For the Greek samples used in the analysis, we follow the exact SIGNAL pipeline to identify as accurately as possible the mutations present in the samples as well as their frequency. For the Brazilian samples we followed a simpler pipeline, in which only mapping (bwa) and `samtools mpileup` was used, since we were interested only in the bases that are mapped at certain locations.  

#### Between patients divergence
The between-patient-variability was measured by data from the *GISAID* website. We used the 0312 version (i.e. March 12th, 2021). 

