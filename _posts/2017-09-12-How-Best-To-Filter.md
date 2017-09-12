---
layout: post
title: How Best To Filter WGS Variant Calls
subtitle: Variant Calling
tags: [Variant Calling, exciting-stuff]
---


It's hard to know what the best approach is for filtering variant calls from WGS data, but I think that the approach should reflect the underlying goal. For association/enrichment, genotyping, and database building it makes sense to have a clean set of variants to work with, and strict cutoffs can be enforced that may remove some of the more difficult-to-identify variants.  These filters can be set based on inherent quality characteristics of the variants and applied by BCFtools, VCFtools, VT, and GATK (to name a few). Complex regions of the genome can be avoided and filtered, and there may be some true genomic variants lost along the way...but no sweat.

However, in the field of rare genetic disorder diagnosis, maybe there's an equally viable approach to variant calling that leverages one key characteristic of the goal: rarity.  Now rarity, depending on where you decide to set your threshold...let's say for arguments sake allele frequency (AF) < 1%...is generally applied within the observable variants called with high confidence and present in databases (e.g. gnomAD, dbSNP).  But many groups have argued that in-house databases, where variants are deposited pre-filtration, will populate with the recurrent low-quality artifacts that quite often pass through the gnomAD AF < 1% filter. These variants are important to remove, because from an AF standpoint, they seem to be exeedingly rare or novel, and yet in the end they are called in numerous samples with low quality.  

Is it possible that with a lack of hard filtering or a VQSR-framework where true variants are known to be lost*, that a well-populated database of artifacts, specific to your analysis pipeline, can perform on the level or *better* than standard variant filtration techniques? It's tough to quantify something like this, but one possible medium is to compare the set of variants that end up on a candidate list for causing the rare genetic disorder in question.  

*Need to quantify this

