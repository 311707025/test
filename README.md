# taiwanese-speech-recognition-using-transformer-311707025 #
taiwanese-speech-recognition-using-transformer-311707025 created by GitHub Classroom

## Kaggle 網址
Kaggle 競賽網址: [https://www.kaggle.com/competitions/espnet-taiwanese-asr1/overview](https://www.kaggle.com/competitions/espnet-taiwanese-asr1/overview)

## Requirements
   - Python 3.6.1+
   - gcc 4.9+ for PyTorch1.0.0+
   - Cuda 8.0, 9.0, 9.1, 10.0 depending on each DNN library
   - Cudnn 6+, 7+
   - NCCL 2.0+ (for the use of multi-GPUs)

## Package
   $ sudo apt-get install cmake  
   $ sudo apt-get install sox  
   $ sudo apt-get install libsndfile1-dev  
   $ sudo apt-get install ffmpeg  
   $ sudo apt-get install flac  

## Setup Python environment ##

### 下載Anaconda
   - $ bash Anaconda3-2020.02-Linux-x86_64.sh

### 從github上下載 espnet
   - $ git clone https://github.com/espnet/espnet

### 建立 espnet 的環境
   - $ conda create -n espnet python=3.9  
   - $ conda activate espnet  
   - $ cd <username>/espnet/tools  
   - $ CONDA_TOOLS_DIR=$(dirname ${CONDA_EXE})/…  
   - $ ./setup_anaconda.sh ${CONDA_TOOLS_DIR} espnet 3.9  

### 建構Makefile中的相關應用程序
   - $ make

### 首次執行`run.sh`後，需安裝 kenlm
   1. cd 到 `/home/username/espnet/egs2/aishell/asr1` 後，執行`run.sh`
   2. 出現需安裝 `kenlm` 的 Error
   3. 接著照著Error中的指示安裝即可

### 正常執行 `run.sh`
   1. 執行`run.sh`
   2. 在`/home/username/espnet/egs2/aishell/asr1/downloads/data_aishell/wav`，即可看到原本espnet的音檔如下
   ![本地圖片示例](https://scontent.ftpe3-2.fna.fbcdn.net/v/t1.15752-9/340755117_235688892283032_3386157052203892726_n.png?_nc_cat=102&ccb=1-7&_nc_sid=ae9488&_nc_ohc=3QMkFt5I1s4AX_tNspt&_nc_ht=scontent.ftpe3-2.fna&oh=03_AdTCAgXD2y6XUSrXUaC_WHYZbkGUT0824DlAWsrSrd6AwA&oe=64631DA8)

## 本次作業需修改原本espnet的既有檔案 ##
   - `/home/username/espnet/egs2/aishell/asr1/downloads/data_aishell/wav/dev`
   - `/home/username/espnet/egs2/aishell/asr1/downloads/data_aishell/wav/test`
   - `/home/username/espnet/egs2/aishell/asr1/downloads/data_aishell/wav/train`
   - `/home/username/espnet/egs2/aishell/asr1/downloads/data_aishell/transcript/aishell_transcript_v0.8.txt`
   - `/home/username/espnet/egs2/aishell/asr1/downloads/resource_aishell/lexicon.txt`
   - `/home/username/espnet/egs2/aishell/asr1/downloads/resource_aishell/speaker.info`
   - `/home/username/espnet/egs2/aishell/asr1/local/data.sh`
   - `/home/username/espnet/egs2/aishell/asr1/conf/train_asr_branchformer.yaml`
   - `/home/username/espnet/egs2/aishell/asr1/run.sh`
   
## 處理作業所需的客語音檔
   1. 路徑：`/home/username/espnet/egs2/aishell/asr1/downloads/data_aishell/wav`
   2. 將原本 `/wav/dev`、`/wav/test`、`/wav/train`底下的音檔都刪除(P.S. dev即代表validation資料)
   3. 在 `/wav/dev`、`/wav/test`、`/wav/train`底下都加入名為`global`的資料夾，如下  
   ![本地圖片示例](https://scontent.ftpe3-2.fna.fbcdn.net/v/t1.15752-9/328472027_142504238749218_6882377873597117873_n.png?_nc_cat=102&ccb=1-7&_nc_sid=ae9488&_nc_ohc=sghCXzbATHgAX9Iwo7X&_nc_ht=scontent.ftpe3-2.fna&oh=03_AdQ4uXGgWuXSr3Wqx-iqX7aYprE9Ye6WWbDaSIpxwvPL6w&oe=64633E3E)
   4. 從kaggle上下載本次作業所需之客語音檔: [https://www.kaggle.com/competitions/espnet-taiwanese-asr1/data](https://www.kaggle.com/competitions/espnet-taiwanese-asr1/data)
   5. 將載下來的音檔皆放入 global 底下(validation至少需要20個檔案)
   6. 透過`for file in *.wav; do sox "$file" -b 16 "$file"; done`將音檔格式轉成 16 kHz sampling, signed-integer, 16 bits
   
## aishell_transcript_v0.8.txt
   1. 路徑：`/home/username/espnet/egs2/aishell/asr1/downloads/data_aishell/transcript/aishell_transcript_v0.8.txt`
   2. 從 kaggle 中下載 `train-toneless` ，用來替代 `aishell_transcript_v0.8.txt`
   3. 移除第一行的 "id"、"text"，並且需要參照原本`aishell_transcript_v0.8.txt`的格式
   4. 在後方加入`test a e i o u`，如下  
   ![本地圖片示例](https://scontent.ftpe3-2.fna.fbcdn.net/v/t1.15752-9/340852871_620752589523669_372926150382182444_n.png?_nc_cat=108&ccb=1-7&_nc_sid=ae9488&_nc_ohc=K5hOGSwabtIAX8ZE1pU&_nc_ht=scontent.ftpe3-2.fna&oh=03_AdSk5emg_NNelans2ReRv0F92K95-idMvqPylWdEOSfHmw&oe=6463295F)   
   5. 最後將`train-toneless`的檔名改成`aishell_transcript_v0.8.txt`
   
## lexicon.txt
   1. 路徑：`/home/username/espnet/egs2/aishell/asr1/downloads/resource_aishell/lexicon.txt`
   2. 直接以從kaggle下載下來的`lexicon.txt`取代掉
   
## speaker.info
   1. 路徑：`/home/username/espnet/egs2/aishell/asr1/downloads/resource_aishell/speaker.info`
   2. 刪除原本檔案裡面的所有內容
   3. 寫入 global F 即可
   
## data.sh
   1. 路徑：`/home/username/espnet/egs2/aishell/asr1/local/data.sh`
   2. 註解：
      - 23行：`data_url = #www.openslr.org/resources/33` 避免從網上下載
      - 52~55行： 下載資料
      - 115~116行： 刪除空格
   3. 新增：
      - 117行：paste  data/${x}/text
   
## train_asr_branchformer.yaml
   1. 路徑：`/home/username/espnet/egs2/aishell/asr1/conf/train_asr_branchformer.yaml`
   2. 修改第45行，調整 batch_size 大小，避免out of memory

## run.sh
   1. 路徑：`/home/username/espnet/egs2/aishell/asr1/run.sh`
   2. 第12行可更換 model
   3. 修改第26行，`--ngpu 1 \`
   
## 執行程式語法：
   - $ ./run.sh --ngpu 1 (ngpu 0 表示用cpu跑，ngpu 1 表示用1張gpu跑，以此類推)
   - $ ./run.sh --stage n (從上次中斷的第n個stage開始執行)
   - $ nohup ./run.sh (若train到一半網路中斷，確保仍可繼續執行)
   - $ watch nvidia-smi (隨時查看GPU使用狀況)
   - $ nvtop (隨時查看GPU使用狀況)
   - 可透過train.log查看訓練狀況

## Output結果
   1. 路徑：`/home/username/espnet/egs2/aishell/asr1/exp/asr_train_asr_branchformer_raw_zh_char_sp/decode_asr_branchformer_asr_model_valid.acc.ave/test/text`
      - 此為預測結果的檔案，將內容格式改為如同從 kaggle 下載下來的`sample.csv`後，即可上傳 kaggle 競賽
   2. 路徑：`/home/username/espnet/egs2/aishell/asr1/exp/asr_train_asr_branchformer_raw_zh_char_sp/decode_asr_branchformer_asr_model_valid.acc.ave/org/dev/score_wer/result.txt`
      - 查看績效
