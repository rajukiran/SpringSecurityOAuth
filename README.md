# SpringSecurityOAuth
Spring security using oauth authentication.

#Endpoints and their purpose
Attempt to access resources [REST API] without any authorization [will fail of-course].
GET http://localhost:8080/SpringSecurityOAuth2Example/user/
Ask for tokens[access+refresh] using HTTP POST on /oauth/token, with grant_type=password,and resource owners credentials as req-params. Additionally, send client credentials in Authorization header.
POST http://localhost:8080/SpringSecurityOAuth2Example/oauth/token?grant_type=password&username=bill&password=abc123

Ask for a new access token via valid refresh-token, using HTTP POST on /oauth/token, with grant_type=refresh_token,and sending actual refresh token. Additionally, send client credentials in Authorization header.
POST http://localhost:8080/SpringSecurityOAuth2Example/oauth/token?grant_type=refresh_token&refresh_token=094b7d23-973f-4cc1-83ad-8ffd43de1845

Access the resource by providing an access token using access_token query param with request.
GET http://localhost:8080/SpringSecurityOAuth2Example/user/?access_token=3525d0e4-d881-49e7-9f91-bcfd18259109

#Let's dive into usage
1. Let’s get the tokens. First add an authorization header with client credentials [my-trusted-client/secret].
2. Click on update request, verify the header in header-tab.
3. Send the Post request, you should receive the response containing access-token as well as refresh-token.
4. Save these tokens somewhere, you will need them. Now you can use this access-token [valid for 2 minutes] to access resources.
5. After 2 minutes, access-token gets expired, your further resource requests will fail.
6. We need a new access-token. Fire a post to with refresh-token to get a brand-new access-token.
7. Use this new access-token to access the resources.
8. Refresh-token expires too[10 minutes]. After that, you should see your refresh request getting failed.
9. It means you need to request a new refresh+access-token, as in step 2.
