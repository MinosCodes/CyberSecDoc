# IDOR

An access control vulnerability allowing attackers to bypass authorization and access resources directly by modifying object identifiers.

## Definition

IDOR (Insecure Direct Object Reference) is an access control vulnerability where applications expose direct references to objects (like user IDs, file IDs, or database records) without proper authorization checks. Attackers can modify these identifiers to access unauthorized data.

## Why It Matters

IDOR allows attackers to access sensitive information belonging to other users by simply changing ID values in URLs or API calls. It's a critical vulnerability because the attack requires minimal effort—just incrementing or guessing IDs—yet can expose highly sensitive data.

## Notes

- Changing ID values in URLs (e.g., `http://website.com/profile?user_id=1000`) can reveal sensitive information accessible only to authorized users.
- Base64 is the standard encoding technique for passing data between pages; encoded IDs still reveal patterns.
- Hashed IDs are safer and harder to crack. Use crackstation.net to attempt hash lookups.
- Unpredictable IDs (random, long strings) make direct object reference attacks much harder.
- Parameter mining involves identifying the parameter used to display users (e.g., `/user/information?uID=33`).
- Test endpoints and JSON responses for direct object references that might be exploitable.