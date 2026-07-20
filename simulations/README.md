# Simulation Results Organization

This directory contains all simulation results for the RCOA project.

## 📁 Folder Structure

Each simulation scenario should have its own folder with a descriptive name:

```
simulations/
├── scenario_1_dense_obstacles/
├── scenario_2_narrow_passages/
├── scenario_3_dynamic_obstacles/
└── ...
```

## 📝 What to Include

For each simulation, include the following files in its folder:

### 1. **Media Files**
- `results.gif` - Animated GIF preview (recommended for quick viewing)
- `results.mp4` - Full video file (higher quality, optional)

### 2. **Metadata File** (`metadata.json`)
```json
{
  "title": "Scenario Name",
  "description": "A detailed description of what this simulation demonstrates",
  "date": "YYYY-MM-DD",
  "category": "dense|narrow|dynamic|other",
  "parameters": {
    "environment": "Indoor/Outdoor/Corridor/etc",
    "robot_type": "Circular/Rectangular/Custom",
    "num_obstacles": 15,
    "environment_size": "10m x 10m",
    "max_velocity": "1.5 m/s",
    "computation_time": "0.5 seconds"
  },
  "results": {
    "success": true,
    "path_length": "15.2 meters",
    "time_to_goal": "10.2 seconds",
    "collisions": 0,
    "notes": "Successfully completed navigation"
  }
}
```

### 3. **Optional: Detailed Report** (`report.md`)
```markdown
# Simulation Report

## Scenario Overview
[Description]

## Parameters
[Parameter details]

## Results
[Analysis and findings]

## Plots/Metrics
[Any additional visualizations]
```

## 🎬 How to Create GIFs from Videos

### Using FFmpeg:
```bash
ffmpeg -i results.mp4 -vf "fps=10,scale=640:-1:flags=lanczos" -c:v pam -f image2pipe - | convert -delay 10 - -loop 0 -layers Optimize results.gif
```

### Using ImageMagick:
```bash
convert -delay 10 -loop 0 results.mp4 results.gif
```

### Using Python (with imageio):
```python
import imageio
import numpy as np
from PIL import Image

# Read video
reader = imageio.get_reader('results.mp4')

# Extract frames
frames = []
for i, frame in enumerate(reader):
    if i % 5 == 0:  # Every 5th frame to reduce size
        frames.append(frame)

# Save as GIF
imageio.mimsave('results.gif', frames, fps=10)
```

## ✅ Adding a New Simulation

1. Create a new folder: `simulations/scenario_NAME/`
2. Add your `results.gif` and `results.mp4`
3. Create `metadata.json` with the template above
4. (Optional) Add a `report.md` with detailed analysis
5. Commit and push to GitHub
6. The gallery will automatically pick up the new simulation

## 🔄 Gallery Integration

The main gallery (`/index.html`) automatically discovers simulations. To manually update:

1. Edit the `simulations` array in `index.html`
2. Add entries matching your `metadata.json` structure
3. Commit changes

## 💡 Tips

- **GIF Optimization**: Keep GIFs under 10MB for fast loading
- **Video Codec**: Use H.264 for broad compatibility
- **Naming**: Use consistent, descriptive folder names
- **Metadata**: Fill in all fields for better documentation
- **Categories**: Use consistent category names (dense, narrow, dynamic, etc.)

## 📊 Example Structure

```
simulations/
├── README.md (this file)
├── scenario_1_dense_obstacles/
│   ├── results.gif
│   ├── results.mp4
│   ├── metadata.json
│   └── report.md
├── scenario_2_narrow_passages/
│   ├── results.gif
│   ├── results.mp4
│   ├── metadata.json
│   └── report.md
└── scenario_3_dynamic_obstacles/
    ├── results.gif
    ├── results.mp4
    ├── metadata.json
    └── report.md
```

---

**Happy simulating! 🚀**
