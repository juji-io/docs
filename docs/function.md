---
no_toc: true
---

These functions can be used in REP patterns directly without namespace. The first argument of these functions is always `rep`, the reference to the REP chatbot itself. It should be omitted when calling the functions in REP patterns. For example, `(user-first-name)` is the right way to call the function `(juji.func.user/user-first-name rep)` as in `[my pattern (user-first-name)]`.

However, when using such function outside of REP patterns (e.g., in a self defined function in REP script), it should be called with appropriate namespace and all of its arguments, e.g., `(juji.func.user/user-first-name rep)`.

<iframe width="1280" height="720" src="../sys-fun/" frameborder="0" allowfullscreen></iframe>
