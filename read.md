@import url('https://fonts.googleapis.com/css2?family=Bebas+Neue&family=Host+Grotesk:wght@300..800&display=swap');
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    text-decoration: none;
    list-style: none;
    letter-spacing: -0.03em;
    -webkit-font-smoothing: antialiased;
}

:root {
    --max-width: 1600px;
    --border-radius: 20px;
    --page-padding: clamp(0.75rem, 1vw + 0.5rem, 1.5rem);
    --content-padding: clamp(1.25rem, 3vw, 4rem);
}

html,
body {
    width: 100%;
    min-height: 100%;
}

body {
    background: #111;
}

main {
    min-height: 100svh;
    padding: var(--page-padding);
}

#hero {
    width: 100%;
    min-height: calc(100svh - 2 * var(--page-padding));
    display: flex;
    justify-content: center;
    align-items: stretch;
    color: white;
}

.container {
    width: min(100%, var(--max-width));
    border-radius: var(--border-radius);
    min-height: 100%;
    padding: var(--content-padding);
    background: linear-gradient(
        to bottom,
        #919dad 64%,
        #e19f92 100%
    );
    display: flex;
    align-items: center;
    justify-content: center;
    overflow: hidden;
}

.heroText {
    width: min(100%, 62rem);
    font-family: "Host Grotesk", sans-serif;
    font-optical-sizing: auto;
    font-weight: 400;
    text-align: center;
    display: grid;
    gap: clamp(1rem, 2vw, 2rem);
    justify-items: center;
}

.wordmark {
    font-size: clamp(3rem, 13vw, 10rem);
    line-height: 0.88;
    letter-spacing: -0.06em;
    display: flex;
    flex-direction: column;
    align-items: center;
}

.wordmarkLine {
    line-height: 0.82;
}

.wordmark span {
    font-style: italic;
    display: inline-block;
    margin-right: clamp(0.4rem, 0.6vw, 1.5rem);
}

.heroText p {
    max-width: 44rem;
    font-size: clamp(0.85rem, 1.1vw, 1.15rem);
    line-height: 1.5;
    letter-spacing: 0.08em;
    text-wrap: balance;
}

@media (max-width: 700px) {
    :root {
        --border-radius: 16px;
        --content-padding: clamp(1rem, 4vw, 1.5rem);
    }

    .wordmark {
        font-size: clamp(2.5rem, 18vw, 6rem);
    }

    .heroText p {
        max-width: 30rem;
        font-size: 0.8rem;
        letter-spacing: 0.06em;
    }
}

@media (max-width: 420px) {
    .heroText {
        gap: 0.75rem;
    }

    .wordmarkLine {
        line-height: 0.9;
    }

    .heroText p {
        max-width: 100%;
    }
}


What changed:

Replaced brittle height: 100vh usage with min-height: 100svh so the layout behaves better on mobile browsers. See style.css (line 29).
Added fluid padding and width constraints with clamp() and min() so the content scales instead of stretching awkwardly. See style.css (line 12) and style.css (line 43).
Centered the content with flex/grid instead of relying on fixed spacing. See style.css (line 53).
Turned the wordmark into semantic heading structure and removed forced line breaks in the paragraph so text can wrap naturally. See index.html (line 14).
Added mobile breakpoints to reduce type size, padding, and border radius on smaller screens. See style.css (line 97).
Why it previously felt inefficient:

It depended on fixed viewport height, which is fragile on phones because browser UI changes the available space.
It used manual <br /> breaks in the paragraph, which forces one desktop layout instead of letting the text reflow.
The content had no real max width, so it could expand too freely on large screens.
There was no clear content hierarchy beyond “make it fit”, which is usually a sign the design is not yet content-driven.
What was missing conceptually:

Fluid layout thinking: spacing, font sizes, and container widths should scale continuously, not jump only at breakpoints.
Content-first structure: the text should be allowed to wrap naturally, and the layout should adapt around it.
Semantic hierarchy: a hero title should be a real h1, not just styled <div>s.
Viewport safety: mobile browsers need svh, flexible spacing, and overflow awareness.
Constraint-based design: define a max readable width early so the composition stays balanced.
What to keep in mind next time:

Start with the content, not the decoration.
Ask: what is the minimum screen size, and what should still remain readable there?
Use min(), max(), and clamp() before reaching for lots of breakpoints.
Prefer natural wrapping over manual line breaks.
Check the layout at three checkpoints: small phone, tablet, and wide desktop.
If the design only works at one exact size, the structure is probably too rigid.
A good way to approach new layouts:

Build the semantic HTML first.
Set container widths and readable text measures.
Add fluid typography and spacing.
Center and align with flex/grid.
Test the smallest viewport, then widen from there.
Only add media queries for true layout changes, not to patch everything.