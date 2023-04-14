# outline-docker-compose

快速安裝一個自托管的 [Outline](https://github.com/outline/outline) wiki

## 功能:

1. 以簡單的make和bash腳本來生成所有所需的設定
1. 以`docker-compose`或`docker compose`來執行服務
1. 以 [MinIO](https://github.com/minio/minio) 代替AWS S3，實現真正自托管
1. 以 [OIDC server](https://github.com/vicalloy/oidc-server) 來管理使用者，無需通過slack或google登錄

## 如何使用

1. 初始化系統
    ```
    git clone https://github.com/vicalloy/outline-docker-compose.git
    cd outline-docker-compose
    cp scripts/config.sh.sample scripts/config.sh
    # 更新配置文件：vim scripts/config.sh
    make install  # 創建docker-compose配置文件並啟動它，隨後初始化oidc-server（為outline添加oidc客戶端並創建超級用戶）
    ```
1. 打開 `http://127.0.0.1:8888` 並登錄到Outline
1. 打開 `http://127.0.0.1:8888/uc/admin/auth/user/` 來添加新用戶

## scripts/config.sh

設定檔 [scripts/config.sh.sample](scripts/config.sh.sample)

## Makefile

- `make install` 建立docker-compose設定檔並啟動。初始化oidc-server（為outline添加oidc使用者端並創建超級使用者）
- `make start` 啟動Outline
- `make stop` 停止Outline
- `make clean` 刪除腳本生成的所有設定檔
- `make clean-data` ⚠️ 清除所有資料


## 常見問題解答

1. Q: 添加了新的使用者，但無法登錄Outline
    - 你應該為新的使用者添加電子郵件
    - 如果電子郵件中的域名與管理員的域名不同，你應該將該域名添加到設置`ALLOWED_DOMAINS`中
