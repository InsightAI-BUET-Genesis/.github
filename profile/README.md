# InsightAI Technical Documentation

**Authors:** 
- Nazmus Sakib
- Saad Md Rafid Pial

InsightAI consists of three main modules:
1. Study-Companion
2. Project Planner
3. ShopGenie

## 1. Study-Companion

**Study Companion** is an AI-powered study platform that helps organize study materials and enhances productivity using AI. Its core components include:

- Resource Management
- Collection-based Vector DB
- Generating MCQ Quiz
- Generating Flashcards
- Chatting with Knowledge Basis
- Generate Notes

### Resource Management
Organize study materials by any criteria. Create and delete collections, which are groups of materials such as files, web pages, and even YouTube videos. This is managed with:
- **Postgres Database**: Hosted in Supabase, managed by a Spring backend.
- **Vector Database**: Managed in Qdrant.

### Collection-based Vector DB
Create a vector database based on your collection, supporting files, URLs, and YouTube videos. The process involves:
- **File Parsing**: Using Unstructured parsing library for robust parsing-architecture. Semantic chunking is done with Langchain’s semantic chunker, and embedding is done for vector DB storage.
- **URL Parsing**: Content is retrieved using `beautifulsoup4` and cleaned with OpenAI’s GPT-4o-mini model.
- **YouTube Video Parsing**: Subtitles are retrieved using `youtube-transcript-api` and processed similarly to a text file.

### Generate MCQ Quiz
Generate quizzes based on selected files, with options for difficulty level and number of questions. The workflow includes:
- Retrieving chunks from the vector DB.
- Sorting chunks by page number.
- Generating quiz questions, answers, and explanations using OpenAI’s GPT-4o-mini model.

### Generate Flashcards
Flashcards can be generated similarly to quizzes, with additional schema including:
- Questions
- Answers
- Step-by-step explanations
- Tips and tricks

### Chatting with Knowledge Basis
Users can chat with their knowledge base at both file and collection levels, supported by Qdrant and OpenAI’s GPT-4o-mini model. The model can be augmented to behave as a teacher, storyteller, summarizer, researcher, code assistant, etc.

### Note Generation
Generate notes that include both vector DB search and web search. The workflow includes:
- Collecting user parameters.
- Fetching vector chunks.
- Searching for relevant YouTube videos.
- Generating notes with examples, Q&A, tips, tricks, and YouTube video links.

## 2. Project Planner

**Project Planner** is an AI assistant that helps plan projects with the following components:

### Database Integration
- Users provide the project title and description.
- A customized web search is performed using Serper API to find related projects.
- The results are cleaned and processed by the GPT-4o-mini model.
- A Pydantic schema guides the user with the project plan, which includes setting time and goals for subtasks.

## 3. ShopGenie

**ShopGenie** is an AI-powered shopping platform with the following components:

### Data Scraping
- Data scraped from major fashion brands in Bangladesh using Selenium and parsed with `beautifulsoup4`.

### Data Processing & Hosting
- Normalization of field names and consistency across product records.
- Dataset hosted on Huggingface: [Product Dataset](https://huggingface.co/datasets/Melikshah/products).

### Data Augmentation
- Product descriptions generated using the LLaVA (Language and Vision Assistant) model.
- Poorly formatted descriptions are improved using the same model.

### Vector Database
- Hosted in Qdrant with vectors for both images and text:
  - Image embedding using `clip-ViT-B-32`.
  - Summary embedding using `text-embedding-3-large`.
- Products can be retrieved using text, image, or a combination of both.

### Product Recommendation
- Recommendation system based on a best-score strategy, finding vectors closest to positive examples and avoiding negative ones.

### Sentiment Analysis for Product Reviews
- Sentiment is measured using OpenAI’s GPT-4o-mini’s structured output, categorizing reviews as positive, negative, or neutral.

## System Architecture

InsightAI uses a microservice-based architecture with the following components:

- **Frontend**: Developed in SvelteKit.
- **Backend Services**:
  1. **Database**: Spring backend handling interactions with Postgres database, hosted in Supabase.
  2. **LLM Tasks**: FastAPI backend handling AI and RAG-related tasks. API documentation: [InsightAI Python Backend](https://insightai-6hp4.onrender.com/docs).
  3. **Scraping**: Cron-job based service for scraping and updating vector points in Qdrant.
  4. **Vector DB and Data Augmentation**: Service for data cleaning and augmentation using the LLaVA model.
  5. **Auth Flow**: Handled by SvelteKit using Supabase Auth.

## System Architecture Diagram
![System Architecture](https://fgdanyiprenrzvmxnjxw.supabase.co/storage/v1/object/public/statics/system_architecture_insightAI.png)

## Workflow Diagram

### Study Companion Module
The Study Companion module consists of two main components:

1. **Resource Management**
![Study Companion - Resource Management](https://fgdanyiprenrzvmxnjxw.supabase.co/storage/v1/object/public/statics/stud_companion_1.png)

2. **Productivity (Note Generation, Quiz & Flashcards)**
![Study Companion - Productivity](https://fgdanyiprenrzvmxnjxw.supabase.co/storage/v1/object/public/statics/stud_companion_2.png)

### Project Planner Module
![Project Planner](https://fgdanyiprenrzvmxnjxw.supabase.co/storage/v1/object/public/statics/project_planner.png)

### ShopGenie Module
![ShopGenie](https://fgdanyiprenrzvmxnjxw.supabase.co/storage/v1/object/public/statics/genie.png)

These diagrams provide a high-level overview of the system flow for each module in the InsightAI application. They illustrate the key components and interactions within each module, helping developers and stakeholders understand the overall architecture and data flow.

## Additional Resources
- [Product Dataset](https://huggingface.co/datasets/Melikshah/products)
- [InsightAI Python Backend API Documentation](https://insightai-6hp4.onrender.com/docs)

