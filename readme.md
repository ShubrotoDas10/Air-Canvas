# 🎨 Iron Canvas Pro - Air Drawing with Hand Gestures

![Python](https://img.shields.io/badge/Python-3.8+-blue?style=for-the-badge&logo=python)
![OpenCV](https://img.shields.io/badge/OpenCV-4.5+-green?style=for-the-badge&logo=opencv)
![MediaPipe](https://img.shields.io/badge/MediaPipe-Latest-orange?style=for-the-badge)
![License](https://img.shields.io/badge/License-MIT-yellow?style=for-the-badge)

**Iron Canvas Pro** is a futuristic air drawing application that lets you paint in the air using just your hand gestures! Draw, sketch, and create with pinch gestures detected through your webcam - no physical tools required.

## ✨ Features

🖐️ **Hand Gesture Detection** - Uses MediaPipe for accurate real-time hand tracking

✍️ **Pinch to Draw** - Bring your thumb and index finger together to draw

🎨 **Arc Color Palette** - Beautiful semi-circle color picker at the top of the screen

🌟 **Neon Glow Effects** - Smooth neon glow on your drawings

🎵 **Audio Feedback** - Dynamic sound effects based on drawing speed (Windows only)

🎯 **Sci-Fi HUD** - Futuristic heads-up display showing hand skeleton and pinch indicator

🧹 **Clear Canvas** - Built-in eraser option to clear your artwork

⚡ **Smooth Movement** - Configurable smoothing for stable drawing

## 🎮 How to Use

1. **Run the application**
2. **Show your hand** to the camera (palm facing the camera)
3. **Hover over the arc palette** at the top to see colors
4. **Pinch** (touch thumb to index finger) to select a color
5. **Move below the palette** and pinch again to draw
6. **Release the pinch** to stop drawing
7. **Select "CLEAR"** from the palette to erase everything
8. **Press 'q'** to quit

### Gesture Controls

| Gesture | Action |
|---------|--------|
| 👆 Index finger up | Control the cursor |
| 🤏 Pinch (thumb + index) | Draw or select color |
| 🖐️ Open hand | Stop drawing |
| 🎨 Pinch over palette | Change color or clear canvas |

## 🚀 Quick Start

### Prerequisites

- Python 3.8 or higher
- Webcam
- Windows OS (for sound effects - optional)

### Installation

1. **Clone or download the file**
```bash
# Download canvas.py to your computer
```

2. **Install required packages**
```bash
pip install opencv-python mediapipe numpy
```

3. **Run the application**
```bash
python canvas.py
```

## 📦 Dependencies

```bash
pip install opencv-python==4.8.0
pip install mediapipe==0.10.0
pip install numpy==1.24.0
```

Or install all at once:
```bash
pip install opencv-python mediapipe numpy
```

## ⚙️ Configuration

You can customize the application by modifying the `Config` class:

```python
class Config:
    WIDTH, HEIGHT = 1280, 720   # Window resolution
    
    PINCH_THRESHOLD = 40        # Sensitivity (lower = more sensitive)
    SMOOTHING = 0.6             # Movement smoothing (0.0 - 1.0)
    
    BRUSH_SIZE = 8              # Drawing brush thickness
    NEON_GLOW = True            # Enable/disable glow effect
    
    ARC_RADIUS = 150            # Color palette arc radius
    ARC_THICKNESS = 60          # Color palette thickness
```

### Adjusting Sensitivity

**If drawing is too sensitive:**
```python
PINCH_THRESHOLD = 50  # Increase this value
```

**If drawing is not responsive enough:**
```python
PINCH_THRESHOLD = 30  # Decrease this value
```

**For smoother but slightly laggy drawing:**
```python
SMOOTHING = 0.4  # Lower value
```

**For faster but jittery drawing:**
```python
SMOOTHING = 0.8  # Higher value
```

## 🎨 Available Colors

The arc palette includes:
- 🔴 **Red**
- 🟠 **Orange**
- 🟡 **Yellow**
- 🟢 **Green**
- 🔵 **Cyan**
- 🟣 **Purple**
- ⚪ **White**
- 🧹 **Clear** (erases canvas)

## 🛠️ Technical Details

### How It Works

1. **Hand Detection**
   - Uses MediaPipe Hands solution
   - Detects 21 hand landmarks in real-time
   - Tracks index finger (landmark 8) and thumb (landmark 4)

2. **Pinch Detection**
   - Calculates distance between thumb tip and index finger tip
   - Pinch detected when distance < threshold (default: 40 pixels)

3. **Drawing System**
   - Smooth cursor position using exponential smoothing
   - Lines drawn between consecutive positions
   - Neon glow effect using Gaussian blur

4. **Color Palette**
   - Arc-shaped UI at top of screen
   - Hover detection using angle calculation
   - Selection by pinching over desired color

5. **Audio Feedback** (Windows only)
   - Sound frequency changes based on drawing velocity
   - Runs in separate thread to avoid blocking
   - Automatically falls back if not available

### Architecture

```
┌─────────────┐
│   Camera    │
│   Input     │
└──────┬──────┘
       │
       ▼
┌─────────────┐
│  MediaPipe  │
│Hand Tracking│
└──────┬──────┘
       │
       ▼
┌─────────────┐      ┌──────────────┐
│ Hand System │─────▶│   Canvas     │
│   (HUD)     │      │  (Drawing)   │
└──────┬──────┘      └──────┬───────┘
       │                     │
       ▼                     ▼
┌─────────────┐      ┌──────────────┐
│Arc Palette  │      │ Neon Glow    │
│  Selection  │      │   Effect     │
└─────────────┘      └──────────────┘
```

## 🎯 Features Breakdown

### 1. Hand System
- Real-time hand tracking using MediaPipe
- 21 landmark points detection
- Sci-fi styled HUD overlay
- Joint connections visualization
- Pinch distance indicator bar

### 2. Arc Palette
- 8 color options in semi-circle
- Hover highlight effect
- Color name display on hover
- Selection feedback with white ring

### 3. Drawing Engine
- Smooth line drawing with anti-aliasing
- Configurable brush size
- Movement-based line thickness
- Neon glow post-processing

### 4. Sound Engine
- Velocity-based frequency modulation
- Non-blocking threaded audio
- Graceful fallback on non-Windows systems

## 📊 Performance

- **FPS:** 30-60 (depends on camera and CPU)
- **Latency:** ~30-50ms hand tracking
- **CPU Usage:** ~15-25% on modern processors
- **Memory:** ~200-300 MB

## 🐛 Troubleshooting

### Camera not detected
```python
# Try different camera index
cap = cv2.VideoCapture(1)  # or 2, 3, etc.
```

### Hand not detected
- Ensure good lighting
- Keep hand within camera frame
- Try adjusting `min_detection_confidence`:
```python
self.hands = self.mp_hands.Hands(
    min_detection_confidence=0.5,  # Lower for easier detection
    min_tracking_confidence=0.3
)
```

### Drawing is jittery
```python
# Increase smoothing
SMOOTHING = 0.4  # Lower = smoother
```

### Drawing is laggy
```python
# Decrease smoothing
SMOOTHING = 0.8  # Higher = more responsive
```

### Sound not working
- Sound only works on Windows
- Install winsound (usually pre-installed)
- Application will work fine without sound

### Low FPS
- Reduce resolution:
```python
WIDTH, HEIGHT = 640, 480
```
- Disable glow effect:
```python
NEON_GLOW = False
```

## 🎨 Usage Tips

### Best Practices
1. **Position your hand 1-2 feet from camera** for best tracking
2. **Use good lighting** - avoid backlit situations
3. **Keep hand still** when selecting colors
4. **Draw in smooth motions** for best results
5. **Practice pinch gesture** - don't press too hard

### Creating Better Art
- Use smooth, flowing movements
- Vary your drawing speed for different effects
- Mix colors by drawing over previous lines
- Use the glow effect for ethereal designs

## 🔧 Advanced Customization

### Custom Colors
Add your own colors to the palette:
```python
self.colors = [
    ((0, 0, 255), "RED"),
    ((128, 0, 128), "CUSTOM"),  # Add custom color
    # ... more colors
]
```

### Brush Styles
Modify drawing style:
```python
# Thicker brush
Config.BRUSH_SIZE = 12

# Dotted style (in drawing logic)
cv2.circle(canvas, (cx, cy), Config.BRUSH_SIZE, color, -1)
```

### Different HUD Styles
Customize the heads-up display colors:
```python
# In draw_sci_fi_hud method
cv2.circle(overlay, pt, 3, (255, 0, 0), -1)  # Red joints
cv2.line(overlay, pt1, pt2, (0, 255, 0), 1)   # Green lines
```

## 🚀 Future Enhancements

- [ ] Multiple brush styles (spray, pencil, marker)
- [ ] Undo/Redo functionality
- [ ] Save drawings as images
- [ ] Adjustable brush size with gestures
- [ ] Two-hand drawing support
- [ ] Shape recognition (circles, squares)
- [ ] Layer system
- [ ] Background image selection
- [ ] Recording drawing as video
- [ ] Export to SVG format

## 💡 Use Cases

- 🎓 **Education** - Teaching, presentations, remote learning
- 🎨 **Art** - Digital sketching, concept art, doodling
- 🎮 **Gaming** - Gesture-based game controls
- 📊 **Presentations** - Live annotations during talks
- 🧩 **Fun** - Creative play, party entertainment
- ♿ **Accessibility** - Touch-free interaction

## 📝 Code Structure

```
canvas.py
├── Config                  # Configuration settings
├── SoundEngine             # Audio feedback system
│   ├── set_drawing()      # Update drawing state
│   └── _loop()            # Background audio thread
├── HandSystem             # Hand tracking and HUD
│   ├── process()          # Extract hand landmarks
│   └── draw_sci_fi_hud()  # Render HUD overlay
├── ArcPalette             # Color picker UI
│   └── draw()             # Render and detect selection
└── main()                 # Application loop
    ├── Video capture
    ├── Hand processing
    ├── Drawing logic
    └── Display rendering
```

## 🔐 Privacy & Security

- **No data collection** - everything runs locally
- **No internet required** - fully offline
- **Camera access** - only during runtime
- **No file creation** - unless you save screenshots

## 📄 License

This project is open source and available under the MIT License.

## 🙏 Acknowledgments

- [MediaPipe](https://google.github.io/mediapipe/) - Hand tracking solution
- [OpenCV](https://opencv.org/) - Computer vision library
- Inspired by futuristic UI designs and gesture interfaces

## 👨‍💻 Author

**Shubroto Das**
- GitHub: [@ShubrotoDas10](https://github.com/ShubrotoDas10)

## 🆘 Support

Having issues? Try these resources:
- Check the troubleshooting section above
- Ensure all dependencies are installed correctly
- Verify your webcam is working
- Check Python version (3.8+ required)

## 🎯 Quick Command Reference

```bash
# Install dependencies
pip install opencv-python mediapipe numpy

# Run application
python canvas.py

# Quit application
Press 'q' key
```

## 📸 Screenshots

```
[Camera View]  →  [Hand Detection]  →  [Drawing Canvas]
                         ↓
                  [Arc Color Palette]
```

---

<div align="center">

**Made with ❤️ by Shubroto Das**

Draw in the air, create with gestures! ✨

[Report Bug](https://github.com/ShubrotoDas10/issues) · [Request Feature](https://github.com/ShubrotoDas10/issues)

</div>
