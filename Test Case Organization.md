# Test Case Creation: Planetarium User Registration

- Use Case Id: 1
- Description: Users should be able to open a new User account with the Planetarium
- Actors:
  - New User

### Pre-requirement

- Username 'Robin' not present in the database
- Usernmae 'Batman' present in the database
- Username with no characters is not present in the database
- Username "BatmanAndRobinToTheRescue20202" not present in the database

### Test Data

#### Requirement: Usernames and passwords should not be longer than 30 characters

| 0 character Username | 30 characters Username         | 31 characters Usernames         |
| -------------------- | ------------------------------ | ------------------------------- |
|                      | BatmanAndRobinToTheRescue20202 | JokerAndRiddlerAreAtItAgain1010 |

| 0 character Password | 30 characters Password         | 31 characters Password          |
| -------------------- | ------------------------------ | ------------------------------- |
|                      | GordonIsMyHeroForeverGoodMan11 | LexLuthorIsSchemingAgainOhNo!!! |

#### Requirement: Users should have unique usernames

| Unique Username | Non-Unique Username |
| --------------- | ------------------- |
| Robin           | Batman              |

#### Requirement: Passwords should never be visible in plaintext

- Password that should be obfuscated: "I am the night"
  - use for both Exploratory Testing and Error Guess Testing

#### Acceptance Testing Data

