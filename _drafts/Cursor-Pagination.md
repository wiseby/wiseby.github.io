---
layout: post
title:  "Pagination with a Cursor"
categories: ['Architecture']
---

https://jsonapi.org/profiles/ethanresnick/cursor-pagination/

```json
{
    "cursor": "5",
    "name": "c"
}
```
Sorted by **Id**:

| Row Number | Id   | Name      | Value   |     |
|:----------:|:----:|:----------|:--------|:----|
|     1      | 1    |  Calle    |   100   |     |
|     2      | 2    |  Emil     |   10    |     |
|     3      | 3    |  Gösta    |   29    |     |
|     4      | 4    |  Gunnar   |   23    |     |
|     5      | 5    |  Stina    |   75    |  << |
|     6      | 6    |  Evert    |   79    |     |
|     7      | 7    |  Alfred   |   26    |     |
|     8      | 8    |  Alma     |   49    |     |
|     9      | 9    |  Ida      |   7     |     |
|     10     | 10   |  Lina     |   25    |     |

Sorted by **Name**:

| Row Number | Id   | Name      | Value   |     |
|:----------:|:----:|:----------|:--------|:----|
|     1      | 7    |  Alfred   |   26    |     |
|     2      | 8    |  Alma     |   49    |     |
|     3      | 1    |  Calle    |   100   |     |
|     4      | 2    |  Emil     |   10    |     |
|     5      | 6    |  Evert    |   79    | <<  |
|     6      | 4    |  Gunnar   |   23    |     |
|     7      | 3    |  Gösta    |   29    |     |
|     8      | 9    |  Ida      |   7     |     |
|     9      | 10   |  Lina     |   25    |     |
|     10     | 5    |  Stina    |   75    |     |