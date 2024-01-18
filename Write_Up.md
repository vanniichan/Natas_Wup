# Lv 0 --> 1
Không có gì


---

# Lv 1 --> 2

- F12 thấy có 1 thẻ img 

![Ảnh chụp màn hình 2024-01-18 042133](https://github.com/vanniichan/Natas_Wup/assets/112863484/3e81c8e1-5375-46e1-af31-758a4ddfd723)

- Thử kiểm tra xem path /file có chứa những gì không 

![Ảnh chụp màn hình 2024-01-18 042247](https://github.com/vanniichan/Natas_Wup/assets/112863484/12fe78bc-3bb4-41b8-b4f4-3a48e8311860)

- Ở đây có một file `/user.txt` mở file này và lấy được password



---
# Lv 2 --> 3
- Check file `/robots.txt` và nó cho mình 1 path đến file `/user.txt`
  
![image](https://github.com/vanniichan/Natas_Wup/assets/112863484/ecab6b5c-7548-431d-baa1-f4f8429d37b4)

---
# Lv 3 --> 4
- Bài này gg lòi mắt được nhưng hiểu được nó liên quan đến `Referer` và cần phải set lại nó để có quyền access
- Dùng `curl` để in nội dung sau khi sửa lại `referer` ```curl -u natas4:tKOcJIbzM4lTs8hbCmzn5Zr4434fGZQm --referer http://natas5.natas.labs.overthewire.org/ http://natas4.natas.labs.overthewire.org```  
![image](https://github.com/vanniichan/Natas_Wup/assets/112863484/ec74ae8f-71ba-4bc9-8d04-e75569b936e6)

---
# Lv 4 --> 5
- Thường có thông báo Acess not allow mình sẽ thường check cookie của nó thì thấy có 1 trường loggedin với value là 0 tức là không cho phép

![image](https://github.com/vanniichan/Natas_Wup/assets/112863484/e52026fa-fa91-41c4-97fc-98d84a428d7c)

- Sửa lại 1 và Refresh trang và lấy được pass

---
# Lv 5 --> 6
- Xem src code site, ta có đoạn mã như sau:
- 
![image](https://github.com/vanniichan/Natas_Wup/assets/112863484/fa064fb6-e68b-4e01-93f5-9dd657bd37b7)

- Đoạn code này so sánh input có khớp với nôi dung file `secret.inc`. Và như đoạn code này ngta còn để lộ path để lấy nội dung file này
  
![image](https://github.com/vanniichan/Natas_Wup/assets/112863484/9a2e3add-f357-44c2-8450-a5680212f3d7)
---
# Lv 6 --> 7
- Mở src code thấy hint:
- Cái này nghĩ đến IDOR thử và thành công luôn 
`http://natas7.natas.labs.overthewire.org/index.php?page=/etc/natas_webpass/natas8`

---
# Lv 7 --> 8
- Vào src code ta thấy một code đã encode
  
![image](https://github.com/vanniichan/Natas_Wup/assets/112863484/1c54a40e-da5b-4f2c-ad97-c9b0d6a85959)

- Viết payload để decode nó ra
  
![image](https://github.com/vanniichan/Natas_Wup/assets/112863484/e2114681-183f-4088-8f9e-2f98e4062d45)

