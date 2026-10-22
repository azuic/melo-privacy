# Optional vocabulary auto-save

Melo saves words when you ask. To enable auto-save, explicitly ask Claude to use
these instructions in a conversation, or add them yourself to a language-learning
project's instructions. Connecting Melo alone does not opt you in.

## Instructions to enable

I want to save vocabulary from this language-learning conversation to Melo.
When we discuss a new foreign word or expression as something I am learning,
use `save_word` to save that word with a concise meaning and its language.
Include pronunciation, part of speech, examples, translations, and inflections
when known. Omit uncertain details. Save only the vocabulary entry; do not copy
unrelated conversation content or personal information into examples.

Saving the same exact word replaces its existing entry. Respect the client's
permission and confirmation controls. Briefly tell me which words were saved.
Stop auto-saving when I ask you to stop. When I only ask for an explanation
outside this opted-in context, explain it without saving.

Use `search_vocab` for searches and compact browsing. Use `get_vocab` only for
app synchronization or when I explicitly request a full export. Delete a word
or the whole vocabulary only when I request that action, following the client's
confirmation controls.

## To stop

Tell Claude: "Stop saving words to Melo in this conversation."
If you installed these instructions in a project, remove them there to turn
off the preference for future conversations in that project.
