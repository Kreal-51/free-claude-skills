# Nikolai - Worked Example

One full planning cycle on an explainer video: the runtime checked against the script, a flat
section diagnosed to the frame, a rebuilt beat sheet in which every frame is accounted for, a
lip-sync sheet timed off the waveform, and a character-design handoff. Invented company,
*Ledgerly*, a small-business bookkeeping SaaS. Every frame count in this document has been added
up; the rows sum.

---

# Example - A 90-Second Brief That Was Not 90 Seconds, and the Flat Section Underneath It

**Ask:** Ledgerly's marketing lead brought a locked script, a 90-second runtime, and a rough
animatic cut by an in-house junior animator. The note: "the middle section feels flat and boring,
everything else feels okay, can you tell us why and fix the plan before we go into full
production." No character designs existed yet.

**Frame rate for everything below: 24 fps.** One frame is 41.67 ms. Where a figure is given in
seconds it is also given in frames, because frames are what gets keyed.

---

## 1. Before Anything Else: The Runtime Does Not Fit The Script

I counted the words before I looked at the animatic, and the answer changed the whole engagement.

| Beat | Script line | Words | Voiceover at 2.5 w/s | Slot in the brief |
|---|---|---|---|---|
| 1. Hook | "Every small business owner has a shoebox of receipts somewhere." | 10 | 4.0 s | 0:00-0:08, 8 s |
| 2. Problem | "Manual bookkeeping eats hours you don't have, and one missed entry throws off your whole tax season." | 17 | 6.8 s | 0:08-0:22, 14 s |
| 3. Turn | "Meet Ledgerly." | 2 | 0.8 s | 0:22-0:27, 5 s |
| 4. How it works | "Snap a receipt, Ledgerly categorizes it, reconciles it, and files it, automatically." | 12 | 4.8 s | 0:27-0:55, 28 s |
| 5. Proof | "Businesses using Ledgerly save an average of 6 hours a week." | 11 | 4.4 s | 0:55-1:12, 17 s |
| 6. CTA | "Start your free trial today." | 5 | 2.0 s | 1:12-1:30, 18 s |
| **Total** | | **57** | **22.8 s** | **90 s** |

**57 words in 90 seconds is 38 words per minute.** Explainer voiceover runs 140 to 160. A
90-second explainer at 150 wpm carries about 225 words. This script carries a quarter of that.

Voiceover density is 22.8 of 90 seconds, which is 25%. The working range for an explainer is 40%
to 70%. Beat 4 is the extreme case: 12 words, 4.8 seconds of voiceover, in a 28-second slot. That
is 30 words per minute and 23 seconds of something else.

This is the finding, and it comes before the flat diagnosis because it causes it:

> The middle section does not feel flat because of how it was animated. It feels flat because 28
> seconds were allocated to a 12-word line and nobody decided what happens in the other 23. The
> junior animator filled the gap by slowing four actions down and holding on each one. Anyone
> would have. There is nothing else to do with 23 unassigned seconds.

### 1.1 The two options, and what I recommend

**Option A, recut to 48 seconds. Recommended.** 57 words at 2.5 w/s is 22.8 seconds of
voiceover; at 48 seconds total that is 48% density, which is the middle of the working range. The
script survives untouched, which matters because it is locked, and the piece gets tighter rather
than thinner. A 48-second explainer is a normal length for a paid social cut and a product-page
hero.

**Option B, keep 90 seconds and write about 140 more words.** That means a second proof beat, a
named objection handled, and probably an on-screen number. It is a copy commission and a new
voiceover session, and it is not a timing problem. If Ledgerly wants 90 seconds for a media
reason, this is the honest route, and the timing sheet should not be built until the words exist.

What I will not do is deliver a 90-second sheet carrying 23 seconds of hold and call it pacing.
Ledgerly took Option A. Everything below is the 48-second cut.

### 1.2 The 48-second beat budget

48 s x 24 fps = **1,152 frames.** The beat budgets sum to it.

