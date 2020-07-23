#### Start
    Open   https://colab.research.google.com
    set Runtime/Change runtime type as GPU
    
#### Install fawkes
    !pip install fawkes

#### Create folders and download sample file
    !mkdir  /content/sample_photo
    !mkdir  /content/rezult_photo
    !wget --output-document="/content/sample_photo/face.jpg" "https://upload.wikimedia.org/wikipedia/commons/1/14/ADAC_MX_Masters_ADAC_Promotiongirls.JPG"

#### Default mode
    !fawkes --directory "/content/sample_photo/" 
    !mv "/content/sample_photo/face_low_cloaked.png" "/content/rezult_photo/face_low_cloaked.png"

#### Mode with GPU and ultra_cloaked
    !fawkes  --gpu "0" --mode "ultra" --directory "/content/sample_photo/" 
    !mv  "/content/sample_photo/face_ultra_cloaked.png" "/content/rezult_photo/face_ultra_cloaked.png"

#### Show rezults and difference
    import matplotlib.pyplot as plt
    import cv2

    face = cv2.imread("/content/sample_photo/face.jpg")
    face = cv2.cvtColor(face,  cv2.COLOR_BGR2RGB)
    face_low_cloaked = cv2.imread("/content/rezult_photo/face_low_cloaked.png")
    face_low_cloaked = cv2.cvtColor(face_low_cloaked,  cv2.COLOR_BGR2RGB)

    face_ultra_cloaked = cv2.imread("/content/rezult_photo/face_ultra_cloaked.png")
    face_ultra_cloaked = cv2.cvtColor(face_ultra_cloaked,  cv2.COLOR_BGR2RGB)

    fig, axs = plt.subplots(1,3, figsize=(20, 10))
    axs[0].set_title('face')
    axs[0].imshow(face)
    axs[1].set_title('face_low_cloaked')
    axs[1].imshow(face_low_cloaked)
    axs[2].set_title('face_ultra_cloaked')
    axs[2].imshow(face_ultra_cloaked)
    plt.show()

    diff_low = face - face_low_cloaked
    diff_ultra = face - face_ultra_cloaked

    fig, axs = plt.subplots(1,2, figsize=(20, 10))
    axs[0].set_title('diff_low')
    axs[0].imshow(diff_low)
    axs[1].set_title('diff_ultra')
    axs[1].imshow(diff_ultra)
    plt.show()

#### fawkes bash parameters

    cloak generation mode ('low'/'mid'/ 'high'/'ultra')
      --mode, -m, type=str, default='low'

     the directory with images to run protection
        --directory, -d, type=str, default='imgs/'


    the GPU id when using GPU for optimization
     '--gpu', '-g', type=str, default='0'


    number of images to run optimization together
        --batch-size, type=int, default=1

    format of the output image
      --format, type=str, default="png"

    custom  feature extractor (name of the feature extractor used for optimization)
      --feature-extractor, type=str, default="high_extract"
