# Planner Esami – configurazione (circa 10 minuti)

## 1. Firebase (gratuito)
1. Vai su https://console.firebase.google.com → **Aggiungi progetto**.
2. **Build → Authentication → Inizia → Email/Password → Abilita**.
3. **Build → Firestore Database → Crea database** (modalità produzione).
4. Scheda **Regole** di Firestore, incolla e pubblica:
   ```
   rules_version = '2';
   service cloud.firestore {
     match /databases/{db}/documents {
       match /users/{uid} {
         allow read, write: if request.auth != null && request.auth.uid == uid;
       }
     }
   }
   ```
5. **Impostazioni progetto → Le tue app → Web (</>)** → registra l'app e copia l'oggetto `firebaseConfig`.
6. Apri `index.html`, trova `const FIREBASE_CONFIG = null;` e sostituisci `null` con l'oggetto copiato.

## 2. Pubblica i file
Metti l'intera cartella online (serve HTTPS):
- **Netlify Drop**: trascina la cartella su https://app.netlify.com/drop, oppure
- **GitHub Pages**: carica i file in un repository e attiva Pages.

Poi in Firebase: **Authentication → Impostazioni → Domini autorizzati → Aggiungi** il dominio ottenuto (es. `tuosito.netlify.app`).

## 3. Usa l'app
- **PC**: apri il link e accedi (o crea account).
- **Android**: apri il link in Chrome → menu ⋮ → **Installa app**. Accedi con lo stesso account: i dati si sincronizzano.
- Funziona anche offline; i dati si allineano appena torni online.
- Senza configurare Firebase l'app funziona solo in locale (con backup JSON da Impostazioni).
