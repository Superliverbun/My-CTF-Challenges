

##### 攻擊主機：Kali_Linux_2019.3 
##### 靶機：JIS-CTF-VulnUpload-CTF01

**Kali>** <code>arp-scan -l</code> (尋找靶機)<br/>
**Kali>** <code>nmap -A 192.168.203.132</code> (去看他開啟了甚麼port) <br/>
![image](https://github.com/Superliverbun/My-CTF-Challenges/assets/113052517/587481ef-dc6a-4eb7-b822-6aaab8f60a39)
(我發現他開啟了22port，那就可以走簡單的ssh，也發現他有開samba 我選擇走enum4linux)<br/>
**Kali>** <code>enum4linux 192.168.203.132</code> (掃描，看看能掃到甚麼)<br/>
![image](https://github.com/Superliverbun/My-CTF-Challenges/assets/113052517/934b796a-fdba-4e40-9714-ea289b312fed)
(得到兩個使用者帳號 Kay 和 Jan)<br/>
(Jan 權限較低，較好攻擊)<br/>

