# Iridium Compressor

![Windows](https://img.shields.io/badge/OS-Windows-blue.svg)
![.NET](https://img.shields.io/badge/.NET-8.0-purple.svg)
![License](https://img.shields.io/badge/License-MIT-green.svg)

A standalone Windows utility for high-ratio compression using a custom `.icf` format. Designed to bypass file size upload limits through GZip solid archiving.

## Purpose

Iridium Compressor helps you compress large files and folders into a single archive to bypass upload size restrictions on web services, file sharing platforms, or any system with file size limitations.

## Features

- **CLI and GUI Modes**: Use from command line or graphical interface
- **Solid Archiving**: Combines multiple files/folders into a single byte stream for better compression
- **GZip Compression**: Built-in .NET compression with adjustable levels (1-10)
- **Custom .icf Format**: Uses proprietary `[IRID_COMP_v1]` header
- **Windows Shell Integration**: Right-click any file/folder to compress/decompress via context menu (no admin required)
- **Background Processing**: UI remains responsive during compression
- **Folder Recursion**: Automatically includes all files in subdirectories
- **No External Dependencies**: Uses only built-in .NET libraries

## Requirements

- **For running**: Windows 10 or later 

## Building

### Download Standalone Executable
Download the latest release from the [Releases](https://github.com/skonplayz/IFCT-Iridium-File-Compression-Tool/releases) page.

## Usage

### CLI Mode

The application supports both GUI and CLI modes. Use CLI for quick operations without the graphical interface.

**Compress files/folders:**
```bash
IridiumCompressor.exe compress "C:\Users\MyUser\Documents\FolderToCompress" [compression level 1-10]
```

**Decompress .icf files:**
```bash
IridiumCompressor.exe decompress "C:\Users\MyUser\Documents\Archive.icf"
```

**Examples:**
```bash
# Compress a folder with default compression level (5)
IridiumCompressor.exe compress "C:\Users\MyUser\Documents\MyProject"

# Compress with maximum compression
IridiumCompressor.exe compress "C:\Users\MyUser\Documents\MyProject" 10

# Decompress an archive
IridiumCompressor.exe decompress "C:\Users\MyUser\Downloads\Archive.icf"
```

> **Note:** When using CLI mode, the application will not display the GUI window. All progress is shown in the console.

### GUI Mode

1. Launch Iridium Compressor
2. Click "Add Files..." to select files/folders
3. Adjust compression level (1-10, where 10 is maximum compression)
4. Click "Process" to compress
5. Output .icf file will be saved in the same directory as the first selected file

### Shell Integration

1. Run Iridium Compressor
2. Click "Register Shell" button (no admin required)
3. Right-click any file or folder in Windows Explorer
4. Select "Compress to .icf" from the context menu
5. The app will launch with the selected file(s) and begin compression automatically

For .icf files, you'll see a "Decompress .icf" option in the context menu.

To remove the context menu entry, click "Unregister Shell".

## Compression Levels

- **1-3**: Fast compression, lower ratio (suitable for large files)
- **4-6**: Balanced speed/ratio (recommended for most use cases)
- **7-8**: High compression, slower (best for text/code files)
- **9-10**: Maximum compression, very slow (for when every byte counts)

##  .icf File Format

The custom archive format includes:

1. **Header**: `[IRID_COMP_v1]` (14 bytes)
2. **File Count**: 4-byte integer
3. **File Metadata**: Path, size, and timestamp for each file
4. **File Data**: Raw bytes for each file
5. **GZip Compression**: Entire stream compressed with configurable compression level

## Technical Details

- **Compression Algorithm**: GZip (built-in .NET)
- **Compression Levels**: Fastest, Optimal, SmallestSize (mapped from 1-10 slider)
- **Threading**: Compression runs on background thread to keep UI responsive
- **Memory Usage**: Depends on file sizes (generally efficient)

## Troubleshooting

**Shell integration not appearing:**
- Try restarting Windows Explorer after registration
- Check that the application is in a stable location (not a temporary folder)

**Compression fails:**
- Check file permissions
- Ensure sufficient disk space for output file
- Try a lower compression level if memory is limited

**Application won't start:**
- For standalone executable: Ensure you're running on Windows 10 or later
- For source build: Verify .NET 8.0 SDK is installed
- Check Windows Event Viewer for error details

## License

See the [LICENSE](LICENSE) file for details.

## Future Enhancements

- [ ] Progress cancellation during compression
- [ ] Multi-file selection in shell integration
- [ ] Compression presets
- [ ] Archive verification
- [ ] Batch compression from CLI
- [ ] LZMA2 compression option (for higher ratios)

**Made with ❤️ to help you bypass file size limits**
