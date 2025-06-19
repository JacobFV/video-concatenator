# Video Concatenator 🎬

A professional command-line tool for creating cinematic video compilations with automatic intro slides and grid view finales.

## ✨ Features

- **🎬 Automatic Intro Slide**: 5-second black screen with red text listing all scenes and their durations
- **🏷️ Smart Watermarks**: Each video segment displays its filename in the bottom-right corner
- **📐 Grid View Finale**: All videos displayed simultaneously in an optimized grid layout
- **⚖️ Duration Normalization**: All videos in the grid are time-adjusted to the mean duration
- **📦 Size Optimization**: Automatic compression to stay under specified file size limits
- **🎨 Professional Styling**: Consistent red text styling with black backgrounds for readability
- **📱 Responsive Grids**: Automatic grid layout optimization based on number of videos
- **🔄 Alphabetical Sorting**: Videos are processed in alphabetical order automatically

## 🚀 Quick Start

```bash
# Basic usage
./video-concat /path/to/video/directory

# Specify output file and size limit
./video-concat -o my-compilation.mp4 -s 20 ./videos/

# Verbose mode for detailed output
./video-concat --verbose --output final.mp4 ~/Desktop/clips/
```

## 📦 Installation

### Prerequisites

Make sure you have the following dependencies installed:

- **ffmpeg** with libx264 support
- **ffprobe** (usually included with ffmpeg)
- **bc** (basic calculator)

#### macOS
```bash
brew install ffmpeg bc
```

#### Ubuntu/Debian
```bash
sudo apt update
sudo apt install ffmpeg bc
```

#### Windows (via Chocolatey)
```bash
choco install ffmpeg
# bc is typically included with Git Bash or WSL
```

### Download and Install

```bash
# Clone the repository
git clone https://github.com/JacobFV/video-concatenator.git
cd video-concatenator

# Make the script executable
chmod +x video-concat

# Optionally, add to your PATH
sudo ln -s $(pwd)/video-concat /usr/local/bin/video-concat
```

## 📖 Usage

### Command Line Options

```
video-concat [OPTIONS] <input_directory>

ARGUMENTS:
    <input_directory>    Directory containing video files to concatenate

OPTIONS:
    -o, --output FILE    Output filename (default: output.mp4)
    -s, --size SIZE      Maximum output size in MB (default: 10)
    -v, --verbose        Enable verbose output
    -h, --help          Show help message
```

### Supported Video Formats

- `.mov`, `.MOV`
- `.mp4`, `.MP4`
- `.avi`, `.AVI`
- `.mkv`, `.MKV`

### Examples

#### Basic Compilation
```bash
./video-concat ./my-videos/
```
Creates `output.mp4` with all videos from `./my-videos/` directory.

#### Custom Output and Size
```bash
./video-concat -o vacation-highlights.mp4 -s 50 ~/Videos/vacation/
```
Creates a 50MB max compilation named `vacation-highlights.mp4`.

#### Verbose Processing
```bash
./video-concat --verbose --output presentation.mp4 ./slides/
```
Shows detailed processing information while creating the compilation.

## 🎥 Output Structure

The final video includes three main sections:

### 1. Intro Slide (5 seconds)
- Black background with red text
- Lists all upcoming scenes with durations
- Example:
  ```
  This video will show the following scenes:
  
  1. beach-sunset (15s)
  2. mountain-hike (23s)
  3. city-lights (18s)
  
  Final: Grid view of all scenes (19s)
  ```

### 2. Individual Video Segments
- Each video plays in full with its original duration
- Red filename watermark in bottom-right corner
- Audio is removed for consistency
- Videos maintain their original quality and aspect ratio

### 3. Grid View Finale
- All videos displayed simultaneously
- Each video adjusted to mean duration of all videos
- Smart grid layout (2x1 for 2 videos, 2x2 for 3-4 videos, etc.)
- Individual filename labels for each grid cell
- Professional padding between grid cells

## ⚙️ Technical Details

### Video Processing Pipeline

1. **Discovery**: Recursively finds all supported video files
2. **Analysis**: Uses ffprobe to determine duration and resolution
3. **Intro Generation**: Creates text-based intro slide with scene list
4. **Watermarking**: Adds filename watermarks to each video segment
5. **Grid Assembly**: Creates synchronized grid view with duration normalization
6. **Concatenation**: Combines intro + segments + grid into final video
7. **Optimization**: Applies compression to meet size requirements

### Grid Layout Logic

| Video Count | Grid Layout |
|-------------|-------------|
| 1           | 1x1         |
| 2           | 2x1         |
| 3-4         | 2x2         |
| 5-6         | 3x2         |
| 7-9         | 3x3         |
| 10+         | 4x4         |

### Compression Strategy

The tool applies progressive compression to meet size limits:

1. **Initial**: CRF 28 with medium preset
2. **If oversized**: Scale down 20%, CRF 32 with slow preset  
3. **If still oversized**: Scale down 40%, CRF 35 with veryslow preset

## 🛠️ Development

### Project Structure

```
video-concatenator/
├── video-concat          # Main CLI script
├── README.md            # This file
├── LICENSE              # MIT License
└── examples/            # Example videos and outputs
```

### Contributing

1. Fork the repository
2. Create a feature branch: `git checkout -b feature/amazing-feature`
3. Commit your changes: `git commit -m 'Add amazing feature'`
4. Push to the branch: `git push origin feature/amazing-feature`
5. Open a Pull Request

### Testing

```bash
# Test with sample videos
mkdir test-videos
# Add some .mov or .mp4 files to test-videos/
./video-concat --verbose test-videos/
```

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🐛 Troubleshooting

### Common Issues

**"Missing required dependencies" error**
- Install ffmpeg and bc using your system's package manager

**"No video files found" error**
- Ensure your directory contains supported video formats
- Check that files aren't hidden or in subdirectories

**Output file too large**
- Increase the size limit with `-s` option
- Consider reducing input video quality beforehand

**Grid view issues**
- Ensure all videos have valid metadata
- Try with `--verbose` flag to see detailed processing info

### Performance Tips

- For faster processing, keep videos in the same resolution
- Place input directory on an SSD for better I/O performance
- Use `--verbose` mode to monitor progress on large batches

## 🎯 Roadmap

- [ ] Support for audio preservation/mixing
- [ ] Custom intro slide templates
- [ ] Batch processing multiple directories
- [ ] GPU acceleration support
- [ ] Web interface for drag-and-drop functionality
- [ ] Custom watermark positioning
- [ ] Transition effects between segments

## 💖 Acknowledgments

- Built with [FFmpeg](https://ffmpeg.org/) - the Swiss Army knife of video processing
- Inspired by the need for quick, professional video compilations
- Created with the assistance of Claude AI 