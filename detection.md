
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
11. config should be the same in any where
12. repeat is increase dim at the front side, NOT the tail side
13. in fpn, you should keep the order of roi_batch
14. loss normalize or not
15. cls loss normalized by num_pos
16. too large batch size may drop the performance in one_stage
17. using ohem is helpful for training classification
18. keypoint encode may be better than that of fasterrcnn(more smooth)
19. reweight between multi-task is very important
20. fraction in first stage should be slow(e,g fg_fraction=0.25) to suppress bg
21. prediction more meaningful thing not according to its distance



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
