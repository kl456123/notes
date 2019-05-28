# detection

## idea
1. hem sort by score(DONE)
2. cls concat feat map(DONE)
3. multiple level bbox pred
4. multiple loss
5. score/bbox_area
6. auto adjust IoU(?)
7. set intermediate threshold(conf) to train
8. sort by IoU(DONE)


9. scale invariance ,select a better regression method


10. don't do roi pooling,just embeding back to orignal image



11. adjust bbox bigger slight to make a good view

12. match policy(DONE)

13. interpolate using deep learning

14. inbalanced anchors inplacement

15. multiple anchor to fuse to predict gt boxes

16. new version of nms,merge by distance of feat

17. single iou(rpn_iou enable)

18. separate iou(cls_iou,bbox_iou)

19. label for part cover proposals

20.  amplify the images

21. do not train bbox reg, valid the influence of the cls branch

22. points in overlaps between two gt bboxes are not regressed(contrast)

23. automatic select is All you need according to the loss

24. scores for the boundary
