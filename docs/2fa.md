
## 2 Factor Authentication (2fa)

#### 1. Install Google Authenticator PAM module

``` bash
sudo apt install libpam-google-authenticator
```

#### 2. Configure SSH

Modify `/etc/pam.d/ssh`:

``` /etc/pam.d/ssh
# @include common-auth # COMMENT THIS LINE OUT
auth required pam_google_authenticator.so # ADD THIS LINE UNDERNEATH
```

Modify / add the following lines in `etc/ssh/sshd_config`:

``` etc/ssh/sshd_config
ChallengeResponseAuthentication yes # CHANGE TO YES

# ADD THE FOLLOWING
KbdInteractiveAuthentication yes
AuthenticationMethods publickey,keyboard-interactive
```

Restart the ssh daemon:

``` bash
sudo systemctl restart sshd.service
```

#### 3. Configure Authentication

Run the following command:

``` bash
google-authenticator
```

Scan the QR code using the authenticator app of choice.

Enter the code displayed in your app. 

Save the emergency scratch codes in a safe place.

Answer the questions using the recommended configuration:

| Setting                                     | Flag | Reason                                   |
| ------------------------------------------- | ---- | ---------------------------------------- |
| Make tokens "time-base"                     | yes  | Standard **TOTP** method                 |
| Update the `.google_authenticator` file     | yes  | Allows setup to overwrite default config |
| Disallow multiple uses                      | yes  | Prevents 2FA codes from being reused     |
| Increase the original generation time limit | no   | Handles clock skew                       |
| Enable rate-limiting                        | yes  | Aids in brute-force attack prevention    |

#### 4. Test

**Before closing the current ssh session**, open a new terminal and attempt to connect. If you're prompted for a verification code and are able to connect, everything is correct.

