import smtplib
from email.mime.text import MIMEText
from email.mime.multipart import MIMEMultipart
from datetime import datetime

def send_birthday_email(to_email, subject, body):
    # Email configuration
    smtp_server = "smtp.gmail.com"  # Update with your email provider's SMTP server
    smtp_port = 587  # Update with the appropriate port for your email provider
    sender_email = "your_email@gmail.com"  # Update with your email address
    sender_password = "your_password"  # Update with your email password

    # Create the email message
    message = MIMEMultipart()
    message['From'] = sender_email
    message['To'] = to_email
    message['Subject'] = subject

    # Attach the body of the email
    message.attach(MIMEText(body, 'plain'))

    # Connect to the SMTP server
    with smtplib.SMTP(smtp_server, smtp_port) as server:
        # Start TLS for security
        server.starttls()
        
        # Login to the email account
        server.login(sender_email, sender_password)
        
        # Send the email
        server.sendmail(sender_email, to_email, message.as_string())

if __name__ == "__main__":
    # Birthday person's information
    to_email = "recipient@example.com"  # Replace with the recipient's email address
    subject = "Happy Birthday!"
    body = "Happy Birthday! 🎉🎂\n\nWishing you a fantastic day!"

    # Birthday date
    birthday_date = datetime.strptime("2005-06-20", "%Y-%m-%d")  # Update with the actual birthdate

    # Check if it's the birthday
    current_date = datetime.now()
    if current_date.date() == birthday_date.date():
        send_birthday_email(to_email, subject, body)
        print("Birthday email sent successfully.")
    else:
        print("No birthday today.")
