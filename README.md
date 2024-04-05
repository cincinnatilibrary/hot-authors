# Hot Authors / Hot Tickets Program Workflow

## Patron Perspective

### Subscription Sign-up
- Patrons log into their library account through the library's website or visit the library in person.
- They navigate to the "Hot Authors" / "Hot Tickets" program section.
- They select their preferred authors or genres from a list. Each author and genre is associated with a unique ID. For example, Dan Brown could be ID `6`.
- Patrons select their preferred format (regular print, large print, eAudio, eBook) for each subscription.
- Upon submission, the system generates a unique subscription ID for each selection, which ties together the author/genre ID, patron ID, and format preference.

### Managing Subscriptions
- Patrons can view their current subscriptions, including author/genre, format, and unique subscription ID, through their account.
- They have the option to add new subscriptions, change format preferences, or cancel subscriptions.

## Staff Perspective

### Cataloging New Items
- **Initial Cataloging:**
  - When new titles are added to the library catalog, staff includes a note field in the bibliographic record (TODO: specify a field -- 590 subfield a? 950 subfield a?) with the format `ha-[Author/Genre ID]`. This ID corresponds to the subscription IDs for authors or genres.
  - For example, a new Dan Brown book would have a note field `ha-6`.
- **Suppressing Records:**
  - Initially, the bibliographic records are cataloged in a "suppressed" state, meaning they are not yet visible to the general public in the library’s online catalog. This allows the automated system to process the new arrivals and match them with "Hot Authors" / "Hot Tickets" subscriptions before general availability.

### Automated Matching Script
- **Identifying Matches:**
  - An automated script runs daily, scanning the bibliographic records for note fields (TODO: use the filed noted above) that match the regular expression pattern indicative of "Hot Authors" / "Hot Tickets" subscriptions.
  - The script extracts the ID from the note field and matches it against the list of active subscriptions, taking into account the format preferences of each subscription -- indicated by the format assigned in the bibliographic record.
- **Placing Holds:**
  - Once a match is found, the script gathers the list of patrons matching that subscription and format type, randomizes the list, and automatically places a bib-level hold for the title on behalf of the patrons. For eaudio and ebook titles -- a different workflow is needed depending on the vendor supplying the e-resource.
- **Unsuppressing Records:**
  - After processing for subscriptions is complete, the script changes the bibliographic records from "suppressed" to "unsuppressed." This change makes the records fully discoverable in the public access catalog by all patrons, enhancing visibility and access.

### Notification and Fulfillment
- Logs are generated of every hold that has been placed, or has failed to place. Logs are used for assessment and troubleshooting purposes.
- TODO: ? Patrons receive notifications (email, SMS, etc.) when a hold is automatically placed for them, including details about the item and expected availability.
- TODO: ? A specific Stat Group is assigned to each hold so that it can be used in future assessments.
---
