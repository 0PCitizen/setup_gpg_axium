#!/bin/bash
# Check for GPG installation
if ! command -v gpg &> /dev/null; then
echo "GPG is not installed. Install it first (e.g.,
exit 1
'sudo apt install gnupg').
"
fi
# Prompt for user input
echo "Setting up GPG for the Axium project...
"
read -p "Enter your name (e.g., Axium Project): " NAME
read -p "Enter your email (e.g., your-email@example.com): " EMAIL
# Generate GPG key
echo "Generating GPG key...
"
gpg --batch --gen-key <<EOF
%no-protection
Key-Type: RSA
Key-Length: 4096
Subkey-Type: RSA
Subkey-Length: 4096
Name-Real: $NAME
Name-Email: $EMAIL
Expire-Date: 1y
EOF
# Fetch the key ID
KEY
_
ID=$(gpg --list-keys --with-colons | grep -m 1 pub | cut -d: -f5)
# Export public key
PUBLIC
KEY
FILE="axium
_
_
_public
_
key.asc"
gpg --export --armor $KEY
ID > $PUBLIC
_
_
echo "Public key exported to $PUBLIC
KEY
_
_
KEY
FILE
_
FILE.
"
# Sign a sample JavaScript file
SAMPLE
_
FILE="axium.js"
echo "// Axium project JavaScript file" > $SAMPLE
FILE
_
gpg --detach-sign --armor $SAMPLE
FILE
_
echo "Signed $SAMPLE
_
FILE. Signature file: $SAMPLE
_
FILE.asc"
# Optional: Configure Git to use this GPG key for signing
read -p "Would you like to configure Git to sign commits with this GPG key? (y/n): "
CONFIGURE
GIT
_
if [[ $CONFIGURE
_
GIT =~ ^[Yy]$ ]]; then
git config --global user.signingkey $KEY
ID
_
git config --global commit.gpgsign true
echo "Git is now configured to sign commits with your GPG key.
"
fi
echo "GPG setup for the Axium project is complete!"
chmod +x setup_gpg_
axium.sh
./setup_gpg_
axium.sh
