## experiments

### multibin
1. 单分支，两阶段同时训练,num_bins=12,overlaps=30度, 2d bbox,  3D AP(0-2)
2. 多分支，固定部分训练， num_bins=4, overlaps=30 , 2d bbox, 3D AP(5-6) (final bbox)
3. 多分支，两阶段同时训练，num_bins=12, overlaps=30 度, 2d bbox, 3D AP(~9) (roi bbox)
4. 多分支，两阶段同时训练，　overlaps=0 3D AP(~1.9)
随着训练的进行，精度都会下降(WHY)


### cls orient
3. 多分支，固定部分训练， cls_orient 3D AP (1-10)
4. 多分支，固定部分训练训练，　cls_orient 3D AP(~2) 2d bbox
5. 多分支，同时训练，　3D AP (~3) 3d bbox


### 分开预测，避免互相干扰




## Conclude

1. Two stage detector is different from One stage detector in mono_3d
due to RoI Pooling Ops!()

2. Depth Can be estimated well directly in One stage detector, In the future
all params should be predicted from 3d space invariance of perspective transform

