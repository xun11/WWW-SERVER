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
  - [開啟個人網站功能](#開啟個人網站功能)





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


## 開啟個人網站功能
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










