# Classification of arginase inhibitors using machine learning

#### Ella Hanzin, Shira Swissa, Abraham O. Samson

#### Bioinformatics Dept. Jerusalem College of Technology, Jerusalem



## Abstract

Arginase is an enzyme that catalyzes the last step of the urea cycle, and converts L-arginine into L-ornithine and urea.  Multiple arginase inhibitors have been identified, of which some reverse Alzheimer’s disease, hypertension, and diabetes. Here, we propose to develop a machine learning program which can classify arginase inhibitors. 
To classify inhibitors, the program uses molecular features, such as the number of C, N, and O atoms, the number of double bonds, and molecular weight. First, we train our program using a dataset of strong, medium, and weak-inhibitors (n=120). Then, we test our program in a similar, yet distinct dataset (n=20). Remarkably, the program successfully classifies arginase inhibitors in 83% of the test database. The success rate is remarkable despite the limited size of the training dataset, and the scarcity of molecular features. 
The program may be used to classify other datasets (e.g. ZINC, drugs@FDA), and to compare AI results with those obtained from molecular docking. Our results pave the way for identification of novel arginase inhibitors that can potentially reverse Alzheimer’s disease, hypertension, and diabetes. 

## Introduction

Arginases (EC 3.5.3.1) are metalloenzymes responsible for the last step of the urea cycle, in which L-arginine is converted into L-ornithine and urea1. In mammals, two highly similar isoforms of the enzyme exist, arginase type I (ARGI) and type II (ARGII)2 and in humans, ARGI and ARGII contain 322 and 354 amino acids respectively, with 59% sequence identity. ARGI is a cytosolic enzyme that is expressed mostly in the liver3 and ARGII is a mitochondrial enzyme that is expressed in the kidneys, prostate, blood vessels, intestines, red blood cells, and immune cells4. Arginase deficiency extends life-span in mice5, with no significant changes in plasma amino acids and ammonia levels6.  Moreover, genetic knock-downs and knock-outs of arginase, in mice and cells, demonstrate countless beneficial effects against aging-associated diseases.  For example, arginase deficiency prevents atherosclerosis7, delays vascular aging8, suppresses insulin resistance9, ameliorates diabetic renal injury10, protects against hypoxia‐induced pulmonary hypertension11, prevents oxidative stress12, and attenuates autoimmune encephalomyelitis13.  Here, we propose a novel therapy for old-age disease, namely arginase inhibition.  

Arginase inhibitors include various D- and L-amino-acid derivatives, polyphenols, purines, pyrimidines, and polyamines (for an excellent review see Pudlo et al.14). Notably, arginase inhibitors, such as L-norvaline, protect mice against age-related diseases, such as Alzheimer’s disease15–20, hypertension21, and diabetes22. Likewise, arginase inhibitors, such as N-hydroxy-nor-L-arginine (nor-NOHA) protects mice against endothelial  dysfunction, hypertension, and diabetes23.  Also arginases inhibitors, such as boronic acid derivatives, 2(S)-Amino-6-boronohexanoic acid (ABH), (2R)-2-Amino-3-(2-boronoethylsulfanyl)propanoic acid (BEC), and nor-NOHA protect against endothelial dysfunction, diabetes, and hypertension24.  Arginase inhibitors are also found among traditional medicinal plants, such as polyphenols, and (−)-epicatechin which reverse endothelial cell aging25.  Arginase inhibitors also include purines and pyrimidines, as well as antiviral drugs.14 

Machine learning programs and virtual screening technologies have become a classical tool in drug discovery, and in the race for novel compounds that target a given protein26. Computational screening approaches have gained general acceptance because, in comparison with high-throughput screening techniques, they are able to reduce both time and cost by limiting the number of compounds that must be experimentally tested27. There are two main approaches for virtual screening: (1) ligand-based and (2) structure-based 28. In the past we have used, the latter approach to identify potential arginase inhibitors using the 3D-structure of arginases. 

Here, we propose to classify arginase inhibitors, using a ligand-based machine learning program. First, we train our program against a dataset of known inhibitors. Then, we test our program in a similar dataset. 

## Methods

### Experimental data. 
All experimental data, related to arginase inhibitor, was compiled from Pudlo et al.14  The experimental dataset included name, dissociation constants (Kd), inhibition constants (Ki), half maximum inhibitory concentration (IC50).  The experimental dataset was divided into a  training dataset, and a test dataset.  

### Test and training dataset.  
The test and training dataset used 120 and 20 known arginase inhibitors, respectively 14.  SMILES codes were added to each arginase inhibitor, and used to derive molecular features. 

### Machine learning algorithm. 
To identify potential arginase inhibitors, we wrote a python program using the decision tree classifier of Sklearn.  Table 1 contains an example program, and includes a training dataset with 3 known inhibitors, with features such as the number of carbons (C), nitrogens (N), oxygens (O), double bonds (=), amines (NH2), hydroxyls (OH), and the molecular weight. For example, the vector [1,2,1,74], corresponds to 1 nitrogen, 2 oxygens, 1 double bond, and 74 kDa.   In this program, the 3 inhibitors are labelled as a strong-inhibitor (“1”), as medium-inhibitor (“2”), and as weak-inhibitor (“3”).   On the last line, the program predicts a new object from the test dataset, and classifies it based on its features, into a strong, medium, or weak-inhibitor.  

