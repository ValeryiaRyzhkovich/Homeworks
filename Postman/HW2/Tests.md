## 1. GET/first
1. Получить статус код 200
```js
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});
```
2. Проверить, что в body приходит правильный string.
```js
pm.test("Body matches string", function () {
    pm.expect(pm.response.text()).to.include("This is the first responce from server!ss");
});
```
---
## 2. POST/user_info_3
1. Получить статус код 200
```js
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});
```

2. Спарсить response body в json.
```js
let parsing_response = pm.response.json()
console.log("parsing_response", parsing_response);
```
3. Проверить, что name в ответе равно name s request (name вбить руками.)
```js
pm.test("name", function(){
    pm.expect(parsing_response.name).to.equal("Marina");
});
```
4. Проверить, что age в ответе равно age s request (age вбить руками.)
 ```js
pm.test("age", function(){
    pm.expect(parsing_response.age).to.equal("40");
});
```

5. Проверить, что salary в ответе равно salary s request (salary вбить руками.)
```js
pm.test("salary", function(){
    pm.expect(parsing_response.salary).to.equal(1500);
});
```

6. Спарсить request.
```js
let parsing_request = request.data
console.log("parsing_request", parsing_request);
```

7. Проверить, что name в ответе равно name s request (name забрать из request.)
```js
pm.test("name from request", function(){
    pm.expect(parsing_response.name).to.equal(parsing_request.name);
});
```

8. Проверить, что age в ответе равно age s request (age забрать из request.)
```js
pm.test("age from request", function(){
    pm.expect(parsing_response.age).to.equal(parsing_request.age);
});
```

9. Проверить, что salary в ответе равно salary s request (salary забрать из request.)
```js
pm.test("salary from request", function(){
    pm.expect(parsing_response.salary).to.equal(+parsing_request.salary);
});
```

10. Вывести в консоль параметр family из response.
```js
console.log("family", parsing_response.family);
```

11. Проверить что u_salary_1_5_year в ответе равно salary*4 (salary забрать из request)
```js
pm.test("u_salary_1_5_year", function(){
    pm.expect(parsing_response.family.u_salary_1_5_year).to.equal(+parsing_request.salary*4);
});
```
---
## 3. GET/object_info_3
1. Получить статус код 200
```js
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});
```

2. Спарсить response body в json
```js
let response_parsing = pm.response.json()
console.log("response_parsing", response_parsing);
```
3. Спарсить request.
```js
let request_parsing = pm.request.url.query.all()
console.log("request_parsing", request_parsing);
```
4. Проверить, что name в ответе равно name s request (name забрать из request.)
```js
pm.test("name from request", function(){
    pm.expect(response_parsing.name).to.equal(request_parsing[0].value)
} );
```

5. Проверить, что age в ответе равно age s request (age забрать из request.)
```js
pm.test("age from request", function(){
    pm.expect(response_parsing.age).to.equal(request_parsing[1].value)
});
```
6. Проверить, что salary в ответе равно salary s request (salary забрать из request.)
```js
pm.test("salary from request", function(){
    pm.expect(response_parsing.salary).to.equal(+request_parsing[2].value)
});
```
7. Вывести в консоль параметр family из response.
```js
console.log("family", response_parsing.family);
```
8. Проверить, что у параметра dog есть параметры name.
```js
pm.test("dog_name", function(){
    pm.expect(response_parsing.family.pets.dog).to.have.property("name")
});
```
9. Проверить, что у параметра dog есть параметры age.
```js
pm.test("dog_age", function(){
    pm.expect(response_parsing.family.pets.dog).to.have.property("age")
});
```
10. Проверить, что параметр name имеет значение Luky.
```js
pm.test("dog_Luky", function(){
    pm.expect(response_parsing.family.pets.dog.name).to.equal("Luky")
});
```

