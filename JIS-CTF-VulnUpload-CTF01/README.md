

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
