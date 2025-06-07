# Google Agent Development Kit (ADK) for Java with Ollama

Guillaume Laforge [is exploring building a LangChain4j LLM Adapter for the Google Agent Development Kit, ADK](https://glaforge.dev/posts/2025/06/05/expanding-adk-java-llm-coverage-with-langchain4j/).

I decided to take it for a spin, and see if I can get this to work e.g. with
[Gemma](https://deepmind.google/models/gemma/) running on [Ollama](https://ollama.com).

We also wanted this to "just work" for other users, so I've done some work to put together
a few of the missing pieces which aren't merged into the https://github.com/google/adk-java repo just yet
(we working on it!) to be able to make it available via https://jitpack.io, by currently still pulling
and building it from a branch on the temporary fork at https://github.com/enola-dev/adk-java
instead of the origin upstream https://github.com/google/adk-java.

The resulting demo is now on https://github.com/enola-dev/LearningADK, and you could try it like this:

```sh
$ ollama pull gemma3:4b
$ git clone https://github.com/enola-dev/LearningADK
$ cd LearningADK
$ ./run-cli.sh "hi, who are you and what can you do?"
[INFO] Scanning for projects...
[INFO]
[INFO] ---------------------< dev.enola.adk:langchain4j >----------------------
[INFO] Building langchain4j 0.0.1-SNAPSHOT
[INFO]   from pom.xml
[INFO] --------------------------------[ jar ]---------------------------------
[INFO]
[INFO] --- resources:3.3.1:resources (default-resources) @ langchain4j ---
[INFO] skip non existing resourceDirectory /home/vorburger/git/github.com/enola-dev/LearningADK/LangChain4j/src/main/resources
[INFO]
[INFO] --- compiler:3.13.0:compile (default-compile) @ langchain4j ---
[INFO] Nothing to compile - all classes are up to date.
[INFO]
[INFO] --- exec:3.5.1:java (default-cli) @ langchain4j ---
19:23:02.450 [dev.enola.adk.learn.OllamaWithoutTools.main()] INFO dev.langchain4j.http.client.log.LoggingHttpClient -- HTTP request:
- method: POST
- url: http://localhost:11434/api/chat
- headers: [Content-Type: application/json]
- body: {
  "model" : "gemma3:4b",
  "messages" : [ {
    "role" : "system",
    "content" : "You are an agent. Your internal name is multi_tool_agent. The description about you is Ollama"
  }, {
    "role" : "user",
    "content" : "hi, who are you and what can you do?"
  } ],
  "options" : {
    "stop" : [ ]
  },
  "stream" : false,
  "tools" : [ ]
}

19:23:19.445 [dev.enola.adk.learn.OllamaWithoutTools.main()] INFO dev.langchain4j.http.client.log.LoggingHttpClient -- HTTP response:
- status code: 200
- headers: [content-length: 1150], [content-type: application/json; charset=utf-8], [date: Sat, 07 Jun 2025 17:23:19 GMT]
- body: {"model":"gemma3:4b","created_at":"2025-06-07T17:23:19.433520588Z","message":{"role":"assistant","content":"Hello there! I'm Ollama, and I'm a multi-tool agent. Think of me as a helpful assistant that can do a wide variety of things. \n\nEssentially, I'm built to be flexible and adaptable. I can:\n\n*   **Answer your questions:** I can provide information on a huge range of topics, drawing on my knowledge base.\n*   **Generate text:** Need a poem, a story, a code snippet, or a different creative text format? I can generate it for you.\n*   **Translate languages:** I can translate text between many different languages.\n*   **Summarize text:**  I can condense large amounts of text into shorter, more manageable summaries.\n*   **And much more!** I'm still under development and constantly learning new things.\n\nBasically, I’m here to help you with whatever you need – just let me know what you have in mind!\n\nDo you want to try something out?"},"done_reason":"stop","done":true,"total_duration":16944139462,"load_duration":50999699,"prompt_eval_count":47,"prompt_eval_duration":1055489650,"eval_count":204,"eval_duration":15836903855}

Hello there! I'm Ollama, and I'm a multi-tool agent. Think of me as a helpful assistant that can do a wide variety of things.

Essentially, I'm built to be flexible and adaptable. I can:

*   **Answer your questions:** I can provide information on a huge range of topics, drawing on my knowledge base.
*   **Generate text:** Need a poem, a story, a code snippet, or a different creative text format? I can generate it for you.
*   **Translate languages:** I can translate text between many different languages.
*   **Summarize text:**  I can condense large amounts of text into shorter, more manageable summaries.
*   **And much more!** I'm still under development and constantly learning new things.

Basically, I’m here to help you with whatever you need – just let me know what you have in mind!

Do you want to try something out?
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time:  19.361 s
[INFO] Finished at: 2025-06-07T19:23:19+02:00
[INFO] ------------------------------------------------------------------------

$
```

There is still some work left to "fully integrate this upstream", and perhaps iron out some kinds.

Enjoy!
