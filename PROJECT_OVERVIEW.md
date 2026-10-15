# DevKit — Project Overview

> **Document status:** Draft · Phase 1 (Project Documentation)
> **Last updated:** 2026-10-15
> **Implementation status:** Planning only. No part of DevKit has been built, tested, or deployed. Everything described in this document is **planned**, not completed.

---

## About This Document

This document is the primary reference for what DevKit is, who it is for, what the first release will include, and what it will deliberately leave out. It describes **what** the product does and **why**. It does not describe **how** the code is organized or how the visuals are specified; those topics belong in separate documents.

### Conventions

| Term | Meaning |
| --- | --- |
| **Must / Must not** | A firm requirement taken from the original project brief. |
| **Should / Should not** | A strong recommendation. Deviating from it needs a recorded reason. |
| **May** | Optional. |
| **(Proposed)** | A detail that goes beyond the original brief (for example, a specific limit or option name). It can be refined during implementation, but the change must be recorded here. |

### Status labels

Every feature in this document carries one of the following statuses. Today, **everything is Planned.** Update the status only when it is actually true.

| Status | Meaning |
| --- | --- |
| **Planned** | Agreed and documented, but no work has started. |
| **In progress** | Implementation has started but is not finished. |
| **Implemented** | Built, but not yet verified against the requirements. |
| **Verified** | Built and checked against the requirements in this document. |

### Related documents

The following topics will be covered in separate documents and are intentionally **not** repeated here: the technical architecture, the design tokens (colors, spacing, typography values), and the development roadmap. If this document and a later document disagree about what the product *does*, this document is the source of truth and the other document must be corrected (or this one updated through a recorded decision).

---

## Contents

