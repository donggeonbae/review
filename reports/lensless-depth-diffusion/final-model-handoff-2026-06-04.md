# Final Model Handoff: Lensless Depth Diffusion v15

## Metadata

- Research ID: `lensless-depth-diffusion/2026/final-v15-physics-integrated-ldm`
- Project label: `Ours`
- Model family: v15 physics-integrated latent diffusion with DAPS-lite posterior sampling
- Review type: method/evidence handoff for final paper and poster preparation
- Source note status: `donggeonbae/research` was not accessible through the current connector during this run, so source-note links remain placeholders.
- Related writing artifacts: ICCP-style short report and poster draft in the working project.

## Executive Status

`Ours` is fixed as the best policy-compliant diffusion model, not the strongest supervised baseline. The selected model is v15 because it puts PSF/deconvolution physics into the latent diffusion model and reverse sampling process. A stronger supervised teacher may be reported as an upper bound or baseline, but should not replace `Ours`.

Current full-test evidence from the v15 195k-step checkpoint:

| Model | Train state | Test split | fg delta1 | fg delta2 | fg delta3 | fg MAE | fg AbsRel |
| --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| Physics-only focus/deconv | no training | 6,000 | 0.391 | 0.617 | 0.816 | 0.214 | - |
| Ours v15, current paper result | 195,000 steps, 2.95 epoch | 6,000 | 0.871 | 0.913 | 0.930 | 0.0567 | 0.133 |
| Supervised residual teacher, not Ours | trained baseline | 6,000 | - | - | 0.971 | - | - |

The requested 98% target is not yet verified by the diffusion model. A final convergence run is active in the working project from 2.95 epochs to 5.0 epochs. The final paper numbers should be updated only after a fresh 6,000-sample evaluation.

## Gap -> Method -> Evidence -> Implication

### Existing Research Core

MWDN-style Wiener/deconvolution produces a PSF-depth-dependent focus volume, and depth can be inferred from which plane is locally sharp. FlatNet3D-like networks learn lensless 3D reconstruction from coded measurements. Marigold and DiffusionDepth-style methods show diffusion priors are useful for depth regularization. DiffBIR/StableSR-style methods often use diffusion as a restoration prior after degradation features are extracted.

### Project Gap

The target is not a simple `deconv -> UNet` baseline and not a DiffBIR-like post-hoc enhancer. The technical question is how PSF/deconvolution physics can enter the diffusion process itself, especially during reverse diffusion, while preserving the per-depth focus behavior of the deconvolution stack.

### Ours v15 Method

Ours v15 uses:

- a latent depth autoencoder that encodes depth into compact latents and decodes predicted latents back to depth;
- a latent denoising diffusion model for depth;
- a 42-plane PSF-stack Wiener/deconvolution condition;
- focus probability, depth hint, and auxiliary focus channels to expose per-pixel focus structure;
- learnable time-conditioned Wiener parameters plus a fixed auxiliary depth-wise Wiener bank selected from per-depth parameter search;
- DAPS-lite posterior guidance/refinement during reverse diffusion;
- depth-guided fusion of deconvolution planes for all-in-focus RGB reconstruction.

This makes v15 the correct `Ours` even if a pure supervised teacher scores higher.

### Current Evidence

At 195k steps, v15 improves strongly over physics-only focus/deconvolution on the full 6k test split:

- fg delta1: 0.391 -> 0.871
- fg delta2: 0.617 -> 0.913
- fg delta3: 0.816 -> 0.930
- fg MAE: 0.214 -> 0.0567

The evidence is suitable for a preliminary paper result, but final convergence and final full-test metrics are still pending.

### Implication

The results support the claim that PSF-depth deconvolution features carry usable depth information and that a latent diffusion prior can regularize these cues. The remaining open question is whether reverse-diffusion physics guidance improves over a strong supervised deconvolution teacher, or mainly improves methodological alignment and interpretability.

## Figure Snapshot Map

| Figure | Status | What it proves |
| --- | --- | --- |
| Architecture figure | Needs final check before submission | Shows latent encoder/decoder, denoising UNet, PSF/deconv condition, and posterior guidance |
| Deconvolution focus planes | Current | Shows valid focus behavior for mid/late planes; avoid early planes that do not produce interpretable deconvolution |
| Clean depth qualitative panel | Current | Shows RGB, GT depth, physics baseline, and Ours without teacher/error clutter |
| Poster result panel | Current draft | Presentation-ready summary, should be refreshed after final full-test eval |

## Paper Update Rules

1. Run the final full-test evaluation after the 5-epoch checkpoint is complete.
2. Replace the `Ours` row in the paper, poster, and comparison reports with the final v15 metrics.
3. If the 5-epoch checkpoint underperforms the 195k checkpoint, report the best v15 checkpoint as `Ours` and state that extended fine-tuning did not improve validation.
4. Keep the supervised teacher as a baseline or upper-bound comparison only.
5. Rebuild the paper and poster PDFs after metric replacement.

## Presentation Handoff

| Slide | Title | Purpose | Figure Snapshot | Script Point |
| --- | --- | --- | --- | --- |
| 1 | Problem | Define lensless depth from PSF-coded measurements | Raw/PSF/depth sample | Depth must be estimated from depth-dependent coded blur. |
| 2 | Prior Limitation | Explain why plain deconvolution or plain UNet is insufficient | Deconv focus planes | Each depth plane sharpens different regions, so depth depends on focus structure. |
| 3 | Method | Present Ours v15 | Architecture figure | Latent diffusion predicts depth while deconvolution physics conditions and guides reverse sampling. |
| 4 | Results | Compare physics-only, Ours, and non-Ours teacher/baselines | Clean depth results + table | Ours beats physics-only substantially; teacher is stronger but not the target model. |
| 5 | Discussion | State implications and limits | Result table | Current evidence supports physics-integrated diffusion, but 98% remains unverified. |

## Likely Questions

| Question | Suggested answer | Evidence |
| --- | --- | --- |
| Is this actually latent diffusion? | Yes. Depth is encoded into latent space, denoised by a latent diffusion UNet, and decoded back to depth. | v15 model code and architecture figure |
| Is physics inside reverse diffusion? | Partially. v15 includes posterior guidance/refinement during sampling and learnable/time-conditioned Wiener conditioning; it is not just `deconv -> UNet`. | v15 sampling config and DAPS-lite guidance settings |
| Why not report the teacher as Ours? | The project goal is diffusion with embedded physics. The teacher is a useful upper bound/baseline, not the final policy-compliant model. | Project policy and comparison table |
| Has the model fully converged? | Not yet at the time of this handoff. It is being resumed from 2.95 to 5.0 epochs. | Final convergence run metadata in working project |

## Manual Verification Needed

- Confirm the final checkpoint reaches 5.0 epochs.
- Run and log the full 6,000-sample evaluation.
- Decide whether the 5-epoch checkpoint or an earlier v15 checkpoint is the final reported `Ours`.
- Update paper/poster numbers and rebuild PDFs.
- Check that the architecture figure uses the generated/polished figure, not an interim rough diagram.
