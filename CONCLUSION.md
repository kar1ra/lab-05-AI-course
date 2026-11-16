# Lab 05 — Conclusion

<!--
Read this before you write.

This file is graded by your instructor, by hand, and it is worth 6 of the 15 points.

- Type it yourself. Do not use a chatbot, an AI assistant, an AI autocomplete or a "rewrite my
  text" tool for any part of it, not even for grammar. English that is plain and a little
  clumsy but yours is better than polished text that is not.
- Use your own numbers. Every number you quote must be one your own notebook printed. Copy
  the number exactly as it appeared. A number your notebook did not print is marked as wrong.
- Answer in your own words, about 80-200 words per question. A short answer that uses your
  numbers beats a long answer that could have been written by anyone.
- Delete these comment lines if you like. Keep the three headings and the last line.
-->

## 1. Which layer changed your results the most?

Give the numbers before -> after for that layer (correct / wrong / no answer, out of 20) and say
whether it changed what the agent *can do* or only what it *admits*. If no layer changed the
number of correct answers, say so and explain what the layers did change instead.

(write here)
Layer 1 changed my results the most. The bare agent had 16 correct, 4 wrong and 4 no answer out of 24. With layer 1 it had 18 correct, 6 wrong and 0 no answer. This layer changed what the agent can do. When a tool did not know a region name, the error went back to the model, and the model could try again. Because of this, q23 and q24 became correct. But q21 and q22 became wrong answers instead of no answer, so wrong went up from 4 to 6. Layer 2 changed nothing: it had the same 18, 6, 0, the same 62 model calls and the same 48708 tokens. Layer 3 only changed what the agent admits: 18 correct, 4 wrong, 2 no answer. Two wrong answers became no answer, but the number of correct answers stayed 18

## 2. One failure the full harness did not fix

Pick one question that the full harness (layer 3) still gets wrong or refuses. Give its id
(q01 ... q20). Open its trace in the notebook: at which step did it go wrong, and what did
the model do instead? Name one thing you would add to the harness, and what it would cost
(extra model calls, tokens, time, or a new way to fail).

(write here)
q21 is still wrong with layer 3. The question asks about Nur-Sultan, and the answer was 3.9%. In the first step the model used the name Nur-Sultan and the tool said it was an unknown region. In the second step the model called list_regions, which was good. In the third step it asked for Almaty City, but the correct region is Astana. The tool gave 3.9 for Almaty City, so the number really came from a tool and layer 3 accepted it. I would add a check that the region in the last tool call matches the region from the question. It would cost at least one more model call for these questions, more tokens, and it could fail in a new way, because the same small model could match the name wrongly again

## 3. Workflow or agent for the monthly ranking?

Dala Insight wants to publish, every month, "which region is highest and which is lowest on one
indicator in one year". Would you ship the fixed workflow or the agent? Use the accuracy, the
number of model calls, the tokens and the time you measured in Part 1. Then say in one sentence
what kind of question would make you choose the other one.

(write here)
I would ship the fixed workflow. On the 15 fixed-shape questions the workflow got 13 correct, 0 wrong and 2 no answer. It used 15 model calls, 3852 tokens and 16.2 seconds. The bare agent got 9 correct, 2 wrong and 4 no answer. It used 26 model calls, 19835 tokens and 49.3 seconds. So the workflow was more accurate, cheaper and faster. Its two failures (q21 and q22) were no answer, not a wrong number, so a person can see them. The agent gave wrong answers on q08 and q11. Only 15 questions is not many, and the intervals overlap, so this is not proven. I would choose the agent for an open question, for example a percent change, because the workflow has no shape for it

---

I wrote this file myself, without any AI tool.
