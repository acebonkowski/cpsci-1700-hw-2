# CPSC 1710 Lab 2 – Ace Bonkowski

## What is this?

**Warm or Cool?** is a tiny, from-scratch machine-learning classifier, built in a single self-contained HTML page (`warm-cool.html`). It looks at a color's Red and Blue values and predicts whether the color reads as "warm" or "cool" — no libraries, no pretrained models, no API calls.

The purpose isn't the classifier itself (it's deliberately as simple as possible — one learned number, one comparison). The purpose is to make every step of that classifier — labeling data, training, and predicting — visible and explained in plain language, so a visitor can see exactly what goes in, what comes out, and why.

## How to open and use it

No build step, no server, no API keys.

1. Open `warm-cool.html` directly in Chrome, Safari, or Firefox (double-click it, or drag it into an open browser window). Avoid VS Code's built-in "Open Preview" — its internal links don't behave like a normal browser tab.
2. **Step 0 – Warm-up:** drag the Red / Green / Blue sliders and watch how those three numbers build the picture.
3. **Step 1 – Label:** look at each of the 10 colors and click "Cool" or "Warm" (or use the arrow keys to browse and C / W to label).
4. **Step 2 – Train:** once all 10 are labeled, click "Train, then test the model," then "Train the model." Watch it search for the best cutoff, then click "Test the model →" when it's done.
5. **Step 3 – Test:** mix your own color with the Red / Green / Blue sliders and see the model's prediction, plus the exact calculation behind it.
6. "Start over" resets everything back to Step 1 if you want to try different labels.

If you'd rather serve it locally: `python3 -m http.server 8000`, then visit `http://localhost:8000/warm-cool.html` — but this is optional, since the file works fine opened directly.

## How it makes a prediction (plain language)

The model never actually "sees" a color the way a person does. Here's the entire process:

1. **Reduce.** Every color is boiled down to one number: **Red − Blue**. Green is never used.
2. **Train.** Using your 10 labeled colors, the model tries every possible whole-number cutoff from −255 to 255, and for each one counts how many of your labels it would get wrong. It keeps whichever cutoff produces the fewest mistakes.
3. **Predict.** For any new color, it does exactly one comparison: if that color's (Red − Blue) score is at or above the learned cutoff, it predicts "warm"; otherwise, "cool."

That's the whole model — one number (the cutoff), one comparison. It has no idea what a color looks like; it's only ever comparing two numbers.

## A limitation I found

**Strange case: pure black**

- RGB: (0, 0, 0)
- Score (Red − Blue): 0
- Prediction: **Warm**

Black is a color most people would not call warm. But the model has no concept of black, brightness, or how a color actually looks — it only compares its Red−Blue score to the cutoff it learned. In this run, the learned cutoff was −19, and since 0 is greater than −19, the rule fires "warm" anyway.

This is an edge case that exposes the gap between what the model is doing (comparing one number to a threshold) and what a person would actually judge. Any grayscale color (black, white, or any gray in between) has a Red−Blue score of exactly 0, so the model's prediction for all of them depends entirely on which side of the cutoff zero happens to land on — not on anything about the color itself.

## Lab 2 – Dev Log

01 – I prompted the generation of the first version, attaching the task assignment, the One-Pixel.html as a design blueprint & my edited chapter 4 PDF for factual context.

02 – Feedbacked the initial version to remove some book quotes, shuffle the colors and add an explaination for RGB. 

03 – Restructured Step 0 to be an explanaition of RGB to smooth out the learning curve and set the stage.

04 – Restructured Step 2 and Step 3 by separating them.

05 – Switched out repeating content for additional ML training explainer. 

