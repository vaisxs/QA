# Запросы/Тесты

### POST /user_info

```json
{
   "request":{
      "method":"POST",
      "header":[
         
      ],
      "body":{
         "mode":"raw",
         "raw":{
            "age":23,
            "salary":1000,
            "name":"Svetik",
            "auth_token":"{{tokent}}"
         },
         "options":{
            "raw":{
               "language":"json"
            }
         }
      },
      "url":{
         "raw":"{{url}}user_info",
         "host":[
            "{{url}}"
         ],
         "path":[
            "user_info"
         ]
      }
   },
   "response":[
      
   ]
}
```

Тесты
 ```javascript
 //Статус код 200
 
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});


// Проверка структуры json

const schema = {"properties": {"alpha": {"type": "boolean"}}};

pm.test("Schema is valid ", function() {
pm.response.to.have.jsonSchema(schema);
});

// Проверка коэффициентов перемножения 

pm.test("qa_salary_after_12_months", function () {
    var jsonData = pm.response.json();
    pm.expect(jsonData.qa_salary_after_12_months).to.eql(jsonData.start_qa_salary * 2.9);
});

pm.test("qa_salary_after_6_months", function () {
    var jsonData = pm.response.json();
    pm.expect(jsonData.qa_salary_after_6_months).to.eql(jsonData.start_qa_salary * 2);
});


pm.test("u_salary_1_5_year", function () {
    var jsonData = pm.response.json();
    pm.expect(jsonData.person.u_salary_1_5_year).to.eql(jsonData.start_qa_salary * 4);
});

//Достать значение из поля u_salary_1_5_year
// и передать его в поле salary запроса http://162.55.220.72:5005/get_test_user

var jsonData = pm.response.json();
pm.environment.set('u_salary_1_5_year', jsonData.person.u_salary_1_5_year);
```
### POST /new_data

```json
{
   "request":"method":"POST",
   "header":[
      
   ],
   "body":{
      "mode":"formdata",
      "formdata":[
         {
            "key":"age",
            "value":"28",
            "type":"int"
         },
         {
            "key":"salary",
            "value":"1000",
            "type":"int"
         },
         {
            "key":"name",
            "value":"Nikita""type":"text"
         },
         {
            "key":"auth_token""values":{
               {
                  "token"
               }
            }
         }
      ]
   },
   "url":{
      "raw":"{{url}}new_data",
      "host":[
         "{{url}}"
      ],
      "path":[
         "new_data"
      ]
   }
},
"response":[]
```

Тесты 
```javascript
// Статус код 200
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});

// Проверка структуры json
const schema = {"properties": {"alpha": {"type": "boolean"}}};

pm.test("Schema is valid ", function() {
pm.response.to.have.jsonSchema(schema);
});


// Проверка коэффициентов перемножения
pm.test("1salary*", function () {
    var jsonData = pm.response.json();
    pm.expect(+jsonData.salary[1]).to.eql(jsonData.salary[0] * 2);
});


pm.test("2salary*", function () {
    var jsonData = pm.response.json();
    pm.expect(+jsonData.salary[2]).to.eql(jsonData.salary[0] * 3);
});

// Проверить, что 2-й элемент массива salary больше 1-го и 0-го
pm.test("salary3", function () {
    var jsonData = pm.response.json();
    pm.expect(+jsonData.salary[1])<(+jsonData.salary[2])>(jsonData.salary[0]);
});

```
### POST /test_pet_info
```json
{
   "request":"method":"POST",
   "header":[
      
   ],
   "method":"POST",
   "header":[
      
   ],
   "body":{
      "mode":"formdata",
      "formdata":[
         {
            "key":"age",
            "value":"23",
            "type":"text"
         },
         {
            "key":"salary",
            "value":"1000",
            "type":"text"
         },
         {
            "key":"name",
            "value":"Sveta",
            "type":"text"
         },
         {
            "key":"auth_token",
            "value":{
               {
                  "token"
               }
            },
            "type":"text"
         }
      ]
   },
   "url":{
      "raw":"{{url}}test_pet_info",
      "host":[
         "{{url}}"
      ],
      "path":[
         "test_pet_info"
      ]
   }
},
"response":[]
```

Тесты 

```javascript

// Статус код 200
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});

// Проверка структуры json
const schema = {"properties": {"alpha": {"type": "boolean"}}};

pm.test("Schema is valid ", function() {
pm.response.to.have.jsonSchema(schema);
});

// Проверка коэффициентов перемножения
let req = request.data;
let weight = parseInt(req.weight)


pm.test("weight*0.012", function () {
    var jsonData = pm.response.json();
    pm.expect(jsonData.daily_food).to.eql(weight * 0.012);
});

pm.test("weight*2.5", function () {
    var jsonData = pm.response.json();
    pm.expect(jsonData.daily_sleep).to.eql(weight * 2.5);
});
```
### POST /get_test_user
```json
"request":{
   "method":"POST",
   "header":[
   ],
   "body":{
      "mode":"formdata",
      "formdata":[
         {
            "key":"age",
            "value":"23",
            "type":"text"
         },
         {
            "key":"salary",
            "value":"{{salary}}",
            "type":"text"
         },
         {
            "key":"name",
            "value":"{{name}}",
            "type":"text"
         },
         {
            "key":"auth_token",
            "value":"{{token}}",
            "type":"text"
         }
      ]
   },
   "url":{
      "raw":"{{url}}/get_test_user",
      "host":[
         "{{url}}"
      ],
      "path":[
         "get_test_user"
      ]
   }
},
"response":[
   
]
```
Тесты

```javascript
// Статус код 200
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});

// Проверка формата json
const schema = {"properties": {"alpha": {"type": "boolean"}}};

pm.test("Schema is valid ", function() {
pm.response.to.have.jsonSchema(schema);
});

// Проверить, что поле name = значению переменной name из окружения 
pm.test("name", function () {
    var jsonData = pm.response.json();
    pm.expect(jsonData.name).to.eql(pm.environment.get("name"));
});


// Проверить, что значение поля age соответствует отправленному в запросе значению age 

pm.test("age", function () {
    var jsonData = pm.response.json();
    pm.expect(+jsonData.age).to.eql(23);
});
```
