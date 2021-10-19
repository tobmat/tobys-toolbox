# Setup STS

STS enables you to assume a role and it's access with another user and role. Our current use case allows us to run ansible aws modules on another instance that doesn't have aws credentials.

**For one role to assume another:**

1. create role you want to be able to assume
2. give role access it needs
3. create trust with role that needs to assume it

Example: see ansible-sts

For User to assume ansible-sts role (Using ansible-service user as example):

1. create trust with ansible-service user from ansible-sts role
2. add ansible-service user to tower creds
3. include ansible-service creds on template where sts assume is needed
