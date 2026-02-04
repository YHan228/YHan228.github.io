---
title: 'The Shape of Wabi: Digital Morphometrics of Japanese Tea Bowls'
date: 2026-01-25
permalink: /posts/2026/01/wabimorph/
tags:
  - Morphometrics
  - Japanese Ceramics
  - Data Science
  - Art History
---

*A Computational Study of Raku, Hagi, and Karatsu Ware*

## 1. From Photo to Shape: Extracting Geometry from Images

How do we capture the "essence" of a tea bowl? A photograph is rich with information—lighting, angle, color—but to study **form** rigorously, we must look past these distractions.

Our method acts as a "digital potter's eye," tracing the vessel's silhouette to isolate its fundamental geometry. By converting the bowl's outline into a mathematical series of elliptical harmonics (Elliptic Fourier Analysis), we can quantify subtle variations in curvature, lip shape, and foot profile that might escape the naked eye.

<figure style="text-align: center;">
  <img src="/images/wabimorph/image_contour_comparison.svg" alt="From Photo to Data" style="max-width: 100%; width: 600px;">
  <figcaption><em>From Photo to Data: The contour extraction process abstracts the vessel into a pure mathematical signature, removing surface noise to focus on structural DNA.</em></figcaption>
</figure>

This abstraction allows us to compare hundreds of bowls simultaneously, revealing patterns that span centuries of ceramic tradition.

*Dataset note:* Shape analysis uses **255** bowls from **35 institutions** across three continents (including the Metropolitan Museum of Art, Cleveland Museum of Art, Smithsonian, and Japan Search); texture and shape–texture coupling use a **195-image high-resolution subset** (see the "Resolution Trap"; filtered to ≥100k pixels, i.e., ~0.1 MP).

> **Key terms (plain-language)**
> - **Typicality distance**: how far a bowl is from its tradition's "center" in shape space (a Mahalanobis distance; lower = more typical).
> - **ICC (reliability)**: what fraction of measured variation is real between-bowl difference vs segmentation noise (higher = more trustworthy).
> - **CCA (shape–texture coupling)**: finds paired patterns in shape and surface that tend to vary together.

---

## 2. Raku: Standardized Skeleton, Variable Skin

**Raku ware** is often celebrated for its "handmade" character, shaped by the *tezukune* (hand-forming) technique rather than a potter's wheel. Paradoxically, our analysis reveals it to be the most morphologically standardized of the three traditions—at least in its primary dimensions.

### The Canonical Form

In the "morphospace" below, Raku bowls (blue) form a dense, tight cluster. This indicates a strict adherence to a specific height-to-width ratio and general curvature. The constraints of the Raku firing process and the tea ceremony's codified aesthetics likely enforced this standardization.

<figure style="text-align: center;">
  <img src="/images/wabimorph/pca_plot.png" alt="Morphospace of Japanese Tea Bowls" style="max-width: 100%; width: 500px;">
  <figcaption><em>Morphospace of Japanese Tea Bowls: Raku (blue) clusters tightly, while Hagi (red) and Karatsu (green) are dispersed.</em></figcaption>
</figure>

<details>
<summary><strong>Statistical Foundation</strong> (click to expand)</summary>

<p>The morphospace above is derived from Principal Component Analysis (PCA) of shape coefficients. The first two axes capture <strong>87%</strong> of total shape variation (PC1: 72%, PC2: 15%). The scree plot and shape-variation diagrams below show what each axis represents geometrically.</p>

<figure style="text-align: center;">
  <img src="/images/wabimorph/pca_scree.png" alt="Scree Plot" style="max-width: 100%; width: 450px;">
  <figcaption><em>Scree Plot: Variance explained by each principal component. The first two PCs dominate.</em></figcaption>
</figure>

<figure style="text-align: center;">
  <img src="/images/wabimorph/pca_shape_variation.png" alt="Shape Variation" style="max-width: 100%; width: 550px;">
  <figcaption><em>Shape Variation: What do the principal components mean? PC1 captures height-to-width ratio; PC2 captures curvature of the walls.</em></figcaption>
</figure>

</details>

This clustering has practical consequences: Raku's tight grouping yields **92%** classification recall (the algorithm rarely misidentifies a Raku bowl), while Hagi (**51%**) and Karatsu (**47%**) frequently confuse with each other due to their overlapping morphospace.

<figure style="text-align: center;">
  <img src="/images/wabimorph/shapes_overlaid.png" alt="Shape Overlap" style="max-width: 100%; width: 500px;">
  <figcaption><em>Shape Overlap: All contours overlaid by tradition reveal Raku's tight conformity (blue) versus the broader diversity of Hagi (red) and Karatsu (green).</em></figcaption>
