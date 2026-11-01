# Create_brep_model

**RU** · [EN](#english)

Описание алгоритма преобразования полигональной (триангулированной) модели в контурную
модель — B-rep — и его частичная реализация на C++.

## Что в репозитории

| Файл | Что это |
|---|---|
| `Алгоритм создания brep-а.pdf` | алгоритм создания B-rep из триангулированного объекта (3 стр., май 2019) |
| `Еще 1 алгоритм. Другой взгляд на проблему.pdf` | второй вариант алгоритма (2 стр., май 2019) |
| `brep.h`, `brep.cpp` | реализация: класс `plane` (грань) |

Идея первого алгоритма: объект — это вектор треугольников. По одному треугольнику строится
плоскость, затем в неё собираются все треугольники, у которых все три вершины лежат в
плоскости с допуском `tolerance`. При добавлении треугольника общие рёбра удаляются, так что на
грани остаются контуры. Внешний контур отделяется от внутренних по вершинам с наименьшей и
наибольшей суммой `x + y + z`.

## Состояние кода

- Реализовано: построение плоскости по трём точкам, проверка точки на плоскости,
  добавление треугольника на грань (`insert_triangle`), работа с рёбрами и вершинами,
  выделение контуров (`create_conturs`).
- Функция `createBrep(std::vector<triangle>)` объявлена в `brep.h`, но не реализована.
- Код не собирается отдельно: он подключает `stdafx.h` и `graphie.h` (тип `Vertex`) из проекта
  [StairGenerator](https://github.com/beanbo/StairGenerator), где лежат те же `brep.h` и
  `brep.cpp`. Сборка в этом окружении не проверялась.

## Контекст

Алгоритм описан в 2019 году, на GitHub загружен в декабре 2022.

---

## English

A description of an algorithm that turns a triangulated polygon mesh into a boundary
representation (B-rep), plus a partial C++ implementation.

- Two PDFs (in Russian, May 2019) describe two variants of the algorithm: build a plane from one
  triangle, collect every triangle whose vertices lie on that plane within a tolerance, drop
  shared edges so only contours remain, then separate the outer contour from inner ones using
  the vertices with the smallest and largest `x + y + z`.
- `brep.h` / `brep.cpp` implement the `plane` (face) class. `createBrep()` is declared but not
  implemented.
- The code is not standalone: it includes `stdafx.h` and `graphie.h` from
  [StairGenerator](https://github.com/beanbo/StairGenerator), which contains the same files.
  Not built here.
