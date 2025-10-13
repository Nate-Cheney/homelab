
## 2 Factor Authentication (2fa)

I've used [this guide](https://ubuntu.com/tutorials/configure-ssh-2fa#1-overview) to enable 2fa for ssh sessions on my homelab server.

## Steps

#### 1. Install Google Authenticator PAM module

``` bash
sudo apt install libpam-google-authenticator
```

#### 2. Configure SSH

Append the following to `/etc/pam.d/ssh`:

``` /etc/pam.d/ssh
auth required pam_google_authenticator.so
```

Restart the ssh daemon:

``` bash
sudo systemctl restart sshd.service
```

Modify `etc/ssh/sshd_config`:

``` etc/ssh/sshd_config
# Change to yes to enable challenge-response passwords 
ChallengeResponseAuthentication no # CHANGE THIS TO YES
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

