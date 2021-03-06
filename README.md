# fire-detect-yolov4 and [fire-detect-dataset](https://pan.baidu.com/s/1AvCMcmZ7SaAZznmyTO65cg)

* author is leilei(CSU)
* fire-detection qq群: 980489677

## Some details
* [darknet-yolov4-install-tutorial](https://github.com/AlexeyAB/darknet#how-to-compile-on-linux-using-make)
* latest-fire-dataset (with xml annotations) download: [BaiDuYunPan](https://pan.baidu.com/s/1AvCMcmZ7SaAZznmyTO65cg) 提取码->(3q4r)
* ~~fire-dataset (with xml annotations) download: [BaiDuYunPan](https://pan.baidu.com/s/1QlUTC8QW4wj0-Rwfx3fIPA) 提取码->(9mr7)~~
* fire-yolov4-weights download: [BaiDuYunPan](https://pan.baidu.com/s/14g0SkV5vR8OhnDOCTW6r9A) 提取码->(w3ip)
* yolov4.conv.137 -> GoogleDriver download: [yolov4.conv.137 ](https://drive.google.com/open?id=1cewMfusmPjYWbrnuJRuKhPMwRe_b9PaT)

## How to use dataset?
* We annotate the fire-detection-dataset as Pascal VOC format:
    ```
    --VOC2020
        --Annotations (xml_num: 2059)
        --ImageSets(Main)
        --JPEGImages (image_num: 2059)
        
        --label_name: fire
    ```
* If you want to convert VOC to YOLO format:
    ```
    Call darknet-yolov4's scripts voc_label.py
    ```
* Fire scene:
    ```
    vehicle-fire、grassland-fire、forest-fire、building-fire、Big and small fire、Day and night fire;
    ```

## How to use this code (test)?
0. installed darknet-yolov4, and put darknet_API.py into ./darknet
1. put cfg into ./darknet
2. download fire-yolov4's weight, and put it in backup_fire folder
3. Call the darknet_API main function:
    ```
    from darknet_API import Detect
    detect = Detect(metaPath=r'./cfg/fire.data', configPath=r'./cfg/yolov4-fire.cfg',\
                    weightPath=r'./backup_fire/yolov4-fire_best.weights',\
                    namesPath=r'./cfg/fire.names')
    image = cv2.imread(r'/home/Datasets/20200714085948.jpg', -1)
    draw_img = detect.predict_image(image, save_path='./pred.jpg')
    ```
* Note: 
    * This project should be placed in the ./darknet folder;
    * Fire generally coexists with smoke, but we only marked fire;
    * In addition, it is easy to confuse the negative sample of the fire and the light;
    
## How to train yolov4 in darknet (train)?
0. Convert VOC format data to YOLO format data
1. Configure file information such as cfg
2. Call the darknet command:
    ```
    ./darknet detector train cfg/fire.data cfg/yolov4-fire.cfg yolov4.conv.137 -gpus 0 -map -dont_show
    ```

## demo
* ./result: fire-detect demos

|![fire-detect-demo](https://github.com/gengyanlei/fire-detect-yolov4/blob/master/result/result_demo.jpg?raw=true)|
|----|

* ./xml_lab: fire-detection image annotations

|![fire-detect-annotation](https://github.com/gengyanlei/fire-detect-yolov4/blob/master/xml_lab/annotation.jpg)|
|----|

## Cite
* train_data contain 1-2-3-4:
* train_data1: https://blog.csdn.net/LEILEI18A/article/details/107334474
* train_data2: https://bitbucket.org/gbdi/bowfire-dataset/downloads/
* train_data3: https://github.com/OlafenwaMoses/FireNET/releases/download/v1.0/fire-dataset.zip
* train_data4: https://github.com/cair/Fire-Detection-Image-Dataset/blob/master/Fire%20images.rar
* 
* fire-demo-dataset: http://signal.ee.bilkent.edu.tr/VisiFire/Demo/SampleClips.html

## Reputation:
* This data set contains 2 parts:
* (1) Images crawled by myself, marked by myself
* (2) The data that others open source, some have annotations, some have no annotations (I re-annotate it)

## other
* [building-segmentation-dataset](https://github.com/gengyanlei/build_segmentation_dataset)