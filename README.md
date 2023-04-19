# Popable Public API Documentation
Contained here are the info and details necessary to functionally use the Popable REST API. If you have questions, please reach out to support @ Popable . com

### Table of Contents
* [Endpoint Info](https://github.com/popupshopsio/public_api#endpoint)
* [Authentication](https://github.com/popupshopsio/public_api#authentication)
* [JSON object](https://github.com/popupshopsio/public_api#json-object-to-send)
  * [Object](https://github.com/popupshopsio/public_api#json-object)
  * [Data Table](https://github.com/popupshopsio/public_api#data)
  * [Available Spaces Table](https://github.com/popupshopsio/public_api#available_spaces)
* [Examples](https://github.com/popupshopsio/public_api#examples)
  * [Add a Property](https://github.com/popupshopsio/public_api#add-a-property)
  * [Update a Property](https://github.com/popupshopsio/public_api#update-a-property)
  * [Delete a Property](https://github.com/popupshopsio/public_api#delete-a-property)
  * [Delete multiple Properties](https://github.com/popupshopsio/public_api#delete-several-properties)
* [Returns](https://github.com/popupshopsio/public_api#return)
  * [Return Codes](https://github.com/popupshopsio/public_api#return-codes)


# ENDPOINT
https://popable.com/wp-json/pop/v1/manage_space

HTTP Method: Post


# AUTHENTICATION
Popable will enable API access on a per-user basis. 
When activated, we will provide an API key that is required for all calls.


# JSON OBJECT TO SEND
In the body of your request, the JSON opject should follow this format:


## JSON OBJECT
|Parameter Name|Type  |Required|Description                       |Options|
|--------------|------|--------|----------------------------------|-------|
|user_email    |string|Yes     |The email address of the user     |       |
|api_key       |string|Yes     |The API key assigned to user_email|       |
|data          |object|Yes     |[See the `data` table](https://github.com/popupshopsio/public_api#data).                    |       |


### data
**note:** while several properties can be managed on a single call, we request a single property per call. Timeout for the call is 60 seconds. Exceeding this will produce a 524 connection error.

|Parameter Name         |Type   |Required                                 |Description                                                                                                                 |Options                                                                                                                                                                        |
|-----------------------|-------|-----------------------------------------|----------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|action                 |string |Yes                                      |The action to be performed                                                                                                  |add / update / delete                                                                                                                                                          |
|property_id            |integer|Required on actions: ‘update’ and ‘delete|The Popable ID of the property                                                                                              |                                                                                                                                                                               |
|status                 |string |Required on actions: ‘add’ and ‘update’  |The status of the space.                                                                                                    |archived / inactive / public / private                                                                                                                                         |
|name_for_listing       |string |Yes                                      |The name of the property as it will appear in listings                                                                      |                                                                                                                                                                               |
|address                |string |Yes                                      |The street address of the property                                                                                          |                                                                                                                                                                               |
|type_of_property       |string |Yes                                      |The type(s) of property. Separated with a vertical pipe &#124;                                                                   |Shopping Center – Power&#124;Shopping Center – Strip&#124;Shopping Center – Open Air&#124;Shopping Center – Lifestyle&#124;Mall&#124;Event Space&#124;Pop-up Collective&#124;Retail Space&#124;Restaurant&#124;Outdoor Space|
|available_spaces       |array  |Yes                                      |An array of available spaces in the property                                                                                |[See the `available_spaces` Table](https://github.com/popupshopsio/public_api#available_spaces).                                                                                                                                              |
|logo                   |string |Yes                                      |The URL of the image file for the logo of the property. Images should be square.                                            |                                                                                                                                                                               |
|top_image              |string |Yes                                      |The URL of the image file for the top image for the property. Best is 1500px X 500px                                        |                                                                                                                                                                               |
|long_description       |string |Yes                                      |A long description of the property. Can include html, but the HTML entities need to be encoded/escaped. Example: Replace `<` with `&lt;`. In PHP `htmlspecialchars_encode()` is apropreiate.()                     |                                                                                                                                                                               |
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
|owner_user          |string |No                                       |The email address of existing user who will be primary owner of property.                   |                                                                                                                                                                               |
|editing_users          |string |No                                       |The email address(es) of existing users who are allowed to edit the property. Separated with a vertical pipe &#124;                  |                                                                                                                                                                               |
|messaging_users        |string |No                                       |The email address(es) of existing users who will receive emails of messages to the property. Separated with a vertical pipe &#124;   |                                                                                                                                                                               |
|popable_match_users   |string |No                                       |The email address(es) of existing users who will receive Popable Match emails for the property. Separated with a vertical pipe &#124;|                                                                                                                                                                               |

### available_spaces

|Parameter Name|Type   |Required|Description                                                                                 |Options                                              |
|--------------|-------|--------|--------------------------------------------------------------------------------------------|-----------------------------------------------------|
|suite         |string |Yes     |The name of the available space or suite                                                    |                                                     |
|space_type    |string |Yes     |The type of space available                                                                 |common, inline, kiosk, restaurant, outdoors, or other|
|gla           |integer|Yes     |The Gross Leasable Area (GLA) of the available space                                        |                                                     |
|gallery       |string |No      |The URL(s) of the image(s) file for a gallery of the space. Separated with a vertical pipe &#124;|                                                     |
|video_url     |string |No      |The URL of the video. Include "https://…"                                                   |                                                     |
|embed_360     |string |No      |The iFrame embed code for a 360-degree view of the available space. The HTML entities need to be encoded/escaped. Example: Replace `<` with `&lt;`. In PHP `htmlspecialchars_encode()` is apropreiate.                                |                                                     |
|apply_link    |string |No      |The URL for applying for the available space                                                |                                                     |

## Examples
### add a property
```json
{
    "user_email": "john@johndoe.com",
	"api_key": "***********",
    "data": [
        {
            "action": "add",
            "status": "public",
            "name_for_listing": "New Property Name",
            "address": "742 E Evergreen St, Springfield, MO 65803, USA",
            "type_of_property": "Mall|Shopping Center – Open Air",
            "available_spaces": [
                {
                    "suite": "GB2",
                    "space_type": "inline",
                    "gallery": "https://i.imgur.com/ZBvtxcw.jpeg|https://i.imgur.com/3H4jIhf.jpeg|https://i.imgur.com/sS3sGIv.jpeg",
                    "video_url": "https://vimeo.com/432723379",
                    "embed_360": "&lt;iframe src=&#039;https://www.google.com/maps/embed?pb=!4v1679349548762!6m8!1m7!1sCAoSLEFGMVFpcFBieDdaV3FHRWFIODBsTHMwSEFVNUQ4ZjJJOHBCalotV0ZyS1I2!2m2!1d29.7260481!2d-95.39058279999999!3f118.17964895712494!4f0!5f0.7820865974627469&#039; width=&#039;600&#039; height=&#039;450&#039; style=&#039;border:0&#039; allowfullscreen=&#039;&#039;&gt;&lt;/iframe&gt;",
                    "gla": "2400",
                    "apply_link": "https://google.com"
                },
                {
                    "suite": "FM2",
                    "space_type": "kiosk",
                    "gallery": "https://i.imgur.com/ZBvtxcw.jpeg|https://i.imgur.com/3H4jIhf.jpeg|https://i.imgur.com/sS3sGIv.jpeg",
                    "video_url": "https://vimeo.com/432723379",
                    "embed_360": "&lt;iframe src=&#039;https://www.google.com/maps/embed?pb=!4v1679349548762!6m8!1m7!1sCAoSLEFGMVFpcFBieDdaV3FHRWFIODBsTHMwSEFVNUQ4ZjJJOHBCalotV0ZyS1I2!2m2!1d29.7260481!2d-95.39058279999999!3f118.17964895712494!4f0!5f0.7820865974627469&#039; width=&#039;600&#039; height=&#039;450&#039; style=&#039;border:0&#039; allowfullscreen=&#039;&#039;&gt;&lt;/iframe&gt;",
                    "gla": "400",
                    "apply_link": "https://google.com"
                },
                {
                    "suite": "GB2",
                    "space_type": "inline",
                    "gallery": "https://i.imgur.com/ZBvtxcw.jpeg|https://i.imgur.com/3H4jIhf.jpeg|https://i.imgur.com/sS3sGIv.jpeg",
                    "video_url": "https://vimeo.com/432723379",
                    "embed_360": "&lt;iframe src=&#039;https://www.google.com/maps/embed?pb=!4v1679349548762!6m8!1m7!1sCAoSLEFGMVFpcFBieDdaV3FHRWFIODBsTHMwSEFVNUQ4ZjJJOHBCalotV0ZyS1I2!2m2!1d29.7260481!2d-95.39058279999999!3f118.17964895712494!4f0!5f0.7820865974627469&#039; width=&#039;600&#039; height=&#039;450&#039; style=&#039;border:0&#039; allowfullscreen=&#039;&#039;&gt;&lt;/iframe&gt;",
                    "gla": "2400",
                    "apply_link": "https://google.com"
                },
                {
                    "suite": "FM2",
                    "space_type": "kiosk",
                    "gallery": "https://i.imgur.com/ZBvtxcw.jpeg|https://i.imgur.com/3H4jIhf.jpeg|https://i.imgur.com/sS3sGIv.jpeg",
                    "video_url": "https://vimeo.com/432723379",
                    "embed_360": "&lt;iframe src=&#039;https://www.google.com/maps/embed?pb=!4v1679349548762!6m8!1m7!1sCAoSLEFGMVFpcFBieDdaV3FHRWFIODBsTHMwSEFVNUQ4ZjJJOHBCalotV0ZyS1I2!2m2!1d29.7260481!2d-95.39058279999999!3f118.17964895712494!4f0!5f0.7820865974627469&#039; width=&#039;600&#039; height=&#039;450&#039; style=&#039;border:0&#039; allowfullscreen=&#039;&#039;&gt;&lt;/iframe&gt;",
                    "gla": "400",
                    "apply_link": "https://google.com"
                },
                {
                    "suite": "GB2",
                    "space_type": "inline",
                    "gallery": "https://i.imgur.com/ZBvtxcw.jpeg|https://i.imgur.com/3H4jIhf.jpeg|https://i.imgur.com/sS3sGIv.jpeg",
                    "video_url": "https://vimeo.com/432723379",
                    "embed_360": "&lt;iframe src=&#039;https://www.google.com/maps/embed?pb=!4v1679349548762!6m8!1m7!1sCAoSLEFGMVFpcFBieDdaV3FHRWFIODBsTHMwSEFVNUQ4ZjJJOHBCalotV0ZyS1I2!2m2!1d29.7260481!2d-95.39058279999999!3f118.17964895712494!4f0!5f0.7820865974627469&#039; width=&#039;600&#039; height=&#039;450&#039; style=&#039;border:0&#039; allowfullscreen=&#039;&#039;&gt;&lt;/iframe&gt;",
                    "gla": "2400",
                    "apply_link": "https://google.com"
                },
                {
                    "suite": "FM2",
                    "space_type": "kiosk",
                    "gallery": "https://i.imgur.com/ZBvtxcw.jpeg|https://i.imgur.com/3H4jIhf.jpeg|https://i.imgur.com/sS3sGIv.jpeg",
                    "video_url": "https://vimeo.com/432723379",
                    "embed_360": "&lt;iframe src=&#039;https://www.google.com/maps/embed?pb=!4v1679349548762!6m8!1m7!1sCAoSLEFGMVFpcFBieDdaV3FHRWFIODBsTHMwSEFVNUQ4ZjJJOHBCalotV0ZyS1I2!2m2!1d29.7260481!2d-95.39058279999999!3f118.17964895712494!4f0!5f0.7820865974627469&#039; width=&#039;600&#039; height=&#039;450&#039; style=&#039;border:0&#039; allowfullscreen=&#039;&#039;&gt;&lt;/iframe&gt;",
                    "gla": "400",
                    "apply_link": "https://google.com"
                },
                {
                    "suite": "GB2",
                    "space_type": "inline",
                    "gallery": "https://i.imgur.com/ZBvtxcw.jpeg|https://i.imgur.com/3H4jIhf.jpeg|https://i.imgur.com/sS3sGIv.jpeg",
                    "video_url": "https://vimeo.com/432723379",
                    "embed_360": "&lt;iframe src=&#039;https://www.google.com/maps/embed?pb=!4v1679349548762!6m8!1m7!1sCAoSLEFGMVFpcFBieDdaV3FHRWFIODBsTHMwSEFVNUQ4ZjJJOHBCalotV0ZyS1I2!2m2!1d29.7260481!2d-95.39058279999999!3f118.17964895712494!4f0!5f0.7820865974627469&#039; width=&#039;600&#039; height=&#039;450&#039; style=&#039;border:0&#039; allowfullscreen=&#039;&#039;&gt;&lt;/iframe&gt;",
                    "gla": "2400",
                    "apply_link": "https://google.com"
                },
                {
                    "suite": "FM2",
                    "space_type": "kiosk",
                    "gallery": "https://i.imgur.com/ZBvtxcw.jpeg|https://i.imgur.com/3H4jIhf.jpeg|https://i.imgur.com/sS3sGIv.jpeg",
                    "video_url": "https://vimeo.com/432723379",
                    "embed_360": "&lt;iframe src=&#039;https://www.google.com/maps/embed?pb=!4v1679349548762!6m8!1m7!1sCAoSLEFGMVFpcFBieDdaV3FHRWFIODBsTHMwSEFVNUQ4ZjJJOHBCalotV0ZyS1I2!2m2!1d29.7260481!2d-95.39058279999999!3f118.17964895712494!4f0!5f0.7820865974627469&#039; width=&#039;600&#039; height=&#039;450&#039; style=&#039;border:0&#039; allowfullscreen=&#039;&#039;&gt;&lt;/iframe&gt;",
                    "gla": "400",
                    "apply_link": "https://google.com"
                }
            ],
            "logo": "https://i.imgur.com/3jWdoKW.jpeg",
            "top_image": "https://i.imgur.com/am2LQon.jpeg",
            "short_description": "Brief intro, your elevator pitch. 280 characters max.",
            "long_description": "&lt;h1&gt;This is a great property&lt;/h1&gt;&lt;p&gt;It is where you want to pop up! &lt;span style=&quot;text-transform:uppercase;&quot;&gt;Don&apos;t miss this opportunity&lt;/span&gt;&lt;br&gt;Message us today!&lt;/p&gt;",
            "info_packet": "https://www.nasa.gov/sites/default/files/atoms/files/nasa_graphics_manual_nhb_1430-2_jan_1976",
            "diagram": "https://www.nasa.gov/sites/default/files/atoms/files/nasa_graphics_manual_nhb_1430-2_jan_1976.pdf",
            "site_plan": "https://www.spacex.com/media/falcon-users-guide-2021-09.pdf",
            "photos": "https://i.imgur.com/ZBvtxcw.jpeg|https://i.imgur.com/3H4jIhf.jpeg|https://i.imgur.com/sS3sGIv.jpeg",
            "website": "https://google.com",
            "website_button_text": "View Website",
            "video_source": "vimeo",
            "video_orientation": "horizontal",
            "video_url": "https://vimeo.com/432723379",
            "available_lease_lengths": "Weekend|Week",
            "median_age": 32,
            "population": 1.2,
            "average_hh_income": 120000,
            "key_tenants_tenant": "Apple|Starbucks|Chick-Fil-A",
            "owner_user": "john@johndoe.com",
            "editing_users": "jane@johndoe.com",
            "messaging_users": "jane@johndoe.com|jack@johndoe.com",
            "popable_match_users": "jack@johndoe"
        }
    ]
}
```

### update a property
```json
{
    "user_email": "john@johndoe.com",
    "api_key": "***********",
    "data": [
        {
            "action": "update",
            "property_id": 132674,
            "status": "public",
            "name_for_listing": "Existing Property Name",
            "address": "742 E Evergreen St, Springfield, MO 65803, USA",
            "type_of_property": "Mall|Shopping Center – Open Air",
            "available_spaces": [
                {
                    "suite": "GB2",
                    "space_type": "inline",
                    "gallery": "https://i.imgur.com/ZBvtxcw.jpeg|https://i.imgur.com/3H4jIhf.jpeg|https://i.imgur.com/sS3sGIv.jpeg",
                    "video_url": "https://vimeo.com/432723379",
                    "embed_360": "&lt;iframe src=&#039;https://www.google.com/maps/embed?pb=!4v1679349548762!6m8!1m7!1sCAoSLEFGMVFpcFBieDdaV3FHRWFIODBsTHMwSEFVNUQ4ZjJJOHBCalotV0ZyS1I2!2m2!1d29.7260481!2d-95.39058279999999!3f118.17964895712494!4f0!5f0.7820865974627469&#039; width=&#039;600&#039; height=&#039;450&#039; style=&#039;border:0&#039; allowfullscreen=&#039;&#039;&gt;&lt;/iframe&gt;",
                    "gla": "2400",
                    "apply_link": "https://google.com"
                },
                {
                    "suite": "FM2",
                    "space_type": "kiosk",
                    "gallery": "https://i.imgur.com/ZBvtxcw.jpeg|https://i.imgur.com/3H4jIhf.jpeg|https://i.imgur.com/sS3sGIv.jpeg",
                    "video_url": "https://vimeo.com/432723379",
                    "embed_360": "&lt;iframe src=&#039;https://www.google.com/maps/embed?pb=!4v1679349548762!6m8!1m7!1sCAoSLEFGMVFpcFBieDdaV3FHRWFIODBsTHMwSEFVNUQ4ZjJJOHBCalotV0ZyS1I2!2m2!1d29.7260481!2d-95.39058279999999!3f118.17964895712494!4f0!5f0.7820865974627469&#039; width=&#039;600&#039; height=&#039;450&#039; style=&#039;border:0&#039; allowfullscreen=&#039;&#039;&gt;&lt;/iframe&gt;",
                    "gla": "400",
                    "apply_link": "https://google.com"
                },
                {
                    "suite": "GB2",
                    "space_type": "inline",
                    "gallery": "https://i.imgur.com/ZBvtxcw.jpeg|https://i.imgur.com/3H4jIhf.jpeg|https://i.imgur.com/sS3sGIv.jpeg",
                    "video_url": "https://vimeo.com/432723379",
                    "embed_360": "&lt;iframe src=&#039;https://www.google.com/maps/embed?pb=!4v1679349548762!6m8!1m7!1sCAoSLEFGMVFpcFBieDdaV3FHRWFIODBsTHMwSEFVNUQ4ZjJJOHBCalotV0ZyS1I2!2m2!1d29.7260481!2d-95.39058279999999!3f118.17964895712494!4f0!5f0.7820865974627469&#039; width=&#039;600&#039; height=&#039;450&#039; style=&#039;border:0&#039; allowfullscreen=&#039;&#039;&gt;&lt;/iframe&gt;",
                    "gla": "2400",
                    "apply_link": "https://google.com"
                },
                {
                    "suite": "FM2",
                    "space_type": "kiosk",
                    "gallery": "https://i.imgur.com/ZBvtxcw.jpeg|https://i.imgur.com/3H4jIhf.jpeg|https://i.imgur.com/sS3sGIv.jpeg",
                    "video_url": "https://vimeo.com/432723379",
                    "embed_360": "&lt;iframe src=&#039;https://www.google.com/maps/embed?pb=!4v1679349548762!6m8!1m7!1sCAoSLEFGMVFpcFBieDdaV3FHRWFIODBsTHMwSEFVNUQ4ZjJJOHBCalotV0ZyS1I2!2m2!1d29.7260481!2d-95.39058279999999!3f118.17964895712494!4f0!5f0.7820865974627469&#039; width=&#039;600&#039; height=&#039;450&#039; style=&#039;border:0&#039; allowfullscreen=&#039;&#039;&gt;&lt;/iframe&gt;",
                    "gla": "400",
                    "apply_link": "https://google.com"
                },
                {
                    "suite": "GB2",
                    "space_type": "inline",
                    "gallery": "https://i.imgur.com/ZBvtxcw.jpeg|https://i.imgur.com/3H4jIhf.jpeg|https://i.imgur.com/sS3sGIv.jpeg",
                    "video_url": "https://vimeo.com/432723379",
                    "embed_360": "&lt;iframe src=&#039;https://www.google.com/maps/embed?pb=!4v1679349548762!6m8!1m7!1sCAoSLEFGMVFpcFBieDdaV3FHRWFIODBsTHMwSEFVNUQ4ZjJJOHBCalotV0ZyS1I2!2m2!1d29.7260481!2d-95.39058279999999!3f118.17964895712494!4f0!5f0.7820865974627469&#039; width=&#039;600&#039; height=&#039;450&#039; style=&#039;border:0&#039; allowfullscreen=&#039;&#039;&gt;&lt;/iframe&gt;",
                    "gla": "2400",
                    "apply_link": "https://google.com"
                },
                {
                    "suite": "FM2",
                    "space_type": "kiosk",
                    "gallery": "https://i.imgur.com/ZBvtxcw.jpeg|https://i.imgur.com/3H4jIhf.jpeg|https://i.imgur.com/sS3sGIv.jpeg",
                    "video_url": "https://vimeo.com/432723379",
                    "embed_360": "&lt;iframe src=&#039;https://www.google.com/maps/embed?pb=!4v1679349548762!6m8!1m7!1sCAoSLEFGMVFpcFBieDdaV3FHRWFIODBsTHMwSEFVNUQ4ZjJJOHBCalotV0ZyS1I2!2m2!1d29.7260481!2d-95.39058279999999!3f118.17964895712494!4f0!5f0.7820865974627469&#039; width=&#039;600&#039; height=&#039;450&#039; style=&#039;border:0&#039; allowfullscreen=&#039;&#039;&gt;&lt;/iframe&gt;",
                    "gla": "400",
                    "apply_link": "https://google.com"
                }
            ],
            "logo": "https://i.imgur.com/3jWdoKW.jpeg",
            "top_image": "https://i.imgur.com/am2LQon.jpeg",
            "short_description": "Brief intro, your elevator pitch. 280 characters max.",
            "long_description": "&lt;h1&gt;This is a great property&lt;/h1&gt;&lt;p&gt;It is where you want to pop up! &lt;span style=&quot;text-transform:uppercase;&quot;&gt;Don&apos;t miss this opportunity&lt;/span&gt;&lt;br&gt;Message us today!&lt;/p&gt;",
            "info_packet": "https://www.nasa.gov/sites/default/files/atoms/files/nasa_graphics_manual_nhb_1430-2_jan_1976.pdf",
            "diagram": "https://www.nasa.gov/sites/default/files/atoms/files/nasa_graphics_manual_nhb_1430-2_jan_1976.pdf",
            "site_plan": "https://www.spacex.com/media/falcon-users-guide-2021-09.pdf",
            "photos": "https://i.imgur.com/ZBvtxcw.jpeg|https://i.imgur.com/3H4jIhf.jpeg|https://i.imgur.com/sS3sGIv.jpeg",
            "website": "https://google.com",
            "website_button_text": "View Website",
            "video_source": "vimeo",
            "video_orientation": "horizontal",
            "video_url": "https://vimeo.com/432723379",
            "available_lease_lengths": "Weekend|Week",
            "median_age": 32,
            "population": 1.2,
            "average_hh_income": 120000,
            "key_tenants_tenant": "Apple|Starbucks|Chick-Fil-A",
            "owner_user": "john@johndoe.com",
            "editing_users": "jane@johndoe.com",
            "messaging_users": "jane@johndoe.com|jack@johndoe.com",
            "popable_match_users": "jack@johndoe"
        }
    ]
}
```

### delete a property
```json
{
    "user_email": "john@johndoe.com",
    "api_key": "***********",
    "data": [
        {
            "action": "delete",
            "property_id": "1234567"
        }
    ]
}
```

### delete several properties
```json
{
    "user_email": "john@johndoe.com",
    "api_key": "***********",
    "data": [
        {
            "action": "delete",
            "property_id": "1234567"
        },
		{
            "action": "delete",
            "property_id": "87654321"
        },
		{
            "action": "delete",
            "property_id": "56784321"
        }
    ]
}
```

## Return
This is what can be expected on the return.
Please be sure to save the `property_id` so that future `update` or `delete` calls can be made against that property.

### Successful `add` call return
```json
[
    {
        "ret_code": 701,
        "property_id": 2345678,
        "response": "added with errors",
        "property_url": "https://popable.com/space/new-property-name/",
        "errors": [
            {
                "property_id": 2345678,
                "error": "error saving 'info_packet'"
            }
        ]
    }
]
```

### Successful `update` call return
```json
[
    {
        "ret_code": 710,
        "property_id": "3456789",
        "response": "update Success",
        "property_url": "https://popable.com/space/existing-property-name/"
    }
]
```



### Successful `delete` call return
```json
[
    {
        "ret_code": 400,
        "property_id": "1234567",
        "error_msg": "'property_id' provided does not exist: 1234567"
    }
]
```
### Return Codes
|Action        |Result             |ret_code|
|--------------|-------------------|--------|
|Authenticaiton|Failed             |401     |
|add           |Success            |700     |
|add           |Success with errors|701     |
|add           |Failed             |400     |
|update        |Success            |710     |
|update        |Success with errors|711     |
|update        |Failed             |400     |
|delete        |Success            |720     |
|delete        |Failed             |400     |