### Approximation of Kd, Ki, and IC50. 
The inhibition constant is Ki = [E][I]/[EI], where [E] is the enzyme concentration, [I] is the   inhibitor concentration, and [EI] is their complex concentration. Notably, Ki is a special case of Kd = [A][B]/[AB], where [A] is protein concentration, [B] is ligand concentration, and [AB] is their complex concentration. Thus, Ki and Kd and both equal here.

Arginase inhibitors are mostly competitive, and the half maximum inhibitory concentration IC50 = Ki (1 + Km/[S]), thus IC50 is always larger than Ki (Km is the Michaelis constant, and [S] is the substrate concentration). In most cases,  Km ≥ 1-3mM and [S] ≥ 1-10mM, and thus approximately Ki < IC50 < 3 Ki. As a result, a very coarse approximation is Kd=Ki≈IC50. Therefore, strong, medium, and weak inhibitors were taken as following: (1) Strong-inhibitor Kd=Ki≈IC50 < 1 µM , (2) Medium-inhibitor with 1 µM < Kd=Ki≈IC50 < 1 mM affinity range, and (3) Weak-inhibitors with Kd=Ki≈IC50 > 1 mM. 

## Results

Validation. Table 2 shows the experimental classification of arginase inhibitors, and that predicted by the program, during 10 consecutive runs. On average, the AI program succesfully classifies 83% of the test dataset into strong (1), medium (2), and weak inhibitors (3). The program average classification success of 83% is consistent in 100 consecutive runs.  The classification accuracy of arginase inhibitors is 100%, except in the case of Chloroquine, D-Tryptophane, L-Ornithine, NOHA (3), and NAME (90%) 14.  The classification accuracy of all runs varies between 80% and 85%.  The accuracy is remarkable, considering the small training dataset, and the simple molecular features.  
Molecular features. Notably, the classification is based solely on the number of carbons (C), nitrogens (N), oxygens (O), double bonds (=), amines (NH2), hydroxyls (OH), and the molecular weight.  
Our program is successful despite its immense limitations, such as the small training dataset (n=120), and its poor molecular features.  The molecular features ignore  crucial information like  partial charges )pH 7.4), aromaticity, number of rotatable bond, size of polycyclic ring systems, and other atom types.  In addition, some molecular feature are partially represented only. For example, hydrogen-bond donors and acceptors are limited, and do not include carbonyls, amides, etc. Finally, the molecular features do not contain any information about the relative positions of atoms, or any 3D coordinates.
Our program is successful despite the coarse approximation of Kd and Ki with IC50.  The successful end also justifies the means, particularly in light of the sparse dataset of arginase inhibitors.

Comparison with molecular docking. Preliminary data show that our program is comparable to molecular docking predictions. For example, dihydroergotamine is classified as a potential strong inhibitor of arginase. This agrees with earlier molecular docking results which rank dihydroergotamine among the top arginase inhibitors (unpublished results).


## Discussion. 

Here, we develop an AI program to classify arginase inhibitors based ligand features. First, we train our program against a dataset of known inhibitors (n=120). Then, we test our program in a similar dataset (n=20). Notably, the success rate changes from run to run, and the average success rate is 83%.
The success of the machine learning program strongly depends on the features, and the size of the training dataset. In the future, the molecular features will be fine-tuned to best represent the determinants for inhibition.  Also, the datasets will be fine-tuned to exclude “problematic” experimental values, using different parts of the training dataset as a test dataset, etc. Moreover, the current trinary labels (i.e. strong, medium, and weak-inhibitors), will be expanded to include a wider spectrum of labels (i.e.very-strong, strong, medium, weak, to very weak inhibitors). 
Despite it multiple limitations, the program paves the way for classification of novel potential arginase inhibitors, capable of reversing senility, hypertension, and diabetes.

## Bibliography

