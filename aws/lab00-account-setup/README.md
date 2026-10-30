# Lab 0: Secure AWS account setup

> My DevOps arc starts here. Curiosity got me this far.

## What I built
- New AWS account on the Free plan
- MFA on the root user, then a separate `wolfshade-admin` IAM user (also with MFA) for daily work. Root stays locked 
in the drawer.
- Two budgets: a zero-spend alert and a $10 monthly cap
- AWS CLI v2 on my home server (berserkernode), region eu-west-1

## Commands I used
    aws --version
    aws configure
    aws sts get-caller-identity   # the "whoami" of AWS

## What broke and how I fixed it
After scanning the QR code and entering the codes, MFA setup hung. I refreshed, tried again, and got 
"You need permissions... authenticate with an MFA device."

**Root cause:** the first attempt had actually succeeded. MFA was active, but my session started before MFA existed, 
so AWS blocked MFA changes from it.

**Fix:** signed out and back in with an MFA code. Confirmed one device under Security credentials and removed the 
duplicate from my authenticator app.

**Lesson:** when a change looks like it failed, check whether it went through before retrying.

## Screenshots
<img width="1622" height="262" alt="image" src="https://github.com/user-attachments/assets/d97774ed-cef3-4785-8e79-41c7fee93033" />
<img width="713" height="137" alt="AwsGetCallerId" src="https://github.com/user-attachments/assets/8d643084-b5c1-47c1-b7f0-31c2984327dd" />
