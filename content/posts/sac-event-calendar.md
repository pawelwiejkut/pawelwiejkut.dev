---
title: "SAC Event Calendar"
date: 2024-10-26T21:03:40+01:00
tags: ["SAC","custom widget","calendar","event"]
editPost:
    URL: "https://github.com/pawelwiejkut/pawelwiejkut.dev/tree/main/content"
    Text: "Suggest Changes" # edit text
    appendFilePath: true # to append file path to Edit link
---

Today I would like to share with you my new development - custom widgets calendar event for SAC. This is an idea of how custom widgets can be used beyond creating a graph showing numbers.

{{<figure align=center src="/sac_event_calendar/1.png"  width="70%" >}}

Project premise: To create a calendar that would be able to show up to 4 events per day. The events could last for several days, or they could go between weeks or months. Each event can contain its own description. Potentially, using the widget you can present, for example, a production calendar.

## Installation

1. [Download latest zip release](https://github.com/pawelwiejkut/sac_event_calendar/releases/tag/latest)
2. Extract only event_calendar.json, and do not remove zip
3. Load event_calendar.json to SAC, and attach downloaded zip file

## License

MIT License, so you can use it for free. Solution is also build without any third party libraries.

## Improvements:

I invite you to test and open pull requests, as well as issue on github:
https://github.com/pawelwiejkut/sac_event_calendar