# Postman Demo for GK 
#### HENRY CHAMPION
How I set up my postman-jenkins API testing framework
_____

Prerequisites:
- Jenkins installed on localhost:8080
- Collection.JSON file exported from a Postman collection: 
    - here all my test scripts are contained that run before/after the endpoints of the API have been called.
- newman installed under npm

Once all this was set, I headed to my localhost:8080 jenkins dashboard and created a new item:
- Name: postman_test1 > select 'freestyle project' > OK.
- then on next screen under the 'Build' tab, select 'Execute Windows batch command'
- Specify Execute Windows batch command as follows: 
    
    
      cd C:\git projects\postman-newman-jenkins\postman_demo
      C:\Users\User\AppData\Roaming\npm\newman run GK_postman_collection.postman_collection.json

- now, for some reason my jenkins was refusing to locate newman therefore the hardcoded: 

    
        C:\Users\User\AppData\Roaming\npm\newman
        
        
- next step is to click 'Build Now' under your newly created job.
- once this is clicked it should now run the newman command which should execute the API tests.
- you can find the output under the 'Console output' tab of your build. (tip: use 'View as plain text')
- here , mine shows the following: 

        Started by user Henry
        Running as SYSTEM
        Building in workspace C:\Windows\system32\config\systemprofile\AppData\Local\Jenkins.jenkins\workspace\postman_test1
        [postman_test1] $ cmd /c call C:\Windows\TEMP\jenkins1050755456342116460.bat
        
        C:\Windows\system32\config\systemprofile\AppData\Local\Jenkins.jenkins\workspace\postman_test1>cd C:\git projects\postman-newman-jenkins\postman_demo 
        
        C:\git projects\postman-newman-jenkins\postman_demo>C:\Users\User\AppData\Roaming\npm\newman run GK_postman_collection.postman_collection.json 
        newman
        
        GK_postman_collection
        
        □ GETS
        └ GET USERS
          ┌
          │ 'welcome to my jenkins + postman test automation build
          │ '
          │ 'Connecting to API at URL: https://reqres.in'
          └
          GET https://reqres.in/api/users?page=1 [200 OK, 1.88KB, 515ms]
          √  Check that GET USER request response code was 200
          √  Check that GET USER request response time was below 2 seconds
          √  Test to confirm that Janet Weaver's user profile is contained within the GET USER request response body
          ┌
          │ 'Users from response:'
          │ [
          │   {
          │     id: 1,
          │     email: 'george.bluth@reqres.in',
          │     first_name: 'George',
          │     last_name: 'Bluth',
          │     avatar: 'https://s3.amazonaws.com/uifaces/faces/tw
          │ itter/calebogden/128.jpg'
          │   },
          │   {
          │     id: 2,
          │     email: 'janet.weaver@reqres.in',
          │     first_name: 'Janet',
          │     last_name: 'Weaver',
          │     avatar: 'https://s3.amazonaws.com/uifaces/faces/tw
          │ itter/josephstein/128.jpg'
          │   },
          │   {
          │     id: 3,
          │     email: 'emma.wong@reqres.in',
          │     first_name: 'Emma',
          │     last_name: 'Wong',
          │     avatar: 'https://s3.amazonaws.com/uifaces/faces/tw
          │ itter/olegpogodaev/128.jpg'
          │   },
          │   {
          │     id: 4,
          │     email: 'eve.holt@reqres.in',
          │     first_name: 'Eve',
          │     last_name: 'Holt',
          │     avatar: 'https://s3.amazonaws.com/uifaces/faces/tw
          │ itter/marcoramires/128.jpg'
          │   },
          │   {
          │     id: 5,
          │     email: 'charles.morris@reqres.in',
          │     first_name: 'Charles',
          │     last_name: 'Morris',
          │     avatar: 'https://s3.amazonaws.com/uifaces/faces/tw
          │ itter/stephenmoon/128.jpg'
          │   },
          │   {
          │     id: 6,
          │     email: 'tracey.ramos@reqres.in',
          │     first_name: 'Tracey',
          │     last_name: 'Ramos',
          │     avatar: 'https://s3.amazonaws.com/uifaces/faces/tw
          │ itter/bigmancho/128.jpg'
          │   }
          │ ]
          └
        
        □ POSTS
        └ REGISTER USERS
          ┌
          │ 'This is a pre request script that sets the username a
          │ nd password variable to keep the test from failing'
          └
          POST https://reqres.in/api/register [200 OK, 521B, 371ms]
          ┌
          │ 'This should pass as the response is 200.'
          └
          √  Check that POST-REGISTER request response status was OK (200 response)
          ┌
          │ 'This test only runs when the test is successful. ( 20
          │ 0)'
          └
          √  Check that POST-REGISTER request response contained a token and a id for the new user
        
        └ REGISTER USERS FAIL
          POST https://reqres.in/api/register [400 Bad Request, 551B, 363ms]
          ┌
          │ 'This test should not pass as the response is 400: '
          └
          1. Check that request was OK (200 response)
          ┌
          │ 'This test only runs when the response is not successf
          │ ul. ( NOT OK)'
          └
          √  Check that the user is informed that 'Only defined users succeed registration' 
        
        ┌─────────────────────────┬────────────────────┬────────────────────┐
        │                         │           executed │             failed │
        ├─────────────────────────┼────────────────────┼────────────────────┤
        │              iterations │                  1 │                  0 │
        ├─────────────────────────┼────────────────────┼────────────────────┤
        │                requests │                  3 │                  0 │
        ├─────────────────────────┼────────────────────┼────────────────────┤
        │            test-scripts │                  7 │                  0 │
        ├─────────────────────────┼────────────────────┼────────────────────┤
        │      prerequest-scripts │                  7 │                  0 │
        ├─────────────────────────┼────────────────────┼────────────────────┤
        │              assertions │                  7 │                  1 │
        ├─────────────────────────┴────────────────────┴────────────────────┤
        │ total run duration: 1387ms                                        │
        ├───────────────────────────────────────────────────────────────────┤
        │ total data received: 1.28KB (approx)                              │
        ├───────────────────────────────────────────────────────────────────┤
        │ average response time: 416ms [min: 363ms, max: 515ms, s.d.: 69ms] │
        └───────────────────────────────────────────────────────────────────┘
        
          #  failure         detail                                                
                                                                                   
         1.  AssertionError  Check that request was OK (200 response)              
                             expected response to have status code 200 but got 400 
                             at assertion:0 in test-script                         
                             inside "POSTS / REGISTER USERS FAIL"                  
        Build step 'Execute Windows batch command' marked build as failure
        Finished: FAILURE
        
- as one can see , a summary is contained at the bottom showing a failure for the one assertion: where the response should have been 200.