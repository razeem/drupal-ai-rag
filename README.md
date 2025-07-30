# Drupal CMS

Drupal CMS is a fast-moving open source product that enables site builders to easily create new Drupal sites and extend them with smart defaults, all using their browser.

## Getting started

If you want to use [DDEV](https://ddev.com) to run Drupal CMS locally, follow these instructions:

1. Install DDEV following the [documentation](https://ddev.com/get-started/)
2. Open the command line and `cd` to the root directory of this project
3. Run the following commands:
```shell
ddev config --project-type=drupal11 --docroot=web
ddev start
ddev composer install
ddev composer drupal:recipe-unpack
ddev launch
```

Drupal CMS has the same system requirements as Drupal core, so you can use your preferred setup to run it locally. [See the Drupal User Guide for more information](https://www.drupal.org/docs/user_guide/en/installation-chapter.html) on how to set up Drupal.

### Installation options

The Drupal CMS installer offers a list of features preconfigured with smart defaults. You will be able to customize whatever you choose, and add additional features, once you are logged in.

After the installer is complete, you will land on the dashboard.

## Documentation

Coming soon ... [We're working on Drupal CMS specific documentation](https://www.drupal.org/project/drupal_cms/issues/3454527).

In the meantime, learn more about managing a Drupal-based application in the [Drupal User Guide](https://www.drupal.org/docs/user_guide/en/index.html).

## Contributing

Drupal CMS is developed in the open on [Drupal.org](https://www.drupal.org). We are grateful to the community for reporting bugs and contributing fixes and improvements.

[Report issues in the queue](https://drupal.org/node/add/project-issue/drupal_cms), providing as much detail as you can. You can also join the #drupal-cms-support channel in the [Drupal Slack community](https://www.drupal.org/slack).

Drupal CMS has adopted a [code of conduct](https://www.drupal.org/dcoc) that we expect all participants to adhere to.

To contribute to Drupal CMS development, see the [drupal_cms project](https://www.drupal.org/project/drupal_cms).

## License

Drupal CMS and all derivative works are licensed under the [GNU General Public License, version 2 or later](http://www.gnu.org/licenses/old-licenses/gpl-2.0.html).

Learn about the [Drupal trademark and logo policy here](https://www.drupal.com/trademark).

# Ollama Installation and Configuration Using DDEV

## Installation Steps

1. **Install Ollama via DDEV:**
   ```bash
    ddev get stinis87/ddev-ollama && ddev restart
   ```
   ```bash
    ddev ssh -s ollama
    ```
    ```bash
    ollama run mistral:latest
    ```

## Drupal configuration
  - Navigate to : */admin/config/ai/providers*
  - Click Ollama Configuration.
  - Host name : http://ollama
  - Port : 11434
  - Save configuration.

## Testing in drupal
  - Navigate to : *admin/config/ai/explorers*.
  - Click on Chat Generation Explorer.
  - Choose ollama and mistral as its model.
  - Provide a prompt in message section.
  - Click Ask AI.
  - Done. you can see the response!

AI Search in Drupal: A Practical Guide to Smarter Content Discovery
===================================================================

The Drupal community is gaining fresh momentum by integrating AI into what it already does best—structured content management, flexible architecture, and collaborative innovation.

One of the most promising AI applications is **AI-powered search**.

Why AI Search Matters
---------------------

Search plays a central role in user experience. Traditional keyword-based search often fails when users phrase queries naturally or ask complex questions.

**AI Search** addresses this by blending **vector-based retrieval** with **large language models (LLMs)**. This adds semantic context and user intent to the equation—helping users find what they _mean_, not just what they _type_.

What You'll Learn
-----------------

In this guide, we'll walk through integrating AI Search into your Drupal site:

*   Setting up a **vector database** to store semantic embeddings
    
*   Connecting it to your **Drupal content**
    
*   Building a **conversational assistant**
    
*   Using **prompt engineering** to refine tone, accuracy, and depth of responses
    

Whether you're managing a public knowledge base, internal documentation hub, or structured content system, this guide helps you add practical, meaningful AI functionality to your site.

What Is AI Search?
------------------

**AI Search** is a submodule of the [AI module](https://www.drupal.org/project/ai) that extends [Search API AI](https://www.drupal.org/project/search_api_ai), offering tight integration with Drupal’s Search API.

It uses **vector databases** and **LLMs** to enable **semantic search**—meaningful, intelligent matching beyond simple keywords.

### Key Features

*   Built on the popular **Search API** module
    
*   Uses **Retrieval-Augmented Generation (RAG)**: Retrieves relevant data from a vector DB, then sends it to an LLM for accurate, context-aware responses
    
*   Supports full **semantic indexing** and **vector-based search**
    

How It Works
------------

1.  **Content Chunking**: Large content is broken into smaller "chunks".
    
2.  **Vectorization**: Each chunk is converted into a **vector**, a numerical representation of its meaning.
    
3.  **Metadata Storage**: Metadata (e.g., title, tags) is preserved with each chunk.
    
4.  **Query Matching**: User queries are converted into vectors and compared to stored vectors.
    
5.  **Semantic Matching**: Closest matches are returned, offering a much more accurate search than traditional methods.
    

Step-by-Step Setup Guide
------------------------

### Required Modules

Install the following Drupal modules:

*   AI Core
    
*   AI Search
    
*   Search API
    
*   Key
    
*   AI Chatbot
    
*   AI Assistant
    
*   AI Agents
    
*   AI API Explorer
    
*   AI Provider (e.g. Ollama(ai_provider_ollama) )
    
*   Vector Database Provider (e.g., Milvus or Zilliz)
    

### Choosing a Vector Database

- Milvus is recommended for open-source/self-hosted setups.
- Zilliz is the managed SaaS version of Milvus. If using Zilliz, provide your cluster endpoint and API key.

Milvus Configuration
--------------------
For milvus configuration in drupal: (Install and Enable the module [Milvus VDB Provider](https://www.drupal.org/project/ai_vdb_provider_milvus))

1. In your IDE, navigate to: ai_vdb_provider_milvus/docs/docker-compose-examples
    
2.  Copy ddev-example.docker-compose.milvus.yaml
    
3.  Paste it into .ddev/ folder and rename to docker-compose.milvus.yaml
    
4.  Restart ddev: ```ddev restart```

5.  Run ```ddev describe``` to view configurations
    
6.  Locate and open the ***Attu*** interface and Click **Connect** to view the Milvus configuration dashboard (Use the exact URL provided in the ***Attu***).
    
7.  Now navigate to /admin/config/ai/vdb_providers/milvus
    
    *   Server: http://milvus
        
    *   Port: 19530
        
    *   Click **Save Configuration**

    *   Confirmation message: ***The configuration options have been saved.*** Which indicates milvus connection is properly configured.
        

Zilliz Configuration
--------------------
For Zilliz configuration in drupal: (Install and Enable the module [Milvus/Zilliz VDB Provider](https://www.drupal.org/project/ai_vdb_provider_milvus))

1.  Create an account at [Zilliz Cloud](https://cloud.zilliz.com/)
    
2.  Create a cluster (In the dashboard, click **+Cluster**)
    
3.  /admin/config/system/keys
    
    *   Add a key and paste the 'Token' from the cluster into key value
        
    *   Save the key
        
4.  Find **Public Endpoint** in your cluster details tab
    
5.  Navigate to /admin/config/ai/vdb_providers/milvus and use this public endpoint.

    *   Server: *Public Endpoint*
    
    *   Port: 443
        
    *   Select your API key(The token configured in /system/keys)
        
    *   Click **Save Configuration**

    * **Confirmation message**: "The configuration options have been saved."
        

Configure AI Search with Search API
-----------------------------------

1.  Navigate to: /admin/config/search/search-api
    
2.  Click **Add Server**
    
    *   Name: *Give a proper name for the server.*

    *   Enable the server.
        
    *   Backend: AI Search
        
    *   Description: *Provide a description*
        
3.  In the **AI Search Backend Configuration**:
    
    *   **Embeddings Engine**: Ollama | mistral:latest
        
    *   **Tokenizer chat counting model**: (select appropriately)
        
    *   **Vector DB**: Milvus DB

    *   **Database Name**: (you can use default or specify)

    *   **Collection Name**: (enter desired name eg: zillizdbcollection)
        
    *   **Similarity Metric**: Cosine Similarity
        
4.  Click **Save**
    

Create a Search Index (Using 'your_content_type' Content Type)
--------------------------------------------------

1.  Click **Add Index**
    
    *   Name: your_content_type Index
        
    *   Datasource: Content
        
    *   Bundle: your_content_type
        
    *   Server: 'Select your search server created earlier'.
        
    *   Click **Save**
        
2.  In **Fields** tab ( */admin/config/search/search-api/index/ai_content_search/field* ):
    
    *   Add:
        
        *   Rendered HTML output: 
            -   Type : Full Text 
            -   Indexing option: Main Content
            
        *   URL & Title:
            -  Type: String 
            -   Indexing option: Contextual Content
            

    Index Options Explained
    -----------------------

    - Main content: Main body of content, broken into chunks. One field recommended.
    - Context content: Adds helpful context (title, summary, author) to chunks.
    - Filterable attributes: Enables pre-search filtering (e.g., by category/date).
    - Ignore: Excludes field from indexing.


3.  Go to **Views** tab ( */admin/config/search/search-api/index/ai_content_search* ):
    
    *   Set **Batch Indexing**: 5
        
    *   Click **Index Now**

        
**After indexing, view the data in Milvus or Zilliz Cloud to find your content being indexed.**

In Zillis Cloud:(Navigate to Clusters->Click the tab: Collections->Data)

Test Index with AI API Explorer
-------------------------------

1.  /admin/config/ai/explorers/vector_db_generator
    
2.  Input a prompt
    
3.  Select your Search API index
    
4.  Click **Run DB Query**
    
5.  If similarity scores are returned, the index is working.

Set Up AI Agent
---------------

1. Navigate to /admin/config/ai/agents
    
2.  Click **Add AI Agent**
    
    *   Add label and description
        
    *   Check **Swarm Orchestration Agent**

    *   Enable the Project Manager agent if needed.

    *   Provide detailed instructions.
        
    *   Tools: Select RAG/Vector Search Tool
        
3.  Test the tool with ( */admin/config/ai/explorers/tools_explorer* ):
    
    *   Index machine name (your search index)
        
    *   Search string
        
    *   Min score (e.g., 0.3)
        
4.  Under **Property Restrictions**:( Detailed Tool Usage > /admin/structure/ai-agent/ > (edit your agent) )
    
    *   index: Force Value → (index machine name)
        
    *   amount: Force Value → 5
        
    *   min_score: Force Value → 0.3
        
5.  Click **Save**
    

Configure AI Assistant
----------------------

1. Navigate to /admin/config/ai/ai-assistant
    
2.  Click **Add AI Assistant**
    
    *   Use agent as assitant: (e.g., Events Agent)
        
    *   Add label, description, and instructions
        
    *   Agents to use : 'Use the agent you created earlier'.
3.  Under **RAG Actions Configuration**:
    
    *   Enable RAG Action
        
    *   Select RAG Database(Search API index)
        
    *   Threshold: 0.3
        
    *   Max Results: (set appropriately)
        
4.  Select AI Provider (Ollama)
    
5.  Click **Save**
    

Enable AI DeepChatbot Block
---------------------------

1.  /admin/structure/block
    
2.  Place the **AI DeepChatbot block** in a visible region
    
3.  Configure it to use your AI Assistant. (the one you created earlier)
    
4.  Click **Save Configuration**
    

You now have an AI-powered chatbot on your site’s homepage.

Conclusion
----------

**AI Search** in Drupal transforms search from a mechanical keyword match into a nuanced, semantic understanding.

Whether you're suggesting your things based on user preferences or surfacing modules for site builders, AI Search helps your Drupal site respond intelligently—leading to smoother, more helpful digital experiences.

This is just the beginning of how AI is reshaping Drupal's future.

