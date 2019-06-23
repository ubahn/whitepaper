# Whitepaper

<img src="https://raw.githubusercontent.com/ubahn/whitepaper/master/ubahn.jpg" alt="Ubahn" width="250"/>

Ubahn is a framework for creating chatbot conversations. Key aspects of Ubahn:
* Developers define a conversation structure in a YAML file.
* Each conversation consists of named inputs and outputs.
* The logic and appearance of inputs and outputs is defined by external applications which use Ubahn.
* The framework doesn’t do any NLP or AI, it doesn’t assume which channel is used for communication. It’s purely about creating a structure of a conversation and building specific implementations on top of that structure.
* Named after Munich subway system of the same name.

Here’s an example of a conversation:

```yaml
version: 1

sequence:
  - welcome
  - weather-report

triggers:
  - i-user-welcome

fallback: clarification

outputs:
  welcome:
    expectedInputs:
      i-yes: next
      i-no: bye
    fallback: welcome-clarification
```

* `version: 1` defines Ubahn protocol version number. It’s useful if we introduce breaking changes to the format of conversation file.
* `sequence` outlines the structure we want to have in the conversation. It should have a list of named agent outputs, in order of their appearance. Even though the structure is linear, Ubahn supports conditional jumps.
* `triggers` is a list of named inputs that trigger conversation start.
* `fallback` defines the global fallback output which is called when Ubahn doesn’t know which output to call.
* `outputs` defines named agent outputs. Each output may have a dedicated `fallback` and may expect many inputs. For example in this case:
```yaml
i-yes: next
i-no: bye
```
we say that if user input was `i-yes`, the conversation goes to the next element (`weather-report`), if the input was `i-no`, the conversation goes to the `bye` output.

You may wonder, where do we have those `weather-report`, `bye`, `i-yes` etc.? All of them are just names. You should use Ubahn API to map those names to specific entities with business logic.
For example `weather-report` output may be a rich UI, or a picture—whatever. `bye` maybe a smile, or a text. `i-yes` is how your implementation interprets Yes answer, and btw you don’t have to name it `i-yes`, this is just an example.

Here’s how the above conversation may look like in real life:

<img src="https://raw.githubusercontent.com/ubahn/whitepaper/master/ubahn-sample.png" alt="Ubahn Sample" />
