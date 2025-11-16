
# lambda-symfony-template

A minimal, production-ready starter template for running **Symfony 7** on **AWS Lambda** using **Bref** and the **Serverless Framework**.

This template provides:

- Symfony 7 skeleton with a `/health` endpoint  
- Fully configured Bref runtime  
- Serverless Framework configuration  
- Production-ready logging (JSON to stderr → CloudWatch Logs)  
- PHPUnit test suite  
- Local development via Symfony local server or PHP built-in server  
- Clean project structure optimized for serverless workloads  

---

## 🚀 Requirements

- PHP 8.2+
- Composer
- Serverless Framework (v3)
- AWS credentials configured locally
- Docker (optional for local Lambda layers)

---

## 📦 Installation

Clone the repository:

```
git clone https://github.com/RichardTrujilloTorres/lambda-symfony-template.git
cd lambda-symfony-template
composer install
```

---

## 🧪 Running Tests

```
composer test
```

Or manually:

```
./vendor/bin/phpunit
```

---

## 🖥️ Local Development

### Symfony CLI (preferred)

```
symfony server:start
```

### PHP built-in server

```
php -S localhost:8000 -t public
```

Then visit:

```
http://localhost:8000/health
```

---

## 📝 Logging

Production logging is configured to:

- Use JSON formatter  
- Write to `php://stderr`  
- Send logs directly to AWS CloudWatch in Lambda

Local development uses normal file logging under `var/log/`.

---

## ☁️ Deploying to AWS Lambda

1. Ensure Serverless Framework 3.x is installed:

```
npm install -g serverless
```

2. Deploy:

```
serverless deploy
```

After deployment, Serverless prints your API endpoint, e.g.:

```
https://xxxxx.execute-api.region.amazonaws.com/health
```

---

## 📁 Project Structure

```
.
├── config/              # Symfony configuration
├── public/              # Front controller for Symfony
├── src/                 # PHP source files
├── tests/               # PHPUnit tests
├── serverless.yml       # Lambda + API Gateway configuration
└── composer.json
```

---

## 🧱 Included Features

### ✓ Health Endpoint
Simple `/health` endpoint for uptime checks.

### ✓ PHPUnit Setup
Fully configured and ready to run.

### ✓ Bref Lambda Runtime
Using `bref/symfony-bridge` & `php-82` layer.

### ✓ CloudWatch Logging
Production logs use a JSON stream handler to stderr.

---

## 📄 License

This project is licensed under the **MIT License**.  
See the [`LICENSE`](./LICENSE) file for details.

---

## 🙌 Contributing

PRs welcome after initial template stabilization.
