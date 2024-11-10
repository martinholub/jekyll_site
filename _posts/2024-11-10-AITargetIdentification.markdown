---
layout: post
title: Accelerating Drug Discovery - The Role of AI in Uncovering New Targets 
date: 2024-11-10 16:22
tags: biotech science
categories: 
description: |
     In this article, we highlight the role of AI in a critical task in the early drug discovery process-target identification. We first introduce the technical background. Next, we review the state-of-the-art using industry examples. Finally, we highlight challenges and directions for future development. Questions we address are a) How is AI currently used in target identification?, and b) What future developments of AI would position it to make the largest positive impact on this task? 
---

<i>This article was co-authored by [Kevin Merchant](https://www.linkedin.com/in/merchantkevinwb/) and [Martin Holub](https://www.martinholub.com/).</i>

## Introduction

Development of novel drugs has been a critical contributor to extending healthspan and fighting diseases, but the process is complex. The involvement of multiple stakeholders and strict regulatory processes are responsible for some of it, but that contribution is dwarfed by our limited understanding of underlying biological processes. Over the past decade, artificial intelligence (AI) has progressed rapidly showing reasoning ability over large multidimensional datasets. AI, indeed, is transforming the drug discovery process as well.

In this article, we highlight the role of AI in a critical task in the early drug discovery process: target identification. We first introduce the technical background. Next, we review the state-of-the-art using industry examples. Finally, we highlight challenges and directions for future development. Questions we address are: **How is AI currently used in target identification?** And: **What future developments of AI would position it to make the largest positive impact on this task?** 

## Understanding Target Identification

Drug development is a long and complex process, with average estimates of around 12 years from conceptualization to approval — although post-COVID-19, [efforts have been made by approval bodies to shorten it](https://doi.org/10.1016/S0140-6736(22)01276-4) [1]. This is happening through a number of approaches, including [accelerated approval pathways](https://doi.org/10.1111%2Fcts.12745) [2], leveraging [real world data and evidence](https://www.statnews.com/2022/08/10/real-world-data-expedite-drug-approval-process/) as well as [changes to clinical trial design](https://www.fda.gov/regulatory-information/search-fda-guidance-documents/master-protocols-efficient-clinical-trial-design-strategies-expedite-development-oncology-drugs-and) [3]. Lead discovery is the first step, including target identification & screening for compounds or biologics against the target, followed by optimization of lead compound and preclinical testing. If the lead compound manages to get through these hoops, it can finally go into clinical trials, where success can pave the way for approval and the title “drug”. 

Target identification is an inherent part of academic and industry research. Traditionally, it describes the process of identifying proteins and their roles in specific disease conditions through different experimental methods (Fig.1). A common pipeline is discovering and knocking out the gene coding for the protein of interest and studying the effects on a disease model. Recently, a number of different target types have emerged. Coding and regulatory nucleic acids, both DNA and RNA, different metabolites, and even whole cell types (in the context of cell therapy) all represent potential targets for a drug candidate. 

With the arrival of methods like [RNA interference](https://journals.asm.org/doi/full/10.1128/mmbr.67.4.657-685.2003) [4] (see also [my post on RNAi](https://www.martinholub.com/2024/10/16/RNAi.html)), or more recently [CRISPR-based tools](https://royalsocietypublishing.org/doi/full/10.1098/rstb.2015.0496) [5], large-scale screens for experimental target identification have become common in well-resourced labs. Using these methods, a range of genes in disease-model cell lines can be knocked out. Subsequent phenotypic and/or genotypic assaying allows the identification of new possible drug target candidates (Fig.1).

<div class="img_row"> 
<img class="col three" src="{{ site.baseurl }}/img/techbio_targetIdentification.png" alt="" title="Header"/> 
</div> 
<div class="col three caption">Fig.1: Overview of target identification approaches. <a href="https://doi.org/10.1016/j.tips.2023.06.010">Adapted from Pun et al., 2023</a>. </div>

These experimental approaches widen our horizons by characterizing proteins whose functions were not previously known. Most commonly, this knowledge ends up accessible on the internet — through publications — and can be leveraged. Considerable efforts have been made to develop and maintain massive databases containing information on genes, their corresponding proteins, and their function. All of this plays a crucial role in the usage of sequencing technologies, which involve using these databases at some point in their downstream analysis.

In the last decade, with the increased abundance of genomic data, genome-wide association studies (GWAS) have gained a lot of traction. Using GWAS, the genetic makeup of patients suffering from certain ailments can be compared to healthy individuals to identify targets specific to disease pathologies. Similarly, the availability of other omics datasets (transcriptomic, proteomic, epigenomic, metabolomic, etc.) (Fig.1) in the public domain has exponentially increased due to advancements in technologies and lower costs of the corresponding experiments. Consequently, while requiring bioinformatics expertise, leveraging publicly and commercially available multiomics datasets _in silico_ has become a go-to strategy for identifying promising targets before testing them in the lab.

## Understanding AI in Target Identification

With the plethora of data and the rapid advances in computer hardware, today there is no domain of biomedical research where AI doesn’t contribute – from information retrieval to clinical diagnoses, and from data processing & integration to protein modeling ([AlphaFold](https://alphafold.ebi.ac.uk/about)). AI is an umbrella term that has been used to denote traditional mathematical models such as regression, to abstract phenomena like artificial general intelligence (AGI). The use cases of AI discussed in this article are in between these two extremes. In the following text, we briefly introduce AI as it is being used in target discovery.

Artificial intelligence, or AI, refers to a computer’s ability to perform tasks that are characteristic of intelligent beings. What these algorithms attempt to do is _learn_ trends from swathes of data, and apply what they _learned_ to new, unseen data. For example, an accurate skin cancer detection model has to be fed thousands of images of skin cancer and benign tumors, so that it can _learn_ to discriminate between the two. Similarly, large language models (LLMs) like [ChatGPT](https://chat.openai.com/) or [Claude](https://www.anthropic.com/claude) are trained on books, articles, and pretty much every text available on the internet in the public domain, which makes them robust in answering a broad range of questions. On the other hand, specialist models like [BioMedBERT](https://github.com/BioMedBERT/biomedbert) or [Perplexity AI](https://www.perplexity.ai/hub/about), are geared towards scientific conversations and provide resources and citations.  All these models are examples of deep learning.

Deep learning is a vast subfield of AI that makes use of neural networks. Neurons form the fundamental unit of these networks and are similar to biological neurons: receiving multiple signals from surrounding neurons, processing them in a certain way, and having a single output that is then sent to another neuron. Using multiple layers of such neurons leads to neural networks that come in all [shapes and sizes](https://www.asimovinstitute.org/neural-network-zoo/) and varying complexities.

The deep learning models’ ability to learn & generalize makes them extremely versatile in biomedical research. Companies discussed below are using different variations of deep learning to integrate publicly available and self-generated multi-omics datasets along with other types of data like microscopy images, text from biomedical literature, and patient data to capture intricacies and trends that are difficult to detect manually. By training such models biomarkers, perturbation effects, and novel targets can be predicted _in silico_ and subsequently validated through experimentation. Hence, biomedical data in every available form is being leveraged with complex, computation-heavy, and often proprietary AI architectures for identifying new targets against diseases. 

## Case Studies and Real-world Examples


At the moment of writing, there are [over 20 assets](https://doi.org/10.1016/j.tips.2023.06.010) in clinical trials where AI was leveraged for target identification, as well as along the downstream drug development process [6]. A number of them are already in phase II, and many more are in the Investigational New Drug (IND) enabling phase. 


[Recursion Pharmaceuticals](https://www.recursion.com/) is a pioneer in data-driven, platform-first biotech (known as [TechBio](https://medium.com/cantos-ventures/what-is-techbio-ef01cd61834d)). Since its founding in 2013, the company built up the capacity to run over 2 million experiments every week and collected over 22 PB (that’s 10<sup>15</sup>) of data. Their pipeline generates lead candidates by applying reverse-genetic causal machine learning models on patient-specific sequencing data and integrating it with health records, databases on small molecule compounds, their target interaction predictions, and data from scientific publications. To facilitate this workflow, the company developed LOWE (Large Language Model-Orchestrated Workflow Engine) that allows users to interface with the pipeline with natural language.


The lead molecules are screened in imaging-based and sc-RNA sequencing workflows, generating genome-wide perturbation datasets that are fed into deep learning models.  Recursion differentiates itself from its competition by being an early and bullish adopter of image-based data collection (phenomics). While [a fraction of the generated dataset has been made public](https://www.rxrx.ai/rxrx3#about) [7], much of it remains proprietary to Recursion. Their phenomics foundation model (trained on the publicly available data) [Phenome-Beta](https://www.recursion.com/news/nothing-short-of-phenomenal-new-deep-learning-model-available-on-nvidias-bionemo-platform) was released on NVIDIA’s [BioNeMo platform](https://www.nvidia.com/en-us/clara/bionemo/) earlier this year. Recursion’s most advanced model, Phenome-1 remains proprietary. 

<div class="img_row"> 
<img class="col three" src="{{ site.baseurl }}/img/techbio_recursionPhenomics.png" alt="" title="Header"/> 
</div> 
<div class="col three caption">Fig.2: Overview of ‘phenomics’ for high-throughput screening. Top panel: Cell images are collected at different perturbations (middle) and across multiple color channels (right). Adapted from <a href="https://fintel.io/doc/sec-recursion-pharmaceuticals-inc-1601830-10k-2023-february-27-19415-6506">Recursion’s 2023 annual report</a>. Bottom panel: Multi-channel images are the training data for a deep learning model that learns their experimentally relevant features. The model can be used for future inference. Adapted from <a href="https://www.rxrx.ai/rxrx3">rxrx.ai</a>.</div>

Recursion currently has [five small molecule drugs in phase II trials](https://clinicaltrials.gov/search?spons=Recursion%20Pharmaceuticals%20Inc.). [REC-4881](https://ir.recursion.com/news-releases/news-release-details/recursion-initiates-two-additional-clinical-trials-total-four) is an orally bioavailable, non-ATP-competitive allosteric small molecule inhibitor of [MAP2K1](https://en.wikipedia.org/wiki/MAP2K1)/[2](https://en.wikipedia.org/wiki/MAP2K2) being developed to reduce polyp burden and cancer progression in people living with FAP (familial adenomatous polyposis). FAP is an inherited disease that leads to formation of polyps in the rectum and colon, eventually manifesting in colorectal cancer (CRC). [REC-3964](https://ir.recursion.com/news-releases/news-release-details/recursion-announces-completion-phase-1-study-rec-3964) is a non-antibiotic small molecule inhibitor of C.difficile toxins which is being developed for the potential treatment of gastrointestinal infection. It finished phase I in 2023, and started enrollment for phase II in October 2024. Most recently [REC-1245](https://ichgcp.net/clinical-trials-registry/NCT06678659) entered phase I/II clinical trials for advanced metastatic tumors


[InSilico Medicine](https://insilico.com/) is another early adopter of AI in small molecule drug discovery and design. The company leverages its end-to-end integrated Pharma.AI platform consisting of three components to drive its drug discovery and development: [PandaOmics](https://pubs.acs.org/doi/full/10.1021/acs.jcim.3c01619), [Chemistry42](https://pubs.acs.org/doi/full/10.1021/acs.jcim.2c01191) and [inClinico](https://ascpt.onlinelibrary.wiley.com/doi/full/10.1002/cpt.3008) [8-10]. PandaOmics is an AI target identification engine that combines a diverse range of omics data totalling over 10<sup>12</sup> data points across disease-specific and healthy tissue datasets. The platform further integrates text-based analysis on clinical trials, grants and publications, all together allowing for identification of novel targets that meet a large need. “Our target discovery philosophy is to find an optimal balance between commercial tractability, novelty, and confidence,” [said](https://www.drugdiscoverytrends.com/insilico-ai-cancer-treatment-ism9274/?utm_source=TrendMD&utm_medium=cpc&utm_campaign=Drug_Discovery_and_Development__TrendMD_0) Alex Zhavoronkov, founder and CEO of Insilico Medicine for Drug Discovery & Development.


The company currently has one asset in a phase II trial, [four more in phase I](https://clinicaltrials.gov/search?spons=InSilico%20Medicine%20Hong%20Kong%20Limited), and one preclinical asset. [INS018_055](https://www.nature.com/articles/s41587-024-02143-0) is an orally available small molecule TRAF2- and NCK-interacting kinase (TNIK) inhibitor with therapeutic potential in idiopathic pulmonary fibrosis currently in phase II trials [11]. [ISM3091/XL309](https://www.businesswire.com/news/home/20230912041846/en/Exelixis-and-Insilico-Medicine-Enter-into-Exclusive-Global-License-Agreement-for-ISM3091-a-Potentially-Best-in-Class-USP1-Inhibitor) is a small molecule inhibitor of USP1, an enzyme implicated in DNA damage repair and relevant in the context of some forms of ovarian, prostate, and breast cancers, [ISM5411](https://www.drugdiscoverytrends.com/insilico-medicines-latest-ai-engineered-drug-ism5411-could-provide-a-novel-approach-for-treating-ibd/) is an oral prolyl hydroxylase domain (PHD) inhibitor for the treatment of inflammatory bowel disease (IBD), this investigational drug is supposed to regulate levels of hypoxia-inducible factor 1alpha (HIF-1a), which should in turn control gut inflammation. Finally, the firm has a CDK12/13 inhibitor, [ISM9274](https://www.drugdiscoverytrends.com/insilico-ai-cancer-treatment-ism9274/?utm_source=TrendMD&utm_medium=cpc&utm_campaign=Drug_Discovery_and_Development__TrendMD_0), in the preclinical pipeline that shows promise against multiple cancers, particularly triple-negative breast cancer and pancreatic cancer.


While others focus purely on target-identification (e.g. [Biorelate](https://biorelate.com/company)), most companies integrate AI-driven target identification into a full drug development pipeline (further examples include  [Valo Health](https://www.valohealth.com/), [Relay Therapeutics](https://relaytx.com/), [Exscientia](https://www.exscientia.ai/pipeline) (recently [acquired](https://investors.exscientia.ai/press-releases/press-release-details/2024/Recursion-and-Exscientia-Enter-Definitive-Agreement-to-Create-a-Global-Technology-Enabled-Drug-Discovery-Leader-with-End-to-End-Capabilities/default.aspx) by Recursion), [Nimbus Therapeutics](https://www.nimbustx.com/), and [Benevolent A](https://www.benevolent.com/pipeline/). Finally, [Open Targets](https://www.opentargets.org/) stands out as a notable example of open and collaborative science, bringing multiple industry stakeholders together to share disease and target annotation data in easily accessible format. 


## Future Outlook and Challenges


When applying AI to target discovery, a number of challenges emerge. First, any model is only as good as the data it has been trained on. Failing to collect data in areas of unmet needs or for underserved patient populations is at large risk of leading to biased models that exacerbate health inequality. Second, AI models have only limited transparency, and to an extent function as black boxes. Managing their regulatory compliance and data integrity requires teams to adapt to changing frameworks. Third, training AI models requires substantial computational resources. This presents challenges to equity of access, where well-resourced companies may benefit from preferential access to compute hardware. Finally, a culture of keeping these models, and the data they have been trained on, proprietary is likely to create silos of knowledge and hinder progress.


Despite these challenges, AI has clearly taken a firm hold across the drug development pipeline, including target identification. The increased volume and modality of datasets, together with more computational power and advances in AI architectures, are increasing the rate at which new candidates are discovered and enter clinical trials. In the future, there is a hope that AI will substantially increase the success rate of these trials as well as be helpful in aiding the development of drugs for previously intractable targets. Examples in this article have focused on protein targets and small-molecule drugs. It is likely that AI-driven models optimized for discovery of different targets than proteins will emerge in the near future. Similarly, other modalities than small molecules are poised to gain more prominence. [Peptide-based therapeutics](https://www.nature.com/articles/s41589-023-01524-x) [12], for example, have seen [a number of successes](https://drughunter.com/articles/mk-0616-the-2023-molecule-of-the-year/) in the last year.


The future of AI in drug discovery is bright. If you want to learn more about how AI is revolutionizing biotech and stay up to date, be sure to check [Nucleate’s AI in Biotech](https://linktr.ee/aixbiotech_nucleate) initiative. 


<i>We would like to thank Alice Martin, Natalie Losada, Samantha Avina and Shawn Rumrill for feedback on the draft.</i>

<hr>

## References

\[1\] Hwang, T. J.; Trinh, Q.-D.; Tibau, A.; Vokinger, K. N. Reforms to Accelerated Approval of New Medicines: Long Overdue. *The Lancet* **2022**, *400* (10349), 357--358. <https://doi.org/10.1016/S0140-6736(22)01276-4>.

\[2\] Cox, E. M.; Edmund, A. V.; Kratz, E.; Lockwood, S. H.; Shankar, A. Regulatory Affairs 101: Introduction to Expedited Regulatory Pathways. *Clinical Translational Sci* **2020**, *13* (3), 451--461. <https://doi.org/10.1111/cts.12745>.

\[3\] Master Protocols: Efficient Clinical Trial Design Strategies to Expedite Development of Oncology Drugs and Biologics. *Clinical Trial Design*. <https://www.fda.gov/regulatory-information/search-fda-guidance-documents/master-protocols-efficient-clinical-trial-design-strategies-expedite-development-oncology-drugs-and> 

\[4\] Agrawal, N.; Dasaradhi, P. V. N.; Mohmmed, A.; Malhotra, P.; Bhatnagar, R. K.; Mukherjee, S. K. RNA Interference: Biology, Mechanism, and Applications. *Microbiol Mol Biol Rev* **2003**, *67* (4), 657--685. <https://doi.org/10.1128/MMBR.67.4.657-685.2003>.

\[5\] Hille, F.; Charpentier, E. CRISPR-Cas: Biology, Mechanisms and Relevance. *Phil. Trans. R. Soc. B* **2016**, *371* (1707), 20150496. <https://doi.org/10.1098/rstb.2015.0496>.

\[6\] Pun, F. W.; Ozerov, I. V.; Zhavoronkov, A. AI-Powered Therapeutic Target Discovery. *Trends in Pharmacological Sciences* **2023**, *44* (9), 561--572. <https://doi.org/10.1016/j.tips.2023.06.010>.

\[7\] Fay, M. M.; Kraus, O.; Victors, M.; Arumugam, L.; Vuggumudi, K.; Urbanik, J.; Hansen, K.; Celik, S.; Cernek, N.; Jagannathan, G.; Christensen, J.; Earnshaw, B. A.; Haque, I. S.; Mabey, B. RxRx3: Phenomics Map of Biology. February 8, 2023. <https://doi.org/10.1101/2023.02.07.527350>.

\[8\] Kamya, P.; Ozerov, I. V.; Pun, F. W.; Tretina, K.; Fokina, T.; Chen, S.; Naumov, V.; Long, X.; Lin, S.; Korzinkin, M.; Polykovskiy, D.; Aliper, A.; Ren, F.; Zhavoronkov, A. PandaOmics: An AI-Driven Platform for Therapeutic Target and Biomarker Discovery. *J. Chem. Inf. Model.* **2024**, *64* (10), 3961--3969. <https://doi.org/10.1021/acs.jcim.3c01619>.

\[9\] Ivanenkov, Y. A.; Polykovskiy, D.; Bezrukov, D.; Zagribelnyy, B.; Aladinskiy, V.; Kamya, P.; Aliper, A.; Ren, F.; Zhavoronkov, A. Chemistry42: An AI-Driven Platform for Molecular Design and Optimization. *J. Chem. Inf. Model.* **2023**, *63* (3), 695--701. <https://doi.org/10.1021/acs.jcim.2c01191>.

\[10\] Aliper, A.; Kudrin, R.; Polykovskiy, D.; Kamya, P.; Tutubalina, E.; Chen, S.; Ren, F.; Zhavoronkov, A. Prediction of Clinical Trials Outcomes Based on Target Choice and Clinical Trial Design with Multi‐Modal Artificial Intelligence. *Clin Pharma and Therapeutics* **2023**, *114* (5), 972--980. <https://doi.org/10.1002/cpt.3008>.

\[11\] Ren, F.; Aliper, A.; Chen, J.; Zhao, H.; Rao, S.; Kuppe, C.; Ozerov, I. V.; Zhang, M.; Witte, K.; Kruse, C.; Aladinskiy, V.; Ivanenkov, Y.; Polykovskiy, D.; Fu, Y.; Babin, E.; Qiao, J.; Liang, X.; Mou, Z.; Wang, H.; Pun, F. W.; Ayuso, P. T.; Veviorskiy, A.; Song, D.; Liu, S.; Zhang, B.; Naumov, V.; Ding, X.; Kukharenko, A.; Izumchenko, E.; Zhavoronkov, A. A Small-Molecule TNIK Inhibitor Targets Fibrosis in Preclinical and Clinical Models. *Nat Biotechnol* **2024**. <https://doi.org/10.1038/s41587-024-02143-0>.

\[12\] Pal, S.; 'T Hart, P. Imbuing Peptide Libraries with Drug-Likeness. *Nat Chem Biol* **2024**. <https://doi.org/10.1038/s41589-023-01524-x>.











 

