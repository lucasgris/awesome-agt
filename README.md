# Awesome Guitar Transcription

### A curated list of awesome things related to Automatic Guitar Transcription (AGT)

![awsome-agt-image](https://user-images.githubusercontent.com/34692520/64824341-44161d00-d5a9-11e9-8821-9f4416d4d8f9.png)

Audio-to-notes and audio-to-tablature for guitar, plus the neighbouring tasks (fingering assignment, playing techniques, tablature generation). Last major update: November 2026.

## Contents

- [Datasets](#datasets)
- [Audio to tablature](#audio-to-tablature)
- [Audio to notes (MIDI) for guitar](#audio-to-notes-midi-for-guitar)
- [MIDI or score to tablature (string, fret, fingering)](#midi-or-score-to-tablature-string-fret-fingering)
- [Playing techniques, strumming and rhythm guitar](#playing-techniques-strumming-and-rhythm-guitar)
- [Synthetic data, augmentation and domain adaptation](#synthetic-data-augmentation-and-domain-adaptation)
- [Weak, semi- and self-supervision](#weak-semi--and-self-supervision)
- [Multimodal and video](#multimodal-and-video)
- [Tablature generation and synthesis](#tablature-generation-and-synthesis)
- [General music transcription relevant to guitar](#general-music-transcription-relevant-to-guitar)
- [Code and tools](#code-and-tools)
- [Classic and pre-deep-learning work](#classic-and-pre-deep-learning-work)
- [Notes on evaluation](#notes-on-evaluation)

## Datasets

### Audio with annotations

| Dataset | Year | Size | Content | Annotations |
|---|---|---|---|---|
| [GuitarSet](https://zenodo.org/records/3371780) | 2018 | ~3 h, 360 excerpts, 6 players | Acoustic guitar, hexaphonic pickup + mic | String/fret notes, per-string pitch contours, chords, beats |
| [IDMT-SMT-Guitar](https://www.idmt.fraunhofer.de/en/publications/datasets/guitar.html) | 2014 | ~340 min, 7 guitars | Electric and acoustic | Notes with string/fret, plucking and expression styles |
| [EGDB](https://ss12f32v.github.io/Guitar-Transcription) | 2022 | ~2 h DI, 240 tabs, plus amp renders | Electric guitar | Note-level MIDI |
| [EGDB-PG](https://arxiv.org/abs/2504.07406) | 2025 | EGDB re-rendered through many amp/cab presets | Electric guitar, many tones | Note-level |
| [GAPS](https://huggingface.co/datasets/xavriley/GAPS) ([paper](https://arxiv.org/abs/2408.08653), [Zenodo](https://zenodo.org/records/17152440)) | 2024 | 14 h, 300 performances, 200+ performers | Classical guitar | Score-aligned note MIDI, video links |
| [EGSet12](https://zenodo.org/records/11406378) | 2024 | 12 solo pieces | Electric guitar, amp + mic | String/fret tab (evaluation set) |
| [Guitar-TECHS](https://guitar-techs.github.io) ([paper](https://arxiv.org/abs/2501.03720), [Zenodo](https://zenodo.org/records/14963133)) | 2025 | ~5 h, 3 players | Electric guitar: DI, amp, room mics | Per-string MIDI, techniques, chords, scales |
| [GOAT](https://zenodo.org/records/15690894) ([paper](https://arxiv.org/abs/2509.22655), [repo](https://github.com/JackJamesLoth/GOAT-Dataset)) | 2025 | 5.9 h DI, 29.5 h with amp re-rendering | Electric guitar | Guitar Pro tabs (string/fret + techniques), aligned MIDI; access on request |
| [EGFxSet](https://zenodo.org/records/7044411) | 2022 | 8,970 single tones through real effects | Electric guitar | Note, string/fret, effect |
| [Guitar strumming dataset](https://github.com/Klangio/guitar-strumming-transcription) ([paper](https://arxiv.org/abs/2508.07973)) | 2025 | 90 min real + 4 h synthetic | Acoustic guitar | Strum onsets, direction, chords |
| [GuiFiR](https://github.com/kmu-ee-ailab/guifir_dataset) | 2026 | 1,030 videos | Guitar performance video | Pseudo-tabs, hand pose |

### Synthetic and symbolic

| Dataset | Year | Size | Content |
|---|---|---|---|
| [DadaGP](https://github.com/dada-bots/dadaGP) ([paper](https://arxiv.org/abs/2107.14653)) | 2021 | 26,181 Guitar Pro songs | Symbolic multi-track tablature with techniques; on request |
| [SynthTab](https://www.synthtab.dev) ([paper](https://arxiv.org/abs/2309.09085), [repo](https://github.com/yongyizang/SynthTab)) | 2024 | Thousands of hours rendered from DadaGP | Synthetic audio with string-accurate tablature |
| [SCORE-SET](https://arxiv.org/abs/2507.18723) | 2025 | Guitar Pro files derived from piano MIDI corpora | Symbolic tabs with techniques |
| [AnimeTAB](https://arxiv.org/abs/2210.03027) | 2022 | Fingerstyle tabs | Symbolic |

## Audio to tablature

- [Guitar Tablature Estimation with a Convolutional Neural Network (TabCNN)](https://archives.ismir.net/ismir2019/paper/000033.pdf) - Wiggins & Kim, ISMIR 2019. CNN on CQT frames with one softmax per string; defined the tablature F1 and disambiguation-rate metrics. [Code](https://github.com/andywiggins/tab-cnn).
- [A Data-Driven Methodology for Considering Feasibility and Pairwise Likelihood in Deep Learning Based Guitar Tablature Transcription Systems](https://arxiv.org/abs/2204.08094) - Cwitkowitz, Driedger & Duan, SMC 2022. Inhibition loss built from DadaGP statistics.
- [A Few-Sample Strategy for Guitar Tablature Transcription Based on Inharmonicity Analysis and Playability Constraints](https://robotics.ntua.gr/wp-content/uploads/sites/2/BastasKoutoupis_TablatureTranscription_ICASSP22_Paper.pdf) - Bastas et al., ICASSP 2022. String classification from inharmonicity.
- [FretNet: Continuous-Valued Pitch Contour Streaming for Polyphonic Guitar Tablature Transcription](https://arxiv.org/abs/2212.03023) - Cwitkowitz, Hirvonen & Klapuri, ICASSP 2023. [Code](https://github.com/cwitkowitz/guitar-transcription-continuous).
- [Sequence-to-Sequence Network Training Methods for Automatic Guitar Transcription with Tokenized Outputs](https://zenodo.org/record/10265341) - Kim, Takeda & Toda, ISMIR 2023. Hybrid CTC-attention.
- [SynthTab: Leveraging Synthesized Data for Guitar Tablature Transcription](https://arxiv.org/abs/2309.09085) - Zang, Zhong, Cwitkowitz & Duan, ICASSP 2024.
- [Leveraging Real Electric Guitar Tones and Effects to Improve Robustness in Guitar Tablature Transcription Modeling](https://arxiv.org/abs/2405.14679) - Pedroza, Abreu, Corey & Roman, DAFx 2024. [Project](https://robust-guitar-tabs.github.io/), [code](https://github.com/robust-guitar-tabs/code).
- [Leveraging Unlabeled Data to Improve Guitar Tablature Transcription](https://researchdiscovery.drexel.edu/esploro/outputs/doctoral/991021899513904721) - Wiggins, PhD thesis, Drexel 2024.
- [Automatic Guitar Transcription with Deep Neural Networks](https://rppaiva.dei.uc.pt/publications/Journals/Access_2025_Chieppa.pdf) - Chieppa, Brutti & Paiva, IEEE Access 2025.
- [Separate and Transcribe: Deep Guitar String Separation for Tablature Transcription](https://robotics.ntua.gr/wp-content/uploads/sites/2/2025_Bastas_Deep-Guitar-StringSeparation-TablatureTranscription_TASLP_final.pdf) - Bastas, Katsouros & Maragos, 2025.
- [GOAT: A Large Dataset of Paired Guitar Audio Recordings and Tablatures](https://arxiv.org/abs/2509.22655) - Loth et al., ISMIR 2025. Also tries audio to Guitar Pro tokens. [Audio2Tab](https://github.com/JackJamesLoth/Audio2Tab).
- [TART: A Modular Tool for Technique-Aware Audio-to-Tablature Guitar Transcription](https://arxiv.org/abs/2609.11904) - Gupta et al., ISMIR 2026. Audio to MIDI, technique tagging, audio-conditioned fingering. [Earlier version](https://arxiv.org/abs/2510.02597).
- [Playability-Aware Audio-to-Tablature Guitar Transcription via Diffusion Models (Noise2Fret)](https://arxiv.org/abs/2608.30854) - Simionato & Bigo, ISMIR 2026. [Code](https://github.com/RiccardoVib/Noise2Fret).

## Audio to notes (MIDI) for guitar

- [Towards Automatic Transcription of Polyphonic Electric Guitar Music: A New Dataset and a Multi-Loss Transformer Model (EGDB)](https://arxiv.org/abs/2202.09907) - Chen et al., ICASSP 2022.
- [High Resolution Guitar Transcription via Domain Adaptation](https://arxiv.org/abs/2402.15258) - Riley, Edwards & Dixon, ICASSP 2024. Piano model adapted with score-aligned guitar recordings. [Supplement](https://xavriley.github.io/HighResolutionGuitarTranscription/).
- [GAPS: A Large and Diverse Classical Guitar Dataset and Benchmark Transcription Model](https://arxiv.org/abs/2408.08653) - Riley, Guo, Edwards & Dixon, ISMIR 2024.
- [Towards Generalizability to Tone and Content Variations in the Transcription of Amplifier Rendered Electric Guitar Audio (EGDB-PG)](https://arxiv.org/abs/2504.07406) - Chen et al., 2025.
- [Exploring Procedural Data Generation for Automatic Acoustic Guitar Fingerpicking Transcription](https://arxiv.org/abs/2508.07987) - Murgul & Heizmann, AIMC 2025.
- [Velocity Prediction in Automatic Guitar Transcription](https://arxiv.org/abs/2606.24912) - Loth, Riley, Dixon & Benetos, EUSIPCO 2026.

## MIDI or score to tablature (string, fret, fingering)

- [A Machine Learning Approach for MIDI to Guitar Tablature Conversion](https://arxiv.org/abs/2510.10619) - Kaliakatsos-Papakostas et al., SMC 2022.
- [MIDI-to-Tab: Guitar Tablature Inference via Masked Language Modeling](https://arxiv.org/abs/2408.05024) - Edwards, Riley, Sarmento & Dixon, ISMIR 2024.
- [From MIDI to Rich Tablatures: an Automatic Generative System incorporating Lead Guitarists' Fingering and Stylistic choices](https://arxiv.org/abs/2407.09052) - Bontempi, Manerba, D'Hooge & Canazza, SMC 2024.
- [Guitar Chord Diagram Suggestion for Western Popular Music](https://arxiv.org/abs/2407.14260) - d'Hooge, Bigo, Déguernel & Martin, SMC 2024.
- [Fretting-Transformer: Encoder-Decoder Model for MIDI to Tablature Transcription](https://arxiv.org/abs/2506.14223) - Hamberger, Murgul, Schmidt & Heizmann, ICMC 2025.
- [Explicit Note-Event Tokenization and Pitch-Validity Constrained Decoding for MIDI-to-Tablature Transcription](https://arxiv.org/abs/2607.26440) - Hsu, Wang, Hong & Chen, 2026.

## Playing techniques, strumming and rhythm guitar

- [TENT: Technique-Embedded Note Tracking for Real-World Guitar Solo Recordings](https://doi.org/10.5334/tismir.23) - Su et al., TISMIR 2019.
- [Real-Time Percussive Technique Recognition and Embedding Learning for the Acoustic Guitar](https://arxiv.org/abs/2307.07426) - Martelloni, McPherson & Barthet, ISMIR 2023.
- [Modeling Bends in Popular Music Guitar Tablatures](https://arxiv.org/abs/2308.12307) - d'Hooge, Bigo & Déguernel, ISMIR 2023.
- [A multimodal dataset for electric guitar playing technique recognition](https://www.sciencedirect.com/science/article/pii/S2352340923009046) - Mitsou et al., Data in Brief 2024.
- [EG-IPT: electric guitar instrumental playing techniques](https://nime.org/proceedings/2025/nime2025_14.pdf) - Fiorini et al., NIME 2025. [Dataset](https://zenodo.org/records/15699591).
- [Joint Transcription of Acoustic Guitar Strumming Directions and Chords](https://arxiv.org/abs/2508.07973) - Murgul, Schimper & Heizmann, ISMIR 2025.
- [Transcribing Rhythmic Patterns of the Guitar Track in Polyphonic Music](https://arxiv.org/abs/2510.05756) - Lukoianov & Klapuri, WASPAA 2025.

## Synthetic data, augmentation and domain adaptation

See also SynthTab, EGDB-PG, GOAT and the DAFx 2024 tones-and-effects paper above.

- [Annotation-free Automatic Music Transcription with Scalable Synthetic Data and Adversarial Domain Confusion](https://arxiv.org/abs/2312.10402) - Sato & Akama, 2023. Evaluated on GuitarSet.
- [Open-Amp: Synthetic Data Framework for Audio Effect Foundation Models](https://arxiv.org/abs/2411.14972) - 2024. Amp and effects rendering for augmentation.
- [GuitarFlow: Realistic Electric Guitar Synthesis From Tablatures via Flow Matching and Style Transfer](https://arxiv.org/abs/2510.21872) - Loth, Sarmento, Sandler & Barthet, CMMR 2025.
- [DDSP-based Neural Waveform Synthesis of Polyphonic Guitar Performance from String-wise MIDI Input](https://arxiv.org/abs/2309.07658) - Jonason et al., DAFx 2024.
- [A Differentiable Acoustic Guitar Model for String-Specific Polyphonic Synthesis](https://ismir2022program.ismir.net/lbd_407.html) - Wiggins & Kim, ISMIR 2022 late-breaking.

## Weak, semi- and self-supervision

- [Towards Unsupervised Acoustic Guitar Transcription](https://archives.ismir.net/ismir2020/latebreaking/000023.pdf) - Wiggins & Kim, ISMIR 2020 late-breaking.
- [Unaligned Supervision for Automatic Music Transcription in the Wild (NoteEM)](https://arxiv.org/abs/2204.13668) - Maman & Bermano, ICML 2022.
- [Timbre-Trap: A Low-Resource Framework for Instrument-Agnostic Music Transcription](https://arxiv.org/abs/2309.15717) - Cwitkowitz et al., ICASSP 2024.
- [Toward Fully Self-Supervised Multi-Pitch Estimation](https://arxiv.org/abs/2402.15569) - Cwitkowitz & Duan, 2024. [Code](https://github.com/cwitkowitz/ss-mpe).
- [Investigating an Overfitting and Degeneration Phenomenon in Self-Supervised Multi-Pitch Estimation](https://arxiv.org/abs/2506.23371) - Cwitkowitz & Duan, ISMIR 2025.
- [Count the Notes: Histogram-Based Supervision for Automatic Music Transcription (CountEM)](https://arxiv.org/abs/2511.14250) - Yaffe, Maman, Müller & Bermano, ISMIR 2025. [Code](https://github.com/Yoni-Yaffe/count-the-notes).
- [Music Transcription with (Almost) No Supervision](https://arxiv.org/abs/2605.24193) - Shin et al., 2026. Cycle consistency with unpaired audio and scores; reports gains on GuitarSet from unlabelled guitar audio.
- [Semi-supervised piano transcription (pseudo-labelling, consistency)](https://github.com/groupmm/onsets_frames_semisup) - Strahl & Müller, ISMIR 2024.

## Multimodal and video

- [TapToTab: Video-Based Guitar Tabs Generation using AI and Audio Analysis](https://arxiv.org/abs/2409.08618) - Ghaleb et al., 2024.
- [GuiFiR: Weakly Supervised Learning of Hand Pose for Guitar Finger Reading](https://ailab.kookmin.ac.kr/publications/2026-07-15-guifir-weakly-supervised-learning-of-han/) - An, Chung, Park & Lee, IEEE Access 2026.
- [Multimodal guitar strumming transcription (audio + IMU)](https://github.com/Klangio/KLANGIO-GST-MM-T) - Murgul & Heizmann, ISMIR 2022 late-breaking.

## Tablature generation and synthesis

- [Automatic Composition of Guitar Tabs by Transformers and Groove Modeling](https://arxiv.org/abs/2008.01431) - Chen et al., ISMIR 2020.
- [DadaGP: A Dataset of Tokenized GuitarPro Songs for Sequence Models](https://arxiv.org/abs/2107.14653) - Sarmento et al., ISMIR 2021.
- [GTR-CTRL: Instrument and Genre Conditioning for Guitar-Focused Music Generation with Transformers](https://arxiv.org/abs/2302.05393) - Sarmento et al., EvoMUSART 2023.
- [ShredGP: Guitarist Style-Conditioned Tablature Generation](https://arxiv.org/abs/2307.05324) - Sarmento et al., CMMR 2023.
- [ProgGP: From GuitarPro Tablature Neural Generation To Progressive Metal Production](https://arxiv.org/abs/2307.05328) - Loth et al., 2023.
- [Guitar Tablature Generation with Deep Learning](https://qmro.qmul.ac.uk/xmlui/handle/123456789/98872) - Sarmento, PhD thesis, QMUL 2024.
- [Rhythm Guitar Tablature Continuation Through Picking Pattern Generation](https://reference-global.com/article/10.5334/tismir.368) - D'Hooge, Déguernel & Bigo, TISMIR 2026.

## General music transcription relevant to guitar

- [Onsets and Frames: Dual-Objective Piano Transcription](http://arxiv.org/abs/1710.11153) - Hawthorne et al., 2017.
- [Adversarial Learning for Improved Onsets and Frames Music Transcription](http://arxiv.org/abs/1906.08512) - Kim & Bello, 2019.
- [Multitask Learning for Polyphonic Piano Transcription, a Case Study](https://arxiv.org/abs/1902.04390) - Kelz, Böck & Widmer, 2019.
- [High-resolution Piano Transcription with Pedals by Regressing Onset and Offset Times](https://arxiv.org/abs/2010.01815) - Kong et al., 2020. The backbone most recent guitar note transcribers are fine-tuned from.
- [MT3: Multi-Task Multitrack Music Transcription](https://arxiv.org/abs/2111.03017) - Gardner et al., 2021.
- [A Lightweight Instrument-Agnostic Model for Polyphonic Note Transcription and Multipitch Estimation (Basic Pitch)](https://arxiv.org/abs/2203.09893) - Bittner et al., ICASSP 2022.
- [Multitrack Music Transcription with a Time-Frequency Perceiver](https://arxiv.org/abs/2306.10785) - Lu et al., 2023.
- [YourMT3+: Multi-instrument Music Transcription with Enhanced Transformer Architectures and Cross-dataset Stem Augmentation](https://arxiv.org/abs/2407.04822) - Chang et al., MLSP 2024.
- [MuScriptor: An Open Model for Multi-Instrument Music Transcription](https://arxiv.org/abs/2607.08168) - Rouard et al., ISMIR 2026. Open-weight multi-instrument transcription model.
- [DiffRoll: Diffusion-based Generative Music Transcription with Unsupervised Pretraining Capability](https://arxiv.org/abs/2210.05148) - Cheuk et al., 2022.
- [Joint Transcription of Lead, Bass, and Rhythm Guitars Based on a Factorial Hidden Semi-Markov Model](https://ieeexplore.ieee.org/document/8682817) - Shibata et al., ICASSP 2019.
- [Music Theory Inspired Policy Gradient Method for Piano Music Transcription](https://nips2018creativity.github.io/doc/music_theory_inspired_policy_gradient.pdf) - Li & Qu, 2018.

## Code and tools

### Research code

- [amt-tools](https://github.com/cwitkowitz/amt-tools) - Transcription framework with a reference TabCNN re-implementation used by many follow-ups.
- [tab-cnn](https://github.com/andywiggins/tab-cnn) - Original TabCNN.
- [guitar-transcription-continuous](https://github.com/cwitkowitz/guitar-transcription-continuous) - FretNet.
- [Noise2Fret](https://github.com/RiccardoVib/Noise2Fret) - Diffusion-based audio-to-tablature.
- [YourMT3](https://github.com/mimbres/YourMT3) - Multi-instrument transcription.
- [MuScriptor](https://github.com/muscriptor/muscriptor) - Open-weight multi-instrument transcription.
- [Basic Pitch](https://github.com/spotify/basic-pitch) - Lightweight instrument-agnostic note transcription.
- [e2e-agt](https://github.com/lucasgris/e2e-agt) - End-to-end tablature transcription with cross-entropy and CTC training.

### Applications

- [NeuralNote](https://github.com/DamRsn/NeuralNote) - Audio-to-MIDI plugin built on Basic Pitch.
- [guitab](https://github.com/DanieleMorotti/guitab) - Solo guitar audio to Guitar Pro file.
- [Klangio Guitar2Tabs](https://klang.io/guitar2tabs/) - Commercial audio-to-tab service.
- [AnthemScore](https://www.lunaverus.com/) - Commercial transcription software with tab output.
- [Robotaba](https://github.com/gburlet/robotaba) - Early online guitar tablature transcription framework.
- [Audiogram](https://github.com/nypublicradio/audiogram) - Turn audio into a shareable video.

## Classic and pre-deep-learning work

- [Automatic Guitar Tablature Transcription Online](http://digitool.library.mcgill.ca/webclient/StreamGate?folder_id=0&dvs=1568584947861~691) - Thesis by Gregory D. Burlet, McGill University, 2013.
- [Isolated guitar transcription using a deep belief network](https://peerj.com/articles/cs-109/) - Burlet & Hindle, PeerJ Computer Science 2017.
- [Automatic Transcription of Guitar Chords and Fingering from Audio](https://ieeexplore.ieee.org/document/6064873) - Barbancho et al., IEEE TASLP 2012. Fingering configurations with HMMs.
- [Automatic Real-Time Electric Guitar Audio Transcription](https://ieeexplore.ieee.org/document/5946418) - Fiss & Kwasinski, ICASSP 2011.
- [A segmentation-based prototype to compute string instruments fingering](http://pgp.unito.it/~anselma/pdf/RadicioniAnselmaLombardoCIM04.pdf) - Radicioni, Anselma & Lombardo, 2004. Graph-search fingering model.
- [Diferentes abordagens evolutivas aplicadas no processo de transcrição automática de partituras musicais em tablaturas](http://search.ebscohost.com/login.aspx?direct=true&db=cat07269a&AN=utfpr.277940&lang=pt-br&site=eds-live&scope=site) - Ramos, Sanches & Silla Jr., UTFPR 2016. Evolutionary algorithms for score-to-tab (in Portuguese).

## Notes on evaluation

- GuitarSet has no official split. Papers use at least four incompatible protocols (6-fold by player, random split by track, and two different held-out test sets), so numbers are comparable only within a protocol.
- Frame-level tablature F1 and disambiguation rate hide poor note-level output. Report note-level, string-dependent metrics as well.
- Cross-dataset (zero-shot) evaluation on GAPS, GOAT, EGDB, EGSet12 or Guitar-TECHS is increasingly expected alongside GuitarSet cross-validation.

## Contributing

Pull requests are welcome. Please add a link, the venue and year, and a one-line description.
