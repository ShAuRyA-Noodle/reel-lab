# reel-lab

A personal video editing workspace for building short-form vertical reels. It holds the raw footage, the FFmpeg filter scripts used to grade and assemble each cut, the animated overlay assets, and the final rendered exports, alongside a vendored copy of the HyperFrames engine used to produce the HTML-based overlay compositions.

## What is in here

```
.
├── Her.MOV                         # Source footage (Git LFS)
├── edit/                           # The actual edit
│   ├── her_reel_filter.ffscript    # FFmpeg filtergraph: trims, speed ramps,
│   ├── her_reel_long_filter.ffscript #   color grade, crops, overlay compositing
│   ├── final_her_viral_reel.mp4    # Rendered exports (Git LFS)
│   ├── final_her_viral_reel_long_clean_audio.mp4
│   ├── overlays/                   # Animated overlay: webm + PNG frame sequences
│   ├── hyperframes-her-overlays/   # HTML overlay composition (HyperFrames)
│   └── verify/                     # Stills pulled for QA / color checks
└── repos/
    └── hyperframes/                # Vendored copy of the HyperFrames engine
```

## The edit

The reels are assembled directly with FFmpeg filtergraphs in the `.ffscript` files. Each clip is trimmed, speed ramped, color graded (BT.2020 to BT.709 conversion, contrast, saturation, sharpening, vignette), cropped to a 1080x1920 vertical frame with a subtle handheld motion path, and then composited with a transparent overlay layer. Audio is normalized with a compressor, bass and treble shaping, and a limiter.

The overlay layer is built as an HTML composition and rendered to a transparent video with [HyperFrames](https://github.com/heygen-com/hyperframes), an open-source HTML-to-video framework. The frame sequences in `edit/overlays/` are the exported result.

## repos/hyperframes

`repos/hyperframes/` is a vendored snapshot of the upstream [HyperFrames](https://github.com/heygen-com/hyperframes) monorepo (Apache-2.0). It is kept here as a reference copy of the toolchain used to produce the overlay compositions. It is not a fork and is not modified. Refer to the upstream project for the canonical source, documentation, and license.

## Large files

Video sources and rendered exports are tracked with [Git LFS](https://git-lfs.com). Install Git LFS before cloning to pull the actual media instead of pointer files:

```bash
git lfs install
git clone https://github.com/ShAuRyA-Noodle/reel-lab.git
```
