import re
import os
from datetime import datetime

INPUT_FILE = "input.txt"
OUTPUT_FILE = "emails.txt"
LOG_FILE = "log.txt"


def extract_emails(text):
    """
    Extracts valid email addresses using regex
    """
    pattern = r'[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]+'
    emails = re.findall(pattern, text)
    return list(set(emails))  # remove duplicates


def read_file(file_path):
    if not os.path.exists(file_path):
        print("❌ Input file not found.")
        return None

    with open(file_path, 'r', encoding='utf-8') as file:
        return file.read()


def save_emails(emails, output_path):
    with open(output_path, 'w') as file:
        for email in sorted(emails):
            file.write(email + "\n")


def log_activity(count):
    with open(LOG_FILE, 'a') as log:
        log.write(f"{datetime.now()} - Extracted {count} emails\n")


def main():
    print("📂 Smart Email Extractor Started...\n")

    content = read_file(INPUT_FILE)
    if content is None:
        return

    emails = extract_emails(content)

    if emails:
        save_emails(emails, OUTPUT_FILE)
        log_activity(len(emails))
        print(f"✅ {len(emails)} unique emails saved to '{OUTPUT_FILE}'")
    else:
        print("⚠️ No emails found.")


if __name__ == "__main__":
    main()
