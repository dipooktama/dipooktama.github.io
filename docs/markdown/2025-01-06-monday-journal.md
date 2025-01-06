---
title: Monday Journal
author: Dipo Oktama
datetime: 2025-01-06 21:49:46
summary: My recap on things that went on monday 6th Jan 2025.
---

# Monday Journal

Today is monday. Actually I didn't do much on this day. Well, I did sold some foods.
I also solved a mundane problem at the office. But still, I don't think I did much today.

I also felt a bit lazy today. But, I finally solved the problem on how to handle the LLM chat stuffs.
All this time, I'm stuck on how to make it so that the user can send a message,
and got the stream reply by the llm, but then that response could be saved to the db too?

## so here is how I solved it!

1. user send the message via `POST` request
2. the `FastAPI` backend then saved it to db, and respond back with that saved message's id.
3. in the client, after completing sending the message, it then open an `SSE` connection to the server, sending the `chat_id` too.
4. the `FastAPI` backend then fetch that `chat_id`, and fetchs the other 20 latest message.
5. then, it create a **convo buffer**, which then sent to the LLM service which will respond with a stream of chunked string.
6. the backend then streamed back the content to the client.
7. **BUT**, before it sends the `EOF` chunk, it actually save the cummulated string to the DB (flagged as the llm's message)
8. sending the EOF.

Actually I consult this stuffs with [deepseek](https://www.deepseek.com/), but it gives me complex solution like using redis, etc.
(which actually synergized with my first thought to use some kind of background process/worker).

All in all, this monday is going kinda well.
