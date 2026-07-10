# Bug Journal Starter

I am starting a bug journal and I have never heard of such a frivolous thing before.

All I did before was write some spaghetti, and if the sauce did not taste right or spilled somewhere, I would go to Google or Stack Overflow and paste the entire fucking error. Not just the error code or message. The entire fucking object.

For future me: I am writing this not because I am bored, but because I am trying hard to find my footing again. Life is hard right now. I am creating my own problems that I can solve first.

Enough rambling. Let us make a template for this bad boy.

## What Is a Bug Anyway?

A bug in a program is a weak point that causes the program to fail its intended result.

There are four common types of bugs:

- `Syntax Errors`
- `Runtime Errors`
- `Logic Errors`
- `Semantic Errors`

A decent analogy I saw from Reddit:

Programs are specific and abstract at the same time. It is like your mom saying no PlayStation after 8 PM, but she catches you playing on your phone instead. Then you stupidly talk back and say she only said no PlayStation. Then she smacks your ass because what she actually meant was stop fucking around and study.

Computah is you. Mommy is the program. Real language works like that too. Instructions can have loopholes, and loopholes create bad results.

## The Four Common Bug Types

### Syntax Errors

These happen when you break the grammar rules of a programming language.

Examples:

- Typo
- Missing semicolon
- Mismatched brackets
- Wrong keyword

### Runtime Errors

These happen while the program is already running.

The app starts fine, then suddenly some cosmic particle hits Earth and fucks the program sideways. More realistically:

- Dividing by zero
- Calling something that does not exist
- Accessing bad memory
- Missing dependency
- Bad environment config

### Logic Errors

This is usually your dumbass.

The program still runs. No crash. No obvious error. It just produces the wrong output.

Examples:

- Wrong condition
- Wrong formula
- Wrong order of operations
- Confusing `AND` and `OR`
- Updating the wrong state or variable

### Semantic Errors

This sounds legal. Call your lawyer.

The code may look valid, and it may even pass basic checks, but the meaning is wrong or impossible in context.

Example:

- Treating one data type like another
- Passing the wrong kind of value into code that technically accepts it
- Writing code that is syntactically fine but conceptually wrong

## Why Keep a Bug Journal?

Because memory is trash.

If a bug wasted three hours today, there is a decent chance future you will meet the same kind of bug again. A bug journal turns random suffering into reusable knowledge.

It also forces you to answer:

- What actually broke?
- How do I reproduce it?
- What evidence do I have?
- What was the real cause?
- What change fixed it?
- How do I stop this from happening again?

## Bug Journal Template

Use the standalone template in [Bug_Journal_Template.md](/home/wks-002/Desktop/Projects/ZeroToHero/Bug-Journal/Bug_Journal_Template.md).

