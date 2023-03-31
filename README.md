# Popable Public API Documentation
Contained here are the info and details necessary to functionally use the Popable API. If you have questions, please reach out to support @ Popable . com

***
# ENDPOINT
https://popable.com/wp-json/pop/v1/manage_space

HTTP Method: Post

***
# AUTHENTICATION
Popable will enable API access on a per-user basis. When actiavted, we will provide an API key that is required for all calls.

***
# JSON OBJECT TO SEND
In the body of your request, the JSON opject should follow this format:
|Parameter Name|Type  |Required|Description                       |Options|
|--------------|------|--------|----------------------------------|-------|
|user_email    |string|Yes     |The email address of the user     |       |
|api_key       |string|Yes     |The API key assigned to user_email|       |
|data          |object|Yes     |See Data table                    |       |
