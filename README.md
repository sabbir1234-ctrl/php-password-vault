# PHP Password Vault

An object-oriented **PHP password manager**: users register and log in, then save passwords for different websites. The saved passwords are **encrypted** in the database, not stored as plain text.

![PHP](https://img.shields.io/badge/PHP-OOP-777BB4?logo=php&logoColor=white) ![MySQL](https://img.shields.io/badge/MySQL-PDO-4479A1?logo=mysql&logoColor=white)

## Features

- **Register / log in.** Account passwords are hashed with **bcrypt** (`password_hash` / `password_verify`).
- **Per-user encryption key.** Each user gets a key derived at sign-up, and saved site passwords are encrypted with **OpenSSL AES** before they reach the database.
- **Add, view and decrypt** saved passwords on a personal dashboard.
- **Password generator:** choose the length and the number of lowercase, uppercase, digit and special characters, or type your own password.
- **PDO prepared statements** for all queries (protects against SQL injection).
- Output is escaped with `htmlspecialchars` (protects against XSS).

## Structure

```
classes/User.php              registration, login, encryption key
classes/PasswordManager.php   save, list, encrypt and decrypt passwords
classes/PasswordGenerator.php random password generation
config/Database.php           PDO connection
public/                       register, login, dashboard, add and view pages
sql/schema.sql                users and passwords tables (foreign key, ON DELETE CASCADE)
```

## Run locally (XAMPP)

1. Import `sql/schema.sql` in phpMyAdmin (it creates the `passwords_db` database).
2. Check the database settings in `config/Database.php`.
3. Put the folder in `htdocs` and open `http://localhost/php-password-vault/public/register.php`.

> Learning project. For production I would switch the cipher mode from ECB to an authenticated mode such as AES-GCM with a random IV.
