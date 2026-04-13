## 1. General Security Principles

Basic rules that apply everywhere: - Never trust user input - Validate
and sanitize all inputs - Use least privilege - Keep systems updated

------------------------------------------------------------------------

## 2. Cross-Site Scripting (XSS)

**Brief:** Injecting malicious JS that runs in users' browsers.

**Prevention:** - Escape output with `htmlspecialchars()`

``` php
echo htmlspecialchars($user_input, ENT_QUOTES, 'UTF-8');
```

------------------------------------------------------------------------

## 3. SQL Injection

**Brief:** Attacker alters database queries via input.

**Prevention:** - Use prepared statements

``` php
$stmt = $pdo->prepare('SELECT * FROM users WHERE email = ?');
$stmt->execute([$email]);
```

------------------------------------------------------------------------

## 4. Remote File Inclusion (RFI)

**Brief:** Including malicious external files in your app.

**Prevention:** - Disable `allow_url_include` - Use whitelist for
includes

------------------------------------------------------------------------

## 4. Password Hashing

**Brief:** Storing passwords securely to prevent leaks.

``` php
$hash = password_hash($password, PASSWORD_DEFAULT);
password_verify($password, $hash);
```

------------------------------------------------------------------------

## 5. Error Handling

**Brief:** Avoid exposing sensitive system info.

-   display_errors = Off
-   log_errors = On

------------------------------------------------------------------------

## 6. Directory Listing

**Brief:** Prevent users from browsing server folders.

    Options -Indexes

------------------------------------------------------------------------

## 7. File Upload Security

**Brief:** Prevent uploading malicious files.

-   Validate type & size
-   Rename files
-   Store outside public folder

------------------------------------------------------------------------

## 8. HTTPS

**Brief:** Encrypt communication between client and server.

-   Prevents data theft (MITM)

------------------------------------------------------------------------

## 9. Session Security

**Brief:** Protect user sessions from hijacking.

``` php
session_regenerate_id(true);
```

------------------------------------------------------------------------

## 10. Safe Redirect

**Brief:** Prevent accessing hidden content after redirect.

``` php
header("Location: dashboard.php");
exit();
```

------------------------------------------------------------------------

## 11. Logging

**Brief:** Track errors and suspicious activity.

-   Monitor logs regularly

------------------------------------------------------------------------


