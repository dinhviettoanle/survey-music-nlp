# Natural Language Processing Methods for Symbolic Music Generation and Information Retrieval Systems: a Survey
Authors: Dinh-Viet-Toan Le, Louis Bigo, Mikaela Keller, Dorien Herremans

- [Representations](#representations)
  - [Time-slice-based tokenization](#time-slice-based-tokenization)
  - [Event-based tokenization](#event-based-tokenization)
    - [Elementary tokens](#elementary-tokens)
    - [Composite tokens](#composite-tokens)
- [Models](#models)
  - [Recurrent models](#recurrent-models)
    - [RNN](#rnn)
    - [LSTM](#lstm)
    - [GRU](#gru)
  - [Attention-based models](#attention-based-models)
    - [End-to-end models](#end-to-end-models)
      - [Transformer decoder-only architecture](#transformer-decoder-only-architecture)
      - [Transformer encoder-decoder architecture](#transformer-encoder-decoder-architecture)
      - [Model combinations](#model-combinations)
    - [Pre-trained models](#pre-trained-models)
      - [Transformer encoder-only architecture](#transformer-encoder-only-architecture)
      - [Transformer decoder-only architecture](#transformer-decoder-only-architecture-1)
      - [Transformer encoder-decoder architecture](#transformer-encoder-decoder-architecture-1)
      - [Comparative studies](#comparative-studies)
- [Citation](#citation)


## Representations

### Time-slice-based tokenization

| **Tokenization** | **Reference** | **Data** |
| ---------------- | ------------- | -------- |
|                  |               |          |

### Event-based tokenization

#### Elementary tokens

| **Tokenization**                    | **Score-based / Performance-based** | **Alphabet**                                                                                                                                                                                                                                                                                                   | **Grouping**        | **Vocab. size** | **Data**    |
| ----------------------------------- | ----------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------- | --------------- | ----------- |
| [ABC notation]()                    | Score                               | Text alphabet                                                                                                                                                                                                                                                                                                  | [Bar patching]()    | N/A             | Monophonic  |
| [MIDI-like (2018)]()                | Performance                         | <details>`<Note-ON>` (MIDI value) <br> `<Note-OFF>` (MIDI value) <br> `<Time-shift>` (absolute time) `<Velocity>` (integer)</details>                                                                                                                                                                          | [BPE]() [Unigram]() | 388             | Piano       |
| [LakhNES (2019)]()                  | Performance                         | <details>`<Note-ON-[Trk]>` (MIDI value) <br> `<Note-OFF-[Trk]>` (MIDI value) <br> `<Time-shift>` (absolute time) </details>                                                                                                                                                                                    | -                   | 630             | Multi-track |
| [REMI (2020)]()                     | Score                               | <details>`<Pitch>` (MIDI value) <br> `<Duration>` (music time) <br> `<Velocity>` (integer) <br> `<Bar>` <br> `<Position>` (music time) <br> `<Chord>` (class)</details>                                                                                                                                        | [BPE]() [Unigram]() | 332             | Piano       |
| [REMI+ (2022)]()                    | Score                               | <details>REMI alphabet + metadata: <br> `<BPM>` (integer) <br> `<Key>` (class) <br> `<Instrument>` (class) <br> `<Time-Signature>` (class) <br> `<Pitch-range>` (class) <br> `<Number-of-measures>` (number) <br> `<Min-velocity>` (integer) <br> `<Max-velocity>` (integer) <br> `<Rhythm>` (class)</details> | -                   | 728             | Multi-track |
| [MusIAC (2022)]()                   | Score                               | <details>REMI alphabet + control info: <br> `<Tensile-train>` (class) <br> `<Cloud diameter>` (class) <br> `<Density>` (class) <br> `<Polyphony>` (class) <br> `<Occupation>` (class)</details>                                                                                                                | -                   | 360             | Multi-track |
| [Gover & al. (2022)]()              | Score                               | <details>`<Pitch>` (MIDI value) <br> `<Duration>` (music time) <br> `<Position>` (music time) <br> `<Bar>` <br> `<Hand>` (class)</details>                                                                                                                                                                     | -                   | N/A             | Piano       |
| [Wu & Yang (2023)]() (MuseMorphose) | Score                               | <details>`<Pitch-[Trk]>` (MIDI value) <br> `<Duration-[Trk]>` (music time) <br> `<Velocity-[Trk]>` (integer) <br> `<Bar>` <br> `<Position>` (music time) <br> `<Tempo>` (integer)</details>                                                                                                                    | -                   | 3440            | Multi-track |
| [MultiTrack (2020)]() (MMM)         | Performance                         | <details>`<Start-piece>` <br> `<Start-track>/<End-track>` <br> `<Start-bar>/<End-bar>` <br> `<Start-fill><End-fill>` <br> `<Note-ON>` (MIDI value) <br> `<Note-OFF>` (MIDI value) <br> `<Time-shift>` (absolute time) <br> `<Instrument>` (class) <br> `<Density level>` (integer)</details>                   | -                   | 440             | Multi-track |
| [MMR (2022)]() (SymphonyNet)        | Score                               | <details>`<Start-score>/<End-score>` <br> `<Start-bar>/<End-bar>` <br>  `<Chord>` (class) <br> `<Change-track>` <br> `<Position>` (integer) <br> `<Pitch>` (MIDI value) <br> `<Duration>` (music time)</details>                                                                                               | [BPE]()             | N/A             | Multi-track |
| [TSD (2023)]()                      | Performance                         | <details>`<Pitch>` (MIDI value) <br> `<Velocity>` (integer) <br> `<Duration>` (absolute time) <br> `<Time-shift>` (absolute time) <br> `<Rest>` (absolute time) <br> `<Program>` (class)</details>                                                                                                             | [BPE]()             | 249             | Multi-track |
| [Structured (2021)]()               | Performance                         | <details>`<Pitch>` (MIDI value) <br> `<Velocity>` (integer) <br> `<Duration>` (absolute time) <br> `<Time-shift>` (absolute time)</details>                                                                                                                                                                    | -                   | 428             | Piano       |
| [Chen & al. (2020)]()               | Score (tabs)                        | <details>`<Pitch>` (MIDI value) <br> `<Duration>` (music time) <br> `<Velocity>` (integer) <br> `<Position>` (music time) <br> `<Bar>` (integer) <br> `<String>` (integer) <br> `<Fret>` (integer) <br> `<Technique>` (class) <br> `<Grooving>` (class)</details>                                              | -                   | 231             | Guitar      |
| [Li & al. (2023)]()                 | Score                               | <details>`<Pitch-class>` (class) <br> `<Octave>` (integer) <br> `<Duration>` (music time) <br> `<Bar>` (integer) <br> `<Position>` (music time) <br> `<Velocity>` (integer)</details>                                                                                                                          | -                   | N/A             | Monophonic  |
| [DadaGP (2021)]()                   | Score (tabs)                        | <details>`<Start><End>` <br> `<Instrument:note>` (class) <br> `<String>` (integer) <br> `<Fret>` (integer) <br> `<Drums:note>` (MIDI value) <br> `<Effect>` (class) <br> `<Wait>` (integer)</details>                                                                                                          | [BPE]() [Unigram]() | 2140            | Guitar      |


#### Composite tokens

| **Tokenization**                        | **Musical features**                                                                                                                                                                                                                                           | **Embedded object**                             | **Data**                                 |
| --------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------- | ---------------------------------------- |
| [PiRhDy (2020)]()                       | <details>`<Chroma>` (class) <br> `<Octave>` (integer) <br> `<Inter-onset-interval>` (music time) <br> `<Note-state>` (class) <br> `<Velocity>` (integer)</details>                                                                                             | 5-long vector                                   | Multi-track                              |
| [Compound Word (2021)]()                | <details>`<Family>` (class) <br> `<Time-signature>` (class) <br> `<Bar>` (integer) <br> `<Beat>` (music time) <br> `<Chord>` (class) <br> `<Tempo>` (integer) <br> `<Pitch>` (MIDI value) <br> `<Duration>` (music time) <br> `<Velocity>` (integer)</details> | Note / Event grouping                           | Piano                                    |
| [Di & al. (2021)]()                     | <details>`<Type>` (class) <br> `<Bar/beat>` (integer) <br> `<Density>` (class) <br> `<Strenth>` (class) <br> `<Instrument>` (integer) <br> `<Pitch>` (MIDI value) <br> `<Duration>` (music time)</details>                                                     | Note / Event grouping                           | Multi-track                              |
| [Octuple (2021)]() (MusicBERT)          | <details>`<Time-signature>` (class) <br> `<Tempo>` (integer) <br> `<Bar>` (integer) <br> `<Position>` (music time) <br> `<Instrument>` (class) <br> `<Pitch>` (MIDI value) <br> `<Duration>` (music time) <br> `<Velocity>` (integer)</details>                | 8-long vector                                   | Multi-track                              |
| [MuMIDI (2020)]()                       | <details>`<Bar>` <br> `<Position>` (music time) <br> `<Tempo>` (integer) <br> `<Track>` (class) <br> `<Chord>` (class) <br> `<Pitch>` (MIDI value) <br> `<Drum>` (MIDI value) <br> `<Velocity>` (integer) <br> `<Duration>` (music time)</details>             | Note / Event grouping                           | Multi-track                              |
| [Wang & al. (2021)]() (MuseBERT)        | <details>`<Onset>` (music time) <br> `<Pitch>` (MIDI value) <br> `<Duration>` (music time) <br> + factorized properties</details>                                                                                                                              | Matrices of factorized attributes and relations | Multi-track                              |
| [Dong & al. (2023)]() (MMT)             | <details>`<Type>` (class) <br> `<Beat>` (integer) <br> `<Position>` (music time) <br> `<Pitch>` (MIDI value) <br> `<Duration>` (music time) <br> `<Instrument>` (class)</details>                                                                              | 6-long vector                                   | Multi-track                              |
| [Luo & al. (2020)]() (MG-VAE)           | <details>`<Pitch>` (class) <br> `<Interval>` (number) <br> `<Rhythm>` (class)</details>                                                                                                                                                                        | 3-long vector                                   | Monophonic                               |
| [Zhang (2020)]()                        | <details>`<Program>` (class) <br> `<Pitch>` (integer) <br> `<Velocity>` (integer)</details>                                                                                                                                                                    | 3-long vector + Time-shift                      | Multi-track                              |
| [Zixun & al. (2021)]()                  | <details>`<Pitch>` (one-hot) <br> `<Duration>` (one-hot) <br> `<Current-chord>` (one-hot) <br> `<Next-chord>` (one-hot) <br> `<Bar>` (one-hot)</details>                                                                                                       | 246-long vector                                 | Lead sheet                               |
| [Makris & al. (2022)]()                 | <details>Encoder input: <br> `<Onset>` (number) <br> `<Group>` (class) <br> `<Type>` (class) <br> `<Duration>` (music time or none) <br> `<Value>` (any - depends on type) <br> Decoder output: <br> `<Onset>` (number) <br> `<Drums>` (integer)</details>     | Note / Event grouping                           | Encoder: Multi-track <br> Decoder: Drums |
| [Dalmazzo & al. (2023)]() (Chordinator) | <details>`<Chord-root>` (class) <br> `<Chord-nature>` (class) <br> `<Chord-extensions>` (class) <br> `<MIDI-array>` (multi-hot) <br> `<Slash-chord>` (boolean)</details>                                                                                       | 8-long vector                                   | Chord sequences                          |

## Models

### Recurrent models

#### RNN 

| **Model**          | **Recurrent unit** | **Architecture** | **Data**    | **Representation**      | **Tasks**       |
| ------------------ | ------------------ | ---------------- | ----------- | ----------------------- | --------------- |
| [RNN-RBM (2012)]() | Vanilla RNN        | RBM + RNN        | Multi-track | Time-slice (piano roll) | Free generation |
| [RNN-DBN (2014)]() | Vanilla RNN        | RBM + DBN + RNN  | Multi-track | Time-slice (piano roll) | Free generation |

#### LSTM 

| **Model**                         | **Recurrent unit** | **Architecture**                         | **Data**        | **Representation**                                          | **Tasks**                                          |
| --------------------------------- | ------------------ | ---------------------------------------- | --------------- | ----------------------------------------------------------- | -------------------------------------------------- |
| [Folk-RNN (2016)]()               | LSTM               | LSTM                                     | Monophonic      | ABC notation                                                | Free generation                                    |
| [C-RNN-GAN (2016)]()              | LSTM               | GAN + Bi-LSTM                            | Multi-track     | Pitch + duration + time-shift + velocity (composite tokens) | Free generation                                    |
| [Song from Pi (2016)]()           | LSTM               | Hierarchical + LSTM                      | Multi-track     | Custom features (composite tokens)                          | Free generation (melody, chord, drum generation)   |
| [Melody / Attention-RNN (2016)]() | LSTM               | LSTM (+ Attention)                       | Monophonic      | Note-ON / Note-OFF                                          | Priming                                            |
| [DeepBach (2017)]()               | LSTM               | Bi-LSTM                                  | 4-part chorales | Time-slice-based                                            | Harmonization <br> Free generation                 |
| [Anticipation-RNN (2017)]()       | LSTM               | LSTM                                     | Monophonic      | Pitch + duration (time-slice-based)                         | Infilling                                          |
| [JamBot (2017)]()                 | LSTM               | LSTM                                     | Multi-track     | Time-slice (piano roll)                                     | Chord generation <br> Chord-conditioned generation |
| [Note-RNN / RL Tuner (2017)]()    | LSTM               | LSTM (+ Reinforcement Learning)          | Monophonic      | Note-ON / Note-OFF                                          | Free generation                                    |
| [PerformanceRNN (2018)]()         | LSTM               | LSTM                                     | Piano           | MIDI-like                                                   | Expressive performance generation                  |
| [Chen & Su (2018)]()              | LSTM               | Bi-LSTM                                  | Piano           | Time-slice (piano roll)                                     | Roman Numeral Analysis                             |
| [StructureNet (2018)]()           | LSTM               | LSTM                                     | Monophonic      | Custom features (composite tokens)                          | Free generation                                    |
| [Music-VAE (2018)]()              | LSTM               | VAE + LSTM                               | Monophonic      | MIDI-like                                                   | Samples interpolation <br> Free generation         |
| [JazzGAN (2018)]()                | LSTM               | GAN + LSTM                               | Lead sheet      | Pitch + duration + chord (event-based)                      | Chord-conditioned generation                       |
| [DeepJ]()                         | LSTM               | Biaxial LSTM                             | Piano           | Time-slice (piano roll)                                     | Free generation <br> Style embedding analysis      |
| [Chen & al. (2019)]()             | LSTM               | Bi-LSTM                                  | Lead sheet      | Time-slice (piano roll)                                     | Chord-conditioned generation                       |
| [Makris & al. (2019)]()           | LSTM               | LSTM (Drums) / Feed-forward (Context)    | Multi-track     | Drums: event-based <br> Context: time-slice                 | Drums accompaniment generation                     |
| [MahlerNet (2019)]()              | LSTM               | VAE + Bi-LSTM                            | Multi-track     | Event-based                                                 | Samples interpolation                              |
| [GrooVAE (2019)]()                | LSTM               | VAE + Bi-LSTM                            | Drums           | Time-slice (drumroll)                                       | Drum Infilling <br> Tap2Drum <br> Humanization     |
| [Wu & al. (2019)]()               | LSTM               | Hierarchical + Bi-LSTM                   | Monophonic      | Note-ON / Note-OFF                                          | Structure-conditioned generation                   |
| [VirtuosoNet (2019)]()            | LSTM               | Hierarchical + VAE + Bi-LSTM + Attention | Piano           | Custom features (composite tokens)                          | Expressive performance generation                  |
| [Amadeus (2019)]()                | LSTM               | Hierarchical + Reinforcement Learning    | Piano           | Pitch + duration (event-based)                              | Free generation                                    |
| [MuseAE (2020)]()                 | LSTM               | Adversarial Auto-encoder + LSTM          | Multi-track     | Time-slice (piano roll)                                     | Samples interpolation <br> Embedding analysis      |
| [Jin & al. (2020)]()              | LSTM               | LSTM + Reinforcement Learning            | Multi-track     | Time-slice (piano roll)                                     | Free generation                                    |
| [GGA-MG (2020)]()                 | LSTM               | Bi-LSTM + Genetic Algorithm              | Monophonic      | ABC notation                                                | Free generation                                    |
| [Yu & al. (2021)]()               | LSTM               | GAN + LSTM                               | Monophonic      | Pitch + duration (event-based)                              | Lyrics-conditioned generation                      |
| [CM-HRNN (2021)]()                | LSTM               | Hierarchical + LSTM                      | Lead sheet      | Pitch + duration + chord + bar (composite tokens)           | Chord-conditioned generation                       |
| [Keerti & al. (2022)]()           | LSTM               | Bi-LSTM + Attention                      | Monophonic      | Pitch + duration (event-based)                              | Sequence reconstruction                            |
| [LStoM (2022)]()                  | LSTM               | Bi-LSTM                                  | Multi-track     | Custom features (event-based)                               | Melody extraction                                  |
| [Turker & al. (2022)]()           | LSTM               | VAE + LSTM                               | Piano           | Note-ON / Note-OFF                                          | Sequence reconstruction <br> Latent space analysis |

#### GRU

| **Model**                | **Recurrent unit** | **Architecture**         | **Data**            | **Representation**                            | **Tasks**                                                               |
| ------------------------ | ------------------ | ------------------------ | ------------------- | --------------------------------------------- | ----------------------------------------------------------------------- |
| [MIDI-VAE (2018)]()      | GRU                | VAE + GRU                | Multi-track         | Time-slice (piano roll)                       | Style transfer <br> Samples interpolation                               |
| [XiaoIce Band (2018)]()  | GRU                | GRU + Attention          | Multi-track         | Pitch + duration + chord (event-based)        | Chord-conditioned generation <br> Arrangement generation                |
| [Songwriter (2019)]()    | GRU                | GRU + Attention          | Monophonic          | Pitch + duration (event-based)                | Lyrics-conditioned generation                                           |
| [Yang & al. (2019)]()    | GRU                | VAE + bi-GRU             | Lead sheet          | Time-slice (piano roll) + chords (chromagram) | Melody contour-conditioned generation <br> Chord-conditioned generation |
| [BUTTER (2020)]()        | GRU                | VAE + GRU                | Monophonic          | Time-slice (piano roll)                       | Text-based query <br> Music captioning <br> Text-conditioned generation |
| [Kong & al. (2020)]()    | GRU                | Bi-GRU                   | Piano               | Time-slice (piano roll)                       | Composer classification                                                 |
| [MG-VAE (2020)]()        | GRU                | VAE + Bi-GRU             | Monophonic          | Pitch + interval + duration (event-based)     | Free generation                                                         |
| [PianoTree-VAE (2020)]() | GRU                | VAE + bi-GRU             | Piano / Multi-track | Time-slice (pianoroll / MIDI-like)            | Samples interpolation <br> Free generation <br> Embedding analysis      |
| [Su & al. (2022)]()      | GRU                | Bi-GRU + CNN + Attention | Monophonic          | Pitch + duration (time-slice-based)           | Free generation                                                         |

### Attention-based models

#### End-to-end models

##### Transformer decoder-only architecture

| **Model**                               | **Base model**                            | **MIR mechanism**                               | **Data**                  | **Representation**                    | **Tasks**                                                           |
| --------------------------------------- | ----------------------------------------- | ----------------------------------------------- | ------------------------- | ------------------------------------- | ------------------------------------------------------------------- |
| [Music Transformer (2018)]()            | Transformer decoder                       | Relative attention                              | Piano / Choral            | MIDI-like                             | Priming <br> Harmonization                                          |
| [Chen & al. (2020)]()                   | Transformer-XL                            | -                                               | Guitar tabs               | REMI-derived (tabs)                   | Free tabs generation                                                |
| [Pop Music Transformer (2020)]()        | Transformer-XL                            | -                                               | Piano                     | REMI                                  | Priming <br> Free generation                                        |
| [Jazz Transformer (2020)]()             | Transformer-XL                            | -                                               | Lead sheet                | REMI-derived (chords)                 | Free generation                                                     |
| [PopMAG (2020)]()                       | Transformer-XL                            | -                                               | Multi-track               | MuMIDI                                | Accompaniment generation                                            |
| [Wu & al. (2020)]()                     | Transformer-XL                            | -                                               | Piano                     | MIDI-like-derived (composite tokens)  | Free generation                                                     |
| [Di & al. (2020)]()                     | Transformer decoder                       | -                                               | Multi-track               | Compound-word-derived (rhythm family) | Video-to-music                                                      |
| [Chang & al. (2021)]()                  | XLNet                                     | Relative bar encoding                           | Piano                     | Compound Word                         | Infilling                                                           |
| [Compound Word Transformer (2021)]()    | Linear Transformer decoder                | -                                               | Piano                     | Compound Word                         | Priming <br> Free generation                                        |
| [Sarmento & al. (2021)]()               | Transformer-XL                            | -                                               | Guitar tabs + multi-track | DadaGP                                | Metadata-conditioned generation                                     |
| [Sulun & al. (2022)]()                  | Music Transformer                         | -                                               | Multi-track               | MIDI-like                             | Emotion-conditioned generation                                      |
| [ComMU (2022)]()                        | Transformer-XL                            | -                                               | Multi-track               | REMI + metadata                       | Metadata-conditioned generation <br> Multi-track combination        |
| [SymphonyNet (2022)]()                  | Linear Transformer                        | 3-D positional encoding                         | Orchestral                | MMR                                   | Chord-conditioned generation <br> Priming <br> Free generation      |
| [Li & al. (2023)]()                     | Transformer-XL                            | -                                               | Lead sheet                | REMI-derived (pitch class)            | Free generation                                                     |
| [Multitrack Music Transformer (2023)]() | Transformer decoder                       | -                                               | Orchestral                | MMT                                   | Free generation <br> Instrument-conditioned generation <br> Priming |
| [GTR-CTRL (2023)]()                     | Transformer-XL                            | -                                               | Guitar tabs + multi-track | DadaGP                                | Instrument-conditioned generation <br> Genre-conditioned generation |
| [ShredGP (2023)]()                      | Transformer-XL                            | -                                               | Guitar tabs               | DadaGP                                | Style-conditioned generation                                        |
| [Choir Transformer (2023)]()            | Transformer decoder                       | Relative attention                              | 4-part chorales           | Chord + pitch (event-based)           | Harmonization                                                       |
| [Guo & al. (2023)]()                    | Transformer decoder with custom attention | Fundamental music embedding <br> RIPO attention | Monophonic                | FME                                   | Priming                                                             |
| [Compose & Embellish (2023)]()          | Transformer decoder                       | -                                               | Multi-track               | REMI                                  | Lead sheet priming <br> Accompaniment refinement                    |
| [Tang & al. (2023)]()                   | Transformer decoder                       | -                                               | Piano                     | Octuple                               | Expressive performance generation                                   |
| [Angioni & al. (2023)]()                | Transformer decoder                       | -                                               | Multi-track               | TSD-like                              | Style classification                                                |
| [Chordinator (2023)]()                  | minGPT (no pre-training)                  | -                                               | Chords                    | Custom chord features (+ MIDI array)  | Chord generation                                                    |


##### Transformer encoder-decoder architecture

| **Model**                      | **Base model**                                      | **MIR mechanism**                                 | **Data**    | **Representation**                                        | **Tasks**                                   |
| ------------------------------ | --------------------------------------------------- | ------------------------------------------------- | ----------- | --------------------------------------------------------- | ------------------------------------------- |
| [Transformer-VAE (2020)]()     | Transformer encoder-decoder                         | -                                                 | Monophonic  | Pitch + duration (time-slice-based)                       | Priming                                     |
| [Harmony Transformer (2021)]() | Transformer encoder-decoder                         | -                                                 | Piano       | Pianoroll time-slices                                     | Roman Numeral Analysis                      |
| [Makris & al. (2021)]()        | Transformer encoder-decoder                         | -                                                 | Lead sheet  | Encoder: bar features / Decoder: chord + pitch + duration | Emotion-conditioned generation              |
| [Liutkus & al. (2021)]()       | Performer                                           | Stochastic positional encoding                    | Multi-track | REMI / MIDI-like-derived (multi-track)                    | Free generation <br> Groove continuation    |
| [Gover & al. (2022)]()         | BART                                                | -                                                 | Piano       | REMI-derived (hands token)                                | Arrangement generation                      |
| [Museformer (2022)]()          | Transformer encoder-decoder with custom attention   | Fine-/coarse-grained attention <br> Bar selection | Multi-track | REMI                                                      | Free generation                             |
| [Theme Transformer (2022)]()   | Transformer encoder-decoder                         | Theme-aligned positional encoding                 | Multi-track | REMI-derived (theme tokens)                               | Theme-conditioned generation                |
| [FIGARO (2022)]()              | Transformer encoder-decoder                         | -                                                 | Multi-track | REMI+                                                     | Controllable generation                     |
| [MuseMorphose (2023)]()        | Transformer encoder + Transformer-XL                | In-attention conditioning                         | Piano       | REMI-derived (multi-track)                                | Style transfer <br> Controllable generation |
| [Accomontage 3 (2023)]()       | Transformer encoder-decoder                         | Instrument embedding                              | Multi-track | Piano roll time-slices                                    | Accompaniment generation                    |
| [TeleMelody (2023)]()          | Transformer encoder-decoder                         | -                                                 | Monophonic  | Bar + position + pitch + duration (event-based)           | Lyrics-to-melody                            |
| [MuseCoco (2023)]()            | Text2Attr: BERT <br> Attr2Music: Linear Transformer | -                                                 | Multi-track | REMI                                                      | Text-to-MIDI                                |

##### Model combinations

| **Model**                  | **Base model**                                                                                          | **MIR mechanism**    | **Data**    | **Representation**                        | **Tasks**                                                          |
| -------------------------- | ------------------------------------------------------------------------------------------------------- | -------------------- | ----------- | ----------------------------------------- | ------------------------------------------------------------------ |
| [Zhang (2020)]()           | Generator: Transformer decoder <br>Discriminator: Transformer encoder                                   | -                    | Multi-track | MIDI-like-derived (composite tokens)      | Free generation                                                    |
| [Transformer-GAN (2021)]() | Generator: Transformer-XL <br>Discriminator: BERT                                                       | -                    | Piano       | MIDI-like                                 | Free generation                                                    |
| [Dai & al. (2021)]()       | Generator: Transformer encoder <br> Discriminator: LSTM                                                 | -                    | Multi-track | Pitch + rhythm (event-based)              | Structure-conditioned generation <br> Chord conditioned generation |
| [Choi & al. (2021)]()      | Chord encoder: Bi-LSTM <br> Rhythm decoder: Transformer decoder <br> Pitch decoder: Transformer decoder | -                    | Lead sheet  | Pitch + rhythm + chord (time-slice-based) | Chord-conditioned generation                                       |
| [Makris & al. (2022)]()    | Bi-LSTM encoder / Transformer encoder                                                                   | -                    | Multi-track | Compound-word-derived                     | Drums accompaniment generation                                     |
| [Neves & al. (2022)]()     | Generator: Linear Transformer <br> Discriminator: Linear Transformer                                    | Local prediction map | Piano       | REMI                                      | Emotion-conditioned generation                                     |
| [Q&A (2023)]()             | PianoTree-VAE <br> Transformer decoder                                                                  | Instrument embedding | Multi-track | Piano roll time-slices                    | Accompaniment generation                                           |
| [Duan & al. (2023)]()      | Generator: Transformer encoder <br> Discriminator: LSTM                                                 | -                    | Monophonic  | Pitch + duration + rest (event-based)     | Lyrics-to-melody                                                   |
| [Video2Music (2023)]()     | GRU + Transformer encoder-decoder                                                                       | -                    | Multi-track | MIDI-like                                 | Video-to-music                                                     |




#### Pre-trained models

##### Transformer encoder-only architecture

| **Model**                 | **Base model**                                     | **MIR mechanism**                                                 | **Data**    | **Representation**             | **Tasks**                                                                                           |
| ------------------------- | -------------------------------------------------- | ----------------------------------------------------------------- | ----------- | ------------------------------ | --------------------------------------------------------------------------------------------------- |
| [MuseBERT (2021)]()       | BERT                                               | Generalized relative positional encoding                          | Multi-track | MuseBERT representation        | Controllable generation <br> Chord analysis <br> Accompaniment refinement                           |
| [MidiBERT-Piano (2021)]() | BERT                                               | -                                                                 | Piano       | REMI / Compound Word           | Melody extraction <br> Velocity prediction <br> Composer classification <br> Emotion classification |
| [MusicBERT (2021)]()      | RoBERTa                                            | Bar-level masking                                                 | Multi-track | Octuple                        | Melody completion <br> Accompaniment suggestion <br> Genre classification <br> Style classification |
| [MRBERT (2023)]()         | BERT                                               | Melody/rhythm cross-attention                                     | Lead sheet  | Pitch + duration (event-based) | Free generation <br> Infilling <br> Chord analysis                                                  |
| [SoloGPBERT (2023)]()     | BERT                                               | -                                                                 | Guitar tabs | DadaGP                         | Guitar player classification                                                                        |
| [Shen & al. (2023)]()     | MidiBERT-Piano                                     | Pre-training tasks <br> (quad-attribute masking / key prediction) | Multi-track | Compound Word simplified       | Melody extraction <br> Velocity prediction <br> Composer classification <br> Emotion classification |
| [CLaMP (2023)]()          | Text encoder: DislRoBERTa <br> Music encoder: BERT | -                                                                 | Lead sheet  | ABC notation-derived           | Text-based semantic music search <br> Music recommandation <br> Music classification                |



##### Transformer decoder-only architecture

| **Model**                | **Base model**      | **MIR mechanism**                       | **Data**    | **Representation**                           | **Tasks**                                                                 |
| ------------------------ | ------------------- | --------------------------------------- | ----------- | -------------------------------------------- | ------------------------------------------------------------------------- |
| [LakhNES (2019)]()       | Transformer-XL      | -                                       | Multi-track | MIDI-like                                    | Free generation                                                           |
| [Musenet (2019)]()       | GPT-2               | Timing embedding / Structural embedding | Multi-track | MIDI-like                                    | Priming                                                                   |
| [MMM (2020)]()           | GPT-2               | -                                       | Multi-track | MultiTrack representation                    | Free generation <br> Priming <br> Inpainting <br> Controllable generation |
| [DBTMPE (2021)]()        | Transformer encoder | -                                       | Multi-track | Pitch combinations + durations (event-based) | Style classification                                                      |
| [Angioni & al. (2023)]() | GPT-2               | -                                       | Multi-track | TSD-like                                     | Priming                                                                   |
| [Zhang & al. (2023)]()   | GPT-3               | -                                       | Drums       | Drumroll time-slices                         | Priming                                                                   |
| [Bubeck & al. (2023)]()  | GPT-4               | -                                       | Text        | ABC notation                                 | Text-to-ABC                                                               |


##### Transformer encoder-decoder architecture

| **Model**             | **Base model**                | **MIR mechanism** | **Data**    | **Representation**             | **Tasks**                                                                                           |
| --------------------- | ----------------------------- | ----------------- | ----------- | ------------------------------ | --------------------------------------------------------------------------------------------------- |
| [MusIAC (2022)]()     | Transformer encoder-decoder   | -                 | Multi-track | REMI                           | Infilling <br> Controllable generation                                                              |
| [Li & al. (2023)]()   | Transformer encoder-decoder   | -                 | Lead sheet  | Pitch + duration (event-based) | Harmony analysis <br> Chord generation                                                              |
| [Fu & al. (2023)]()   | MusicBERT + Music Transformer | -                 | Multi-track | Octuple                        | Melody completion <br> Accompaniment suggestion <br> Genre classification <br> Style classification |
| [Multi-MMLG (2023)]() | XLNet + MuseBERT              | -                 | Multi-track | Compound-word-derived          | Melody extraction                                                                                   |


##### Comparative studies

| **Model**           | **Base model**      | **MIR mechanism** | **Data**   | **Representation** | **Tasks**   |
| ------------------- | ------------------- | ----------------- | ---------- | ------------------ | ----------- |
| [Wu & al. (2023)]() | BERT / GPT-2 / BART | -                 | Lead sheet | ABC notation       | Text-to-ABC |




## Citation
If you find this useful, please cite our paper.

```
bibtex
```
