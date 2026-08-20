Logical loopholes/business loopholes
================================

Introduction
--------------------------------
Logic vulnerabilities refer to vulnerabilities caused by incorrect processing of some logical branches due to loose program logic.

In actual development, similar vulnerabilities often appear because developers have different levels of security awareness and the business develops rapidly and internal tests are not implemented in a timely manner.

Installation logic
--------------------------------
- Check if you can bypass the judgment and reinstall
- See if you can use the installation file to obtain information
- See if you can use the update function to get information

trade
--------------------------------

Buy
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Modify the price paid
- Modify payment status
- Modify the purchase quantity to a negative number
- Modify the amount to be a negative number
- Replay successful requests
- Improper handling of concurrent database locks

Business risk control
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Use coupons
- Cash out

Account
--------------------------------

register
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Override registration
- Try repeating username
- Register, traverse and guess existing accounts

password
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Passwords are not saved using a hash algorithm
- No verification of user set password strength

Email username
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- spaces before and after
- Case conversion

Cookie
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Contains sensitive information
- Can be forged without verification of legality

Mobile phone number username
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- spaces before and after
- +86

Log in
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Credential stuffing
    - Set up remote login check and other mechanisms
- Account hijacking
- Malicious attempts to account and password lock the account
    - Need to set up locking mechanism and unlocking mechanism
- Insecure transmission channels
- Login credentials stored in an insecure location

Retrieve password
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Reset any user password
- After password reset, the new password will be in the return package
-Token verification logic is on the front end
- X-Forwarded-Host is not handled correctly
- The password retrieval function leaks sensitive user information

Change password
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Changing password beyond your authority
- Change password without old password verification

Appeal
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Identity forgery
- Logic bypass

renew
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Improper ORM update operation can update any field
- Improper permission restrictions can lead to unauthorized modifications

Information inquiry
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Improper permission restrictions can lead to unauthorized inquiries
- User information ID can be guessed leading to traversal

2FA
--------------------------------
- Automatic login after password reset without 2FA
- OAuth login without 2FA enabled
- 2FA can be blasted
- 2FA conditional competition
- Modify return value to bypass
- Activation link does not have 2FA enabled
- 2FA can be disabled via CSRF

Verification code
--------------------------------
- Verification code can be reused
- Verification codes are predictable
- The verification code is not strong enough
- The verification code has no time limit or long expiration time
- No limit on the number of guesses for the verification code
- The verification code passes special parameters or does not pass parameters to bypass
- The verification code can be obtained directly from the returned package
- The verification code does not refresh or is invalid
- The number of verification codes is limited
- Verification code is returned in the data packet
- Modify cookie bypass
- Modify return package bypass
- The verification code is generated or verified on the client side
- Verification codes can be OCR or recognized using machine learning
- Verification code is used for SMS/email bombing

Session
--------------------------------
- Session mechanism
- Session guessing / blasting
- Session forgery
- Session leak
- Session Fixation

ultra vires
--------------------------------
- Unauthorized access
    - static files
    - Prevent access through specific URLs
- Horizontal override
    - The attacker can access resources of users who have the same permissions as him
    - Permission type remains unchanged, ID changes
- Vertical override
    - Low-level attackers can access resources of high-level users
    - Permission ID remains unchanged, but type changes
- Cross ultra vires
    - Permission ID changes, type changes

Random number security
--------------------------------
- Use an unsafe random number generator
- Use easy-to-guess factors such as time as random number seeds

other
--------------------------------
- User/order/coupon IDs are generated regularly and can be enumerated
- The interface has no permissions and times limit
- Misuse of encryption algorithms
- Execution order
- Leakage of sensitive information

Reference link
--------------------------------
- `Horizontal override vulnerability and its solution <http://blog.csdn.net/mylutte/article/details/50819146#10006-weixin-1-52626-6b3bffd01fdde4900130bc5a2751b6d1>`_
- `Elaborate on verification code security and review of testing ideas <https://xz.aliyun.com/t/6029>`_
