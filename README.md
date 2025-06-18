# Calculator-Application-Automation-Email-Notification
# Power Automate Desktop Flow: Calculator Automation & Email Notification

This repository contains a Power Automate Desktop flow designed to automate arithmetic calculations using the Windows Calculator and then send the final result via email.

## Table of Contents

- [Features](#features)
- [Prerequisites](#prerequisites)
- [Installation & Setup](#installation--setup)
- [How to Run](#how-to-run)
- [Flow Details](#flow-details)
- [Troubleshooting](#troubleshooting)
- [Contributing](#contributing)
- [License](#license)

## Features

- Launches the Windows Calculator application in Scientific mode.
- Executes a predefined sequence of mathematical operations.
- Extracts the final calculated value from the Calculator's display.
- Saves the extracted value to a text file on the user's desktop.
- Automatically generates and sends an email via Microsoft Outlook containing the calculated amount to a specified recipient.

## Prerequisites

Before running this flow, ensure you have the following:

- **Windows Operating System:** Windows 10 or Windows 11.
- **Power Automate Desktop:** Installed and configured on your machine.
- **Microsoft Outlook:** An active Outlook installation with a configured email account.

## Installation & Setup

### Option 1: Importing the Flow (Recommended)

1.  Download the `.pad` flow file (if available, it would be attached here).
2.  Open Power Automate Desktop.
3.  Click on the "Import" option from the main dashboard.
4.  Browse to the downloaded `.pad` file and select it.
5.  Follow the on-screen instructions to complete the import process.

### Option 2: Manually Recreating the Flow

If you don't have the `.pad` file, you can recreate the flow step-by-step in Power Automate Desktop:

1.  **Create a New Flow:** Open Power Automate Desktop and click "New flow".
2.  **Launch Calculator:**
    -   Drag and drop the "Run application" action.
    -   Set "Application path" to `calculator.exe`.
3.  **Perform Calculations:**
    -   Drag and drop multiple "Press button in window" actions.
    -   For each action, select the Calculator window.
    -   Use the UI element picker to select the numerical and operator buttons as per the video demonstration:
        -   `1`, `0`, `0`, `+`, `6`, `0`, `+`, `1`, `5`, `5`, `+`, `3`, `7`, `+`, `4`, `0`, `+`, `2`, `2`, `4`, `+`, `2`, `3`, `+`, `2`, `2`, `+`, `3`, `5`, `+`, `6`, `0`, `=`
4.  **Get Calculation Result:**
    -   Drag and drop the "Get details of UI element in window" action.
    -   Select the Calculator window and then target the display area that shows the result.
    -   Set "Attribute name" to the appropriate attribute that holds the display value (commonly "Display is" or similar depending on OS version).
    -   Store the result in a variable named `DisplayValue`.
5.  **Get Desktop Path:**
    -   Drag and drop the "Get special folder" action.
    -   Select "Desktop" as the special folder.
    -   Store the path in a variable named `SpecialFolderPath`.
6.  **Write Result to File:**
    -   Drag and drop the "Write text to file" action.
    -   Set "File path" to `%SpecialFolderPath%\CalculatedAmount.txt`.
    -   Set "Text to write" to `%DisplayValue%`.
    -   Choose `Overwrite` if the file exists.
7.  **Launch Outlook:**
    -   Drag and drop the "Launch Outlook" action.
8.  **Send Email:**
    -   Drag and drop the "Send email message through Outlook" action.
    -   Set "To" to `sathwikheg@gmail.com` (or your desired recipient).
    -   Set "Subject" to `Total Amount`.
    -   Set "Email body" to `Kindly Pay the amount : Display is %DisplayValue%`.

## How to Run

1.  Open the flow in Power Automate Desktop.
2.  Click the "Run" button (play icon) in the top toolbar.
3.  The flow will execute all the defined steps automatically.

## Flow Details

The flow automates the following sequence of actions:

1.  Starts the Windows Calculator application.
2.  Interacts with the Calculator by "pressing" virtual buttons to input the arithmetic expression: $100 + 60 + 155 + 37 + 40 + 224 + 23 + 22 + 35 + 60$.
3.  Reads the final numerical result (which is 950) from the Calculator's display.
4.  Saves this result into a text file named `CalculatedAmount.txt` on your desktop.
5.  Initiates Microsoft Outlook.
6.  Composes and sends an email to `sathwikheg@gmail.com` with the subject "Total Amount" and a body stating "Kindly Pay the amount : Display is 950".

## Troubleshooting

-   **Calculator Issues:** If the Calculator isn't responding or buttons aren't pressed correctly, ensure the Calculator is closed before running the flow. You might need to re-capture the UI elements if the Calculator's interface has changed.
-   **Email Sending Errors:** Verify that your Outlook account is properly configured and that the recipient's email address is correct. Check Outlook's outbox for any unsent messages or error notifications.
-   **Incorrect Calculation Result:** Double-check the sequence of numbers and operators in the "Press button in window" actions to ensure they match the intended calculation.
-   **Display Value Not Captured:** If the `Get details of UI element` action fails, inspect the Calculator's display element again to confirm the correct attribute name for the displayed text.

## Contributing

Feel free to suggest improvements or report issues by opening an issue in this repository.

## License

This project is open-source and available under the [MIT License](LICENSE.md). (You would typically include a LICENSE.md file in a real repository).
