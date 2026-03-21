# Task 2 – Notes Feature Documentation

## 1. Filtering Notes by User

Each note in our application belongs to a specific user via the `user_id` column.
To retrieve all notes for a user, I learned to query the database like this:

```php
$notes = DB::query("SELECT * FROM notes WHERE user_id = 1")->fetchAll();
```

Changing the user_id lets us fetch notes for different users (e.g., user_id = 2 for Kate). This ensures that users can only see their own notes.

## 2. Adding a Notes Navigation Link

I added a link /notes in the navigation bar.

The link becomes active when the URL contains /notes. This improves user experience by visually showing which page is active.

## 3. Registering the Notes Route

I created a route /notes in routes.php.

When a user visits /notes, the NotesController handles the request. The controller queries the database for the user's notes and passes the data to the view. The view displays the notes in HTML, using a foreach loop to list each note.

## 4. Creating a Single Note Page

Each note can be viewed individually via /note?id=ID. I used $_GET['id'] to get the note ID.

**Security:** I used prepared statements to prevent SQL injection. I also added an authorization check to ensure the user owns the note:

```sql
SELECT * FROM notes WHERE id = ? AND user_id = $currentUserId;
```

* If a note doesn't exist → return 404 Not Found.
* If a note exists but belongs to another user → return 403 Forbidden.

## 5. Refactoring Database Fetch

I improved the code by:

* Returning a Database instance instead of PDO directly.
* Adding a fetch() method to get query results cleanly.
* Creating findOrFail() to fetch a record or abort with 404 if not found.
* Introducing an authorize() helper to centralize authorization logic (403 if unauthorized).
* Renaming fetchAll() to get() for clarity.

## 6. Creating and Styling Notes

* Wrapped notes in an unordered list in the view.
* Added a “Create Note” link and styled it using CSS/Tailwind to be blue and underlined on hover.
* Created a separate view note_create.view.php with a form to add new notes.

## 7. Handling Form Submission

* Changed the form method to POST because creating notes modifies data.
* Accessed form data via $_POST['body'].
* Used prepared statements to safely insert notes into the database.
* Escaped output using htmlspecialchars() to prevent XSS attacks.

## 8. Validation

* Added server-side validation before inserting notes:

  * Ensure note body is not empty.
  * Limit length: 1–1000 characters.
  * Used $_POST['body'] ?? '' to preserve input after validation fails.
* Later, extracted validation logic into a Validator class:

  * Static methods like Validator::validateString($value, $min, $max).
  * Can validate emails, usernames, passwords, URLs.
* **Benefits:**

  * Cleaner controller code.
  * Reusable validation across the project.
  * Easy to maintain and extend.

## 9. Summary of Process

* Added /notes route and navigation link.
* Fetched notes by user using secure queries.
* Created single-note view with authorization and error handling (403/404).
* Built a form for creating notes and implemented POST submission.
* Escaped outputs to prevent XSS.
* Implemented validation and later moved it to a reusable Validator class.
* Refactored code to make it clean, readable, and reusable.

This documentation reflects my understanding and personal implementation of the concepts from the video tutorial.
