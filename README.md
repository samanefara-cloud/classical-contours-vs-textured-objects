# classical-contours-vs-textured-objects
# Classical Contour-Based Object Counting on Textured Objects  Exploring the limitations of threshold + contour pipelines on real-world textured scenes (chocolates, bottles).
## Pipeline

1. Read image (`cv2.imread`)
2. Convert to grayscale / HSV-V
3. Blur (Gaussian)
4. Threshold:
   - Global (Otsu)
   - Adaptive (Mean / Gaussian)
5. `cv2.findContours` (external)
6. Geometric filters: area, aspect ratio, extent
7. Draw contours + index labels with `cv2.putText`
## Results

### Chocolates

- Left: Original image
- Right: Detected contours (many internal edges due to texture, not only outer shape)

### Bottles

- Top: Original image
- Bottom: Contours on highly textured transparent bottles
## Limitations Observed

- **Texture-heavy objects**: Both global and adaptive thresholding generate many small contours inside each object because the texture has strong intensity variations.
- **Shadows and soft self-shading**: When part of an object is under soft shadow, thresholding often breaks the object into multiple pieces or erodes the shadowed part.
- **Contour-based segmentation ≠ "one contour per object"**:
  - The algorithm only sees intensity changes, not the semantic concept of “one chocolate” or “one bottle”.
  - Complex patterns and highlights are treated as separate objects.
## What I Learned

- Classical pipelines (blur + threshold + contours) work very well on simple, high-contrast scenes with solid objects and plain backgrounds.
- Even with **adaptive thresholding**, local intensity changes from texture or reflections can produce many unwanted internal contours.
- Geometric filters (area, aspect ratio, extent) help suppress noise, but they cannot fully recover a single clean contour for each textured object.
- For real-world textured products (like chocolates and patterned bottles), more advanced methods (color-based segmentation, clustering, or learning-based models) are often needed.
)
