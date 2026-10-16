# Divvy Design System

Design system for **Divvy**, an iOS-first bill-splitting app (Flutter) with a swag 3D pig as its mascot.
Currency is LKR, whole rupees only. Light and dark themes are both first-class.

Live reference with all components and six sample screens:
https://claude.ai/artifact/BgrJ43C5xXJwr9Wh2RHTvq

---

## 1. Design direction

A lilac canvas of pastel "bento" tiles, **one ink-black card per screen** for the number that matters, and a swag pig that steps out of the cards and talks to you.

Three reference apps shaped it. Colours were sampled from the supplied screenshots.

| Reference | What we took |
|---|---|
| **Blinky** (health app) | Mascot as the host, speech bubbles, small-caps eyebrow labels with a coloured dot, round icon chips, mood-tinted gradient wash behind the hero. |
| **Calm** (wellness app) | Flat colour blocks, a single near-black card for the key message, everything is a pill or a circle, tag pills, mood-style selectable chips. |
| **Lesley** (fitness app) | Lilac ground, pastel bento tiles with about 28px radius, a 3D hero object overlapping the card edge, a floating black pill tab bar with a white active circle, overlapping face stacks with a "+N" count. |

Principles:

1. **Colour separates things.** No outlines, almost no shadows.
2. **One hero per screen.** One pig, one ink card.
3. **Big radius everywhere.** 28px tiles, full-round buttons and avatars.
4. **Numbers get calm space.** Never put the pig inside a balance table.
5. **Cheeky, never shaming.** Humour is fine; mocking someone who owes money is not.

---

## 2. Colour tokens

Every colour is a token with a light and a dark value. Never hard-code a hex value in a widget.

### 2.1 Surfaces and text

| Token | Light | Dark | Use |
|---|---|---|---|
| `bg` | `#F3EEFE` | `#110E1A` | App canvas |
| `bgTop` | `#DED2FF` | `#2B2150` | Top of gradient wash (welcome, home, settle-up) |
| `surface` | `#FFFFFF` | `#1B1727` | Plain cards, inputs, bubbles |
| `surface2` | `#F8F5FF` | `#241F33` | Tab track, neutral pills, bar track |
| `line` | `#E3DBF3` | `#312A45` | Hairlines, input borders |
| `ink` | `#14111C` | `#F5F1FF` | Primary text |
| `ink2` | `#3A3347` | `#D5CDEB` | Secondary text |
| `muted` | `#756C8B` | `#A399BE` | Captions, inactive tabs, "Settled" |

### 2.2 Buttons and nav

| Token | Light | Dark | Use |
|---|---|---|---|
| `btnBg` | `#14111C` | `#F5F1FF` | Primary button fill (inverts in dark) |
| `btnFg` | `#FFFFFF` | `#110E1A` | Primary button text |
| `navBg` | `#0D1019` | `#2D2545` | Floating tab bar |
| `navFg` | `#FFFFFF` | `#FFFFFF` | Tab icons (active circle is white with `#0D1019` icon) |
| `glass` | `rgba(255,255,255,.62)` | `rgba(255,255,255,.14)` | Pills sitting on pastel tiles |

### 2.3 Pastel bento tiles

| Token | Light | Dark | Typical use |
|---|---|---|---|
| `lilac` | `#C3B0FF` | `#5B46B8` | Default tile, "you", hero owed card |
| `peach` | `#FFC98A` | `#9A6420` | Food groups, warmth |
| `sky` | `#A9D0FF` | `#2F5F9E` | Trips and travel |
| `bubble` | `#FFB8E3` | `#9C3F80` | Pig pink: nudge buttons, brand accents |
| `mint` | `#B8EBD0` | `#1F6E4E` | Home, bills, totals |
| `inkCard` | `#17131F` | `#0A0810` | The one hero card per screen |

Text on any pastel tile uses `ink`. Do not place the pig on `bubble` or `peach` tiles because the pink skin disappears.

### 2.4 Money-state colours (meaning only, never decoration)

| State | Text | Soft background | Light text / soft | Dark text / soft |
|---|---|---|---|---|
| You're owed | `owed` | `owedSoft` | `#0E7A52` / `#CBF2E0` | `#6FE3AE` / `#154433` |
| You owe | `owe` | `oweSoft` | `#CC3B27` / `#FFDFD8` | `#FF9A86` / `#47231D` |
| Waiting (pending) | `wait` | `waitSoft` | `#8A5A00` / `#FFE8BE` | `#FFCB6B` / `#473515` |
| Settled | `muted` | `surface2` | neutral | neutral |

