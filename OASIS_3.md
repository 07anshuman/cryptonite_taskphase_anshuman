# Spotted QR Code Challenge - CTF Writeup

## The Challenge
We were given a damaged QR code where some parts were obscured or "spotted out." The twist? The QR code itself was the flag, so we needed to reconstruct it correctly to scan and obtain the flag.

## The Journey

### Initial Research: QR Code Resilience
First, I had to understand how QR codes actually work:

1. **Error Correction Levels**
   - QR codes have four levels of error correction:
     - L (Low) - 7% of data can be restored
     - M (Medium) - 15% of data can be restored
     - Q (Quartile) - 25% of data can be restored
     - H (High) - 30% of data can be restored

2. **Critical Components**
   I learned which parts of a QR code are essential:
   - Finder patterns (the three large squares in corners)
   - Alignment patterns
   - Timing patterns
   - Version information
   - Format information

3. **Data Distribution**
   - Data in QR codes is distributed with redundancy
   - Some parts can be damaged while keeping the code readable

### The Reconstruction Process

1. **Assessment**
   - Analyzed what parts of the QR code were visible
   - Identified the version of the QR code based on its size
   - Checked which critical components were intact

2. **Pattern Recognition**
   - Looked for patterns in the visible parts
   - Used the structural rules of QR codes to infer missing parts

3. **Reconstruction Techniques**
   - Started with the known parts
   - Used an image editor to carefully redraw missing dark dots
   - Kept the finder patterns and timing patterns intact
   - Ensured alignment patterns were correctly placed

4. **Trial and Error**
   - Made educated guesses for unclear sections
   - Tested frequently with different QR readers
   - Adjusted based on error messages or partial reads

## Key Insights

1. **QR Code Resilience**
   - Learned that QR codes can still work with significant damage
   - Understood which parts are most critical for readability

2. **Pattern Importance**
   - The regular patterns in QR codes aren't just for show
   - They help readers orient and understand the code

3. **Error Correction is Amazing**
   - Even with some wrong guesses, error correction could fix our mistakes
   - This gave us more confidence in trying different solutions

## Tools Used

- Image editing software (for reconstruction)
- Multiple QR code readers (some readers work better than others)
- QR code specification documents (for reference)

## Step-by-Step Solution

1. **Started with a template**
   - Used the visible parts to determine QR version
   - Drew a grid matching the original size

2. **Filled in the knowns**
   - Added all clearly visible black modules
   - Ensured finder patterns were perfect

3. **Reconstructed pattern by pattern**
   - Worked outward from known areas
   - Used QR code rules to infer likely patterns

4. **Testing and refinement**
   - Scanned after each significant change
   - Used error messages as hints for corrections

## Learning Outcomes

1. **Technical Knowledge**
   - Deeper understanding of QR code structure
   - Learned about error correction in digital formats

2. **Problem-Solving Skills**
   - Improved pattern recognition abilities
   - Learned to balance perfection with "good enough"

3. **Tools and Techniques**
   - Got better at image editing for precision work
   - Learned which QR readers work best for damaged codes

## Tips for Similar Challenges

1. Start by understanding the format you're working with
2. Don't aim for perfection immediately - build up gradually
3. Use multiple tools for verification
4. Keep track of what works and what doesn't

## Conclusion
This challenge taught me that sometimes, recovery and reconstruction can be just as interesting as breaking or exploiting. It also showed me that understanding the resilience of a format can be key to solving problems related to it.

