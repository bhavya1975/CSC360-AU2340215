
# Learning Notes — 29 October 2026

## 1. JavaDoc

### What is JavaDoc?

JavaDoc is a documentation format used to describe Java classes, interfaces, enums, and methods.

A JavaDoc comment starts with `/**` and ends with `*/`.

```java
/**
 * Represents a student in the university system.
 *
 * @author YourName
 * @version 1.0
 */
public class Student {
}
```

### Common JavaDoc Tags

| Tag | Purpose |
|---|---|
| `@author` | Identifies the author of the code. |
| `@version` | Specifies the version of the class. |
| `@since` | Indicates when the class or method was introduced. |
| `@see` | References a related class, method, or resource. |
| `@deprecated` | Marks code that should no longer be used. |
| `@param` | Documents a method parameter. |
| `@return` | Documents the return value of a method. |

### Why Use `@author`?

- **Accountability:** Identifies who originally wrote the code.
- **Maintenance:** Helps developers identify whom to contact about a class.
- **Team collaboration:** Provides context when multiple developers work on a project.
- **Documentation:** Author information can appear in generated JavaDoc HTML pages.

`@author` is optional. Java code works perfectly fine without it.

For professional projects, Git history is often more reliable for tracking who wrote or modified particular sections of code.

### Types of Comments in Java

```java
// Single-line comment

/*
 * Multi-line comment
 */

/**
 * JavaDoc comment
 */
```

- `//` — Single-line comment.
- `/* ... */` — Multi-line comment.
- `/** ... */` — JavaDoc comment.

**Important:** JavaDoc is generally placed immediately before the class, interface, enum, or method it documents. It does not necessarily need to appear at the very beginning of every file.

---

## 2. Introduction to Image Processing with Java and ImageJ

### What Is ImageJ?

ImageJ is an image-processing application that can also be extended using Java plugins.

It allows us to:
- Open and display images.
- Access and modify pixel values.
- Apply image-processing operations.
- Generate processed images.
- Develop custom image-processing plugins using Java.

### Basic Concept of Image Processing

A digital image consists of pixels. Each pixel stores information about the image's colour or intensity.

For an 8-bit grayscale image:

- `0` represents black.
- `255` represents white.
- Values between `0` and `255` represent different shades of gray.

Image processing involves reading pixel values, modifying them according to an algorithm, and displaying or saving the resulting image.

### Beginner-Friendly Image Processing Projects

#### 1. Image Negative Generator

**Goal:** Create an inverted version of an image.

For an 8-bit channel:

```java
newValue = 255 - oldValue;
```

For example:
- `0` becomes `255`.
- `50` becomes `205`.
- `255` becomes `0`.

**Concepts learned:**
- Accessing pixel values.
- Modifying intensity values.
- Creating and displaying an output image.

**Estimated time:** 2–3 hours for a basic implementation.

#### 2. Grayscale Converter

**Goal:** Convert a colour image into shades of gray.

**Concepts learned:**
- RGB colour representation.
- Pixel intensity.
- Colour conversion.

A common grayscale approximation is:

```java
gray = (int) (0.299 * red
            + 0.587 * green
            + 0.114 * blue);
```

#### 3. Brightness Adjustment

**Goal:** Make an image brighter or darker.

A simple transformation is:

```java
newValue = oldValue + brightness;
```

The result must be limited to the valid intensity range of `0` to `255`.

**Concepts learned:**
- Intensity transformations.
- Pixel value limits.
- Image appearance.

#### 4. Contrast Adjustment

**Goal:** Increase or decrease the difference between dark and bright regions.

**Concepts learned:**
- Pixel intensity distribution.
- Contrast stretching.
- Linear transformations.

#### 5. Image Blur

**Goal:** Smooth an image by averaging neighbouring pixel values.

**Concepts learned:**
- Neighbouring pixels.
- Filters and kernels.
- Averaging operations.

#### 6. Thresholding

**Goal:** Convert an image into a binary black-and-white image.

For a threshold `T`:

```java
if (pixelValue >= T) {
    newValue = 255;
} else {
    newValue = 0;
}
```

**Concepts learned:**
- Conditional pixel transformations.
- Binary images.
- Image segmentation basics.

---

## 3. Horizontal and Vertical Edge Detection

### Goal

Build a Java and ImageJ project that detects horizontal and vertical edges separately and combines them into one result.

### What Is an Edge?

An edge is a region where the intensity of an image changes significantly.

For example, the boundary between a black object and a white background has a large intensity difference.

Edge detection helps identify:
- Object boundaries.
- Shapes and outlines.
- Changes in image regions.
- Important structural details.

### Basic Idea

Compare the intensity of neighbouring pixels.

Let `I(x, y)` represent the intensity of the pixel at coordinates `(x, y)`.

A simple estimate of horizontal intensity change is:

```text
Gx = |I(x + 1, y) - I(x - 1, y)|
```

A simple estimate of vertical intensity change is:

```text
Gy = |I(x, y + 1) - I(x, y - 1)|
```

Here:

- `Gx` measures intensity changes across the horizontal direction.
- `Gy` measures intensity changes across the vertical direction.
- Larger values indicate stronger intensity changes in the corresponding direction.

These are simple gradient estimates suitable for learning.

### Combining the Edge Maps

The horizontal and vertical responses can be combined to create an overall edge map.

One simple approach is:

```text
G = sqrt(Gx * Gx + Gy * Gy)
```

This calculates the magnitude of the combined gradient.

The resulting image highlights areas where intensity changes significantly.

### Implementation Steps

1. Open an image in ImageJ.
2. Convert the image to grayscale or calculate grayscale intensity.
3. Read pixel intensities from neighbouring locations.
4. Calculate the horizontal response `Gx`.
5. Calculate the vertical response `Gy`.
6. Store the horizontal responses in a separate image.
7. Store the vertical responses in another image.
8. Combine the responses into one edge map.
9. Display all three results alongside the original image.

### Expected Output

The program should display:

1. Original image.
2. Horizontal edge map.
3. Vertical edge map.
4. Combined edge map.

### Difficulty and Estimated Time

- With basic Java knowledge and some ImageJ familiarity: approximately 2–4 hours.
- If ImageJ and plugin development are completely new: approximately 4–6 hours.

These are estimates. Initial setup and debugging may take additional time.

---

## 4. Recommended Learning Order

A beginner-friendly progression is:

1. Image Negative Generator
2. Grayscale Converter
3. Brightness Adjustment
4. Contrast Adjustment
5. Image Blur
6. Thresholding
7. Horizontal and Vertical Edge Detection

This order gradually introduces pixel access, intensity transformations, neighbourhood operations, and edge detection.

## 5. Key Takeaways

- JavaDoc documents code but does not affect program execution.
- `@author` is optional and provides useful information about code ownership.
- JavaDoc comments use `/** ... */`.
- Image processing involves reading pixel values, applying transformations, and producing output images.
- ImageJ provides tools for experimenting with images and developing custom Java plugins.
- Edge detection identifies significant changes in image intensity.
- Horizontal and vertical edge maps capture intensity changes in different directions.
- Small projects with clearly defined goals are an effective way to learn image processing.
