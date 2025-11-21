# Segmentation-based for surface-defect detection
第一阶段分割网络，第二阶段决策网络，克服深度学习中样本数量少的问题。

A Tensorflow implementation of "**Segmentation-Based Deep-Learning Approach for Surface-Defect Detection**"
  The author submitted the paper to  Journal of Intelligent Manufacturing (https://link.springer.com/article/10.1007/s10845-019-01476-x), where it was published In May 2019 . 
  
datasets: https://www.vicos.si/resources/kolektorsdd/

JIM paper: https://go.vicos.si/kolektorsdd
# The test environment
```
tensorflow-gpu	2.10.0
cudatoolkit     11.2.2
cudnn		    8.1.0.77 
python          3.8
```
# You should know

  I used the Dataset used in the papar, you can download [KolektorSDD](https://www.vicos.si/Downloads/KolektorSDD) here.
  If you train you own datset ,you should change the dataset interfence for you dataset.

  You can refer to the [paper](https://link.springer.com/article/10.1007/s10845-019-01476-x) for details of the experiment.
 


# my experimental results on KolektorSDD
  **Notes:**  the first 30 subfolders are used as training sets, the remaining 20 for testing.    Although, I did not strictly follow the   params of the papar , I still got a good result.
```
2019-05-21 09:20:54,634 - utils - INFO -  total number of testing samples = 160
2019-05-21 09:20:54,634 - utils - INFO - positive = 22
2019-05-21 09:20:54,634 - utils - INFO - negative = 138
2019-05-21 09:20:54,634 - utils - INFO - TP = 21
2019-05-21 09:20:54,634 - utils - INFO - NP = 0
2019-05-21 09:20:54,634 - utils - INFO - TN = 138
2019-05-21 09:20:54,635 - utils - INFO - FN = 1
2019-05-21 09:20:54,635 - utils - INFO - accuracy(准确率) = 0.9938
2019-05-21 09:20:54,635 - utils - INFO - prescision（查准率） = 1.0000
2019-05-21 09:20:54,635 - utils - INFO - recall（查全率） = 0.9545
```
**visualization:**
![kos49_Part4.jpg](/visualization/test/kos48_Part5.jpg)

# testing the KolektorSDD
  After downloading the KolektorSDD and changing the param[data_dir]
  ```
  python run.py 
    --test
  ```
  Then you can find the result in the "/visulaiation/test" and  "Log/*.txt"
  
 # training the KolektorSDD
 
 **First, only the segmentation network is independently trained, then the weights for the segmentation network are frozen and only the decision network layers are trained.**
 
   training the segment network
   ```
   python run.py 
    --train_segment
    --anew
    --valid_ratio
    0
    -ckpt
    "E:\University\graduate\defect_detection\recurrence\Segmentation\checkpoint"
    -dd
    "E:\University\graduate\defect_detection\recurrence\Segmentation\Datasets\KolektorSDD"
    --batch_size
    1
    -en
    500
   ```
   training the  decision network
   ```
   python run.py 
    --train_decision
    --anew
    --valid_ratio
    0
    -ckpt
    "E:\University\graduate\defect_detection\recurrence\Segmentation\decision_net_482"
    -dd
    "E:\University\graduate\defect_detection\recurrence\Segmentation\Datasets\KolektorSDD"
    --batch_size
    1
    -en
    50
