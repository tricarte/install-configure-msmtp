#!/usr/bin/env bash

sudo apt install msmtp msmtp-mta -y

GPGKEY_REALNAME=""
GPGKEY_EMAIL=""

ACCOUNTNAME="" # Enter whatever you want as a config name
SMTPHOST=""
FROM=""

ENCRYPTED_PASS_FILE="$HOME/.msmtp.gpg"

gpg --batch --gen-key <<EOF
%no-protection
Key-Type:1
Key-Length:2048
Subkey-Type:1
Subkey-Length:2048
Name-Real: $GPGKEY_REALNAME
Name-Email: $GPGKEY_EMAIL
Expire-Date:0
EOF

echo "
# Set default values for all following \"account\" sections
defaults
port 587
tls on
tls_trust_file /etc/ssl/certs/ca-certificates.crt
# logfile		/var/log/msmtp.log

account $ACCOUNTNAME
host $SMTPHOST
from $FROM
auth on
user $USERNAME
passwordeval gpg --no-tty -q -d $ENCRYPTED_PASS_FILE
# If you are using pass password manager
# passwordeval \"pass email/user1\"

# Set a default account
account default : $ACCOUNTNAME
" | tee "$HOME/.msmtprc"

echo "Enter your password for your SMTP host:"
echo "Then press Enter again to go to a new line and and CTRL+D to exit."
gpg --encrypt -o "$ENCRYPTED_PASS_FILE" -r $GPGKEY_EMAIL -
