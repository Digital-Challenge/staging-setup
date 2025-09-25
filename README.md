# Staging Setup Repository

Αυτό είναι ένα **Public Repository** που περιέχει scripts για να αρχικοποιούμε ένα **staging site** σε περιβάλλον WordPress/WooCommerce μέσω SSH.

## Τι κάνει το script

Το script αυτό έχει σχεδιαστεί για να αυτοματοποιεί τη διαδικασία δημιουργίας ενός "staging" περιβάλλοντος. Αναλαμβάνει όλες τις παρακάτω ενέργειες:

*   **Ενεργοποίηση "Coming Soon"**: Θέτει το site σε κατάσταση "Coming Soon" μέσω της λειτουργίας του WooCommerce.
*   **Αποτροπή Ευρετηρίασης**: Αποθαρρύνει τις μηχανές αναζήτησης από το να ευρετηριάσουν το staging site (no-index).
*   **Ενεργοποίηση Debugging**: Ενεργοποιεί τις σταθερές `WP_DEBUG` και `WP_DEBUG_LOG` στο αρχείο `wp-config.php` για ευκολότερη αποσφαλμάτωση.
*   **Απενεργοποίηση Plugins**: Απενεργοποιεί μια προκαθορισμένη λίστα από plugins που συνήθως δεν χρειάζονται σε staging περιβάλλον (π.χ. caching, import/export, tracking pixels, XML feeds).
*   **Απενεργοποίηση Custom Admin Monitors**: Διαγράφει ρυθμίσεις από το plugin "Custom Admin" που παρακολουθούν feeds ή imports.
*   **Διακοπή Συγχρονισμού ERP**: Απενεργοποιεί τον αυτόματο συγχρονισμό παραγγελιών με συστήματα ERP.
*   **Αλλαγή Email Διαχειριστή**: Αλλάζει το email του διαχειριστή του WordPress.
*   **Αλλαγή Email Παραληπτών WooCommerce**: Αλλάζει τον παραλήπτη για όλα τα email ειδοποιήσεων του WooCommerce στο email του διαχειριστή.

## Προαπαιτούμενα

- Πρόσβαση SSH στον server.
- Δικαιώματα `root` ή `sudo` για τον χρήστη που θα εκτελέσει το script.
- `wget` εγκατεστημένο στον server.
- Το site πρέπει να είναι WordPress.

## Οδηγίες Χρήσης

Για να εκτελέσετε το script, συνδεθείτε στον server σας μέσω SSH και μεταβείτε στον κεντρικό κατάλογο (root directory) του WordPress site σας. Στη συνέχεια, εκτελέστε τις παρακάτω εντολές:

```bash
# Κατεβάζει το script
wget -q -O staging-setup.sh https://raw.githubusercontent.com/Digital-Challenge/staging-setup/main/staging-setup.sh

# Δίνει δικαιώματα εκτέλεσης
chmod +x staging-setup.sh

# Εκτελεί το script
./staging-setup.sh
```

Το script θα εκτελέσει αυτόματα όλες τις παραπάνω ενέργειες. Μετά την εκτέλεση, το `staging-setup.sh` και το `staging-setup.php` θα διαγραφούν αυτόματα από τον server.

## Παραμετροποίηση

Το script είναι σχεδιασμένο για να λειτουργεί χωρίς παραμέτρους. Ωστόσο, περιέχει κάποιες προκαθορισμένες τιμές που ίσως θέλετε να αλλάξετε.

**Σημαντική Σημείωση:** Το script αλλάζει το email του διαχειριστή στη διεύθυνση `dichadev@gmail.com`. Αν θέλετε να χρησιμοποιήσετε διαφορετικό email, θα πρέπει να επεξεργαστείτε το αρχείο `staging-setup.php` και να αλλάξετε την τιμή στη συνάρτηση `dc_staging_change_admin_email`.

Ομοίως, η λίστα με τα plugins που απενεργοποιούνται βρίσκεται στο ίδιο αρχείο, στη συνάρτηση `dc_staging_deactivate_plugins`.