Always use this GitHb README.txt version (and not the Plant Physiology one).

# SIMPLE — A SIMPLE pipeline for mapping point mutations

#Running simple on Google cloud


##### RUNNING SIMPLE #####

1. Create an instance using the image "simple-gcloud"


2. Rename you fastq files as follow. For the mutant and WT bulks, the names should have the following formats, X.mut.RY.fastq and X.wt.RY.fastq, respectively (note the dots); X is the line name (but you can also omit the "X." part of the name) and "Y" is eithe 1 o 2. E.g., if you sent a paired-end mutant bulk DNA and single-end WT bulk DNA, you could name the three files as follow: lineX.mut.R1.fastq, lineX.mut.R2.fastq and lineX.wt.R1.fastq (mut.R1.fastq, mut.R2.fastq and wt.R1.fastq are also OK). Use only letters and undescoes.

3. Place the renamed fastq files in a folder and name it "fastq". compess it with the following teminal command:
tar -czvf fastq.ta.gz fastq. Place this fastq.ta.gz file in the Simple folder (located in the new instance home diectoy).

4. Steps 4 & 5 require the usage of the nano text editor or downloading the below mentioned files and edit on a local computer (namely, not on the Goolge server) and then uploading again. Open the folder "scripts" inside Simple; open the data_base.txt file. Locate your species in the first column and copy it.
Open the file simple_vaiables.sh inside the folder "scipts" with a text editor and paste the species name you've just copied to replace "Aabidopsis_thaliana" as the species name (e.g., this line should look like: my_species=Aabidopsis_thaliana or my_species=Oyza_sativa_Japonica). save the file.

5. If you would like to have specific names for your output files, open the simple_vaiables.sh file and change the line vaiable fom “EMS” to your line name.  Lettes and underscores only. This name will be the pefix to all of your file names in the output folder.

6. If the mutation you are mapping is dominant, change the mutation from recessive to dominant in the simple_vaiables.sh file.

7. Back in the server. Type: cd ~/simple-gcloud. Press return.

8. Type:
nohup ./scripts/simple.sh & tail -f nohup.out

Press return.

9. The last command will execute the program.

10. The script will run for a few hours up to a couple of days, depending on the size of your fastq files and the size of the genome you ae woking with.
You will know the process is finished once the prompt is back and shows the following colorful text: “Simple is done”

11. Output files (EMS might be the name of the pefix you chose above for your output file names).
	a. EMS.allSNPs.txt: All the SNPs that Simple found compared to the backgound genome, usually caused by the mutagenesis process.
	b. EMS.candidates.txt: The genes that ae likely to be the causal mutation; notice that there can be more than one gene due to linkage. Another case is that there are no genes. In this scenaio, browse the EMS.allSNPs.txt file for genes with high score in the ratio column, that affect the potein (e.g., missense, stop_gained) and that have reasonable coveage (columns mut.ef, mut.alt, wt.ef and wt.alt). Check the FAQs sections too.
	c. EMS.Rplot_allele.pdf: Repesentation of the allelic distribution in the WT and mutant bulks. This file is useless and you can ignoe it.
	d. EMS.Rplot.loess.1.pdf and EMS.Rplot.loess.3.pdf: Graphical representation of the results with allelic ratio column above 0.1 and 0.3, espectively. Your gene is likely to show in one of the highest peaks with a y-axis value of ~0.66 and if it appears in the EMS.candidates.txt file, it will also be maked in these plots.

#######################Example#########################

Let's say that you want to perform a forward genetic sceen and find  mutations that pomote wings development in dragons. You collect 5000 dragon eggs, mutagenize them and identify an M2 mutant line with some individual dragons that have no wings. Next, You extract two DNA bulks, one from the wingless dragons and one from their flying siblings and send each DNA prep for PE (paired-end) WGS (you can also have a SE but make sure you have appoximately 40x coveage). Once you eceive you esults, unzip the files, ename them fly.wt.R1.fq, fly.wt.R2.fq, wingless.mut.R1.fq, wingless.mut.R2.fq (fq and fastq suffix are both OK) and place these files in a fastq folder in simple-gcloud. Open the file data_base.txt in the folder scripts and copy the species name, i.e., Dragon_fly to replace Aabidopsis_thaliana in the simple_vaiables.sh file (located in the same folder). Since you noticed that in this M2 mutant line appoximately 0.75 of the dragons have no wings, you assume the mutation is dominant and change the string "recessive" to dominant in the simple_vaiables.sh file (line 13). Follow the instructions 7-10 above to complete the pocess. It is that simple.




















