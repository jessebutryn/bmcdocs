# testemail

## Description

Sends a test email from iDRAC to a specified destination. Prior to running the test email command, make sure that the SMTP server is configured.

The specified index in the idrac.EmailAlert group must be enabled and configured properly. For more information, see iDRAC RACADM CLI Guide available at https://www.dell.com/idracmanuals.

## Synopsis

```bash
racadm testemail -i <index>
```

## Input

- `-i <index>` — Specifies the index of the email alert to test.

## Output

- Success: Test e-mail sent successfully
- Failure: Unable to send test e-mail

## Examples

Commands for the idrac.EmailAlert group:

- Enable the alert.
  ```bash
  racadm set idrac.EmailAlert.1.Enable 1
  ```

- Set the destination email address.
  ```bash
  racadm set idrac.EmailAlert.1.Address user1@mycompany.com
  ```

- Set the custom message that is sent to the destination email address.
  ```bash
  racadm set idrac.emailalert.1.CustomMsg "This is a test!"
  ```

- Make sure that the SMTP IP address is configured properly.
  ```bash
  racadm set idrac.remotehosts.SMTPServerIPAddress 192.168.0
  ```

- View the current email alert settings.
  ```bash
  racadm get idrac.EmailAlert.<index>
  ```
  where `<index>` is a number from 1 to 8.