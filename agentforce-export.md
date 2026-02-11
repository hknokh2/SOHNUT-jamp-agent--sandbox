# Agentforce + Data Cloud + Knowledge Migration (SOURCE -> TARGET)

Date: 2026-02-01

Source org alias: SOHNUT-jamp-agent--sandbox (Org Id: 00DVe000003Fhm5MAC)
Target org alias: SOHNUT-jamp-agent2--sandbox (Org Id: 00Ddt000005UPR7EAO)

Scope
- Move Data Cloud + Knowledge + Agentforce configuration and data from SOURCE to TARGET.
- This document is based on read-only SF CLI queries only. No write operations were executed in either org.

---

## 1) Current inventory (read-only evidence)

### 1.1 Flows
| Component | Source | Target | Notes |
| --- | --- | --- | --- |
| Get_Family_Member_Information | Present | Missing | Source has the flow; target does not. |

### 1.2 Prompt Templates (GenAiPromptTemplate)
Source prompt templates (relevant):
- Answer_Questions_with_Ogdan
- answerWithKnowledge_Override (UI name: einstein_gpt__answerWithKnowledge override)

Target observation:
- GenAiPromptTemplate metadata type is not supported in TARGET (API error), so Prompt Templates cannot be deployed until feature access is enabled.

### 1.3 Agents / Bots
Source bots (relevant):
- Aliyah_Support

Target observation:
- Bot metadata type is not supported in TARGET (API error), so Agentforce/Service Agent metadata is not deployable until feature access is enabled.

### 1.4 Data Cloud (Data 360)
Data Streams (Knowledge-related):
| Data Stream Name | Source Status | Target Status |
| --- | --- | --- |
| Knowledge_kav_Home | ACTIVE / SUCCESS | Missing |
| Knowledge_DataCategorySelection_Home | ACTIVE / SUCCESS | Missing |
| DataCategory_Home | ACTIVE / SUCCESS | Missing |
| DataCategoryGroup_Home | ACTIVE / SUCCESS | Missing |

Target data streams currently present:
- ProvisionedFeatureStream
- TenantBillingUsageEventStream
- TenantEntitlementTransactionStream
- TenantUsageTypeMultiplierStream

Data Lake Objects (DLO) in SOURCE (Tooling API):
| DLO Developer Name | External Name |
| --- | --- |
| Knowledge_kav_Home | Knowledge_kav_Home__dll |
| Knowledge_DataCategorySelection_Home | Knowledge_DataCategorySelection_Home__dll |

Target observation:
- MktDataLakeObject is not supported in TARGET (API error), which strongly indicates Data Cloud is not enabled.

Search Index + Retriever:
- Cannot be queried via Metadata API in this org. Must be validated in Data Cloud app / Einstein Studio UI.

### 1.5 Knowledge
Data Category Groups:
| Data Category Group | Source | Target |
| --- | --- | --- |
| Portal_Aliyah | Present | Present |
| Ogdan | Present | Missing |

Knowledge article count:
- SOURCE (Knowledge__kav): 165
- TARGET (Knowledge__kav): 0

### 1.6 Permission sets present in orgs (relevant)
Prompt Builder:
- EinsteinGPTPromptTemplateManager (Label: Prompt Template Manager)
- EinsteinGPTPromptTemplateUser (Label: Prompt Template User)

Agentforce:
- AgentforceServiceAgentBuilder
- AgentforceServiceAgentUser
- AgentforceServiceAgentBase
- AgentforceServiceAgentSecureBase
- AgentPlatformBuilder
- AgentforceServiceAgentUserPsg

Knowledge:
- Knowledge Manager
- Knowledge Manager End User
- Lightning Knowledge Manager

---

## 2) Gaps / blockers (must be resolved first)
1) TARGET does not support GenAiPromptTemplate metadata type.
2) TARGET does not support Bot metadata type.
3) TARGET does not support MktDataLakeObject and lacks Knowledge data streams.
4) Data Category Group "Ogdan" missing in TARGET.
5) Knowledge articles are missing in TARGET.

---

## 3) Required permissions and licenses

Knowledge (import/export and management)
- Knowledge User license must be enabled for users who manage or import articles.
- Required permissions for import/export and management include:
  - Manage Articles
  - Manage Salesforce Knowledge
  - Manage Knowledge Article Import/Export
  - Manage Data Categories
  - CRUD permissions on the specific article type(s)

Prompt Builder
- Builders must have the Prompt Template Manager permission set.
- Users who run prompts should have the Prompt Template User permission set.

Data Cloud / Einstein Studio
- Use a Data Cloud admin-level permission set (or equivalent) and grant Einstein Studio model management access to users who create retrievers/search indexes.

Agentforce / Service Agent
- Assign AgentforceServiceAgentBuilder and AgentPlatformBuilder to builders.
- Assign AgentforceServiceAgentUser (and related AgentforceServiceAgentBase/SecureBase) to runtime users.

---

## 4) Dependency-aware deployment order (based on actual org contents)