Rules:
- Positive amounts show `+Rs 2,000`, negative show `−Rs 2,000` (true minus sign). Never rely on colour alone.
- Avatar backgrounds cycle `lilac, peach, sky, bubble, mint` per member.

---

## 3. Typography

| Role | Font | Weight | Size / line | Tracking |
|---|---|---|---|---|
| Money XL | Bricolage Grotesque | 800 | 56 / 56 | −0.04em |
| Money L (hero card) | Bricolage Grotesque | 800 | 50 / 50 | −0.04em |
| Money M (tiles) | Bricolage Grotesque | 800 | 26 / 28 | −0.04em |
| Display | Bricolage Grotesque | 800 | 36 / 38 | −0.035em |
| Screen title | Bricolage Grotesque | 800 | 22–24 / 26 | −0.03em |
| Section label | Bricolage Grotesque | 700 | 17 / 22 | −0.01em |
| Body | DM Sans | 500 | 16 / 24 | 0 |
| Body strong | DM Sans | 700 | 16 / 24 | 0 |
| Caption | DM Sans | 500 | 13 / 18 | 0 |
| Eyebrow | DM Sans | 700 | 12 / 16, uppercase | +0.08em |
| Button | DM Sans | 700 | 16 (15 small, 14 extra-small) | 0 |

- **All numbers use tabular figures** so columns of rupees line up (`FontFeature.tabularFigures()` in Flutter).
- Bricolage Grotesque has a slightly cheeky, chunky character that suits the pig. DM Sans keeps lists and forms calm.
- Do not set long body text in Bricolage.
- Support Dynamic Type. Layouts must survive text scale up to 1.3 without clipping. Tile text wraps instead of truncating money.

---

## 4. Shape, spacing, depth, motion

**Radius**

| Token | px | Use |
|---|---|---|
| `rXs` | 12 | Chips inside tiles |
| `rSm` | 16 | Icon boxes |
| `rMd` | 20 | Inputs |
| `rLg` | 28 | Bento tiles, cards, pig stage |
| `rFull` | 999 | Buttons, pills, avatars, tabs, tab bar |

**Spacing** uses a 4-point grid: 4, 8, 12, 16, 20, 24, 32.
- Screen gutter: 20
- Between list rows: 12
- Between tiles: 12–16
- Between sections: 24–32

**Touch targets:** 44pt minimum. Primary buttons are 56 tall, small 44, extra-small 36 (only inside cards).

**Depth:** flat colour first. A soft shadow is allowed only on the pig (`0 12 14 rgba(40,20,90,.28)`) and on floating bubbles.

**Icons:** 24 grid, 2px stroke, round caps and joins, drawn in the current text colour. Set used so far: home, receipt (activity), users, user, plus, share, search, back, close, check, fork, car, bell, arrow.

**Motion:** 180 ms ease-out for state changes. The pig does one small bounce on success. Respect "reduce motion".

---

## 5. Components

### Buttons
| Variant | Fill | Text | Use |
|---|---|---|---|
| Primary | `btnBg` | `btnFg` | One per screen: Add expense, Save, Continue |
| Soft | `lilac` | `ink` | Secondary actions |
| Pink | `bubble` | `ink` | Nudge |
| Ghost | transparent, 1.5px `ink` ring | `ink` | "Not yet" |
| Glass | `glass` | `ink` | Inside pastel tiles |
| Destructive | `oweSoft` | `owe` | Delete (soft, never solid red) |
| Icon circle | `surface` + `line` ring, or `btnBg` | | 48 diameter |

### Pills and status
- Neutral, ink, owed, owe, wait, glass pills: 30 high, 13px bold.
- **Form status line:** full-width rounded 14, green "Adds up to Rs 10,000" or red "Rs 2,000 left to assign" with an icon. Save buttons stay disabled until the status is green.

### Avatars (pig heads)
- Circle on a pastel background, head image 118% wide, bottom-aligned.
- Sizes 24, 30, 36, 44, 54, 58.
- Selected: 3px `bg` gap plus 2px `ink` ring.
- Face stack: overlap −10, 2.5px `surface` ring, trailing "+N" ink circle.

