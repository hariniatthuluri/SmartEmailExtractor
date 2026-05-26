

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
