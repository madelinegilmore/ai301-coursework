# Voice guide: how I talk upstream

<!--
THIS IS THE PART YOU WRITE (new this week). Live mode reads this file
before any comment of yours goes out the door; eval mode ignores it
entirely, because your voice is yours and carries no gold labels.

This is not etiquette. "Be polite and concise" is advice for everyone
and therefore rules for no one. Write rules YOU need, in your own
words, each one concrete enough that the skill can hold a draft
against it and say which rule it breaks.

Three sections. Fill all three.
-->

## Who I am in threads

<!-- 2-3 lines. Who is talking when you comment on an issue: your
experience level stated plainly, what you are doing in this repo, what
readers can expect from you. This is the register your rules protect. -->
I am the one talking when I comment on an issue. I am a college student with a small-medium amount of expereince. 

## Rules I write by

<!-- 3-5 rules, drafted from the lecture's slide-12 moment. Each rule
needs a wrong/right pair from your own hand: one line you might
actually have written that breaks the rule, and the line you would
post instead. The pair is what makes a rule executable; a rule without
one is a wish.


Format each rule like this:

### Rule: <short name>

<The rule, one or two sentences.>

- Wrong: "<a line that breaks it>"
- Right: "<the line to post instead>"
-->
Rule: No deadlines

No timeline promisses.

- Wrong: "I will finish this tommorow"
- Right: "I will work on this tommorow"

Rule: version and behavior

Name the version and the behavior

- Wrong: "this doesn't work"
- Right: "this bug’ → ‘v1.20.0 ignores --style"


Rule: speak normally

Write more formally than you would text a friend, but no bot voice

- Wrong: "idk wat to do"
- Right: "I don't know to start this issue"


## Rules for PR titles and descriptions

My comment rules above still apply to the PR. A PR also makes claims
that a reviewer checks against the diff, so it needs these too.

Rule: title says what changed

The title names the behavior that changes, in the repo's commit
format. It is the PR version of "name the version and the behavior".

- Wrong: "fixed the bug!!"
- Right: "fix(ingestion): dedent README fixture so headings parse"

Rule: only claim what I showed

Every sentence about what the PR does points at something in the diff
or the test evidence. If I did not run something, I say that and why.

- Wrong: "This should fix it and everything works now."
- Right: "Re-ran the repro on my branch: headings now parse (output in Testing). I did not run the integration tests locally because Docker is not set up; CI runs them."

Rule: say what I left out

If I changed or dropped part of the plan, I write it in plan.md first
and then say it in the description. No surprises in the diff.

- Wrong: (diff touches a second file, description says nothing)
- Right: "One change from my plan: the fix also needed a one-line change in `parser.py`. Recorded in my plan's Deviations section."

Rule: AI disclosure in my own words

I say which tool I used and what it helped with, every time.

- Wrong: "AI was used."
- Right: "I used Claude Code to help find where the fixture is parsed and to draft the test. I read and ran every change myself."


## Things I never post

<!-- A short list. Promises you cannot keep, tones you refuse,
shortcuts you know you reach for when tired. The skill quotes this
list back at you when a draft crosses it. -->


"I'll have a PR up this week."
"Give me an hour and this will be done."
"I'll get to this ASAP."
"I can reproduce this bug."
"Same issue here, on the latest version."
"Confirmed, it crashes."
"Very interested in this amazing project!!"
"Great catch! Thank you so much for raising this important issue."
"I hope this message finds you well. I would be delighted to contribute."
"idk what to do lol"
"Tests pass." (without naming which tests)
"This should fix it."
"Cleaned up some formatting while I was in there."
"Ready to merge!"