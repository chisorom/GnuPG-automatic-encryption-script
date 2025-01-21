# GnuPG-automatic-encryption-script
This BASH script can be used to automatically encrypt all the files in a directory you want kept top secret for information security,<br />
First, ensure GnuPG is downloaded on the system and you are good to go<br />




##!/bin/bash <br />

##Directory to watch for files<br />
WATCH_DIR="/home/workstation/Downloads"<br />

##Passphrase for symmetric encryption<br />
GPG_PASSPHRASE="your_passphrase_here"<br />

##Find files in the directory (modify as needed to filter files)<br />
find "$WATCH_DIR" -type f -name "*.txt" | while read FILE; do<br />

  ##Create a new file name by replacing the .txt extension with .cis<br />
  OUTPUT_FILE="${FILE%.txt}.cis"<br />

  ##Encrypt the file with GPG using symmetric encryption<br />
  gpg --batch --yes --passphrase "$GPG_PASSPHRASE" --symmetric --cipher-algo AES256 --output "$OUTPUT_FILE" "$FILE"<br />

  ##Check if encryption was successful<br />
  if [ $? -eq 0 ]; then<br />
    echo "Encrypted $FILE to $FILE.cis"<br />
    ## Optionally, delete the original unencrypted file"<br />
    rm "$FILE""<br />

  
  else<br />
    echo "Failed to encrypt $FILE"<br />
  fi<br />
done<br />

