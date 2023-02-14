## Проверить всё ли нормально в работе связки веб-сервисов.
### Есть 2 WS:
- WS_1: http://162.55.220.72:5031
- WS_2: http://23.88.52.139:5032
### GET. http://162.55.220.72:5031/jobs_count
- WS_1 получает запрос от клиента.
- Никаких параметров не нужно.
- WS_1 отправляет запрос на WS_2 - http://23.88.52.139:5032/get_jobs_count.
- WS_2 получает запрос от WS_1.
- WS_2 парсит json, в которой 7 вакансий и считает количество вакансий. По умолчанию в json 7 вакансий.
- WS_2 отправляет ответ на WS_1 в котором будет json:
```js 
{"jobs_count": 7}
```
- WS_1 получает ответ от WS_2 и отправляет json {“jobs_count”:7} клиенту.
### GET. http://162.55.220.72:5031/all_jobs
- WS_1 получает запрос от клиента.
- Никаких параметров не нужно.
- WS_1 отправляет запрос на WS_2.
- WS_2 получает запрос от WS_1.
- WS_2 парсит json, в которой 7 вакансий и считает количество вакансий. По умолчанию в json 7 вакансий.
- WS_2 отправляет ответ на WS_1 в котором будет json + все добавленные пользователем вакансии.
- WS_1 получает ответ от WS_2 и отправляет json клиенту.
### POST. http://162.55.220.72:5031/add_job
- WS_1 получает запрос от клиента в теле которого должна быть json-ка:
```js 
{   "firm_title": "firm_title",
   "position_title": "position_title",
   "skills": ["skill_1", "skill_2", "skill_3"],
   "description": "description",
   "Job Posting": "job_posting",
   "Employee Status": "employee_status"
}
```
- WS_1 отправляет запрос на WS_2 - http://23.88.52.139:5032/add_job_item
- В теле запроса должен быть json полученный от клиента.
 ```js 
{   "firm_title": "firm_title",
   "position_title": "position_title",
   "skills": ["skill_1", "skill_2", "skill_3"],
   "description": "description",
   "Job Posting": "job_posting",
   "Employee Status": "employee_status"
}
```
- WS_2 получает запрос от WS_1.
- WS_2 парсит json, в которой 7 вакансий и считает количество вакансий. По умолчанию в json 7 вакансий.
- WS_2 добавляет в json присланную из WS_1 json.
- У добавленной вакансии будет id = +1 к общему количеству вакансий в json (n+1)
- WS_2 отправляет ответ на WS_1 в котором будет json
 ```js 
 {"result_message":"Job added. Job id is 8",
"check_message": "call /all_jobs endpoint for checking."}
 ```
 ## *Решение*
 ### 1. Отправить запрос GET. http://162.55.220.72:5031/jobs_count
  ```js
 Response:
 {"jobs_count": 298}
  ```
 ### 2. Отправить запрос GET. http://23.88.52.139:5032/get_jobs_count
 ```js
 Response:
 {"jobs_count": 298}
  ```
 ### 3. Отправить запрос GET. http://162.55.220.72:5031/all_jobs
 ```js
Response:
{
    "1": {
        "Employee Status": "Full-time",
        "Job Posting": "Aug 02 2022",
        "description": "Experience with Functional Testing, including Regression Testing, Integration Testing, and API Testing. Experience with creating and executing test scripts. Experience testing developments against wireframes and style guide. Experience with systems, integration, and user acceptance testing. Experience in working with offshore /onsite Model",
        "firm_title": "Cognizant Technology Solutions",
        "position_title": "QA Functional Tester",
        "skills": [
            "postman",
            "js",
            "client_server",
            "api_testing"
        ]
    },
    "10": {
        "Employee Status": "full-time",
        "Job Posting": " ",
        "description": "Good Job",
        "firm_title": "Acosoft",
        "position_title": "QA Engineer",
        "skills": [
            "Java",
            "Janjins",
            "QA Automation"
        ]
    },
    "100": {
        "Employee Status": "full-time",
        "Job Posting": " ",
        "description": "Test plan development. Working from the specifications to develop and perform test plans that ensure the accurate functioning of the system. Issue management.Identifying, raising & prioritizing issues and tracking these to a successful resolution. Drive defect management and RCA for various client projects and find opportunities for improvement.",
        "firm_title": "GlobalLogic",
        "position_title": "QA Engineer",
        "skills": [
            "JavaScript",
            "Python",
            "Postman"
        ]
    },
    "101": {
        "Employee Status": "full-time",
        "Job Posting": " ",
        "description": "Building, maintaining and contributing to the development of industry recognised standard testing methodologies, and processes. Producing clear specification documents, designing and implementing Automated UW Rules, building and carrying out unit and scenario tests. Working through timelines and within defined processes. To analyse data and underwriting outcomes to improve rule performance will compliment your core responsibilities.",
        "firm_title": "SoftServe",
        "position_title": "Junior Tester",
        "skills": [
            "JavaScript",
            "Python",
            "Jenkins"
        ]
    },
И так далее...
 ```
 ### 4. Отправить запрос POST. http://162.55.220.72:5031/add_job
```js
Body: Raw(json)
{   "firm_title": "ITX",
   "position_title": "Junior QA",
   "skills": ["testing theory", "SQL", "Postman"],
   "description": "Experience with Functional Testing, including Regression Testing, Integration Testing, and API Testing.",
   "Job Posting": "Feb 14 2023",
   "Employee Status": "Remote"
}
```
```js
Response:
{
    "check_message": "call /all_jobs endpoint for checking.",
    "result_essage": "Job added. Job id is 299"
}
```
### 5. Отправить запрос POST. http://23.88.52.139:5032/add_job_item
```js
Body: Raw(json)
{   "firm_title": "ITX",
   "position_title": "Junior QA",
   "skills": ["testing theory", "SQL", "Postman"],
   "description": "Experience with Functional Testing, including Regression Testing, Integration Testing, and API Testing.",
   "Job Posting": "Feb 14 2023",
   "Employee Status": "Remote"
}
```
```js
Response:
{
    "check_message": "call /all_jobs endpoint for checking.",
    "result_essage": "Job added. Job id is 300"
}
``` 
### 3. Отправить запрос GET. http://162.55.220.72:5031/all_jobs для проверки 
 ```js
Response:
...
"300": {
        "Employee Status": "Remote",
        "Job Posting": " ",
        "description": "Experience with Functional Testing, including Regression Testing, Integration Testing, and API Testing.",
        "firm_title": "ITX",
        "position_title": "Junior QA",
        "skills": [
            "testing theory",
            "SQL",
            "Postman"
        ]
    },
...
 ```
## Ответ: отсутсвует часть ответа в json "Job Posting": " " при отправке запроса POST. http://23.88.52.139:5032/add_job_item. Т.е. ошибка в работе WS_2.