| Beat | Slot | Frames | Running frame | Words | VO | Air | VO density |
|---|---|---|---|---|---|---|---|
| 1. Hook | 7.0 s | 168 | 0-167 | 10 | 4.0 s | 3.0 s | 57% |
| 2. Problem | 10.0 s | 240 | 168-407 | 17 | 6.8 s | 3.2 s | 68% |
| 3. Turn | 3.0 s | 72 | 408-479 | 2 | 0.8 s | 2.2 s | 27% |
| 4. How it works | 16.0 s | 384 | 480-863 | 12 | 4.8 s | 11.2 s | 30% |
| 5. Proof | 7.0 s | 168 | 864-1031 | 11 | 4.4 s | 2.6 s | 63% |
| 6. CTA | 5.0 s | 120 | 1032-1151 | 5 | 2.0 s | 3.0 s | 40% |
| **Total** | **48.0 s** | **1,152** | | **57** | **22.8 s** | **25.2 s** | **48%** |

Beat 4 is still the lowest-density beat at 30%, and deliberately so: it is the only beat where
the picture carries information the voiceover does not, four separate mechanics shown in
sequence. Beat 3 at 27% is a held brand moment, which is what a turn is for. Both are now
intentional, sized, and small enough to design rather than absorb.

---

## 2. Diagnosing the Flat Section (Beat 4)

With the runtime fixed, the animatic's actual craft faults are visible and they are real. I
reviewed the rough frame by frame. **The flat feeling has two causes, and both are countable.**

**Cause 1: four consecutive sub-actions on an identical spacing curve.** Each of the four
actions (snap, categorize, reconcile, file) was a single linear move from pose A to pose B, no
wind-up, no settle, instant stop:

- **Snap (receipt to phone):** the receipt travelled in a straight line at constant speed from
  the hand to the phone screen and stopped dead. No anticipation, no follow-through. The phone
  should take the impact and the hand should overshoot and settle.
- **Categorize (receipt sorts into a folder icon):** same straight line, same linear ease, same
  instant stop.
- **Reconcile (checkmark appears):** scaled 0% to 100% in one linear tween with no overshoot, so
  it read as a UI toggle rather than a confirmation.
- **File (folder slides into a cabinet):** the same linear-in, linear-out pattern a fourth time.

Four identical spacing signatures in a row reads as mechanical regardless of what each icon is
doing. This is the principle "slow in and slow out" absent four times, compounded by having no
variation to hide behind.

**Cause 2, and the one nobody looked for: the sheet did not add up.** The junior animator's sheet
gave each sub-action a 7-second slot labelled 168 frames, and then listed phases totalling 28
frames (6 anticipation, 14 action, 8 settle). Across all four sub-actions the sheet specified 105
frames of motion inside 672 frames of beat.

| | Frames |
|---|---|
| Beat 4 length | 672 |
| Frames the sheet accounted for | 105 |
| Frames with nothing written against them | **567, which is 84%** |

Eighty-four percent of the beat was undesigned. Not held on purpose, which is a legitimate and
common choice. Undesigned: no row, no instruction, no note about what changes on screen. That
gap is what the animatic filled with dead screen, and it is why the note came back as "boring"
rather than as a specific complaint. A sheet whose rows do not sum to the beat has delegated the
hardest part of the timing to whoever happens to be keying it.

---

## 3. The Fix: Beat 4 Timing Sheet, Every Frame Accounted For

Beat 4 is now 384 frames (16.0 s), four sub-actions of **96 frames (4.0 s)** each. Frame numbers
below are local to the beat, 0 to 383. Add 480 to get the sheet-wide frame.

### 3.1 Sub-action 1: Snap, frames 0-95

| Phase | Frames | Count | Step | Content and ease |
|---|---|---|---|---|
| Entry hold | 0-11 | 12 | twos | Hand holding receipt, phone in other hand. State readable before anything moves. |
| Anticipation | 12-17 | 6 | ones | Hand pulls the receipt back about 8% of its travel distance. Ease in. |
| Main action | 18-31 | 14 | ones | Receipt travels to the phone screen. Ease out sharply on arrival: a snap should feel decisive, not floaty. |
| Follow-through | 32-39 | 8 | ones | Phone scales 100-104-100 over 8 frames; hand overshoots 6% past its rest pose and settles in 2 diminishing oscillations. |
| Read hold | 40-95 | 56 | twos | Receipt thumbnail appears on the phone and a "Captured" chip fades in over frames 40-48. Nothing else moves. Voiceover "Snap a receipt" lands across 44-68. |
| | | **96** | | |

