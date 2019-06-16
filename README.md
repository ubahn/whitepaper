# Whitepaper

<img src="https://raw.githubusercontent.com/ubahn/whitepaper/master/ubahn.jpg" alt="Ubahn" width="250"/>

Ubahn is a framework for creating chatbot conversations. Key aspects of Ubahn:
* Developers define a conversation structure in a YAML file.
* Each conversation consists of named inputs and outputs.
* The logic and appearance of inputs and outputs is defined by external applications which use Ubahn.
* The framework doesn’t do any NLP or AI, it doesn’t assume which channel is used for communication. It’s purely about creating a structure of a conversation and building specific implementations on top of that structure.
