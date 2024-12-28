# 问卷星 RSA 加密
访问地址： https://www.wjx.cn/login.aspx  
随机输入用户密码：123123/123123  
查看数据包看到 password 字段加密  
![image](https://github.com/user-attachments/assets/239451c7-34ea-4789-8b86-477162e2a159)  

搜索 password 字段，筛选有用信息后，找到如下代码  
![image](https://github.com/user-attachments/assets/0e38bc0a-3ddb-4237-be47-11b4b2b1a052)  

> 代码解释：  
Password 可能是一个指向某个 HTML <input> 元素的引用，这个元素用来接收用户输入的密码。Password.value 就是获取用户输入的密码文本。  
该密码文本会作为参数传递给 DoRsaEncrypt 函数，后者使用加密算法对密码进行加密，并返回加密后的密码。  
加密后的密码会被重新赋值给 Password.value。  

跟踪函数继续查看，能看到公钥，使用的是rsa 512 位加密  
![image](https://github.com/user-attachments/assets/1bd69317-525c-474d-941c-e849f88b7eb6)

## 编写代码还原：  
![image](https://github.com/user-attachments/assets/2427f95b-6d70-4496-81da-4afe93a104a2)


> RSA 加密算法本身不直接生成固定的加密结果，原因在于 RSA 加密通常结合了一个随机数（通常称为“填充”或“padding”） 来保证每次加密的结果不同，即使输入相同。  
填充机制（Padding）：为了增强 RSA 的安全性和避免一些攻击（如选择明文攻击），RSA 加密通常会使用一种称为 填充 的技术。这些填充方法会在加密前对明文数据进行一定的处理，以确保每次加密的结果不同。  
