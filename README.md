## simplevk - минималистичная библиотека для удобного использования VkApi

---
### Поехали

Сначала импортируем библиотеку

    import simplevk

Затем создаем объект для дальнейшей работы

    vk = simplevk.vk()

При желании можно авторизироваться

    vk.authorize('id приложения', 'логин', 'пароль', 'разрешения', 'весрия api')

 разрешения должны быть в таком формате: 'messages+offline+smth'
 
 если не удалось авторизоваться - AuthorizationError

 после авторизации доступны атрибуты:
 * vk.app_id
 * vk.user_id
 * vk.access_token
 * vk.v

Отправляем запросы

    vk.request('methodname', 'parametrs')

#### Пример

```
import simplevk

myvk = simplevk.vk()
myvk.request('users.get','user_id=1') # не требует авторизации

try:
    myvk.authorize('1234567', 'dartveider@yandex.ru', 'qwerty', 'photos+wall', '5.64')
except simplevk.AuthorizationError as err:
    print(err)

my_id = myvk.user_id
mywall = myvk.request('wall.get', 'owner_id='+str(my_id)'&count=1') # обратите внимание, что параметры отделены друг от друга знаком '&'
print(mywall['response']['items'][0]['text'])
```


