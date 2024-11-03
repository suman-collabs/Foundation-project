## Acceptance Testing Summary Report

### Overview

The application functions according to requirements and generally allows users to navigate and complete tasks intuitively. Users can use the service without needing detailed instructions, and the service's intended purpose is clear. However, multiple areas require improvement to enhance user experience, security, and interface cohesion. While the application is easy to navigate, significant security concerns and user interface issues undermine user confidence and the overall user experience.

#### Key Finding

##### Security Issues

Critical Security Concern: Passwords are displayed in plain text upon account creation, which poses a major security risk.
Unauthorized Access: Users can access other users' resources, a severe issue that compromises data security and privacy.
Lack of User Control Over Credentials:
A "show password" feature is absent during password entry.
Users are not prompted to confirm their password during account creation.

###### User Interface & Navigation

Home Page:
The “Create an Account” button is too small, making it less visible and accessible for new users.
Navigation Flow:
After creating an account, users should either be redirected to the login page or taken directly to the home page. A “Return to Login” link would streamline this process.
Inconsistent Design:
While the home page has an engaging universe-themed background, the login page lacks a visually appealing design and does not align with the overall theme.
Sorting and Organization:
Planets and Moons lack sorting options, which could help users manage their resources. Related resources should also be displayed together for easier navigation.

##### User Feedback & Alert Messages

Vague Error Messages: Error alerts should provide specific guidance, helping users identify and correct issues.
Examples:
Duplicate username: Display "User already exists" instead of "Failed."
Duplicate planet: Display "Planet already exists" instead of "Failed."
Missing planet/moon name: Display "Enter name of the Planet/Moon."
Duplicate resource: Display "Resource already exists."
Planet/moon deletion: Provide a clear alert with instructions and the reason for the error.
Password Confirmation: Users are not required to confirm their password, potentially leading to account access issues due to typos.

### Recommendations

#### Security Enhancements:

Avoid displaying passwords in any user-facing messages.
Implement access control to prevent unauthorized users from viewing or modifying other users' resources.
Add a "show password" feature during password entry and require a password confirmation field for account creation.

#### User Interface Improvements:

Increase the size of the "Create an Account" button on the home page for better visibility.
Update the login page design to align with the universe theme of the home page, creating a cohesive and visually appealing experience.

#### Enhanced User Feedback:

Ensure all alert messages are specific and user-friendly, guiding users to resolve errors effectively.
Add sorting and organization options for planets and moons, and display related resources together.

### Conclusion

While the application largely meets functional requirements and provides an intuitive user experience, significant improvements are required to ensure security, enhance the user interface, and optimize the navigation flow. Addressing these issues will inspire greater user confidence and create a smoother, more secure experience.
