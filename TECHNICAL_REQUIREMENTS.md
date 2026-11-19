# Checkpoint 2 technical requirements

[Open the studio](https://davidzhangsan.github.io/sculpt-lyric-studio/) · [Open the checkpoint checks](https://davidzhangsan.github.io/sculpt-lyric-studio/#checks)

For the mentor meeting, use desktop Chrome with sound enabled. Each row gives an action and the result to look for. The two Hello checks and five project-specific requirements follow the [Checkpoint 2 assignment](https://docs.google.com/document/d/1cfrxgHMlFfXeXybADRh1FuGOCThVNYmx-hNoeDMWHwo/edit).

The public demo supports hands-on checks for phrasing, emphasis, recording, comparison and optional offline interpretation. Live model quality and latency, a physical microphone check, and mentor approval remain open.

| Requirement | Observable acceptance check |
| --- | --- |
| Hello world | Open **Technical requirements** from the studio footer. A React component displays **Hello world**. Reload the route directly and see the same heading. |
| Hello styles | On the requirements page, inspect the named interface palette, interface heading and body samples, italic lyric display, and every icon in the project’s icon registry. Compare them with the corresponding elements in the studio. |
| 1. Locate a line and fit syllables to its melody | Select line 05 and confirm chorus bars 9–10. Select **BEAU**, inspect its offset from A4, align it, listen to the onset click and Undo. Select **beautiful** in the lyric, enter **home** and use **Play both**. The first pass highlights the original, the second highlights the alternative. Keep original should leave the draft intact. Applying the edit should keep **to** at 3.16 seconds and Undo should restore all six original syllables. Tap one entrance per syllable after the four-beat count-in. Loop the phrase and verify that the playhead crosses each tile’s left edge with its click. Cancel a partial tap pass and verify that the previous timing remains. |
| 2. Draw and manipulate vocal emphasis | On line 03, choose Sculpt delivery and drag **said** above **never**. The SVG point follows the pointer, the filled curve reshapes, and both the lyric and word label highlight **said**. The reference melody keeps its pitches. Preview changes note intensity. Undo restores the curve in one step. Reset restores the line’s initial curve. Repeat using the focused point’s arrow keys. |
| 3. Capture, review and play audio | Record a phrase, stop, and play the review. Record again with a clearly different phrase. Save the take, reload, and find its playable audio in Compare. While capturing, navigation and editing are locked. Repeat after denying mic access and with an unavailable device. The app should explain recovery and preserve the current sculpt. |
| 4. Save, compare and choose performances | Save two different drafts of one line and record a different take for each. Reload. Select the line in Compare. Reading A and B show their own curves, words, interpretations and players. Compare timing and accent changes for identical text. Try different lyrics and check that each card preserves its words and cue times. Play both takes, then choose **Use this delivery** and verify those values load in the studio. |
| 5. Interpret the actual emphasis pattern | Choose **Interpret this reading** in the local studio. The local backend calls OpenAI (default model `gpt-4o-mini`) when a server-side key is configured. Run the six cases below with and without a valid key. The portable edition uses offline examples. Check the source label, loading message, network duration and human-rated relevance. Dismiss leaves all peak heights unchanged. With an invalid test key the request should fail visibly. Restore valid configuration, restart the server, and use Retry. |

## AI quality and latency exercise

Start the studio and run `npm run evaluate:ai`. Each response is printed alongside its intended distinction. Review the result as a possible reading of the lyric. Other plausible interpretations can pass.

| Case | Lyric and emphasis | Evidence to look for |
| --- | --- | --- |
| Denial | “I **never** said you were the one” | A denial or correction tied to *never*. |
| Implication | “I never **said** you were the one” | A distinction between words spoken and meaning implied. |
| Admiration | “You're **beautiful** to me” | The compliment itself comes forward. |
| Perspective | “You're beautiful to **me**” | The singer’s personal point of view matters. |
| Shared emphasis | “The **harbor** holds its **breath**” | Both accented images contribute to an open reading. |
| Flat delivery | “Leave a little light for me” with values from 48 to 50 | An even delivery or an acknowledgment of ambiguity. |

For each live output, give one point each for grounding in the lyric, sensitivity to the supplied pattern, and tentative language. Record the text and reason for any lost point. A suggested checkpoint target is at least 15/18 with both paired contrasts distinguishable. This is a proposed review criterion.

Run the suite three times on the demo network. Record the model, source label, median and slowest round trip. Suggested target is median under 3 seconds, with a visible retry on a failed or timed-out request. The server applies a 12-second upstream timeout. Script timing excludes the editor’s 350 ms debounce. Offline latency measures local transport and rules only.

## Verification record

The production build passed. Browser checks exercised horizontal syllable dragging and Undo, vertical peak dragging and keyboard input, both example lyrics, dismiss/show, guide playback, two saved sculpts, comparison deltas and restoring a delivery. In an isolated test origin, a simulated permission denial was followed by successful capture of two generated audio streams through the browser’s actual MediaRecorder. Both recordings survived reload and decoded for playback. Physical microphone quality and live provider quality/latency require a separate run with the demo device and a configured API key.

The six offline evaluation cases returned six labeled readings. One localhost run measured a median of 1 ms and a slowest response of 35 ms. These numbers describe the offline path on this machine.


## Round-two portable check

The standalone HTML was opened from disk in a clean desktop Chrome profile with networking disabled. Browser checks covered dragging and undoing a syllable entrance, aligning to a note, rewriting a six-syllable line as two syllables, capturing two Space-bar taps after a count-in, looping past the end of the phrase, and restoring a saved rewrite after refresh. A simulated input device exercised the browser recorder and the take remained linked to its draft. Optional interpretation and both Hello checks ran offline. The run made zero HTTP requests. This is a software test, separate from a musician's evaluation of the timing cues or physical microphone.


## Round-three verification

The previous line-rewrite behavior shifted the chorus word *to* about 0.91 seconds earlier following a single-word substitution. The new word-trial and full-line rewrite checks both retained the original 3.16-second entrance. Model checks covered 138 substitutions across the eight demo lines, plus repeated words, manually tapped entrances, empty inputs and crowded slots. An offline Chrome browser check exercised two-pass playback, applying, canceling and undoing a trial, the full-refit warning, the narrow-screen line picker, saved drafts and microphone capture with a synthetic source. These checks cover implementation behavior. A songwriter listening test is still pending.

Run `npm run check:phrasing` from the source project to repeat the timing regression checks.
