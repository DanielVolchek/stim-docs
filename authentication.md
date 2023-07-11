# Authentication Flow

Diagram [[authentication.excalidraw|here]]

Authentication flow works in the following way

## Register

when a user [[api/core/register|registers]] for the service the following events occur
-  a request is made to /core/user/register 
- check if the password passes server-side checks
	- we also want to check this on client first
	 I would like to add a [[show password]] icon to the login #todo
- Core POSTs email, username, password to [[api/db/user/register|db/user/register]]
- db/user/register checks
	- does the email exist
	- does the username exist
	- does the password fail checks
-  if any are true, request fails
- otherwise
- request POSTs to [[api/email/register]]
## Login

When a user [[api/core/login|logs in]] 