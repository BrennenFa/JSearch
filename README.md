# JSearch

https://chat-epstein.vercel.app/


What I built:
Political misinformation has been a huge issue in the internet age. This has been very applicable to the release of the Epstein files. While there’s been a lot of information about Epstein released in the past year, much of it is very unorganized. This makes it hard to decipher what’s true, false, or nonexistent. There have been platforms like jmail.world (put files in a gmail format) that attempt to address this, but they still contain a wide array of information that is difficult to search through quickly.
To solve these issues, I created JSearch, a RAG chatbot with access to text-based data in the Epstein files to provide a more targeted, accessible search. This tool includes almost 300,000 documents from various recent sources that the chatbot uses to provide information. With all queries, results are quoted, and a link to the source is provided. This helps prevent the dangers of hallucinations, which can lead to more misinformation that can be very harmful and contrary to the tool’s purpose to begin with.




How I built it:
For initial storage, I put all the files in an AWS S3 bucket. Then, I processed all data into Pinecone as a vector database. For my chunking strategy, I initially used a character count of 1024 for each chunk, which worked well for long, multipage documents. However, since many of the documents are single-page and have a lot of continuous context, I switch to a page-based chunking strategy. Additionally, I am used spAcy to find people, places, and geopolitical entities. Sources, file name, and entities were stored as metadata.
During the retrieval phase, I used a hybrid search, fetching both using traditional query methods and entity-based matching with the query. Doing both of these gives me more accurate but diverse results. I am also having it keep track of the last 2 2 exchanges (4 messages: 2 user + 2 assistant). Overall, this gives me a token usage of 2k-4k per query. Because I’m a semi-broke college student, I used Groq’s cheap llama-3.1-8b-instant API.

Why it’s worth sharing:
Although not the most lines of code, this is my favorite project I’ve built to date. It tackles a real world problem of a lack of accessible access to important documents, and as such, had about 1,000 searches the week it was released. This demonstrates a real-world scale. Additionally, it forced me to address very complex, non-deterministic problems. For example, managing the trade-off between token usage, speed, and accuracy was an issue I had to really think about, and ended leading to my usage of hybrid search. By combining this problem with a modern AI tech stack, I am very proud of this project.


Link here: https://chat-epstein.vercel.app/
