---
name: design-ui-first
description: Design a UI before implementation. Use for new screens, redesigns, visual reference research, and layout comparisons. Produce a brief, annotated references, option previews, and a recommendation grounded in the user's task.
---

# Design UI First

Use the user's language. Match the depth of exploration to the size of the change. Ground visual decisions in observable needs. Who opens this screen? What should they notice first? What should be easy to do? How much content will they typically see? Use whitespace to group related information, support reading, or establish focus.

## 1. Understand the task

Read the brief and inspect the current flow, screenshots, sample data, brand assets, components, and project design conventions. For a redesign, identify what already works. Record the screens in scope, primary user, device, goal, and implementation constraints. Ask questions when the answers would materially change the direction. Label assumptions you can test with a sketch.

Write a short brief with one scenario and an observable outcome. For a request inspector, a developer should be able to find a failed callback, read the failure reason, and retry delivery from that request.

## 2. Establish content priorities

Map how the user enters the screen, makes a decision, and recognizes the result. Decide what must be visible immediately, what supports the decision, and what can appear on demand. Assemble representative content, including long labels and a realistic number of items. For a landing page, identify the promise, supporting evidence, and action. For a work screen, identify the objects, task frequency, states, and available actions.

Produce a content outline and one sample dataset to use across all options.

## 3. Research references

Search by task and screen type, such as “webhook delivery log retry detail” or “mobile genealogy person search.” Start with shipped products, product documentation with screenshots, or screen collections such as [Mobbin](https://mobbin.com/). For landing page composition, try [Landbook](https://land-book.com/). When the product lacks a visual identity, explore an adjacent domain, such as a family archive index for a genealogy app.

Open the relevant screen or image. Select roughly two to four references that solve different problems. For each, provide a direct link when possible, describe what you observed, identify a decision worth adapting, and explain where it might fall short. When access is limited, report what you could inspect. Use user-supplied screenshots when available.

## 4. Compare design options

Create two lightweight sketches or wireframes of the same screen using the same content. Add a third when it introduces a meaningful trade-off. Vary the composition, focal point, or interaction model. For example, a split list and detail view lets a developer move quickly between requests. A transaction timeline makes retry order clearer but takes longer to compare across transactions.

For each option, show the initial view, reading order, primary action, mobile behavior, one distinctive visual choice, and its consequences. Present visual previews side by side when supported. Recommend one direction based on the brief. When the user asks to explore or choose, stop after presenting the options. When the user delegates the decision and requests implementation, continue with the recommended direction.

## 5. Record the selected direction

Write a brief implementation specification using project conventions or an existing DESIGN.md. Capture the relevant decisions:

- Composition and the first element that should draw attention.
- Content width, column behavior, information density, and narrow-screen layout.
- Typography roles, color roles, and when an accent should draw attention.
- Spacing within label–value pairs, between repeated items, and between sections.
- A visual detail grounded in the product and where it belongs.
- Long content, loading, empty and error states, and available recovery actions.

Give each card, badge, illustration, gradient, and animation a purpose in the content, brand, or interaction. Use copy that helps the user understand or act. Choose visual details independently for each product.

## 6. Implement and inspect the rendered screen

When implementation is in scope, build one representative screen first. Run the primary scenario at relevant desktop and mobile widths. Check the transition width if the column layout changes. Try short, long, empty, and dense content as appropriate. Check keyboard focus, labels, legibility, overflow, and access to the main action as content grows.

When a layout feels unbalanced, point to the specific area. Inspect minimum heights, forced equal-height columns, line length, and the relative spacing within and between groups. Preserve space that clarifies relationships. Fix the issue that most interferes with the task, render again, and compare the result with the first version. Report the checks performed and any remaining validation.

## Further reading

- Common visual defaults and concrete design guidance — [Anthropic](https://claude.com/resources/articles/improving-frontend-design-through-skills).
- Visual references and real content — [OpenAI](https://developers.openai.com/blog/designing-delightful-frontends-with-gpt-5-4).
- Scale, hierarchy, and balance — [Nielsen Norman Group](https://www.nngroup.com/articles/principles-visual-design/).
- Internal tool redesign walkthrough — [Steve Schoger](https://www.youtube.com/watch?v=BMHUKij1yUE).
- Recording design decisions and reviewing interfaces — [DESIGN.md](https://github.com/google-labs-code/design.md) and [Impeccable](https://github.com/pbakaus/impeccable).
