# Laravel Secure Email

🔒 Secure email sending with ZeroBounce validation and AWS SES bounce/complaint handling for Laravel 11 & 12.

## Features

- ✅ **ZeroBounce Validation** - Pre-validate emails before sending
- ✅ **SES Bounce Handling** - Automatic blacklisting of bounced emails
- ✅ **Complaint Management** - Handle spam complaints automatically
- ✅ **Smart Caching** - Reduce API costs with intelligent caching
- ✅ **Delivery Tracking** - Monitor successful deliveries
- ✅ **Blacklist Management** - Comprehensive email blacklist system
- ✅ **Laravel 11 & 12** - Fully compatible with latest Laravel versions

## Installation
```bash
composer require fakeeh/laravel-secure-email
```

Install the package:
```bash
php artisan secure-email:install
```

## Configuration

Add to your `.env`:
```env
ZEROBOUNCE_API_KEY=your-zerobounce-key
AWS_ACCESS_KEY_ID=your-aws-key
AWS_SECRET_ACCESS_KEY=your-aws-secret
AWS_DEFAULT_REGION=us-east-1
```

## Usage

### Using Facade
```php
use Fakeeh\SecureEmail\Facades\SecureEmail;
use App\Mail\WelcomeEmail;

// Send email with validation
$result = SecureEmail::send(
    new WelcomeEmail(),
    'user@example.com',
    'John Doe'
);

if ($result['success']) {
    // Email sent successfully
}
```

### Using Service
```php
use Fakeeh\SecureEmail\Services\SecureEmailService;

$emailService = app(SecureEmailService::class);

// Check if email can be sent
$check = $emailService->canSendEmail('user@example.com');

// Get ZeroBounce credits
$credits = $emailService->getCredits();

// Get blacklist stats
$stats = $emailService->getStats();

// Manually blacklist
$emailService->blacklist('spam@example.com');

// Remove from blacklist
$emailService->whitelist('user@example.com');
```

## AWS SNS Setup

1. Create SNS topics for bounces, complaints, and deliveries
2. Subscribe your webhooks:
   - Bounce: `https://yourapp.com/webhooks/ses/bounce`
   - Complaint: `https://yourapp.com/webhooks/ses/complaint`
   - Delivery: `https://yourapp.com/webhooks/ses/delivery`
3. Configure SES to publish to your SNS topics

## License

MIT

## Credits

Created by [Fakeeh Group Development Team]
