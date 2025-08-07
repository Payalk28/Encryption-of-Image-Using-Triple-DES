# 🔐 Image Encryption & Decryption GUI using Triple DES


## 📂 Project Structure

- `main.py` — Main entry point with GUI for choosing encryption or decryption.
- `encrypt_img.py` — Handles image encryption using Triple DES and SHA-256 hashing.
- `decrypt_img.py` — Handles image decryption and integrity verification.

---


## 🛠️ Technologies Used

- **Python**
- **Tkinter** — GUI framework
- **PyCryptodome** — Cryptographic library for Triple DES
- **Pyperclip** — Clipboard support
- **Secrets & String** — For secure key generation
- **Hashlib** — SHA-256 hashing
- **File Dialogs** — For image selection

---


## 🔐 Features

### ✅ Encryption (`encrypt_img.py`)
- Select `.jpg`, `.jpeg`, or `.png` image files.
- Generate a secure 16-character encryption key.
- Encrypt image data using Triple DES in `MODE_CFB`.
- Pad image data to match block size using `@`.
- Append SHA-256 hash of original padded data to encrypted file.
- Display encryption success message and copy key to clipboard.

### 🔓 Decryption (`decrypt_img.py`)
- Select encrypted image file.
- Enter the 16-character encryption key.
- Extract and verify SHA-256 hash from encrypted file.
- Decrypt image data using Triple DES.
- **⚠️ Note:** There is a known logical flaw in the integrity check:
  - The application incorrectly proceeds with decryption when hashes **do not match**.
  - It incorrectly shows an error when hashes **do match**.
  - This logic should be reversed to ensure proper integrity verification.

---


## 🧪 How It Works

### Encryption Flow:
1. User selects an image file.
2. A 16-character key is generated.
3. Image data is padded and encrypted using Triple DES.
4. SHA-256 hash of the padded data is calculated.
5. Encrypted data + hash (`&&hashIs=` + hex digest) is saved to a new file.

### Decryption Flow:
1. User selects encrypted file and enters key.
2. Hash is extracted from the end of the file.
3. Encrypted data is decrypted using Triple DES.
4. SHA-256 hash of decrypted data is calculated.
5. Hashes are compared to verify integrity.
6. **Logical bug:** Integrity check logic is reversed and needs correction.

---


## 🚧 Known Issues

- ❌ **Integrity Check Bug in `decrypt_img.py`:**
  - The condition `if res.hexdigest() != str(hashcode.decode())` is incorrect.
  - It should be `if res.hexdigest() == str(hashcode.decode())` to validate integrity correctly.

 