### Bento tile
- Radius 28, padding 16. Eyebrow label on top, money number below.
- Group tiles carry an icon box (glass), group name, people count and a glass status pill.

### Ink card (hero)
- One per screen. Eyebrow in white at 70% opacity, money number white, pig overlapping the bottom-right edge, cropped at the card boundary.

### Segmented control (Equal / Percent / Exact, and screen tabs)
- Track `surface` with a `line` inset ring. Selected segment is `btnBg` / `btnFg`.

### Inputs
- Field: 56 tall, radius 20, 1.5px `line` ring, focus ring `ink`.
- Amount input: big Bricolage numerals, "Rs" prefix in `muted`.
- Percent and exact inputs are right-aligned, tabular, with a live status line below.

### List rows
- Expense row: 46px icon box, title, "Paid by You +3 · 10 Oct", amount right with "Your share Rs 2,000" under it.
- Balance row: avatar, name, signed amount, then a diverging bar (red grows left, green grows right from a centre tick).

### Speech bubble
- `surface` fill, radius 22, 15px semi-bold, a rotated-square tail, soft shadow. Max one bubble per screen.

### Floating tab bar
- 68 tall pill, `navBg`, 4 items, active item is a 48px white circle with dark icon. Sits 24 above the home indicator. Hidden on screens with a bottom primary button (group, add expense).

### Toast
- Ink pill, bold 15px, check icon. Example: "Expense added. Everyone sees it now."

---

## 6. The mascot

One character, **ten outfits**. The app voice uses whichever pose fits the moment, and each member picks an outfit as their avatar. Art is generated 3D, cut out on transparent backgrounds, exported as WebP/PNG.

| # | Name | Look | Use in the app |
|---|---|---|---|
| 1 | Divvy | Sunglasses, black tee, cream cargo shorts, gold watch | Default host: welcome, profile |
| 2 | Chill | Backwards cap, white hoodie, arms crossed | Quiet states, settings |
| 3 | Hype | Orange puffer, beanie, peace sign | Expense added, success toast |
| 4 | Point | Varsity jacket, bucket hat, pointing | Nudges and reminders ("Ravi owes you") |
| 5 | Slick | Burgundy tracksuit, gold chain, hand on hip | Friend who owes |
| 6 | Baller | Teal jersey, spinning a basketball | Money coming in, home hero, all settled |
| 7 | Undercover | Camo, bandana, shield shades | Guest view-only mode |
| 8 | Dance | Tie-dye set, headphones, mid-dance | Loading, first-run delight |
| 9 | Wide open | Leather bomber, snapback, arms spread | Empty states ("No expenses yet") |
| 10 | Waiting | Baby-blue tracksuit, sitting on sneaker boxes | Pending confirmation |

Asset set to export to `assets/pigs/`:
- `bust_01…10`: upper body, cropped at about 77% of height, for tile hero use.
- `head_01…10`: square head crops for avatars.
- Full-body versions only where needed (for example the welcome hero).

**Do**
- Crop at the waist and overlap a card edge. Never float the pig mid-card.
- Put the pig on lilac, sky, mint or ink tiles.
- One pig per screen as the hero. Faces in lists are small head crops.
- Short, friendly lines: "Ravi still owes you Rs 2,000. Nudge him?"

**Avoid**
- Pig on pink or peach tiles.
- Pig inside balance rows or money tables.
- Text, logos or numbers printed on the pig's clothes. Outfits stay blank so the art works in any language.
- Shaming copy about debt.

**Generation prompt rules** (for new outfits): same character as the reference, plain flat background for easy cut-out, full body, no text on clothing, 9:16 portrait, one pig per image.

---

## 7. Screens (v1)

All screens are 390 × 844 design size. The lunch example runs through all of them: five people, Rs 10,000 total, four payers (Rs 4,000 / 2,000 / 2,000 / 2,000), Ravi owes Amal Rs 2,000.

