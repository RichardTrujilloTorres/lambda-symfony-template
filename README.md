# lambda-symfony-template

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
