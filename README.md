# Math Captcha

> Adapted from Ruby Quiz 48 by Gavin Kistner

## Overview

"What is fifty times 'a', if 'a' is three?" #=> 150

Write a Captcha system that uses english-based math questions to distinguish humans from bots.

Background and Details

A 'captcha' is an automated way for a computer (usually a web server) to try to weed out bots, which don't have the 'intelligence' to answer a question that's fairly straightforward for a human. Captcha is an acronym for "Completely Automated Public Turing-test to tell Computers and Humans Apart"

The most common form of captcha is an image that has been munged in such a way
that it's supposed to be very hard for a computer to tell you what it says, but
easy for a human. Recent studies (or at least articles) claim that it's proven
quite possible to write OCR software that determines the right answer a large
percentage of the time. Although image-based captchas can be improved (for
example, by placing multiple colored words and asking the user to identify the
'cinnamon' word), they still have the fatal flaw of being inaccessible to the
visually impaired.

This quiz is to write a different kind of captcha system - one that asks the
user questions in plain text. The trick is to use mathematics questions with a
variety of forms and varying numbers, so that it should be difficult (though of
course not impossible) to write a bot to parse them.

For example, this questions of this form might be easy for a bot to parse:

"What is five plus two?"

while this question should be substantially harder:

"How much is fifteen-hundred twenty-three, less the amount of non-thumbs on
one human hand?"

A good balance between human comprehension, variety of question form, and ease of computation is an interesting challenge.

The Rules

Write a module that has two module methods: 'create_question' and 'check_answer'.

The create_question method should return a hash with two specific keys:

```ruby
p MathCaptcha.create_question
#=> { :question => "Here is the string of the question", :answer_id => 17 }
```

The check_answer method is passed a hash with two specific keys, and should return true if the supplied answer is correct, false if not.

```ruby
p MathCaptcha.check_answer :answer => "Answer String", :answer_id => 17
#=> false
```

Extra Credit

1) Ensure that your library is easily extensible, making it easy for someone
using your library to add new forms of question creation, and the answer that
goes with each form.

2) For automated testing and non-ruby usage, it would be nice to provide your
module with a command-line wrapper, with the following interface:

```bash
> ruby math_captcha.rb
1424039 : What is the sum of the number of thumbs on a human and the number
of hooves on a horse?

> ruby math_captcha.rb --id 1424039 --answer 7
false

> ruby math_captcha.rb --id 1424039 --answer 6
true
```

3) Allow your 'create_question' method to take an integer difficulty argument. Low difficulties (0 being the lowest) represent trivial questions that an elementary school student might be able to answer, while higher difficulties range into algebra, trigonometry, calculus, linear algebra, and beyond. (It's up to you as to what the scale is.)

"Type the number that comes right before seventy-five."
"What is fifteen plus twelve minus six?"
"What is six x minus three i, if I said that i is two and x three?"
"What is two squared, cubed?"
"Is the cosine of zero one or zero?"
"What trigonometric function of an angle of a right triangle yields the
ratio of the adjacent side's length divided by the hypotenuse?"
"What is the derivative of 2x^2, when x is 3?"
"What is the dot product of the vectors [4 7] and [3 4]?"
"What is the cross product of the vectors [4 7] and [3 4]?"

4) Let your 'check_answer' method take a unique identifier (such as an IP address) along with the answer, and always return false for that identifier after a certain number of consecutive (or accumulated) failures have occurred.

A Tip - Generating English Numerals

Presumably parsing large numbers from english to computerese adds another stumbling block for any bot writer. ("5 + 2" is slightly easier than "five plus two" and a fair amount easier than "three-thousand-'n'-five twenty three plus five-oh-five".

Ruby Quiz #25 has some nice code that you can appropriate for turning integers into english: http://www.rubyquiz.com/quiz25.html

