### 攻擊主機：Kali_Linux_2019.3 
### 靶機：RickdiculouslyEasy
#### 掃描
**Kali>**<code>nmap -v -sS -O -A -p- 140.138.53.186</code></br>
###### 找到第一支旗子🚩
![image](https://github.com/Superliverbun/My-CTF-Challenges/assets/113052517/37b3e4f1-4cb2-4649-81ad-e765977894ca)
#### 看看奇怪的60000port 
**Kali>** <code>nc 140.138.53.186 60000</code></br>
###### 找到第二支旗子🚩
![image](https://github.com/Superliverbun/My-CTF-Challenges/assets/113052517/5c1405ac-e18f-405d-a769-9809180951dd)
</br>
(他也有開80port)</br>
**Kali>** <code>dirb http:// 140.138.53.186</code></br>
![image](https://github.com/Superliverbun/My-CTF-Challenges/assets/113052517/15553221-aa97-4471-8c88-8dbe4f7a6744)
###### 在網站中找到第三支旗子🚩
![image](https://github.com/Superliverbun/My-CTF-Challenges/assets/113052517/180ee0af-c23a-45d9-9416-5f96e8ed0db1)
</br>
#### 看看9090port
###### 找到第四支旗子🚩
![image](https://github.com/Superliverbun/My-CTF-Challenges/assets/113052517/e986a246-ea88-47d1-9c22-6271769b9839)
</br>
#### 看看ftp
###### 第五支旗子🚩
![image](https://github.com/Superliverbun/My-CTF-Challenges/assets/113052517/3394afc0-6b9f-4a6e-9a8e-df808b4c45c6)
</br>
(在http:// 140.138.53.186的開發人員工具有寫密碼是winter)</br>
**Kali>** hydra -L users.txt -p winter </br>
**Kali>** ssh://192.168.43.27:22222</br>
(得到使用者Summer)</br>
#### 登入
###### 找到第六支旗🚩</br>
![image](https://github.com/Superliverbun/My-CTF-Challenges/assets/113052517/635ce820-db4b-4243-a1d5-09828d32d9d3)
</br>
在summer的權限下，將位置跳到其他使用者，讀取檔案進行解密</br>
###### 得到第七支旗🚩</br>
![image](https://github.com/Superliverbun/My-CTF-Challenges/assets/113052517/3d294b21-df1d-402f-a4b1-6fa19bcf2193)
移動檔案並加入上個旗提示的參數</br>
###### 得到第八支旗🚩</br>
![image](https://github.com/Superliverbun/My-CTF-Challenges/assets/113052517/0ec1b0b0-f0c3-4727-9342-3aca206ac69b)
</br>
接下來的作法，教授不予苟同，但是我認為這很快很好用。</br>
因為取得了Rick的權限，可以用sudo變成root，於是我就在各個檔案夾中搜尋關鍵字”FLAG”，得到了最後的旗子</br>
![image](https://github.com/Superliverbun/My-CTF-Challenges/assets/113052517/7cd2e73b-9f8d-45ad-8b5a-696164ff9d5b)</br>
這個專題是我們第一次實戰CTF，緊張的氣氛加上不知道下一支旗會在哪蹦出來的期待感讓我深深的愛上這個競賽，我努力鑽研並學習更多的手法來應對下一次的競賽。
