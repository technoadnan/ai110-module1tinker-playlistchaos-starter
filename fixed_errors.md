- installed the streamlit
- Chill keyword match case-sensitive
    - Changed to title.lower() before matching
- Hype ratio always 1.0
    - Changed total to len(all_songs)
- after reloading the song disappears
    - is in-memory only — every page reload wipes it clean, losing any songs the user added.
    - shift the existing songs to a json file 
    - including the new songs 
- lo-fi keyword issue because we have hyphen
    - added a list chill_keywords = ["lofi", "lo-fi", "ambient", "sleep"]
- Search — partial match broken
    - Before: value in q → searched if the song's value was inside the query
    - After: q in value → correctly checks if the query is inside the song's value
   - "ice" now finds "Vanilla Ice"
- Artist name — lost original casing
    - used strip function to remove whitespace only, removed .lower() so "AC/DC" stays as "AC/DC"

- Average energy — wrong songs summed
    - Before: summed only Hype songs' energy but divided by all songs
    - After: sums all songs' energy divided by all songs

- Lucky pick — crash on empty list
    - Before: random.choice([]) crashed with IndexError when no songs in category
    - After: returns None if list is empty, UI shows a warning instead

- Lucky pick "any" mode — excluded Mixed songs
    - Before: only pulled from Hype + Chill
    - After: pulls from Hype + Chill + Mixed

- Add song — no feedback
    - Before: button silently did nothing visible on success or failure
    - After: shows success message on add, warning if title or artist is missing

- Update song — feature missing
    - Before: no way to edit an existing song
    - After: added update sidebar with song picker and editable fields

- Clear history — UI did not refresh
    - Before: cleared the list but page did not visually update
    - After: added st.rerun() so the UI reflects the cleared state immediately

- Merge playlists — mutated original data
    - Before: assigned the original list reference then .extend() corrupted base_playlists
    - After: wrapped in list() to copy first, keeping originals safe

- Favorite genre — always reset to rock on every render
    - Before: selectbox(index=0) hardcoded, ignored the saved profile value
    - After: derives the index from the current profile so it reflects the user's choice