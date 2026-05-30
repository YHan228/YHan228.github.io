---
title: 'What Amphibian Data Reveal — and What Data Deficiency Conceals'
date: 2026-03-09
permalink: /posts/2026/03/amphibian-data-deficiency/
tags:
  - Amphibians
  - Conservation
  - Data Science
  - Biostatistics
---

> *This essay was originally published in **AmphiBios**: Han, Y. (2026). What amphibian data reveal — and what data deficiency conceals. **AmphiBios**, 1. [amphibios.app/articles/amphibian-data-deficiency](https://amphibios.app/articles/amphibian-data-deficiency).*

Amphibians are the most threatened vertebrate class on Earth. The second Global Amphibian Assessment found that 40.7% of assessed species are Critically Endangered, Endangered, or Vulnerable, a figure that has worsened since the first assessment two decades ago *(1)*. But this headline conceals a structural gap in the evidence base: 909 of 8,011 assessed species, roughly one in nine, are classified as Data Deficient (DD) by the IUCN *(1, 2)*. There is not enough information to evaluate whether they face extinction. These species are present on the Red List but excluded from the Red List Index (RLI), the primary global barometer used to track progress toward international biodiversity targets. They are, in effect, invisible to the metrics that drive policy.

This invisibility is not random. Howard and Bickford *(3)* noted over a decade ago that DD amphibians are disproportionately tropical and range-restricted, sharing the ecological profile of species already known to be threatened. The broader DD literature has addressed prediction and reassessment-prioritization using machine learning and trait-based approaches *(4, 5)*, but the framework applied here is different.

What enables a different approach is the quality of the global amphibian metadata. The GAA2 *(1)* is one of the most comprehensive species-level threat assessments conducted for any vertebrate class: 8,011 species individually evaluated, with standardized threat and habitat classifications, range polygons, and documented status changes across assessment rounds spanning four decades. GBIF *(6)*, AmphibiaWeb *(7)*, and AmphiBIO *(8)* provide complementary ecological, life-history, and taxonomic coverage at a scale few other taxa can match. Yet standard quantitative methods for handling incomplete data, including missing-data theory, propensity-score matching, and multiple imputation, while routine in biomedical research, have not been applied to this system. This analysis attempts to close that gap.

## The species we know least are likely the ones in most trouble

To build an integrated picture, five global datasets were linked into a single, publicly archived species-level table (Figure 1): the GAA2 (8,011 species) as the taxonomic backbone *(1)*, 9.8 million occurrence records from GBIF *(6)*, taxonomic synonymies from AmphibiaWeb *(7)*, life-history traits from AmphiBIO *(8)*, and the European Red List (ERL) *(9)*. Cross-referencing against AmphibiaWeb identified over 1,100 additional species not yet included in the global assessment, recently described, 75% from tropical countries, and essentially absent from conservation accounting.

<figure style="text-align: center;">
  <img src="/images/amphibian-data/figure1.png" alt="Dataset coverage and assessment breakdown" style="max-width: 100%; width: 700px;">
  <figcaption><em><strong>Figure 1.</strong> Dataset coverage and assessment breakdown against the GAA2 backbone (8,011 species). Grey tiers show the backbone and its key subsets: 2,873 species (35.9%) are threatened (CR + EN + VU) and 909 (11.3%) are Data Deficient. Coloured bars show external dataset coverage: GBIF contributes occurrence records for 86.2% of species, AmphibiaWeb taxonomic cross-references for 97.9%, AmphiBIO traits for 71.2%, and the European Red List covers 93 European species.</em></figcaption>
</figure>

Four predictive models trained on this integrated dataset show strong discrimination between DD and assessed species (area under the receiver operating characteristic curve, AUC = 0.86–0.89). The strongest predictors of DD status (few occurrence records, restricted geographic range, few habitat types) are the same traits that predict threatened status among assessed species (AUC = 0.89). Even when occurrence record count is removed entirely (the most potentially circular predictor), discriminative performance barely changes (AUC = 0.878).

This matters because it allows a principled estimate of how many DD species are likely threatened. In biostatistics, data that are systematically missing, where the probability of being unobserved depends on observable characteristics, are described as “missing at random” (MAR). DD amphibian species fit this pattern precisely: their unresolved threat status is predictable from their traits. But the data suggest something worse. Among assessed species, those with fewer than ten GBIF records are 60% threatened (n = 1,557), compared to 8% for species with over a thousand records (n = 711). Species described after 2010 are 54% threatened (n = 1,075), compared to 26% for species described before 1980 (n = 557). DD species sit at the extreme low end of both distributions. The pattern is consistent with “missing not at random” (MNAR): true threat and data deficiency reinforce each other.

Using two complementary approaches, propensity-score matching (comparing DD species to assessed species with statistically similar ecological profiles) and multiple imputation (generating plausible threat-status assignments that propagate uncertainty through the estimates), the analysis converges on 58–67% of DD species being likely threatened. That represents 530–610 species not reflected in current Red List summaries. Prior estimates have varied widely: Gonzalez-del-Pliego et al. *(10)* estimated 47% using spatio-phylogenetic trait imputation; Howard and Bickford *(3)* estimated approximately 63%; and Borgelt et al. *(11)* predicted 85%. What distinguishes this estimate is the methodology: missing-data theory provides a formal framework for diagnosing *why* the data are missing and choosing corrections appropriate to the diagnosis.

An independent check supports this range. Isa, Tapley et al. *(12)* found that ~50% of DD species reassessed in historical Red List updates were classified as threatened, but reassessment targets the most accessible species first, so the unresolved remainder is likely more threatened, consistent with the higher estimate here.

If 530–610 DD species are indeed threatened, the official count of globally threatened amphibians (2,873) understates the true figure by roughly 20%. It means that conservation priority-setting tools built on Red List tallies, from protected-area gap analyses to funding allocation models, may be systematically underweighting the regions and taxa where unquantified risk concentrates. The map makes this concrete.

## Where the hot blindspots are

Figure 2 juxtaposes two views of the same planet. Panel A shows where threatened amphibian species concentrate: the tropical Andes, Atlantic Forest, Madagascar, Central Africa, and Southeast Asia. Panel B shows GBIF sampling completeness for species-rich cells (those with 25 or more expected species), the fraction of expected species actually documented by occurrence records.

<figure style="text-align: center;">
  <img src="/images/amphibian-data/figure2.png" alt="The mismatch between amphibian threat and observation" style="max-width: 100%; width: 760px;">
  <figcaption><em><strong>Figure 2.</strong> The mismatch between amphibian threat and observation. (A) Threatened amphibian species richness per one-degree grid cell. (B) GBIF sampling completeness for high-richness cells (upper quartile, 25 or more expected species), with hot blindspot cells (lower quartile of completeness, below 41%) in dark red. Tropical hotspots of threatened species border the most severe monitoring gaps, consistent with the possibility that the blindspots themselves hide additional unreported threats.</em></figcaption>
</figure>

The mismatch is telling. Threatened species concentrate on the periphery of hot blindspots, bordering the Amazon basin, the Atlantic Forest, and Central Africa, while the blindspots themselves appear nearly empty of threatened species, possibly because reporting is sparse rather than because threats are absent. Mapping GBIF completeness onto one-degree grid cells (~111 km), this analysis finds that among cells with high amphibian diversity, over 50% qualify as hot blindspots: species-rich cells where monitoring coverage is too sparse to detect threats. This is consistent with realm-level patterns identified by Gonzalez-del-Pliego et al. *(10)* and Herrera-Lopera et al. *(13)*.

Not all hot blindspots are alike. In the Amazon basin and Central Africa, fewer than 15% of species in under-sampled cells are classified as threatened, suggesting that the true threat burden remains largely invisible. In Southeast Asia, 34% of species in under-sampled cells are already classified as threatened despite GBIF completeness of only 38%, a partially visible crisis constrained less by ignorance than by conservation capacity. Amphibians receive less than 3% of global vertebrate conservation funding *(14)*, and Southeast Asian protected areas face chronic operational underfunding even after establishment *(15)*. The Indomalayan realm also carries the highest DD proportion of any biogeographic realm (15%), suggesting that even these elevated threat figures understate the true burden. Where threats are already partially documented, funding for management may matter as much as funding for discovery.

## The species citizen science cannot see

The hot blindspots are not simply places where no one has looked. They reflect a structural limitation in how biodiversity data are now collected. Among assessed species, 67% of GBIF records come from citizen-science platforms, predominantly iNaturalist. For DD species, the ratio inverts: 70% of their records come from preserved museum specimens. Nearly half of DD species with any GBIF data are documented only by specimen records. iNaturalist, contributing 2.2 million amphibian records to GBIF *(6)*, covers only 164 of 909 DD species; just 0.1% of its amphibian records pertain to DD species.

The geographic and temporal reach of DD records is equally thin. The median DD species has occurrence data from a single grid cell; its museum records span a median of one year. For assessed species, the typical temporal coverage spans decades.

The decline in specimen-based collecting compounds the problem (Figure 3A). In the GBIF data used here, amphibian museum specimens averaged over 40,000 per year in the 1960s–70s and have since halved, stabilizing at roughly 17,000 per year from the 1990s onward. Over the same period, citizen-science records exploded from fewer than 2,000 per year in the 1960s to over 500,000 per year in the 2020s. The monitoring effort that can reach DD species is shrinking while the effort that cannot is growing. For species that cannot be photographed, the window for discovery is narrowing.

<figure style="text-align: center;">
  <img src="/images/amphibian-data/figure3.png" alt="Data gaps and their consequences for global amphibian conservation metrics" style="max-width: 100%; width: 760px;">
  <figcaption><em><strong>Figure 3.</strong> Data gaps and their consequences for global amphibian conservation metrics. (A) Divergent trajectories of biodiversity monitoring methods: average annual museum specimen records peaked in the 1960s-70s and have since halved, while citizen-science records have grown over 200-fold since the 1950s. (B) Red List Index (RLI) values under different assumptions about DD species. The uncertainty range from DD assumptions (0.059) exceeds the observed 1980 to 2022 decline (0.031) by nearly two-fold, but all scenarios show deterioration over time. Grey ribbon shows 95% bootstrap confidence interval for the baseline. (C) Driver-disaggregated RLI change by period. Each bar shows the RLI decrement attributable to a threat driver, split into deterioration (red, species uplisted) and recovery (green, species downlisted). Numbers indicate species. Disease dominated 1980 to 2004; from 2004 to 2022, climate change shows zero recoveries while disease and habitat loss both show substantial recovery offsets.</em></figcaption>
</figure>

Citizen science has transformed biodiversity monitoring for well-known species in well-surveyed regions. But it structurally misses the species that most need discovery. Closing this gap will require survey expeditions, not smartphone apps.

## DD uncertainty dwarfs the observed global decline

These are regional patterns. Their cumulative effect on the global conservation barometer can be quantified.

The Red List Index (RLI) runs from 1 (all species Least Concern) to 0 (all species Extinct); lower values mean worse conservation status *(16)*. Under the standard methodology, which excludes DD species entirely, the amphibian RLI declined from 0.765 \[95% bootstrap CI: 0.758–0.771\] in 1980 to 0.734 \[0.727–0.742\] in 2022, a drop of 0.031 units.

To test how sensitive this trend is to DD assumptions, the present analysis recomputed the RLI under six alternative scenarios, ranging from treating all DD species as Least Concern to treating 85% as threatened *(11)*. The resulting uncertainty spans 0.059 RLI units, nearly twice the observed decline itself (Figure 3B). The direction of decline is robust: under all six scenarios, the RLI falls over time. What is uncertain is the level: we cannot currently distinguish a moderately deteriorating situation from one that is substantially worse.

Model-based imputations place the 2022 RLI between 0.715 and 0.727, well below the official 0.734. If correct, Global Biodiversity Framework targets assessed against the official RLI are systematically optimistic, and the degree of optimism is unknowable without resolving the DD species.

## The threat landscape is shifting

Luedtke et al. *(1)* documented a qualitative shift in amphibian threat drivers over time. The present analysis quantifies this by decomposing the RLI trend by proximate driver *(16, 17, 18)* for global amphibians for the first time (Figure 3C).

From 1980 to 2004, disease and habitat loss jointly drove over 90% of status deteriorations *(1)*, with disease the larger contributor. From 2004 to 2022, climate change drove the single largest net RLI decline: 119 species were uplisted, zero downlisted. Habitat loss remained sustained (112 uplisted, 41 downlisted). Disease showed substantial recovery: 40 of 109 previously disease-affected species improved in status, partially offsetting deterioration. What distinguishes climate as a driver is not the severity per species, as each climate-driven or disease-driven deterioration was about equally severe, but the complete absence of recovery. The threat landscape has shifted, and management frameworks need to shift with it.

This finding interacts directly with the DD problem. If the majority of DD species are indeed threatened, and most are tropical species in regions experiencing accelerating habitat loss and climate change, then a driver decomposition that excludes them may systematically undercount climate- and habitat-driven declines. The species absent from the analysis are precisely those most exposed to the threats now dominating.

## A resource for the community

One output of this work is the integrated dataset itself. The species-level table described above contains over 100 columns per species, including IUCN status at three time points (1980, 2004, 2022), genuine status-change flags with attributed threat drivers, and synonym reconciliation across all five source databases. It is designed to be extended: adding regional Red Lists, environmental DNA detections, or acoustic monitoring data can begin with a species-name join to the existing backbone. The full dataset, code, and model specifications will be publicly archived alongside the preprint (target: mid-2026).

## What comes next

I welcome contact from researchers with field expertise in under-represented regions, access to regional amphibian databases not yet included, or interest in extending the analytical framework. The DD problem is a data problem at its root, and the gap between what existing amphibian data can support and what is currently extracted from it is wider than it needs to be. Bridging that gap is work worth doing together.

For the 909 species currently hidden behind a “Data Deficient” label, that bridge could be the one that matters.

## Acknowledgments

This analysis was conducted independently by the author in a personal capacity and was not supported by institutional funding. The author thanks the data providers behind the GAA2, GBIF, AmphibiaWeb, AmphiBIO, and the European Red List, whose open-data commitments made this integration possible.

## References

1)  Luedtke, J.A. et al. Ongoing declines for the world’s amphibians in the face of emerging threats. *Nature* **622**, 308–314 (2023).

