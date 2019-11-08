# NaNoAbMo
Entries for National Novel Abridgment Month, November 2019.

It might be fun to use algorithms to extract new works from public domain novels by selectively removing words. I guess I'll find out.

For this project, I'm sourcing my public domain novels from the [Standard Ebooks](https://standardebooks.org/) project.

## 1
[Anne of Green Gables, by L.M. Montgomery](./01-l-m-montgomery_anne-of-green-gables.md)

This algorithm starts by recording the first word in the book. Then it reads ahead until that same word is encountered again. It records the subsequent word, and again reads ahead until this new word is encountered again. The process repeats until the end of the book is reached.

If the algorithm fails to find a word (because it's starting from the last occurrence in the book), it returns to where it started and continues to the next word instead. As a result, the last several words of the book are usually copied word-for-word.

This algorithm (or something like it) was described by John Pierce in *Symbols, Signals and Noise*, where he credits it to Claude Shannon.

## 2
[The Adventures of Sherlock Holmes, by Arthur Conan Doyle](./02-arthur-conan-doyle_the-adventures-of-sherlock-holmes.md)

The code is very simple at the moment. It looks for exact word matches, including capitalization and surrounding punctuation. For example, "Doctor" would not match "Doctor," or "doctor".

## 3
[Twenty Thousand Leagues Under the Sea, by Jules Verne](03-jules-verne_twenty-thousand-leagues-under-the-seas.md)

The source files that I'm getting from Standard Ebooks are collections of xhtml files, with each chapter in a separate file. This script discards all the xhtml tags, discards chapter titles, and joins the chapter text together before running the resulting text through the "abridger" algorithm.

I'm also discarding any sections that aren't part of the main body of work (such as introductions, colophons, and so on).

## 4
[The Secret Adversary, by Agatha Christie](04-agatha-christie_the-secret-adversary.md)

I tried changing the algorithm to ignore adjacent punctuation, but the results were unsatisfying. The output wasn't as coherent as earlier results, and not much longer (which is what I was primarily hoping for).

In hindsight, I suppose that this makes sense. Including the punctuation in the search pattern means that every pair of consecutive words appeared exactly as-is in the original work. It's reasonable that this would increase coherence at the expense of originality and variety, and discarding the punctuation would do the opposite.

I gave up on this for now and went back to the punctuation-included code.

## 5
[Pride and Prejudice, by Jane Austen](05-jane-austen_pride-and-prejudice.md)

Speaking of punctuation, Pride and Prejudice is the only work I've tested so far that produces exactly one sentence (long and convoluted though it is, as you would expect from this kind of exercise).

## 6
[Silas Marner, by George Eliot](06-george-eliot_silas-marner_r13.md)

My second approach to making the output longer is to search again from the beginning if a match isn't found in the remainder of the book. Depending on how many times we're willing to start over at the beginning, the output can be as long as we want.

In some cases, this may cause the entire output to simply repeat (specifically, if word that isn't found is also the first word of the book), but I haven't encountered that yet.

## 7
[Stand by for Mars!, by Carey Rockwell](07-carey-rockwell_stand-by-for-mars_r100.md)

But, how many passes should be used? Is there an ideal number for each book?

The downside of having the number of passes through the book controlled by a parameter is that it reintroduces human choice into a process that I intended to be completely mechanical.