# Setup Sendmail with Sendgrid

How to setup Sendmail MTA (Mail Transport Agent) on server to use Sendgrid SMTP.

## Prerequisites

Install required packages.

```bash
wo stack install --sendmail
apt install libsasl2-modules
```

## 1. Sendgrid API key

[Create a new Sendgrid API key](https://app.sendgrid.com/settings/api_keys) (if not already created).

## 2. Create Auth File

```bash
mkdir /etc/mail/authinfo
chmod 700 /etc/mail/authinfo
```

Create `/etc/mail/authinfo/smtp-auth` and add the following content:

```ini
AuthInfo: "U:root" "I:apikey" "P:API_KEY"
```

Create a hash map file of above created auth file.

```bash
makemap hash /etc/mail/authinfo/smtp-auth < /etc/mail/authinfo/smtp-auth
```

## 3. Configure Sendmail with SMART_HOST

Add the following configuration lines into `/etc/mail/sendmail.mc` after `MAILER_DEFINITIONS` and before ``MAILER(`local')dnl`` at the bottom.

```ini
define(`SMART_HOST',`[smtp.sendgrid.com]')dnl
define(`RELAY_MAILER_ARGS', `TCP $h 587')dnl
define(`ESMTP_MAILER_ARGS', `TCP $h 587')dnl
define(`confAUTH_OPTIONS', `A p')dnl
TRUST_AUTH_MECH(`EXTERNAL DIGEST-MD5 CRAM-MD5 LOGIN PLAIN')dnl
define(`confAUTH_MECHANISMS', `EXTERNAL GSSAPI DIGEST-MD5 CRAM-MD5 LOGIN PLAIN')dnl
FEATURE(`authinfo',`hash -o /etc/mail/authinfo/smtp-auth.db')dnl
```

Re-build sendmail's configuration:

```bash
make -C /etc/mail
```

## 4. Verify setup

```bash
service sendmail reload
```

Send test email to name@domain.tld:

```bash
sendmail name@domain.tld
Subject: Test
This is the body of the test email.
```

Press `control + d` to send.
