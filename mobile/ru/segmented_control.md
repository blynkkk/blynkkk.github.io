
### Сегментированный переключатель (Segmented Switch)

Виджет Сегментированный переключатель позволяет отправлять команды на ваше оборудование на основе выбора, сделанного вами в пользовательском интерфейсе. Сегментированный переключатель отправляет индекс выбранного вами элемента, а не строку метки. Отправленный индекс начинается с 1. Он работает так же, как типовой элемент [Комбинированный список (ComboBox)](https://ru.wikipedia.org/wiki/%D0%9A%D0%BE%D0%BC%D0%B1%D0%B8%D0%BD%D0%B8%D1%80%D0%BE%D0%B2%D0%B0%D0%BD%D0%BD%D1%8B%D0%B9_%D1%81%D0%BF%D0%B8%D1%81%D0%BE%D0%BA) или [Меню (Menu)](https://github.com/blynkkk/blynkkk.github.io/blob/master/mobile/ru/menu.md).

Пример кода:

```cpp
BLYNK_WRITE {
  switch (param.asInt()) {
    case 1: { // Пункт 1
      Serial.println("Выбран пункт 1");
      break;
    }
    case 2: { // Пункт 2
      Serial.println("Выбран пункт 2");
      break;
    }    
  }
}
```

Вы также можете установить пункты меню со стороны оборудования с помощью кода:

```cpp
Blynk.setProperty(V1, "labels", "label 1", "label 2", "label 3");
```

**Пример кода:** [Меню](https://github.com/blynkkk/blynk-library/blob/master/examples/Widgets/Menu/Menu.ino)
