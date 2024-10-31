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

| username | password |
| -------- | -------------- | <------ While logging in
| Batman | I am the night |

| username | password |
| -------- | ------------ | <------- While creating a new user
| Joker | I am the day |

#### Requirement: Only logged in Users should be able to access the Planetarium home page

| logged in user |
| -------------- |
| Batman         |

link: http://localhost:8080/

#### Requirement: Users should only be able to interact with resources they have added to the Planetarium

-Equivalence Partition
| Batman's resources | Joker's resources |
|----------|-------|

#### Acceptance Testing Data

Use positive and negative test data found for logged in user

### Test Scenarios

#### Decision Table for User's attempt to access their account

| Username | Account Access Result | Redirect                       |
| -------- | --------------------- | ------------------------------ |
| Batman   | user logged in        | User directed to the home page |
| Joker    | User not logged in    | User remains on the login page |

#### Parameterized Test Scenario

| Step                                    | Actor | Data                   | Result                              |
| --------------------------------------- | ----- | ---------------------- | ----------------------------------- |
| Given the user is on the login page     | User  | http://localhost:8080/ |                                     |
| user provides <username> and <password> | User  | <username>,<password>  | should be directed to the home page |

- To see the user can't access other user's resources
  | Step | Actor | Data | Result |
  |------|--------|-----|-------|
  |Given the user is on the login page|Username: "Batman" Password "I am the night" | http://localhost:8080/| |
  |the user explores |

### Use Case Id: 3

- Description: Users should be able to see planets and moons added to the planetarium
- Actors:
  - Logged in User

### Test Data

#### Requirement: Only logged-in Users should be able to access the Planetarium home page

| username | password         |
| -------- | ---------------- |
| Batman   | 'I am the night' |
| Joker    | 'I am the day'   |

#### Requirement: Planets should be "owned" by the user that added them to the Planetarium

- Exploratory and Error Guessing Testing needed here.

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

## Test Data

#### Requirement: Planet and Moon names should not have more than 30 characters

| 0 character Planet name | 30 characters Planet name       | 31 characters Planet name        |
| ----------------------- | ------------------------------- | -------------------------------- |
|                         | ThisIsAPlanetWith30characters01 | ThisIsAPlanetWith31characters022 |

| 0 character Moon name | 30 characters Moon name        | 31 characters Moon name         |
| --------------------- | ------------------------------ | ------------------------------- |
|                       | ThisIsAMoonWith30characters011 | ThisIsAMoonWith31characters0212 |

#### Requirements: Planets should be “owned” by the user that added it to the Planetarium

-

#### Requirements: "Planets and moons should have unique names

-- No same name regardless of Lowercase/uppercase letters

| Unique Planet name | Duplicate Planet name |
| ------------------ | --------------------- |
| Earth              | earth                 |
| Earth              | Earth                 |

#### Requirements: Planets and Moons should allow adding an associated image, but it is not required for the data to be added to the database

| Photo of Planet Jupiter | Only Name of Planet Jupiter |
| ----------------------- | --------------------------- |

### Acceptance Testing Data