2)  IUCN. The IUCN Red List of Threatened Species. Version 2025-2. https://www.iucnredlist.org (accessed 4 March 2026).

3)  Howard, S.D. & Bickford, D.P. Amphibians over the edge: silent extinction risk of Data Deficient species. *Divers. Distrib.* **20**, 837–846 (2014).

4)  Bland, L.M., Collen, B., Orme, C.D.L. & Bielby, J. Predicting the conservation status of data-deficient species. *Conserv. Biol.* **29**, 250–259 (2015).

5)  Cazalis, V. et al. Prioritizing the reassessment of data-deficient species on the IUCN Red List. *Conserv. Biol.* **37**, e14139 (2023).

6)  GBIF.org. GBIF Occurrence Download. https://doi.org/10.15468/dl.3xrhsz (accessed 4 March 2026).

7)  AmphibiaWeb. https://amphibiaweb.org (University of California, Berkeley; accessed 4 March 2026).

8)  Oliveira, B.F., São-Pedro, V.A., Santos-Barrera, G., Penone, C. & Costa, G.C. AmphiBIO, a global database for amphibian ecological traits. *Sci. Data* **4**, 170123 (2017).

9)  Crnobrnja-Isailović, J., Schmidt, B.R., Denoël, M. et al. Measuring the Pulse of European Biodiversity. European Red List of Amphibians (European Commission, Brussels, 2025). https://doi.org/10.2779/035237.