### 3.2 Sub-action 2: Categorize, frames 96-191

| Phase | Frames | Count | Step | Content and ease |
|---|---|---|---|---|
| Entry hold | 96-107 | 12 | twos | Folder icon enters frame left, parks, holds. |
| Anticipation | 108-111 | 4 | ones | Folder "perks up", scales 100-106, before the receipt arrives. 4 frames is deliberately shorter than the Snap's 6 so this does not read as a repeat. |
| Main action | 112-127 | 16 | ones | Receipt travels on an **arc**, not a straight line, into the folder. The arc is the whole reason this reads as a different action from Snap. |
| Follow-through | 128-133 | 6 | ones | Folder settles with a slight squash, one oscillation. |
| Read hold | 134-191 | 58 | twos | Category label "Office supplies" types on over frames 134-150. Voiceover "Ledgerly categorizes it" lands across 140-162. |
| | | **96** | | |

### 3.3 Sub-action 3: Reconcile, frames 192-287

| Phase | Frames | Count | Step | Content and ease |
|---|---|---|---|---|
| Entry hold | 192-205 | 14 | twos | Two ledger rows on screen, no checkmark yet. Longest entry hold of the four, because the viewer has to read two rows before the payoff means anything. |
| Anticipation | 206-210 | 5 | ones | Checkmark held just off-screen with a faint pulse. |
| Main action | 211-220 | 10 | ones | Checkmark scales in with overshoot to 115%. |
| Follow-through | 221-228 | 8 | ones | Settles to 100% in 2 small oscillations. **The only spring curve in the beat**, reserved so the confirmation is the emotional peak of the section. |
| Read hold | 229-287 | 59 | twos | Both ledger rows turn green in sequence, 4 frames apart, over frames 229-240. Voiceover "reconciles it" lands across 232-248. |
| | | **96** | | |

### 3.4 Sub-action 4: File, frames 288-383

| Phase | Frames | Count | Step | Content and ease |
|---|---|---|---|---|
| Entry hold | 288-299 | 12 | twos | Cabinet enters, parks. |
| Anticipation | 300-305 | 6 | ones | Drawer nudges open. |
| Main action | 306-319 | 14 | ones | Folder slides in, ease in on departure, ease out on arrival, slower overall than the Snap to signal the beat is closing. |
| Follow-through | 320-327 | 8 | ones | Drawer closes with a soft bounce on the latch. |
| Read hold | 328-383 | 56 | twos | Drawer label settles; the whole group drifts 3% left over frames 350-383 to lead the eye into the Beat 5 cut at frame 864. Voiceover "and files it, automatically" lands across 330-354. |
| | | **96** | | |

### 3.5 The beat reconciles

| | Frames | Share |
|---|---|---|
| Entry holds (12 + 12 + 14 + 12) | 50 | 13% |
| Motion (28 + 26 + 23 + 28) | 105 | 27% |
| Read holds (56 + 58 + 59 + 56) | 229 | 60% |
| **Beat 4 total** | **384** | **100%** |

**The same 105 frames of motion as the junior animator's sheet.** That is the point worth
sitting with. The motion was not the problem and the fix is not more animation. What changed is
that the beat is 384 frames instead of 672, so the holds are 229 frames instead of 567, and
every one of those 229 frames now has an instruction against it. Each read hold does something:
a chip fades, a label types on, rows turn green in sequence, a group drifts into the cut. A hold
with a job is a beat. A hold with nothing written against it is dead screen with a frame count.

**Four distinct spacing signatures**, so no two consecutive sub-actions share a curve:

| Sub-action | Signature |
|---|---|
| Snap | Decisive: short anticipation, straight travel, hard ease out |
| Categorize | Soft: arced path, gentler ease on both ends, shortest anticipation |
| Reconcile | Spring: overshoot to 115% with 2 oscillations. The emotional beat. |
| File | Settling: slowest main action, soft latch bounce, drift into the cut |

