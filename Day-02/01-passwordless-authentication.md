# How to setup Passwordless Authentication

## EC2 Instances

### Using Public Key

## Convert .pem private key to a public key
ssh-keygen -y -f ~/ayush077.pem > ~/ayush.pub

ssh-keygen -y extracts the public key from your AWS private key.
Output is saved as ayush.pub.
Keep .pem safe; share only .pub.

## Copy the public key to EC2 (authorized_keys)
ssh-copy-id -f -i ~/ayush.pub -o IdentityFile=~/ayush077.pem ubuntu@<EC2-PUBLIC-IP>

-i ~/ayush.pub → key to install.
-o IdentityFile=~/ayush077.pem → tells SSH to use the AWS PEM for login.
-f → forces installation even if no matching private key file exists locally.

## Test passwordless login
ssh ubuntu@<EC2-PUBLIC-IP>


Notes

Always chmod 400 your .pem before use:
chmod 400 ~/ayush077.pem


If your .pem is on Windows, copy it to WSL/Linux ~ before using:
cp /mnt/c/Users/<username>/Downloads/ayush077.pem ~/
chmod 400 ~/ayush077.pem

You only need the .pem once; after setup, you can log in with your new SSH key pair.

