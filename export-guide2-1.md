1. Give permissions to Admin:

   - Knowledge User
2. Assign PS to admin

   - Agentforce Service Agent Configuration	 
   - Agent Platform Builder	 
   - Data Cloud User
   - Data Cloud Architect
   - Data Cloud Activation Specialist	
   - Data Cloud Activation Manager
   - Knowledge Manager 
   - Prompt Template Manager	 
3. Setup -> Data Cloud -> Get Started  => Wait...
4. Setup -> Knowledge Settings 

   - Allow users to create and edit articles from the Articles tab (Classic Only)
   - Allow users to add external multimedia content to HTML in the standard editor (Classic Only)
   - Internal App
   - Customer
   - Partner
5. Setup -> Einstein Setup -> Turn on Einstein  Toggle
6. Setup -> Einstein Bots -> Turn On Einstein Bots Toggle
7. Setup -> Agentforce Agents -> Turn On Agentforce Toggle
8. Assign Permission Set License Assignment to Admin

   - Einstein Agent
   - Messaging for In-App and Web User
9. Profiles -> System Administrator ->  Object Settings -> Data Streams and Data Lake Objects  => Tabs On
10. Create "EinsteinServiceAgent User" .
    Give it some user name similar to the source org, like: aliyah_support@00dve000010fhm5.ext 
    email: noreply@salesforce.com 
    Profile: Einstein Agent User
    User License: Einstein Agent
    Role: Aliya Division Manager
11. Give him permissions sets of:
    - Prompt Template User
    - Agentforce Service Agent Object Access
    - Agentforce Service Agent Secure Base
    - Data Cloud User
