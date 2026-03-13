# JSpoke Formant Synthesizer

JSpoke is a lightweight, formant-based speech synthesis engine implemented in C++. It generates audible speech from phoneme sequences or detailed phonetic specifications using digital signal processing techniques, including glottal pulse train generation, shaped noise sources, and time-varying IIR filtering.

The synthesizer supports both interactive command-line usage and batch processing via arguments. It includes a default voice profile with predefined formant frequencies for standard English phonemes, stops, fricatives, and affricates.

## Features

- **Formant Synthesis:** Generates speech using cascaded resonators to model vocal tract characteristics.
- **Dual Input Modes:**
  - **Phoneme Mode:** Accepts space-separated phoneme strings with automatic timing and pitch assignment.
  - **Specification Mode:** Allows fine-grained control over duration, overlap, and pitch contours per phoneme.
- **Signal Processing:** Implements Butterworth filters, glottal waveform modeling with jitter/shimmer, and coarticulation handling via spline interpolation.
- **Output:** Produces standard 16-bit PCM WAV files.
- **Portability:** Written in standard C++ with no external dependencies beyond the standard library.

## Compilation

Ensure a C++ compiler (such as `g++`) is installed. Optimization flags are recommended for real-time performance.

**Standard Build:**
```bash
g++ jspoke.cpp -s -O3 -funroll-loops -o jspoke
```

**Compacted Build:**
```bash
g++ jspoke_compacted.cpp -s -O3 -funroll-loops -o jspoke_compacted
```

## Usage

### Interactive Mode
Run the executable without arguments to enter the interactive menu. This mode allows for setting parameters (pitch, sample rate, volume) and synthesizing speech interactively.

```bash
./jspoke
```

### Command-Line Mode
Use command-line flags for batch processing or script integration. Either `-phon` or `-spec` must be provided.

**Options:**
- `-phon="<text>"`: Space-separated phonemes (e.g., `"HH EH L OW"`).
- `-spec="<text>"`: Pipe-separated specifications (e.g., `"HH 0.12 0.015 95|EH 0.14 0.018 105 110"`).
- `-p=<Hz>`: Base pitch frequency (default: 115).
- `-v=<dB>`: Volume adjustment in decibels (default: 0).
- `-r=<rate>`: Sample rate in Hz (default: 44100).
- `-o=<file>`: Output WAV filename (default: output.wav).
- `-voice=<name>`: Voice preset name (default: Default).
- `-h`, `--help`: Display help message.

**Examples:**

Synthesize "hello" using default timing:
```bash
./jspoke -phon="HH EH L OW" -o=hello.wav
```

Synthesize with custom duration and pitch contour:
```bash
./jspoke -spec="HH 0.12 0.015 95|EH 0.14 0.018 105 110" -o=custom.wav
```

## Phoneme Set

The system supports ARPABET-style phonemes, including vowels, diphthongs, stops, fricatives, nasals, and approximants. Silent intervals are denoted by `SIL`. Aspirated variants (e.g., `HAE`, `HIY`) are available for specific consonant-vowel transitions.

## License

This project is licensed under the MIT License. See the LICENSE file for details.
