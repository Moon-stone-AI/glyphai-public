# GlyphAI

**Keep the meaning. Control who can read it.**

GlyphAI is a framework for semantic-preserving text transformation. It turns text into *glyphs*: compact symbols that stand for meaning rather than for words. What a glyph means is defined by a **codebook**, and whoever holds the codebook decides who can read it back.

Two consequences follow:
- **Different words, one meaning, one glyph.** Three vendors, two languages and a binary record that report the same event become the same symbol.
- **Analysis without exposure.** Glyphs can be counted, compared and reasoned about by people who cannot see the raw text behind them.

## Where the idea comes from

*"In the beginning was the Word."* The Greek of John 1:1 says **λόγος**, and logos means far more than "word": reason, thought, meaning, proportion. The translation kept the outer form and lost most of the content. The most translated sentence in the world opens with a loss of meaning in translation.

GlyphAI starts from the other end: record the meaning first, and let the words be one of many possible renderings.

## The monograph

**GlyphAI: A Tiered Framework for Semantic-Preserving Text Transformation with Codebook-Controlled Non-Interpretability**, by Vitali de Mille.
Zenodo: https://zenodo.org/records/20813531

What it covers:
- **Semantic atoms, ontological relations and many-to-one projection**: many surface forms map to one invariant core meaning.
- **Three tiers**:
  - *Tier 1*: reversible demonstration layer, fully inspectable.
  - *Tier 2*: hybrid secure compression with decoder separation, the practical balance between utility and protection.
  - *Tier 3*: theoretical model-as-key bound, where the ability to interpret is itself controlled infrastructure.
- **The codebook as a semantic control plane**: public, private and domain-specific codebooks, ownership, custody and governance.
- **Security model and its limits**: what reconstruction is architecturally prevented, and where residual risk and uncertainty remain.
- **A formal treatment** in the appendix.

## First application: fleet root-cause analysis

**[glyph-fleet-rca](https://github.com/Moon-stone-AI/glyph-fleet-rca)** applies GlyphAI to server event logs.

When thousands of servers fail at once, the ones that died instantly could not write down why. Their logs are a storm of identical errors, and the cause is in the log of the one machine that lived a second longer. Finding it by hand can take weeks.

In glyphs it takes seconds:

| Level | What happens |
|---|---|
| L1 word → word glyph | vendor vocabulary normalised |
| L2 phrase → concept glyph | one meaning per line, whatever the vendor, language or format |
| L3 run → concept × count | a storm of millions of lines becomes one glyph with a counter |
| L4 fleet → signatures × servers | servers with the same story collapse into one line; **the survivor stands alone** |

On a synthetic fleet of 6,000 servers and 4.1 million events from five sources (four BMC log dialects, two kernel log formats, DCGM telemetry and diagnostics), it found the single survivor, tied the crash to one firmware version, and told a faulty PCIe switch apart from a faulty GPU, in about 98 seconds on one CPU core.

Honest numbers: at L1–L2, plain gzip compresses better. What gzip cannot do is see that different words mean the same thing. Glyphs pull ahead at L3 and L4 (×26,440 at L4), where meaning, not bytes, is being compressed.

**Tier 2 in practice**: the same analysis can be produced in opaque tokens and shared with a vendor or contractor. They see which pattern is a storm and which is rare. They do not see hosts, slots, firmware versions or events. The private codebook stays with the owner of the data.

## Timeline

- **2025**: GlyphAI framework and this repository.
- **2025–2026**: the monograph, published on Zenodo.
- **October 2026**: first applied domain, server event logs: `glyph-fleet-rca` v0.1 (IPMI SEL, binary and text, PCIe tree, the survivor search).
- **16 October 2026**: `glyph-fleet-rca` v0.2: five sources read into one glyph language: SEL, Linux kernel and NVIDIA Xid, DCGM telemetry and active diagnostics. Triage rules reviewed by a practitioner from his own records.
- **17 October 2026**: v0.2.1 released: a health index from 0 to 100 % for every GPU, built from its own history. Uncorrectable memory errors and failed matrix-math tests cap the score.
- **17 October 2026**: v0.3: vendor codebooks built from the official Dell, Lenovo and HPE message guides (69 Dell iDRAC IDs, 67 Lenovo XCC/UEFI IDs, 53 HPE IML messages), including GPU-server platforms. Every entry cites its guide; nothing is guessed.
- **Next**: Supermicro and AMD records, Windows Event Log in several languages, and an analysis service that receives only tokens, never raw data.

## About the author

**Vitali de Mille**: 20+ years in mission-critical and hyperscale data centres (Equinix, Microsoft), from live-site operations to hardware fleet reliability. GlyphAI grew out of two long interests: how meaning survives translation between languages, and how the truth about a failure hides inside millions of log lines.

- LinkedIn: https://www.linkedin.com/in/vitali-de-mille-14598034/
- Email: de.mille@outlook.com

## License

Copyright © 2025–2026 Vitali de Mille. See [LICENSE](LICENSE). Each project in this family carries its own license: `glyph-fleet-rca` is free for noncommercial use, and commercial use requires a license.
