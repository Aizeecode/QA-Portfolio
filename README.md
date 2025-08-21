# 🧑‍💻 QA Portfolio — Ailat Internship

Добро пожаловать в мой QA-портфолио!  
Здесь собраны примеры моей работы во время стажировки над продуктом Ailat(Android приложения по инвестициям по Шариату), а также дополнительные учебные и практические материалы по тестированию.  

**Linked in:** www.linkedin.com/in/aizada-altynbekova
Contact: aizaturar@mail.ru
---

## 📌 Обо мне
Я начинающий QA-инженер с опытом стажировки, где занималась тестированием мобильного-приложения, поиском багов и улучшением UX.  
Умею работать с:
- написанием баг-репортов, тест-кейсов, чек-листов
- **API-тестированием** (Postman, Swagger)  
- базами данных (**SQLite**)  
- таск-трекерами (**Jira, Notion**)
- Admin panel (**создать, удалить пользователя, добавить продукт и услугу на сайт**)
- Web тестирование(**dev tools**)
- Проверка верстки и соответствие с макетом Figma и ТЗ.**(Figma, UX/UI)**

---

## 📂 Структура репозитория
- **BugReports/** — примеры баг-репортов (60 штук за время стажировки, здесь представлены основные) **https://codeunion.notion.site/21fe5d447d058007a89fdb8b29e1afa8?v=21fe5d447d05818d91ef000c06a92cac**
- **BugReports** - (примеры учебных баг-репортов) **https://docs.google.com/spreadsheets/d/16cuGDkDigcdgfvf4KzGqeUoIMyD-X69poCn41jYYaQ8/edit?usp=sharing**
- **TestCases/** — тест-кейсы для функционального тестирования по учебному проекту Arbuz.kz **https://docs.google.com/spreadsheets/d/1o5ud8AnWf7TgU1Fszlur-I2fwMGvUU3oi4_Ecf0fh_8/edit?gid=0#gid=0https://docs.google.com/spreadsheets/d/1o5ud8AnWf7TgU1Fszlur-I2fwMGvUU3oi4_Ecf0fh_8/edit?gid=0#gid=0**  
- **Checklists/** — чек-листы (по учебному проекту)  **https://docs.google.com/spreadsheets/d/1F8kYo3KiyhYn_XIznxaabDDdGZr_ZLvuevSZFS4vpXM/edit?gid=0#gid=0**
**  
---

## 🐞 Пример баг-репорта
```markdown
# Bug 001: [Back] Неверное сообщение при входе

**Описание:**
При попытке входа на эндпоинт **{{api_base_url}}/{{authentication_prefix}}/tokens/new**
с правильным email и **неверным паролем**, API возвращает сообщение (ниже), что не соответствует контексту действия.
Проверка "прочности" пароля должна выполняться только при регистрации или смене пароля, но не при логине.

{
"statusCode": 400,
"error":
{"message": "password is not strong enough",
"code": "USER_PASSWORD"}
}

**Окружение:**

Инструмент: Postman
Метод: `POST`
Endpoint: `{{api_base_url}}/{{authentication_prefix}}/tokens/new`

**Ожидаемый результат:**
HTTP статус: `401 Unauthorized`
Тело ответа:  "message": "Неверный логин или пароль”

**Фактический результат:**
{
"statusCode": 400,
"error": {"message": "password is not strong enough",
"code": "USER_PASSWORD"}
}


## 🐞 Примеры SQL запросов


--1) Выбрать фамилии и имена всех сотрудников, фамилия (Lastname) которых начинается на гласную букву

SELECT e.FirstName,  e.LastName  
From Employee e 
WHERE e.LastName LIKE 'A%'
   OR e.LastName LIKE 'E%'
   OR e.LastName LIKE 'I%'
   OR e.LastName LIKE 'O%'
   OR e.LastName LIKE 'U%';


--2) Выбрать идентификаторы всех должностей, у которых описание начинается с 'Sales'

SELECT e.EmployeeId 
From Employee e 
WHERE e.Title LIKE 'Sales%'

--3) Выбрать всех сотрудников, у которых номер телефона  заканчивается на 3.

SELECT e.EmployeeId, e.FirstName, LastName , e.Title, e.Phone
From Employee e 
WHERE e.Phone LIKE '%3'

--5) Выбрать всех сотрудников с идентификаторами между 2 и 7

SELECT e.EmployeeId, e.FirstName, LastName , e.Title
From Employee e 
WHERE e.EmployeeId between 3 and 6;

--Выбрала 3 и 6, т.к запрсо был между 2 и 7 не включая.

--6) Выбрать всех сотрудников, подчиняющихся сотрудникам с идентификаторами 2, 6

SELECT e.EmployeeId, e.FirstName, LastName , e.Title
From Employee e 
WHERE e.ReportsTo IN (2, 6);


--7) Выбрать всех сотрудников, у которых идентификатор находится в диапазоне от 2 до 5 включительно.

SELECT e.EmployeeId, e.FirstName, LastName , e.Title
From Employee e 
WHERE e.EmployeeId between 2 and 5;


---  Операторы манипуляции данными

– 8) Добавить нового сотрудника (имя, фамилия)  в таблицу Employee на должность "Courier".

INSERT 
INTO Employee (FirstName, LastName, Title)
VALUES ('Zee', 'Zoo', 'Courier')


– 9) Удалить "созданного" (в задаче 8) сотрудника

DELETE 
from Employee   
where EmployeeId=9

--10) Добавить нового сотрудника с фамилией 'John', именем 'Doe' и адресом электронной почты          'johndoe@example.com' в таблицу Employee.

INSERT 
INTO Employee (FirstName, LastName, Email )
VALUES ('Doe', 'John', 'johndoe@example.com')

--11) Изменить имя нового сотрудника (из задачи 10) на ”'Bond-07”

UPDATE Employee 
SET FirstName ='Bond-07'
WHERE  EmployeeId=9

---Условные операторы AND, OR, NOT

--12) Выбрать всех сотрудников,для которых одновременно выполняются условия : фамилия начинается на 'J' и адрес электронной почты содержит 'doe'.

SELECT FirstName ,e.LastName, e.Title
from Employee e
WHERE LastName like 'J%' and Email like '%doe%'

--13) Выбрать сотрудников, которые не работают в отделе "IT Staff"

SELECT e.FirstName ,e.LastName, e.Title
from Employee e
WHERE Title NOT LIKE 'IT Staff'

--14) Выбрать сотрудников, работающих в должности "IT Manager" или живущих в “Edmonton"

SELECT e.FirstName ,e.LastName, e.Title
from Employee e
WHERE Title LIKE '%IT Manager%' or  City  like  'Edmonton'

--15) Выбрать все должности с идентификаторами или 1 или 2 или 4.

SELECT e.EmployeeId, e.FirstName, LastName , e.Title
