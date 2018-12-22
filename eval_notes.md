# kitti_evaluation code

## getThresholds

## cleanData
as for gt
1. height of gt 
2. valid_class
3. ignore
    * occlusion or truncation or height
    * ignored_gt
    ```cpp
    if(valid_class==1&&!ignore){
        ignored_gt.push_back(0);
    }else if(valid_class==0||(valid_class==1&&ignore)){
        // ignored due to height neiborhood
        ignored_gt.push_back(1);
    }else{
        //The class is not evaluated
        ignored_gt.push_back(-1);
    }
    ```
4. dont care

as for detection
1. valid_class
2. height
3. ignore vector
```
if(height<MIN_HEIGHT[difficulty])
      ignored_det.push_back(1);
    else if(valid_class==1)
      ignored_det.push_back(0);
    else
      ignored_det.push_back(-1);
```

## computeStatistics
1. compute_fp
```
ignored_threshold
for(all gt_boxes){
    if(ignored_gt)
        continue;
        // find matched dets
        for(all dets){
        if(ignored_dets||assigned_dets||ignored_threshold)continue;
        // find max overlaps,note that priviledge level of ignored_dets is lower
        // than that of not ignored dets.
        }
        // analysis after match
        if(ignored_gt==false&&NO_DETECTION)fn++;
        else if(detect difficulty level){
            assigned_detection=true;
            // not a tp
            }else if(detect a normal gt){
                tp++;
                assigned_detection = true;
                }
    }
// compute fp
for(all dets){
if(not assigned_det or not ignored_det){
        fp++;
    }
}
for(all dont_care){
    for(all det){
        if(match det with dont_care){
            nstuff++;
            }
        }
    }
fp -= nstuff;
```

## eval_class
```
for(all groundtruth){
    computeStatistics()
    }
    thresholds = getThresholds()
    for(all gt){
        for(all thresholds){
            
            get_statistics
            }
        }
    for(thresholds){
        get recall and precision
        }
        for(i in len(thresholds)){
        max_elements(precision[i])
            }

```
