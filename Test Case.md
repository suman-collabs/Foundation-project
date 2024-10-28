# Test Case

## Planetarium User Registration

-Use Case ID: 1

- Description: Users should be able to open a new User account with the Planetarium
- Actors:
  - New user

### Test Data

#### Requirement: Usernames and passwords should not be longer than 30 characters

| 0 character username | 30 characters username         | 31 character Usernames          |
| -------------------- | ------------------------------ | ------------------------------- |
|                      | BatmanAndRobinToTheRescue20202 | JokerAndRiddlerAreAtItAgain1010 |

#### Requirement: Users should have unique usernames

| Unique Username | Non-Unique Username |
| --------------- | ------------------- |
| Robin           | Batman              |

#### Requirement: Passwords should never be visible in plaintext

- Password that should be obfuscated: "I am the night"
  - use for both Exploratory Testing and Error Guess Testing

#### Acceptance Testing Data

Use positive and negative test data found [credentials length](#requirement-usernames-and-passwords-should-not-be-longer-than-30-characters) and [username uniqueness](#requirement-users-should-have-unique-usernames)

#### Environment Data

- Browser: Chrome

- Operating System : Mac Os Sonoma 14.5
- Version of Planetarium: 1.0
- Background Data:

  - Login Page for Planetarium: http://localhost:8080/