**Step discipline:** all motion on ones, all holds on twos. The only place this could break is the
Categorize arc, where the receipt crosses roughly 40% of frame width in 16 frames; that is inside
the range where twos would start to step, so it stays on ones. Noting it because it is a drawing
count the animator has to budget for.

---

## 4. Style Direction

Ledgerly's brand brief: "approachable but credible, not cartoonish, not sterile enterprise
software." I locked the register as numbers before finalising the sheet above, so two animators
key the same thing.

**Register: corporate-warm.** Not playful, not technical.

| Parameter | Value | Why |
|---|---|---|
| Scale overshoot | 104% to 115%, never past 120% | 104% on the phone impact, 106% on the folder perk, 115% on the checkmark. Above 120% the piece reads as a kids' app. |
| Oscillations on settle | 1 to 2 | 2 on the checkmark and the hand, 1 on the folder. Three or more is playful. |
| Squash and stretch on the human character | None | Icons take squash; the person does not. This is the single line that keeps it credible. |
| Ease curves | Standard ease in / ease out throughout | One exception, below. |
| Spring curve | Exactly one in the piece: the Reconcile checkmark, frames 211-228 | Reserved so the confirmation is the payoff. A second spring curve anywhere and the first one stops meaning anything. |
| Secondary motion density | Restrained but present | Phone bounce, folder perk, one blink, one head tilt. Nothing idles for decoration. |

---

## 5. Lip-Sync Sheet, Beat 3

The voiceover is narration over most of the piece. Beat 3 is the only beat that cuts to the
small-business-owner character speaking to camera. Timed against the waveform, not syllable
count.

**Mouth set: Preston Blair's 10 shapes** (from *Advanced Animation*). Naming the set matters,
because the A-H plus X set a tool like Rhubarb Lip Sync produces does not map one to one onto it
and an animator working from the wrong set will key the wrong shapes. **All shapes keyed 1 frame
ahead of the audio**, which is how the mouth reads as forming the sound rather than reacting to
it. Frame numbers are local to Beat 3, 0 to 71.

"Meet Ledgerly" is 2 words, 13 phonemes written out, and 27 frames of mouth. It is **not** three
viseme transitions: "Ledgerly" alone needs six.

| Frames | Count | ms | Audio | Mouth shape (Blair) | Note |
|---|---|---|---|---|---|
| 0-5 | 6 | 250 | silence | Rest | Air before the line. Head tilt starts frame 4. |
| 6-7 | 2 | 83 | M in "Meet" | M-B-P (closed) | **Closed, then open.** M is the closed shape; the mouth opens into the vowel after it, not before. |
| 8-13 | 6 | 250 | IY in "Meet" | E (wide, narrow aperture) | 6 frames: the stressed vowel of the stressed word, held at the top of the budget. The vowel in "meet" is IY, not EH. |
| 14-15 | 2 | 83 | T in "Meet" | C-D-G-K-N-R-S-Th-Y-Z | Stop consonant, 2 frames, minimum. |
| 16-18 | 3 | 125 | L in "Ledgerly" | L | |
| 19-21 | 3 | 125 | EH | A-I (open) | |
| 22-24 | 3 | 125 | JH | C-D-G-K-N-R-S-Th-Y-Z | The "dg" affricate. |
| 25-27 | 3 | 125 | ER | U (rounded) | |
| 28-29 | 2 | 83 | L | L | 2 frames not 3: unstressed, mid-word, and shortening it keeps the brand name from sounding laboured. |
| 30-32 | 3 | 125 | IY | E | Final vowel. |
| 33-71 | 39 | 1,625 | silence | Rest, settling to a small smile over 33-44 | Blink frames 34-39: 2 closing, 1 held, 3 opening. |
| | **72** | **3,000** | | | |

**Why the blink sits at frame 34 and not at 20.** Frames 19-32 carry the brand name. A blink
takes the eye to the eyes, and a blink landing mid-"Ledgerly" costs the one word the beat exists
to deliver. It goes immediately after the line, where it reads as the character finishing a
thought.

