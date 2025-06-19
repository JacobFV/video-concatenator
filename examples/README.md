# Examples

This directory contains examples and sample outputs from the Video Concatenator tool.

## Basic Usage Example

```bash
# Create a compilation from a directory of videos
./video-concat /path/to/your/videos/

# Custom output filename and size limit
./video-concat -o vacation-highlights.mp4 -s 20 ~/Videos/vacation/

# Verbose mode for detailed output
./video-concat --verbose --output presentation.mp4 ./slides/
```

## Sample Output Structure

When you run the tool, you'll get a video with this structure:

1. **Intro Slide (5 seconds)**: Black background with red text listing all scenes
2. **Individual Videos**: Each video with filename watermark in bottom-right
3. **Grid View Finale**: All videos playing simultaneously, time-normalized

## Expected File Sizes

- Input: 2 videos (~14MB total)
- Output: Compressed to under 10MB (default) or your specified limit
- Processing time: ~30-60 seconds depending on video length and resolution

## Tips

- Videos are automatically sorted alphabetically
- All audio is removed for consistency
- Grid layout is automatically optimized based on number of videos
- Use `-v` flag to see detailed processing information 