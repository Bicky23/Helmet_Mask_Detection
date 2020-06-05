**DATA PREPARATION**
Image and labels needed to be properly configured in the correct format. Some key points in the process are mentioned below:

- Raw Image files are stored in (`data/dataset`)

- Notebook to get image labels from `annotations.xml` and then convert to required input format for model (`data/dataset/convert-to-YOLO-format.ipynb`) which are then stored in `data/dataset/labels` as `.txt` files.

- Notebook to split into training & validation data for both images and labels (`data/dataset/data-preparation.ipynb`) which are then stored in train & valid directories of both `data/images` and `data/labels`. It also prepares files named `objects.data` (contains class names, class numbers, train.txt & valid.txt), `objects.names` (names of three classes: head, mask, helmet), `train.txt` (file locations for images in training set), `valid.txt` (file locations for images in validation set) in data directory.

- New files on which we want to detect can be placed in `data/samples`


**FRAMEWORK OF CHOICE**: `PyTorch` was chosen (personal preference)

**EXTRA TRAINING DATA**: None 

**NUMBER OF MODELS**: `1`

**EVALUATION METRIC**:  `Precision`, `Recall` and `mAP` have been shown as results. Apart from mAP, `class-wise precision` values should also be evaluated. **Because we don't want the model to detect mask(s)/helmet(s) in a human when actually there was/were none**. This situation is more harmful than the model not detecting mask(s)/helmet(s) when actually there was/were.

**Model configuration files**: Stored in `cfg` directory

**How to execute `training`, `testing` & `detecting`? (examples)**

**Train model**: `python3 train.py --data ./data/objects.data --cfg ./cfg/yolov3-tiny-3cls.cfg --epochs 500`

**Test model**: `python3 test.py --data data/objects.data --cfg ./cfg/yolov3-tiny-3cls.cfg --weights weights/last.pt --img-size 416`

**Detect objects in new image**: `python3 detect.py --names data/objects.names --cfg ./cfg/yolov3-tiny-3cls.cfg --weights weights/last.pt`
