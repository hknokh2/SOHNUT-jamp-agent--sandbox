# Data Cloud Data Kit: пошаговая инструкция (SOURCE -> TARGET)

Дата: 2026-02-01

Эта инструкция объясняет, как вручную создать Data Cloud Data Kit и получить manifest (package.xml) через UI Data Cloud Setup. В ней учтены ваши реальные компоненты в SOURCE org.

Важно
- Data Kit переносит только метаданные Data Cloud (настройки и определения), но не переносит данные (например, записи Knowledge). Это нужно делать отдельно.
- Начиная с Winter ’25, Data Cloud метаданные нельзя смешивать с Platform метаданными в одном пакете. Для Data Cloud и для Platform используйте разные manifests/пакеты.

---

## 1) Предусловия
1. В обеих org (SOURCE и TARGET) должен быть включен Data Cloud (Data 360).
2. В обеих org должен существовать Data Space с одинаковым именем/префиксом.
3. У пользователя должны быть права на Data Cloud Setup и создание Data Kits.

---

## 2) Создание Data Kit в SOURCE (SOHNUT-jamp-agent--sandbox)

1) Откройте Setup.
2) В Quick Find введите: Data Cloud Setup.
3) Откройте Data Cloud Setup.
4) В левом меню откройте раздел Data Kits.
5) Нажмите New.
6) Заполните:
   - Data Kit Type: DevOps
   - Name: например, SOHNUT_KB_Agentforce_DevOps
   - Description: при необходимости
   - Data Space: выберите существующий Data Space, который совпадает по имени с TARGET
7) Нажмите Save.

---

## 3) Какие компоненты добавить в Data Kit (конкретно для вашего случая)

### 3.1 Data Streams (обязательные для Knowledge)
Добавьте Data Streams, которые есть в SOURCE и нужны для Knowledge:
- Knowledge_kav_Home
- Knowledge_DataCategorySelection_Home
- DataCategory_Home
- DataCategoryGroup_Home

Как добавить:
- В карточке Data Kit найдите секцию Data Stream Bundles (или Data Streams)
- Нажмите Add
- Выберите тип источника (обычно Salesforce CRM)
- Выберите нужные Data Streams из списка
- Сохраните

### 3.2 Data Lake Objects (DLO)
Добавьте DLO, которые соответствуют Knowledge потокам:
- Knowledge_kav_Home__dll
- Knowledge_DataCategorySelection_Home__dll

Если в SOURCE добавляли кастомное поле в DLO (например, Full_Article_URL__c в Knowledge_kav_Home__dll), убедитесь, что оно уже создано и включено в DLO — тогда оно попадет в Data Kit как часть метаданных.

### 3.3 Остальные компоненты (добавлять только если реально используются)
- Data Model Objects (DMO)
- Data Graphs
- Calculated Insights
- Segments
- Identity Resolution

Если эти компоненты не используются в вашей модели — не добавляйте их.

---

## 4) Проверка порядка публикации (Deployment Sequence)
После добавления компонентов Data Kit покажет рекомендуемый порядок публикации (sequence).
- Проверьте его и сохраните.
- Для Knowledge обычно логика такая: сначала Data Streams и DLO, затем остальные компоненты (если есть).

---

## 5) Скачивание manifest (package.xml) из UI

1) В Data Cloud Setup откройте Data Kits.
2) Выберите ваш DevOps Data Kit.
3) Нажмите Download Manifest.
4) Сохраненный package.xml используйте для retrieve/deploy через SF CLI.

Этот package.xml и есть «официальный» manifest, который формирует UI Data Kit. Он отличается от обычного manifest для Platform метаданных.

---

## 6) Что дальше (после создания Data Kit)

Дальше обычно делается:
- Retrieve Data Kit метаданных в проект SF CLI
- Deploy Data Kit метаданных в TARGET
- Отдельно перенос Knowledge статьи (данные)
- Обновление/перестроение Data Streams и Search Index

Если нужно — скажи, и я добавлю в этот документ готовые CLI команды под ваши алиасы.

---

## 7) Напоминание про Knowledge данные
Data Kit не переносит записи Knowledge.
Значит, после деплоя Data Cloud метаданных нужно:
- Экспортировать Knowledge__kav из SOURCE
- Импортировать Knowledge__kav в TARGET
- Запустить обновление Data Streams
- Перестроить Search Index

