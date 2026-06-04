# **AES Git Workshop**
***Created by Nathan Whittenburg, June 4, 2026***

## **Table of Contents**
- [Cloning with HTTPS](#cloning-with-https)
- [Cloning with SSH](#cloning-with-ssh)

## **Cloning with HTTPS** 
>***Recommended for first-time git users***

```bash
git clone https://github.com/UCBoulder/AES-GitWorkshop.git
```

When prompted, use your GitHub username and a **Personal Access Token (PAT)** as the password.

### Creating a PAT
1. Go to **GitHub → Settings → Developer settings → Personal access tokens → Fine-grained tokens**
2. Click **Generate new token**
3. Under **Resource owner**, select the **organization**
4. Set an expiration
5. Under **Repository access**, select **Only select repositories** and choose `AES-GitWorkshop`
6. Under **Permissions**, set **Contents** to `Read and Write` (or `Read-only` if you only need to clone)
7. Click **Generate token** and copy it; you won't see it again

Store it somewhere safe (e.g. a password manager). To avoid re-entering it, cache it with:

```bash
git config --global credential.helper store
```

The next time you clone or push, Git will save the token to `~/.git-credentials`.

<br>

## **Cloning with SSH**
>***Recommended for regular git users***

SSH lets you authenticate with GitHub without entering a password every time. You'll set it up once and it just works after that.

### ***It is highly recommended to read [GitHub's SSH tutorial](https://docs.github.com/en/authentication/connecting-to-github-with-ssh) for an in depth guide on connecting to GitHub with SSH.***


### 1. Check for an existing SSH key

**Mac/Linux:**
```bash
ls ~/.ssh
```

**Windows (PowerShell):**
```powershell
ls $env:USERPROFILE\.ssh
```

If you see `id_ed25519.pub` or `id_rsa.pub`, you already have a key — skip to step 3.

---

### 2. Generate a new SSH key

*Windows (PowerShell)/Mac/Linux:*
```bash
ssh-keygen -t ed25519 -C "your@email.com"
```

Press enter through the prompts to accept the defaults. This creates two files in your `.ssh` folder (location varies on Windows vs Mac/Linux):
- `id_ed25519` — your **private key**, never share this
- `id_ed25519.pub` — your **public key**, this is what you give to GitHub

---

### 3. Add the public key to GitHub

Copy your public key:

**Mac/Linux:**
```bash
cat ~/.ssh/id_ed25519.pub
```

**Windows (PowerShell):**
```powershell
type $env:USERPROFILE\.ssh\id_ed25519.pub
```

Then in GitHub: **Settings → SSH and GPG keys → New SSH key**, paste it in and save.

---

### 4. Test the connection

```bash
ssh -T git@github.com
```

You should see: `Hi <username>! You've successfully authenticated.`

---

### 5. Clone the repo

```bash
git clone git@github.com:UCBoulder/AES-GitWorkshop.git
```

---

> SSH keys are per machine. If you're working on a new computer, repeat this process and add that machine's public key to GitHub.