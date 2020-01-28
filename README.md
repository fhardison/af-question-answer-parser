# AF question and answer parser

This script will parse a question file and read a corresponding file containing the text the questions are about. It will then extract the text being questioned and output the text, questions, and answers (if there are any).

## Output format

Currently it exports a vary basic markdown output. I hope to expand it to use `reveal.js` and other outputs as well.

## Text file format

The script doesn't really care what the format of the file containing the text being asked about is, as long as each line has some kind of line number or address that doesn't contain `@`. The script was, however, created with format used by James Tauber and Seumas Macdonald's [Apostolic Fathers](https://github.com/jtauber/apostolic-fathers) format in mind.

I have taken `015-diognetus.txt` from their repo and used it as an example file. It is therefore not to be used except under the terms of the [Creative Commons Attribution-ShareAlike 4.0 International License](http://creativecommons.org/licenses/by-sa/4.0/) they have applied to that work.

## Question file format

```
ref-to-text-in-file@words-being-asked-about.questions-num.question-or-answer qustion/answer content
```

The first part of each line is a reference that tells the script what part of the text the question pertains to and some other details about the question.

Then comes an `@` followed by the details about the questions separated by a `.`.

* the word or words in the text the question refers to. This can be a range that is separated by `-`. `1` and `1-4` are valid. This is a 0 based index.
* The question number. This must be unique for each question (a question and its answers must share the same number).
* The type of the line. `q` for a question and `a` for an answer.

The line below is about line `2.5` in the text file. It asks about the first word in the sentence. It is the first question about this word and this is the question.

```
2.5@0.1.q τὶ σημαίνει τὸ ταῦτα;
```

This line is the answer for the question above.

```
2.5@0.1.a τα καλοῦνται θεούς;
```

See `test_questions.txt` for more examples.

## Example usage

If you pull this repo and run the following, the you should display the what is found in `qoutput.md` on your terminal window. You can then pipe this into whatever file you want and you've got markdown formatted questions.

```
python3 qaparser.py test_questions.txt 015-diognetus.txt
```



## License

This work is licensed under a [Creative Commons Attribution-ShareAlike 4.0 International License](http://creativecommons.org/licenses/by-sa/4.0/).