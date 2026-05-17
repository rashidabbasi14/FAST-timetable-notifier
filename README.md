# 🚀 FAST Timetable Notifier: Revolutionizing Campus Schedule Management 🚀

<p align="center">
  ![Banner Image Placeholder](https://i.pinimg.com/564x/fb/9a/59/fb9a59e629af43e1f8bd809b256d6918.jpg)
</p>

> "Never miss a beat. Always be on time. Your academic success, amplified."

## ✨ Introduction

In the dynamic and often demanding environment of university life, keeping track of ever-changing timetables, lecture halls, and lab sessions can be a monumental challenge. Students frequently face the stress of missed classes, last-minute room changes, and the sheer mental overhead of managing complex schedules. For academic institutions, the administrative burden of communicating these critical updates efficiently and reliably to thousands of students is immense.

## 💡 The Problem We Solve

Traditional methods of timetable dissemination are often fragmented, inefficient, and prone to human error. Static PDFs, outdated notice boards, and manual email blasts fail to meet the modern student\'s need for instant, personalized, and accurate information. This leads to confusion, frustration, and ultimately, impacts academic performance and resource utilization.

## 🌟 The Solution: FAST Timetable Notifier

Enter the **FAST Timetable Notifier**, an ingenious, cutting-edge system meticulously engineered to eliminate timetable-related anxieties for students and streamline administrative operations for educational institutions. This isn\'t just a notification system; it\'s your personal academic concierge, ensuring every student is perfectly aligned with their educational journey, every single day.

## 💎 Unrivaled Features & Benefits

Prepare to be amazed by a suite of features designed for unparalleled efficiency and user satisfaction:

*   **Hyper-Personalized Daily Reminders (Your Academic Guardian Angel):** Our flagship feature, developed with student success at its core. Say goodbye to missed lectures and forgotten labs! The system intelligently compiles and delivers a precise, personalized timetable for *tomorrow\'s* classes directly to each student\'s inbox, every evening. It\'s like having a dedicated assistant ensuring you\'re always one step ahead.

*   **Intelligent Timetable Parsing Engine (Mastering Complexity):** Designed to effortlessly ingest and interpret even the most intricate university timetable data from standard Excel files (`Book.xls`). Our advanced parsing algorithms extract critical information with surgical precision, transforming raw data into actionable, easy-to-understand schedules.

*   **Effortless Registration & Course Selection (Designed for You):** A remarkably intuitive web interface allows students to register in mere seconds using their unique university ID and email. They can then seamlessly select their specific courses and sections from a dynamic, always up-to-date list, ensuring their personalized timetable is perfectly tailored.

*   **Robust Account Verification System (Fortress-Grade Security):** We prioritize data integrity and user authentication. Every new registration undergoes a secure email verification process, safeguarding student accounts and ensuring only legitimate users receive notifications. This adds an impenetrable layer of trust and reliability.

*   **Dynamic, Visually Engaging Timetable Generation (Clarity at a Glance):** Beyond mere text, our system crafts beautiful, easy-to-read HTML-formatted timetables within each email. With clear layouts, prominent class details, room numbers, and timings, students can grasp their entire schedule for the next day with a single glance.

*   **Scalable & Resilient Infrastructure (Built for Excellence):** Engineered on a robust PHP and MySQL foundation, coupled with the industry-leading PHPMailer for email delivery, this system is built to handle thousands of students with unwavering performance and reliability. It\'s an investment in uninterrupted operational excellence.

## 🌐 How It Works: A Symphony of Automation

Our system operates with seamless precision, orchestrating complex processes behind the scenes to deliver a simple, powerful experience:

```mermaid
graph TD
    A[Student Accesses main.php] --> B{Register or Remove?};
    B --> |Register| C[Student Enters ID & Email];
    C --> D[main.php Validates & Redirects to register.php];
    D --> E[register.php Displays Courses for Selection];
    E --> F[Student Selects Courses & Sections];
    F --> G[register.php Sends Data to registered.php via AJAX];
    G --> H[registered.php Saves Student & Course Data to DB];
    H --> I[registered.php Sends Verification Email (PHPMailer)];
    I --> J[Student Clicks Verification Link in Email];
    J --> K[verify.php Activates Account (Updates status=1 in DB)];
    K --> L[Daily Cron Job Triggers sendMail.php];
    L --> M[sendMail.php Fetches Active Students & Courses];
    M --> N[sendMail.php Reads Timetable from Excel (Book.xls)];
    N --> O[sendMail.php Generates Personalized Timetable Email];
    O --> P[sendMail.php Sends Daily Timetable Email];
    B --> |Remove| Q[Student Enters ID to Remove];
    Q --> R[main.php Removes Student from DB];
```

## 🚀 Getting Started (For Developers)

To set up the FAST Timetable Notifier for development or deployment, follow these steps:

### Prerequisites

Ensure you have the following installed:

*   PHP (7.x or higher recommended)
*   MySQL Database Server
*   Web Server (Apache, Nginx, or similar)
*   Composer (for PHPMailer dependencies, if not manually included)

### Installation

1.  **Clone the Repository:**
    ```bash
    git clone https://github.com/your-username/FAST-timetable-notifier.git
    cd FAST-timetable-notifier
    ```

2.  **Database Setup:**
    *   Create a MySQL database (e.g., `id5977010_notifier`).
    *   The `main.php` script will automatically create the necessary `students`, `courses`, and `course_names` tables upon its first run if they don\'t exist. However, you will need to manually populate the `course_names` table with your university\'s courses and their full names.
    *   **Crucially, update the database connection details in `main.php`, `register.php`, `registered.php`, `sendMail.php`, and `verify.php` to match your MySQL credentials:**
        ```php
        mysqli_connect(\'localhost\',\'your_db_username\',\'your_db_password\',\'your_db_name\');
        ```

3.  **PHPMailer Configuration:**
    *   Ensure the PHPMailer library is correctly included. The current setup expects it in `PHPMailer/src/` relative to `registered.php` and `sendMail.php`.
    *   **Update SMTP settings in `registered.php` and `sendMail.php`** with your email provider\'s SMTP details:
        ```php
        $mail->Username = \'your_email@example.com\';                 // SMTP username
        $mail->Password = \'your_email_password\';                           // SMTP password
        $mail->setFrom(\'your_email@example.com\', \'Time Table Notifier\');
        $mail->addReplyTo(\'your_email@example.com\', \'Information\');
        ```
        **Note:** For security, it\'s highly recommended to use environment variables or a configuration file for sensitive credentials rather than hardcoding them.

4.  **Place Timetable Excel File:**
    *   Place your university\'s timetable Excel file, named `Book.xls`, in the project\'s root directory. Ensure its format is consistent with how `sendMail.php` expects to read it.

5.  **Configure Cron Job:**
    *   Set up a daily cron job (or scheduled task on Windows) to execute `sendMail.php` at a desired time (e.g., late evening) to send out the next day\'s timetables.
    *   Example cron entry (adjust path and PHP executable): `0 22 * * * /usr/bin/php /path/to/your/FAST-timetable-notifier/sendMail.php > /dev/null 2>&1`

### Project Structure

*   [`main.php`](main.php): User interface for registration and account removal.
*   [`register.php`](register.php): Course selection interface.
*   [`registered.php`](registered.php): Backend for processing registration and sending verification emails.
*   [`sendMail.php`](sendMail.php): Core logic for daily timetable generation and email dispatch (cron job).
*   [`verify.php`](verify.php): Account verification endpoint.
*   `README.md`: This file.
*   `css/`: Contains Bootstrap CSS.
*   `js/`: Contains Bootstrap JS and potentially custom JS.
*   `PHPMailer/`: PHPMailer library (assumed structure for includes).
*   `Libraries/reader.php`: Assumed library for reading `.xls` files.
*   `Book.xls`: The Excel file containing the university\'s master timetable data.

## 📝 Usage (For End-Users)

1.  **Visit the Registration Page:** Navigate to `main.php` in your web browser.
2.  **Register Your Account:** Enter your FAST University ID and your preferred email address. Click the "Register" button.
3.  **Select Your Courses:** On the next page (`register.php`), you will see a list of available courses. For each course you are enrolled in, select your specific section from the dropdown menu. Click the "Register" button at the bottom to finalize your course selections.
4.  **Account Verification:** An email will be sent to the address you provided. Click the verification link in this email to activate your account. Until your account is verified, you will not receive timetable notifications.
5.  **Receive Daily Notifications:** Once your account is activated, you will automatically start receiving personalized timetable emails daily, reminding you of your classes for the upcoming day.
6.  **Remove Your Account:** If you wish to stop receiving notifications, visit `main.php` again, enter your FAST University ID in the "Remove Account" section, and click the "Remove" button.

## 🤝 Contributing

We welcome contributions from the community to make the FAST Timetable Notifier even better! Whether it\'s bug reports, feature suggestions, or code contributions, your input is invaluable. Please feel free to open an issue or submit a pull request.

## 📄 License

This project is licensed under the MIT License - see the `LICENSE.md` file for details.

## 📞 Contact

For any inquiries, support, or collaboration opportunities, please reach out to:

*   **Email:** your.email@example.com
*   **Project Link:** [https://github.com/your-username/FAST-timetable-notifier](https://github.com/your-username/FAST-timetable-notifier)
