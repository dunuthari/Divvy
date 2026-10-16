# Divvy test app (web prototype)

`divvy-test-app.html` is a single-file working prototype of the Divvy flows, used to test and tune
the product before the real Flutter iOS app is built. It follows `../design.md` and `../user-flows.md`.

- Runs standalone in any browser. Without a backend it stores data in `localStorage` ("Local only").
- Published as a Claude artifact it uses the shared `db` capability, so everyone with write access sees the same groups live ("Live, shared").
- The split engine (equal, percent, exact, leftover rupees to the top payer, balances, minimum-payment suggestions) lives between the `/*ENGINE*/` markers and is plain JavaScript that ports directly to Dart.
- Capybara art is embedded as WebP data URIs. The source files are in `../assets/capybaras/`.

Test-only features: the "switch person" pill in a group lets one person act as any member to try both sides of a flow.
