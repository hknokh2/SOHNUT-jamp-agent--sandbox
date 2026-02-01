## 1) Подготовка TARGET

1) Открыть Data Cloud (приложение):
   - App Launcher -> Data Cloud.
   - В приложении доступны вкладки Data Streams / Data Lake Objects.
2) Если нужно попасть в Data Cloud Setup:
   - Setup -> Quick Find -> искать "Data Cloud Setup" или "Data 360 Setup".
3) Если Data Cloud Setup НЕ видно:
   - Работайте через приложение Data Cloud (Data Streams / DLO).
   - Для Data Kits проверьте, есть ли вкладка Data Kits в приложении Data Cloud.
   - Если вкладки нет, попросите администратора добавить её в навигацию приложения и/или назначить Permission Set: Data Cloud Admin.
2) Setup -> Knowledge Settings -> включить Knowledge и выбрать Article Type.
3) Setup -> Einstein Setup -> Turn on Einstein (Generative AI).
4) Setup -> Permission Sets -> EinsteinGPTPromptTemplateManager -> Manage Assignments -> Add Assignments -> выбрать пользователя -> Assign.
5) Setup -> Quick Find: Prompt Builder -> открыть Prompt Builder.
6) Setup -> Agents (Agentforce) -> включить Service Agents.

Где включить лицензии и системные права Knowledge:
- **Setup -> Users -> Users -> открыть пользователя -> Edit:**
  - **Knowledge User (License) = включить**
- Setup -> Knowledge Settings:
  - Manage Articles
  - Manage Salesforce Knowledge
  - Manage Knowledge Article Import/Export
  - Manage Data Categories

Пояснение:
- Prompt Builder, Agentforce, Data Cloud, Knowledge — это функции/разделы Salesforce в Setup, а НЕ объекты и НЕ разделы внутри Permission Set.
- Доступ к этим функциям выдаётся через Permission Sets и лицензии, которые назначаются пользователям.

**Назначить права (где и кому, использовать готовые Permission Sets):**

1. **Какие PS назначать для Admin:**
   **Data Cloud Architect**
   **Data Cloud Activation Specialist**	
   **Data Cloud Activation Manager**
   **Prompt Template Manager**	 
   **Enhanced Chat User**	 
   **Agentforce Service Agent Configuration**	 
   **Agent Platform Builder**	 
   **Knowledge LSF Permission Set**		 
   **Knowledge Manager** 
   **Knowledge Permissions**

2. ***Какие готовые PS назначать пользователю runtime / агенту***

   ***??????????***

---

## 2) SOURCE: Data Kit для Data Cloud

Data Kits создаются в разделе Data Cloud Setup. Если раздел не виден, см. шаг 1 (права/провижнинг).

1) Открыть Data Cloud Setup (см. шаг 1 выше).
2) В Data Cloud Setup -> Data Kits -> New
2) Type: DevOps
3) Name: SOHNUT_KB_Agentforce_DevOps (или своё)
4) Data Space: выбрать тот же, что будет в TARGET
5) Save

Добавить компоненты в Data Kit:

Data Streams:
- Knowledge_kav_Home
- Knowledge_DataCategorySelection_Home
- DataCategory_Home
- DataCategoryGroup_Home

DLO:
- Knowledge_kav_Home__dll
- Knowledge_DataCategorySelection_Home__dll

Проверить поле в DLO:
- Data Cloud -> DLO tab -> Knowledge_kav_Home__dll -> поле Full_Article_URL__c (если нет, создать Formula)

Deployment Sequence:
- Data Streams и DLO первыми

Скачать manifest:
- Data Kit -> Download Manifest -> сохранить package.xml

---

## 3) Data Cloud metadata: retrieve/deploy

Команды (Data Kit manifest из UI):
```
sf project retrieve start -o SOHNUT-jamp-agent--sandbox -x PATH/TO/DATA-KIT-package.xml
sf project deploy start -o SOHNUT-jamp-agent2--sandbox -x PATH/TO/DATA-KIT-package.xml
```

Проверка в TARGET:
- Data Streams: Knowledge_kav_Home, Knowledge_DataCategorySelection_Home, DataCategory_Home, DataCategoryGroup_Home
- DLO: Knowledge_kav_Home__dll, Knowledge_DataCategorySelection_Home__dll
- В Knowledge_kav_Home__dll есть Full_Article_URL__c

---

## 4) TARGET: Search Index и Retriever

Search Index:
1) Data Cloud App -> Search Index
2) Create:
   - Name: Ogdan_Knowledge
   - Type: Hybrid
   - Source: Knowledge_kav_Home__dll

Retriever:
1) Einstein Studio -> Retrievers
2) Create:
   - Name: Ogdan_Knowledge_Retriever_1Cx_hm58199f7ec
   - Search Index: Ogdan_Knowledge

---

## 5) Platform metadata: retrieve/deploy

Команды (manifest/export-guide2-package.xml):
```
sf project retrieve start -o SOHNUT-jamp-agent--sandbox -x manifest/export-guide2-package.xml
sf project deploy start -o SOHNUT-jamp-agent2--sandbox -x manifest/export-guide2-package.xml
```

Проверка в TARGET:
- Setup -> Data Category Groups -> Ogdan
- Setup -> Flows -> Get_Family_Member_Information
- Setup -> Prompt Builder -> Prompt Templates -> Answer_Questions_with_Ogdan, answerWithKnowledge_Override
- Setup -> Agents -> Aliyah_Support

---

## 6) Knowledge записи (данные)

Экспорт из SOURCE:
```
sf data export -o SOHNUT-jamp-agent--sandbox --query "SELECT Id, KnowledgeArticleId, Title, Language, PublishStatus FROM Knowledge__kav" --result-format csv --output-dir temp/exports/knowledge
sf data export -o SOHNUT-jamp-agent--sandbox --query "SELECT ParentId, DataCategoryGroupName, DataCategoryName FROM Knowledge__DataCategorySelection" --result-format csv --output-dir temp/exports/knowledge
```

Импорт в TARGET:
```
sf data import -o SOHNUT-jamp-agent2--sandbox --file temp/exports/knowledge/Knowledge__kav.csv --sobject Knowledge__kav
sf data import -o SOHNUT-jamp-agent2--sandbox --file temp/exports/knowledge/Knowledge__DataCategorySelection.csv --sobject Knowledge__DataCategorySelection
```

После импорта:
- Data Cloud -> Data Streams -> Refresh Knowledge_kav_Home и Knowledge_DataCategorySelection_Home
- Search Index -> Rebuild Ogdan_Knowledge

---

## 7) Проверка работы

1) Data Streams ACTIVE и без ошибок
2) DLO содержит Full_Article_URL__c
3) Search Index и Retriever активны
4) Prompt Templates доступны
5) Flow Get_Family_Member_Information активен
6) Agent Aliyah_Support запускает:
   - Answer_Questions_with_Ogdan
   - Get_Family_Member_Information
   - AnswerQuestionsWithKnowledge
7) Knowledge__kav содержит статьи (не 0)
