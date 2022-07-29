---
layout: post
title: 关于在在jupyter notebook中使用sys添加临时库
categories: Blog
description: none
keywords: 博客
---

python程序中使用 import XXX 时，python解析器会在当前目录、已安装和第三方模块中搜索 xxx，如果都搜索不到就会报错。使用sys.path.insert()方法可以临时添加搜索路径，方便更简洁的import其他包和模块。这种方法导入的路径会在python程序退出后失效。



```python
import os.path as osp
import sys
 
def add_path(path):
    if path not in sys.path:
        sys.path.insert(0, path)
 
this_dir = osp.dirname(__file__)
 
# Add lib to PYTHONPATH
lib_path = osp.join(this_dir, 'lib')
add_path(lib_path)
```

![img](https://img-blog.csdnimg.cn/20190417180202863.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2ExMTAzNjg4ODQx,size_16,color_FFFFFF,t_70)

```python
#调用本地库的时候，如下所示
import _init_paths
from roi_data_layer.roidb import combined_roidb
from roi_data_layer.roibatchLoader import roibatchLoader
from model.utils.config import cfg, cfg_from_file, cfg_from_list, get_output_dir
from model.rpn.bbox_transform import clip_boxes
from model.nms.nms_wrapper import nms
from model.rpn.bbox_transform import bbox_transform_inv
from model.utils.net_utils import save_net, load_net, vis_detections
from model.faster_rcnn.vgg16 import vgg16
from model.faster_rcnn.resnet import resnet
```

参考[blog](https://blog.csdn.net/a1103688841/article/details/89361328)