</figure>

### The Paradox of Variation

However, "standardized" does not mean "identical." While Raku bowls are uniform in their basic silhouette (low median typicality distance of **1.68**), they exhibit the highest variability in fine details (highest standard deviation of **1.25**).

*   **Interpretation:** Raku bowls share a rigid "skeleton" (the canonical tea bowl shape) but possess a highly variable "skin" (surface undulations from hand-carving).
*   **Contrast:** Hagi and Karatsu bowls are the opposite—diverse in their basic skeletons (tall, wide, conical, cylindrical) but smoother and more consistent in their fine contours.

<figure style="text-align: center;">
  <img src="/images/wabimorph/typicality_distribution.png" alt="Typicality Distribution" style="max-width: 100%; width: 450px;">
  <figcaption><em>Typicality Distribution: Raku has a dense "core" of typical shapes but significant outliers, reflecting individual artistic expression within a strict canon.</em></figcaption>
</figure>

*Balancing note:* Hagi shows the most consistent shape overall (lowest typicality spread), while Karatsu sits in-between—more variable than Hagi, less than Raku.

---

## 3. Surface Tells More Than Shape

If you encounter a bowl with an ambiguous shape—perhaps a Hagi bowl that mimics a Karatsu form—where should you look for the truth? **The surface.**

Our analysis shows that while shapes overlap significantly between Hagi and Karatsu, surface cues add useful separation. By analyzing texture features like crackle (crazing), clay roughness, and pitting, we can distinguish the wares **somewhat more accurately** than by shape alone—*when high-resolution images are available*.

### The Hagi-Karatsu Connection

Even with texture, Hagi and Karatsu remain frequently confused (misclassification rates of ~30% each direction). This is not a failure of our method—it reflects a genuine morphological kinship. Both traditions share wheel-thrown forms and regional Kyushu heritage, unlike Raku's hand-formed, Kyoto-centered aesthetic. The algorithm confirms what connoisseurs have long intuited: Hagi and Karatsu are closer cousins to each other than either is to Raku.

<figure style="text-align: center;">
  <img src="/images/wabimorph/texture_lda.svg" alt="Texture Separation" style="max-width: 100%; width: 500px;">
  <figcaption><em>Texture Separation: Surface analysis separates the traditions more effectively than shape. Raku's rough, pitted surface (high contrast) is unmistakably distinct from Hagi's smooth, milky glaze.</em></figcaption>
</figure>

*   **Raku:** High contrast, rough surface (hand-molded clay, porous).
*   **Hagi:** Low contrast, high homogeneity (smooth, milky glaze).
*   **Karatsu:** Intermediate texture, often with iron-painted designs.

<figure style="text-align: center;">
  <img src="/images/wabimorph/texture_ware_profiles.svg" alt="Texture Profiles by Tradition" style="max-width: 100%; width: 550px;">
  <figcaption><em>Texture Profiles by Tradition: Quantitative comparison of GLCM texture features shows clear separation—Raku's rough surface (high contrast, low homogeneity) vs. Hagi's smooth glaze (low contrast, high homogeneity).</em></figcaption>
</figure>

Quantitatively, shape features alone achieve **63%** classification accuracy; texture reaches **69%**, and combining both yields **70%**—a modest but consistent improvement.

<figure style="text-align: center;">
  <img src="/images/wabimorph/accuracy_comparison.svg" alt="Model comparison" style="max-width: 100%; width: 500px;">
  <figcaption><em>Model comparison (high-resolution subset): Texture slightly outperforms shape; combining them yields only a small additional gain.</em></figcaption>
</figure>

---

## 4. Form and Surface Move Together

Did potters mix and match shapes and glazes randomly? Our **Sparse Canonical Correlation Analysis (CCA)** suggests otherwise. We discovered a strong statistical "coupling" in the leading mode (Correlation r ≈ 0.99) between specific shapes and specific textures.

In plain terms, some shape tendencies co-occur with more *orderly/uniform* surface statistics, while other shape tendencies co-occur with more *varied* surfaces. The direction of the axis is arbitrary—what matters is that form and surface move together rather than independently.

<figure style="text-align: center;">
  <img src="/images/wabimorph/cv_extremes.svg" alt="Style Coupling" style="max-width: 100%; width: 600px;">
  <figcaption><em>Style Coupling: Real examples of bowls at the extremes of the Shape-Texture relationship. Form and surface are not independent; they are structural partners.</em></figcaption>
