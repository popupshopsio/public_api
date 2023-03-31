# Popable Public API Documentation
Contained here are the info and details necessary to functionally use the Popable API. If you have questions, please reach out to support @ Popable . com


# ENDPOINT
https://popable.com/wp-json/pop/v1/manage_space

HTTP Method: Post


# AUTHENTICATION
Popable will enable API access on a per-user basis. 

When actiavted, we will provide an API key that is required for all calls.


# JSON OBJECT TO SEND
In the body of your request, the JSON opject should follow this format:

## JSON OBJECT
|Parameter Name|Type  |Required|Description                       |Options|
|--------------|------|--------|----------------------------------|-------|
|user_email    |string|Yes     |The email address of the user     |       |
|api_key       |string|Yes     |The API key assigned to user_email|       |
|data          |object|Yes     |See Data table                    |       |


### data

|Parameter Name         |Type   |Required                                 |Description                                                                                                                 |Options                                                                                                                                                                        |
|-----------------------|-------|-----------------------------------------|----------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|action                 |string |Yes                                      |The action to be performed                                                                                                  |add / update / delete                                                                                                                                                          |
|property_id            |integer|Required on actions: ‘update’ and ‘delete|The Popable ID of the property                                                                                              |                                                                                                                                                                               |
|status                 |string |Required on actions: ‘add’ and ‘update’  |The status of the space.                                                                                                    |archived / inactive / public / private                                                                                                                                         |
|name_for_listing       |string |Yes                                      |The name of the property as it will appear in listings                                                                      |                                                                                                                                                                               |
|address                |string |Yes                                      |The street address of the property                                                                                          |                                                                                                                                                                               |
|type_of_property       |string |Yes                                      |The type(s) of property. Separated with a vertical pipe &#124;                                                                   |Shopping Center – Power&#124;Shopping Center – Strip&#124;Shopping Center – Open Air&#124;Shopping Center – Lifestyle&#124;Mall&#124;Event Space&#124;Pop-up Collective&#124;Retail Space&#124;Restaurant&#124;Outdoor Space|
|available_spaces       |array  |Yes                                      |An array of available spaces in the property                                                                                |See the available_spaces Table                                                                                                                                                 |
|logo                   |string |Yes                                      |The URL of the image file for the logo of the property. Images should be square.                                            |                                                                                                                                                                               |
|top_image              |string |Yes                                      |The URL of the image file for the top image for the property. Best is 1500px X 500px                                        |                                                                                                                                                                               |
|long_description       |string |Yes                                      |A long description of the property. Can include html formatting if passed via htmlspecialchars_encode()                     |                                                                                                                                                                               |
|short_description      |string |No                                       |A short description of the property                                                                                         |                                                                                                                                                                               |
|info_packet            |string |No                                       |The URL of the pdf file of information about the property                                                                   |                                                                                                                                                                               |
|diagram                |string |No                                       |The URL of the pdf file of a diagram of the property                                                                        |                                                                                                                                                                               |
|site_plan              |string |No                                       |The URL of the pdf file of a site plan of the property                                                                      |                                                                                                                                                                               |
|photos                 |string |No                                       |The URL(s) of the image(s) file for a gallery of the property. Separated with a vertical pipe &#124;                             |                                                                                                                                                                               |
|website                |string |No                                       |The website URL of the property. Include "https://…"                                                                        |                                                                                                                                                                               |
|website_button_text    |string |No                                       |The text displayed on the button linking to the property's website. Default: View Website                                   |                                                                                                                                                                               |
|video_source           |string |No                                       |The source of the video.                                                                                                    |youtube, vimeo, or facebook                                                                                                                                                    |
|video_orientation      |string |No                                       |The orientation of the video                                                                                                |horizontal or vertical                                                                                                                                                         |
|video_url              |string |No                                       |The URL of the video. Include "https://…"                                                                                   |                                                                                                                                                                               |
|available_lease_lengths|string |No                                       |The available lease lengths for the property. Separated with a vertical pipe &#124;                                              |Day&#124;Weekend&#124;Week&#124;Month&#124;Long-Term                                                                                                                                               |
|median_age             |float  |No                                       |The median age of the population near the property                                                                          |                                                                                                                                                                               |
|population             |float  |No                                       |The population near the property                                                                                            |                                                                                                                                                                               |
|average_hh_income      |float  |No                                       |The average household income near the property                                                                              |                                                                                                                                                                               |
|key_tenants_tenant     |string |No                                       |The key tenants for the property. Separated with a vertical pipe &#124;                                                          |                                                                                                                                                                               |
|editing_users          |string |No                                       |The email address of existing users who are allowed to edit the property. Separated with a vertical pipe &#124;                  |                                                                                                                                                                               |
|messaging_users        |string |No                                       |The email address of existing users who will receive emails of messages to the property. Separated with a vertical pipe &#124;   |                                                                                                                                                                               |
|popable_mantch_users   |string |No                                       |The email address of existing users who will receive Popable Match emails for the property. Separated with a vertical pipe &#124;|                                                                                                                                                                               |

### available_spaces

|Parameter Name|Type   |Required|Description                                                                                 |Options                                              |
|--------------|-------|--------|--------------------------------------------------------------------------------------------|-----------------------------------------------------|
|suite         |string |Yes     |The name of the available space or suite                                                    |                                                     |
|space_type    |string |Yes     |The type of space available                                                                 |common, inline, kiosk, restaurant, outdoors, or other|
|gla           |integer|Yes     |The Gross Leasable Area (GLA) of the available space                                        |                                                     |
|gallery       |string |No      |The URL(s) of the image(s) file for a gallery of the space. Separated with a vertical pipe &#124;|                                                     |
|video_url     |string |No      |The URL of the video. Include "https://…"                                                   |                                                     |
|embed_360     |string |No      |The embed code for a 360-degree view of the available space                                 |                                                     |
|apply_link    |string |No      |The URL for applying for the available space                                                |                                                     |
