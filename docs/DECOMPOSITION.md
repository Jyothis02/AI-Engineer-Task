## 1. The problem in my own words

Long chats may be difficult to read for a third person , finding important details and context through many messages will be time consuming , instead of the human reading through hundreds of messages , we build a chat analyzer which can answer questions based on the chat we provide. 

## 2. What I noticed in the data

  i> Chat is consisted of two language format -> English and Hinglish , in the same sentence which can confuse the AI as certain words are same in English and Hinglish but has different meaning 
         "05/10/26, 8:11 PM - Kabir: search aur chat dono? thoda zyada hai but ok"  ,  'hai' can be interpreted in two different way , same for 'main'.
  
  ii> 5 people conversing at the same time but context may be different for each , which can lead to confusion on what a person may be responding to.
         "09/10/26, 10:42 PM - Priya: ye screenshot hai, filters abhi nahi hain
          09/10/26, 10:55 PM - Rohan: nice. clean hai
          09/10/26, 10:56 PM - Aarav: color thoda dull hai but fine
          12/10/26, 7:30 PM - Meera: Reminder: report due 3 days before demo day. Demo day 4 Dec so report 1 Dec
          12/10/26, 7:32 PM - Aarav: noted
          12/10/26, 7:33 PM - Kabir: mujhe lagta hai hum late chal rahe hain"
          
  iii>  Images are present and are key part of the chat but is not available , hence making out the relevance of the image is entirely upon the replies that it gets.
         "24/10/26, 11:27 PM - Rohan: <Media omitted>
          24/10/26, 11:27 PM - Rohan: ye schema ka diagram, v1"
          
  iv> Context keeps on changing , therefore the AI has to go through all of the chat to declare a final result
          "05/10/26, 8:10 PM - Meera: payments Razorpay se karungi
           20/10/26, 8:16 PM - Aarav: agreed. final decision: no Razorpay, UPI QR manual
           02/11/26, 8:49 PM - Aarav: haan. Razorpay test mode final. QR wala scrap."
           
  v>

## 3. The simplest thing that could work, and how it would fail

Simplest thing would be to upload the file to AI and get answers, which would not be optimal as it needs to have a context on the matter  and when dealing with large quantity of chat, it can get expensive. 

## 4. Break it into sub-problems

smaller problems would be to manage the chat dataset in a way so that it can be used economically without wasting tokens. Using a RAG pipeline or something similar can make it better.

                  WHATSAPP TXT EXPORT
                          |
                          v
              +-----------------------+
              |   PYTHON PREPROCESSOR  |
              |                       |
              | - Parse messages      |
              | - Extract timestamps  |
              | - Extract senders     |
              +-----------------------+
                          |
                          v
              +-----------------------+
              |       CHUNKING        |
              |                       |
              | - Group messages      |
              | - Preserve context    |
              | - Add metadata        |
              +-----------------------+
                          |
                          v
              +-----------------------+
              |    EMBEDDING MODEL    |
              |                       |
              |  Text -> Vectors      |
              +-----------------------+
                          |
                          v
              +-----------------------+
              |     VECTOR STORE      |
              |                       |
              |       ChromaDB        |
              |                       |
              | - Embeddings          |
              | - Original text       |
              | - Metadata            |
              +-----------------------+
                          |
                          |
             USER ASKS A QUESTION
                          |
                          v
              +-----------------------+
              |   QUESTION EMBEDDING  |
              |                       |
              | Convert query to      |
              | numerical vector      |
              +-----------------------+
                          |
                          v
              +-----------------------+
              |     RETRIEVAL         |
              |                       |
              | - Similarity search  |
              | - Find relevant      |
              |   message chunks      |
              +-----------------------+
                          |
                          v
              +-----------------------+
              |    CONTEXT BUILDER    |
              |                       |
              | Question + Retrieved |
              | messages + metadata   |
              +-----------------------+
                          |
                          v
              +-----------------------+
              |       GPT API         |
              |                       |
              | - Understand context |
              | - Reason             |
              | - Generate answer    |
              +-----------------------+
                          |
                          v
              +-----------------------+
              |     FINAL ANSWER      |
              |                       |
              | - Answer             |
              | - Dates               |
              | - Supporting messages |
              +-----------------------+

## 5. What I don't know yet

in-depth knowledge of RAG architecture which i am planning on studying through youtube.

## 6. Build order

first build a system which connects an AI agent through an API and through which i can do basic tasks. Then implement the RAG pipeline to make it better.

## 7. Where I'll use AI, and where I won't

AI agent will be used for reasoning and forming the final result. Apart from that i will be using it for RAG architecture and i would like to do the system design by myself as i have attended a hackathon on AI agents where i learned how RAG can be implemented and the need for it.
