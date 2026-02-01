1. Give permissions to Admin:

   - Knowledge User

2. Assign PS to admin

   - Agentforce Service Agent Configuration	 
   - Agent Platform Builder	 
   - Data Cloud Architect
   - Data Cloud Activation Specialist	
   - Data Cloud Activation Manager
   - Knowledge Manager 
   - Prompt Template Manager	 

3.  Setup -> Data Cloud -> Get Started  => Wait...

4. Setup -> Knowledge Settings 

   - Allow users to create and edit articles from the Articles tab (Classic Only)
   - Allow users to add external multimedia content to HTML in the standard editor (Classic Only)
   - Internal App
   - Customer
   - Partner

5. Setup -> Einstein Setup -> Turn on Einstein 

6. Assign Permission Set License Assignment to Admin

   - Einstein Agent
   - Messaging for In-App and Web User

7. Data Kits -> New -> "KB Agentforce DevOps"

   - Data Stream Bundles  -> Add -> Salesforce CRM (name the bundle as "KnowledgeDataStream") 

     - Knowledge_kav_Home
     - Knowledge_DataCategorySelection_Home
     - DataCategory_Home
     - DataCategoryGroup_Home

   - Search Indexes -> Add -> Ogdan_Knowledge

   - Retrievers  -> Add -> Ogdan Knowledge Retriever (Ogdan_Knowledge_Retriever_1Cx_hm58199f7ec)

   - Press "Download Manifest File" -> Save to the file to "agentforce-dc-package.xml"


8.     Save the below xml into "agentforce-package.xml":


   ```xml
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
           <members>Ogdan</members>
           <name>DataCategoryGroup</name>
       </types>
       <types>
           <members>Knowledge__kav</members>
           <name>CustomObject</name>
       </types>
       <version>66.0</version>
   </Package>
   
   ```

9. Retrieve the package agentforce-package.xml:
   ```bash
   sf project retrieve start -o SOHNUT-jamp-agent--sandbox -x manifest/agentforce-package.xml
   ```
   
   
   
   
   
   