1.	Grody, W. W. et al. Differential expression of the two human arginase genes in hyperargininemia. Enzymatic, pathologic, and molecular analysis. Journal of Clinical Investigation 83, 602–609 (1989).
2.	Jenkinson, C. P., Grody, W. W. & Cederbaum, S. D. Comparative properties of arginases. Comparative Biochemistry and Physiology Part B: Biochemistry and Molecular Biology 114, 107–132 (1996).
3.	Ikemoto, M. et al. Expression of human liver arginase in Escherichia coli. Purification and properties of the product. Biochemical Journal 270, 697–703 (1990).
4.	Morris, S. M., Bhamidipati, D. & Kepka-Lenhart, D. Human type II arginase: sequence analysis and tissue-specific expression. Gene 193, 157–161 (1997).
5.	Xiong, Y., Yepuri, G., Montani, J.-P., Ming, X.-F. & Yang, Z. Arginase-II Deficiency Extends Lifespan in Mice. Frontiers in Physiology 8, (2017).
6.	Cederbaum, S. D. et al. Arginases I and II: do their functions overlap? Molecular Genetics and Metabolism 81, 38–44 (2004).
7.	Yepuri, G. et al. Positive crosstalk between arginase-II and S6K1 in vascular endothelial inflammation and aging. Aging Cell 11, 1005–1016 (2012).
8.	Wu, Z. et al. Role of p38 mitogen-activated protein kinase in vascular endothelial aging: Interaction with Arginase-II and S6K1 signaling pathway. Aging 7, 70–81 (2015).
9.	Ming, X. et al. Arginase II Promotes Macrophage Inflammatory Responses Through Mitochondrial Reactive Oxygen Species, Contributing to Insulin Resistance and Atherogenesis. Journal of the American Heart Association 1, (2012).
10.	Morris, S. M. et al. Distinct roles of arginases 1 and 2 in diabetic nephropathy. American Journal of Physiology-Renal Physiology 313, F899–F905 (2017).
11.	Huynh, N. N. et al. Arginase II Knockout Mouse Displays a Hypertensive Phenotype Despite a Decreased Vasoconstrictory Profile. Hypertension 54, 294–301 (2009).
12.	Xiong, Y., Yu, Y., Montani, J., Yang, Z. & Ming, X. Arginase‐II Induces Vascular Smooth Muscle Cell Senescence and Apoptosis Through p66Shc and p53 Independently of Its L‐Arginine Ureahydrolase Activity: Implications for Atherosclerotic Plaque Vulnerability. Journal of the American Heart Association 2, (2013).
13.	Choudry, M. et al. Deficient arginase II expression without alteration in arginase I expression attenuated experimental autoimmune encephalomyelitis in mice. Immunology 155, 85–98 (2018).
14.	Pudlo, M., Demougeot, C. & Girard-Thernier, C. Arginase Inhibitors: A Rational Approach Over One Century. Medicinal Research Reviews 37, (2017).
15.	Polis, B. & Samson, A. O. Role of the metabolism of branched-chain amino acids in the development of Alzheimer’s disease and other metabolic disorders. Neural Regeneration Research 15, (2020).
16.	Polis, B. & Samson, A. O. Arginase as a Potential Target in the Treatment of Alzheimer’s Disease. Advances in Alzheimer’s Disease 07, (2018).
17.	Polis, B., Gurevich, V., Assa, M. & Samson, A. O. Norvaline restores the BBB integrity in a mouse model of alzheimer’s disease. International Journal of Molecular Sciences 20, (2019).
18.	Polis, B., Srikanth, K. D., Elliott, E., Gil-Henn, H. & Samson, A. O. L-Norvaline Reverses Cognitive Decline and Synaptic Loss in a Murine Model of Alzheimer’s Disease. Neurotherapeutics 15, (2018).
19.	Polis, B., Srikanth, K. D., Gurevich, V., Gil-Henn, H. & Samson, A. O. L-Norvaline, a new therapeutic agent against Alzheimer’s disease. Neural Regeneration Research 14, (2019).
20.	Polis, B. et al. Arginase inhibition supports survival and differentiation of neuronal precursors in adult alzheimer’s disease mice. International Journal of Molecular Sciences 21, (2020).
21.	Gilinsky, M. A. et al. Norvaline Reduces Blood Pressure and Induces Diuresis in Rats with Inherited Stress-Induced Arterial Hypertension. BioMed Research International 2020, (2020).
22.	De, A., Singh, M. F., Singh, V., Ram, V. & Bisht, S. Treatment effect of l-Norvaline on the sexual performance of male rats with streptozotocin induced diabetes. European Journal of Pharmacology 771, 247–254 (2016).
23.	Peyton, K. J. et al. Arginase inhibition prevents the development of hypertension and improves insulin resistance in obese rats. Amino Acids 50, 747–754 (2018).
24.	Bagnost, T. et al. Cardiovascular effects of arginase inhibition in spontaneously hypertensive rats with fully developed hypertension. Cardiovascular Research 87, 569–577 (2010).
25.	Garate-Carrillo, A. et al. Arginase inhibition by (−)-Epicatechin reverses endothelial cell aging. European Journal of Pharmacology 885, 173442 (2020).
26.	Shoichet, B. K. Virtual screening of chemical libraries. Nature 432, 862–865 (2004).
27.	Lill, M. Virtual Screening in Drug Design. in 1–12 (2013).
28.	Yu, W. & MacKerell, A. D. Computer-Aided Drug Design Methods. in 85–106 (2017). doi:10.1007/978-1-4939-6634-9_5.
29.	Trott, O. & Olson, A. J. AutoDock Vina: Improving the speed and accuracy of docking with a new scoring function, efficient optimization, and multithreading. Journal of Computational Chemistry NA-NA (2009) doi:10.1002/jcc.21334. 


