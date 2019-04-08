
# Detection


## Some Debugs
1. both gt_boxes and anchors should normalize at the same time
2. im_info = [blob_height,blob_width,im_scale]
3. fg and bg balanced
4. config file is the same in all file
5. ratio between width and height is not the good for training
6. bbox normalized means and stds
7. random crop according to aspect and iou
8. image should do the same operation in both training and testing(e.g, subtract mean and divide std)
9. image of type float32  should be converted to unit8 first before using Image.fromarray
10. weight is very important to regress bbox



## Others
Opencv convert to numpy array
Pytorch numpy has a bug

## image input rgb format
PIL.Image.open  rgb
cv2.imread      bgr
plt.imshow      rgb



# code bugs fixed
* subsample index
* encode of prediction
* how to record the batch_size
