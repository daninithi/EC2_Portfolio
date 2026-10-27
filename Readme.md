# Portfolio

A React + Vite site, deployed to an AWS EC2 server that runs Apache.

## How deploy works

1. Push to `main`.
2. GitHub Actions runs `npm ci` and `npm run build`, using `VITE_*` values from GitHub Secrets.
3. It signs in to EC2 with an SSH key and copies `dist/` into `/var/www/html` with `rsync`.
4. Visitors open `http://<EC2-IP>` and Apache serves the files on port 80.

The server only runs Apache. No Node, no Docker, no build tools.

## One-time EC2 setup (Ubuntu)

Security group: allow inbound ports **22** (SSH) and **80** (HTTP).

```bash
sudo apt update
sudo apt install -y apache2 rsync
sudo systemctl enable --now apache2
```

The SSH user (e.g. `ubuntu`) needs passwordless `sudo`, which is the default on Ubuntu EC2 images.

## GitHub Secrets

| Secret | What it is |
| --- | --- |
| `EC2_HOST` | EC2 public IP or DNS name |
| `EC2_USER` | SSH user, e.g. `ubuntu` |
| `EC2_KEY` | Full private key (`.pem` contents) |
| `VITE_EMAIL` | Contact email |
| `VITE_LINKEDIN_URL` | LinkedIn URL |
| `VITE_GITHUB_URL` | GitHub URL |
| `VITE_EMAILJS_PUBLIC_KEY` | EmailJS public key |
| `VITE_EMAILJS_SERVICE_ID` | EmailJS service ID |
| `VITE_EMAILJS_TEMPLATE_ID` | EmailJS template ID |
| `VITE_EMAILJS_RECEIVE_EMAIL` | Email that receives contact form messages |

## Local development

```bash
npm install
npm run dev
```