1. [Project Introduction and Purpose](#1-project-introduction-and-purpose)
2. [The Problem DevKit Solves](#2-the-problem-devkit-solves)
3. [Target Users](#3-target-users)
4. [Project Goals](#4-project-goals)
5. [Scope of the Initial Release](#5-scope-of-the-initial-release)
6. [Detailed Description of the Eight Utilities](#6-detailed-description-of-the-eight-utilities)
7. [Website Pages and Their Responsibilities](#7-website-pages-and-their-responsibilities)
8. [Shared Functionality](#8-shared-functionality)
9. [Design Principles](#9-design-principles)
10. [Technology Stack and Restrictions](#10-technology-stack-and-restrictions)
11. [Data Handling and Privacy Principles](#11-data-handling-and-privacy-principles)
12. [Accessibility and Responsive Design Requirements](#12-accessibility-and-responsive-design-requirements)
13. [Browser Compatibility Expectations](#13-browser-compatibility-expectations)
14. [Deployment Expectations](#14-deployment-expectations)
15. [Excluded Features and Limitations](#15-excluded-features-and-limitations)
16. [Definition of a Successful First Release](#16-definition-of-a-successful-first-release)
17. [Appendix A: Reference Values](#appendix-a-reference-values)
18. [Appendix B: Glossary](#appendix-b-glossary)

---

## 1. Project Introduction and Purpose

**DevKit** is a premium, responsive developer toolbox website. It brings together a set of small, everyday utilities that developers reach for constantly, such as formatting JSON, encoding text, generating identifiers, and converting colors, and presents them through one polished, consistent interface.

DevKit is built with **HTML5, CSS3, and vanilla JavaScript using ES modules**. It has no backend server and no database. The utilities run in the visitor's browser, so the website can be hosted as a set of static files.

### Purpose

The purpose of DevKit is to give people a fast, trustworthy, and pleasant place to complete small technical tasks, without accounts, installation, or clutter, and with a clear understanding of what happens to their data.

### Key facts

| Item | Detail |
| --- | --- |
| Product name | DevKit |
| Product type | Static, browser-based developer toolbox website |
| Initial release | Eight utilities, nine page types (see [Section 7](#7-website-pages-and-their-responsibilities)) |
| Technology | HTML5, CSS3, vanilla JavaScript (ES modules) |
| Intended hosting | GitHub Pages or Vercel (static hosting) |
| Creator | Shishir Pant (<https://www.shishirpant.com.np/>) |
| Form processing | Formspree (the only external service planned for the initial release) |
| Current status | **Planned** (documentation phase) |

---

## 2. The Problem DevKit Solves

Developers, students, and designers regularly face small tasks that do not justify writing a script or installing software: checking whether a JSON payload is valid, decoding a Base64 string, converting a timestamp, or picking a gradient. People usually solve these tasks by searching the web and opening whichever tool appears first.

That approach commonly has problems:

- **Fragmentation.** Each task lives on a different site with a different layout, different behavior, and different quality.
- **Inconsistent quality.** Some tools are outdated, slow, confusing, or give incorrect results for edge cases such as non-English text.
- **Distractions.** Pages can be cluttered with unrelated content, which slows down simple work.
- **Unclear data handling.** It is often not obvious whether pasted data stays in the browser or is uploaded to a server. This matters when the text might contain tokens, internal URLs, or private information.
- **Weak feedback.** When input is invalid, many tools fail silently or show a technical message that does not explain how to fix the problem.
- **Poor mobile and accessibility support.** Many utilities are hard to use on a phone, with a keyboard only, or with assistive technology.

### How DevKit responds

| Problem | DevKit's planned response |
| --- | --- |
| Fragmentation | One website, one navigation system, one consistent tool layout. |
| Inconsistent quality | Each tool must perform its real task correctly and handle edge cases. |
| Distractions | A focused, minimal interface with no unrelated content. |
| Unclear data handling | Browser-side processing wherever practical, and plain-language disclosure of everything else. |
| Weak feedback | Input validation with clear, actionable error messages. |
| Poor mobile and accessibility support | Mobile-first responsive layouts and an accessibility-first approach. |

---

## 3. Target Users

| User group | Typical needs | What DevKit must provide |
| --- | --- | --- |
| **Beginner developers and students** | Learning how formats such as JSON, Base64, and URL encoding behave; checking their own work. | Clear labels, plain-language errors, and results that are easy to understand. |
| **Professional web and software developers** | Quick, reliable utilities during daily work; debugging API payloads, URLs, and timestamps. | Speed, correctness, keyboard-friendly controls, and one-click copy. |
| **Front-end developers and UI designers** | Converting color formats and creating CSS gradients. | Live previews and output that can be pasted straight into code. |
| **QA, support, and technical content people** | Validating payloads, inspecting encoded values, and measuring text. | Dependable results and clear validation feedback. |
| **Mobile-first users** | Completing a quick task on a phone or tablet. | Comfortable touch targets, responsive layouts, and no horizontal scrolling. |
| **Keyboard and assistive-technology users** | Using every feature without a mouse and with screen readers. | Full keyboard operability, visible focus, proper labels, and announced results and errors. |

### Assumptions about users

- Users do not need to create an account or install anything.
- Users may not be experts, so messages must be understandable without deep technical knowledge.
- Users may paste sensitive content, so privacy behavior must be predictable and clearly disclosed.

---

## 4. Project Goals

Each goal has an identifier so that later documents and reviews can refer to it.

### Product goals

- **G1: Correct tools.** Each of the eight utilities must perform its actual task correctly, validate input, and report useful errors.
- **G2: One consistent interface.** All tools share the same layout patterns, controls, notifications, and behavior.
- **G3: Privacy by default.** Tool input is processed in the browser. Anything that leaves the browser is disclosed.
- **G4: Fast and lightweight.** Pages load quickly and tools respond immediately for typical input sizes.

### Experience goals

- **G5: Premium feel.** The site looks and feels like a professionally developed software product.
- **G6: Easy discovery.** Search, category filters, sorting, favorites, and recently used tools help people reach a tool quickly.
- **G7: Accessible and responsive.** Every feature works on mobile, tablet, and desktop, with keyboard and assistive technology.

### Project goals

- **G8: Static deployment.** The site can be deployed to GitHub Pages or Vercel without any server-side code.
- **G9: Maintainable code.** The codebase is modular and readable enough that a beginner developer can understand and extend it.
- **G10: Honest documentation.** Documentation always distinguishes planned work from completed work.

---

## 5. Scope of the Initial Release

The initial release is the first public version of DevKit. Everything below is **in scope** and currently has the status **Planned**.

| Area | Included in the initial release |
| --- | --- |
| **Utilities** | JSON Formatter & Validator, Base64 Encoder & Decoder, URL Encoder & Decoder, UUID Generator, Color Converter, Timestamp Converter, Text Analyzer, CSS Gradient Generator. |
| **Pages** | Home, All Tools, individual tool interfaces, About, Support, FAQs, Privacy Policy, Terms of Use, and a custom 404 page. |
| **Discovery** | Tool search, category filtering, and dynamic sorting and display of tool listings. |
| **Personalization** | Favorite tools, recently used tools, and saved preferences, all stored in the browser. |
| **Appearance** | Complete dark and light themes with a theme switcher. |
| **Shared components** | Reusable header, footer, tool cards, notifications, accordions, and other UI components. |
| **Support content** | Searchable FAQs and functional contact and feedback forms (via Formspree). |
| **Quality** | Responsive layouts, keyboard usability, clear focus states, and an accessibility-first approach. |
| **Deployment** | Static hosting on GitHub Pages or Vercel. |

Features that are **not** part of this release are listed in [Section 15](#15-excluded-features-and-limitations). Any new feature must be added to this document before work on it begins.

---

## 6. Detailed Description of the Eight Utilities

### 6.0 Requirements common to every utility

These rules apply to all eight tools. They are written once here and are not repeated in each tool description.

- **Real results.** Each tool must perform its actual task using browser-side logic. Placeholder or simulated output is not acceptable.
- **Input validation.** Input must be validated before processing. Invalid input must never crash the page or silently produce wrong output.
- **Useful error messages.** Errors must be written in plain language, say what is wrong, and (where possible) explain how to fix it. They appear next to the relevant input and are announced to assistive technology. Showing only a raw browser exception message is not sufficient.
- **Helpful empty state.** Empty input shows a neutral, helpful state, not an error.
- **Copy and download actions.** Provided where they make sense, with a notification confirming success. If the browser blocks a copy action, the user sees a clear message and a way to copy manually.
- **Reset control.** Each tool has a clear way to reset its input and output.
- **Local processing.** Input is processed in the browser and is not sent to any server. Input and output are **not** saved to browser storage by default.
- **Large input.** Reasonably large input should be handled without freezing the page. If input is too large to process comfortably, the tool must say so.
- **Consistent layout.** Title, short description, input area, controls, output area, actions, and a short "processed in your browser" note.
- **Accessible and responsive.** Fully usable by keyboard and on phone-sized screens (see [Section 12](#12-accessibility-and-responsive-design-requirements)).

### Provisional categories (Proposed)

Categories power the category filter described in [Section 8.2](#82-category-filtering). They can be refined during implementation.

| Category | Tools |
| --- | --- |
| Data & Encoding | JSON Formatter & Validator, Base64 Encoder & Decoder, URL Encoder & Decoder |
| Generators | UUID Generator, CSS Gradient Generator |
| Converters | Color Converter, Timestamp Converter |
| Text | Text Analyzer |

---

### 6.1 JSON Formatter & Validator

**Category (Proposed):** Data & Encoding · **Status:** Planned

**Purpose.** Check whether text is valid JSON and display it in a readable (pretty-printed) or compact (minified) form.

**Inputs**

- A text area for pasted JSON.
- Indentation choice for formatted output: 2 spaces, 4 spaces, or tab (Proposed).

**Expected behavior**

- **Validate:** states clearly whether the input is valid JSON.
- **Format:** outputs pretty-printed JSON using the chosen indentation.
- **Minify:** outputs the most compact form, with unnecessary whitespace removed.
- The valid or invalid state is communicated with text and an icon, never by color alone.

**Validation and errors**

- Uses strict JSON rules. Comments, trailing commas, single-quoted strings, and unquoted keys are invalid.
- The error message explains the problem and, where the browser provides the information, shows the line and column (or approximate position). Position details differ between browsers, so this is best effort.
- Common mistakes (such as a trailing comma) should get a short hint (Proposed).

**Actions.** Copy output; download output as a `.json` file; clear.

**Notes and limitations.** Formatting relies on the browser's JSON parser, so whole numbers larger than JavaScript's safe integer range can lose precision when re-formatted. The tool should mention this near the output.

**Suggested search keywords.** json, format, prettify, beautify, minify, validate, lint, parse.

---

### 6.2 Base64 Encoder & Decoder

**Category (Proposed):** Data & Encoding · **Status:** Planned

**Purpose.** Convert text to Base64 and Base64 back to text.

**Inputs**

- A text area for the input.
- A mode switch: Encode or Decode.
- A variant option: Standard Base64 or URL-safe Base64 (Proposed).

**Expected behavior**

- **Encode:** converts text to Base64 using UTF-8, so accented characters, emoji, and non-Latin scripts encode correctly.
- **Decode:** accepts Base64 with or without padding, ignores line breaks and surrounding whitespace, and shows the decoded text.

**Validation and errors**

- Reports invalid characters and invalid length or padding in plain language.
- If the decoded bytes are not valid UTF-8 text, the tool warns that the data may be binary rather than text instead of showing garbled output.

**Actions.** Copy output; download output as a `.txt` file; clear.

**Notes and limitations.** Text only. Encoding and decoding files or images is not part of the initial release.

**Suggested search keywords.** base64, encode, decode, utf-8, atob, btoa, binary.

---

### 6.3 URL Encoder & Decoder

**Category (Proposed):** Data & Encoding · **Status:** Planned

**Purpose.** Percent-encode text so it is safe to place in a URL, and decode percent-encoded text back to readable form.

**Inputs**

- A text area for the input.
- A mode switch: Encode or Decode.
- An encoding scope when encoding (Proposed): **Component** (encodes everything except unreserved characters, intended for query values and path segments) or **Full URL** (keeps structural characters such as `:`, `/`, `?`, `#`, `&`, and `=` intact).
- A decode option: treat `+` as a space, as used in form-encoded data (Proposed).

**Expected behavior**

- **Encode:** produces correct UTF-8 percent-encoding for the chosen scope.
- **Decode:** converts percent-encoded sequences back to characters.

**Validation and errors**

- A malformed sequence (for example, `%` not followed by two hexadecimal digits) or an invalid UTF-8 sequence produces a clear message that points out the problem.

**Actions.** Copy output; clear. (A download action is not considered useful for this tool.)

**Suggested search keywords.** url, uri, encode, decode, percent, query string, escape.

---

### 6.4 UUID Generator

**Category (Proposed):** Generators · **Status:** Planned

**Purpose.** Generate random version 4 UUIDs (universally unique identifiers).

**Inputs**

- Quantity: a whole number from 1 to 100 (Proposed limit).
- Format options: uppercase or lowercase; hyphens on or off (Proposed).

**Expected behavior**

- A **Generate** action produces the requested number of UUIDs, listed one per line.
- Generating again replaces the previous list.
- UUIDs come from the browser's cryptographically secure random source. The tool must never use a weak random source such as `Math.random`. If no secure source is available, the tool shows an error instead of generating weak identifiers.

**Validation and errors**

- A quantity that is empty, not a whole number, or outside the allowed range produces a clear message. The tool must not silently change the value.

**Actions.** Copy a single UUID; copy all; download all as a `.txt` file; clear.

**Notes and limitations.** Only version 4 is supported in the initial release. A UUID is an identifier, not a password or secret token, and the tool should say so briefly.

**Suggested search keywords.** uuid, guid, unique id, identifier, random, v4.

---

### 6.5 Color Converter

**Category (Proposed):** Converters · **Status:** Planned

**Purpose.** Convert a color between HEX, RGB, and HSL notations and preview it.

**Inputs**

- A text field that accepts any supported notation:
  - HEX with 3, 4, 6, or 8 digits (with or without a leading `#`).
  - `rgb()` / `rgba()`.
  - `hsl()` / `hsla()`.
- A native color picker as an alternative way to choose a color (Proposed).

**Expected behavior**

- Shows the same color in HEX, RGB, and HSL, including alpha when one is provided.
- Shows a live preview swatch. The swatch never replaces the text values; the values are always shown.
- Output updates as the input changes.

**Validation and errors**

- HEX must contain only valid hexadecimal digits and a valid length.
- RGB channels must be within 0–255, hue within 0–360, saturation and lightness within 0–100%, and alpha within 0–1.
- Named CSS colors (such as `red`) and other color models (such as CMYK) are not supported in the initial release. The tool must explain this instead of failing without explanation.

**Actions.** Copy each format individually; clear.

**Notes and limitations.** Converted values are rounded, so converting a color back and forth may differ slightly from the original.

**Suggested search keywords.** color, colour, hex, rgb, hsl, rgba, convert, picker.

---

### 6.6 Timestamp Converter

**Category (Proposed):** Converters · **Status:** Planned

**Purpose.** Convert between Unix timestamps and human-readable dates and times.

**Inputs**

- A Unix timestamp (whole number, negative values allowed) in seconds or milliseconds.
- A date and time entered through date and time controls.
- A "use current time" action.

**Expected behavior**

- **Timestamp to date:** shows the date and time in UTC, in the browser's local time zone (with the zone name and offset), and as an ISO 8601 string.
- **Date to timestamp:** shows the Unix timestamp in both seconds and milliseconds.
- The unit (seconds or milliseconds) is detected from the size of the number. The tool must show which unit it assumed and let the user override it.
- A live display of the current Unix time may be included (Proposed). If included, it must not be announced repeatedly by screen readers.

**Validation and errors**

- Non-numeric input, incomplete dates, and values outside the range that JavaScript dates can represent produce clear messages.

**Actions.** Copy each result individually; clear.

**Notes and limitations.** Local time uses the visitor's browser time zone. Choosing arbitrary time zones is not part of the initial release.

**Suggested search keywords.** timestamp, unix, epoch, date, time, iso 8601, utc, convert.

---

### 6.7 Text Analyzer

**Category (Proposed):** Text · **Status:** Planned

**Purpose.** Provide statistics about a piece of text.

**Inputs.** A text area for the text to analyze.

**Metrics**

- Characters (with spaces) and characters (without spaces).
- Words, sentences, paragraphs, and lines.
- Estimated reading time, based on a stated average reading speed.
- Most frequent words, top 10 (Proposed).

**Expected behavior**

- Results update as the user types or pastes, without noticeable lag.
- Characters are counted in a Unicode-aware way, so emoji and combined characters count as one character where the browser supports it. Where it does not, the tool falls back to a simpler method and the difference is documented.
- A short help note explains how each metric is defined, so users can interpret the numbers.
- Empty input shows zero values, not an error.

**Validation and errors.** Any text is acceptable. If the text is too large to analyze comfortably, the tool says so.

**Actions.** Copy a plain-text summary of the results; clear.

**Notes and limitations.** Sentence counting is an approximation. Word counts for languages that do not separate words with spaces are approximate.

**Suggested search keywords.** text, word count, character count, reading time, sentences, paragraphs, analyze.

---

### 6.8 CSS Gradient Generator

**Category (Proposed):** Generators · **Status:** Planned

**Purpose.** Build a CSS gradient visually and copy the resulting CSS.

**Inputs**

- Gradient type: linear or radial.
- For linear gradients: an angle from 0° to 360°, using a slider and a numeric field.
- For radial gradients: a shape, circle or ellipse (Proposed).
- Color stops: from 2 to 8 stops (Proposed maximum), each with a color and a position from 0% to 100%.
- Controls to add and remove stops.

**Expected behavior**

- A live preview updates as any control changes.
- The tool outputs a ready-to-paste CSS declaration, for example `background: linear-gradient(135deg, #6366f1 0%, #8b5cf6 100%);`.
- Stops are ordered by position in the generated CSS.

**Validation and errors**

- At least 2 stops are required. The remove control for a stop is disabled at that minimum, with an explanation.
- Positions and angles must be numeric and within range. Invalid colors are rejected with a clear message. Invalid values must never be applied to the preview.

**Actions.** Copy CSS; reset to default. (A download action is not considered useful for this tool.)

**Notes and limitations.** Conic and repeating gradients, saved presets, and image export are not part of the initial release.

**Suggested search keywords.** gradient, css, linear, radial, background, color stops, generator.

---

## 7. Website Pages and Their Responsibilities

All pages share the same reusable header and footer, the theme switcher, a "skip to main content" link, and the same visual system. Primary navigation is in the header. Legal and secondary links are in the footer. The exact arrangement is defined in the architecture and design documents.

The footer on every page must include the credit **“Designed by Shishir Pant”**, linking to <https://www.shishirpant.com.np/>.

### 7.1 Home

- Explains in one short, clear statement what DevKit is.
- Gives a fast path to tools, including a prominent search entry.
- Shows tool cards for the available tools.
- Shows **Favorites** and **Recently used** sections when the user has any, and a helpful empty state or no section when they do not.
- Links to All Tools, Support, and About.
- Is a quick launch point, not a long marketing page.

### 7.2 All Tools

- Lists every tool as a tool card.
- Provides search, category filtering, and sorting.
- Lets users add and remove favorites directly from cards.
- Shows a clear empty state when no tool matches the search or filter, with a way to reset.

### 7.3 Individual tool interfaces

- There is one interface for each of the eight tools (see [Section 6](#6-detailed-description-of-the-eight-utilities)).
- Every tool interface follows the same layout and includes a favorite toggle and a "processed in your browser" note.
- Opening a tool records it as recently used.
- A request for a tool that does not exist must lead to the custom 404 page.
- Whether each tool has its own HTML file or uses a shared template is an architecture decision.

### 7.4 About

- Explains what DevKit is, why it exists, and the principles behind it (privacy, quality, accessibility).
- Includes a plain-language summary of the technology used.
- Credits the creator and links to <https://www.shishirpant.com.np/>.
- Must not contain unverifiable claims, such as user counts or performance guarantees.

### 7.5 Support

- Hosts the **contact form** and the **feedback form** (see [Section 8.9](#89-contact-and-feedback-forms)).
- Links to the FAQs so users can find answers first.
- States, close to the forms, that submissions are sent to Formspree.
- Does not promise a response time unless the owner commits to one.

### 7.6 FAQs

- Presents questions and answers in accessible accordions.
- Provides live search across questions and answers, with a clear "no results" state.
- Suggested topics: using the tools, privacy and data, favorites and saved preferences, browser support, and getting support.
- Answers must be truthful and consistent with the actual behavior of the site.

### 7.7 Privacy Policy

- Explains in plain language what is processed locally, what is stored in the browser, what is sent to external services, and how users can remove stored data.
- Must name Formspree and describe what the contact and feedback forms send.
- Must mention that the hosting provider may process standard request data (see [Section 11](#11-data-handling-and-privacy-principles)).
- Must always match the real behavior of the site and be updated whenever that behavior changes.

### 7.8 Terms of Use

- Describes the conditions for using DevKit, including acceptable use, that the tools are provided "as is" without guarantees, intellectual property, and how terms may change.
- Is written in plain language.

> **Note:** The Privacy Policy and Terms of Use are drafted to describe the project accurately. They are not legal advice. The site owner should review them (and obtain professional advice if needed) before publishing.

### 7.9 Custom 404 page

- Appears when a user requests a page or tool that does not exist.
- Uses the standard header, footer, and visual style.
- Explains the problem briefly and offers clear next steps: return to Home or browse All Tools.
- Must work correctly on the chosen hosting platform.

---

## 8. Shared Functionality

All items in this section are **Planned**.

### 8.1 Tool search

- Users can search tools by **name**, **description**, or **relevant keywords**.
- Matching is case-insensitive and ignores extra whitespace. Partial words match.
- Results update as the user types.
- Search works together with the category filter (both conditions apply).
- When there are no matches, a clear empty state is shown. The number of results is announced to assistive technology.
- Search is simple text matching. Fuzzy, AI-based, or server-based search is not included.

### 8.2 Category filtering

- Users can filter tool listings by category (see the provisional categories in [Section 6](#provisional-categories-proposed)).
- An "All" option shows every tool.
- The active filter is clearly indicated and operable by keyboard.

### 8.3 Sorting and dynamic display

- Tool listings are rendered dynamically from structured tool data, so that search, filtering, and sorting update the list without a page reload.
- Sort options (Proposed): name A–Z, name Z–A, category, favorites first, and recently used.

### 8.4 Favorites

- Users can add and remove tools from favorites using a clearly labeled toggle on tool cards and tool pages.
- The toggle communicates its state (favorited or not) to assistive technology, and not by color alone.
- Favorites are saved in the browser and shown in a dedicated place on the Home page and as a filter or sort option on All Tools.

### 8.5 Recently used tools

- A tool is recorded as **recently used** when the user opens its page.
- The list is ordered from most recent, contains no duplicates, and is capped at a small number of entries (Proposed: 8).
- Users can clear the list.

### 8.6 Browser storage and saved preferences

The only things planned to be saved in the browser are:

| Data | Purpose |
| --- | --- |
| Theme choice | Remember the user's dark or light preference. |
| Favorite tools | Remember which tools the user has favorited. |
| Recently used tools | Support the "Recently used" list. |
| Sort preference (Proposed) | Remember the last selected sort option for tool listings. |

Requirements:

- The site must keep working when browser storage is unavailable, blocked, full, or contains unexpected data. In that case, preferences simply are not remembered.
- Tool input and output, search text, and form content must **not** be saved.
- Stored data stays in the user's browser and is never sent anywhere by DevKit.

### 8.7 Theme switching

- Users can switch between a **complete dark theme** and a **complete light theme**.
- Dark is the default for first-time visitors (the design is dark-first). The user's explicit choice is saved and takes priority afterward.
- The saved theme must be applied before the page first displays, so that visitors do not see a flash of the wrong theme.
- The switcher is keyboard accessible and communicates its current state.
- Both themes must be fully designed. The light theme is not a simple inversion of the dark theme.

### 8.8 Reusable UI components

The interface is built from reusable components so that behavior and appearance stay consistent. At minimum:

- Header and footer
- Tool cards
- Notifications (toasts)
- Accordions
- Buttons and form controls
- Empty states and error messages

**Notifications** confirm actions (such as "Copied to clipboard"), report problems, and are announced to assistive technology. They must not be the only way an error is communicated; important errors also appear inline.

### 8.9 Contact and feedback forms

- Contact and feedback forms are functional and submit to the Formspree endpoint listed in [Appendix A](#appendix-a-reference-values).
- **Contact form (Proposed fields):** name, email, and message, with a subject if needed.
- **Feedback form (Proposed fields):** feedback type (for example, bug report, suggestion, or general), message, and an optional email.
- The forms must collect only the information needed for their purpose.
- Fields are validated in the browser (required fields, valid email format, reasonable length) with clear, accessible error messages.
- The form shows distinct states: ready, submitting, success, and failure. Double submission is prevented, and entered text is kept if sending fails.
- Spam protection may use the features that Formspree provides.
- The forms need an internet connection and depend on Formspree being available. The site must handle failure gracefully.

### 8.10 Searchable FAQs

- The FAQ search follows the same principles as tool search (see [Section 8.1](#81-tool-search)).
- Accordions follow accessible patterns: keyboard operable, with clear expanded and collapsed states.

### 8.11 Responsive navigation

- On small screens, navigation collapses into a menu that is fully usable with touch and keyboard.
- On larger screens, navigation is shown in full.
- The current page is indicated.

---

## 9. Design Principles

DevKit must feel like a premium, professionally developed software product. Concrete values (colors, spacing scale, type scale, radii, shadows, motion timings) will be defined in the separate design token document. This section describes the principles those values must serve.

1. **Dark-first.** The dark theme is the primary design. The light theme is carefully designed on its own terms and has equal quality.
2. **Strong typography.** Clear type hierarchy and excellent legibility, including for code and monospaced content in tool inputs and outputs.
3. **Consistent spacing and alignment.** A single spacing system is used throughout. Similar elements look and behave the same way everywhere.
4. **Clear visual hierarchy.** On every page, it is obvious what is most important and what to do next.
5. **Restrained gradients.** Gradients are used sparingly to add polish, never to dominate the interface.
6. **Polished cards.** Tool cards and panels have consistent structure, subtle depth, and clear hover, focus, and pressed states.
7. **Subtle, purposeful animation.** Motion should clarify and delight, never distract. Animations are short and are reduced or removed for users who prefer reduced motion.
8. **Tool-first layouts.** In a tool, the input and output are the focus. On desktop they may sit side by side. On mobile they stack.
9. **Complete interaction states.** Every interactive element has designed default, hover, focus, active, disabled, loading (where relevant), and error states.
10. **Plain, concise language.** Interface text is short, friendly, and professional.
11. **Consistent iconography.** One icon style is used across the site.

### What to avoid

- Generic, template-looking layouts
- Excessive decoration
- Unnecessary animations
- Oversized sections and wasteful whitespace
- Inconsistent styling between pages or tools

---

## 10. Technology Stack and Restrictions

### 10.1 Required technologies

| Layer | Technology |
| --- | --- |
| Structure | HTML5 with semantic elements |
| Styling | CSS3 (including modern layout and custom properties) |
| Behavior | Vanilla JavaScript organized as ES modules |
| Hosting | Static hosting on GitHub Pages or Vercel |

### 10.2 Browser capabilities the project is expected to rely on

These are built-in browser features, not external dependencies.

| Need | Browser capability |
| --- | --- |
| JSON processing | `JSON` |
| Base64 with UTF-8 text | `TextEncoder`, `TextDecoder`, `btoa`, `atob` |
| URL encoding | `encodeURIComponent`, `encodeURI`, `decodeURIComponent` |
| UUID generation | `crypto.randomUUID` (with `crypto.getRandomValues` as a fallback) |
| Dates and time zones | `Date`, `Intl` |
| Text segmentation | `Intl.Segmenter` (where supported) |
| Copy to clipboard | Clipboard API (with a clear fallback message) |
| Downloads | `Blob` and object URLs |
| Saved preferences | `localStorage` |
| Form submission | `fetch` |

### 10.3 Restrictions

- **Must not use** React, Next.js, or any other front-end framework or UI library. Any such dependency is considered unnecessary for the initial version.
- **Must not use** a backend server or a database.
- **Must not use** paid APIs, or any feature that depends on an undisclosed external service.
- **Should not add** third-party libraries unless there is a clear, documented need. Each one must be disclosed and justified.
- **Should** process data in the browser whenever practical.
- **Should** avoid loading fonts, icons, or scripts from third-party servers. Prefer system fonts or files hosted with the site. This keeps outside requests to a minimum and keeps privacy disclosure simple.
- **Must** clearly disclose any external service that processes submitted information.

### 10.4 External services register

| Service | Purpose | What it receives | When |
| --- | --- | --- | --- |
| **Formspree** | Receives contact and feedback form submissions. | Whatever the user enters into the form fields, plus technical data that any web request includes. | Only when the user submits a form. |
| **Hosting provider** (GitHub Pages or Vercel) | Serves the website files. | Standard web request data (such as IP address and requested URL), which hosting providers commonly process. | Whenever a page or file is requested. |
| **Creator website** | An outbound link in the footer and on the About page. | Nothing from DevKit, apart from what a browser normally shares when following a link. | Only when the user follows the link. |

No other external services are planned. If one is added, it must be listed here and in the Privacy Policy.

---

## 11. Data Handling and Privacy Principles

### 11.1 Principles

1. **Local by default.** Everything a user pastes or types into a tool is processed in their browser. It is not transmitted to any server by DevKit.
2. **No unnecessary storage.** Only the small preferences in [Section 8.6](#86-browser-storage-and-saved-preferences) are stored, and only in the user's own browser.
3. **No tracking.** DevKit does not include analytics, advertising, or behavior tracking.
4. **No accounts.** There is no sign-in, and no personal profile.
5. **Minimal collection.** Forms collect only what is needed to respond to the user.
6. **Full disclosure.** Anything that leaves the browser is described in plain language near where it happens, and in the Privacy Policy.
7. **Policy matches behavior.** The Privacy Policy and the FAQs must describe what the site really does. If behavior changes, the documents change first or at the same time.
8. **User control.** Users can remove favorites, clear the recently used list, and clear their own browser data at any time.

### 11.2 Data overview

| Data | Processed where | Stored in the browser? | Leaves the browser? |
| --- | --- | --- | --- |
| Tool input and output | In the browser | No | No |
| Search text (tools and FAQs) | In the browser | No | No |
| Theme choice | In the browser | Yes | No |
| Favorite tools | In the browser | Yes | No |
| Recently used tools | In the browser | Yes | No |
| Sort preference (Proposed) | In the browser | Yes | No |
| Contact and feedback form content | Sent to Formspree on submit | No | **Yes**, to Formspree, only on submit |
| Standard web request data | By the hosting provider | Not by DevKit | **Yes**, to the hosting provider, as with any website |

### 11.3 Security principles

The detailed approach belongs in the architecture document. At the project level:

- Treat all input as untrusted text. User input must never be inserted into the page as HTML, and the code must never execute user input.
- Validate values before using them in styles or previews (for example, in the color and gradient tools).
- Use HTTPS in production.
- Links to other websites should be created safely, so that the destination does not receive access to the DevKit page.
- Do not place secrets in the front-end code. The Formspree endpoint is public by nature, and abuse protection relies on the features offered by Formspree.

---

## 12. Accessibility and Responsive Design Requirements

### 12.1 Accessibility

The working target is **WCAG 2.2 Level AA**. This is a goal that must be verified, not a claim of compliance.

- **Semantic HTML.** Use proper landmarks, a logical heading structure, and native elements (buttons, links, form controls) rather than imitating them.
- **Keyboard usability.** Every feature must be usable without a mouse, in a logical focus order, with no keyboard traps. This includes navigation, theme switching, search, filters, favorites, accordions, tool controls, and forms.
- **Visible focus.** A clear focus indicator must be visible on every interactive element, in both themes.
- **Skip link.** A "skip to main content" link is available on every page.
- **Labels and instructions.** Every form control has a visible, programmatically connected label. Helper text and constraints are associated with their fields.
- **Errors.** Errors are described in text, associated with the relevant field, and announced to assistive technology. They do not rely on color alone.
- **Dynamic updates.** Results, notifications, search result counts, and form status changes are announced appropriately to screen readers, without excessive noise.
- **Color contrast.** Text and interactive elements meet contrast requirements in both the dark and light themes. Meaning is never conveyed by color alone.
- **Reduced motion.** Animation is reduced or removed when the user's system requests it.
- **Text scaling and zoom.** Pages remain usable when text is enlarged and when the page is zoomed to 200%.
- **Touch targets.** Primary touch targets should be at least 44 × 44 CSS pixels where practical.
- **Accessible names.** Icon-only buttons have accessible names, and decorative images are hidden from assistive technology.

### 12.2 Responsive design

DevKit is designed **mobile first**: layouts start with the smallest screens and are enhanced for larger ones. Breakpoint values are defined in the design token and architecture documents.

| Viewport class | Expectations |
| --- | --- |
| **Mobile** | Single-column layouts. Navigation collapses to a menu. Tool inputs and outputs stack vertically. Controls are comfortable to tap. |
| **Tablet** | Multi-column card grids where space allows. Navigation adapts to the available width. Tools use space efficiently without crowding. |
| **Desktop** | Multi-column card grids, a constrained maximum content width for readability, and side-by-side input and output panels where useful. |

General requirements:

- Pages must work from a width of **320 CSS pixels** upward.
- No page may require horizontal scrolling, except for contained areas such as long code output. Long output scrolls inside its own container.
- Layouts must work in both portrait and landscape orientation.
- Both themes must be checked at every viewport class.

---

## 13. Browser Compatibility Expectations

DevKit targets modern, evergreen browsers. Because it uses ES modules and modern CSS, it does not support legacy browsers.

| Browser | Expected support |
| --- | --- |
| Google Chrome (desktop and Android) | Latest two major versions |
| Microsoft Edge | Latest two major versions |
| Mozilla Firefox | Latest two major versions |
| Safari (macOS) | Latest two major versions |
| Safari (iOS and iPadOS) | Latest two major versions |

Other modern Chromium-based browsers should work but are not formally targeted.

Expectations:

- **Not supported:** Internet Explorer and other browsers without ES module support.
- Newer browser features are used with **feature detection and a graceful fallback**. For example, if the clipboard is unavailable, the user sees a message and can copy manually. If `Intl.Segmenter` is unavailable, the Text Analyzer uses a simpler counting method.
- Features that need a secure context (HTTPS or `localhost`), such as the Clipboard API, must be tested in that setting.
- If JavaScript is disabled, the site must show a clear message that the tools need JavaScript.
- Visual and functional behavior must be manually checked in each target browser before release.

---

## 14. Deployment Expectations

- **Static files only.** The site is delivered as static HTML, CSS, JavaScript, and asset files. No server-side code runs.
- **Hosting targets.** GitHub Pages or Vercel. The site must work on both without special server configuration.
- **HTTPS.** Production deployments are served over HTTPS (both hosting targets provide this).
- **Subpath support.** A GitHub Pages project site is typically served from a subpath (such as `username.github.io/repository-name/`). Links and asset paths must work both there and at the root of a custom domain.
- **404 handling.** The custom 404 page must be recognized by the hosting platform for unknown URLs.
- **Local development.** ES modules do not load reliably when a page is opened directly from the file system (`file://`). Developers should use a simple local static server while building and testing.
- **No secrets.** No private keys or secrets are stored in the repository or the front-end code.
- **Search engine basics.** Each page has a unique title and meta description, a sensible heading structure, and social preview metadata. A sitemap and robots file are added once the production URL is known.
- **Performance.** The initial release should load quickly on average mobile connections. Any third-party dependency or large asset needs a justification (see [Section 10.3](#103-restrictions)).
- **Pre-release verification.** Before the first public deployment, the checklist in [Section 16](#16-definition-of-a-successful-first-release) is reviewed.

---

## 15. Excluded Features and Limitations

### 15.1 Explicitly excluded from the initial release

The following are **not** part of the initial release and must not be added without first updating this document.

**Accounts and data**

- User accounts, sign-in, or profiles
- Cloud storage or synchronization of any kind (favorites and preferences are per browser and per device)
- Saving or sharing tool input, tool output, or tool history
- A backend server or database

**Tracking and intelligence**

- Analytics, advertising, or behavior tracking
- AI-powered features of any kind

**Services and costs**

- Paid APIs or paid features
- Any external service not listed in the [external services register](#104-external-services-register)

**Tool features beyond the descriptions in Section 6**

- File or image encoding and decoding (Base64 is text only)
- UUID versions other than version 4
- Named CSS colors, and color models other than HEX, RGB, and HSL
- Arbitrary time zone selection in the Timestamp Converter
- Conic and repeating gradients, gradient presets, and image export

**Platform and product**

- Native mobile or desktop apps, and browser extensions
- Offline or installable app support
- Public APIs, plugin systems, or user-generated tools
- Multiple interface languages (the initial release is in English only)
- Comments, social features, or newsletters

### 15.2 Known limitations

These are inherent to the design and should be communicated honestly where relevant (for example, in the FAQs).

- **Per-browser data.** Favorites, recently used tools, and preferences exist only in the browser and device where they were saved. Clearing browser data removes them. They are not shared between devices.
- **Storage may be unavailable.** In some privacy modes or restricted environments, browser storage is blocked. The site still works, but preferences are not remembered.
- **Browser-dependent details.** Some details, such as JSON error position information, depend on the browser.
- **Number precision.** The JSON tool uses the browser's JSON parser, so very large integers can lose precision when reformatted.
- **Approximate text statistics.** Sentence counts and word counts for languages without spaces between words are approximations.
- **Rounded colors.** Color conversions are rounded and may not round-trip exactly.
- **Local time only.** The Timestamp Converter shows local time in the visitor's browser time zone only.
- **Forms depend on a third party.** Contact and feedback forms need an internet connection, depend on Formspree, and are subject to that service's availability and limits.
- **Not an offline app.** Tools process data locally once the page has loaded, but DevKit is not designed to work offline.
- **Large inputs.** Very large inputs may slow down or exceed what a browser can handle comfortably.
- **Identifiers are not secrets.** Generated UUIDs are identifiers and are not intended to be used as passwords or secret tokens.

---

## 16. Definition of a Successful First Release

The first release is successful only when **all** of the items below are true. Each box should be ticked only after the item has been checked, not when it is merely written. At the time of writing, **none** of these items is complete.

### Utilities

- [ ] All eight utilities perform their real tasks correctly, including with typical edge cases.
- [ ] Every utility validates its input and shows clear, actionable error messages.
- [ ] Copy and download actions work wherever this document calls for them.
- [ ] Every utility meets the common requirements in [Section 6.0](#60-requirements-common-to-every-utility).

### Pages and content

- [ ] Home, All Tools, all eight tool interfaces, About, Support, FAQs, Privacy Policy, Terms of Use, and the custom 404 page exist and fulfill their responsibilities.
- [ ] The Privacy Policy, Terms of Use, and FAQs accurately describe the real behavior of the site.
- [ ] The footer credit “Designed by Shishir Pant” appears on every page and links to <https://www.shishirpant.com.np/>.

### Shared functionality

- [ ] Search by name, description, and keywords works for tools, and search works for FAQs.
- [ ] Category filtering and dynamic sorting work and can be combined with search.
- [ ] Favorites and recently used tools work and persist across visits in the same browser.
- [ ] Theme switching works, both themes are complete, and the choice is remembered.
- [ ] Reusable components (header, footer, tool cards, notifications, accordions) are used consistently.
- [ ] Contact and feedback forms submit successfully to Formspree and handle failures gracefully.

### Design

- [ ] The interface feels consistent, polished, and premium in both themes.
- [ ] None of the "what to avoid" items in [Section 9](#9-design-principles) is present.

### Accessibility and responsiveness

- [ ] Every feature is usable with a keyboard alone, with clear focus states.
- [ ] Manual checks and automated checks find no serious accessibility issues, and contrast is verified in both themes.
- [ ] Layouts work from 320 CSS pixels up to large desktop screens without horizontal scrolling.
- [ ] Reduced-motion preferences are respected.

### Privacy and security

- [ ] Verified: tool input is not sent over the network, and it is not stored.
- [ ] Verified: the only data stored in the browser is the data listed in [Section 8.6](#86-browser-storage-and-saved-preferences).
- [ ] No analytics, tracking, accounts, or undisclosed external services are present.
- [ ] User input is never inserted into pages as HTML.

### Compatibility and deployment

- [ ] Manually verified in all browsers listed in [Section 13](#13-browser-compatibility-expectations).
- [ ] Successfully deployed to GitHub Pages or Vercel over HTTPS, with working links, assets, and 404 handling.
- [ ] Quality targets (to be verified): mobile Lighthouse scores of 90 or above for Performance, Accessibility, Best Practices, and SEO on the Home page and on at least one tool page.

### Documentation

- [ ] This document reflects the actual state of the project, with statuses updated honestly.
- [ ] The separate architecture, design token, and roadmap documents exist and do not contradict this document.

---

## Appendix A: Reference Values

| Item | Value |
| --- | --- |
| Formspree endpoint (contact and feedback forms) | `https://formspree.io/f/moejpnpp` |
| Creator website | <https://www.shishirpant.com.np/> |
| Required footer credit text | “Designed by Shishir Pant” (linked to the creator website) |

---

## Appendix B: Glossary

| Term | Meaning |
| --- | --- |
| **Static website** | A website made of files that are served as they are, with no server-side code or database. |
| **ES modules** | The standard way to split JavaScript into separate files that import and export code. |
| **Vanilla JavaScript** | JavaScript used without a framework or library. |
| **Browser storage (`localStorage`)** | A small amount of data a website can keep in the visitor's own browser. It stays on that device and is not sent to any server by DevKit. |
| **Formspree** | A third-party service that receives form submissions and forwards them to the site owner, so that a static site can have working forms. |
| **Accordion** | A set of headings that expand and collapse to show or hide content, used for FAQs. |
| **Toast / notification** | A small, temporary message that confirms an action or reports a problem. |
| **Design tokens** | Named, reusable design values (such as colors and spacing) that keep the visual style consistent. |
| **WCAG** | The Web Content Accessibility Guidelines, a widely used standard for accessible web content. |
| **Semantic HTML** | HTML elements chosen for their meaning (such as `nav`, `main`, and `button`), which helps browsers and assistive technology understand the page. |
| **Feature detection** | Checking whether a browser supports a feature before using it, and providing a fallback if it does not. |
| **UUID** | A universally unique identifier, a 128-bit value commonly written as 32 hexadecimal digits in groups separated by hyphens. |
