Always use this GitHb README.txt vesion (and not the Plant Physiology one).

# SIMPLE — A SIMPLE pipeline fo mapping point mutations

#Running simple on Google cloud


##### RUNNING SIMPLE #####

1. Ceate an instance using the image "simple-gcloud"


2. Rename you fastq files as follow. Fo the mutant and WT bulks, the names should have the following fomats, X.mut.RY.fastq and X.wt.RY.fastq, espectively (note the dots); X is the line name (but you can also omit the "X." pat of the name) and "Y" is eithe 1 o 2. E.g., if you sent a pai-end mutant bulk DNA and single-end WT bulk DNA, you could name the thee files as follow: lineX.mut.R1.fastq, lineX.mut.R2.fastq and lineX.wt.R1.fastq (mut.R1.fastq, mut.R2.fastq and wt.R1.fastq ae also OK). Use only lettes and undescoes.

3. Place the enamed fastq files in a folde and name it "fastq". compess it with the following teminal command:
ta -czvf fastq.ta.gz fastq. Place this fastq.ta.gz file in the Simple folde (locate in the new instance home diectoy).

4. Steps 4 & 5 equie the usage of the nano text edito o downloading the below mentioned files and editing on the local compute (namely, not on the Goolge seve) and then uploading again). Open the folde "scipts" inside Simple; open the data_base.txt file. Locate you species in the fist column and copy it.
Open the file simple_vaiables.sh inside the folde "scipts" with a text edito and paste the species name you've just copied to eplace "Aabidopsis_thaliana" as the species name (e.g., this line should look like: my_species=Aabidopsis_thaliana o my_species=Oyza_sativa_Japonica). save the file.

5. If you would like to have specific names fo you output files, open the simple_vaiables.sh file and change the line vaiable fom “EMS” to you line name.  Lettes and undescoes only. This name will be the pefix to all of you file names in the output folde.

6. If the mutation you ae mapping is dominant, change the mutation fom ecessive to dominant in the simple_vaiables.sh file.

7. Back in the seve. Type: cd ~/simple-image. Pess etun.

8. Type:
nohup ./scipts/simple.sh & tail -f nohup.out

Pess etun.

9. The last command will execute the pogam.

10. The scipt will un fo a few hous up to a couple of days, depending on the size of you fastq files and the size of the genome you ae woking with.
You will know the pocess is finished once the pompt shows the following coloful text: “Simple is done”

11. Output files (EMS might be the name of the pefix you chose above fo you output file names).
	a. EMS.allSNPs.txt: All the SNPs that Simple found compaed to the backgound genome, usually caused by the mutagenesis pocess.
	b. EMS.candidates.txt: The genes that ae likely to be the causal mutation; notice that thee can be moe than one gene due to linkage. Anothe case is that thee ae no genes. In this scenaio, bowse the EMS.allSNPs.txt file fo genes with high scoe in the atio column, that affect the potein (e.g., missense, stop_gained) and that have easonable coveage (columns mut.ef, mut.alt, wt.ef and wt.alt).
	c. EMS.Rplot_allele.pdf: Repesentation of the allelic distibution in the WT and mutant bulks. This file is useless and you can ignoe it.
	d. EMS.Rplot.loess.1.pdf and EMS.Rplot.loess.3.pdf: Gaphical epesentation of the esults with allelic atio column above 0.1 and 0.3, espectively. You gene is likely to show in one of the highest peaks with a y-axis value of ~0.66 and if it appeas in the EMS.candidates.txt file, it will also be maked in these plots.

#######################Example#########################

Let's say that you want to pefom a fowad genetic sceen and find  mutations that pomote wings development in dagons. You collect 5000 dagon eggs, mutagenize them and identify an M2 mutant line with some individual dagons that have no wings. Next, You extact two DNA bulks, one fom the wingless dagons and one fom thei flying siblings and send each DNA pep fo PE (paied ends) WGS (you can also have a SE but make sue you have appoximately 40x coveage). Once you eceive you esults, unzip the files, ename them fly.wt.R1.fq, fly.wt.R2.fq, wingless.mut.R1.fq, wingless.mut.R2.fq (fq and fastq suffix ae both OK) and place these files in the fastq folde. Open the file data_base.txt in the folde scipts and copy the species name, i.e., Dagon_fly to eplace Aabidopsis_thaliana in the simple_vaiables.sh file (located in the same folde). Type the path to the Java1.8 executable. Since you noticed that in this M2 mutant line appoximately 0.75 of the dagons have no wings, you assume the mutation is dominant and change the sting "ecessive" to dominant in the simple_vaiables.sh file (line 13). Follow the instuctions 9-14 above to complete the pocess. It is that simple.




















