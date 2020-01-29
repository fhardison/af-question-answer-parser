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

Note that questions do not require the presence of a corresponding answer.

Finally, any line in the question file starting with `#` is considered a comment and will be ignored.

See `test_questions.txt` for more examples.

## Usage

If you pull this repo and run the following, the you should display the what is found in `qoutput.md` on your terminal window. You can then pipe this into whatever file you want and you've got markdown formatted questions.

```
python3 qaparser.py test_questions.txt 015-diognetus.txt
```

If run as above, the script will output the text and then any questions and answers pertaining to that text without repeating the text.

Adding `--show-text True` will cause it to repeated the text before each question. If you use `--show-text True` you can add `--bold-text True` to bold the words in the text that the question pertains to.

Run the following commands to see how this works.

```
python3 qaparser.py test_questions.txt 015-diognetus.txt --show-text True > qoutput-text.md
```

```
python3 qaparser.py test_questions.txt 015-diognetus.txt --show-text True --bold-text True > qoutput-text-bold.md
```

Markdown is the default output format. You can change to reveal.js output by adding `--format reveal`. The line below will create a reveal.js html file and pipe it to `reveal-test.html`.

```
python3 qaparser.py test_questions.txt 015-diognetus.txt --format reveal > reveal-test.html
```

## License

This work is licensed under a [Creative Commons Attribution-ShareAlike 4.0 International License](http://creativecommons.org/licenses/by-sa/4.0/).

The following files are from [reveal.js](https://github.com/hakimel/reveal.js/) and are released there under an MIT license as described on that repo.

* `reveal.js`
* `reveal.css`
* `reset.css`
* `black.css`
