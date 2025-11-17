# lambda-symfony-template

[![CI](https://github.com/RichardTrujilloTorres/lambda-symfony-template/actions/workflows/ci.yml/badge.svg)](https://github.com/RichardTrujilloTorres/lambda-symfony-template/actions/workflows/ci.yml)
[![Coverage](https://codecov.io/gh/RichardTrujilloTorres/lambda-symfony-template/branch/main/graph/badge.svg)](https://codecov.io/gh/RichardTrujilloTorres/lambda-symfony-template)
[![PHPStan](https://img.shields.io/badge/PHPStan-level%206-blue)](https://github.com/RichardTrujilloTorres/lambda-symfony-template)

A minimal, production-ready starter template for running **Symfony 7** on **AWS Lambda** using **Bref** and the **Serverless Framework**.

This template provides:

- Symfony 7 skeleton with a `/health` endpoint  
- Fully configured Bref runtime  
- Serverless Framework configuration  
- Production-ready logging (JSON to stderr → CloudWatch Logs)  
- PHPUnit test suite  
- Local development via Symfony server or PHP built-in server  
- Clean project structure optimized for serverless workloads  

---

## 🚀 Requirements

- PHP 8.2+
- Composer
- Serverless Framework (v3)
- AWS credentials configured locally
- Docker (optional, for Lambda layers)

---

## 📦 Installation

Clone the repository:

```bash
git clone https://github.com/RichardTrujilloTorres/lambda-symfony-template.git
cd lambda-symfony-template
composer install
```

---

## 🧪 Running Tests

Run the test suite with:

```bash
./vendor/bin/phpunit
```

---

## 🖥️ Local Development

### Symfony CLI (preferred):

```bash
symfony server:start
```

### PHP built-in server:

```bash
php -S localhost:8000 -t public
```

Then visit:

```
http://localhost:8000/health
```

---

## 🧰 Developer Commands (Makefile)

This template includes a **Makefile** to provide a clean developer experience.

### Start local server

```bash
make start
```

Or use PHP built-in:

```bash
make start-php
```

### Run tests

```bash
make test
```

### Deploy to AWS Lambda

```bash
make deploy
```

### Tail CloudWatch logs

```bash
make logs
```

### Clear caches

```bash
make clean
```

### Rebuild production cache

```bash
make cache
```

### Install/update dependencies

```bash
make install
make update
```

---

## 📝 Logging

Production logging is configured to:

- Use JSON formatter  
- Write to `php://stderr`  
- Appear automatically in CloudWatch Logs  

Local development logs remain in `var/log/`.

---

## ☁️ Deploying to AWS Lambda

Ensure Serverless Framework v3 is installed:

```bash
npm install -g serverless
```

Deploy:

```bash
make deploy
```

After deployment, Serverless prints your API endpoint, for example:

```
https://xxxxx.execute-api.region.amazonaws.com/health
```

---

## 📁 Project Structure

```
.
├── config/              # Symfony configuration
├── public/              # Front controller
├── src/                 # Application source code
├── tests/               # PHPUnit test suite
├── serverless.yml       # Lambda + API Gateway config
├── Makefile             # Developer shortcuts
└── composer.json
```

---

## 📄 License

This project is licensed under the **MIT License**.  
See the [`LICENSE`](./LICENSE) file for details.

---

## 🙌 Contributing

PRs welcome after initial template stabilization.

---

## 🧩 Development Notes (Hooks, Commit Format, DX)

This template includes optional but helpful development tooling.

### **Pre-commit hooks (automated checks)**

These run **automatically before each commit**:

- `composer cs:fix` — auto-fixes code style  
- `composer stan` — prevents committing code with PHPStan errors  

To bypass them temporarily:

```bash
git commit --no-verify
```

---

### **Conventional Commit Messages**

Commit messages must follow:

```
<type>(optional-scope): message
```

Allowed types:

`feat`, `fix`, `docs`, `chore`, `ci`, `test`, `refactor`, `perf`, `style`, `build`, `revert`

Example:

```
feat(api): add health check
```

---

## 🔒 Environment Files & Secrets

This repo includes `.env`, `.env.dev`, `.env.test` — **only with non-secret defaults**.

**Never commit real credentials.**

Use:

- `.env.local` (gitignored) for local secrets  
- environment variables in production (Lambda / Serverless)

---

## 🗺️ Project Status

This project is still **stabilizing**.  
You may open issues freely.  
PRs are welcome but may be reviewed after the first milestone release (`v0.1.0`).
