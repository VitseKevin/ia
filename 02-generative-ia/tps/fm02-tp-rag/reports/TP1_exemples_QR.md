# TP 1 · Exemples de questions-réponses

Configuration : `tp1` · chunking markdown 600 car. · top-k 3 · embeddings `BAAI/bge-m3` · LLM `ollama/qwen3:8b` (CPU, Ryzen 7 250)

## Q1. Combien de jours de congés payés acquiert un collaborateur à temps plein ?

Un collaborateur à temps plein acquiert **25 jours ouvrés de congés payés** par période de référence complète [1].

Sources : `01_guide_conges_absences.md`

Latence : 19.9 s

Verdict : **correcte**. Le chiffre (25 jours ouvrés) et la précision « par période de référence complète » correspondent au guide des congés ; la source est citée [1].

## Q2. Quel est le plafond de remboursement d'une nuit d'hôtel à Paris ?

Le plafond de remboursement d'une nuit d'hôtel à Paris est de 150 € [1].

Sources : `04_notes_de_frais.pdf`

Latence : 13.9 s

Verdict : **correcte**. 150 € par nuit à Paris, conforme au tableau des plafonds du PDF : l'extraction pypdf et la suppression des en-têtes/pieds de page répétés conservent bien la ligne du tableau. La réponse aurait pu ajouter « petit-déjeuner inclus ».

## Q3. À quelle heure et où le matériel informatique est-il remis le premier jour ?

Le matériel informatique est remis le premier jour à 9 h 30 au bureau de la DSI, situé au bâtiment A, rez-de-chaussée [1].

Sources : `05_onboarding_it.html`

Latence : 12.1 s

Verdict : **correcte**. Heure et lieu exacts (9 h 30, bureau de la DSI, bâtiment A, rez-de-chaussée) : le nettoyage HTML (menu et pied de page retirés) ne perd pas le contenu utile.

## Q4. Comment signaler un courriel d'hameçonnage ?

Pour signaler un courriel d'hameçonnage, utilisez le bouton « Signaler » de la messagerie [1].

Sources : `03_charte_securite_si.md`, `06_faq_support_it.md`, `05_onboarding_it.html`

Latence : 10.4 s

Verdict : **partielle**. Le bon chunk (section « 6. Signalement des incidents » de la charte sécurité) arrive en 1re position (score 0,688), mais le LLM n'en retient que la dernière phrase. Il omet la procédure : signalement **dans l'heure**, par courriel à securite@orbitale.example ou par un ticket Helpdesk **SEC-2**. Le défaut vient de la génération, pas de la recherche : piste d'amélioration du prompt (demander une réponse complète, procédure en liste).

## Q5. Quelle mutuelle santé Orbitale propose-t-elle à ses salariés ?

Je ne sais pas d'après les documents fournis.

Sources : `02_politique_teletravail.md`, `01_guide_conges_absences.md`, `07_formation_continue.txt`

Latence : 9.5 s

Verdict : **correcte**. Question hors corpus : le modèle applique la règle d'or et répond exactement « Je ne sais pas d'après les documents fournis. » sans inventer de mutuelle, alors que les 3 chunks récupérés (télétravail, congés, formation) sont hors sujet.
