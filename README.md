# HCP Device Status - UiPath RPA

This RPA project automates the process of accessing the **HCP website** to check for **offline devices**, ensuring timely monitoring and alerting. It simulates human interaction to navigate, extract, and analyze device statuses directly within the workflow.

When offline devices are detected, an email is automatically sent using a predefined format.

---

## Project Description

This automation logs into the HCP portal, navigates to the monitoring section, and scrapes device status data. It processes the information in-memory using UiPath, and if offline devices are found, it sends an alert email using a **formatted message body**.

The process leverages **REFramework** for reliability, retry handling, and structured exception handling.

---

## Key Features

- Automated HCP website interaction
- In-memory processing of device statuses (no Excel export)
- Automatic email alerts if offline devices are found
- Email uses a custom, pre-formatted message body
- Built with REFramework for stability and modularity
- Testable design with dedicated xaml modules

---

## Project Structure

| Folder/File                  | Description                                                      |
|------------------------------|------------------------------------------------------------------|
| Main.xaml                    | Main entry point of the automation                              |
| Modular/LoginHCP.xaml        | Logs into the HCP portal                                        |
| Modular/HCPActivity.xaml     | Navigates and processes device status                           |
| Modular/EmailError.xaml      | Sends formatted error email if offline devices are detected     |
| Framework/                   | Standard REFramework components                                 |
| Data/Config.xlsx             | Contains URLs, credentials, and settings                        |
| Tests/                       | Contains test cases for modular workflows                       |
| project.json                 | Project configuration and dependencies                          |
| README.md                    | Project documentation                                            |

---

## Process Workflow

### 1. **Initialization**
- Loads config from `Config.xlsx`
- Initializes logging and retrieves secure credentials

### 2. **Login to HCP**
- `LoginHCP.xaml`:
  - Opens the browser
  - Navigates to HCP login page
  - Logs in using stored credentials

### 3. **Device Status Extraction**
- `HCPActivity.xaml`:
  - Navigates to the device monitoring section
  - Scrapes all device statuses
  - Filters any Offline devices
  - Formats data into a message body

### 4. **Send Alert (If Needed)**
- If offline devices are found:
  - Sends a formatted email alert
- If no devices are offline:
  - Process ends quietly

### 5. **Error Handling**
- Any error triggers:
  - Screenshot capture
  - Logging
  - Execution of `EmailError.xaml` to send error details

---

## How to Run

> Ideal usage is via **Orchestrator schedule** for periodic checks.

### Manual Run:

1. Open the project in **UiPath Studio**
2. Update the `Config.xlsx`:
   - Set HCP portal URL
   - Configure credentials and email parameters
3. Run `Main.xaml`
4. Observe email output if any devices are offline

---

## Exception Handling

- **Business Exceptions**:
  - No device table found
  - No offline status identified (email not triggered)

- **System Exceptions**:
  - Login failure
  - UI elements not detected

Handled via:
- Retry logic (REFramework)
- Screenshots on failure
- `EmailError.xaml` for detailed email alert

---

## Requirements

- UiPath Studio (2022+)
- Chrome/Edge browser with UiPath extension installed
- Access to HCP portal
- Email SMTP/Outlook configuration
- REFramework understanding for modification

---

## Contact

For questions, improvements, or collaboration:

- **Email:** fadillah650@gmail.com  
- **LinkedIn:** [Enrico Naufal Fadilla](https://linkedin.com/in/enrico-naufal-fadilla-54338a256)
