## Coming up the OCR Learning Curve

### Optical Character Recognition (OCR) using 12 lines of code

Came across [this article](https://towardsdatascience.com/optical-character-recognition-ocr-with-less-than-12-lines-of-code-using-python-48404218cccb) and decided to give it a try on my Windows7 laptop.
On advice I got at [stackflow](https://stackoverflow.com/questions/51853018/how-do-i-install-opencv-using-pip)

> conda install opencv

I decided to create a new conda environment called 'cv' and then install the needed python libraries within that environment.

Still needed to install tesseract. Another [stackflow answer](https://stackoverflow.com/questions/50951955/pytesseract-tesseractnotfound-error-tesseract-is-not-installed-or-its-not-i/53672281) directed me to the tesseract installer and the advice to add a line to the python code with the path to the tesseract executable.

```
"""
To run this script:
open bash shell in same folder
$ conda activate cv
$ python ocr_test.py
"""

import cv2
import pytesseract
import numpy as np

pytesseract.pytesseract.tesseract_cmd = r'C:\Program Files\Tesseract-OCR\tesseract.exe'

img = cv2.imread('text.png')
#Alternatively: can be skipped if you have a Blackwhite image
gray = cv2.cvtColor(img, cv2.COLOR_RGB2GRAY)
gray, img_bin = cv2.threshold(gray,128,255,cv2.THRESH_BINARY | cv2.THRESH_OTSU)
gray = cv2.bitwise_not(img_bin)

kernel = np.ones((2, 1), np.uint8)
img = cv2.erode(gray, kernel, iterations=1)
img = cv2.dilate(img, kernel, iterations=1)
out_below = pytesseract.image_to_string(img)
print("OUTPUT:", out_below)
```

### Other Articles on Tesseract and PyTesseract

- [OCR with Python, OpenCV and PyTesseract](https://medium.com/@jaafarbenabderrazak.info/ocr-with-tesseract-opencv-and-python-d2c4ec097866)

- [A comprehensive guide to OCR with Tesseract, OpenCV and Python](https://nanonets.com/blog/ocr-with-tesseract/)

