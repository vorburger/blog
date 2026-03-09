# How I am prompting LLMs?

https://huggingface.co/blog/jdelavande/thank-you-energy is an interesting article.

What it doesn't mention is the "exponential" cost of saying _"Thank You"_ at the end of a long conversation...
as each follow-up prompt must send the entire conversation, real world energy consumption is likely much higher than
the "synthetic" _Thank You_ on an empty context.

Personally I'm currently typically prompting LLMs like this:

1. I create new sessions, instead of never ending long conversations (e.g. /clear in Gemini CLI).
2. I use "imperative" language ("do", not "could" or "please")
3. I don't send any follow-up prompt when the task at hand is completed to my satisfaction
4. I on (pretty rare) occasions still can't quite avoid an "oh wow, you're awesome" 😀

Sending a "Thank You" to an LLM as the last prompt to end a conversation does not like a good idea energy wise.

But I'm not sold on the energy impact of using _"Please"_ **within** an initial or otherwise required follow-up prompt.
That 1 additional token is unlikely going to make a measurable difference (even at scale), IMHO.
