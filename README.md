# Информационная безопасность

## Лабораторная работа №1

### Стек

- Java/Spring
- Hibernate
- PostgeSQL

### Описание API

`POST /auth/register`: метод для регистрации пользователя (принимает логин и пароль).

```json
{
    "login": "username",
    "password": "12345678"
}
```

`POST /auth/login`: метод для аутентификации пользователя (принимает логин и пароль).

```json
{
    "login": "username",
    "password": "12345678"
}
```

`GET /api/data`: метод для получения данных. Доступ только у аутентифицированных пользователей.

### Описание реализованных мер защиты

- От **SQLi** код защищен с помощью ORM Hibernate.
- От **XSS** защищен с помощью экранирования пользовательских данных

```java
AuthModel authModel = new AuthModel(
  HtmlUtils.htmlEscape(credentialsDto.login()),
  passwordEncoder.encode(credentialsDto.password())
);
```

```java
public List<ProductModel> getAllProducts() {
  return productRepository.findAll().stream().peek(
    it -> it.setData(HtmlUtils.htmlEscape(it.getData()))
  ).toList();
}
```

### Отчеты из pipeline

Dependency-check:

![Dependency-check](docs/img/dependency-check.png)

Spotbugs:

![Spotbugs](docs/img/spotbugs.png)
