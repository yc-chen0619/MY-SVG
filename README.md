# Self-Driving Cars - Midterm Project (Localization)

此專案為自駕車定位 (Localization) 模組，包含 ROS 環境的 Docker 容器化設定，以及處理 Track 1 與 Track 2 測資的程式碼。

## 環境安裝與準備 (Environment Setup)

1. **解壓縮專案檔案**
    請將 `midterm_314512056.zip` 內的物件解壓縮並放入以下指定路徑： <br>
    "/home/yc-chen/self_driving_cars_ws/midterm01/"
    * 實際架構如下 <br>
        yc-chen@v:~$ cd self_driving_cars_ws/midterm01/ <br>
        yc-chen@v:~/self_driving_cars_ws/midterm01$ ls <br>
        Dockerfile  build  data  devel  docker-compose.yml  ros_entrypoint.sh  save_data  src <br>
2. **放置測資 (Data)** <br>
    請將 track1 與 track2 的資料夾放入以下路徑：  <br>
    "/home/yc-chen/self_driving_cars_ws/data/"
3. **建置與啟動 Docker 容器** <br>
    打開 Terminal，進入專案目錄並使用 Docker Compose 啟動環境： <br>
   $ cd /home/yc-chen/self_driving_cars_ws/midterm01/ <br>
   $ sudo docker compose build <br>
   $ sudo docker compose up -d
4. **進入 Docker 環境** <br>
   $ sudo docker exec -it midterm01-sdc_ros1_dev-1 bash

## 程式編譯與執行 (Build & Usage)

1. **進入工作區並編譯** <br>
    $ cd ~/midterm <br>
    $ catkin_make
2. **載入環境變數** <br>
    $ source devel/setup.bash
3. **啟動 Localization 程式** <br>
    $ roslaunch localization localization.launch

## 其他補充與進階設定 (Additional Notes)

1. **切換 Track 1 與 Track 2 測資**
    Launch 檔設定：localization.launch 中已寫好對應的路徑參數。
    C++ 程式碼修改：若要切換軌跡，請打開原始碼，在 localization.cpp 中的 Localization(int argc, char** argv) 函式內，更改相對應讀取的參數名稱即可。

2. **輸出平滑化 CSV 檔 (軌跡後處理)**
    若需將輸出的 TXT 軌跡轉換並優化為 CSV 格式，請使用內附的 Python 腳本：
    1. 打開 txt_to_idx_x_y_yaw.py，至程式碼最下方確認檔案輸入與輸出的邏輯。
    2. 在 Docker 的 Terminal 中，切換到該腳本所在的目錄：
        $ cd /root/midterm/src/localization/processing_codes/
    3. 貼上指令並執行，即可生成最終的軌跡 CSV 檔。實際的執行指令（例如）：
        $ python3 txt_to_idx_x_y_yaw.py /root/midterm/src/localization/result/result_1.txt /root/midterm/src/localization/result/result_1.csv
   
