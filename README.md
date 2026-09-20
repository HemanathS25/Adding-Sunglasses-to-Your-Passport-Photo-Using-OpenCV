# Workshop-1 - Adding Sunglasses to Your Passport Photo Using OpenCV

## Name : HEMANATH S

## Reg no :212224230094

## Sturdy Octo Disco is a fun project that adds sunglasses to photos using image processing

Welcome to Sturdy Octo Disco, a fun and creative project designed to overlay sunglasses on individual passport photos! This repository demonstrates how to use image processing techniques to create a playful transformation, making ordinary photos look extraordinary. Whether you're a beginner exploring computer vision or just looking for a quirky project to try, this is for you!

## Features:
- Detects the face in an image.
- Places a stylish sunglass overlay perfectly on the face.
- Works seamlessly with individual passport-size photos.
- Customizable for different sunglasses styles or photo types.

## Technologies Used:
- Python
- OpenCV for image processing
- Numpy for array manipulations

## How to Use:
1. Clone this repository.
2. Add your passport-sized photo to the `images` folder.
3. Run the script to see your "cool" transformation!

## Applications:
- Learning basic image processing techniques.
- Adding flair to your photos for fun.
- Practicing computer vision workflows.

## Program:
```python
import cv2
import numpy as np
import matplotlib.pyplot as plt

#Load face image
faceImage = cv2.imread("ME.jpg")
plt.imshow(faceImage[:,:,::-1]); plt.title("Face")
print("Face shape:", faceImage.shape)

glass= cv2.imread("glass.png")
plt.imshow(glassJPG[:,:,::-1]); plt.title("glass")
print("Glass shape:", glass.shape)

glassBGR = glassJPG[:,:,0:3]
glassGray = cv2.cvtColor(glassBGR, cv2.COLOR_BGR2GRAY)
_, glassMask1 = cv2.threshold(glassGray, 240, 255, cv2.THRESH_BINARY_INV)  # detect non-white

plt.figure(figsize=[15,15])
#Show sunglasses color channels
plt.subplot(121)
plt.imshow(glassBGR[:,:,::-1])  # BGR → RGB
plt.title('Sunglass Color channels')
if faceImage is None or glass is None:
    print("Error loading images")
    exit()

face_h, face_w, _ = faceImage.shape

# Resize glasses (slightly smaller looks more natural)
# Resize glasses
new_w = int(face_w * 0.42)
new_h = int(glass.shape[0] * new_w / glass.shape[1])

glass_resized = cv2.resize(glass, (new_w, new_h))

# Position
x = int((face_w - new_w) / 2) - 5
y = int(face_h * 0.245)

# Split channels
glass_rgb = glass_resized[:, :, :3]
alpha = (glass_resized[:, :, 3] / 255.0) * 0.9
roi = faceImage[y:y+new_h, x:x+new_w]

for c in range(3):
    roi[:, :, c] = (alpha * glass_rgb[:, :, c] +
                    (1 - alpha) * roi[:, :, c])

faceImage[y:y+new_h, x:x+new_w] = roi

plt.figure(figsize=(6,8))
plt.imshow(cv2.cvtColor(faceImage, cv2.COLOR_BGR2RGB))
plt.axis("off")
plt.show()
```

## OUTPUT:

<img width="346" height="434" alt="download" src="https://github.com/user-attachments/assets/37766599-b105-44a3-bfa2-d192d9bc360d" />

<img width="552" height="283" alt="download" src="https://github.com/user-attachments/assets/4c1d3e1f-09c9-40c1-a607-a93b01c85357" />

<img width="585" height="297" alt="download" src="https://github.com/user-attachments/assets/a5be5697-40d8-4961-bb36-9e125c887c3d" />

<img width="484" height="652" alt="download" src="https://github.com/user-attachments/assets/fa255cdd-8518-4334-af70-20172578fba8" />
