# Chess Board Detection
This is an algorithm for the detection of square chess boards in images regardless of various pieces on the board, which is a big limitation of ```cv2.findChessboardCorners()```.

## Usage
Install requirements
```
pip install -r requirements.txt
```
Pass the following arguments to detect.py:
```
usage: detect.py [-h] [-f FILENAME] [-s]

Get location of chessboard on screen. Use -f to input filename (default will take a screenshot). Use -s to show result.

options:
  -h, --help            show this help message and exit
  -f FILENAME, --filename FILENAME
                        Input image filename, otherwise screenshot will be taken
  -s, --show            Show result of detection
```
Input filename or a screenshot of screen will be taken. Output should be something like this:
```
python detect.py -f ./README_Imgs/chessboard1.png -s

Region: (335, 85, 772, 771)
Pixels per Square: 96
```

## Breakdown

| Step  | Visual |
| ------------- | ------------- |
| <p align="center">Board detection is achieved through the use of image manipulation with OpenCV.</p>  | ![Chessboard1](./README_Imgs/chessboard1.png?raw=true "Title")  |
| <p align="center">Using ```cv2.Canny()``` filters the edges of the image, allowing for later use of ```cv2.getStructuringElement()``` and ```cv2.erode()``` to extract horizontal/vertical lines only.</p>   | ![Chessboard2](./README_Imgs/chessboard2.jpg?raw=true "Title")  |
| <p align="center">The next step is to combine the two filtered images into one with ```cv2.maximum(img1, img2)```.</p>    | ![Chessboard2](./README_Imgs/chessboard3.jpg?raw=true "Title") |
| <p align="center">The resultant image now contains only straight and horizontal lines, allowing for contour detection around the vertices of the squares within the image.</p>   | ![Chessboard2](./README_Imgs/chessboard4.jpg?raw=true "Title")  |
| <p align="center">After filtering through contours, 81 points are left. The corners are defined by the leftmost/rightmost, upmost/downmost points.</p>   | ![Chessboard2](./README_Imgs/chessboard5.jpg?raw=true "Title")  |
