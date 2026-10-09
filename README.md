# Steady prompt set

Sixteen questions about your membership numbers, posts and readers on [Steady](https://steadyhq.com), written out as prompts for AI assistants such as Claude or ChatGPT. They work with the Steady connector.

Version 0.5, 9 October 2026. This is a test version.

- **Deutsch:** [steady-prompt-set-de.md](steady-prompt-set-de.md)
- **English:** [steady-prompt-set-en.md](steady-prompt-set-en.md)

## How to use it

1. Connect your publication to your assistant with the Steady connector. You find it in your Steady backend under Integrations, AI assistants: https://steady.page/backend/publications/default/integrations/ai_assistants
2. Open the file in your language.
3. Copy the prompt "Where do I start?" into a new chat.

Choose the strongest model your assistant offers. Small and fast models make more mistakes with numbers.

For better answers, create a project in Claude or ChatGPT and paste "Part A: Standing rules" into the project's instructions. After that, a short question such as "How's it going?" is enough.

The assistant only reads your numbers. It changes nothing in Steady.

## The sixteen questions

| No. | Question | Frage |
| --- | --- | --- |
| 1 | Where do I start? | Wo fange ich an? |
| 2 | How's it going? | Wie läuft’s? |
| 3 | Fewer joining or more leaving? | Kommen weniger oder gehen mehr? |
| 4 | When do I lose members? | Wann verliere ich Mitglieder? |
| 5 | Where will I be in a year? | Wo stehe ich in einem Jahr? |
| 6 | What did the campaign bring? | Was hat die Kampagne gebracht? |
| 7 | Do they stay? | Bleiben sie? |
| 8 | Is that a lot or a little? | Ist das viel oder wenig? |
| 9 | Should I change my price? | Soll ich meinen Preis ändern? |
| 10 | The numbers for pros | Die Zahlen für Profis |
| 11 | The dashboard | Das Dashboard |
| 12 | The full analysis | Die volle Analyse |
| 13 | Which posts bring members? | Welche Beiträge bringen Mitglieder? |
| 14 | How is my newsletter doing? | Wie kommt mein Newsletter an? |
| 15 | Do free readers start paying? | Werden kostenlose Leser:innen zu Zahlenden? |
| 16 | Which topics work? | Welche Themen wirken? |

## If an answer looks wrong

The Steady connector has a feedback tool. Tell your assistant in the same chat: "Send this to Steady as feedback: [what was wrong]." The assistant then writes a short report and sends it to our developers. Steady sees which publication the report comes from. Nothing changes in your publication. You get no reply to this feedback.

If you want a reply, write to support@steadyhq.com. Say which question you asked, which assistant you used, what you expected and what you got. A screenshot helps.

## Changes

- 0.5, 9 October 2026: "The dashboard" builds a live dashboard where the app can: in Claude, an artifact of the type "Dashboard" that fetches fresh numbers through your own Steady connection each time you open it. New charts for the change in revenue by kind, the newsletter open rate and the posts that brought members.
- 0.4, 9 October 2026: Steady now splits member numbers into paying members, guests and bundle members over time, so the estimate from daily revenue is gone. Monthly values in place of daily ones, and fewer calls. Four new questions about posts, the newsletter, free readers and topics. Free readers over time, and revenue split into new memberships, upgrades, price increases, ended memberships and downgrades.
- 0.3, 5 October 2026: one counting rule for paying members in every prompt, also in "How's it going?". One method for projections. A limit of 300 words in place of "one screen". Fewer calls in "When do I lose members?", a plan for the calls in "Where do I start?". Feedback can also go through the feedback tool of the connector.

## Licence

© 2026 Steady Media GmbH. The prompts are licensed under [Creative Commons Attribution 4.0 International (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/). You may copy, change and share them, also commercially, if you name Steady as the source. The full text is in the file [LICENSE](LICENSE).