Use positive and negative testing data found for [unique names](#requirements-planets-and-moons-should-have-unique-names) and [photo](#requirements-planets-and-moons-should-allow-adding-an-associated-image-but-it-is-not-required-for-the-data-to-be-added-to-the-database)

#### Environment Data

- Browser: Edge
- Operating System: Windows 10
- Version of Planetarium: 1.0
- Background Data:
  - Login Page for Planetarium: http://localhost:8080/

## Test Scenarios

### Decision Table For Planet/Moon Character Length Requirement Testing

| Planet Name                      | Moon Name                       | Action Addition result | Redirect                              |
| -------------------------------- | ------------------------------- | ---------------------- | ------------------------------------- |
|                                  |                                 | Nothing added          | Stay on home page                     |
|                                  | ThisIsAMoonWith30characters011  | nothing added          | Stay on home page                     |
|                                  | ThisIsAMoonWith31characters0212 | Nothing Added          | Stay on Home Page                     |
| ThisIsAPlanetWith30characters01  |                                 | Planet Added           | Refreshed home page with updated list |
| ThisIsAPlanetWith30characters01  | ThisIsAMoonWith30characters011  | Planet and Moon Added  | Refreshed home page with updated list |
| ThisIsAPlanetWith30characters01  | ThisIsAMoonWith31characters0212 | Nothing Added          | Stay on Home Page                     |
| ThisIsAPlanetWith31characters022 |                                 | Nothing Added          | Stay on Home Page                     |
| ThisIsAPlanetWith31characters022 | ThisIsAMoonWith30characters011  | Nothing added          | Stay on Home page                     |
| ThisIsAPlanetWith31characters022 | ThisIsAMoonWith31characters0212 | Nothing added          | Stay on Home page                     |

### Decision Table for Unique Planet and Moon name

| Planet Name | Action and message    |
| ----------- | --------------------- |
| Saturn      | Planet added          |
| Earth       | Planet exists already |

--

| Moon Name | Action and message  |
| --------- | ------------------- |
| Dione     | Moon added          |
| Luna      | Moon exists already |

### Decision Table for Planets and Moon to allow an associated image, but not required for the date to be added to the database

| Photo        | Name   | Result                            | Redirect                                   |
| ------------ | ------ | --------------------------------- | ------------------------------------------ |
| Saturn photo | Saturn | Photo and Planet added            | Refreshed Home Page                        |
| Saturn Photo |        | Not Added                         | Need names of planet to be added           |
|              | Saturn | Planet adedd                      | Refreshed Home Page with only name appears |
|              |        | need planet name / name and photo | stay on home page                          |

| Moon Photo | Moon Name | Result               | Redirect                                   |
| ---------- | --------- | -------------------- | ------------------------------------------ |
| Luna photo | Luna      | Photo and Moon added | Refreshed Home Page                        |
| Luna Photo |           | Not Added            | Need names of moon to be added             |
|            | Luna      | Planet adedd         | Refreshed Home Page with only name appears |

## Parameterized Test scenario

| Step                                          | Actor          | Data                     | Result                                  |
| --------------------------------------------- | -------------- | ------------------------ | --------------------------------------- |
| Given the user is on the home page            | User           | http://localhost:8080/   | should be at Home Page                  |
| User provides valid {username} and {password} | User           | {username}, {password}   |                                         |
| User provides valid planet and moon names     | Logged in User | names of planet and moon | {page refreshed and planet/moon added } |

### Use Case Id: 5

- Description: Users should be able to remove Planets from the Planetarium
  - Actors
    - Logged in User

## Test Data

#### Requirement:Users should only be able to interact with resources they have added to the Planetarium

| User   | Resources        |
| ------ | ---------------- |
| Batman | Provided already |
| Joker  | None (new user)  |

#### Requirement: Planets should be “owned” by the user that added it to the Planetarium

| User/Owner | Planets owned by User | Planets not owned by User |
| ---------- | --------------------- | ------------------------- |
| Batman     | Earth, Mars           | Jupiter                   |
| Spiderman  | Jupiter               | Earth, Mars               |

### Acceptance Testing Data

#### Environment Data

- Browser: Edge
- Operating System: Windows 10
- Version of Planetarium: 1.0
- Background Data:
  - Login Page for Planetarium: http://localhost:8080/

## Test Scenarios

### Decision Table for Deletion Criteria

| Drop-down button | Name           | Result                                        |
| ---------------- | -------------- | --------------------------------------------- |
| Planet           |                | Error(provide a name) and stay on Home page   |
| Planet           | Name of Planet | Refreshed and updated Home page               |
| Planet           | Name of Moon   | Error(Wrong Name/Type ) and stay on Home page |
| Moon             | Name of Planet | Error(Wrong Name/Type ) and stay on Home page |

## Parameterized Test scenario

| Step                               | Actor          | Data                              | Result                           |
| ---------------------------------- | -------------- | --------------------------------- | -------------------------------- |
| given the user is on the home page | Logged in User | http://localhost:8080/planetarium | Home page with list of resources |

| User provides resources' valid name and type | User | Names of Planet/Moon | Refreshed and Updated Home Page |

### Use Case Id: 6

- Description: Users should be able to add Moons to the Planetarium associated with a Planet
  -Actors
  -Logged in User

## Test Data

#### Requirement: Moons should be “owned” by the Planet the User adding the moon associated it with

| Planet names | Moon names |
| ------------ | ---------- |
| Earth        | Luna       |
| Mars         | Titan      |

#### Requirement: Planet and Moon names should not have more than 30 characters

| 0 character Planet name | 30 characters Planet name       | 31 characters Planet name        |
| ----------------------- | ------------------------------- | -------------------------------- |
|                         | ThisIsAPlanetWith30characters01 | ThisIsAPlanetWith31characters022 |

| 0 character Moon name | 30 characters Moon name        | 31 characters Moon name         |
| --------------------- | ------------------------------ | ------------------------------- |
|                       | ThisIsAMoonWith30characters011 | ThisIsAMoonWith31characters0212 |

#### Requirement: Planets and Moons should allow adding an associated image, but it is not required for the data to be added to the database

| Photo        | Name   | Result                 | Redirect                                   |
| ------------ | ------ | ---------------------- | ------------------------------------------ |
| Saturn photo | Saturn | Photo and Planet added | Refreshed Home Page                        |
| Saturn Photo |        | Not Added              | Need names of planet to be added           |
|              | Saturn | Planet adedd           | Refreshed Home Page with only name appears |

| Moon Photo | Moon Name | Result               | Redirect                                   |
| ---------- | --------- | -------------------- | ------------------------------------------ |
| Luna photo | Luna      | Photo and Moon added | Refreshed Home Page                        |
| Luna Photo |           | Not Added            | Need names of moon to be added             |
|            | Luna      | Planet adedd         | Refreshed Home Page with only name appears |

### Acceptance Testing Data

#### Environment Data

- Browser: Edge
- Operating System: Windows 10
- Version of Planetarium: 1.0
- Background Data:
  - Login Page for Planetarium: http://localhost:8080/

## Test Scenarios

### Decision Table for moons should be owned by the Planet the User adding the moon associated it with

| Planet name | Moon name |
| ----------- | --------- |
| Earth       | Luna      |
| Mars        | Titan     |

### Decision Table for Moon's Character Length Limit

| Planet Name                      | Moon Name                       | Action Addition result | Redirect                              |
| -------------------------------- | ------------------------------- | ---------------------- | ------------------------------------- |
|                                  |                                 | Nothing added          | Stay on home page                     |
|                                  | ThisIsAMoonWith30characters011  | nothing added          | Stay on home page                     |
|                                  | ThisIsAMoonWith31characters0212 | Nothing Added          | Stay on Home Page                     |
| ThisIsAPlanetWith30characters01  |                                 | Planet Added           | Refreshed home page with updated list |
| ThisIsAPlanetWith30characters01  | ThisIsAMoonWith30characters011  | Planet and Moon Added  | Refreshed home page with updated list |
| ThisIsAPlanetWith30characters01  | ThisIsAMoonWith31characters0212 | Nothing Added          | Stay on Home Page                     |
| ThisIsAPlanetWith31characters022 |                                 | Nothing Added          | Stay on Home Page                     |
| ThisIsAPlanetWith31characters022 | ThisIsAMoonWith30characters011  | Nothing added          | Stay on Home page                     |
| ThisIsAPlanetWith31characters022 | ThisIsAMoonWith31characters0212 | Nothing added          | Stay on Home page                     |

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

## Test Data

#### Requirement: Moons should be “owned” by the Planet the User adding the moon associated it with

| Planets | Moon owned |
| ------- | ---------- |
| Earth   | Luna       |
| Mars    | Titan      |

#### Requirement: Users should only be able to interact with resources they have added to the Planetarium

    - Exploratory and error guess testing to see if you can acces other user's resources

### Acceptance Testing Data

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

| Step                                            | Actor | Data                              | Result                     |
| ----------------------------------------------- | ----- | --------------------------------- | -------------------------- |
| given the user is on the home page              | User  | http://localhost:8080/planetarium |                            |
| user selects moon and valid moon name/planetId/ | User  |                                   | Page refreshed and Updated |
| Moon deleted                                    | User  |                                   | Page refreshed             |