1. **Welcome.** Lilac gradient, pig 1 on a lilac disc, speech bubble, display headline, one Google button, fine print.
2. **Home.** Avatar and greeting, lilac "You're owed" hero with the Baller pig and a "Settle up" button, two group bento tiles, "New group" tile, floating tab bar.
3. **Group.** Back, title, face stack, share. Ink card "Ravi owes you Rs 2,000" with the Point pig and a Nudge button. Total spent and Your share tiles, tabs (Expenses, Balances, Activity), expense row, "Share the view link" row, bottom Add expense button.
4. **Add expense.** Title, big amount, then **one merged card**: split mode control on top, one row per person with a tick box, a Paid field and a Share column (computed, percent, or exact), live green or red status lines, Save.
5. **Settle up (Balances tab).** Sky tile with the Waiting pig and bubble "Ravi says he paid you Rs 2,000. Did it land?" with **Yes, got it / Not yet**. Balances card with diverging bars, "Waiting for you" pill.
6. **Pick your pig.** Large preview of the chosen outfit on a lilac stage, 5 × 2 grid of head avatars, Continue.

Screens still to design: group creation, expense detail sheet, record-payment sheet, activity log, share sheet, guest web page (Undercover pig), empty and all-settled states, error states.

---

## 8. Product rules the UI must enforce

- Money is stored and shown in **whole rupees**. When a split does not divide evenly, the leftover rupees go to the person who paid the most, and a one-line note explains it.
- **Split modes:** Equal, Percent (must total exactly 100%), Exact (must total the expense). Save is disabled until valid, with a status line showing what is left.
- Multiple payers per expense. Payer amounts must add up to the total.
- Everyone is ticked as "shared" by default. Untick to exclude someone from one expense.
- Only the **creator** can edit or delete an expense. Others see "Only Nimal can edit or delete this." Deletes are soft and logged.
- "Mark as paid" is **two-step**: the payer records it (pending), the receiver confirms or rejects.
- Guests (view link) see balances only. No account, no editing.
- Every add, edit, delete and payment writes an activity entry.

---

## 9. Voice and copy

- Plain, warm, a little cheeky. Short sentences. Rupees written as `Rs 2,000`.
- Say what happens: "Send for confirmation", "Yes, got it", "Not yet".
- Errors say what is wrong and how to fix it: "Percentages must add up to 100%."
- The pig can joke ("Oink! Who got lunch today?") but never mocks a debtor.
- Use the person's name, not "the user". "You" for the signed-in person.

---

## 10. Accessibility

- Touch targets 44pt minimum.
- State is never colour only: signs (+ / −), words ("owes", "Settled"), and icons accompany colour.
- Text on pastel tiles is always `ink`. Re-check contrast for every tile and pill in both themes before release.
- Every pig image has a text alternative ("Pig pointing"). Decorative repeats in lists are hidden from screen readers.
- Respect Reduce Motion and Dynamic Type.
- Keyboard and VoiceOver order follows the visual order. The primary action is the last focus stop.

---

## 11. Implementation notes (Flutter)

- Define the tokens above once as a `ThemeExtension<DivvyColors>` with `light` and `dark` instances, and read them through `Theme.of(context).extension<DivvyColors>()`. No hex literals in widgets.
- Fonts: `Bricolage Grotesque` (700, 800) and `DM Sans` (500, 600, 700) via bundled assets or the `google_fonts` package. Enable tabular figures on money text.
- Radius, spacing and motion tokens live in a `DivvyTokens` class (`rLg = 28`, `gutter = 20`, `motion = Duration(milliseconds: 180)`).
- Build the shared widgets first: `DivvyButton`, `Pill`, `PigAvatar`, `FaceStack`, `BentoTile`, `InkCard`, `SegmentedTabs`, `AmountField`, `StatusLine`, `ExpenseRow`, `BalanceRow`, `SpeechBubble`, `FloatingNavBar`, `Toast`.
- Money helpers use `int` rupees only. The split engine (equal, percent, exact, leftover-to-top-payer) is pure Dart with unit tests, including the 10,000 / 5 people / four payers example.
- Pig art is bundled as assets and precached on launch. Use `Image.asset` with `cacheWidth` sized for 3x density.
- iOS only for v1, but nothing in the system depends on Cupertino widgets. Android can follow without redesign.

---

## 12. Open questions and next steps

- Regenerate each pig on its own (flat background, full body) for clean final art. The current cut-outs come from one grid image, so some edges are soft.
- Decide the app icon (likely the Divvy pig head on lilac).
- Design the remaining screens listed in section 7.
- Contrast audit of all tile and pill combinations in light and dark.
- Turn the screens into a clickable prototype or go straight to Flutter theme and widgets.
