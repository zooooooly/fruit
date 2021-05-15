# fruit
在colab上训练模型
#训练：

#第一段执行代码
from google.colab import drive   
drive.mount('/content/drive')

#第二段，My Drive后跟你的工程文件夹
cd '/content/drive/My Drive/fruit'   

#第三段
!git clone https://github.com/ultralytics/yolov5  # clone repo
%cd yolov5
%pip install -qr requirements.txt  # install dependencies

import torch
from IPython.display import Image, clear_output  # to display images

clear_output()
print('Setup complete. Using torch %s %s' % (torch.__version__, torch.cuda.get_device_properties(0) if torch.cuda.is_available() else 'CPU'))

#第四段，--data后跟标签yaml文件所在位置， --weights后跟所用的训练网络模型，训练结果所在文件会显示在最后一行
!python train.py --img 640 --batch 50 --epochs 100 --data data/fruit.yaml --weights yolov5s.pt --nosave --cache



#测试：
#--source 代表测试文件所在位置， --weights，即训练获得的模型
!python detect.py --source data/images --weights runs/train/exp/weights/last.pt --conf 0.25
 