</figure>

<figure style="text-align: center;">
  <img src="/images/wabimorph/canonical_correlations.svg" alt="Canonical correlations" style="max-width: 100%; width: 500px;">
  <figcaption><em>Canonical correlations: The strongest coupling mode is very high (CV1 r≈0.99), and multiple additional modes are statistically significant.</em></figcaption>
</figure>

---

## 5. Measurements Are Reliable—If Resolution Is High

Can we trust these digital measurements? To verify our findings, we tested the "segmentation uncertainty"—the error introduced when outlining the bowls.

### High Reliability

We found that **86.5%** of the variation in our data represents real differences between bowls (Signal), while only **13.5%** is due to measurement noise. This "Signal-to-Noise Ratio" (ICC = 0.865) confirms that the morphological patterns we detect are materially and culturally real, not artifacts of the software.

<figure style="text-align: center;">
  <img src="/images/wabimorph/variance_decomposition.svg" alt="Variance Decomposition" style="max-width: 100%; width: 400px;">
  <figcaption><em>Variance Decomposition: The biological/cultural signal overwhelmingly dominates measurement noise.</em></figcaption>
</figure>

<figure style="text-align: center;">
  <img src="/images/wabimorph/feature_icc_distribution.svg" alt="Per-feature reliability" style="max-width: 100%; width: 500px;">
  <figcaption><em>Per-feature reliability: Most coefficients are stable, but reliability varies across Fourier components—useful context for interpreting fine-grained effects.</em></figcaption>
</figure>

### The Resolution Cliff

However, data quality matters. We observed a clear resolution-dependent pattern: at the low-resolution end, segmentation uncertainty becomes larger and more variable (the funnel plot shows a significant negative association between resolution and uncertainty, Spearman ρ ≈ -0.38). This is why texture and coupling results are reported on a high-resolution subset (**195** images).

One encouraging detail: **Karatsu** features were the most stable under segmentation perturbations (ICC ≈ **0.915**), followed by **Raku** (ICC ≈ **0.884**), while **Hagi** was more sensitive (ICC ≈ **0.756**).

*   **Implication:** Low-resolution thumbnails from aggregators like Japan Search are often insufficient for rigorous morphometrics.
*   **Recommendation:** Reliable digital art history requires high-fidelity imaging. Museums must prioritize resolution to enable this kind of computational scholarship.

<figure style="text-align: center;">
  <img src="/images/wabimorph/uncertainty_funnel.svg" alt="The Funnel Plot" style="max-width: 100%; width: 450px;">
  <figcaption><em>The Funnel Plot: Uncertainty vs. Resolution. Note the rise in error (y-axis), especially at the low-resolution end of the distribution.</em></figcaption>
</figure>

---

## 6. Limitations: A Call for Better Data

This study demonstrates what is possible with computational morphometrics—but it also reveals the constraints of working with limited data.

### Dataset Size and Access

Our corpus of **255 bowls** (195 at high resolution) is modest by machine learning standards. Access restrictions—copyright, institutional policies, and the scarcity of digitized collections—limited what we could gather. Raku ware is overrepresented (58% of samples) simply because more Raku images were publicly available, not because Raku is more common or important.

### What We Cannot Yet Do

Modern deep learning methods (CNNs, vision transformers) typically require thousands of training examples per class. With fewer than 50 high-resolution Hagi and Karatsu images each, such methods would likely overfit. The statistical approaches used here (PCA, LDA, CCA) are more appropriate for small samples, but they make stronger assumptions and capture less complex patterns.

### Findings That May Reflect Dataset Artifacts

We cannot fully rule out that some patterns arise from sampling bias rather than true ceramic properties:

*   **Raku's tight clustering** may partly reflect the fact that our Raku images come from fewer source types (mostly tea ceremony collections), while Hagi and Karatsu span more heterogeneous museum holdings.
*   **The Hagi-Karatsu confusion** might decrease with larger, more balanced samples—or it might persist, reflecting genuine morphological kinship.
*   **Shape-texture coupling strength** (r ≈ 0.99) is estimated from 195 images; larger samples might reveal weaker or more nuanced relationships.

### A Path Forward

For more robust findings and to enable modern machine learning approaches, the field needs:

*   **Larger, balanced datasets** with hundreds of examples per tradition
*   **Standardized imaging protocols** (consistent lighting, angles, resolution)
*   **Open access** to high-resolution museum collections

Until then, results like ours should be treated as *hypotheses to be tested* rather than definitive conclusions. The patterns are real in our data—whether they generalize to the full universe of Japanese tea bowls remains an open question.
