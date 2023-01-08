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
