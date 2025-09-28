# Sharingan - Real-Time Object Detection App

**Author:** Ernest Henry  

<p align="center">
    <img src="https://raw.githubusercontent.com/shashwatah/sharingan/main/assets/images/logos/sharingan-fill.png" alt="Sharingan" width="200">
</p>

<h4 align="center">
A Real-Time object detection app, built with <a href="https://www.electronjs.org/">Electron</a> and <a href="https://www.tensorflow.org/js/">TensorFlow.js</a>.
</h4>

<p align="center">
  <img alt="Release" src="https://img.shields.io/badge/license-MIT-green">
  <img alt="Github Release" src="https://img.shields.io/badge/release-v1.0.2-blue">
</p>

<img alt="Screenshot 1" src="https://raw.githubusercontent.com/shashwatah/sharingan/main/assets/images/screenshots/2.JPG">
<img alt="Screenshot 2" src="https://raw.githubusercontent.com/shashwatah/sharingan/main/assets/images/screenshots/3.JPG">

## Overview

Sharingan is a desktop application that performs real-time object detection using machine learning models running entirely in the browser. Built with modern web technologies, it demonstrates the power of client-side AI inference without requiring external servers or APIs.

### Key Features

- **Real-time Detection**: Live object detection through webcam feed
- **Cross-platform**: Runs on Windows, macOS, and Linux
- **Offline Operation**: No internet connection required after installation
- **Multiple Models**: Support for various TensorFlow.js models
- **Electron Framework**: Native desktop app experience
- **Performance Optimized**: Efficient inference using WebGL acceleration

## Technical Stack

- **Frontend**: HTML5, CSS3, JavaScript (ES6+)
- **Framework**: Electron for cross-platform desktop development
- **ML Library**: TensorFlow.js for in-browser machine learning
- **Models**: Pre-trained object detection models (COCO-SSD, MobileNet)
- **Build Tools**: npm scripts for packaging and distribution

## Prerequisites

Before running the application, ensure you have the following installed:

- **Git**: Version control system for cloning the repository
- **Node.js**: JavaScript runtime (v14.0.0 or higher recommended)
- **npm**: Package manager (comes with Node.js)

### Installation Instructions

#### Ubuntu/Linux
```bash
sudo apt-get update
sudo apt-get install git-core
sudo apt install nodejs
sudo apt install npm
```

#### Windows
Download and install from official sources:
- [Git](https://git-scm.com/)
- [Node.js](https://nodejs.org/en/download/) (includes npm)

#### macOS
```bash
# Using Homebrew
brew install git node npm
```

### Verify Installation
```bash
git --version
node --version
npm --version
```

## Installation

1. **Clone the Repository**
```bash
git clone https://github.com/ernesthenry/sharingan.git
cd sharingan
```

2. **Install Dependencies**
```bash
npm install
```

This will install all required packages including:
- Electron framework
- TensorFlow.js libraries
- Development dependencies
- Build tools

## Usage

### Development Mode
Run the application in development mode:
```bash
npm start
```

This launches the Electron app with hot-reload capabilities for development.

### Production Build
Package the application for distribution:

**Windows:**
```bash
npm run package-win
```

**Linux:**
```bash
npm run package-linux
```

**macOS:**
```bash
npm run package-mac
```

The packaged applications will be available in the `dist/` directory.

## Project Structure

```
sharingan/
├── src/
│   ├── main.js              # Electron main process
│   ├── renderer.js          # Renderer process logic
│   ├── index.html           # Application UI
│   └── styles/              # CSS stylesheets
├── models/                  # TensorFlow.js models
├── assets/
│   ├── images/              # UI assets and screenshots
│   └── icons/               # Application icons
├── package.json             # Dependencies and scripts
├── electron-builder.json    # Build configuration
└── README.md               # Documentation
```

## Implementation Details

### Object Detection Pipeline

1. **Camera Access**: Request webcam permissions and stream video
2. **Frame Processing**: Capture video frames at regular intervals
3. **Model Inference**: Run TensorFlow.js model on each frame
4. **Result Processing**: Parse detection results and filter by confidence
5. **Visualization**: Draw bounding boxes and labels on detected objects
6. **Performance Monitoring**: Display FPS and inference time

### Code Architecture

```javascript
// Main detection function
async function detectObjects(videoElement) {
    const model = await tf.loadLayersModel('/models/model.json');
    
    const detect = async () => {
        const predictions = await model.detect(videoElement);
        drawBoundingBoxes(predictions);
        requestAnimationFrame(detect);
    };
    
    detect();
}
```

### Supported Object Classes

The application can detect 80+ object classes from the COCO dataset including:
- People and animals
- Vehicles (cars, trucks, motorcycles)
- Household items
- Sports equipment
- Food items
- Electronics

## Performance Optimization

### WebGL Acceleration
- Utilizes GPU acceleration through WebGL backend
- Significantly faster inference compared to CPU-only execution
- Automatic fallback to CPU if WebGL unavailable

### Model Optimization
- Quantized models for smaller file sizes
- Optimized model architectures (MobileNet-based)
- Configurable confidence thresholds

### Memory Management
- Efficient tensor disposal to prevent memory leaks
- Frame buffer optimization
- Garbage collection monitoring

## Configuration Options

### Detection Settings
```javascript
const config = {
    modelUrl: './models/cocossd/model.json',
    scoreThreshold: 0.5,
    maxDetections: 20,
    videoSize: { width: 640, height: 480 }
};
```

### Performance Settings
- Frame rate control
- Model precision (float16/float32)
- Batch processing options

## Troubleshooting

### Common Issues

**Camera Not Working:**
- Check browser permissions
- Verify camera is not in use by another application
- Try different camera if multiple available

**Poor Performance:**
- Lower detection threshold
- Reduce video resolution
- Check GPU acceleration status

**Model Loading Errors:**
- Verify model files are present
- Check internet connection for initial model download
- Clear browser cache

## Future Enhancements

- **Custom Model Training**: Support for user-trained models
- **Video File Input**: Detection on pre-recorded videos
- **Export Functionality**: Save detection results and annotations
- **Multiple Camera Support**: Switch between different camera sources
- **Advanced Filters**: Object tracking and counting features
- **Cloud Integration**: Optional cloud-based model updates

## License

MIT License - feel free to use this project for learning, development, or commercial purposes.