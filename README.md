# Chomusuke APT Repository

[![Deploy APT Repository](https://github.com/chomusuke-mk/apt-repository/actions/workflows/deploy-apt.yml/badge.svg)](https://github.com/chomusuke-mk/apt-repository/actions/workflows/deploy-apt.yml)

Official Debian/Ubuntu APT repository for Chomusuke software, currently hosting **Vidra** for Linux.
The repository is automatically generated and hosted on GitHub Pages at [apt.chomusuke.dev](https://apt.chomusuke.dev).

## 🚀 How to Add the Repository

Run the following commands in your terminal to securely add this repository and its GPG key to your system:

```bash
# 1. Download the public security key
wget -qO- https://apt.chomusuke.dev/public.key | sudo tee /etc/apt/keyrings/chomusuke.asc > /dev/null

# 2. Add the repository to your sources list
echo "deb [signed-by=/etc/apt/keyrings/chomusuke.asc] https://apt.chomusuke.dev/ stable main" | sudo tee /etc/apt/sources.list.d/chomusuke.list

# 3. Update package lists
sudo apt update
```

After adding the repository, you can install available packages normally:

```bash
sudo apt install vidra
```

You will receive automatic updates via `sudo apt upgrade`.

## ⚙️ How it Works

This repository is 100% serverless and automated using GitHub Actions and GitHub Pages:

1. When a new release is published in the main application repository (e.g., [Vidra](https://github.com/chomusuke-mk/vidra)), it sends a `repository_dispatch` event (`update-apt`).
2. The GitHub Action in this repository wakes up, downloads the latest `.deb` artifacts from the release.
3. It uses `reprepro` to build the APT index structure.
4. The Release files are securely signed using a GPG Private Key stored in GitHub Secrets.
5. The generated static files are deployed to GitHub Pages.
