# SSH (Secure Shell)

* Create SSH Key

  ```sh
  # Depends on whether the Ed25519 algorithm is supported
  # Connecting to github, email must match github email account
  # A private key and a public key will be created in the folder `~/.ssh`
  # The private key file (e.g. id_ed25519) has the words 'PRIVATE KEY' in the first line
  # Use ed25519 if supported, faster and better security
  ssh-keygen -t ed25519 -C "your_email@example.com"
  ssh-keygen -t rsa -b 4096 -C "your_email@example.com"

  # Using it ad-hoc
  eval `ssh-agent -s`
  ssh-add ~/.ssh/id_ed25519
  ```

* Configure SSH connection via `~/.ssh/config`, these are the preset keys used by the local machine or server to connect to external servers such as github

  * Note: This will replace the need to run `eval $(ssh-agent -s)` and `ssh-add ~/.ssh/...`

  ```
  Host www.example.com
    IdentityFile ~/.ssh/id_ed25519

  Host github.com
    IdentityFile ~/.ssh/id_rsa
  ```

  * If different keys are used to connect to the same server, set up aliases (e.g. me.github.com) in hosts file and change the remote path

    ```sh
    git remote -v
    git remote set-url origin git@me.github.com:ijklim/repo-name.git
    ```

* Establishing SSH connection

  ```sh
  # Note: Must specify user name (e.g. ubuntu)
  ssh ubuntu@www.example.com
  ```

* Copying a file from remote server

  ```sh
  scp ubuntu@www.example.com:/path/file .
  ```

* SSH keys allowed to connect to the server must be specified in `~/.ssh/authorized_keys`

  * Information in this file comes from the public key (e.g. id_rsa.pub)

  ```sh
  # Add key to authorized_keys
  echo -e 'ssh-rsa AAAAB3NzaC1yc2EAAAA...WMrChIPrkGL id_rsa\n' >> ~/.ssh/authorized_keys

  chmod 0600 ~/.ssh/authorized_keys
  ```