Use positive and negative test data found for [credentials length](#requirement-usernames-and-passwords-should-not-be-longer-than-30-characters) and [username uniqueness](#requirement-users-should-have-unique-usernames) depending on what kind of Acceptance Testing you are performing

#### Environment Data

- Browser: Edge
- Operating System: Windows 10
- Version of Planetarium: 1.0
- Background Data:
  - Login Page for Planetarium: http://localhost:8080/

### Test Scenarios

#### Decision Table For Username/Password Character Length Requirement Testing

| Username                        | Password                        | Account Creation Result | Redirect                             |
| ------------------------------- | ------------------------------- | ----------------------- | ------------------------------------ |
| (0 characters)                  | (0 characters)                  | User created            | User redirected to login page result |
| (0 characters)                  | GordonIsMyHeroForeverGoodMan11  | User created            | User redirected to login page        |
| (0 characters)                  | LexLuthorIsSchemingAgainOhNo!!! | User not created        | User remains on creation page        |
| BatmanAndRobinToTheRescue20202  | (0 characters)                  | User created            | User redirected to login page        |
| BatmanAndRobinToTheRescue20202  | GordonIsMyHeroForeverGoodMan11  | User created            | User redirected to login page        |
| BatmanAndRobinToTheRescue20202  | LexLuthorIsSchemingAgainOhNo!!! | User not created        | User remains on creation page        |
| JokerAndRiddlerAreAtItAgain1010 | (0 character)                   | User not created        | User redirected to login page        |
| JokerAndRiddlerAreAtItAgain1010 | GordonIsMyHeroForeverGoodMan11  | User not created        | User remains on creation page        |
| JokerAndRiddlerAreAtItAgain1010 | LexLuthorIsSchemingAgainOhNo!!! | User not created        | User remains on creation page        |

#### Decision Table for Unique Username Requirement Testing

| Username | Password                       | User Created     | User redirected to login page result |
| -------- | ------------------------------ | ---------------- | ------------------------------------ |
| Robin    | GordonIsMyHeroForeverGoodMan11 | User created     | User redirected to login page        |
| Batman   | GordonIsMyHeroForeverGoodMan11 | User not created | User remains on creation page        |

#### Parameterized Test Scenario

| Step                                                                          | Actor    | Data                   | Result                                        |
| ----------------------------------------------------------------------------- | -------- | ---------------------- | --------------------------------------------- |
| given the user is on the login page                                           | new user | http://localhost:8080/ |                                               |
| when the user clicks the create account button                                | new user |                        | should be redirected to the registration page |
| when the user provides {username} and {password} and clicks the create button | new user | {username},{password}  |                                               |
| then the user should be given an alert saying {Account Creation Result}       | new user |                        | {Account Creation Result}                     |
| and {User Redirected to Login Page Result}                                    | new user |                        | {User Redirected to Login Page Result}        |

### Use Case Id: 2

- Description: Users should be able to securely access their account
- Actors:
  - Logged in User

#### Pre-requirement

- Username "Batman" present in the database
- Username "Joker" not present in the database
- Username "Joker" is then adeed to the database

### Test Data

#### Requirement: Passwords should never be visible in plain text

| Username | Password       |
| -------- | -------------- |
| Batman   | I am the night |
| Joker    | I am the night |

#### Requirement: Only logged in Users should be able to access the Planetarium home page

| Username | Password       |
| -------- | -------------- |
| Batman   | I am the night |

link: http://localhost:8080/

#### Requirement: Users should only be able to interact with resources they have added to the Planetarium

-Equivalence Partition
-For this, we make sure newly created User 'Joker' doesn't see any information he hasn't added.

#### Acceptance Testing Data

### Test Scenarios

#### Decision Table for User's attempt to access their account

| Username | Account Access Result | Redirect                       |
| -------- | --------------------- | ------------------------------ |
| Batman   | user logged in        | User directed to the home page |
| Joker    | User not logged in    | User remains on the login page |

#### Parameterized Test Scenario

| Step                                                                                                | Data                   | Result                                    |
| --------------------------------------------------------------------------------------------------- | ---------------------- | ----------------------------------------- |
| Given the user is on the login page                                                                 | http://localhost:8080/ |                                           |
| when the user provides Username: <Username> and Password: <Password> , and clicks the log in button | <username>,<password>  | should be directed to the home page       |
| user is given access to the resource                                                                | N/A                    | Access to User added ressources displayed |

### Use Case Id: 3

- Description: Users should be able to see planets and moons added to the planetarium
- Actors:
  - Logged in User

### Pre-requirement:

- Username 'Batman' present in the database
- Username 'Joker' not present but added later while testing to the database

### Test Data

#### Requirement: Only logged in Users should be able to access the Planetarium home page

| Username | Password       |
| -------- | -------------- |
| Batman   | I am the night |

link: http://localhost:8080/

#### Requirement: Planets should be "owned" by the user that added them to the Planetarium

| Username | Password       |
| -------- | -------------- |
| Joker    | I am the night |

-Exploratory and error guess testing to see if the newly added User 'Joker' doesn't own any planet and have no access to other's resources.

#### Requirement: Users should only be able to interact with resources they have added to the Planetarium

#### Parameterized Test Scenario

| Step                                    | Actor | Data                                                  | Result                                             |
| --------------------------------------- | ----- | ----------------------------------------------------- | -------------------------------------------------- |
| User is on the login page               | User  | http://localhost:8080/                                |                                                    |
| User provides {username} and {password} | User  | {username},{password}                                 | should be directed to the home page                |
| User adds planet and moon               | User  | Photos of Planet and Moons, names of Planet and Moons | should refresh the page and see the updated result |

### Use Case Id: 4

- Description: Users should be able to add new Planets to the Planetarium
  - Actors
    - Logged in User

### Pre-requirement:

- Username 'Batman' present in the database
- Planet 'Earth" present in the database
- Planet 'Jupiter' not present in the database

## Test Data

#### Requirement: Planet and Moon names should not have more than 30 characters

| 0 character Planet name | 30 characters Planet name      | 31 characters Planet name       |
| ----------------------- | ------------------------------ | ------------------------------- |
|                         | ThisIsAPlanetWith30characters0 | ThisIsAPlanetWith31characters01 |

#### Requirements: Planets should be “owned” by the user that added it to the Planetarium

- Exploratory testin to check for the owner id# of the planet matches the Id# of the User.

#### Requirements: "Planets and moons should have unique names

-- No same name regardless of Lowercase/Uppercase letters

| Unique Planet name | Duplicate Planet name |
| ------------------ | --------------------- |
| Earth              | earth                 |
| Earth              | Earth                 |

#### Requirements: Planets and Moons should allow adding an associated image, but it is not required for the data to be added to the database

| Planet  | Planet Photo      |
| ------- | ----------------- |
| Jupiter | no value          |
| Jupiter | Photo_Jupiter.jpg |

#### Environment Data

- Browser: Edge
- Operating System: Windows 10
- Version of Planetarium: 1.0
- Background Data:
  - Login Page for Planetarium: http://localhost:8080/

## Test Scenarios

### Decision Table For Planet/Moon Character Length Requirement Testing

- No value Planet Name
- 30 Character Planet Name
- 31 Character Planet Name

| Planet Name                     | Planet Photo      |
| ------------------------------- | ----------------- |
|                                 | Photo_jupiter.jpg |
| ThisIsAPlanetWith30characters0  | Photo_Jupiter.jpg |
| ThisIsAPlanetWith31characters01 | Photo_Jupiter.jpg |

### Decision Table for Unique Planet and Moon name

| Planet Name | Action and message               |
| ----------- | -------------------------------- |
| Earth       | Planet not added, exists already |
| earth       | Planet not added, exists already |
| Jupiter     | Planet added                     |

### Decision Table for Planets and Moon to allow an associated image, but not required for the date to be added to the database

| Photo         | Name    | Result                            | Redirect                                   |
| ------------- | ------- | --------------------------------- | ------------------------------------------ |
| Jupiter photo | Jupiter | Photo and Planet added            | Refreshed Home Page                        |
| Jupiter Photo |         | Not Added                         | Need names of planet to be added           |
|               | Jupiter | Planet adedd                      | Refreshed Home Page with only name appears |
|               |         | need planet name / name and photo | stay on home page                          |

## Parameterized Test scenario

| Step                                                                                                   | Actor | Data                         | Result                                  |
| ------------------------------------------------------------------------------------------------------ | ----- | ---------------------------- | --------------------------------------- |
| Given the user is on the home page                                                                     | User  | http://localhost:8080/       | should be at Home Page                  |
| User provides valid {username} and {password}                                                          | User  | {username}, {password}       |                                         |
| User selects Planet from the drop down list and enters planet name and clicks the submit planet button | User  | Planet Name and Planet Photo | {page refreshed and planet/moon added } |
| Planet is added/not added                                                                              | User  |                              | Planet added/not added                  |

### Use Case Id: 5

- Description: Users should be able to remove Planets from the Planetarium
  - Actors
    - Logged in User

#### Pre-requirement:

- Username 'Batman' present in the database
- Planet 'Earth', Moon 'Luna' present in the database
- Planet 'Jupier' not present which will be added while testing
- No Moon added for the Planet Jupiter

## Test Data

#### Requirement: Users should only be able to interact with resources they have added to the Planetarium

| User   | Resources        |
| ------ | ---------------- |
| Batman | Provided already |
| Joker  | None (new user)  |

#### Requirement: Planets should be “owned” by the user that added it to the Planetarium

| User/Owner | Planets owned by User | Planets not owned by User |
| ---------- | --------------------- | ------------------------- |
| Batman     | Earth, Mars           | Jupiter                   |
| Joker      | Jupiter               | Earth, Mars               |

#### Environment Data

- Browser: Edge
- Operating System: Windows 10
- Version of Planetarium: 1.0
- Background Data:
  - Login Page for Planetarium: http://localhost:8080/

## Test Scenarios

### Decision Table for Deletion Criteria

| Planet Name | Moon    |
| ----------- | ------- |
| Earth       | Moon    |
| Jupiter     | No moon |

## Parameterized Test scenario

| Step                                                                                                   | Actor          | Data                              | Result                               |
| ------------------------------------------------------------------------------------------------------ | -------------- | --------------------------------- | ------------------------------------ |
| given the user is on the home page                                                                     | Logged in User | http://localhost:8080/planetarium | Home page with list of resources     |
| User provides valid {username} and {password}                                                          | User           | {username}, {password}            |                                      |
| User selects Planet from the drop down list and enters planet name and clicks the delete planet button | User           | Planet Name                       | {page refreshed and planet removed } |
| Planet is removed                                                                                      | User           |                                   | Planet removed                       |

| User provides resources' valid name and type | User | Names of Planet | Refreshed and Updated Home Page |

### Use Case Id: 6

- Description: Users should be able to add Moons to the Planetarium associated with a Planet
  -Actors
  -Logged in User

### Pre-requirement:

- Username 'Batman' present in the database
- Jupiter added to the database
- Moon 'Europa' not present in the database

## Test Data

#### Requirement: Moons should be “owned” by the Planet the User adding the moon associated it with

| Planet Id | Moon names | Owner Id |
| --------- | ---------- | -------- |
| 1         | Europa     | 1        |

#### Requirement: Planet and Moon names should not have more than 30 characters

| 0 character Moon name | 30 characters Moon name        | 31 characters Moon name         |
| --------------------- | ------------------------------ | ------------------------------- |
|                       | ThisIsAMoonWith30characters012 | ThisIsAMoonWith31characters0123 |

#### Requirement: Planets and Moons should allow adding an associated image, but it is not required for the data to be added to the database

| Moon Photo | Moon Name | Result               | Redirect                                   |
| ---------- | --------- | -------------------- | ------------------------------------------ |
| Luna photo | Luna      | Photo and Moon added | Refreshed Home Page                        |
|            | Luna      | Planet adedd         | Refreshed Home Page with only name appears |

#### Requirement: Moons should have unique name

| Moon Name | Moon Photo |
| --------- | ---------- |
| Luna      | Photo_Luna |
| luna      | Photo_Luna |
| Tuna      | Photo      |

#### Environment Data

- Browser: Edge
- Operating System: Windows 10
- Version of Planetarium: 1.0
- Background Data:
  - Login Page for Planetarium: http://localhost:8080/

## Test Scenarios

### Decision Table for Moon's unique Name

| Moon Name | Moon Result |
| --------- | ----------- |
| Luna      | failed      |
| luna      | failed      |
| Tuna      | passed      |

### Decision Table for Moon's Character Length Limit

| Moon Name                       | Action Addition result | Redirect          |
| ------------------------------- | ---------------------- | ----------------- |
|                                 | Nothing added          | Stay on home page |
| ThisIsAMoonWith30characters012  | Moon added             | Stay on home page |
| ThisIsAMoonWith31characters0123 | Nothing Added          | Stay on Home Page |

## Parameterized Test scenario

| Step                                | Actor | Data                              | Result                     |
| ----------------------------------- | ----- | --------------------------------- | -------------------------- |
| given the user is on the home page  | User  | http://localhost:8080/planetarium |                            |
| user provides valid moon name/photo | User  | Names/Photos of moon              | Page refreshed and Updated |
| Moon added                          | User  |                                   | Page refreshed             |

### Use Case Id: 7

- Description: Users should be able to remove Moons from the Planetarium
  -Actors
  -Logged in User

### Pre-requirement:

- Username 'Batman' with Id#1 present in the database

## Test Data

#### Requirement: Moons should be “owned” by the Planet the User adding the moon associated it with

| Moon Name | Moon Id | User Id |
| --------- | ------- | ------- |
| Luna      | 1       | 1       |
| Titan     | 2       | 2       |

#### Requirement: Users should only be able to interact with resources they have added to the Planetarium

    - Exploratory and error guess testing to see if you can acces other user's resources

#### Environment Data

- Browser: Edge
- Operating System: Windows 10
- Version of Planetarium: 1.0
- Background Data:
  - Login Page for Planetarium: http://localhost:8080/

## Test Scenarios

### Decision Table for moon owned by planet

| Drop-down menu | Name | Planet Id | Action                        |
| -------------- | ---- | --------- | ----------------------------- |
| Moon           |      |           | Error{enter all requirements} |
| Moon           | Luna |           | Error{enter all requirements} |
| Moon           | Luna | 2         | Error{wrong parent planet}    |
| Moon           | Luna | 1         | Successfully deleted          |
| Moon           |      | 1         | Error{enter all requirements} |

## Parameterized Test scenario

| Step                                                                                                | Actor | Data                                          | Result                              |
| --------------------------------------------------------------------------------------------------- | ----- | --------------------------------------------- | ----------------------------------- |
| given the user is on the home page                                                                  | User  | http://localhost:8080/planetarium             |                                     |
| when the user provides Username: <Username> and Password: <Password> , and clicks the log in button | User  | Username: <Username> and Password: <Password> | Redirected to Planetarium Home Page |
| Moon deleted                                                                                        | User  |                                               | Page refreshed                      |

## Acceptance Testing

- Is the intended use of the service intuitive?
- Is the service easy to use?
- Does the service inspire confidence?
- Is the service pleasing to look at?

The app works as intended and performs the functions as requirements; however, it can be improved in many areas to make the user's experience easy and smooth.
The intended use of the service is intuitive in general. The user can naturally navigate and use the service without following detailed instruction.
However, the service doesn't inspire confidence beacause of security isssue being compromised. The service could also see some improvements in the User Interface.

- As a general user, on the home page, "Create an Account" button should have been larger.
- While typing the password, "show password" option should have been added, and required to enter the password again for confirmation
- When the account is created, the display message shouldn't have shown the password which is a huge security issue
- There should have been a link to take you back to the login page, or it should have taken the user directly to the home page
- The alert messages when error occurs are vague and should be specific to let the user know about the issue like:
  - When no unique username is provided, "user already exists" is a better alert message than failed
  - When adding already existing planet, "Planet already exists" message should be displayed instead of just failed.
  - When removing Planet/Moon, clear alert message with the reason and instruction should be displayed for the user.
  - When adding only photo. "Enter name of the Planet/Moon" should be displayed instead of just failed.
  - When adding duplicate values, "Resources already exist" messages should be displayed.
  - The Planet/Moon could be managed and sorted with sort by options, and related resources should have been displayed together.

Due to these issues, even though the intended use of service is intuitive and easy to use, the service doesn't provide the user with sense of security, and doesn't inspire confidence with so many critical issues. The home page is good with the good background of universe, but the login page of the application is not pleasing to look at and doesn't keep up with the theme of the app and the home page.
