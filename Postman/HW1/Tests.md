## GET/first 
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
## POST/user_info_3
1. 
```js

