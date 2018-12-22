

1280*384
SINet car_detection AP: 89.486046 87.009201 74.448013







hard example mining

decrease the num of post_nms_topN is not impair the performance


rpn_batch_size=1024
easy      moderate  hard    pos_nms_topN     time
88.842194 82.350960 67.849792   2000         ...
88.962425 83.041359 67.930641   1000         ...
89.134827 82.813591 67.537331    500         0.08s
88.884644 83.006248 67.516319    250         0.05
88.708618 76.275078 66.999588    100       0.03-0.04
87.313171 74.745689 58.688450     50         0.03
77.674110 65.879921 49.905025     25          0.03


rpn_batch_size=2048
easy      moderate  hard    pos_nms_topN     time
94.299393 78.804054 69.013145     2000       0.25
95.738449 86.201729 69.780228     1000       0.19
95.976677 86.195084 69.638458     500         0.08
89.408203 79.037682 69.348404   250          0.05


non hard
88.800850 83.453308 68.821754  2000           0.23
88.917389 83.973846 68.633057  1000           ....
87.825623 76.744041 67.216232  500            ....
86.553902 75.088181 65.759209  250
78.137131 66.423927 57.537903  100
76.015419 64.729279 49.295231  50
58.651375 55.745636 40.718506  25


90  86            ...         1000




scales 4,8,16
car_detection_AP : 97.016853 88.981094 79.037277
89.2

# selection of cls targets
84.04
cls_targets: IoU (exp and mse loss)
cls_weights: ones
reg_targets: scale
reg_weights: ones

# reg_weights
* IoU weights

** exp_iouweights_center
76.39(scale,center,scale)

** exp_iouweights
84.12(scale,scale,scale)
84.03
** exp_iouweigths_balance
(Note that OHME cannot work here due to bad anchor start point)
85.47
** exp_iouweights_reverse_ohem
85.91(31 epoch)
# distance
distance ohem gate 73.5

* faster_rcnn + iou preds
can not work at present

# adaptive ohem(note: detection refers to detection sampler)
88.63(26th epoch) faster_rcnn_ohem(reverse)
89.27(40th epoch) faster_rcnn_detection
89.389381(50th epoch) faster_rcnn_detection(fg:0.3)
89.141068(100th epoch) faster_rcnn_detection(fg:0.7)
88.822365(61th epoch) faster_rcnn_detection(fg:0.5)
89.364983,88.21(31th epoch) faster_rcnn_detection_all(iou_criterion)
94.328812,86.72(13th epoch) iou_faster_rcnn
89.612617(24th epoch) semantic
89.74(40th epoch) semantic
89.618492(56th epoch) semantic
89.73(21th epoch) semantic
89.57(21th epoch) faster_rcnn_detection(fg:0.1)
89.22670 (76th epoch) faster_rcnn_detection(fg:0.1)
89.56(50th epoch) overlaps_faster_rcnn(rpn_fg: 0.1,rcnn_fg:0.5)
# conclusion
* IoU can not work well in occlusion case.
* ohem
* weights can not be added casually

# TODO
1. iou_faster_rcnn(87.95)(fg_thresh 0.3)(88.06,fg:0.7)
iou_faster_rcnn semantic(89.12)(fg:0.3)
50th epoch 88.12(fg:0.3)
2. make gate_faster_rcnn work
3. detection_sampler and iou criterion(not good)
4. direction_sentive bbox



# new experiments(iox)

## iox:
predict iog,iod,iou to refine iou
fail ,too many bbox display

## loss
does not works,too many bbox

## LED pretrained
performance drop,(89.41>89.19)


# iou faster-rcnn summary
  it can not work well in high quality bbox evaluation due to that
*  it can not tell the difference ious among from 0.5-0.7. So that so many
  proposals that are not good enough to training. it results in high recall
  in 0.5 but low recall in 0.7
* scores it predicts are not high, that results can not set a thresh well


# cls summary
when iou thresh of it set too high,it will suppress many proposals that are probable positive
sample, so it is not good choise

# double iou smmary
it can improve recall to 96% when iou thresh is set 0.7

# separate optimization
it will hurt performance,as for good bbox ,it may not very good in confidence

# double_iou_part(50th epoch)(89.24) (recall<92)
# three_iou (73) but (recall>96)
# semantic_finetune(86.799),increase very slowly
# three_iou(semantic in iou prediction mode) 
semantic may hurt performance due to as for low iou,value will be small after muliplied

# add double_iou to semantic faster_rcnn
# fg/bg thresh can not set too low

# 88.97(48th epoch)
# iou prediction(can not suppress bad proposals)
# as for cls prediction, training too long can impair the performance

#ohem for bbox regression
use better for regression,ohem is not great for bbox

# which one is better for learning(hwxy)
# cls feature and bbox regression feature are different
# 0.5,0.6,0.7 can not tell the difference among them
# top 500,1024,2000 ,recall has no difference
# separate trainig for bbox and classification can drop for cls due to augumentation(Maybe)
