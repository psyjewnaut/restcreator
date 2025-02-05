# RestCreator — библиотека автогенерации эффективного REST API

Данная библиотека предоставляет механизм генерации REST API из ORM. Используя аннотации, решение избавляет от шаблонного кода и позволяет в один клик создавать микросервисы с гибким и высокопроизводительным REST-интерфейсом. При этом весь код остается доступным для кастомизации и поддержки.

## Ключевые преимущества

- **Автоматизация** — генерация всех необходимых слоев: контроллеры, сервисы, репозитории и обёртки ответов.
- **Гибкость** — разработчик может вмешаться и донастроить любую часть сгенерированного кода.
- **Высокая производительность** — за счет оптимизированной логики и структуры слоев.
- **Экономия времени** — решение исключает работу по написанию известных решений CRUD операций.
- **Надежность** — минимизация человеческого фактора за счет автогенерации и унифицированной кодовой базы.
- **Документация** — javadoc, OpenAPI спецификация и Swagger UI.

## Требования

- Spring Boot 3 с Hibernate

## Установка

Для установки необходимо просто добавить зависимость в проект

```
<dependency>
    <groupId>dev.psyjewnaut</groupId>
    <artifactId>rest-creator</artifactId>
    <version>1.0.0</version>
</dependency>
```

## Пример использования

Желаемую сущность нужно просто пометить необходимыми аннотациями `@CreateRestApi` (содержит все 3 следующих аннотации), `@CreateService`, `@CreateRestController`, `@CreateRepository`

```
import dev.psyjewnaut.restcreator.annotations.CreateRestApi;
//...
@CreateRestApi
@Entity
public class Brand {
    @Id
    @GeneratedValue
    private Long id;
    private String name;
    // ...
}
```

После этого современные среды разработки распознают код будущих классов `BrandBaseRepository`, `BrandBaseService`, `BrandBaseController` для сущности `Brand` и они будут готовы для кастомизации:

```
import dev.psyjewnaut.restcreator.models.RestResponse;
//...
@Primary
public class BrandController extends BrandBaseController {

    @GetMapping("/load")
    public class loadBrand(HttpServlerRequest request, String name){
        return new RestResponse.ok(request).body(brandBaseService.getByName(name))
    }
    //...
}
```

## Результат

При запуске приложения вы получите готовый REST API с open-api.json и Swagger UI:

![SwaggerUI](RestCreatorAPI.jpg "Swagger")


# License
На данный момент не распространяется публично.<br>
Email для предложений: psyjewnaut@gmail.com
