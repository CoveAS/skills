---
name: working-with-systemone
description: "Use only when invoked. Runs the working-with-agents skill, but the decider is a local decision model on llama.cpp, called through the System One API. The model scores the options. Claude takes the pick when the model is sure, and gives the user the rest."
---
# Working with System One

Follow the `working-with-agents` skill. Change one thing: the decider is a local decision model. Do not start a sub-agent.

A decision model does not write text. It reads the facts once and gives a probability for each option. So you do the parts of the decider rules that need words.

## Find the model

1. Run `lsof -iTCP -sTCP:LISTEN -nP | grep llama` to find the ports.
2. Run `curl -s http://localhost:<port>/v1/models` on each port until one lists models.
3. Pick the model with `"output_modalities":["decisions"]` and status `loaded`. Use its `id`.

Use `LiquidAI/d1-3B-GGUF`. Smaller models such as Laya give wrong picks on plain choices.

If no decision model is loaded, tell the user. Then use `working-with-agents` as it is.

## Before you send

Apply these decider rules yourself:

- **REJECTED.** Split a question that holds more than one choice. Send one choice per question.
- **NEED CONTEXT.** Find the facts first. The model cannot ask for them.
- **ASK USER.** Give the user every choice that is hard to undo or reaches other people, such as a delete, a push or a message. Do not send it to the model.

## Send the choice

POST to `http://localhost:<port>/v1/systemone`:

```json
{
  "model": "<id>",
  "state": "<purpose of the task, the facts, the code, the record of the user's answers>",
  "questions": {
    "pick": {
      "type": "choice",
      "instructions": "<the question, in one line>",
      "criteria": {
        "<short label>": "<the result the user will see with this option>",
        "<short label>": "<the result the user will see with this option>"
      }
    }
  }
}
```

Write each criterion as a full description. Bare labels give bad picks.

Keep `state` short and plain. The model has a small context, often 4096 tokens. Quote only the lines that decide the choice.

## Act on the answer

The answer is in `answers.pick`. `choice` is the top option. `confidence` is the gap between the top two probabilities.

- **Confidence 0.6 or more.** Take the choice. Tell the user in one line what you took, and the probability. Go on.
- **Less than 0.6.** Ask the user in the question shape from `working-with-agents`. Mark the model's pick with ★ only if you agree with it. Add the probabilities to the facts.

<!-- ponytail: 0.6 comes from three sample choices on d1-3B. Tune it from the record of the user's answers. -->

Add each answer from the user to the record, as in `working-with-agents`.
