# Schéma de la base de données (SQLite, chiffrée via SQLCipher)

Schéma complet, toutes phases confondues. En M0–M1, seules les tables utilisées sont remplies.

```sql
CREATE TABLE compte_connexion (
  id TEXT PRIMARY KEY,
  type TEXT NOT NULL,            -- gmail | outlook | imap | gdrive | dropbox | kdrive | pcloud | mega | proton | webdav | local
  libelle TEXT,
  email TEXT,
  tokens_chiffres TEXT,          -- JSON chiffré via safeStorage (jamais en clair)
  actif INTEGER DEFAULT 1,
  cree_le TEXT NOT NULL
);

CREATE TABLE client (
  id TEXT PRIMARY KEY,
  nom TEXT NOT NULL,
  emails TEXT,                   -- JSON
  telephone TEXT,
  couleur TEXT
);

CREATE TABLE projet (
  id TEXT PRIMARY KEY,
  client_id TEXT REFERENCES client(id),
  nom TEXT NOT NULL,
  taux_horaire REAL,
  couleur TEXT,
  dossier_racine TEXT            -- chemin dans le stockage (cloud ou local)
);

CREATE TABLE tag (
  id TEXT PRIMARY KEY,
  libelle TEXT UNIQUE NOT NULL,
  couleur TEXT
);

CREATE TABLE fichier (
  id TEXT PRIMARY KEY,
  nom TEXT NOT NULL,
  nom_normalise TEXT,
  hash_sha256 TEXT,
  taille INTEGER,
  mime TEXT,
  extension TEXT,
  source TEXT,                   -- mail | chat | upload | manuel
  source_ref TEXT,               -- id du message d'origine
  expediteur TEXT,
  projet_id TEXT REFERENCES projet(id),
  client_id TEXT REFERENCES client(id),
  chemin_distant TEXT,
  statut TEXT DEFAULT 'a_classer',  -- a_classer | classe | archive | corbeille
  confiance INTEGER,
  date_reception TEXT,
  date_classement TEXT
);

CREATE TABLE fichier_tag (
  fichier_id TEXT REFERENCES fichier(id),
  tag_id TEXT REFERENCES tag(id),
  PRIMARY KEY (fichier_id, tag_id)
);

CREATE TABLE message (
  id TEXT PRIMARY KEY,
  compte_id TEXT REFERENCES compte_connexion(id),
  message_id_distant TEXT,
  expediteur TEXT,
  destinataires TEXT,            -- JSON
  objet TEXT,
  extrait TEXT,
  date TEXT,
  lu INTEGER DEFAULT 0,
  a_pj INTEGER DEFAULT 0,
  projet_id TEXT REFERENCES projet(id),
  client_id TEXT REFERENCES client(id)
);

CREATE TABLE suggestion (
  id TEXT PRIMARY KEY,
  fichier_id TEXT REFERENCES fichier(id),
  dossier_cible TEXT,
  tags TEXT,                     -- JSON
  score INTEGER,
  statut TEXT DEFAULT 'en_attente',  -- en_attente | validee | modifiee | ignoree
  cree_le TEXT NOT NULL
);

CREATE TABLE regle (
  id TEXT PRIMARY KEY,
  type TEXT NOT NULL,            -- expediteur | mot_cle | extension | domaine
  cle TEXT NOT NULL,
  dossier_cible TEXT,
  tags TEXT,                     -- JSON
  confiance INTEGER,
  active INTEGER DEFAULT 1
);

CREATE TABLE tache (
  id TEXT PRIMARY KEY,
  projet_id TEXT REFERENCES projet(id),
  client_id TEXT REFERENCES client(id),
  libelle TEXT NOT NULL,
  fait INTEGER DEFAULT 0,
  echeance TEXT,
  ordre INTEGER DEFAULT 0,
  cree_le TEXT NOT NULL,
  fichier_id TEXT REFERENCES fichier(id),
  message_id TEXT REFERENCES message(id),
  note_id TEXT,
  reunion_id TEXT
);

CREATE TABLE commentaire (
  id TEXT PRIMARY KEY,
  cible_type TEXT NOT NULL,      -- fichier | note
  cible_id TEXT NOT NULL,
  auteur TEXT,
  date TEXT,
  texte TEXT
);

CREATE TABLE reunion (
  id TEXT PRIMARY KEY,
  projet_id TEXT REFERENCES projet(id),
  date TEXT,
  duree_secondes INTEGER,
  participants TEXT,             -- JSON
  compte_rendu TEXT
);

CREATE TABLE note (
  id TEXT PRIMARY KEY,
  reunion_id TEXT REFERENCES reunion(id),
  horodatage TEXT,
  texte TEXT,
  fichier_md TEXT                -- chemin du fichier Markdown (base de connaissances)
);

CREATE TABLE lien (
  id TEXT PRIMARY KEY,
  note_id TEXT REFERENCES note(id),
  cible_type TEXT NOT NULL,      -- note | projet | client | fichier
  cible_id TEXT NOT NULL
);

CREATE TABLE temps (
  id TEXT PRIMARY KEY,
  projet_id TEXT REFERENCES projet(id),
  tache_id TEXT REFERENCES tache(id),
  debut TEXT,
  fin TEXT,
  duree_secondes INTEGER,
  facturable INTEGER DEFAULT 1
);

CREATE TABLE facture (
  id TEXT PRIMARY KEY,
  numero TEXT UNIQUE,
  type TEXT NOT NULL,            -- devis | facture
  projet_id TEXT REFERENCES projet(id),
  client_id TEXT REFERENCES client(id),
  date_emission TEXT,
  date_echeance TEXT,
  statut TEXT DEFAULT 'brouillon',  -- brouillon | envoye | paye | en_retard
  total_ht REAL,
  tva REAL,
  total_ttc REAL,
  relances TEXT,                 -- JSON (dates/niveaux de relance)
  fichier_pdf TEXT
);

CREATE TABLE sync_meta (
  cle TEXT PRIMARY KEY,          -- ex: hash_fichier_sync, dernier_sync
  valeur TEXT
);
```
