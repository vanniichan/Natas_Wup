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

---
# Lv 8 --> 9
- Vào src code ta thấy có function passthru() hàm này có thể hiểu được nó thực thi các lệnh được gọi đến, chính vì thế có thể nó sẽ dễ xảy ra lỗ hổng OS Command

![image](https://github.com/vanniichan/Natas_Wup/assets/112863484/1c211703-026d-4db7-bf99-faa11accc1b9)

- Trước đó có lệnh `grep -i` nên không thể dùng lệnh `cat` luôn được mà trước đó phải dùng `;` để ngắt câu lệnh này

- Vì passwword luôn nằm ở /etc/natas_webpass/natas nên dùng lệnh này để lấy password
 `; cat /etc/natas_webpass/natas10`

---
# Lv 9 --> 10
- Vào src code ta thấy có function passthru() tuy nhiên đã bị filter 1 số ký tự

![image](https://github.com/vanniichan/Natas_Wup/assets/112863484/e251c2be-8c2b-4e02-a5c7-9868c1f40636)

- Tuy nhiên vẫn có 1 số cách như ("grep -i" " ...") vẫn dùng được
`"" cat /etc/natas_webpass/natas11`

---
# Lv 10 --> 11
- Vào xem src code

  ![image](https://github.com/vanniichan/Natas_Wup/assets/112863484/1545551f-fcd3-4010-83e6-d33382a80a73)

- Sơ qua ta thấy code này liên quan đến việc trao quyền cookie để có thể access vào lấy password 
- Biến đầu tiên có thể thấy biến có `showpassword ==> no` bây giờ làm sao chuyển thành `yes` để lấy pass
- Hàm dưới là sử dụng XOR thông qua `k = p^c` hiện tại chúng ta đã có p(plaintext). Vậy **mục tiêu đề ra** là  chuyển cho `showpassword ==> yes` và cần key(key sẽ không đổi vì nó dùng cho việc encode lại) để có được c(cipher)
- Dòng 4 hàm `loadData` cho thấy data từ cookie sẽ decode = base64

![Ảnh chụp màn hình 2024-01-23 232238](https://github.com/vanniichan/Natas_Wup/assets/112863484/7d70a451-ccec-4b73-bd4f-d53d0235b7a1)

- CHúng ta đã có c từ đây tìm ra k:
  
- ![image](https://github.com/vanniichan/Natas_Wup/assets/112863484/73a8c950-66da-4760-8cbc-551442d05ae1)

- ![image](https://github.com/vanniichan/Natas_Wup/assets/112863484/c0838e0f-a12a-49f0-a725-300d04fe3c35)

- k = 4 ký tự `KNHL`

- ![image](https://github.com/vanniichan/Natas_Wup/assets/112863484/3a4af070-472c-42ef-80e4-3ddad455ca06)

- Đổi cookie và lấy được password

---
# Lv 11 --> 12
- Src code bài này ở php không có gì đáng chú ý

![image](https://github.com/vanniichan/Natas_Wup/assets/112863484/692c23ae-2a16-4251-ac98-64890c352138)

- Tuy nhiên ở phần tag `input` ta thấy:

![image](https://github.com/vanniichan/Natas_Wup/assets/112863484/220f2e2d-13db-4591-9f7d-84061aca85f6)

- Tức là ta có thể thay đổi được đuôi file để sau đó vào đường link để đoạn code được thực thi
- F12 để đổi đuôi file và lấy được pass

![image](https://github.com/vanniichan/Natas_Wup/assets/112863484/2cea23cd-ab53-4a76-9b65-175f53f4b8dd)

---
# Lv 12 --> 1313