0) Enable feature access in TARGET (blocking prerequisites)
- Enable Data Cloud (Data 360) and complete initial setup.
- Enable Prompt Builder / Einstein Generative AI features.
- Enable Agentforce / Service Agent features.
- Ensure Knowledge is enabled (it is, but confirm configuration).

1) Knowledge category metadata
- Deploy DataCategoryGroup "Ogdan" from SOURCE to TARGET.
- Verify categories are available in Setup -> Data Category Groups.

2) Data Cloud Knowledge streams
- Create Data Streams in TARGET:
  - Knowledge_kav_Home
  - Knowledge_DataCategorySelection_Home
  - DataCategory_Home
  - DataCategoryGroup_Home
- Map the Knowledge fields to Data Cloud fields in each stream.
- Activate the streams and run an initial refresh.

3) Data Lake Objects and field additions
- Confirm DLOs were created by the data streams (Knowledge_kav_Home__dll, Knowledge_DataCategorySelection_Home__dll).
- Add formula field Full_Article_URL__c to DLO Knowledge_kav_Home__dll (Data Cloud UI).

4) Search Index + Retriever
- Create Search Index "Ogdan_Knowledge" (Vector or Hybrid) on the Knowledge DLO.
- Ensure a retriever exists in Einstein Studio. Create "Ogdan_Knowledge_Retriever_1Cx_8orcafc5846" if needed.

5) Prompt Templates
- Deploy GenAiPromptTemplate:
  - Answer_Questions_with_Ogdan
  - answerWithKnowledge_Override (override for einstein_gpt__answerWithKnowledge)

6) Flow
- Deploy Flow Get_Family_Member_Information.

7) Agent / Service Agent
- Create or update service agent (Bot) "Aliyah_Support" with same properties as SOURCE.
- Add or update actions:
  - Answer_Questions_with_Ogdan
  - Get_Family_Member_Information
  - AnswerQuestionsWithKnowledge (updated if already exists)

8) Knowledge data migration
- Export Knowledge__kav from SOURCE and import into TARGET.
- Ensure article status, language, and data categories are correctly mapped.
- Run Data Stream refresh to ingest Knowledge into Data Cloud.
- Rebuild or refresh the Search Index.

9) End-to-end validation
- Data Streams are ACTIVE.
- Search Index is built and retriever returns data.
- Agent can answer KB-based questions and execute the Flow action.

---

## 5) Suggested SF CLI commands (do not execute unless you intend to write to org)

Retrieve from SOURCE:
```
sf project retrieve -o SOHNUT-jamp-agent--sandbox -x manifest/agentforce-package.xml
```

Deploy to TARGET:
```
sf project deploy -o SOHNUT-jamp-agent2--sandbox -x manifest/agentforce-package.xml
```

Example manifest (adjust to your needs):
```
<?xml version="1.0" encoding="UTF-8"?>
<Package xmlns="http://soap.sforce.com/2006/04/metadata">
  <types>
    <members>Get_Family_Member_Information</members>
    <name>Flow</name>
  </types>
  <types>
    <members>Answer_Questions_with_Ogdan</members>
    <members>answerWithKnowledge_Override</members>
    <name>GenAiPromptTemplate</name>
  </types>
  <types>
    <members>Aliyah_Support</members>
    <name>Bot</name>
  </types>
  <types>
    <members>Ogdan</members>
    <name>DataCategoryGroup</name>
  </types>
  <version>66.0</version>
</Package>
```

Knowledge data export (read-only example):
```
sf data export -o SOHNUT-jamp-agent--sandbox \
  --query "SELECT Id, KnowledgeArticleId, Title, Language, PublishStatus FROM Knowledge__kav" \
  --result-format csv --output-dir temp/exports/knowledge
```

---

## 6) Open issues (from your list, validated)
- KB permission in destination environment: verify Knowledge User license and required permissions are assigned.
- Are KB Articles exist or not: TARGET has 0 Knowledge__kav records; import required.

---

## 7) References (official docs)
- Agentforce metadata types in Metadata API: https://developer.salesforce.com/docs/atlas.en-us.agentforce.meta/agentforce/agentforce_metadata_types.htm
- Data Cloud data stream creation (Metadata API + UI API): https://developer.salesforce.com/docs/data-cloud/api-create-data-stream/guide/create-data-stream-from-s3.html
- Data Cloud metadata API for DLO/fields: https://developer.salesforce.com/docs/data-cloud/api-query/guide/get-metadata.html
- Data Cloud Search Index and Retriever behavior: https://www.salesforce.com/eu/agentforce/agentforce-and-rag/
- Prompt Builder permissions (Prompt Template Manager): https://developer.salesforce.com/blogs/2024/07/prompt-builder-for-salesforce-developers
- Knowledge permissions for import/export: https://resources.docs.salesforce.com/latest/latest/en-us/sfdc/pdf/salesforce_knowledge_impl_guide.pdf
- Knowledge data categories permissions overview: https://trailhead.salesforce.com/content/learn/modules/knowledge-basics-for-lightning-experience/configure-and-maintain-salesforce-knowledge
