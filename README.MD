# TEST APP

This is test app. Your task is to write a set of automated test for it using **pytest** framework.
App is definitely contain bugs. Some of them are meant to be there while some might be a result of my bad coding skills...
Let's see how many of them you'll be able to find, with automated tests obviously=)

## App spec

Test app allow user to upload templates and then render a simple web page using this template.
Rendered page will contain buttons with the links provided. 
Web page is available on *localhost:5000/* after app is launched.

App should be started in docker using

    docker build --tag test_app:latest .
    
    docker run -p 5000:5000 -d test_app:latest

Template should be a list of blocks:

     -  id: {Element id. Mandatory}
        label: {Button label. Mandatory}
        link: {Web link. Optional}
        depends: {Id of parrent element. Optional}
        
### Constraints

- Each element should have id and label
- Id should be unique
- If link is not set for element button is rendered as disabled
- Parent element should be present in list of elements
- Buttons on the rendered page should be clickable except case with no link provided

### API spec

####Upload template

  Upload your template file

* **URL**

  /api/v1/templates

* **Method:**

  `PUT`
  
*  **URL Params**

   **Required:**
 
   `id=[integer]`

* **Data Params**

  Content-type: Form-data
    
    **Required:**
 
   `file=[file]`
   
    **Optional:**
 
   `data=[json]`
   
   ex:
   
   `deta={"tmpl_id":"my_custom_id"}`
   
####List templates

  List all currently uploaded templates

* **URL**

  /api/v1/templates

* **Method:**

  `GET`

####Delete template

  Delete previously loaded template file

* **URL**

  /api/v1/templates/:tmpl_id

* **Method:**

  `DELETE`
  
*  **URL Params**

   **Required:**
 
   `tmpl_id=[string]`
   
####Install template

  Install previously loaded template file

* **URL**

  /api/v1/templates/:tmpl_id/install

* **Method:**

  `POST`
  
*  **URL Params**

   **Required:**
 
   `tmpl_id=[string]`