**"Meet" gets 10 frames for 2 words' worth of attention and "Ledgerly" gets 17.** That ratio is
the emphasis decision made visible. If the client later wants the product name to land harder,
the frames come out of the 39-frame rest hold, not out of "Meet", because shortening the stressed
vowel of the opening word is what makes a read sound rushed.

---

## 6. Character Design Handoff to Anouk

No character existed beyond a placeholder grey silhouette in the rough. I flagged it rather than
planning rig detail against an undesigned character.

**Handoff notes to Anouk (Character Designer):**
- One small-business-owner character, appearing in Beats 1, 3 and 6 only. Screen time in the
  48-second cut: 168 + 72 + 120 = **360 frames, 15.0 seconds**, 31% of the piece. Design for a
  short, non-hero role that has to read instantly, not a constant on-screen lead.
- Must support the corporate-warm register in section 4: friendly but credible, no exaggerated
  proportions, **no squash and stretch on the figure**. Expression range needed, minimum:
  neutral/listening (Beats 1 and 6), a small smile for the direct-to-camera line (Beat 3, settling
  over frames 441-452 of the sheet), and a satisfied pose for Beat 5's proof moment.
- Rig requirements that follow from the sheet already built, so the design does not fight them:
  - **Articulated jaw with independent upper and lower lip control**, because the Beat 3 sheet
    needs 10 distinct mouth shapes including a closed M-B-P and a wide E, and a single-pivot jaw
    cannot make a closed-lip shape.
  - **Independent brow control**, separate from the eyelids, for the blink at frames 34-39 of Beat
    3 without the brows moving with it.
  - **Shoulder pivot with real range**, not an elbow hinge only. The Snap sub-action times 6
    frames of anticipation as an 8% pull-back of the whole arm; a stiff shoulder will fight it and
    the anticipation will have to come out, which puts the flatness straight back in.
- I did not invent the character's look, proportions or wardrobe. That is Anouk's call. The timing
  above assumes whatever rig she delivers supports the three pivots named.

---

## 7. One Thing I Took Out Of The Animation Notes

Beat 5's line is "Businesses using Ledgerly save an average of 6 hours a week." I have timed it
and I am animating it, and the number is going on screen as a count-up over Beat 5's read hold.

I am not treating that figure as established, and neither should the sheet. It is a marketing
claim from the client's own script, it has no source attached, and an on-screen number carries
more weight than a spoken one. **It needs substantiation before the piece ships, and if there is
no study behind it the line should say "customers tell us" rather than "an average of".** That is
a copy and legal decision, not mine, and I have raised it with the marketing lead rather than
quietly animating it. Flagging it here so it does not get lost between the timing sheet and the
final cut.

---

## 8. Handoffs In This Cycle

- **Tobiah (Storyboard Artist)** framed the shots. The recut from 90 to 48 seconds changes the
  shot count, so the storyboard goes back to him before keying: I retimed within his framing and
  adjusted in-beat paths (the Categorize arc), but dropping 42 seconds is a sequence decision and
  his to re-approve.
- **Anouk (Character Designer)** owns the character, per section 6. Nothing on the figure is keyed
  until her design lands.
- **Saskia (Motion Designer)** takes the logo sting Ledgerly separately asked about for the open.
  That is brand-element motion design with loop points and safe areas, not character and narrative
  animation, and it sits outside this sheet. It also needs its own frame budget on top of the
  1,152, which the 48-second runtime does not currently include.
- **Marketing lead** owns the "6 hours a week" substantiation in section 7 and the Option A
  runtime decision in section 1.1, both of which are recorded as theirs.
- **Ledgerly's production animator** executes in After Effects from the sheets above. The plan is
  the blueprint, not the rendered asset. The drawing count to budget: 105 frames on ones plus 279
  frames of hold on twos is 105 + 140 = 245 drawings for Beat 4.

---

*This example uses an invented company to show the format and depth of Nikolai's output, and
every frame count in it reconciles. Nikolai produces the same structure against your real script,
animatic or character rig.*
