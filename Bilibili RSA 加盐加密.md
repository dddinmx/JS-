# Bilibili RSA 加盐加密
访问地址： https://www.bilibili.com/  
![image](https://github.com/user-attachments/assets/85655769-1af6-432a-b1b1-8aa0f52b22fe)

搜索password关键词，查看所有定位到搜索，跟栈定位到handlerLogin方法如下，函数 br 应为加密函数  
![image](https://github.com/user-attachments/assets/2ab424d6-639a-4b69-b4f6-902ad34221a4)  
![image](https://github.com/user-attachments/assets/919c04de-40f0-4173-8149-c06fa0907caa)  
![image](https://github.com/user-attachments/assets/c5d3b9f2-5e09-4c9d-9154-3ce1d1f07e3d)  



> 代码解释：  
获取表单中的密码 (e.subForm.password)  
调用 br() 函数加密密码  


追进函数 br 继续查看，打断点一步一步测试  
![image](https://github.com/user-attachments/assets/1d42df26-5690-4cd8-bef9-3ee0d7c118eb)  
找到公钥  
![image](https://github.com/user-attachments/assets/c348607f-22b2-4a7e-9650-4c1bbf1ffafe)  

下一步将字符串+密码组成一个新字符串丢进加密算法加密  
![image](https://github.com/user-attachments/assets/737eee8d-4413-4d9a-95b6-742c0c8ce7eb)  
![image](https://github.com/user-attachments/assets/1afb46ae-978a-40bb-8231-60897ec62c56)  


跟进加密算法，看到将拼接后的字符串丢进来了  
![image](https://github.com/user-attachments/assets/3538d80c-a9af-40ea-888e-1e01d733136f)  

继续跟进加密函数，看到最终的加密算法  
![image](https://github.com/user-attachments/assets/816dc07b-e54c-4c7f-a508-75a635784e47)  

目前确认 bilibili 为加盐 RSA 加密，既 password = RSA（字符串+密码）  

接下来寻找公钥和字符串，重新发起查询，记录公钥和字符串  
![image](https://github.com/user-attachments/assets/6fc546a9-70cf-405d-b771-2e1cc6632e5a)

全局搜索字符串，可看到这两个值均为请求服务器返回的值  
![image](https://github.com/user-attachments/assets/609e1c08-d3af-4450-8192-97b06eb37e04)


## bilibili 加密逻辑：  
``Password = RSA(随机字符串（盐）+密码)  ``


