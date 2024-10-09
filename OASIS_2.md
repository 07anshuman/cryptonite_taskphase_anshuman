# Asteroid Game Buffer Overflow Challenge - CTF Writeup

## The Challenge
We were given an asteroid game executable where we needed to achieve a score of over 100 to get the flag. However, the game was broken and couldn't be played normally. The challenge was to find another way to manipulate the score and obtain the flag.

## My Journey (and what I learned)

### Initial Approach (Overthinking It 😅)
When I first got the challenge, I went full "hackerman mode" without even running the game:

1. **File Analysis**: Started digging through all the game files looking for clues
2. **Reverse Engineering**: Tried to decompile the game to find score functions
3. **Memory Editing**: Attempted to use GameConqueror to find and modify the score variable in memory
4. **Complex Scripting**: Wrote Python scripts for various exploit attempts

I was going down a rabbit hole of complexity, thinking "this must be a super technical challenge!"

### The Turning Point
After all the fancy techniques failed, I finally did the simplest thing - I actually ran the game! 🤦‍♂️

The game asked for a player name as input. That's when it clicked: could the vulnerability be in this simple input field?

### The Solution
It turned out the solution was beautifully simple:
1. Enter a string about 16 characters long as the name
2. This caused a buffer overflow
3. The overflow somehow affected the memory where the score was stored
4. Boom! Score became 104 and the flag appeared

### Technical Explanation
What actually happened:
- The game probably had a fixed-size buffer for the name
- When we entered more characters than the buffer could hold, it overflowed
- This overflow corrupted the memory where the score was stored
- Classic buffer overflow vulnerability!

## Key Takeaways

1. **Start Simple**: Don't immediately jump to complex solutions. Try the basics first!
2. **Actually Test**: Run the program and understand its normal behavior before trying to exploit it.
3. **User Input is Key**: Often, vulnerabilities are found in how programs handle user input.
4. **Buffer Overflows Still Exist**: Even in 2024, buffer overflow vulnerabilities are still common and exploitable.

## What I Would Do Differently
If I were to face a similar challenge again:
1. Start by running the program and understanding its normal behavior
2. Test simple inputs before moving to complex exploitation techniques
3. Remember that CTF challenges often have simpler solutions than we expect

## Tools Used
- Initially (unnecessarily 😅):
  - GameConqueror
  - Python scripts
  - Various reverse engineering tools
- What actually worked:
  - Just the game executable and some patient testing!

## Conclusion
Sometimes in security (and in life), we overcomplicate things. This challenge taught me that starting with the basics and gradually increasing complexity is often the best approach. It's a reminder that even as we learn advanced techniques, we shouldn't forget the fundamentals.

Remember: The simplest solution is often the correct one!