11. Проверить, что параметр age имеет значение 4.
```js
pm.test("dog_age_4", function(){
    pm.expect(response_parsing.family.pets.dog.age).to.equal(4)
});
```
---
## 4. GET/object_info_4
1. Получить статус код 200
```js
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});
```
2. Спарсить response body в json
```js
let response_parsing = pm.response.json()
console.log("response_parsing", response_parsing);
```
3. Спарсить request.
```js
let request_parsing = pm.request.url.query.all()
console.log("request_parsing", request_parsing);
```
4. Проверить, что name в ответе равно name s request (name забрать из request.)
```js
pm.test("name from request", function(){
    pm.expect(response_parsing.name).to.equal(request_parsing[0].value)
});
```
5. Проверить, что age в ответе равно age из request (age забрать из request.)
```js
pm.test("age from request", function(){
    pm.expect(response_parsing.age).to.equal(+request_parsing[1].value)
});
```
6. Вывести в консоль параметр salary из request.
```js
console.log("salary from request", request_parsing[2].value);
```
7. Вывести в консоль параметр salary из response.
```js
console.log("salary from response", response_parsing.salary);
```
8. Вывести в консоль 0-й элемент параметра salary из response.
```js
console.log("salary_0 from response", response_parsing.salary[0]);
```
9. Вывести в консоль 1-й элемент параметра salary параметр salary из response.
```js
console.log("salary_1 from response", response_parsing.salary[1]);
```
10. Вывести в консоль 2-й элемент параметра salary параметр salary из response.
```js
console.log("salary_2 from response", response_parsing.salary[2]);
```
11. Проверить, что 0-й элемент параметра salary равен salary из request (salary забрать из request.)
```js
pm.test("salary_0 from request", function(){
    pm.expect(response_parsing.salary[0]).to.equal(+request_parsing[2].value)
});
```
12. Проверить, что 1-й элемент параметра salary равен salary*2 из request (salary забрать из request.)
```js
pm.test("salary_1 from request", function(){
    pm.expect(+response_parsing.salary[1]).to.equal(request_parsing[2].value*2)
});
```
13. Проверить, что 2-й элемент параметра salary равен salary*3 из request (salary забрать из request.)
```js
pm.test("salary_2 from request", function(){
    pm.expect(+response_parsing.salary[2]).to.equal(request_parsing[2].value*3)
});
```
14. Создать в окружении переменную name
```js
pm.environment.set("name");
```
15. Создать в окружении переменную age
```js
pm.environment.set("age");
```
16. Создать в окружении переменную salary
```js
pm.environment.set("salary");
```
17. Передать в окружение переменную name
```js
pm.environment.set("name", "Lera");
```
18. Передать в окружение переменную age
```js
pm.environment.set("age", "25");
```
19. Передать в окружение переменную salary
```js
pm.environment.set("salary", "1000");
```
20. Написать цикл который выведет в консоль по порядку элементы списка из параметра salary.
```js
for (let i of response_parsing.salary) {
   console.log(i)};
```
---
## 5. POST/user_info_2
1. Статус код 200
```js
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});
```
2. Спарсить response body в json.
```js
let response_parsing = pm.response.json()
console.log("response_parsing", response_parsing);
```
3. Спарсить request.
```js
let request_parsing = request.data
console.log("request_parsing", request_parsing);
```
4. Проверить, что json response имеет параметр start_qa_salary
```js
pm.test("start_qa_salary", function(){
    pm.expect(response_parsing).to.have.property("start_qa_salary");
});
```
5. Проверить, что json response имеет параметр qa_salary_after_6_months
```js
pm.test("qa_salary_after_6_months", function(){
    pm.expect(response_parsing).to.have.property("qa_salary_after_6_months");
});
```
6. Проверить, что json response имеет параметр qa_salary_after_12_months
```js
pm.test("qa_salary_after_12_months", function(){
    pm.expect(response_parsing).to.have.property("qa_salary_after_12_months");
});
```
7. Проверить, что json response имеет параметр qa_salary_after_1.5_year
```js
pm.test("qa_salary_after_1.5_year", function(){
    pm.expect(response_parsing).to.have.property("qa_salary_after_1.5_year");
}); 
```
8. Проверить, что json response имеет параметр qa_salary_after_3.5_years
```js
pm.test("qa_salary_after_3.5_years", function(){
    pm.expect(response_parsing).to.have.property("qa_salary_after_3.5_years");
}); 
```
9. Проверить, что json response имеет параметр person
```js
pm.test("person", function(){
    pm.expect(response_parsing).to.have.property("person");
});
```
10. Проверить, что параметр start_qa_salary равен salary из request (salary забрать из request.)
```js
pm.test("start_qa_salary from request", function(){
    pm.expect(response_parsing.start_qa_salary).to.equal(+request_parsing.salary);
});
```
11. Проверить, что параметр qa_salary_after_6_months равен salary*2 из request (salary забрать из request.)
```js
pm.test("qa_salary_after_6_months from request", function(){
    pm.expect(response_parsing.qa_salary_after_6_months).to.equal(+request_parsing.salary*2);
});
```
12. Проверить, что параметр qa_salary_after_12_months равен salary*2.7 из request (salary забрать из request.)
```js
pm.test("qa_salary_after_12_months from request", function(){
    pm.expect(response_parsing.qa_salary_after_12_months).to.equal(+request_parsing.salary*2.7);
});
```
13. Проверить, что параметр qa_salary_after_1.5_year равен salary*3.3 из request (salary забрать из request.)
```js
pm.test("qa_salary_after_1.5_year from request", function(){
    pm.expect(response_parsing["qa_salary_after_1.5_year"]).to.equal(+request_parsing.salary*3.3);
});
```
14. Проверить, что параметр qa_salary_after_3.5_years равен salary*3.8 из request (salary забрать из request.)
```js
pm.test("qa_salary_after_3.5_years from request", function(){
    pm.expect(response_parsing["qa_salary_after_3.5_years"]).to.equal(+request_parsing.salary*3.8);
});
```
15. Проверить, что в параметре person, 1-й элемент из u_name равен salary из request (salary забрать из request.)
```js
pm.test("u_name", function(){
    pm.expect(response_parsing.person.u_name[1]).to.equal(+request_parsing.salary)
});
```
16. Проверить, что что параметр u_age равен age из request (age забрать из request.)
```js
pm.test("u_age", function(){
    pm.expect(response_parsing.person.u_age).to.equal(+request_parsing.age)
});
```
17. Проверить, что параметр u_salary_5_years равен salary*4.2 из request (salary забрать из request.)
```js
pm.test("u_salary_5_years", function(){
    pm.expect(response_parsing.person.u_salary_5_years).to.equal(+request_parsing.salary*4.2)
});
```
18. Написать цикл который выведет в консоль по порядку элементы списка из параметра person.
```js
for (let i = 0; i < response_parsing.person.u_name.length; i++) {
  console.log("Вывод из списка, элемента с индексом " + i + ": " + response_parsing.person.u_name[i]);
}
```
