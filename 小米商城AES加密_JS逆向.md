# 小米商城AES加密 JS逆向

登录地址：https://account.xiaomi.com/fe/service/login/password  
![image](https://github.com/user-attachments/assets/9f0be799-ffbd-4354-bac1-efd3ac8f4d36)

登录看数据包  
![image](https://github.com/user-attachments/assets/c61c8871-4001-409d-a0e0-b063b7b9b252)  

全局搜索 hash:  
找到像加密的部分选择打断点  
![image](https://github.com/user-attachments/assets/3464612f-c299-455e-9b96-fc1fab61d9ae)

成功断住看到明文为 123456，追进函数 v()查看  
![image](https://github.com/user-attachments/assets/c8f94bee-846d-4cb1-a9c4-3bba25e8a363)  

打断点后看到调用了两个函数wordsToBytes()和bytesToHex()  
![image](https://github.com/user-attachments/assets/85fd1f97-f88f-4f98-94a7-bfbe7d659061)  
![image](https://github.com/user-attachments/assets/143a8cea-e969-4103-9ef9-b0bdf9dacd0d)  

 32 位可能为 md5 加密，验证：  
![image](https://github.com/user-attachments/assets/b4a8d47b-1f79-49a8-b88a-d639365a3e01)  


接下来看 user 部分  
继续打断点，往上追踪  
![image](https://github.com/user-attachments/assets/c64015ba-1821-4bac-ac0b-626ff0043f77)  

找到 h，追进去函数打断点测试  
![image](https://github.com/user-attachments/assets/03d16465-bcac-419c-87f5-666f44c34883)  
![image](https://github.com/user-attachments/assets/d2fd0399-9c11-406a-afc7-cf7a5169661c)  

可知偏移量为 s 固定值：0102030405060708  
密钥为 e：L^F17qQES7hUQzA8  
## 验证：  
![image](https://github.com/user-attachments/assets/4f916c0f-2297-4b96-b179-4daef3d81f55)
