# Coding Standards

## CLI Arguments
The command line flags -h & -v should always be implemented.

| Argument Flag | Meaning                       |
|---------------|-------------------------------|
| -h/--help     | Display help information      |
| -v/--version  | Display version information   |
| -V/--verbose  | Enable verbose output         |
| -L/--log      | Set the log level to use      |

## Log Levels
### CRITICAL
  **Description:** Reserved for when an unrecoverable error has occured that stops the application from running
  **Example:**
    A required library, module or resource file is missing
    An unknown exception occurs which is raised to the main method of an application

### ERROR
  **Description:** A recoverable error has occured that stops the process from functioning as intended
  **Example:**
    On a client, the user fails to authenticate successfully
    A network socket failed to connect to a server

### WARNING
  **Description:** A recoverable error has occured that does not stop the process from functioning as intended
  **Example:**
    On a server, a user fails to authenticate successfully
    When information provided by the user is invalid and the user can be prompted for new information

### INFO
  **Description:** High level information regarding what is happening in an application, should be use sparingly within loops
  **Example:**
    Listing resources that are being loaded and processed
    The child pid when fork() is used

### DEBUG
  **Description:** Low level information regarding what is happening in an application including the values of variables, this may be used more frequently within loops
  **Example:**
    Printing identifying information for threads that are spawned
    Printing the value of arguments that are passed into functions
