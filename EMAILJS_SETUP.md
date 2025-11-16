# EmailJS Setup Guide

This guide will help you set up EmailJS for the contact form in your My Home Constructions website.

## Step 1: Create an EmailJS Account

1. Go to [https://www.emailjs.com/](https://www.emailjs.com/)
2. Click "Sign Up" and create a free account
3. Verify your email address

## Step 2: Add an Email Service

1. Once logged in, go to **Email Services** in the left sidebar
2. Click **Add New Service**
3. Choose your email provider (Gmail, Outlook, Yahoo, etc.)
4. Follow the instructions to connect your email account
   - For Gmail: You'll need to allow "Less secure app access" or use an App Password
   - For Outlook: Sign in with your Microsoft account
5. **Copy the Service ID** (e.g., `service_abc123`) - you'll need this later

## Step 3: Create an Email Template

1. Go to **Email Templates** in the left sidebar
2. Click **Create New Template**
3. Replace the default template with this content:

### Email Template Content:

**Template Name:** `contact_form_submission`

**Subject:**
```
New Enquiry from {{from_name}} - {{project_type}}
```

**Body:**
```html
<h2>New Contact Form Submission</h2>

<p><strong>Name:</strong> {{from_name}}</p>
<p><strong>Phone:</strong> {{from_phone}}</p>
<p><strong>Suburb:</strong> {{from_suburb}}</p>
<p><strong>Email:</strong> {{from_email}}</p>
<p><strong>Project Type:</strong> {{project_type}}</p>

<p><strong>Message:</strong></p>
<p>{{message}}</p>

<hr>
<p><small>This email was sent from the My Home Constructions contact form.</small></p>
```

**From Name:** `My Home Constructions`

**Reply To:** `{{from_email}}`

**To Email:** `info@myhomeconstruction.com.au`

4. Click **Save**
5. **Copy the Template ID** (e.g., `template_xyz789`)

## Step 4: Get Your Public Key

1. Go to **Account** (top right corner) → **General**
2. Find your **Public Key** (it looks like: `AbC123dEfGhIjKlMnO`)
3. **Copy the Public Key**

## Step 5: Update Your .env File

Open the `.env` file in your project root and replace the placeholders:

```env
VITE_EMAILJS_SERVICE_ID=service_abc123
VITE_EMAILJS_TEMPLATE_ID=template_xyz789
VITE_EMAILJS_PUBLIC_KEY=AbC123dEfGhIjKlMnO
```

Replace with your actual values from Steps 2, 3, and 4.

## Step 6: Test the Contact Form

1. Restart your development server:
   ```bash
   npm run dev
   ```

2. Fill out the contact form on your website
3. Submit the form
4. Check your email inbox (info@myhomeconstruction.com.au) for the test email
5. Check the EmailJS dashboard to see the email in the logs

## Troubleshooting

### Email not received?

1. **Check EmailJS Dashboard**: Go to Email Logs to see if the email was sent
2. **Check Spam Folder**: The email might be in spam
3. **Verify Template Variables**: Make sure all `{{variable}}` names match exactly
4. **Check Service Connection**: Your email service might need re-authentication

### "Invalid Public Key" Error?

- Make sure you copied the Public Key correctly from Account → General
- Ensure there are no extra spaces in the .env file

### Form submits but no email?

- Open browser console (F12) and check for errors
- Verify all three environment variables are set correctly
- Restart the dev server after changing .env

## EmailJS Free Tier Limits

- **200 emails per month**
- **2 email services**
- **3 email templates**

For higher limits, upgrade to a paid plan at [EmailJS Pricing](https://www.emailjs.com/pricing/).

## Support

- EmailJS Documentation: https://www.emailjs.com/docs/
- EmailJS Support: support@emailjs.com

## Notes

- The contact form still saves submissions to your Supabase database
- Email sending is now handled entirely by EmailJS (no Supabase Edge Functions needed)
- You can customize the email template anytime in the EmailJS dashboard
