# Models

Models are the base of any Django application, and using Django's ORM approach
a model --> a Python class --> a table in the database. For HelpMe Server, we define
the following models:

## Metadata Models

 - **Environment**: Environment corresponds with a dictionary of variables and their values extracted from the runtime environment. An environment is typically closed off to all except for administrators of the user institution.
 - **Capture**: A capture is an asciinema that illustrates the problem at hand. Users are instructed to not include any credentials or secrets in asciinemas, as they are by default public. An admin (or the owner) of an asciinema can always choose to make one private, if necessary.

## Knowledge Models

 - **Message**: a message is the most basic unit of knowledge. It can be a question or an answer, and in both cases the message can have topics and is owned by a user or admin.
 - **Post**: a post in single question and a set of answers. A post is what gets generated when a user submits a question to the application, optionally with an environment and/or capture to give information about the problem. A post is specific in that it is asking a question specific to a user, or cluster resource. A post can belong to one or more topics.
 - **Topic**: A topic is a general question or idea that one or more posts belong to. A topic can be determined manually (e.g., an admin reads a post and assigns it to a topic) or with machine learning (algorithms automatically classify new posts into categories). Importantly, each topic is matched to a version controlled, single collaborative answer that is developed to answer the general question by those that are administrators of the application.


# Structures

```
Structure of a Topic

Topic

   - name: "How do I log into a SLURM cluster?"
   - permissions: admin
   - format: wiki general answer

   Posts:
       - permissions: everyone
       - format: forum / Q&A board (upvote / downvote)
       - tags

       post 1:
           Question: "How do I log into Sherlock?"
           Answer1...AnswerN     
    
       post 2: 
           Question: "Why does my login not work?"
           Answer1..AnswerN


Structure of a Post

    - question
    - answers
    - environment (private) only accessible by admins

```

# Flows

```
Creation of Post Flow:

[cluster] --> [helpme] --> [POST asciiema] --> [create new post]
                                                 - tags

Classification of Post (Manual):

    Admins NEW post 1 --> [ write answer ] --> [ organize ]
           NEW post 2


Classification of Post (Machine Learning)

    [asciinema] --> extract executables from commands
    [environment] --> extract higher level bits
    [question] --> word2vec of question


Search of Post (with and without classification):

    Search "login" --> post 1
                       post 2
```