10) Gonzalez-del-Pliego, P. et al. Phylogenetic and trait-based prediction of extinction risk for data-deficient amphibians. *Curr. Biol.* **29**, 1557–1563 (2019).

11) Borgelt, J. et al. More than half of data deficient species predicted to be threatened by extinction. *Commun. Biol.* **5**, 679 (2022).

12) Isa, H.R., Tapley, B. & Michaels, C.J. How many Data Deficient amphibians are threatened? IUCN Red List assessments for amphibian species previously classed as Data Deficient. *Herpetol. Bull.* **169**, 12–17 (2024).

13) Herrera-Lopera, J.M., Solé, M. & Cultid-Medina, C.A. Mapping the missing: assessing amphibian sampling completeness and overlap with global protected areas. *Ecol. Evol.* **15**, e71137 (2025).

14) Guénard, B. et al. Limited and biased global conservation funding means most threatened species remain unsupported. *Proc. Natl Acad. Sci. USA* **122**, e2412479122 (2025).

15) Sreekar, R. et al. Conservation opportunities through improved management of recently established protected areas in Southeast Asia. *Curr. Biol.* **34**, 3830–3835 (2024).

16) Butchart, S.H.M. et al. Measuring global trends in the status of biodiversity: Red List Indices for birds. *PLoS Biol.* **2**, e383 (2004).

17) Butchart, S.H.M. et al. Using Red List Indices to measure progress towards the 2010 target and beyond. *Phil. Trans. R. Soc. B* **360**, 255–268 (2005).

18) Sandvik, H. & Pedersen, H.C. Using Red List Indices to assess threats to species: counting versus weighting approaches. *Conserv. Biol.* **37**, e14049 (2023).

