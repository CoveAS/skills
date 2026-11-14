---
name: working-with-systemone
description: "Use only when invoked. Runs the working-with-agents skill, but the decider is a local decision model on llama.cpp, called through the System One API. The model scores the options. Claude takes the pick when the model is sure, and gives the user the rest."
---
# Working with System One

Follow the `working-with-agents` skill. Change one thing: the decider is a local decision model. Do not start a sub-agent.

A decision model does not write text. It reads the facts once and gives a probability for each option. So you do the parts of the decider rules that need words.

## Before you send

Apply these decider rules yourself:

- **REJECTED.** Split a question that holds more than one choice. Send one choice per question.
- **NEED CONTEXT.** Find the facts first. The model cannot ask for them.
- **ASK USER.** Give the user every choice that is hard to undo or reaches other people, such as a delete, a push or a message. Do not send it to the model.

## Send the choice

Run this command as it is. Change only `state`, `instructions` and `criteria`.

```bash
PORT=$(ps -ax -o command | grep '[l]lama serve --models-preset' | grep -o -- '--port [0-9]*' | cut -d' ' -f2)
python3 - "$PORT" <<'PY'
import json, sys, urllib.request
base = f"http://localhost:{sys.argv[1]}/v1"
body = {
  "state": "<purpose of the task, the facts, the code, the record of the user's answers>",
  "questions": {"pick": {"type": "choice",
    "instructions": "<the question, in one line>",
    "criteria": {"<short label>": "<the result the user will see with this option>",
                 "<short label>": "<the result the user will see with this option>"}}}
}
models = json.load(urllib.request.urlopen(base + "/models"))["data"]
loaded = [m["id"] for m in models
          if "decisions" in m["architecture"]["output_modalities"] and m["status"]["value"] == "loaded"]
body["model"] = loaded[0] if loaded else "LiquidAI/d1-3B-GGUF:Q4_K_M"
req = urllib.request.Request(base + "/systemone", json.dumps(body).encode(), {"Content-Type": "application/json"})
print(body["model"], json.dumps(json.load(urllib.request.urlopen(req))["answers"]["pick"]))
PY
```

The command finds the Llama.app server and the loaded decision model. When no decision model is loaded, the server loads d1-3B. The first call then takes longer.

If the command fails, tell the user. Then use `working-with-agents` as it is.

Write each criterion as a full description. Bare labels give bad picks.

Keep `state` short and plain. The model has a small context, often 4096 tokens. Quote only the lines that decide the choice.

## Act on the answer

The command prints the model and the answer. `choice` is the top option. `confidence` is the gap between the top two probabilities.

- **Confidence 0.6 or more.** Take the choice. Tell the user in one line what you took, and the probability. Go on.
- **Less than 0.6.** Ask the user in the question shape from `working-with-agents`. Mark the model's pick with ★ only if you agree with it. Add the probabilities to the facts.

If the printed model is not d1-3B, tell the user. Smaller models such as Laya give wrong picks on plain choices.

<!-- ponytail: 0.6 comes from three sample choices on d1-3B. Tune it from the record of the user's answers. -->

Add each answer from the user to the record, as in `working-with-agents`.
