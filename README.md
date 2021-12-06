# VaQuERo
SARS-CoV-2 (Va)riant (Qu)antification in s(E)wage, designed for (Ro)bustness

## Synopsis

Takes allele frequencies in table formate and associated meta data and quantifies different virus variants as defined in provided marker mutation file. The workflow first calls 'detected' variants and subsequently quantifies the abundance of the detected variants based on the observed non-zero frequencies using a SIMPLEX regression.

## Input

## allele frequency file

A TAB separated table with columns in four blocks. First block gives the annotatio of the associated mutation (column 1-18). The next block of N columns (with n samples) specify the allele frequencies. Thereby the column header is named SAMPLE:AF. The next block of N columns specify the read depth in each sample for taht mutation. Thereby the column header is named SAMPLE:DP.  The last block of n columns provides the quality value for the mutation calling. Thereby the column header is named SAMPLE:PQ. 

| Col | HEADER               | EXAMPLE VALUE      | DESCRIPTION                  |
| --- |                  --: |  :--               | :--                          |
| $1  |                CHROM |  NC_045512.2       | chromosome name              |
| $2  |                  POS |  3002              | position                     |
| $3  |                  REF |  G                 | reference base               |
| $4  |                  ALT |  T                 | alternative base             |
| $5  |             ANN.GENE |  ORF1ab            | annotation gene              |
| $6  |        ANN.FEATUREID |  pp1ab_GU280_gp01  | annotation ID                |
| $7  |           ANN.EFFECT |  stop_gained       | annotation effect            |
| $8  |               ANN.AA |  p.E913stop        | AA mutation                  |
| $9  |           ANN.GENE.1 |  ORF1ab            | annotation level 2           |
| $10 |      ANN.FEATUREID.1 |  pp1a_ORF1a        | annotation level 2           |
| $11 |             ANN.AA.1 |  p.E913stop        | annotation level 2           |
| $12 |           ANN.GENE.2 |  ORF1ab            | annotation level 3           |
| $13 |      ANN.FEATUREID.2 |  nsp3              | annotation level 3           |
| $14 |             ANN.AA.2 |  p.E95stop         | annotation level 3           |
| $15 |           ANN.GENE.3 |  ""                | annotation level 4           |
| $16 |      ANN.FEATUREID.3 |  ""                | annotation level 4           |
| $17 |             ANN.AA.3 |  ""                | annotation level 4           |
| $18 |                  EFF |  Gag/Tag           | phased mutation              |
| $19 |      SAMPLE_NAME:AF  |  SAMPLE1:AF        | sample name and allele freq  |
| +N  |                      |                    | N more sample and AF thereof |
| $25 |      SAMPLE_NAME:DP  |  SAMPLE1:DP        | sample name and read depth   |
| +N  |                      |                    | N more sample and DP thereof |
| $32 |      SAMPLE_NAME:PQ  |  SAMPLE1:PQ        | sample name and quality      |
| +N  |                      |                    | N more sample and PQ thereof |

## meta data file

The meta data file connects each sample as defined in the mutation file with the sampling location and time.

| Col | HEADER                  |  EXAMPLE VALUE   | DESCRIPTION                 |
| --- |                     --: |  :--             | :--                         |
| $1  |                 BSF_run |  BSF_0895        | Sequencing batch            |
| $2  |         BSF_sample_name |  SAMPLE1         | Seq. sample name            |
| $3  |          BSF_start_date |  2021-01-18      | Seq. date                   |
| $4  |       LocationID_coronA |  ATTP_10-Krezlin | Sample loction ID           |
| $5  |     LocationName_coronA |  Krezlin         | Sample location name        |
| $6  |          N_in_Consensus |  125             | Nr. Of N in consensus seq   |
| $7  |              RNA_ID_int |  SAMPLE1         | Sample name                 |
| $8  |  additional_information |  Ct = xx.2       | any add. info               |
| $9  |             adress_town |  Krezlin         | Sampling Town               |
| $10 |   connected_people_2018 |  1234567         | Nr. of conncected people    |
| $11 |             dcpLatitude |  48.50452605     | latitude                    |
| $12 |            dcpLongitude |  11.70669547     | lingitude                   |
| $13 |       include_in_report |  TRUE            | should be reported (F|T)    |
| $14 |         report_category |  fictional       | included in which report    |
| $15 |             sample_date |  2020-12-20      | sample date                 |
| $16 |                  status |  passed_qc       | status (passed|failed)      |

## marker mutation definition

The marker mutation file links the mutation expected to be seen in a variant (sensitivity) for all variants. Table is comma separated. If one mutation is sensitive for more than one variants, a list of variants (semicolon separated) can be provided in columns 1.


| Col | HEADER         |  EXAMPLE VALUE   | DESCRIPTION                         |
| --- |            --: |  :--             | :--                                 |
| $1  |       Variants |  AV.1;B.1.1.318  | List of Variants (seperated by ";") | 
| $2  |      Chromosom |  NC_045512.2     | Chromosome name                     |
| $3  |        Postion |  21990           | Chromosome position                 |
| $4  |            REF |  TTTA            | Reference base(s)                   |
| $5  |            ALT |  T               | Alternative base(s)                 |
| $6  |           Gene |  S               | Gene                                |
| $7  |  Sensitivities |  1;0.87;0.96     | Sensitivity in each of the variants |
| $8  |             AA |  S:Y144del       | Mutation in AA nomenclature         |
| $9  v            NUC |  TTTA21990T      | Mutation in nucc nomenclature       |



## Output
