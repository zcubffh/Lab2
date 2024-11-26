# Task 1: Public-key based authentication 
**Question 1**: 
Implement public-key based authentication step-by-step with openssl according the following scheme.
![alt text](image-1.png)

**Answer 1**:
Step1:
Tạo cặp khóa RSA cho client, bao gồm một khóa riêng(private key) và 1 khóa công khai(public key).
Lệnh tạo khóa riêng: openssl genrsa -out client_private.pem 2048
Lệnh tạo khóa công khai: openssl rsa -in client_private.pem -pubout -out client_public.pem
<img width="500" alt="Screenshot" src="https://github.com/zcubffh/Lab2/blob/main/image-2.png?raw=true"><br>
Step2:
Tạo file có thông điệp thử thách: echo "This is a challenge message" > challenge.txt
Mã hóa thông điệp sử dụng khóa công khai: openssl pkeyutl -encrypt -inkey client_public.pem -pubin -in challenge.txt -out challenge.enc
Step3:
Client nhận thông điệp mã hóa từ server, chạy lệnh để giải mã:openssl pkeyutl -decrypt -inkey client_private.pem -in challenge.enc -out challenge_decrypted.txt
Sau đó thông điệp đã được mã hóa xong.
 <img width="500" alt="Screenshot" src="https://github.com/zcubffh/Lab2/blob/main/image-3.png?raw=true"><br>
 Step4:
 Client sử dụng khóa riêng để ký thông điệp giải mã, chứng minh rằng client đã được sở hữu khóa riêng một cách hợp lệ.
 openssl dgst -sha256 -sign client_private.pem -out challenge_signed.sig challenge_decrypted.txt
 Sau đó, client sẽ gửi trả file challenge cho server để xác minh.
 Step 5:
 Server sử dụng khóa công khai của Client để xác minh chữ ký. Xác nhận rằng chữ ký nhận được là từ Client là hợp lệ.
 openssl dgst -sha256 -verify client_public.pem -signature challenge_signed.sig challenge.txt
Kết quả đúng sẽ là:
<img width="500" alt="Screenshot" src="https://github.com/zcubffh/Lab2/blob/main/image.png?raw=true"><br>

# Task 2: Encrypting large message 
Create a text file at least 56 bytes.
**Question 1**:
Encrypt the file with aes-256 cipher in CFB and OFB modes. How do you evaluate both cipher as far as error propagation and adjacent plaintext blocks are concerned. 
**Answer 1**:

**Question 2**:
Modify the 8th byte of encrypted file in both modes (this emulates corrupted ciphertext).
Decrypt corrupted file, watch the result and give your comment on Chaining dependencies and Error propagation criteria.

**Answer 2**:





