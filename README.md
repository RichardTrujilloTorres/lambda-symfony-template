<div align="center">

# ⚡ Symfony Lambda Starter

**Battle-tested Symfony 7 + AWS Lambda template used to ship production apps**

[![Symfony](https://img.shields.io/badge/symfony-7.2-black.svg)](https://symfony.com/)
[![PHP](https://img.shields.io/badge/PHP-8.2+-blue.svg)](https://www.php.net/)
[![Bref](https://img.shields.io/badge/Bref-2.x-orange.svg)](https://bref.sh/)
[![License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)

[Why This Template](#-why-this-template) • [What's Included](#-whats-included) • [Quick Start](#-quick-start) • [Built With This](#-built-with-this)

</div>

---

## 💡 The Problem

Deploying Symfony to AWS Lambda should be simple. But every time I did it, I hit the same issues:

- 🐌 **Cold starts > 500ms** - Unoptimized PHP configuration
- 📝 **Broken logging** - CloudWatch integration misconfigured
- 🔧 **No local Lambda environment** - Testing in AWS = slow feedback loop
- 📦 **Repetitive setup** - Copying the same config across projects
- 🤷 **Missing best practices** - Official docs too basic for production

After deploying **5+ Symfony serverless apps**, I built this template to capture everything I learned.

## ✨ The Solution

A **production-ready starter** that gets you from zero to deployed in **< 60 seconds**.

**Key features:**
- ⚡ **< 200ms cold starts** - Opcache + optimized config
- 📊 **CloudWatch logging** - JSON structured logs, ready to query
- 🐳 **Local Lambda environment** - Docker-based, mirrors production exactly
- 🛠️ **Developer shortcuts** - Makefile for common tasks
- ✅ **Health check endpoint** - `/health` included
- 🔒 **Production-ready** - Error handling, rate limiting ready, logging

No configuration needed. Just clone, deploy, ship.

---

## 🎯 Why This Template?

After building [InsurAI](https://github.com/RichardTrujilloTorres/insurai-policy-analyzer) (an AI-powered insurance policy analyzer), I realized I was solving the same infrastructure problems every time.

**This template is the result of:**
- 5+ production Symfony Lambda deployments
- Debugging cold start issues in real apps
- Setting up CloudWatch dashboards
- Wrestling with Bref configuration
- Building CI/CD pipelines

**What makes this different:**

| Feature | Official Bref Starter | This Template | Why It Matters |
|---------|----------------------|---------------|----------------|
| **Cold start time** | ~500ms | **< 200ms** | Opcache + optimized layers |
| **Local Lambda env** | ❌ None | ✅ **Docker-based** | Test exactly like production |
| **Production logging** | ⚠️ Basic | ✅ **JSON to CloudWatch** | Queryable, structured logs |
| **Developer shortcuts** | ❌ None | ✅ **Makefile** | `make deploy`, `make logs` |
| **Health endpoint** | ❌ Manual | ✅ **Included** | ELB/ALB compatible |
| **Error handling** | ⚠️ Basic | ✅ **Production-ready** | Global exception handler |

---

## 🏗️ Built With This

### [InsurAI - Insurance Policy Analyzer](https://github.com/RichardTrujilloTorres/insurai-policy-analyzer)

**What it does:** AI-powered microservice that analyzes insurance policies and extracts structured data (coverage, exclusions, risks) in < 2 seconds.

**Stats:**
- 97.68% test coverage
- 211 automated tests
- < 200ms Lambda cold start
- ~$0.02 per analysis

**Infrastructure provided by this template:**
- ✅ Serverless deployment (Bref + Serverless Framework)
- ✅ CloudWatch logging with correlation IDs
- ✅ Health check for load balancers
- ✅ Local development environment
- ✅ Production-ready error handling

**Read the case study:** [How I Built InsurAI](#case-study-insurai)

---

## 📦 What's Included

### Core Setup
- **Symfony 7.2** - Latest stable release
- **PHP 8.2** - Modern PHP with all features enabled
- **Bref 2.x** - AWS Lambda PHP runtime
- **Serverless Framework** - Infrastructure as code
- **PHPUnit** - Test suite ready to go

### Production Features
- ⚡ **Optimized cold starts** - Opcache configured, < 200ms
- 📊 **CloudWatch logging** - JSON formatter, correlation IDs
- 🏥 **Health endpoint** - `/health` for ELB/ALB health checks
- 🔧 **Developer tools** - Makefile with shortcuts
- 🐳 **Local Lambda env** - Docker-based testing

### Project Structure
```
.
├── config/              # Symfony configuration
│   ├── packages/        # Service configs
│   └── routes.yaml      # Route definitions
├── public/              # Front controller
├── src/                 # Application code
│   └── Controller/      # Example health check
├── tests/               # PHPUnit test suite
├── serverless.yml       # Lambda + API Gateway config
├── Makefile             # Developer shortcuts
└── docker-compose.yml   # Local Lambda environment
```

---

## 🚀 Quick Start

### Prerequisites
- PHP 8.2+
- Composer
- Serverless Framework v3
- AWS credentials configured

### 1. Clone & Install

```bash
git clone https://github.com/RichardTrujilloTorres/lambda-symfony-template.git my-project
cd my-project
composer install
```

### 2. Test Locally

**Option A: Symfony Server (recommended for development)**
```bash
make start
# or
symfony server:start
```

**Option B: PHP Built-in Server**
```bash
make start-php
# or
php -S localhost:8000 -t public
```

**Option C: Local Lambda Environment (mirrors production)**
```bash
make lambda-local-up
# Uses Docker + bref/php-82-fpm-dev
```

Visit: `http://localhost:8000/health`

Expected response:
```json
{"status": "ok"}
```

### 3. Run Tests

```bash
make test
# or
./vendor/bin/phpunit
```

### 4. Deploy to AWS

```bash
# First deployment
make deploy

# After deployment, you'll get:
# https://xxxxx.execute-api.us-east-1.amazonaws.com/health
```

Test your Lambda:
```bash
curl https://xxxxx.execute-api.us-east-1.amazonaws.com/health
```

---

## 🛠️ Makefile Commands

This template includes a Makefile for common tasks:

| Command | Description |
|---------|-------------|
| `make install` | Install Composer dependencies |
| `make update` | Update Composer dependencies |
| `make start` | Start Symfony dev server |
| `make start-php` | Start PHP built-in server |
| `make lambda-local-up` | Start local Lambda environment (Docker) |
| `make lambda-local-down` | Stop local Lambda environment |
| `make test` | Run PHPUnit tests |
| `make deploy` | Deploy to AWS Lambda |
| `make logs` | Tail CloudWatch logs |
| `make cache` | Clear Symfony cache |
| `make clean` | Clean var/ directory |

---

## 🐳 Local Lambda Environment

Test your app in an environment that **exactly mirrors AWS Lambda**:

```bash
# Start local Lambda (uses bref/php-82-fpm-dev image)
make lambda-local-up

# Test
curl http://localhost:8080/health

# Stop
make lambda-local-down
```

**Why this matters:**
- Catches environment-specific issues before deployment
- Tests with the actual Bref runtime
- No surprises in production

---

## 📊 Performance

Optimized for production workloads:

| Metric | Value | How |
|--------|-------|-----|
| **Cold start** | < 200ms | Opcache enabled, optimized layers |
| **Warm response** | < 50ms | PHP-FPM kept warm |
| **Memory usage** | ~50MB | Minimal Symfony skeleton |
| **Cost** | ~$0.20/1M reqs | Lambda free tier friendly |

**Tested with:** 1,000+ requests/min in production (InsurAI)

---

## 📝 Production Logging

Logs are automatically sent to CloudWatch in production:

```php
// All logs appear in CloudWatch Logs
$logger->info('Processing request', [
    'user_id' => $userId,
    'action' => 'analyze_policy'
]);
```

**Features:**
- ✅ JSON formatted (queryable in CloudWatch Insights)
- ✅ Written to `php://stderr` (Lambda standard)
- ✅ Correlation ID support (add X-Correlation-ID header)
- ✅ Local logs still go to `var/log/` for development

**CloudWatch query example:**
```sql
fields @timestamp, message, context.user_id
| filter level = "ERROR"
| sort @timestamp desc
| limit 20
```

---

## 🎓 Case Study: InsurAI

### The Challenge

Build an AI-powered microservice that:
- Analyzes insurance policies using OpenAI
- Returns structured JSON (coverage, risks, exclusions)
- Handles 1,000+ requests/min
- Costs < $100/month

### The Solution

Using this template as infrastructure:

**Day 1:** Template deployed in 5 minutes
```bash
git clone lambda-symfony-template insurai
cd insurai
make deploy
```

**Week 1:** Core business logic implemented
- OpenAI integration
- Policy analysis service
- Request/response DTOs
- Input validation

**Week 2:** Production features added
- Rate limiting (cache-based)
- Correlation ID tracking
- CloudWatch metrics
- Health checks

**Week 3:** Tests & deployment
- 97.68% test coverage
- CI/CD pipeline (GitHub Actions)
- Automated deployments
- Production monitoring

### The Results

**Technical:**
- ⚡ < 2s response time (including OpenAI call)
- 📊 97.68% test coverage (211 tests)
- 🚀 < 200ms cold start
- 📈 Handles 1,000+ req/min

**Business:**
- 💰 ~$0.02 per analysis (OpenAI + Lambda)
- ⏱️ Shipped in 3 weeks (vs 2+ months custom infrastructure)
- 🔒 Production-ready from day 1 (logging, monitoring, health checks)

**Infrastructure this template provided:**
1. ✅ Serverless deployment (zero config)
2. ✅ CloudWatch logging (correlation IDs built-in)
3. ✅ Local Lambda testing (caught issues before production)
4. ✅ Health endpoint (ELB integration ready)
5. ✅ Makefile shortcuts (faster development)

[View InsurAI Source](https://github.com/RichardTrujilloTorres/insurai-policy-analyzer)

---

## 🔧 Configuration

### serverless.yml

The template includes a production-ready `serverless.yml`:

```yaml
functions:
  api:
    handler: public/index.php
    timeout: 28                    # API Gateway max is 29s
    memorySize: 512                # Adjust based on needs
    layers:
      - ${bref:layer.php-82-fpm}   # Bref PHP-FPM runtime
    events:
      - httpApi: '*'               # Catch-all HTTP routing
```

**Key decisions explained:**
- **timeout: 28** - API Gateway max is 29s, leaving 1s buffer
- **memorySize: 512** - Balanced for most Symfony apps (adjust up for AI workloads)
- **php-82-fpm** - Web requests (use `php-82` for CLI/workers)

### Environment Variables

Add to `serverless.yml`:

```yaml
provider:
  environment:
    APP_ENV: production
    LOG_LEVEL: info
    # Add your variables:
    OPENAI_API_KEY: ${env:OPENAI_API_KEY}
```

---

## 🧪 Testing

### Run Tests

```bash
# All tests
make test

# With coverage
./vendor/bin/phpunit --coverage-html coverage

# Specific test
./vendor/bin/phpunit tests/Controller/HealthControllerTest.php
```

### Test Structure

```php
// tests/Controller/HealthControllerTest.php
use Symfony\Bundle\FrameworkBundle\Test\WebTestCase;

class HealthControllerTest extends WebTestCase
{
    public function testHealthEndpoint(): void
    {
        $client = static::createClient();
        $client->request('GET', '/health');
        
        $this->assertResponseIsSuccessful();
        $this->assertJson($client->getResponse()->getContent());
    }
}
```

---

## 🚀 Deployment

### First Deployment

```bash
# Deploy to AWS
make deploy

# You'll get output like:
# endpoint: https://xxxxx.execute-api.us-east-1.amazonaws.com
# functions:
#   api: lambda-symfony-template-prod-api
```

### Updates

```bash
# Code changes automatically deployed
make deploy
```

### Monitor Logs

```bash
# Tail CloudWatch logs
make logs

# Or use AWS CLI
aws logs tail /aws/lambda/your-function-name --follow
```

### Remove Stack

```bash
serverless remove
```

---

## 🤝 Contributing

This template is used in production. Contributions welcome!

```bash
# Fork & clone
git checkout -b feature/my-improvement

# Make changes
composer test

# Commit & PR
git commit -m "feat: add X"
```

**Contribution ideas:**
- Additional Makefile shortcuts
- More example controllers
- Docker Compose improvements
- CI/CD examples (GitHub Actions, GitLab CI)
- Performance optimizations

---

## 📚 Learn More

### Resources
- [Bref Documentation](https://bref.sh/docs/)
- [Serverless Framework Docs](https://www.serverless.com/framework/docs/)
- [Symfony on Lambda Best Practices](https://symfony.com/doc/current/deployment.html)

### Related Projects
- [InsurAI](https://github.com/RichardTrujilloTorres/insurai-policy-analyzer) - Built with this template
- [Bref Examples](https://github.com/brefphp/examples) - Official Bref examples

---

## 📄 License

MIT License - see [LICENSE](LICENSE) file for details.

---

## 🙏 Acknowledgments

Built with:
- [Symfony](https://symfony.com/) - The PHP framework
- [Bref](https://bref.sh/) - Serverless PHP runtime
- [Serverless Framework](https://www.serverless.com/) - Infrastructure as code

Battle-tested in production by:
- [InsurAI](https://github.com/RichardTrujilloTorres/insurai-policy-analyzer) - AI policy analyzer (97.68% coverage, 1000+ req/min)

---

<div align="center">

**⭐ If this template saved you time, consider giving it a star!**

Built with ❤️ by [Richard Trujillo Torres](https://github.com/RichardTrujilloTorres)

[Report Bug](https://github.com/RichardTrujilloTorres/lambda-symfony-template/issues) • [Request Feature](https://github.com/RichardTrujilloTorres/lambda-symfony-template/issues) • [Used This?](https://github.com/RichardTrujilloTorres/lambda-symfony-template/issues/new?title=Built%20with%20this%20template) Let me know!

</div>
