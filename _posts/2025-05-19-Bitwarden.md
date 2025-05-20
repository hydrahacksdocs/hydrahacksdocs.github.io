---
title: Security - Bitwarden
data: 2025-05-19 17:54:00 -0600
categories: [homelab,security]
tags: [security,homelab]
description: Bitwarden - Secure your passwords and SSH Keys.
author: hydra
media_subpath: /assets/posts/
pin: false
---
# Synopsis
>You are going to be creating a few new accounts, web site logins, SSH Keys, and computer logins. Let's keep them secure!
{: .prompt-info }

Bitwarden is a free to low cost password management solution. It helps us keep all our new secrets that we are going to create private, hard to guess and best of all secure. Bitwarden uses encryption keys to protect your secrets. The key is unique to you and Bitwarden does not store it on any of their own servers, so no chance that a breach of their servers will put your secrets at risk.

While there is a free option and it will work fine for most of what we want to do, I would recommend that you buy the $10/yr personal premium license at least. It adds some great features that we just don't get with the free version. Bitwarden does not pay me to recommend it, so it really is my opinion.

## Account Creation, Extension Install, and First Login Card
1. Create a new account at [Bitwarden Personal](https://bitwarden.com/go/start-free/).
    - As suggested earlier in the [Command & Control Hack](https://hydrahacksdocs.github.io/posts/Command_Control/) I suggest using a new email account for your account.
2. Once your new account is setup and verified, I recommend installing the [Bitwarden Extension](https://chromewebstore.google.com/detail/bitwarden-password-manage/) to Chrome.

    ![Bitwarden Extension](/2025-05-17/bitwarden.png){: width="300" }
    _Bitwarden Extension_

    - Once installed, go ahead and log in so we can create some accounts. You will see the Bitwarden Extension icon if you have pinned it. If not just click on **Extensions** in the Chrome Tool Bar at the top right side.

    ![Bitwarden Login](/2025-05-17/bitwarden-login.png){: width="300" }
    _[Bitwarden Login]_

3. Open up the extension to see the main menu:

    ![Bitwarden Menu](/2025-05-17/bitwarden-menu.png){: width="300" }
    _Bitwarden Menu_

4. Let's create a new folder to hold our online accounts for our home lab user/email:
    - Click the **"+ New"** button and select **Folder** at the bottom of the list.
    - Enter a name for the new folder like **Home Lab Accounts"**.
5. There are a couple ways we can add an account. First, when we enter our user/password on a site that Bitwarden does not have in its database it will offer to save it for us. Second is to manually add the login to Bitwarden. I prefer to use the second method as I feel I have more control over the creation.
    - Navigate to a site you want to save a user/password for, like your new Gmail or Outlook account.
    - Click the Bitwarden Shield Extension Icon, and select **"+ New"** -> Login. This will open up the login creation window in Bitwarden.

    ![Bitwarden Menu](/2025-05-17/bitwarden-add.png){: width="150" }
    _Bitwarden Add_

    - Fill in the details, giving it a name, choose your account and select the folder we created earlier.

    ![Bitwarden Menu](/2025-05-17/bitwarden-details.png){: width="300" }
    _Bitwarden Menu_

    - Under login credentials, enter your account username.

    ![Bitwarden Menu](/2025-05-17/bitwarden-creds.png){: width="300" }
    _Bitwarden Credentials_

    - If you already created a password, enter it as well. If you have not created a password for the site I recommend that you use the **Generate** feature on the right of the password field to create a complex password. Adjust the number of characters and requirements for complexity. 

    ![Bitwarden Menu](/2025-05-17/bitwarden-pass.png){: width="300" }
    _Bitwarden Credentials_

    - You will also see the field for **Authenticator Key**. You can use this field to take a screenshot (Camera Icon) of any 2-factor-authentication QR codes that you may want to use with the account. It will then generate the TOTP (Text-One-Time-Password) for you and you will not need a separate Authenticator App. If you have not already enabled 2-factor-authentication for your account, I suggest you do so while you are already here.
    - Next you will see the autofill options, here you can select the **Gear Cog** to open the options for how you want Bitwarden to match your site. This becomes helpful if you have different services hosted at the same IP address but different ports. You can then use the **Host** option to better match the account.

    ![Bitwarden Menu](/2025-05-17/bitwarden-autofill.png){: width="300" }
    _Bitwarden Autofill_

    - Finally we have notes. Here you can enter any information that may be useful to the account. I will use this to save recovery keys for 2-factor-authentication keys that I have entered, or just remind me about the account usage. Now click on **Save** to save the new login card.

    ![Bitwarden Menu](/2025-05-17/bitwarden-note.png){: width="300" }
    _Bitwarden Notes_

6. Each option under the **"+ New"** button are similar, they just contain different data:
    - Card: Keep credit card data handy.
    - Identity: Create a person card that has addresses, phone numbers and other personal information. Bitwarden will try to fill in this information when you fill out web forms.
    - Note: Simple, secure notes that you may want to keep.
    - SSH Key: This is a place you can keep all your SSH Keys safe. We will be going through creation of SSH Keys in the SSH Hack.


>Disclaimer: This Hack is intended for entertainment purposes only and is not intended to be a complete guide to every situation or need.