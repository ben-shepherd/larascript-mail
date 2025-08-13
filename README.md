# Larascript Mail

A flexible and extensible mail service for Larascript applications with support for multiple mail drivers.

## Features

- **Multiple Mail Drivers**: Support for Local, Nodemailer, and Resend
- **TypeScript**: Full TypeScript support with comprehensive type definitions
- **Extensible**: Easy to add custom mail adapters
- **Template Support**: Built-in support for email templates with locale data
- **Error Handling**: Robust error handling with logging integration

## Installation

```bash
npm install ben-shepherd/larascript-mail
```

## Quick Start

```typescript
import { MailService, Mail, MailConfig } from '@ben-shepherd/larascript-mail';

// Configure mail service
const mailConfig: MailConfig = {
  default: 'resend',
  drivers: [
    {
      name: 'resend',
      driver: ResendMailDriver,
      options: { apiKey: 'your-resend-api-key' }
    }
  ]
};

// Create mail service
const mailService = new MailService(mailConfig, {});

// Send an email
const mail = new Mail({
  to: 'recipient@example.com',
  from: 'sender@example.com',
  subject: 'Hello World',
  body: 'This is a test email'
});

await mailService.send(mail);
```

## Available Drivers

### Local Driver
For development and testing - logs emails to console instead of sending.

### Nodemailer Driver
Uses Nodemailer for SMTP-based email sending.

### Resend Driver
Uses Resend API for reliable email delivery.

## Extending

Need a custom mail driver? See our [extending guide](docs/extending.md) for detailed instructions on creating your own mail adapters.

## API Reference

### MailService
- `send(mail: IMail, driver?: string)`: Send an email
- `getDefaultDriver()`: Get the default mail driver
- `getDriver<T>(name: string)`: Get a specific mail driver

### Mail
- `setTo(to: string | string[])`: Set recipient(s)
- `setFrom(from: string)`: Set sender
- `setSubject(subject: string)`: Set subject
- `setBody(body: string | object)`: Set email body
- `setOptions(options: object)`: Set driver-specific options

## Development

```bash
# Install dependencies
npm install

# Run tests
npm test

# Build
npm run build

# Lint and format
npm run lint
npm run format
```

## License

ISC