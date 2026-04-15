---
layout: page
title: User Guide
---

RosterBolt is built for **volunteer coordinators** who run **recurring events** and manage around **20-500 volunteers**. It helps you reduce repetitive admin work by making roster updates, availability checks, service record reviews, and CSV data transfers faster to handle.

RosterBolt is a **single-user, offline desktop app** for fast typists who prefer entering commands directly. It keeps your volunteer list on screen as you work, so you can review the current roster, filtered search results, and command feedback without switching tools.

Use RosterBolt when you need to make roster changes fast: importing a new volunteer list, finding weekend ushers, updating availability after a message, deleting outdated volunteer records, restoring accidental deletions, or exporting a filtered list for follow-up.

* Table of Contents
{:toc}

--------------------------------------------------------------------------------------------------------------------

## Quick start

Follow these steps to open RosterBolt and try a few common tasks.

1. **Install Java 17 or above.**
   If you are using a Mac, use the JDK version recommended in this [Mac Java installation guide](https://se-education.org/guides/tutorials/javaInstallationMac.html).

1. **Check your Java version.**
   * **Windows:** Press `Win + R`, type `cmd`, and press Enter. In the Command Prompt window, type `java -version` and press Enter.
   * **Mac:** Open Terminal, type `java -version`, and press Enter.

   You should see a version number that starts with `17` or higher. If the command is not recognised, or the version is below 17, install the correct Java version before continuing.

1. **Download RosterBolt.**
   Download the latest `.jar` file from the [RosterBolt releases page](https://github.com/AY2526S2-CS2103T-T12-1/tp/releases).

1. **Place the file somewhere easy to find.**
   For example, you can create a folder called `RosterBolt` in your Documents folder and put the `.jar` file there. RosterBolt will save its data inside the folder where the `.jar` file is located.

1. **Open the RosterBolt folder in a terminal.**
   * **Windows:** Open the folder in File Explorer. Click the long path bar at the top of the window, where the folder path is shown. If you are not sure where to click, press `Alt + D`. Type `cmd` and press Enter. This opens Command Prompt already pointed at that folder.
   * **Mac:** Open Terminal, type `cd ` with a space after it, drag the RosterBolt folder into the Terminal window, and press Enter.

1. **Launch RosterBolt.**
   Run this command:

   ```bash
   java -jar RosterBolt.jar
   ```

   If your downloaded file has a different name, use that exact file name after `java -jar`.

1. **Check that the app opened correctly.**
   A RosterBolt window should appear after a few seconds. You should see:
   * a command box near the top where you type commands,
   * a message area below it showing command results, and
   * a volunteer list with sample data so you can practise safely.

   ![RosterBolt main window](images/Ui.png)

1. **Try a few commands.**
   Type each command into the command box and press Enter.

   | Try this | What it does |
   |----------|--------------|
   | `help` | Opens this guide from inside the app. |
   | `list` | Shows all active volunteers. |
   | `find alex` | Shows volunteers matching `alex`. |
   | `add n/Alex Tan p/91234567 e/alex@example.com a/NUS r/Usher nt/Weekend shifts` | Adds a sample volunteer. |
   | `delete 3` | Moves the 3rd volunteer in the current list to the recycle bin. |
   | `bin` | Shows recently deleted volunteers. |
   | `restore 1` | Restores the 1st volunteer shown in the recycle bin. |
   | `clear` | Moves all active volunteers to the recycle bin. Use `bin` and `restore` before exiting if you want the sample data back. |
   | `exit` | Closes RosterBolt. |

1. **When you are ready, continue with the command sections below.**
   The sample data is there for practice. `delete` and `clear` are reversible while RosterBolt is still open because deleted volunteers go to the recycle bin. The recycle bin is cleared when you run `exit`.

--------------------------------------------------------------------------------------------------------------------

## Guided workflows

These short workflows show how the commands fit into real volunteer coordination tasks.

### Fill a shift fairly

**Situation:** You need a few ushers for a Saturday event from 09:00 to 12:00, and you want to start with active volunteers who have not served recently.

1. `list vr asc`
   Shows volunteers with the oldest or missing service records first.

1. `find va/SATURDAY,09:00,12:00 usher`
   Narrows the list to volunteers who are available for that slot and have `usher` in a searchable field such as role, notes, or tags.

1. `edit 3 nt/Asked for Saturday usher shift; awaiting reply`
   Records your follow-up after contacting the 3rd volunteer in the filtered list.

### Update the right volunteer from a short list

**Situation:** A volunteer says they cannot make a last-minute shift, but you only remember their first name.

1. `find m/ss xiaoming`
   Uses substring search to find volunteers whose details contain `xiaoming`.

1. `edit 1 nt/Not available for Orange Parade 26`
   Updates the 1st volunteer in the search results after you confirm it is the right person.

### Repeat nearby searches quickly

**Situation:** You are checking several possible shift timings and do not want to retype almost the same availability search each time.

1. `alias f find`
   Lets you type `f` instead of `find`.

1. `f va/MONDAY,18:00,20:00 logistics`
   Finds logistics volunteers available for that Monday evening slot.

1. `editprev`
   Loads the previous command back into the command box.

1. Change the loaded command to `f va/MONDAY,20:00,22:00 logistics`, then press Enter.
   This checks the next slot without retyping the whole command.

--------------------------------------------------------------------------------------------------------------------

## Features

<div markdown="span" class="alert alert-warning">:exclamation: **Caution:**
If you are using a PDF version of this guide, be careful when copying commands that wrap across multiple lines. The PDF may remove spaces around line breaks. If a pasted command fails unexpectedly, type it manually into RosterBolt.
</div>

<div markdown="block" class="alert alert-info">

**:information_source: Reading command formats**<br>

| Notation | Meaning | Example |
|----------|---------|---------|
| `UPPER_CASE` | Replace this with your own value. | In `add n/NAME`, type something like `add n/John Doe`. |
| `[OPTIONAL]` | You may leave this part out. | `n/NAME [t/TAG]` works as `n/Alex Tan` or `n/Alex Tan t/usher`. |
| `...` | You may repeat this part. | `[t/TAG]...` can be omitted, used once, or used multiple times such as `t/usher t/weekend`. |
| Prefixes such as `n/`, `p/`, `e/` | Tell RosterBolt which field you are entering. | `n/Alex Tan p/91234567` gives the name first, then the phone number. |

Most prefixes can be typed in any order unless a command says otherwise. For example, `add n/Alex Tan p/91234567 e/alex@example.com a/NUS` and `add e/alex@example.com a/NUS n/Alex Tan p/91234567` both provide the same required fields.

Commands that do not use extra information, such as `help`, `exit`, `clear`, `bin`, `aliases`, and `editprev`, ignore accidental text after the command. For example, `help 123` behaves like `help`.

</div>

<div markdown="block" class="alert alert-warning">

**:exclamation: Avoid slash-style abbreviations that look like command fields**

RosterBolt uses short labels ending in `/` to understand fields. For example, `p/` means phone and `nt/` means notes. Because of this, some normal writing with slashes can look like a field label by accident.

Safe examples:

* `nt/Call c/o Mary` works because `c/o` is treated like a common short abbreviation.
* `nt/Can help w/ packing` works because there is a space after `w/`.

Avoid examples like:

* `nt/Ask he/she before assigning`
* `nt/Available m/w/f mornings`
* `a/Block A x/unknown`

These may be rejected because parts such as `he/`, `m/`, or `x/` look like command fields. To avoid this, write the phrase out clearly:

* Use `he or she` instead of `he/she`.
* Use `Mon Wed Fri` instead of `m/w/f`.
* Avoid invented slash labels such as `x/unknown`; put the text in a notes field instead, such as `nt/Unknown extra detail`.
</div>

<a id="field-constraints"></a>
<div markdown="block" class="alert alert-info">

**:information_source: Field value rules**<br>

RosterBolt removes extra spaces from the start and end of a field before checking it. A field is treated as blank if nothing remains after those spaces are removed.

| Field | What you can enter |
|-------|--------------------|
| Name | Letters, numbers, and spaces only. It must start with a letter or number and cannot be blank. |
| Phone | At least 3 digits. It may start with one `+`, for example `+6591234567`. RosterBolt stores phone numbers exactly as typed, so `+6591234567` and `6591234567` are treated as different phone numbers. |
| Email | Must use `local-part@domain`, such as `alex@example.com`. The local part may use letters, numbers, and `+_.-` between alphanumeric chunks. Domain labels may use letters, numbers, and hyphens, and the last label must be at least 2 characters long. |
| Address | Any characters, but it cannot be blank. |
| Tag | Letters and numbers only. It cannot be blank. |
| Role | Any text. A blank role removes the role. |
| Notes | Any text. Blank notes remove the notes. |
| Availability | `DAY,HH:mm,HH:mm`, for example `MONDAY,14:00,17:00`. The day must be a full day name, case-insensitive, and the start time must be before the end time. |
| Volunteer record | `yyyy-MM-ddTHH:mm,yyyy-MM-ddTHH:mm`, for example `2026-03-20T14:00,2026-03-20T17:00`. The start date-time must be before the end date-time. |

</div>

<div markdown="block" class="alert alert-info">

**:information_source: Where commands work**<br>

RosterBolt has two main views: the **active volunteer list** and the **recycle bin**. Some commands behave differently depending on which view you are currently using.

| Command(s) | From the active volunteer list | From the recycle bin |
|------------|--------------------------------|----------------------|
| `add`, `edit`, `delete`, `clear`, `stats` | Works on active volunteers. | Rejected. These commands do not work with deleted volunteers. |
| `restore` | Rejected. | Restores volunteers from the recycle bin. |
| `find` | Searches active volunteers. | Searches deleted volunteers in the recycle bin. |
| `list` | Shows all active volunteers. | Switches back to the active volunteer list. |
| `bin` | Switches to the recycle bin. | Shows all deleted volunteers in the recycle bin. |
| `import` | Imports into the active volunteer list. | Imports into the active volunteer list and switches back there. |
| `export` | Exports the active volunteers currently displayed. | Exports the active volunteer list instead, then switches back there. |
| `help`, `alias`, `aliases`, `unalias`, `editprev`, `exit` | Works. | Works. |

</div>

### Getting help

#### Viewing help : `help`

Use `help` when you want to open this guide from inside RosterBolt.

Format: `help`

Example:
* `help` opens the help window.

![help message](images/helpMessage.png)

### Everyday volunteer management

#### Adding a volunteer: `add`

Adds a new volunteer to your active roster. Use this when someone signs up, joins a new recurring programme, or needs to be recorded before you assign shifts.

Format: `add n/NAME p/PHONE e/EMAIL a/ADDRESS [t/TAG]... [r/ROLE] [nt/NOTES] [va/AVAILABILITY]... [vr/RECORD]...`

| Prefix | Required? | Use it for |
|--------|-----------|------------|
| `n/` | Yes | Volunteer's name. |
| `p/` | Yes | Phone number. |
| `e/` | Yes | Email address. |
| `a/` | Yes | Address or location note. |
| `t/` | No | Tags such as `usher`, `logistics`, or `weekend`. You may use this more than once. |
| `r/` | No | Main volunteer role. |
| `nt/` | No | Coordination notes. |
| `va/` | No | Availability slots. You may use this more than once. |
| `vr/` | No | Past volunteering records. You may use this more than once. |

<div markdown="span" class="alert alert-primary">:bulb: **Tip:**
If a volunteer can help in several ways, capture that in the same command instead of adding it later. For example, use multiple `t/` prefixes for roles like `usher` and `weekend`, and multiple `va/` prefixes if they are free on more than one day.
</div>

What to expect:
* RosterBolt adds the volunteer and shows a success message with the new details.
* If the phone number matches an existing volunteer exactly, or the email matches an existing volunteer case-insensitively, RosterBolt rejects the command as a duplicate.
* See [field value rules](#field-constraints) if a value is rejected.

Examples:
* `add n/John Doe p/98765432 e/johnd@example.com a/John street, block 123, #01-01 r/Usher nt/Weekend only va/MONDAY,14:00,17:00 vr/2026-03-20T14:00,2026-03-20T17:00`
* `add n/Betsy Crowe t/weekend e/betsycrowe@example.com a/Newgate Prison p/1234567 t/logistics r/Logistics nt/Prefers morning shifts va/SATURDAY,09:00,12:00 va/SUNDAY,13:00,16:00`
* `add n/Alex Tan p/91234567 e/alex@example.com a/NUS`

![result after adding a volunteer with role and notes](images/add-role-notes.png)

#### Listing all active volunteers : `list`

Shows all active volunteers, optionally sorted by a field. Use this for a full roster review, or before choosing index-based commands such as `edit` and `delete`.

<a id="listing-all-volunteers--list"></a>
Format: `list [ATTRIBUTE [asc|desc]]`

| Part | Meaning |
|------|---------|
| `ATTRIBUTE` | Optional. Supported values are `name`, `phone`, `email`, `address`, `role`, `tag`, and `vr`. It is case-insensitive. |
| `asc` or `desc` | Optional. Sorts in ascending or descending order. If omitted, RosterBolt uses ascending order. |

Sorting notes:
* `list` without an attribute shows volunteers in the order they were added.
* `phone` is sorted character by character, not numerically. For example, `100` appears before `20`.
* `tag` sorts each volunteer's tags first, then compares the combined tag list. Volunteers with no tags appear first in ascending order.
* `vr` sorts by the end time of each volunteer's most recent service record. Volunteers without records are treated as least recently served, so `list vr asc` is useful when you want to distribute opportunities fairly.

Examples:
* `list` shows all active volunteers in the default order.
* `list name` shows all active volunteers by name from A to Z.
* `list email desc` shows all active volunteers by email in reverse order.
* `list vr asc` shows volunteers who have not served recently first.

#### Editing a volunteer : `edit`

Updates an existing volunteer. Use this when a volunteer changes contact details, tells you new availability, completes a shift, or needs notes added after follow-up.

The `INDEX` is the number shown beside the volunteer in the current list or filtered search results.

Format: `edit INDEX [n/NAME] [p/PHONE] [e/EMAIL] [a/ADDRESS] [r/ROLE] [nt/NOTES] [t/TAG]... [va/AVAILABILITY]... [vr/RECORD]...`

| Part | What it means |
|------|---------------|
| `INDEX` | The volunteer number shown in the current active list or filtered results. |
| `n/`, `p/`, `e/`, `a/` | Replace the volunteer's name, phone, email, or address. |
| `r/`, `nt/` | Replace the volunteer's role or notes. Use `r/` or `nt/` with nothing after it to clear that field. |
| `t/`, `va/`, `vr/` | Replace all existing tags, availability slots, or volunteer records. Use an empty prefix such as `t/` to clear the whole set. |

What to expect:
* You must provide at least one field to update.
* The values you provide replace the existing values for those fields.
* For tags, availabilities, and volunteer records, editing the field replaces the whole set. It does not add to the existing set.
* You can clear all tags, availabilities, records, role, or notes by typing the prefix with nothing after it: `t/`, `va/`, `vr/`, `r/`, or `nt/`.
* Do not mix empty and non-empty tag values in the same command. For example, `edit 1 t/friend t/` is rejected because it asks RosterBolt to both set and clear tags.
* See [field value rules](#field-constraints) if a value is rejected.

Examples:
* `edit 1 p/91234567 e/johndoe@example.com va/MONDAY,18:00,20:00` updates the 1st volunteer's phone, email, and availability.
* `edit 2 n/Betsy Crower t/ va/ vr/` updates the 2nd volunteer's name and clears all tags, availability slots, and volunteer records.
* `edit 3 nt/Called on 14 Apr; can help with registration if needed` replaces the notes for the 3rd volunteer.

<a id="deleting-volunteers--delete"></a>
#### Deleting volunteer(s) : `delete`

Moves one or more active volunteers to the recycle bin. Use this when volunteers leave the organisation or when you need to remove outdated volunteer records after checking the current list.

<div markdown="span" class="alert alert-info">:information_source: **Note:**
`delete` works only from the active volunteer list. Deleted volunteers can be recovered with [`restore`](#restoring-a-deleted-volunteer--restore) before you close RosterBolt.
</div>

Format: `delete INDEX [MORE_INDICES]`

What to expect:
* The indices are the numbers shown beside volunteers in the current list.
* Each index must be a positive integer, such as `1`, `2`, or `3`.
* Duplicate indices are ignored, so `delete 3 3 2` behaves like `delete 3 2`.
* All deleted volunteers are moved to the recycle bin.

Examples:
* `list` followed by `delete 2 3` deletes the 2nd and 3rd volunteers in RosterBolt.
* If Betsy appears as the 1st volunteer after `find Betsy`, `delete 1` deletes Betsy from the filtered results.

![result after deleting multiple volunteers](images/bulk-delete.png)

<a id="clearing-all-active-volunteers--clear"></a>
#### Clearing all active volunteers : `clear`

Moves every active volunteer to the recycle bin at once. Use this only when you want to start over or replace the roster, because it affects the full active list.

<div markdown="span" class="alert alert-warning">:exclamation: **Warning:**
`clear` affects **all active volunteers**, even if you are currently looking at filtered [`find`](#finding-volunteers-by-keyword-find) results. You can use [`bin`](#viewing-recently-deleted-volunteers--bin) and [`restore`](#restoring-a-deleted-volunteer--restore) to recover cleared volunteers only before you close RosterBolt.
</div>

Format: `clear`

What to expect:
* All active volunteers are moved to the recycle bin.
* If you run `clear` after `find Alex`, RosterBolt still clears every active volunteer, not only the filtered results.
* The recycle bin is cleared when you close RosterBolt, so restore accidental deletions before exiting.

Examples:
* [`list`](#listing-all-volunteers--list) followed by `clear` moves every active volunteer into the recycle bin and leaves the active list empty.
* `clear` followed by [`bin`](#viewing-recently-deleted-volunteers--bin) lets you review the cleared volunteers.
* `bin` followed by `clear` is rejected because `clear` works only from the active volunteer list.

<a id="viewing-recently-deleted-volunteers--bin"></a>
#### Viewing recently deleted volunteers : `bin`

Shows the recycle bin for the current RosterBolt session. Use this after [`delete`](#deleting-volunteers--delete) or [`clear`](#clearing-all-active-volunteers--clear) to check what was removed.

Format: `bin`

What to expect:
* Volunteers removed by `delete` or `clear` appear here.
* The recycle bin can contain volunteers with the same phone number or email if they are not completely identical in every field.
* The recycle bin is cleared when you close RosterBolt.

Examples:
* `delete 2` followed by `bin` shows the deleted volunteer.
* `clear` followed by `bin` shows the volunteers removed by `clear`.
* Use [`restore`](#restoring-a-deleted-volunteer--restore) before closing RosterBolt if you want to recover a deleted volunteer.

![Recycle bin view](images/binView.png)

<a id="restoring-a-deleted-volunteer--restore"></a>
#### Restoring deleted volunteer(s) : `restore`

Restores volunteers from the recycle bin into the active volunteer list. Use this when you deleted someone by mistake or cleared the roster too broadly.

Format: `restore INDEX [MORE_INDICES]`

What to expect:
* The restored volunteers are added to the end of the active volunteer list with their original information intact.
* Duplicate indices are ignored.
* RosterBolt rejects the restore if the active list already contains a volunteer with the same phone number or email.
* RosterBolt also rejects the restore if two volunteers in the same `restore` command share the same phone number or email.

Examples:
* `bin` followed by `restore 2 3` restores the 2nd and 3rd volunteers in the recycle bin.
* `bin` followed by `restore 3 3 2` behaves the same as `restore 3 2`.
* `list` followed by `restore 1` is rejected because you must be viewing the recycle bin.

![result for 'restore 1'](images/restoreResult.png)

### Finding and reviewing volunteers

<a id="finding-volunteers-by-keyword-find"></a>
#### Finding volunteers : `find`

Searches the current view for matching volunteers. Use it to find a specific volunteer, build a shortlist for a shift, or review only volunteers who are available at a certain time.

If you are viewing the active volunteer list, `find` searches active volunteers. If you are viewing the recycle bin, `find` searches the recycle bin.

Format: `find [m/MATCH_TYPE] [va/DAY,HH:mm,HH:mm] [SEARCH_TERM [MORE_SEARCH_TERMS]]`

| Part | Required? | Use it for |
|------|-----------|------------|
| `m/MATCH_TYPE` | No | Choosing how text should match. Use `m/kw` for full words, `m/ss` for substrings, or `m/fz` for fuzzy matches. |
| `va/DAY,HH:mm,HH:mm` | No | Filtering for volunteers available for a specific time slot. |
| `SEARCH_TERM` | Required if no `va/` is used | Searching fields such as name, phone, email, address, role, notes, and tags. |
| `MORE_SEARCH_TERMS` | No | Adding more possible text matches. Multiple search terms use `OR` logic. |

<div markdown="span" class="alert alert-primary">:bulb: **Tip:**
Use `m/fz` when you are not sure about spelling, such as names copied from messages or addresses entered inconsistently. Use `m/ss` when you remember only part of a name, phone number, role, or tag.
</div>

Search terms:
* RosterBolt searches name, phone, email, address, role, notes, and tags.
* Search is case-insensitive. For example, `hans` matches `Hans`.
* Multiple search terms use `OR` logic. For example, `find alex david` shows volunteers matching `alex` or `david`.

Match types:
* `m/kw` is the default keyword search. It matches full words only, so `Han` does not match `Hans`.
* `m/ss` is substring search. It matches parts of words, so `Han` matches `Hans`.
* `m/fz` is fuzzy search. It allows small spelling mistakes of up to 2 edits.
* If you use `m/`, you must also provide at least one search term.

Availability filter:
* `va/DAY,HH:mm,HH:mm` returns volunteers whose availability fully covers that time period.
* The volunteer must be available on the same day, start at or before the requested start time, and end at or after the requested end time.

Important ordering rule:
* If you use `m/` or `va/`, put all plain search terms after the prefixes.
  Use `find va/MONDAY,14:00,17:00 alice`, not `find alice va/MONDAY,14:00,17:00`.
* When you combine search terms with `va/`, the search terms use `OR`, and the availability filter is applied as an extra requirement. For example, `find va/MONDAY,14:00,17:00 alice bob` means volunteers matching `alice` or `bob`, who are also available on Monday from 14:00 to 17:00.
* Phone numbers with a `+` prefix are treated differently by match type. `m/kw` treats `+6591234567` as different from `6591234567`, while `m/ss` and `m/fz` can still match the digits.

Examples:
* `find John` returns volunteers with full-word matches for `John`.
* `find alex david` returns volunteers matching `alex` or `david`.
* `find m/ss ali` returns volunteers with `ali` inside any searchable field, such as `Alice` or `logistics`.
* `find m/fz michigan` can match a close spelling such as `michegan`.
* `find va/MONDAY,14:00,17:00` returns volunteers available for that Monday time slot.
* `find va/SATURDAY,09:00,12:00 usher` returns volunteers matching `usher` who are also available for the Saturday slot.

![result for 'find alex david'](images/findAlexDavidResult.png)

![result for substring search](images/find-substring.png)

#### Viewing volunteer statistics : `stats`

Shows text-based charts for the volunteers currently displayed. Use this to review your roster at a glance, such as checking whether roles are balanced or who has the most service records.

If a [`find`](#finding-volunteers-by-keyword-find) filter is active, RosterBolt calculates statistics from the filtered active list. Run [`list`](#listing-all-volunteers--list) first if you want statistics for the full active roster.

Format: `stats CATEGORY`

| Category | What it shows |
|----------|---------------|
| `role` | Percentage breakdown of volunteer roles. Volunteers without a role are shown as `Unassigned`. |
| `record` | Volunteers ranked by the number of volunteer records they have. |

Examples:
* `stats role` shows the role breakdown for the current active list.
* `find va/SATURDAY,09:00,12:00` followed by `stats role` shows role coverage among volunteers available for that slot.
* `stats record` shows who has the most recorded volunteering sessions.

### Productivity features

#### Creating a command alias : `alias`

Creates a short name for a built-in command. Use aliases for commands you type often during coordination, such as `find` or `list`.

Format: `alias SHORT COMMAND_WORD`

Rules:
* `SHORT` must start with a lowercase letter and contain only lowercase letters, numbers, or hyphens.
* `COMMAND_WORD` must be exactly one allowed target command: `add`, `bin`, `clear`, `delete`, `edit`, `exit`, `export`, `find`, `help`, `import`, `list`, `restore`, or `stats`.
* `alias`, `aliases`, `unalias`, and `editprev` cannot be alias targets.
* An alias replaces only the first word you type. Everything after it is kept as-is.
* Aliases are saved in `preferences.json`, not in your volunteer data file.

Examples:
* `alias f find` followed by `f va/MONDAY,14:00,17:00 alice` behaves like [`find`](#finding-volunteers-by-keyword-find) `va/MONDAY,14:00,17:00 alice`.
* `alias ls list` lets you type `ls name` instead of [`list`](#listing-all-volunteers--list) `name`.
* `alias ep editprev` is rejected because `editprev` cannot be an alias target.
* `alias quickadd add n/John Doe` is rejected because the target must be one command word only.

#### Listing command aliases : `aliases`

Shows the aliases you have created. Use this when you forget which shortcuts are available.

Format: `aliases`

Examples:
* With no aliases defined, `aliases` shows `No aliases defined.`.
* `alias ls list` followed by `aliases` includes `ls -> list`.
* `alias f find` followed by `alias ls list`, then `aliases`, shows both aliases sorted by alias name.

#### Removing a command alias : `unalias`

Deletes an alias you no longer want to use.

Format: `unalias SHORT`

Examples:
* `alias ls list` followed by `unalias ls` removes the `ls` shortcut.
* `unalias ls` is rejected with `This alias does not exist.` if `ls` has not been created.

#### Editing the previous command : `editprev`

Loads your last successfully run command back into the command box so you can edit and run a similar command. Use this for repeated searches or long edits.

Format: `editprev`

What to expect:
* RosterBolt remembers only the most recent successful command, excluding `editprev` itself.
* If the remembered command used an alias, RosterBolt recalls the alias exactly as you typed it.
* The recalled command is not run automatically. Edit it first, then press Enter.

Examples:
* [`find`](#finding-volunteers-by-keyword-find) `Betsy` followed by `editprev` loads `find Betsy` back into the command box.
* `alias f find` followed by `f Betsy` and then `editprev` loads `f Betsy`, not `find Betsy`.
* Running `editprev` before any successful command is rejected with `There is no previous command to edit.`

### Data import/export and storage

<a id="importing-volunteers-from-a-csv-file--import"></a>
#### Importing volunteers from a CSV file : `import`

Imports volunteers from a CSV file. Use this when onboarding a batch of volunteers or moving data from a spreadsheet into RosterBolt.

You can run `import` while viewing either the active list or the recycle bin. Imported volunteers are always added to the active volunteer list, and RosterBolt switches back to that list after import.

Format: `import FILE_PATH`

CSV requirements:
* The file must include these headers: `name`, `phone`, `email`, and `address`.
* These headers are optional: `role`, `notes`, `tags`, `availabilities`, and `records`.
* Header names are case-insensitive after trimming spaces.
* File paths with spaces are not supported.
* Standard CSV quoting is supported. If a cell contains commas, put the whole cell in double quotes.
* Multiple tags, availabilities, or records in one cell are separated with semicolons (`;`).
* Blank optional cells are allowed.
* CSV files exported by [`export`](#exporting-volunteers-to-a-csv-file--export) already use the correct format and can be imported back directly.

What to expect:
* If the file cannot be read, import fails.
* If required headers are missing or duplicated, import fails.
* Rows with invalid data are skipped, but valid rows in the same file are still imported.
* Rows that duplicate an existing volunteer, or another row in the same import, are skipped.
* After import, RosterBolt shows how many volunteers were imported, how many duplicate rows were skipped, and how many invalid rows were skipped.

Examples:
* `import data/volunteers.csv`
* If `missing.csv` does not exist, `import missing.csv` is rejected with `Import failed: could not read file missing.csv`.
* If row 4 has an invalid phone number but the rest of the file is valid, RosterBolt imports the valid rows and reports `Invalid row details: 4 (invalid phone)`.

Correct CSV content with quoted structured fields:

```csv
name,phone,email,address,role,notes,tags,availabilities,records
Bob Lim,92345678,bob@example.com,NUS,Usher,Prefers mornings,weekend;usher,"MONDAY,09:00,12:00;SATURDAY,09:00,12:00","2026-04-01T09:00,2026-04-01T12:00"
Alice Tan,91234567,alice@example.com,NUS,Logistics,,logistics,,
```

Incorrect CSV content:

```csv
Bob Lim,92345678,bob@example.com,NUS,Usher,Prefers mornings,weekend,MONDAY,09:00,12:00,2026-04-01T09:00,2026-04-01T12:00
```

The incorrect row is likely to be read as too many CSV columns because the structured fields contain unquoted commas.

<a id="exporting-volunteers-to-a-csv-file--export"></a>
#### Exporting volunteers to a CSV file : `export`

Exports active volunteer data to a CSV file. Use this to make a backup, share a shortlist, or continue working with the data in Excel or Google Sheets.

Format: `export FILE_PATH`

What gets exported:
* If you are viewing the active volunteer list, RosterBolt exports the volunteers currently displayed. This means active [`find`](#finding-volunteers-by-keyword-find) filters are respected.
* If you are viewing the full unfiltered list, RosterBolt exports all active volunteers.
* Deleted volunteers are never exported.
* If you run `export` while viewing the recycle bin, RosterBolt exports the active volunteer list instead and switches back to it.

<div markdown="span" class="alert alert-info">:information_source: **Note:**
If the requested file already exists, RosterBolt creates a new filename instead of overwriting it. This is why you may see an exported file with a timestamp and short random code in its name.
</div>

File rules:
* Exactly one file path must be provided.
* File paths with spaces are not supported.
* If parent folders in the file path do not exist, RosterBolt creates them.
* If the requested file already exists, RosterBolt does not overwrite it. It creates a new filename beside it, such as `data/volunteers-20260413T153045-1a2b3c4d.csv`.

Examples:
* `export backups/event-a.csv` exports the currently displayed active volunteers into the `backups` folder.
* [`find`](#finding-volunteers-by-keyword-find) `va/SATURDAY,09:00,12:00 usher` followed by `export exports/saturday-ushers.csv` exports only the filtered shortlist.
* `export data/volunteers.csv` creates `data/volunteers.csv` if it does not exist. If it already exists, RosterBolt creates a derived filename instead of overwriting it.

#### Saving the data

RosterBolt saves your volunteer data automatically whenever you make a change. You do not need to save manually.

If a command runs successfully but RosterBolt cannot save to disk, for example because of a file permissions issue, you will see the command's success message together with a warning that the changes were not saved and will be lost if you close the app. You can also use [`export`](#exporting-volunteers-to-a-csv-file--export) to create a CSV backup.

#### Editing the data file

RosterBolt stores your volunteer data as a JSON file at `[JAR file location]/data/rosterbolt.json`.

Only edit this file directly if you are comfortable working with JSON.

<div markdown="span" class="alert alert-warning">:exclamation: **Caution:**
If your edits make the file invalid, RosterBolt discards all data and starts with an empty file on the next launch. Back up the file before editing it manually. Values outside the accepted field rules can also cause unexpected behaviour.
</div>

#### Exiting the program : `exit`

Closes RosterBolt. Your active volunteer data is saved automatically, but the recycle bin is cleared.

Format: `exit`

Examples:
* `exit` closes RosterBolt after saving active volunteer data.
* If you have accidentally deleted a volunteer, [`restore`](#restoring-a-deleted-volunteer--restore) them before running `exit`.

--------------------------------------------------------------------------------------------------------------------

## FAQ

**Q**: How do I transfer my data to another computer?<br>
**A**: Install RosterBolt on the other computer, then copy the data file from your old RosterBolt home folder and use it to replace the empty data file in the new installation.

**Q**: Where is my volunteer data stored?<br>
**A**: RosterBolt stores your volunteer data at `[JAR file location]/data/rosterbolt.json`.

**Q**: Do I need to save manually?<br>
**A**: No. RosterBolt saves automatically whenever a command changes your volunteer data. If saving fails, RosterBolt shows a warning.

**Q**: Can I undo `delete` or `clear`?<br>
**A**: Yes, but only before you close RosterBolt. Deleted volunteers go to the recycle bin, where you can use `restore`. The recycle bin is cleared when you run `exit` or close the app.

**Q**: Why did `restore` fail?<br>
**A**: RosterBolt blocks a restore if the active volunteer list already has someone with the same phone number or email, or if you try to restore two volunteers with the same phone number or email in one command.

**Q**: Why did `find 6591234567` not match a phone number stored as `+6591234567`?<br>
**A**: Keyword search treats `+6591234567` as different from `6591234567`. Use substring search instead: `find m/ss 6591234567`.

**Q**: How do I record more than one availability slot for a volunteer?<br>
**A**: Use `va/` more than once, for example `va/MONDAY,09:00,12:00 va/SATURDAY,14:00,17:00`.

**Q**: Why did `export data/volunteers.csv` create a file with a longer name?<br>
**A**: RosterBolt does not overwrite an existing export file. If `data/volunteers.csv` already exists, it creates a derived filename such as `data/volunteers-20260413T153045-1a2b3c4d.csv`.

**Q**: Can multiple coordinators edit the same RosterBolt data file at the same time?<br>
**A**: No. RosterBolt is designed as a single-user offline app. Export the roster if you need to share a copy with someone else.

--------------------------------------------------------------------------------------------------------------------

## Known issues

1. **When using multiple screens**, if you move the application to a secondary screen, and later switch to using only the primary screen, the GUI opens off-screen. The remedy is to delete the `preferences.json` file created by the application before running the application again.
2. **If you minimize the Help Window** and then run the `help` command (or use the `Help` menu, or the keyboard shortcut `F1`) again, the original Help Window will remain minimized, and no new Help Window will appear. The remedy is to manually restore the minimized Help Window.

--------------------------------------------------------------------------------------------------------------------

## Command summary

<!-- The `list` row uses a Unicode fullwidth vertical bar (U+FF5C: ｜) instead of ASCII pipe (|) to avoid breaking the Markdown table. -->

### Everyday volunteer management

Action | Format, Example
--------|----------------
**Add** | `add n/NAME p/PHONE e/EMAIL a/ADDRESS [t/TAG]... [r/ROLE] [nt/NOTES] [va/AVAILABILITY]... [vr/RECORD]...` <br> e.g., `add n/James Ho p/22224444 e/jamesho@example.com a/123, Clementi Rd, 1234665 t/weekend r/Usher nt/Available weekends va/SUNDAY,14:00,17:00 vr/2026-03-20T14:00,2026-03-20T17:00`
**List** | `list [ATTRIBUTE [asc｜desc]]`<br> e.g., `list name desc`, `list vr asc`
**Edit** | `edit INDEX [n/NAME] [p/PHONE] [e/EMAIL] [a/ADDRESS] [r/ROLE] [nt/NOTES] [t/TAG]... [va/AVAILABILITY]... [vr/RECORD]...`<br> e.g., `edit 2 n/James Lee e/jameslee@example.com va/MONDAY,14:00,17:00`
**Delete** | `delete INDEX [MORE_INDICES]`<br> e.g., `delete 2 3`
**Clear** | `clear`
**Bin** | `bin`
**Restore** | `restore INDEX [MORE_INDICES]`<br> e.g., `restore 2 3`

### Finding and reviewing volunteers

Action | Format, Example
--------|----------------
**Find** | `find [m/MATCH_TYPE] [va/DAY,HH:mm,HH:mm] [SEARCH_TERM [MORE_SEARCH_TERMS]]`<br> e.g., `find m/kw James Jake`, `find m/ss ali`, `find m/fz michigan`, `find va/MONDAY,14:00,17:00`, `find va/MONDAY,14:00,17:00 alice`
**Stats** | `stats CATEGORY`<br> e.g., `stats role`, `stats record`

### Productivity features

Action | Format, Example
--------|----------------
**Alias** | `alias SHORT COMMAND_WORD`<br> e.g., `alias f find`
**Aliases** | `aliases`
**Unalias** | `unalias SHORT`<br> e.g., `unalias f`
**Edit Previous** | `editprev`

### Data import/export and app control

Action | Format, Example
--------|----------------
**Import** | `import FILE_PATH`<br> e.g., `import data/volunteers.csv`
**Export** | `export FILE_PATH`<br> e.g., `export data/volunteers.csv`
**Help** | `help`
**Exit** | `exit`
