# Hough-Line-Detection

### Orignal image
![phone](https://user-images.githubusercontent.com/47830409/63932360-b7734700-ca5f-11e9-8325-ecb3c824a61c.jpg)

### Make image gray and display
```sh
image = cv2.imread('phone.jpg')
image_copy = np.copy(image)
image_copy = cv2.cvtColor(image_copy, cv2.COLOR_BGR2RGB)
gray = cv2.cvtColor(image_copy, cv2.COLOR_RGB2GRAY)

f, (ax1, ax2) = plt.subplots(1, 2, figsize=(10,5))

ax1.imshow(image_copy)
ax1.set_title('Original')

ax2.imshow(gray, cmap="gray")
ax2.set_title('Gray image')
```
![ss1](https://user-images.githubusercontent.com/47830409/63932491-f4d7d480-ca5f-11e9-9f7b-86e3fb7fa6c1.PNG)

### Canny
```sh
low_threshold = 50
high_threshold = 150

edges = cv2.Canny(gray, low_threshold, high_threshold)

plt.imshow(edges, cmap="gray")
plt.title('edges image')
```
### And Hough Line
```sh
rho = 1
thea = np.pi / 180.0
threshold = 60
min_line_length = 100
max_line_gap = 5
lines = cv2.HoughLinesP(edges, 
                        rho, 
                        thea, 
                        threshold, 
                        np.array([]), 
                        min_line_length, 
                        max_line_gap)
line_image = np.array(image_copy)
```

  - For loop in lines each line have 4 arg (x1, y1, x2, y2)
  - we want find Rectangle
```sh
for line in lines:
    for x1, y1, x2, y2 in line:
        cv2.line(line_image, (x1, y1), (x2, y2), (255, 0, 0), 5)
        
plt.imshow(line_image)
```

![ss3](https://user-images.githubusercontent.com/47830409/63932820-a37c1500-ca60-11e9-98e0-5952dbd81112.PNG)

