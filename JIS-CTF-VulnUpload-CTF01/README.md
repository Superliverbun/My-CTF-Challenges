

### 攻擊主機：Kali_Linux_2019.3 
### 靶機：JIS-CTF-VulnUpload-CTF01

#### 搜尋靶機IP
> **Kali>** <code>arp-scan -l</code> </br>
![image](https://github.com/Superliverbun/My-CTF-Challenges/assets/113052517/e53f9a10-cfff-4cc6-8ea3-7891432dcc6c)</br>
💡：去掉頭跟尾(IP)，確定靶機為192.168.203.129


#### 弱點掃描
> 使用nmap進行弱掃
**Kali>** <code>nmap -v -sS -O -A -p- 192.168.203.129</code> </br>
![image](https://github.com/Superliverbun/My-CTF-Challenges/assets/113052517/6ced9f28-af7e-4be8-bbe9-12c976a83bc6)</br>
💡得知有開啟22port和80port

#### 先看看http://192.168.203.129
> 意外發現第四支旗
> ![image](https://github.com/Superliverbun/My-CTF-Challenges/assets/113052517/1b4aea6e-8720-47a5-a6ab-4ba0bb10bb08) <br/>
> (在Inspect Element中)
> 解碼之後：
> ![image](https://github.com/Superliverbun/My-CTF-Challenges/assets/113052517/90dd9069-88ed-4e84-bb42-b2909b14955f)
```js
    There is a vuln of upload service on the next page after you log in. Please find the php-reverse-shell.php under /usr/share/webshells/php in kali linux. In order to get the reverse session from target, run nc -lvnp port#. Edit the "CHANGE THIS" in the  php-reverse-shell.php and then upload it :10 points
```
> 這個線索告訴我接下來要用反向工程，但我先把1~3支旗找回來

#### 使用dirb嘗試看看
![image](https://github.com/Superliverbun/My-CTF-Challenges/assets/113052517/378d385b-8ddc-4073-9f80-a24841b581d4)
![image](https://github.com/Superliverbun/My-CTF-Challenges/assets/113052517/954f81f4-387a-4f15-aa83-fdcdeba341ba)
> 在http://192.168.203.129/flag找到第一支旗
![image](https://github.com/Superliverbun/My-CTF-Challenges/assets/113052517/3029e6e9-a3a2-4390-91ad-1f08fa929ecd)
```js
    This is a Jimmy's Cyber Class:10 points
```
![image](https://github.com/Superliverbun/My-CTF-Challenges/assets/113052517/dd47bca4-4bc2-4d34-963a-36900ca3a86b)
> 並在admin_area中找到第二支旗，還附了admin的帳密
![image](https://github.com/Superliverbun/My-CTF-Challenges/assets/113052517/b017c504-588b-4e7c-ae12-8f6d97677872)
```js
    You might have great time in this security class:10 points
```
> 在CSS中找到hint檔案，找到第三支旗
![image](https://github.com/Superliverbun/My-CTF-Challenges/assets/113052517/eaed5634-4316-43a6-9f16-86afdf364032)
![image](https://github.com/Superliverbun/My-CTF-Challenges/assets/113052517/e5449597-ff8a-4b4e-a411-86f6ff4b8ead)
![image](https://github.com/Superliverbun/My-CTF-Challenges/assets/113052517/3577cf9d-dbc5-4caa-87d0-714a526f7033)
```js
    Of course you know password crack is illegal:10 points
```

#### 使用第二支旗給的帳密
> 在http://192.168.203.129/login.php(第四支旗的網頁)進入了可以上傳資料的網頁

