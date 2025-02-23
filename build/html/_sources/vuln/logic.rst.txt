Logical vulnerabilities / Business vulnerabilities
================================

Introduction
--------------------------------
Logical vulnerabilities refer to vulnerabilities caused by some logical branches processing errors due to poor program logic.

In actual development, similar vulnerabilities often occur because the developers have different levels of security awareness and the business is developing rapidly.

Installation logic
--------------------------------
- Check whether you can bypass the judgment and reinstall it
- Check whether you can use the installation file to obtain information
- See if you can use the update function to obtain information

trade
--------------------------------

Buy
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Modify the price paid
- Modify payment status
- Modify the purchase quantity to negative
- Modify the amount to negative
- Replay successful request
- Improper handling of concurrent database locks

Business risk control
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Scan the coupon
- Cash out

Account
--------------------------------

register
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Overwrite registration
- Try to repeat username
- Register and traverse guess the existing account

password
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Password not saved using hashing algorithm
- No verification of the user's password set strength

Email username
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Front and back spaces
-Case transformation

Cookie
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Contains sensitive information
- Unverified legality can be forged

Mobile phone number username
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Front and back spaces
- +86

Log in
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Crazy library
- Set up mechanisms such as remote login checking
- Account Hijacking
- Maliciously try to lock the account
- Locking mechanism and unlocking mechanism need to be set
- Insecure transmission channels
- Login credentials are stored in an unsafe location

Retrieve password
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Reset any user password
- After password reset, the new password is in the return package
- Token verification logic is on the front end
- X-Forwarded-Host is incorrectly handled
- Password recovery function leaks user sensitive information

Modify password
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Unauthorized password modification
- Change password without old password verification

Complaint
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Identity forgery
- Logical Bypass

renew
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Any field can be updated if the ORM update operation is incorrect
- Improper permission restrictions can be modified beyond the authority

Information query
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Inappropriate permission restrictions can be exceeded
- User information ID can guess the traversal results

2FA
--------------------------------
- Automatic login after resetting password without 2FA
- OAuth login does not enable 2FA
- 2FA can be blasted
- 2FA conditional competition
- Modify the return value bypass
- Activate link does not enable 2FA
- 2FA can be disabled via CSRF

Verification code
--------------------------------
- Verification code can be reused
- Verification code is predictable
- The verification code is not strong enough
- There is no time limit for verification code or long expiration time
- No limit on the number of guesses for verification code
- Verification code passes special parameters or does not pass parameters by bypass
- Verification code can be obtained directly from the return package
- Verification code is not refreshed or invalid
- Limited number of verification codes
- Verification code is returned in the data packet
- Modify cookie bypass
- Modify return package bypass
- Verification code is generated or verified on the client side
- Verification code can be recognized using OCR or using machine learning
- Verification code is used for mobile phone text messages/email bombing

Session
--------------------------------
- Session mechanism
- Session guess / Blast
- Session forgery
- Session Leak
- Session Fixation

Overreach of authority
--------------------------------
- Unauthorized access
- Static files
- Prevent access by specific url
- Level overreach
- The attacker can access the resources of a user with the same permissions as him
- Permission type remains unchanged, ID changes
- Vertical overreach
- Low-level attackers can access resources of high-level users
- Permission ID remains unchanged, type changes
- Cross-over
- Permission ID changes, type changes

Random number safety
--------------------------------
- Use unsafe random number generator
- Use time and other easy-to-guess factors as random number seeds

other
--------------------------------
- User/order/coupon and other ID generation is regular and can be enumerated
- No permissions on the interface, limited number of times
- Misuse of encryption algorithm
- Execution order
- Sensitive information leakage

Reference link
--------------------------------
- `Horily overprivileges vulnerability and its solutions <http://blog.csdn.net/mylutte/article/details/50819146#10006-weixin-1-52626-6b3bffd01fdde4900130bc5a2751b6d1>`_
- `Detailed explanation of verification code security, comprehensive review of testing ideas <https://xz.aliyun.com/t/6029>`_