12. In the **Source Org:**  Data Kits -> New -> "KB Agentforce DevOps"

    - Data Stream Bundles  -> Add -> Salesforce CRM (name the bundle as "KnowledgeDataStream") 

      - Knowledge_kav_Home
    - Search Indexes -> Add -> Ogdan_Knowledge
    - Retrievers  -> Add -> Ogdan Knowledge Retriever (Ogdan_Knowledge_Retriever_1Cx_hm58199f7ec)
    - Press "Download Manifest File" -> Save to the file to "manifest/agentforce-dc-package.xml" (typically  it's a part of your SFDX project inside ./manifest folder), below is the actual manifest file from the jamp--agent.sandbox:

```XML
<?xml version="1.0" encoding="UTF-8"?>
<Package xmlns="http://soap.sforce.com/2006/04/metadata">
    <types>
        <members>ssot__KnowledgeArticleVersion__dlm.Aliyah_Portal_FAQ_Categories_c__c</members>
        <members>ssot__KnowledgeArticleVersion__dlm.Aliyah_Portal_StepbyStep_Categories_c__c</members>
        <members>ssot__KnowledgeArticleVersion__dlm.Answer_c__c</members>
        <members>ssot__KnowledgeArticleVersion__dlm.AssignmentNote__c</members>
        <members>ssot__KnowledgeArticleVersion__dlm.Content_c__c</members>
        <members>ssot__KnowledgeArticleVersion__dlm.DigitalEngagementResponse_c__c</members>
        <members>ssot__KnowledgeArticleVersion__dlm.Index_Number_c__c</members>
        <members>ssot__KnowledgeArticleVersion__dlm.InternalNotes_c__c</members>
        <members>ssot__KnowledgeArticleVersion__dlm.LargeLanguageModel__c</members>
        <members>ssot__KnowledgeArticleVersion__dlm.MigratedToFromArticleVersion__c</members>
        <members>ssot__KnowledgeArticleVersion__dlm.Question_c__c</members>
        <members>ssot__KnowledgeArticleVersion__dlm.index_c__c</members>
        <name>CustomField</name>
    </types>
    <types>
        <members>DataCategoryCustom__dlm</members>
        <members>DataCategoryGroupCustom__dlm</members>
        <members>DataCategorySelectionCustom__dlm</members>
        <name>CustomObject</name>
    </types>
    <types>
        <members>DataCategoryGroup_Home</members>
        <members>DataCategory_Home</members>
        <members>Knowledge_DataCategorySelection_Home</members>
        <members>Knowledge_kav_Home</members>
        <members>SalesforceDotCom_Home3</members>
        <name>DataKitObjectDependency</name>
    </types>
    <types>
        <members>DataCategoryGroup_Home</members>
        <members>DataCategory_Home</members>
        <members>Knowledge_DataCategorySelection_Home</members>
        <members>Knowledge_kav_Home</members>
        <members>Ogdan_Knowledge</members>
        <members>Ogdan_Knowledge_Retriever_1Cx_hm58199f7ec</members>
        <members>SalesforceDotCom_Home</members>
        <name>DataKitObjectTemplate</name>
    </types>
    <types>
        <members>KB_Agentforce_DevOps</members>
        <name>DataPackageKitDefinition</name>
    </types>
    <types>
        <members>KB_Agentforce_DevOps_1769977775330</members>
        <members>KB_Agentforce_DevOps_1769977815348</members>
        <members>KB_Agentforce_DevOps_1769978232569</members>
        <members>KB_Agentforce_DevOps_1769978232944</members>
        <members>KB_Agentforce_DevOps_1769978235580</members>
        <members>KB_Agentforce_DevOps_1769978236606</members>
        <members>KB_Agentforce_DevOps_1769978237835</members>
        <members>KB_Agentforce_DevOps_1769978239700</members>
        <members>KB_Agentforce_DevOps_1769978242477</members>
        <name>DataPackageKitObject</name>
    </types>
    <types>
        <members>Salesforce_Home</members>
        <name>DataSource</name>
    </types>
    <types>
        <members>KnowledgeDataStream</members>
        <name>DataSourceBundleDefinition</name>
    </types>
    <types>
        <members>DataCategoryGroup_Home1</members>
        <members>DataCategory_Home1</members>
        <members>Knowledge_DataCategorySelection_Home1</members>
        <members>Knowledge_kav_Home1</members>
        <name>DataSourceObject</name>
    </types>
    <types>
        <members>KB_Agentforce_DevOpsSalesforce_HomeAliyah_Portal_FAQ_Categories_cKnowledgeArticleVersionAliyah_Portal_FAQ_Categories_cHHnOVAZpUaXMafk</members>
        <members>KB_Agentforce_DevOpsSalesforce_HomeAliyah_Portal_StepbyStep_Categories_cKnowledgeArticleVersionAliyah_Portal_StepbyStep_Categories_cjLDMbQugFXMjeta</members>
        <members>KB_Agentforce_DevOpsSalesforce_HomeAnswer_cKnowledgeArticleVersionAnswer_cyASUYLNzuvWorEH</members>
        <members>KB_Agentforce_DevOpsSalesforce_HomeArticleMasterLanguageKnowledgeArticleVersionPrimaryLanguagefuOZMyMbhOKuFMG</members>
        <members>KB_Agentforce_DevOpsSalesforce_HomeArticleNumberKnowledgeArticleVersionArticleNumberBwBRkjjyborgGUK</members>
        <members>KB_Agentforce_DevOpsSalesforce_HomeAssignmentNoteKnowledgeArticleVersionAssignmentNotezvepzemBRTMJiSU</members>
        <members>KB_Agentforce_DevOpsSalesforce_HomeContent_cKnowledgeArticleVersionContent_cLXHCVteThIubgbV</members>
        <members>KB_Agentforce_DevOpsSalesforce_HomeCreatedByIdDataCategoryCustomCreatedByIdXVOpHDizcZagper</members>
        <members>KB_Agentforce_DevOpsSalesforce_HomeCreatedByIdDataCategoryGroupCustomCreatedByIdByANHghooHqRttj</members>
        <members>KB_Agentforce_DevOpsSalesforce_HomeCreatedByIdDataCategorySelectionCustomCreatedByIdndMamZEQSLGuKpF</members>
        <members>KB_Agentforce_DevOpsSalesforce_HomeCreatedDateDataCategoryCustomCreatedDatewPrTPSdqEEXnJQE</members>
        <members>KB_Agentforce_DevOpsSalesforce_HomeCreatedDateDataCategoryGroupCustomCreatedDateYoZqmmGTrMxfJzK</members>
        <members>KB_Agentforce_DevOpsSalesforce_HomeCreatedDateDataCategorySelectionCustomCreatedDateBPFUkuptMJbIozz</members>
        <members>KB_Agentforce_DevOpsSalesforce_HomeCreatedDateKnowledgeArticleVersionCreatedDatepRebcFaYRtIgLhF</members>
        <members>KB_Agentforce_DevOpsSalesforce_HomeDataCategoryGroupIdDataCategoryCustomDataCategoryGroupIdAmnOWeXOSKAvuqz</members>
        <members>KB_Agentforce_DevOpsSalesforce_HomeDataCategoryGroupIdDataCategorySelectionCustomDataCategoryGroupIdJbvAGwFhPeTZmIa</members>
        <members>KB_Agentforce_DevOpsSalesforce_HomeDataCategoryIdDataCategorySelectionCustomDataCategoryIdyDXuJtEwCridDfb</members>
        <members>KB_Agentforce_DevOpsSalesforce_HomeDataSourceDataCategoryCustomDataSourceWouzwqIldZKKPQD</members>
        <members>KB_Agentforce_DevOpsSalesforce_HomeDataSourceDataCategoryGroupCustomDataSourceFLPiWBdlOmASBdH</members>
        <members>KB_Agentforce_DevOpsSalesforce_HomeDataSourceDataCategorySelectionCustomDataSourceIUkjqmrCVNhvkbz</members>
        <members>KB_Agentforce_DevOpsSalesforce_HomeDataSourceKnowledgeArticleVersionDataSourceIdaEFTVxuwxSVexwK</members>
        <members>KB_Agentforce_DevOpsSalesforce_HomeDataSourceObjectDataCategoryCustomDataSourceObjectIjXOmxicNMMLjoF</members>
        <members>KB_Agentforce_DevOpsSalesforce_HomeDataSourceObjectDataCategoryGroupCustomDataSourceObjectSSVnIvaNPtSuQyF</members>
        <members>KB_Agentforce_DevOpsSalesforce_HomeDataSourceObjectDataCategorySelectionCustomDataSourceObjectwFRTOqxJgDGoFne</members>
        <members>KB_Agentforce_DevOpsSalesforce_HomeDataSourceObjectKnowledgeArticleVersionDataSourceObjectIdvFnRPuGELCeojzN</members>
        <members>KB_Agentforce_DevOpsSalesforce_HomeDescriptionDataCategoryGroupCustomDescriptiondOWhQWnbrGTFSYC</members>
        <members>KB_Agentforce_DevOpsSalesforce_HomeDeveloperNameDataCategoryCustomDeveloperNameeoxomyKaCSQuKJN</members>
        <members>KB_Agentforce_DevOpsSalesforce_HomeDeveloperNameDataCategoryGroupCustomDeveloperNamerWGIxbYeIelnhoe</members>
        <members>KB_Agentforce_DevOpsSalesforce_HomeDigitalEngagementResponse_cKnowledgeArticleVersionDigitalEngagementResponse_cbiQSNOKxJSZMZaK</members>
        <members>KB_Agentforce_DevOpsSalesforce_HomeFirstPublishedDateKnowledgeArticleVersionFirstPublishedDateTimeYKalcCYLYyalZld</members>
        <members>KB_Agentforce_DevOpsSalesforce_HomeFull_Article_URLKnowledgeArticleVersionExternalURLFHYXlQZeTJAQbbD</members>
        <members>KB_Agentforce_DevOpsSalesforce_HomeIdDataCategoryCustomIduLvZSPJvOIgOqwu</members>
        <members>KB_Agentforce_DevOpsSalesforce_HomeIdDataCategoryGroupCustomIdYmlBkpcCORQEjzS</members>
        <members>KB_Agentforce_DevOpsSalesforce_HomeIdDataCategorySelectionCustomIdMdPMPyYjQutYtNH</members>
        <members>KB_Agentforce_DevOpsSalesforce_HomeIdKnowledgeArticleVersionIdmbZHjMMYscoSIQX</members>
        <members>KB_Agentforce_DevOpsSalesforce_HomeIndex_Number_cKnowledgeArticleVersionIndex_Number_cRLudMgKVskfgAbY</members>
        <members>KB_Agentforce_DevOpsSalesforce_HomeInternalNotes_cKnowledgeArticleVersionInternalNotes_crsNJgijNQmDOrOj</members>
        <members>KB_Agentforce_DevOpsSalesforce_HomeIsLatestVersionKnowledgeArticleVersionIsLatestVersionnUEbEnyblolZcAm</members>
        <members>KB_Agentforce_DevOpsSalesforce_HomeIsVisibleInAppKnowledgeArticleVersionIsVisibleInAppEoiBofJtteqshdR</members>
        <members>KB_Agentforce_DevOpsSalesforce_HomeIsVisibleInCspKnowledgeArticleVersionIsVisibleToCustomerPhFeHBweahJBRaD</members>
        <members>KB_Agentforce_DevOpsSalesforce_HomeIsVisibleInPkbKnowledgeArticleVersionIsVisibleInPublicKnowledgeBasebgNalhFiYIsfzRm</members>
        <members>KB_Agentforce_DevOpsSalesforce_HomeIsVisibleInPrmKnowledgeArticleVersionIsVisibleToPartnerqnuCeqhqRCIfuPg</members>
        <members>KB_Agentforce_DevOpsSalesforce_HomeKnowledgeArticleIdKnowledgeArticleVersionKnowledgeArticleIdjMHHXzIUGEgYNRg</members>
        <members>KB_Agentforce_DevOpsSalesforce_HomeLanguageKnowledgeArticleVersionLanguageCudoxlQxHOdDddR</members>
        <members>KB_Agentforce_DevOpsSalesforce_HomeLargeLanguageModelKnowledgeArticleVersionLargeLanguageModelDwccVvPsYMpwBSx</members>
        <members>KB_Agentforce_DevOpsSalesforce_HomeLastModifiedByIdDataCategoryCustomLastModifiedByIdYEFOONzwTbyboVK</members>
        <members>KB_Agentforce_DevOpsSalesforce_HomeLastModifiedByIdDataCategoryGroupCustomLastModifiedByIdLONQfZshPxAPcOI</members>
        <members>KB_Agentforce_DevOpsSalesforce_HomeLastModifiedDateDataCategoryCustomLastModifiedDateCndHoHtbLqIpQnb</members>
        <members>KB_Agentforce_DevOpsSalesforce_HomeLastModifiedDateDataCategoryGroupCustomLastModifiedDateiAHazhhobylxHDk</members>
        <members>KB_Agentforce_DevOpsSalesforce_HomeLastModifiedDateKnowledgeArticleVersionLastModifiedDateDSJHLLYmAhJXVuB</members>
        <members>KB_Agentforce_DevOpsSalesforce_HomeMasterLabelDataCategoryCustomMasterLabelBlSFaSxemtEIdld</members>
        <members>KB_Agentforce_DevOpsSalesforce_HomeMasterLabelDataCategoryGroupCustomMasterLabelkBREMmmOVJJkwuc</members>
        <members>KB_Agentforce_DevOpsSalesforce_HomeMasterVersionIdKnowledgeArticleVersionMasterVersionIdaePHmEmEdYmLmam</members>
        <members>KB_Agentforce_DevOpsSalesforce_HomeMigratedToFromArticleVersionKnowledgeArticleVersionMigratedToFromArticleVersionLpJDkFPeDjakmRW</members>
        <members>KB_Agentforce_DevOpsSalesforce_HomeNextReviewDateKnowledgeArticleVersionNextReviewDateTimeiHqwMRLefkjtlWb</members>
        <members>KB_Agentforce_DevOpsSalesforce_HomeParentIdDataCategoryCustomParentIdmYmdjsVydtTJURN</members>
        <members>KB_Agentforce_DevOpsSalesforce_HomeParentIdDataCategorySelectionCustomParentIdVdNdNVPbYbPDryZ</members>
        <members>KB_Agentforce_DevOpsSalesforce_HomePublishStatusKnowledgeArticleVersionKnowledgePublicationStatusxozOJTYMyqBDsgN</members>
        <members>KB_Agentforce_DevOpsSalesforce_HomeQuestion_cKnowledgeArticleVersionQuestion_cdGHpATrREcRboKJ</members>
        <members>KB_Agentforce_DevOpsSalesforce_HomeRecordTypeIdKnowledgeArticleVersionRecordTypeVwtsmFJuiVkTtqj</members>
        <members>KB_Agentforce_DevOpsSalesforce_HomeSortOrderDataCategoryCustomSortOrderbDavCLPbhEjaYtV</members>
        <members>KB_Agentforce_DevOpsSalesforce_HomeSortStyleDataCategoryCustomSortStyleTLTpopzpjExefwJ</members>
        <members>KB_Agentforce_DevOpsSalesforce_HomeStatusDataCategoryGroupCustomStatusAFnZblXZCHZfYVW</members>
        <members>KB_Agentforce_DevOpsSalesforce_HomeSummaryKnowledgeArticleVersionDescriptionUPAyihcvhtnYRuq</members>
        <members>KB_Agentforce_DevOpsSalesforce_HomeTitleKnowledgeArticleVersionNameSTBJThwOPCkoOaO</members>
        <members>KB_Agentforce_DevOpsSalesforce_HomeUrlNameKnowledgeArticleVersionURLhJSKQMBsAVZCJhv</members>
        <members>KB_Agentforce_DevOpsSalesforce_HomeVersionNumberKnowledgeArticleVersionVersionNumberZyNDbAExkmHMcAL</members>
        <members>KB_Agentforce_DevOpsSalesforce_Homeindex_cKnowledgeArticleVersionindex_cBbWuOUzlcQNqdEE</members>
        <name>DataSrcDataModelFieldMap</name>
    </types>
    <types>
        <members>Knowledge_kav_Home_1769978244545</members>
        <name>DataStreamTemplate</name>
    </types>
    <version>66.0</version>
</Package>

```


8.     Save the below xml into "manifest/agentforce-package.xml"  (actual for the  jamp--agent.sandbox)


   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <Package xmlns="http://soap.sforce.com/2006/04/metadata">
       <types>
           <members>Get_Family_Member_Information</members>
           <members>Case_from_Agent</members>
           <name>Flow</name>
       </types>
       <types>
           <members>Answer_Questions_with_Ogdan</members>
           <members>answerWithKnowledge_Override</members>
           <name>GenAiPromptTemplate</name>
       </types>
       <types>
           <members>answerWithKnowledge</members>
           <name>GenAiPromptTemplateActv</name>
       </types>
       <types>
           <members>Answer_Questions_with_Ogdan</members>
           <members>Get_Family_Member_Information</members>
           <members>Case_from_Agent</members>
           <name>GenAiFunction</name>
       </types>
       <types>
           <members>Aliyah_Support</members>
           <name>Bot</name>
       </types>
       <types>
           <members>*</members>
           <name>BotVersion</name>
       </types>
       <types>
           <members>*</members>
           <name>GenAiPlannerBundle</name>
       </types>
       <types>
           <members>*</members>
           <name>DataCategoryGroup</name>
       </types>
       <types>
           <members>Knowledge__kav</members>
           <name>CustomObject</name>
       </types>
       <types>
           <members>MessagingSession.Contact_Id__c</members>
           <name>CustomField</name>
       </types>
       <version>65.0</version>
   </Package>
   
   ```

9. Retrieve the package agentforce-package.xml.
   ```bash
   sf project retrieve start -o SOHNUT-jamp-agent--sandbox -x manifest/agentforce-package.xml
   ```

10. Retrieve the package agentforce-dc-package.xml.
    ```bash
    sf project retrieve start -o SOHNUT-jamp-agent--sandbox -x manifest/agentforce-dc-package.xml
    ```

11. From the package which is retrieved and stored locally, remove the files associated with the following fields (since they are system and created automatically):

    - DataCategorySelectionCustom\_\_dlm.KQ_Id__c
    - DataCategoryCustom\_\_dlm.KQ_Id__c
    - DataCategoryGroupCustom\_\_dlm.KQ_Id__c

12. Go to Aliya_Support.bot-met.xml and change  to the username which was set at the step 10.
    `<botUser>aliyah_support@00dve000003fhm5.ext</botUser>`
    to `<botUser>aliyah_support@00dve000010fhm5.ext</botUser>`

13. Deploy the package manifest/agentforce-dc-package.xml:

    ```bash
    sf project deploy start -o SOHNUT-jamp-agent2--sandbox -x manifest/manifest/agentforce-dc-package.xml
    ```

13. In the T**arget Org**: Setup -> Salesforce CRM -> Jewish Agency => Connect

14. In the **Target Org**: Setup -> Data Kits -> KB Agentforce DevOps => Click on "Data Kit Deploy"

12. Deploy the package manifest/agentforce-package.xml:

```bash
sf project deploy start -o SOHNUT-jamp-agent2--sandbox -x manifest/agentforce-package.xml
```



   

   