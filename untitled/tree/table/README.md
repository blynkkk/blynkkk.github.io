# Таблица \(Table\)

Табличный виджет удобен, когда вам нужно структурировать аналогичные данные в пределах одного графического элемента. Работает как обычная таблица.

Вы можете добавить строку в таблицу с помощью кода:

```text
Blynk.virtualWrite(V1, "add", id, "Имя", "Значение");
```

Вы можете обновить строку в таблице с помощью кода:

```text
Blynk.virtualWrite(V1, "update", id, "Новое имя", "Новое значение");
```

Чтобы выделить любой элемент в таблице, используйте его идентификатор:

```text
Blynk.virtualWrite(V1, "pick", 0);
```

Чтобы выбрать/отменить выбор \(сделать значок зеленым/серым\) элемент в таблице, используйте его идентификатор:

```text
Blynk.virtualWrite(V1, "select", 0);
Blynk.virtualWrite(V1, "deselect", 0);
```

Чтобы очистить таблицу используйте код:

```text
Blynk.virtualWrite(V1, "clr");
```

Вы также можете обрабатывать другие действия из таблицы. Например, использовать строку таблицы в качестве кнопки переключения.

```text
BLYNK_WRITE(V1) {
   String cmd = param[0].asStr();
   if (cmd == "select") {
       // строка в таблице была выбрана.
       int rowId = param[1].asInt();
   }
   if (cmd == "deselect") {
       // строка в таблице была отменена.
       int rowId = param[1].asInt();
   }
   if (cmd == "order") {
       // когда строки в таблице переупорядочиваются
       int oldRowIndex = param[1].asInt();
       int newRowIndex = param[2].asInt();
   }
}
```

**Примечание:** Максимальное количество строк в таблице равно 100. Когда вы достигнете предела, таблица будет работать как список FIFO \(Первый пришел - первый ушел\). Это ограничение можно изменить, настроив свойство `table.rows.pool.size` в параметрах локального сервера.

**Пример кода:** [Простое использование таблицы](https://github.com/blynkkk/blynk-library/blob/master/examples/Widgets/Table/Table_Simple/Table_Simple.ino)

**Пример кода:** [Расширенное использование таблицы](https://github.com/blynkkk/blynk-library/blob/master/examples/Widgets/Table/Table_Advanced/Table_Advanced.ino)

