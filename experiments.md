

# TwoStageDetector(FasterRCNN)
## common config 
    * dataset config
        1. kitti 2d,
        2. use train dataset to train
        3. use val dataset to evaluate

    * model config
        1. pooling roi_align
        2. backbone res50

## model info
* baseline(faster_rcnn)
* semantic faster_rcnn,use cls prediction to mask features before bbox regression
* iou faster_rcnn,discard cls branch,use iou as bbox criterion
* separate both, cls pred and bbox pred use different fg thresh to train(used in two stages)
* separate first, used in the first stage,the same in the second stages
* feat separate, features used for cls and bbox is different







## performance

|    model_info    | ap(moderate) | ar(recall in rpn proposals) | ap(easy) |
| ---------- | --- | ------------------------- |------------------------ |
| baseline  |  89.2 | ~86 | 97 |
| semantic | 89.7 | x | x |
| iou(used in both of two stages) | 88.06 | x | 89 |
| separate both | 88.6 | ~96 | x |
| separate first | 89.2 | ~90 | x |
| separate first,remove cls branch | x | ~95 | |
| separate first, feat separate in pooling | x | ~90 | |



## notes
* fg_thresh/bg_thresh can change the results slightly
* features separate in pooling is not works
* top 500,1024,2000 ,recall has no difference
* many methods of bbox encode can work,but have no difference in performance


## sample

## both branch and only cls branch
cls branch will impair the recall


* detach
| model | AP | Speed(fps) | val or test |
| ---- | ---- | --- | ---- |
| res50 1920*576 | | | |

* semantic
| model | AP | Speed(fps) | val or test |
| ---- | ---- | --- | ---- |
| res50,384*1280 | 89.72 | 0.2 | val |
| res50,576*1920 | 90.12 | 0.2 | val |
| res50,576*1920 | 89.24 | 0.2 | test |
| res50,768*2560 | 90.18 | x | val |

* semantic_sinet
multiple pooling
| res50 | res101 | res152 |
| ---- | ----- | ----- |
| 89.56 | 89.76 | None(cannot write data) |


* DONE
    * semantic res101 576*1920
    * semantic res152 576*1920
    * detach res50 576*1920
    * detach_sinet res50 576*1920
    * detach res50 384*1280 88.9
    * detach_sinet 384*1280 89.2


## new experiments
1. fg thresh should be low(e,g 0.3) for predicting 3d bbox proj
2. more data or more data augmentation so that the recall is descend
3. rear_side cannot predicted well so that is orientation is not smooth
4. image size is very import 
5. 3d bbox proj is very hard to predict than 2d bbox
6. when 3d bbox is truncated(outside of image), its projection may be very large
so that cannot match any anchor(just be ignored)
