---

# Slide 1: Title Slide
**Title:** Encryption Tool  
**Subtitle:** A Python-Based AES Encryption and Decryption Application  
**Presenter:** [Your Name]  
**Date:** [Date]

---

# Slide 2: Introduction
**Introduction**

- **Purpose**: To securely encrypt and decrypt files and directories using AES encryption.
- **Features**:
  - AES encryption in CBC mode
  - Password-based key derivation
  - Graphical User Interface (GUI)
  - Recursive directory handling

---

# Slide 3: Key Components
**Key Components**

1. **Key Derivation**:
   - **Algorithm**: PBKDF2HMAC with SHA-256
   - **Purpose**: Converts a password into a strong encryption key

2. **Encryption/Decryption**:
   - **Algorithm**: AES in CBC mode
   - **Padding**: PKCS7

3. **File Handling**:
   - Encrypts and decrypts individual files
   - Handles directories recursively

4. **GUI**:
   - User-friendly interface built with Tkinter

---

# Slide 4: Key Derivation
**Key Derivation**

- **Function**: `derive_key(password: str, salt: bytes) -> bytes`
- **Algorithm**: PBKDF2HMAC
- **Parameters**:
  - Password: User input
  - Salt: Randomly generated
- **Output**: 32-byte encryption key

**Code Snippet**:
```python
def derive_key(password: str, salt: bytes) -> bytes:
    kdf = PBKDF2HMAC(
        algorithm=hashes.SHA256(),
        length=32,
        salt=salt,
        iterations=100000,
        backend=default_backend()
    )
    return kdf.derive(password.encode())
```

---

# Slide 5: Encryption
**Encryption**

- **Function**: `encrypt_data(data: bytes, key: bytes) -> bytes`
- **Process**:
  - Generate Initialization Vector (IV)
  - Pad data using PKCS7
  - Encrypt data using AES

**Code Snippet**:
```python
def encrypt_data(data: bytes, key: bytes) -> bytes:
    iv = os.urandom(16)
    cipher = Cipher(algorithms.AES(key), modes.CBC(iv), backend=default_backend())
    encryptor = cipher.encryptor()
    padder = padding.PKCS7(algorithms.AES.block_size).padder()
    padded_data = padder.update(data) + padder.finalize()
    ciphertext = encryptor.update(padded_data) + encryptor.finalize()
    return iv + ciphertext
```

---

# Slide 6: Decryption
**Decryption**

- **Function**: `decrypt_data(data: bytes, key: bytes) -> bytes`
- **Process**:
  - Extract IV
  - Decrypt data using AES
  - Unpad data using PKCS7

**Code Snippet**:
```python
def decrypt_data(data: bytes, key: bytes) -> bytes:
    iv = data[:16]
    encrypted_data = data[16:]
    cipher = Cipher(algorithms.AES(key), modes.CBC(iv), backend=default_backend())
    decryptor = cipher.decryptor()
    padded_data = decryptor.update(encrypted_data) + decryptor.finalize()
    unpadder = padding.PKCS7(algorithms.AES.block_size).unpadder()
    return unpadder.update(padded_data) + unpadder.finalize()
```

---

# Slide 7: File Handling
**File Handling**

- **Encrypting Files**:
  - Reads file
  - Encrypts data
  - Saves as `.enc` file

- **Decrypting Files**:
  - Reads encrypted file
  - Decrypts data
  - Restores original file

**Code Snippets**:
```python
def encrypt_file(file_path: str, password: str):
    ...
def decrypt_file(file_path: str, password: str, master_password: str):
    ...
```

---

# Slide 8: Recursive Directory Handling
**Recursive Directory Handling**

- **Encrypting Directories**:
  - Walk through directory
  - Encrypt each file

- **Decrypting Directories**:
  - Walk through directory
  - Decrypt each `.enc` file

**Code Snippets**:
```python
def encrypt_directory(directory_path: str, password: str):
    ...

def decrypt_directory(directory_path: str, password: str, master_password: str):
    ...
```

---

# Slide 9: GUI Overview
**GUI Overview**

- **Components**:
  - Path entry field
  - Password entry fields
  - Buttons for browse, encrypt, and decrypt

- **Features**:
  - Browse for files or directories
  - Input passwords
  - Perform encryption/decryption

**Code Snippet**:
```python
class EncryptionApp:
    def __init__(self, master):
        ...
```

---

# Slide 10: Usage Instructions
**Usage Instructions**

1. **Start the Application**:
   - Run `encrypt.py`

2. **Select File/Directory**:
   - Use the "Browse" button

3. **Enter Password**:
   - For encryption or decryption

4. **Perform Operation**:
   - Click "Encrypt" or "Decrypt"

5. **Provide Master Password**:
   - For decryption if needed

---

# Slide 11: Security Considerations
**Security Considerations**

- **Password Management**: Use strong, unique passwords
- **Key Storage**: Ensure secure handling of salts and keys
- **Error Handling**: Handle decryption errors and password mismatches securely

---

# Slide 12: Future Improvements
**Future Improvements**

- **Progress Indicators**: For large files or directories
- **Advanced Error Handling**: More robust error messages and recovery
- **User Experience Enhancements**: Improved GUI and feedback mechanisms

---

# Slide 13: Q&A
**Questions & Answers**

- Open the floor for questions and provide answers as needed.

---

# Slide 14: Contact Information
**Contact Information**

- **Email**: [Your Email]
- **Website**: [Your Website]

---
