# WEB-SERVER


* [web-server](#web-server)
* [Apache ](#apache)
* [在virtualbox中安裝web-server](#在virtualbox中安裝web-server)
  - [網路更改橋接介面卡](#網路更改橋接介面卡)
  - [更新](#更新)
  - [安裝apache](#安裝apache)
  - [查看apache的狀態](#查看apache的狀態)
  - [查看ip](查看ip)
  - [修改主網頁](#修改主網頁)
  - [個人網站功能](#個人網站功能)
* [系統日誌](#系統日誌)
* [參考資料](#參考資料)

## web-server
網頁伺服器程式都需要從網路接受HTTP請求，然後提供HTTP回覆給請求者。HTTP回覆一般包含一個HTML檔案，有時也可以包含純文字檔案、圖像或其他類型的檔案。

一般來說這些檔案都儲存在網頁伺服器的本地檔案系統裡，伺服器會簡單的把URL對照到本地檔案系統中。當正確安裝和設定好網頁伺服器軟體，伺服器管理員會從伺服器軟體放置檔案的地方指定一個本地路徑名為根目錄。

- Web Server 的基本功能流程如下：

1. web server收到瀏覽器所傳來的網址
2. 取出相對應的檔案
3. 將檔案內容傳回給瀏覽器

![1652793397817](https://user-images.githubusercontent.com/105623904/168819988-9acac526-bd0c-470f-ac2f-b70d7558c400.jpg)

## Apache
Apache HTTP Server（簡稱Apache）是Apache軟體基金會的一個開放原始碼的網頁伺服器軟體，可以在大多數電腦作業系統中運行。由於其跨平台和安全性，被廣泛使用，是最流行的Web伺服器軟體之一，維基百科網站的伺服器就使用了Apache。

## 在virtualbox中安裝web-server

### 網路更改橋接介面卡 

![網路改橋接介面卡1](https://user-images.githubusercontent.com/105623904/168826654-e3007f0a-a4e8-491a-bdd2-975579380cfe.jpg)
![網路改橋接介面卡2](https://user-images.githubusercontent.com/105623904/168826660-e4cd41aa-0fd2-4035-83b1-448bc8372643.jpg)


### 更新

```
sudo apt-get update 
sudo apt-get upgrade
```

### 安裝apache

```
sudo apt install apache2
```

### 查看apache的狀態
確認狀態為active
```
sudo systemctl status apache2
```
![apache狀態圖](https://user-images.githubusercontent.com/105623904/168845254-3f251372-32a8-47e1-9724-94f1e8fc9c4b.jpg)


### 查看ip

```
hostname -I
```

### 開啟瀏覽器並輸入IP，確認跳出APACHE預設主網頁
![apache預設主網頁](https://user-images.githubusercontent.com/105623904/168847359-1c029ff0-92fd-416a-9b21-23e9662be794.jpg)


### 修改主網頁
- 進入主網頁html檔案

```
sudo nano /var/www/html/index.html
```
- 將檔案原內容全部刪除，並放入以下內容，儲存並退出
```
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>主網頁測試</title>
</head>
<body>
	這是主網頁
</body>
</html>

```
![修改主網頁html檔案](https://user-images.githubusercontent.com/105623904/168848449-372a3ca9-d9ad-44ae-9c47-a310640915ce.jpg)

- 將網頁重新整理即可看到網頁內容改變

![主網頁](https://user-images.githubusercontent.com/105623904/168848754-7eea369d-a3cf-4a05-ae83-d94f4cf2d21d.jpg)


## 個人網站功能
- 進入目錄

```
cd /etc/apache2/mods-enabled
```
- 在目錄中建立軟式連結

```
sudo ln -s ../mods-available/userdir.conf
```
- 目錄中再建立另一個軟式連結

```
sudo ln -s ../mods-available/userdir.load
```
![軟式連結](https://user-images.githubusercontent.com/105623904/168849922-91ebc5ee-fea6-4920-8e10-3f61307aeec7.jpg)

- 編輯userdir.conf

```
sudo nano userdir.conf
```

- 刪除option之indexs參數，儲存離開

![刪除option1](https://user-images.githubusercontent.com/105623904/169029072-aeb6aef5-2fc2-4863-aba0-8f98f8b80abd.jpg)

![刪除option2](https://user-images.githubusercontent.com/105623904/169029092-f2bdc708-31d3-40cb-94fb-86e2084b8a00.jpg)

- 重啟apache
 ```
sudo systemctl restart apache2 
```

- 為使用者建立存放個人網頁的目錄(圈起來的地方請修改成自己的使用者名稱)
 ```
mkdir /home/b1042303/public_html
```
![個人網頁目錄](https://user-images.githubusercontent.com/105623904/169030516-0608618a-6366-49c7-bc69-a931a1db0b05.jpg)

- 為使用者創建html檔(注意路徑)
```
nano /home/b1042303/public_html/index.html
```
- html檔內容放入
```
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>個人網頁測試</title>
</head>
<body>
	這是個人網頁
</body>
</html>
```
![個人網頁內容](https://user-images.githubusercontent.com/105623904/169032891-1fb79176-ac0a-4fa3-8c4e-cd25891622f9.jpg)

- 開啟瀏覽器並輸入IP及使用者名稱(注意要加波浪符)，即可看到個人網頁

![1652875102872](https://user-images.githubusercontent.com/105623904/169033590-1c055d88-6d87-468c-aa74-911d4a3a5d46.jpg)

## 系統日誌
安裝Apache後，會在 /var/log/apache2 目錄中建立日誌文件，查看這些日誌可了解與Web伺服器相關的問題。 /var/log/apache2目錄下的日誌文件如下:

1.access.log:訪問您的網站的人已訪問了哪些文件的日誌。它包含有關傳輸是否成功完成，請求的來源(IP地址)，傳輸了多少數據以及傳輸發生在何時的訊息。

2.error.log:包含Apache中發生的所有錯誤。並非所有發生的錯誤都是致命的，有些僅僅是客戶端連接的問題。


- 查看access.log，顯示文件的最後10行內容。
```
sudo tail /var/log/apache2/access.log
```

- 查看最後20行的錯誤訊息。
```
sudo tail -n 20 /var/log/apache2/error.log
```

- 及時查看錯誤或正在生成的日誌。
```
sudo tail -n 10 -f /var/log/apache2/error.log
```
## 參考資料
 [https://ithelp.ithome.com.tw/articles/10225447](https://ithelp.ithome.com.tw/articles/10225447)
 [https://zh.wikipedia.org/wiki/%E7%B6%B2%E9%A0%81%E4%BC%BA%E6%9C%8D%E5%99%A8](https://zh.wikipedia.org/wiki/%E7%B6%B2%E9%A0%81%E4%BC%BA%E6%9C%8D%E5%99%A8)
